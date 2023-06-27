---
title: 为服务器端API生成访问令牌
description: 了解如何通过生成安全的JWT令牌来促进第三方服务器和AEMas a Cloud Service之间的通信
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '2090'
ht-degree: 0%

---

# 为服务器端API生成访问令牌 {#generating-access-tokens-for-server-side-apis}

某些体系结构依赖于对AEM的调用as a Cloud Service于托管在AEM基础架构以外服务器上的应用程序。 例如，调用服务器的移动应用程序，然后该应用程序向AEM发出as a Cloud Service的API请求。

下面介绍了服务器到服务器流程，以及简化的开发流程。 AEMas a Cloud Service [开发人员控制台](development-guidelines.md#crxde-lite-and-developer-console) 用于生成身份验证过程所需的令牌。

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## 服务器到服务器流 {#the-server-to-server-flow}

具有IMS组织管理员角色以及AEM创作中的AEM用户或AEM管理员产品配置文件成员的用户可以从AEMas a Cloud Service生成一组凭据。 每个凭据都是一个JSON有效负载，其中包括证书（公钥）、私钥和由以下内容组成的技术帐户： `clientId` 和 `clientSecret`. 具有AEMas a Cloud Service环境管理员角色的用户以后可以检索这些凭据，这些凭据应安装在非AEM服务器上，并仔细视为密钥。 此JSON格式文件包含与AEMas a Cloud ServiceAPI集成所需的全部数据。 该数据用于创建已签名的JWT令牌，该令牌与AdobeIdentity Management服务(IMS)交换以获得IMS访问令牌。 然后，可将此访问令牌用作持有者身份验证令牌，以向AEM发出as a Cloud Service请求。 默认情况下，凭据中的证书在一年后到期，但可在需要时刷新，如所述 [此处](#refresh-credentials).

服务器到服务器流涉及以下步骤：

* 从开发人员控制台获取AEMas a Cloud Service上的凭据
* 在调用AEM的非AEM服务器上安装AEMas a Cloud Service的凭据
* 生成JWT令牌并使用Adobe的IMS API交换该令牌作为访问令牌
* 使用访问令牌作为持有者身份验证令牌调用AEM API
* 在AEM环境中为技术帐户用户设置适当的权限

### 获取AEMas a Cloud Service凭据 {#fetch-the-aem-as-a-cloud-service-credentials}

有权访问AEMas a Cloud Service开发人员控制台的用户可以在开发人员控制台中查看给定环境的集成选项卡。 具有AEMas a Cloud Service环境管理员角色的用户可以创建、查看或管理凭据。

点击 **创建新的技术帐户**，创建了一组凭据，其中包括客户端id、客户端密钥、私钥、证书，以及环境的创作层和发布层的配置，而不考虑面板选择。

![创建新的技术帐户](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

此时将打开一个新的浏览器选项卡，其中显示凭据。 您可以使用此视图通过按状态标题旁边的下载图标来下载凭据：

![下载凭据](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

创建凭据后，它们将显示在 **技术帐户** 在中选项卡 **集成** 部分：

![查看凭据](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

用户以后可以使用“查看”操作查看凭据。 此外，如文章稍后所述，用户可以编辑同一技术帐户的凭据。 在必须续订或吊销证书的情况下，他们通过创建新的私钥或证书来完成此编辑。

具有AEMas a Cloud Service环境管理员角色的用户以后可以为其他技术帐户创建凭据。 当不同的API具有不同的访问要求时，此功能非常有用。 例如，读取与读写。

>[!NOTE]
>
>客户最多可以创建10个技术帐户，包括那些已删除的帐户。

>[!IMPORTANT]
>
>IMS组织管理员（通常是通过Cloud Manager配置环境的同一用户）同时也是AEM Author上的AEM用户或AEM管理员产品配置文件的成员，必须首先访问开发人员控制台。 然后，单击 **创建新的技术帐户** 凭据将由具有AEMas a Cloud Service环境管理员权限的用户生成和检索。 如果IMS组织管理员尚未创建技术帐户，则会有一条消息通知他们需要IMS组织管理员角色。

### 在非AEM服务器上安装AEM服务凭据 {#install-the-aem-service-credentials-on-a-non-aem-server}

对AEM进行调用的应用程序应能够访问AEMas a Cloud Service的凭据，并将其视为机密。

### 生成JWT令牌并将其交换为访问令牌 {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

在调用Adobe的IMS服务时，使用这些凭据创建JWT令牌以检索访问令牌，该令牌的有效期限为24小时。

可以使用为此目的而设计的客户端库将AEM CS服务凭据交换为访问令牌。 客户端库可从以下位置获得： [Adobe的公共GitHub存储库](https://github.com/adobe/aemcs-api-client-lib)，其中包含更详细的指导和最新信息。

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

可以用能够生成具有正确格式的已签名JWT令牌并调用IMS令牌交换API的任何语言执行相同的交换。

访问令牌定义其过期时间，通常为24小时。 Git存储库中存在一些示例代码，用于管理访问令牌并在令牌过期前刷新该令牌。

>[!NOTE]
>如果有多个凭据，请确保为稍后调用的AEM API调用引用相应的json文件。

### 调用AEM API {#calling-the-aem-api}

对AEMas a Cloud Service环境进行适当的服务器到服务器API调用，包括标头中的访问令牌。 因此，对于“Authorization”标头，请使用 `"Bearer <access_token>"`. 例如，使用 `curl`：

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在AEM中为技术帐户用户设置适当的权限 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

首先，必须在Adobe Admin Console中创建新的产品配置文件。

1. 转到Adobe Admin Console，网址为 [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).
1. 按 **管理** 链接位于 **产品和服务** 栏中。
1. 选择 **AEMas a Cloud Service**.
1. 按 **新建配置文件** 按钮。

   ![新配置文件](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. 命名用户档案并按 **保存**.

   ![保存配置文件](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. 从配置文件列表中选择您创建的配置文件。
1. 选择 **添加用户**.

   ![添加用户](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. 添加您创建的技术帐户（在本例中） `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`)，然后单击 **保存**.

   ![添加技术帐户](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. 等待10分钟以使更改生效，然后使用从新凭据生成的访问令牌对AEM进行API调用。 作为cURL命令，它的表示方式与以下示例类似：

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


进行API调用后，产品配置文件在AEMas a Cloud Service创作实例中显示为用户组，相应的技术帐户是该组的成员。

要检查此信息，请执行以下操作：

1. 登录到创作实例。
1. 转到 **工具** > **安全性**，然后单击 **组** 信息卡。
1. 在组列表中找到您创建的配置文件的名称，然后单击该名称：

   ![组配置文件](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. 在以下窗口中，切换到 **成员** 选项卡并检查该处是否正确列出了技术帐户：

   ![“成员”选项卡](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


或者，您也可以通过在创作实例上执行以下步骤来验证技术帐户是否显示在用户列表中：

1. 转到 **工具** > **安全性** > **用户**.
1. 检查您的技术帐户是否为用户列表，然后选择它。
1. 单击 **组** 选项卡，以便您可以验证用户是否属于与产品配置文件相对应的组。 此用户还是其他几个组的成员，包括“参与者：

   ![组成员资格](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>在2023年年中之前，在可以创建多个凭据之前，没有引导客户在Adobe Admin Console中创建产品配置文件。 因此，在AEMas a Cloud Service实例中，技术帐户未与“参与者”以外的组关联。 为了保持一致性，建议您针对此技术帐户，按如上所述在Adobe Admin Console中创建产品配置文件，并将现有技术帐户添加到该组。

<u>**设置适当的组权限**</u>

最后，为组配置所需的适当权限，以便您可以相应地调用或锁定API。

1. 登录到相应的创作实例，然后导航到 **设置** > **安全性** > **权限**
1. 在左侧窗格中，搜索与产品配置文件对应的组的名称（在本例中为“只读API”），然后选择它：

   ![搜索组](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. 单击以下窗口中的“编辑”按钮：

   ![编辑权限](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. 适当修改权限，然后单击 **保存**

   ![确认编辑权限](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>了解有关AdobeIdentity Management System (IMS)和AEM用户和组的更多信息。 请参阅 [文档](/help/security/ims-support.md).

## 开发人员流程 {#developer-flow}

开发人员可能希望使用非AEM应用程序的开发实例（在其笔记本电脑上运行或托管）进行测试，该实例会向AEMas a Cloud Service开发环境发出请求。 但是，由于开发人员不一定具有IMS管理员角色权限，因此Adobe不能假设他们能够生成常规服务器到服务器流中描述的JWT载体。 因此，Adobe为开发人员提供了一种直接生成访问令牌的机制，可用于对AEMas a Cloud Service上他们有权访问的环境的请求。

请参阅 [开发人员指南文档](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) 有关使用AEMas a Cloud Service开发人员控制台所需的权限的信息。

>[!NOTE]
>
>本地开发访问令牌的有效期最长为24小时，之后必须使用相同方法重新生成该令牌。

开发人员可以使用此令牌从其非AEM测试应用程序向AEMas a Cloud Service环境进行调用。 通常，开发人员在自己的笔记本电脑上对非AEM应用程序使用此令牌。 此外，AEM as a Cloud通常是非生产环境。

开发人员流程涉及以下步骤：

* 从开发人员控制台生成访问令牌
* 使用访问令牌调用AEM应用程序。

开发人员还可以对其本地计算机上运行的AEM项目进行API调用，在这种情况下，不需要访问令牌。

### 生成访问令牌 {#generating-the-access-token}

1. 转到 **本地令牌** 下 **集成**
1. 单击 **获取本地开发令牌** ，以便生成访问令牌。

### 使用访问令牌调用AEM应用程序 {#call-the-aem-application-with-an-access-token}

从非AEM应用程序对AEMas a Cloud Service环境进行适当的服务器到服务器API调用，包括标头中的访问令牌。 因此，对于“Authorization”标头，请使用 `"Bearer <access_token>"`.

## 刷新凭据 {#refresh-credentials}

默认情况下，AEMas a Cloud Service上的凭据在一年后过期。 为确保服务的连续性，开发人员可以选择刷新凭据，将其可用性延长一年。

要实现此刷新扩展，请执行以下操作：

* 使用 **添加证书** 按钮位于 **集成** - **技术帐户** 在开发人员控制台中，如下所示

  ![凭据刷新](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* 按下按钮后，将生成一组包含新证书的凭据。 在off-AEM服务器上安装新凭据，并确保在不删除旧凭据的情况下按预期进行连接。
* 在生成访问令牌时，请确保使用新凭据而不是旧凭据。
* 可以选择撤消（然后删除）以前的证书，使其无法再用于通过AEMas a Cloud Service进行身份验证。

## 凭据吊销 {#credentials-revocation}

如果私钥被盗用，您必须使用新证书和新私钥创建凭据。 在应用程序使用新凭据以便生成访问令牌后，可通过执行以下操作来撤销和删除旧证书：

1. 首先，添加新键。 此密钥生成包含新私钥和新证书的凭据。 新私钥在用户界面中标记为 **当前** 因此，和将用于此技术帐户以后的所有新凭据。 与旧版私钥关联的凭据在撤消之前仍然有效。 要实现此撤销，请选择三个点(**...**)，然后选择 **添加新私钥**：

   ![添加新私钥](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. 选择 **添加** 出现以下提示时：

   ![确认添加新私钥](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   此时将打开一个包含新凭据的新浏览选项卡，并更新用户界面以显示两个私钥，其中新私钥标记为 **当前**：

   ![UI中的私钥](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. 在非AEM服务器上安装新凭据，并确保连接按预期工作。 参见 [“服务器到服务器流量”部分](#the-server-to-server-flow) 了解详细信息。
1. 通过选择三个圆点(**...**)的右侧，并选择 **撤销**：

   ![撤销证书](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   然后，在下面的提示中通过按 **撤销** 按钮：

   ![撤销证书确认](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. 最后，删除受损的证书。
