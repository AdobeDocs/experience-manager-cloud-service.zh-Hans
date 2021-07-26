---
title: 为服务器端API生成访问令牌
description: 了解如何通过生成安全的JWT令牌来促进第三方服务器与作为Cloud Service的AEM之间的通信
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: 89b43e14f35e18393ffab538483121c10f6b5a01
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 0%

---

# 简介 {#introduction}

某些体系结构依赖于从托管在AEM基础架构外的服务器上的应用程序中调用AEM作为Cloud Service。 例如，一个移动设备应用程序，它调用服务器，然后向AEM发出API请求，作为Cloud Service。

服务器到服务器的流程以及简化的开发流程如下所述。 AEM as aCloud Service[Developer Console](development-guidelines.md#crxde-lite-and-developer-console)用于生成身份验证过程所需的令牌。

>[!NOTE]
>
>除了本文档之外，您还可以查阅有关[AEM as a Cloud Service基于令牌的身份验证](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication)的教程。

## 服务器到服务器流 {#the-server-to-server-flow}

具有IMS组织管理员角色的用户，以及AEM作者上的AEM用户或AEM管理员产品配置文件的成员，可以生成AEM作为Cloud Service凭据。 随后，具有AEM作为Cloud Service环境管理员角色的用户可检索该凭据，该凭据应安装在服务器上，并且需要谨慎处理为密钥。 此JSON格式文件包含与AEM as a Analytics API集成所需的所有数据。 数据用于创建已签名的JWT令牌，该令牌与IMS交换以获取IMS访问令牌。 然后，此访问令牌可用作载体身份验证令牌，以向AEM作为Cloud Service发出请求。

服务器到服务器流程涉及以下步骤：

* 从开发人员控制台中获取AEM as a Cloud Service凭据
* 在对AEM进行调用的非AEM服务器上将AEM作为Cloud Service凭据进行安装
* 使用Adobe的IMS API生成JWT令牌并交换该令牌以用于访问令牌
* 使用访问令牌作为载体身份验证令牌调用AEM API
* 在AEM环境中为技术帐户用户设置适当的权限

### 获取AEM作为Cloud Service凭据 {#fetch-the-aem-as-a-cloud-service-credentials}

对AEM as a Cloud Service开发人员控制台具有访问权限的用户将在开发人员控制台中看到给定环境的“集成”选项卡，以及两个按钮。 具有AEM作为Cloud Service环境管理员角色的用户可以单击&#x200B;**获取服务凭据**&#x200B;按钮以显示服务凭据json，其中将包含非AEM服务器所需的所有信息，包括客户端ID、客户端密钥、私钥、证书以及环境创作层和发布层的配置，而不考虑面板选择。

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

>[!IMPORTANT]
>
>IMS组织管理员（通常是通过Cloud Manager配置环境的同一用户）(也应是AEM创作上AEM用户或AEM管理员产品配置文件的成员)必须先访问开发人员控制台并单击&#x200B;**获取服务凭据**&#x200B;按钮，以便具有AEM作为Cloud Service环境的管理员权限的用户生成并稍后检索凭据。 如果IMS组织管理员尚未执行此操作，则会显示一条消息，告知他们需要IMS组织管理员角色。

### 在非AEM服务器上安装AEM服务凭据 {#install-the-aem-service-credentials-on-a-non-aem-server}

调用AEM的非AEM应用程序应能够访问AEM作为Cloud Service凭据，并将其视为机密。

### 生成JWT令牌并将其交换为访问令牌{#generate-a-jwt-token-and-exchange-it-for-an-access-token}

在对AdobeIMS服务的调用中，使用凭据创建JWT令牌，以检索有效期为24小时的访问令牌。

可以使用为此目的而设计的客户端库将AEM CS服务凭据交换为访问令牌。 客户端库可从[Adobe的公共GitHub存储库](https://github.com/adobe/aemcs-api-client-lib)获取，其中包含更详细的指导和最新信息。

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

对AEM作为Cloud Service环境进行相应的服务器到服务器API调用，包括标头中的访问令牌。 因此，对于“Authorization”标头，请使用值`"Bearer <access_token>"`。 例如，使用`curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在AEM中为技术帐户用户设置适当的权限 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

在AEM中创建技术帐户用户（这在具有相应访问令牌的第一个请求之后发生）后，技术帐户用户必须在&#x200B;**AEM中获得相应的**&#x200B;权限。

请注意，在AEM创作服务中，默认情况下，技术帐户用户会添加到提供读取访问权限的参与者用户组中。AEM

可以使用常用方法进一步为AEM中的此技术帐户用户授予权限。

## 开发人员流程 {#developer-flow}

开发人员可能希望使用其非AEM应用程序的开发实例（在其笔记本电脑上运行或托管）进行测试，该实例可以请求将开发AEM作为Cloud Service开发环境。 但是，由于开发人员不一定具有IMS管理员角色权限，因此我们不能假定他们可以生成常规服务器到服务器流中描述的JWT载体。 因此，我们为开发人员提供了一种机制，用于直接生成访问令牌，该令牌可用于作为他们有权访问的Cloud Service环境的AEM请求中。

有关将AEM用作Cloud Service开发人员控制台所需权限的信息，请参阅[开发人员指南文档](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)。

>[!NOTE]
>
>本地开发访问令牌的有效期最长为24小时，之后必须使用同一方法重新生成该令牌。

开发人员可以使用此令牌从其非AEM测试应用程序向AEM作为Cloud Service环境进行调用。 通常，开发人员会在自己的笔记本电脑上将此令牌与非AEM应用程序一起使用。 此外，AEM as a Cloud通常是非生产环境。

开发人员流程涉及以下步骤：

* 从开发人员控制台中生成访问令牌
* 使用访问令牌调用AEM应用程序。

开发人员还可以对其本地计算机上运行的AEM项目进行API调用，在这种情况下，不需要访问令牌。

### 生成访问令牌 {#generating-the-access-token}

单击开发人员控制台中的&#x200B;**获取本地开发令牌**&#x200B;按钮以生成访问令牌。

### 调用，然后使用访问令牌调用AEM应用程序 {#call-the-aem-application-with-an-access-token}

从非AEM应用程序向AEM作为Cloud Service环境进行相应的服务器到服务器API调用，包括标头中的访问令牌。 因此，对于“Authorization”标头，请使用值`"Bearer <access_token>"`。

## 服务凭据吊销 {#service-credentials-revocation}

如果凭据需要撤消，您需要使用以下步骤向客户支持提交请求：

1. 在用户界面中禁用Adobe Admin Console的技术帐户用户：
   * 在Cloud Manager中，按&#x200B;**...**&#x200B;按钮。 此时将打开产品配置文件页面
   * 现在，单击&#x200B;**AEM Users**&#x200B;配置文件，以显示用户列表
   * 单击&#x200B;**API凭据**&#x200B;选项卡，然后找到相应的技术帐户用户并将其删除
2. 联系客户支持，并请求删除该特定环境的服务凭据
3. 最后，您可以再次生成凭据，如本文档所述。 另外，请确保所创建的新技术帐户用户具有相应的权限。
