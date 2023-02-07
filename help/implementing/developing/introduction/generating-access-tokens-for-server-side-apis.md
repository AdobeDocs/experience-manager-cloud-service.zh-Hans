---
title: 为服务器端 API 生成访问令牌
description: 了解如何通过生成安全的JWT令牌来促进第三方服务器与AEMas a Cloud Service之间的通信
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: 9f7157be1a9e7b635b9c7d0f0c653646e6f1b43b
workflow-type: tm+mt
source-wordcount: '2132'
ht-degree: 1%

---

# 为服务器端 API 生成访问令牌 {#generating-access-tokens-for-server-side-apis}

某些架构依赖于从AEM基础架构外的服务器上托管的应用程序as a Cloud Service调用AEM。 例如，一个移动设备应用程序，它调用服务器，然后向AEM发出API请求as a Cloud Service。

服务器到服务器的流程以及简化的开发流程如下所述。 AEMas a Cloud Service [开发人员控制台](development-guidelines.md#crxde-lite-and-developer-console) 用于生成身份验证过程所需的令牌。

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## 服务器到服务器流 {#the-server-to-server-flow}

具有IMS组织管理员角色的用户(也是AEM作者上的AEM用户或AEM管理员产品配置文件的成员)可以生成一组AEMas a Cloud Service凭据，每个凭据都是JSON有效负载，其中包含证书（公钥）、私钥和由 `clientId` 和 `clientSecret`. 这些凭据随后可由具有AEMas a Cloud Service环境管理员角色的用户检索，并应安装在非AEM服务器上，并谨慎地作为密钥处理。 此JSON格式文件包含与AEMas a Cloud ServiceAPI集成所需的所有数据。 该数据用于创建已签名的JWT令牌，该令牌与AdobeIdentity Management服务(IMS)交换，以获取IMS访问令牌。 然后，此访问令牌可用作承载身份验证令牌，以向AEMas a Cloud Service发出请求。 默认情况下，凭据中的证书将在一年后过期，但可以根据需要刷新，如所述 [此处](#refresh-credentials).

服务器到服务器流程涉及以下步骤：

* 从开发人员控制台获取AEMas a Cloud Service凭据
* 在对AEM进行调用的非AEM服务器上安装AEMas a Cloud Service凭据
* 使用Adobe的IMS API生成JWT令牌并交换该令牌以用于访问令牌
* 使用访问令牌作为载体身份验证令牌调用AEM API
* 在AEM环境中为技术帐户用户设置适当的权限

### 获取AEMas a Cloud Service凭据 {#fetch-the-aem-as-a-cloud-service-credentials}

有权访问AEMas a Cloud Service开发人员控制台的用户将在开发人员控制台中看到给定环境的集成选项卡。 具有AEMas a Cloud Service环境管理员角色的用户可以创建、查看或管理凭据。

单击 **创建新技术帐户** 按钮，将创建一组新的凭据，其中包括客户端id、客户端密钥、私钥、证书，以及环境创作层和发布层的配置，而不考虑面板选择。

![创建新技术帐户](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

将打开一个新的浏览器选项卡，显示凭据。 您可以使用此视图通过按状态标题旁边的下载图标来下载凭据：

![下载凭据](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

创建凭据后，这些凭据将显示在 **技术帐户** 选项卡 **集成** 部分：

![查看凭据](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

用户稍后可以使用查看操作查看凭据。 此外，如文章后面所述，对于需要续订或吊销证书的情况，用户可以通过创建新的私钥或证书来修改同一技术帐户的凭据。

具有AEMas a Cloud Service环境管理员角色的用户稍后可以为其他技术帐户创建新凭据。 当不同的API具有不同的访问要求时，此功能非常有用。 例如，读和读。

>[!NOTE]
>
>客户最多可以创建10个技术帐户，包括已删除的帐户。

>[!IMPORTANT]
>
>IMS组织管理员（通常是通过Cloud Manager配置环境的同一用户）(也应是AEM作者上AEM用户或AEM管理员产品配置文件的成员)必须先访问开发人员控制台并单击 **创建新技术帐户** 按钮，以便具有AEMas a Cloud Service环境的管理员权限的用户生成并稍后检索凭据。 如果IMS组织管理员尚未执行此操作，则会显示一条消息，告知他们需要IMS组织管理员角色。

### 在非AEM服务器上安装AEM服务凭据 {#install-the-aem-service-credentials-on-a-non-aem-server}

调用AEM的应用程序应能够访问AEMas a Cloud Service凭据，并将其视为机密。

### 生成JWT令牌并将其交换为访问令牌 {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

在对AdobeIMS服务的调用中，使用凭据创建JWT令牌，以检索有效期为24小时的访问令牌。

可以使用为此目的而设计的客户端库将AEM CS服务凭据交换为访问令牌。 客户端库可从 [Adobe的公共GitHub存储库](https://github.com/adobe/aemcs-api-client-lib)，其中包含更多详细信息和最新信息。

```
/*jshint node:true */
"use strict";

const fs = require('fs');
const exchange = require("@adobe/aemcs-api-client-lib");

const jsonfile = "aemcs-service-credentials.json";

var config = JSON.parse(fs.readFileSync(jsonfile, 'utf8'));
exchange(config).then(accessToken => {
    // output the access token in json form including when it will expire.
    console.log(JSON.stringify(accessToken,null,2));
}).catch(e => {
    console.log("Failed to exchange for access token ",e);
});
```

可以使用能够生成具有正确格式的签名JWT令牌并调用IMS令牌交换API的任何语言来执行相同的交换。

访问令牌将定义其过期的时间（通常为24小时）。 Git存储库中有一个示例代码，用于管理访问令牌并在其过期之前刷新该令牌。

>[!NOTE]
>如果有多个凭据，请确保为AEM的API调用引用相应的json文件，该文件稍后将会调用。

### 调用AEM API {#calling-the-aem-api}

对AEMas a Cloud Service环境进行相应的服务器到服务器API调用，包括标头中的访问令牌。 因此，对于“授权”标头，请使用值 `"Bearer <access_token>"`. 例如，使用 `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在AEM中为技术帐户用户设置适当的权限 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

首先，需要在Adobe Admin Console中创建新的产品用户档案。 您可以按照以下步骤来实现此目的：

1. 前往Adobe Admin Console，地址为 [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/)
1. 按 **管理** 链接 **产品和服务** 列。
1. 选择 **AEMas a Cloud Service**
1. 按 **新建用户档案** 按钮

   ![新配置文件](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. 命名配置文件并按 **保存**

   ![保存配置文件](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. 从用户档案列表中选择之前创建的用户档案
1. 按 **添加用户** 按钮

   ![添加用户](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. 添加您刚刚创建的技术帐户(在本例中为 `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`)和按 **保存**

   ![添加技术帐户](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. 等待10分钟，以使更改生效，并对AEM进行API调用，并使用从新凭据生成的访问令牌。 作为cURL命令，它将表示为与以下示例类似：

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


进行API调用后，产品配置文件将在AEMas a Cloud Service创作实例中显示为用户组，并且相应的技术帐户将作为该组的成员。

要检查此内容，您需要：

1. 登录创作实例
1. 转到 **工具** - **安全性** ，然后单击 **群组** 卡片
1. 在组列表中找到您创建的配置文件的名称，然后单击该名称：

   ![组配置文件](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. 在以下窗口中，切换到 **成员** 选项卡，并检查技术帐户是否正确列在此处：

   ![“成员”选项卡](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


或者，您也可以对创作实例执行以下步骤，以验证技术帐户是否显示在用户列表中：

1. 转到 **工具** - **安全性** - **用户**
1. 检查您的技术帐户是否为用户列表，然后单击
1. 单击 **群组** 选项卡，以验证用户是否属于与您的产品配置文件对应的群组。 此用户还是少数几个其他组的成员，包括参与者：

   ![组成员资格](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>在2023年年中之前，在创建多个凭据之前，客户在Adobe管理控制台中没有被指导创建产品配置文件，因此技术帐户没有与AEMas a Cloud Service实例中的“参与者”以外的组关联。 为保持一致性，建议为此技术帐户在Adobe Admin Console中创建新产品用户档案，并将现有技术帐户添加到该组。

<u>**设置相应的群组权限**</u>

最后，为组配置所需的适当权限，以正确调用或锁定您的API。 您可以通过以下方式执行此操作：

1. 登录到相应的创作实例，然后转到 **设置** - **安全性** - **权限**
1. 在左侧窗格中搜索与产品配置文件对应的组名称（在本例中为只读API），然后单击该组：

   ![搜索群组](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. 在以下窗口中单击编辑按钮：

   ![编辑权限](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. 正确修改权限，然后单击 **保存**

   ![确认编辑权限](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>通过咨询以下网站，进一步了解AdobeIdentity Management系统(IMS)和AEM用户和组 [文档](/help/security/ims-support.md).

## 开发人员流程 {#developer-flow}

开发人员可能希望使用其非AEM应用程序的开发实例（在其笔记本电脑上运行或托管）进行测试，该实例会向AEMas a Cloud Service开发环境发出请求。 但是，由于开发人员不一定具有IMS管理员角色权限，因此我们不能假定他们可以生成常规服务器到服务器流中描述的JWT载体。 因此，我们为开发人员提供了一种机制，用于直接生成访问令牌，该令牌可用于他们有权访问的AEMas a Cloud Service环境的请求。

请参阅 [开发人员准则文档](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) 有关使用AEMas a Cloud Service开发人员控制台所需权限的信息。

>[!NOTE]
>
>本地开发访问令牌的有效期最长为24小时，之后必须使用同一方法重新生成该令牌。

开发人员可以使用此令牌从其非AEM测试应用程序向AEMas a Cloud Service环境进行调用。 通常，开发人员会在自己的笔记本电脑上将此令牌与非AEM应用程序一起使用。 此外，AEM as a Cloud通常是非生产环境。

开发人员流程涉及以下步骤：

* 从开发人员控制台中生成访问令牌
* 使用访问令牌调用AEM应用程序。

开发人员还可以对其本地计算机上运行的AEM项目进行API调用，在这种情况下，不需要访问令牌。

### 生成访问令牌 {#generating-the-access-token}

1. 转到 **本地令牌** 在 **集成**
1. 单击 **获取本地开发令牌** 按钮以生成访问令牌。

### 使用访问令牌调用AEM应用程序 {#call-the-aem-application-with-an-access-token}

从非AEM应用程序向AEMas a Cloud Service环境进行相应的服务器到服务器API调用，包括标头中的访问令牌。 因此，对于“授权”标头，请使用值 `"Bearer <access_token>"`.

## 刷新凭据 {#refresh-credentials}

默认情况下，AEMas a Cloud Service凭据会在一年后过期。 为确保服务连续性，开发人员可以选择刷新凭据，将其可用性延长一年。

要实现此目的，您可以：

* 使用 **添加证书** 按钮 **集成** - **技术帐户** ，如下所示

   ![凭据刷新](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* 按下按钮后，将生成一组包含新证书的凭据。 在AEM外的服务器上安装新凭据，并确保连接正常，而无需删除旧凭据 
* 在生成访问令牌时，请确保使用新凭据而不是旧凭据
* （可选）撤消（然后删除）之前的证书，以便不再能够使用AEMas a Cloud Service进行身份验证。

## 凭据吊销 {#credentials-revocation}

如果私钥受损，您需要使用新证书和新私钥创建凭据。 在您的应用程序使用新凭据生成访问令牌后，您可以撤消和删除旧证书。

可执行以下步骤来做到这一点：

1. 首先，添加新密钥。 这将生成具有新私钥和新证书的凭据。 新私钥将在UI中标记为 **当前** 因此，和将用于今后此技术帐户的所有新凭据。 请注意，与旧私钥关联的凭据在被撤消之前仍然有效。 要实现此目的，请按三个圆点(**...**) **添加新私钥**:

   ![添加新私钥](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. 按 **添加** 提示如下：

   ![确认添加新私钥](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   此时将打开一个新的浏览选项卡，其中包含新目录，并且UI将进行更新以显示两个私钥，其中新目录的标记为 **当前**:

   ![UI中的私钥](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. 在非AEM服务器上安装新凭据，并确保连接正常。 请参阅 [服务器到服务器流量部分](#the-server-to-server-flow) 有关如何执行此操作的详细信息
1. 撤消旧证书。 为此，您可以选择三个圆点(**...**)并按 **撤销**:

   ![撤消证书](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   然后，按下 **撤销** 按钮：

   ![撤消证书确认](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. 最后，删除已泄露的证书。
