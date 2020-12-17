---
title: 为服务器端API生成访问令牌
description: 了解如何通过生成安全的JWT令牌，将第三方服务器与AEM作为Cloud Service进行通信
translation-type: tm+mt
source-git-commit: 9a4cb6d981fdf5eea4d1b9c7ae9e3c99947d9745
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---


# 简介 {#introduction}

>[!IMPORTANT]
>
>此功能尚不可用。 有关最新功能列表，请参阅[发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

某些体系结构依赖于从托管在AEM基础架构外的服务器上的应用程序发出调用作为Cloud Service调用AEM。 例如，调用服务器的移动应用程序，然后作为Cloud Service向AEM发出API请求。

服务器到服务器的流程如下所述，还有简化的开发流程。 AEM作为Cloud Service[开发者控制台](development-guidelines.md#crxde-lite-and-developer-console)用于生成身份验证过程所需的令牌。

## 服务器到服务器流{#the-server-to-server-flow}

具有管理员角色的用户可以生成JWT承载令牌，该令牌应安装在服务器上，并应谨慎视为密钥。 JWT载体令牌应与IMS交换以获得访问令牌，该令牌应包含在发给AEM的请求中作为Cloud Service。

服务器到服务器的流程涉及以下步骤：

* 从开发人员控制台生成JWT载体令牌
* 在向AEM发出调用的非AEM服务器上安装令牌
* 使用Adobe的IMS API为访问令牌交换JWT载体令牌
* 调用AEM API

### 生成JWT承载令牌{#generating-the-jwt-bearer-token}

具有组织管理员角色的用户将看到给定环境的开发人员控制台中的集成选项卡以及两个按钮。 单击&#x200B;**获取服务凭据**&#x200B;按钮将生成私钥、证书和配置。

![JWT Generation](assets/JWTtoken3.png)

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

### 在非AEM服务器{#install-the-token-on-a-non-aem-server}上安装令牌

向AEM发出调用的非AEM应用程序应安装JWT承载令牌，将其视为机密。

### 将JWT令牌交换为访问令牌{#exchange-the-jwt-token-for-an-access-token}

在对AdobeIMS服务的调用中包含JWT令牌以检索访问令牌，该令牌的有效期为24小时。

### 调用AEM API {#calling-the-aem-api}

将相应的服务器到服务器API调用作为Cloud Service环境(包括头中的访问令牌)发送到AEM。 因此，对于“Authorization”头，请使用值`"Bearer <access_token>"`。

<!-- ### Code Samples {#code-samples}

https://git.corp.adobe.com/boston/skyline-api-client-lib (internal note: URL will change to public git repo before we publish) contains client libraries written in node.js that will exchange the JSON outputted by the developer console for an access token. -->

## 开发人员流{#developer-flow}

开发人员可能希望使用其非AEM应用程序的开发实例进行测试（在其笔记本电脑上运行或托管），该实例向开发AEM提出请求，作为Cloud Service开发环境。 但是，由于开发人员不一定作为Cloud Service开发环境对AEM具有管理员角色访问权，因此我们不能假设他们可以生成常规服务器到服务器流中描述的JWT载体。 因此，我们为开发者提供了一种机制，使开发者能够直接生成访问令牌，该机制可以在请求AEM时用作他们有权访问的Cloud Service环境。 有关将AEM用作Cloud Service开发者控制台所需权限的信息，请参阅[开发者准则文档](/help/implementing/developing/introduction/development-guidelines.md)。

>[!NOTE]
>
>令牌的有效期为24小时，之后必须使用同一方法重新生成令牌。

开发人员可以使用此令牌从其非AEM测试应用程序向AEM发出调用，作为Cloud Service环境。 通常，开发人员会将此令牌与非AEM应用程序一起使用在自己的笔记本电脑上。 此外，AEM a Cloud通常是非生产环境。

开发人员流程包括以下步骤：

* 从开发人员控制台生成访问令牌
* 使用访问令牌调用AEM应用程序。

开发人员还可以对运行在其本地计算机上的AEM项目进行API调用，在这种情况下，不需要访问令牌。

### 生成访问令牌{#generating-the-access-token}

单击“开发人员控制台”中的&#x200B;**获取本地开发令牌**&#x200B;按钮以生成访问令牌。

### 然后调用访问令牌{#call-the-aem-application-with-an-access-token}的AEM应用程序

将非AEM应用程序的适当服务器到服务器API调用作为Cloud Service环境，包括头中的访问令牌。 因此，对于“Authorization”头，请使用值`"Bearer <access_token>"`。

## JWT承载令牌吊销{#jwt-bearer-token-revocation}

如果需要撤销JWT承载令牌，请向客户支持提交请求。