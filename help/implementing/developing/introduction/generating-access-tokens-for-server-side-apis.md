---
title: 为服务器端 API 生成访问令牌
description: 了解如何通过生成安全的JWT令牌来促进第三方服务器与AEMas a Cloud Service之间的通信
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: fc49b004a61d5f981ac61cca684dc0bacf843443
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---

# 简介 {#introduction}

某些架构依赖于从AEM基础架构外的服务器上托管的应用程序as a Cloud Service调用AEM。 例如，一个移动设备应用程序，它调用服务器，然后向AEM发出API请求as a Cloud Service。

服务器到服务器的流程以及简化的开发流程如下所述。 AEMas a Cloud Service [开发人员控制台](development-guidelines.md#crxde-lite-and-developer-console) 用于生成身份验证过程所需的令牌。

>[!NOTE]
>
>除了本文档之外，您还可以查阅 [AEMas a Cloud Service的基于令牌的身份验证](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) 和 [获取集成的登录令牌](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html).

## 服务器到服务器流 {#the-server-to-server-flow}

具有IMS组织管理员角色的用户，以及AEM作者上AEM用户或AEM管理员产品配置文件的成员，可以生成AEMas a Cloud Service凭据。 随后，具有AEMas a Cloud Service环境管理员角色的用户可检索该凭据，该凭据应安装在服务器上，并且需要谨慎处理为密钥。 此JSON格式文件包含与AEMas a Cloud ServiceAPI集成所需的所有数据。 数据用于创建已签名的JWT令牌，该令牌与IMS交换以获取IMS访问令牌。 然后，此访问令牌可用作承载身份验证令牌，以向AEMas a Cloud Service发出请求。 默认情况下，凭据会在一年后过期，但可以根据需要刷新凭据，如所述 [此处](#refresh-credentials).

服务器到服务器流程涉及以下步骤：

* 从开发人员控制台获取AEMas a Cloud Service凭据
* 在对AEM进行调用的非AEM服务器上安装AEMas a Cloud Service凭据
* 使用Adobe的IMS API生成JWT令牌并交换该令牌以用于访问令牌
* 使用访问令牌作为载体身份验证令牌调用AEM API
* 在AEM环境中为技术帐户用户设置适当的权限

### 获取AEMas a Cloud Service凭据 {#fetch-the-aem-as-a-cloud-service-credentials}

有权访问AEMas a Cloud Service开发人员控制台的用户将在开发人员控制台中看到给定环境的“集成”选项卡，以及两个按钮。 具有AEMas a Cloud Service环境管理员角色的用户可以单击 **生成服务凭据** 按钮以生成和显示服务凭据json，它将包含非AEM服务器所需的所有信息，包括客户端id、客户端密钥、私钥、证书，以及环境创作层和发布层的配置，而不考虑面板选择。

![JWT生成](assets/JWTtoken3.png)

输出将类似于：

```
{
  "ok": true,
  "integration": {
    "imsEndpoint": "ims-na1.adobelogin.com",
    "metascopes": "ent_aem_cloud_sdk,ent_cloudmgr_sdk",
    "technicalAccount": {
      "clientId": "cm-p123-e1234",
      "clientSecret": "4AREDACTED17"
    },
    "email": "abcd@techacct.adobe.com",
    "id": "ABCDAE10A495E8C@techacct.adobe.com",
    "org": "1234@AdobeOrg",
    "privateKey": "-----BEGIN RSA PRIVATE KEY-----\r\REDACTED\r\n==\r\n-----END RSA PRIVATE KEY-----\r\n",
    "publicKey": "-----BEGIN CERTIFICATE-----\r\nREDACTED\r\n-----END CERTIFICATE-----\r\n"
  },
  "statusCode": 200
}
```

生成凭据后，可以在稍后的日期通过按 **获取服务凭据** 按钮。

>[!IMPORTANT]
>
>IMS组织管理员（通常是通过Cloud Manager配置环境的同一用户）(也应是AEM作者上AEM用户或AEM管理员产品配置文件的成员)必须先访问开发人员控制台并单击 **生成服务凭据** 按钮，以便具有AEMas a Cloud Service环境的管理员权限的用户生成并稍后检索凭据。 如果IMS组织管理员尚未执行此操作，则会显示一条消息，告知他们需要IMS组织管理员角色。

### 在非AEM服务器上安装AEM服务凭据 {#install-the-aem-service-credentials-on-a-non-aem-server}

调用AEM的非AEM应用程序应能够访问AEMas a Cloud Service凭据，并将其视为机密。

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

### 调用AEM API {#calling-the-aem-api}

对AEMas a Cloud Service环境进行相应的服务器到服务器API调用，包括标头中的访问令牌。 因此，对于“授权”标头，请使用值 `"Bearer <access_token>"`. 例如，使用 `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在AEM中为技术帐户用户设置适当的权限 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

在AEM中创建技术帐户用户（这在具有相应访问令牌的第一个请求后发生）后，技术帐户用户必须获得相应的权限 **in** AEM。

请注意，在AEM创作服务中，默认情况下，技术帐户用户会添加到提供读取访问权限的参与者用户组中。AEM

可以使用常用方法进一步为AEM中的此技术帐户用户配置权限。

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

单击 **获取本地开发令牌** 按钮以生成访问令牌。

### 调用，然后使用访问令牌调用AEM应用程序 {#call-the-aem-application-with-an-access-token}

从非AEM应用程序向AEMas a Cloud Service环境进行相应的服务器到服务器API调用，包括标头中的访问令牌。 因此，对于“授权”标头，请使用值 `"Bearer <access_token>"`.

## 刷新凭据 {#refresh-credentials}

默认情况下，AEMas a Cloud Service凭据会在一年后过期。 为确保服务连续性，开发人员可以选择刷新凭据，将其可用性延长一年。

要实现此目的，您可以使用 **刷新服务凭据** 按钮 **集成** 选项卡，如下所示。

![凭据刷新](assets/credential-refresh.png)

按按钮后，将生成一组新的凭据。 您可以使用新凭据更新您的密钥存储，并验证它们是否按原样运行。

>[!NOTE]
>
> 单击 **刷新服务凭据** 按钮时，旧凭据会一直进行注册，直到过期，但只有最新的凭据集可在任何时候从开发人员控制台查看。

## 服务凭据吊销 {#service-credentials-revocation}

如果凭据需要撤消，您需要使用以下步骤向客户支持提交请求：

1. 在用户界面中禁用Adobe Admin Console的技术帐户用户：
   * 在Cloud Manager中，按 **...** 按钮。 此时将打开产品配置文件页面
   * 现在，单击 **AEM用户** 用户档案，以显示用户列表
   * 单击 **API凭据** 选项卡，然后找到相应的技术帐户用户并将其删除
2. 联系客户支持，并请求删除该特定环境的服务凭据
3. 最后，您可以再次生成凭据，如本文档所述。 另外，请确保所创建的新技术帐户用户具有相应的权限。
