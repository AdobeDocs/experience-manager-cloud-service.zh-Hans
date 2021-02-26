---
title: 为服务器端API生成访问令牌
description: 了解如何通过生成安全的JWT令牌来促进第三方服务器与作为Cloud Service的AEM之间的通信
translation-type: tm+mt
source-git-commit: 41b4bb3a63089c05750a40e910ee7578727d8b15
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 0%

---


# 简介 {#introduction}

某些体系结构依赖于从托管在AEM基础架构外的服务器上的应用程序发出对AEM的Cloud Service调用。 例如，调用服务器的移动应用程序，然后作为Cloud Service向AEM发出API请求。

服务器到服务器的流程如下所述，同时还简化了开发流程。 AEM作为Cloud Service[开发者控制台](development-guidelines.md#crxde-lite-and-developer-console)用于生成身份验证过程所需的令牌。

>[!NOTE]
>
>除本文档外，您还可以参阅关于作为Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication)的AEM基于令牌的身份验证的教程。[

## 服务器到服务器的流{#the-server-to-server-flow}

具有IMS组织管理员角色的用户可以生成AEM作为Cloud Service凭据，随后可以由具有AEM作为Cloud Service环境管理员角色的用户检索该凭据，并应该安装在服务器上，并需要谨慎地作为密钥处理。 此JSON格式文件包含与AEM集成为Cloud ServiceAPI所需的所有数据。 该数据用于创建已签名的JWT令牌，该令牌与IMS交换以用于IMS访问令牌。 然后，此访问令牌可用作承载身份验证令牌以作为Cloud Service向AEM发出请求。

服务器到服务器的流包括以下步骤：

* 从开发人员控制台获取AEM作为Cloud Service凭据
* 在向AEM发出调用的非AEM服务器上将AEM作为Cloud Service凭据进行安装
* 生成JWT令牌，并使用Adobe的IMS API交换访问令牌的令牌
* 使用作为承载身份验证令牌的访问令牌调用AEM API
* 在AEM环境中为技术帐户用户设置适当的权限

### 将AEM作为Cloud Service凭据{#fetch-the-aem-as-a-cloud-service-credentials}

作为Cloud Service开发人员控制台访问AEM的用户将看到给定环境的开发人员控制台中的集成选项卡以及两个按钮。 以AEM为Cloud Service环境管理员角色的用户可以单击&#x200B;**获取服务凭据**&#x200B;按钮来显示服务凭据json，该凭据将包含非AEM服务器所需的所有信息，包括客户端id、客户端密钥、私钥、证书以及环境创作层和发布层的配置，而不管选择了哪个窗格。

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
>IMS组织管理员(通常是通过Cloud Manager设置环境的同一用户)必须首先访问开发人员控制台并单击&#x200B;**获取服务凭据**&#x200B;按钮，以便生成凭据，然后由具有AEM管理员权限的用户以Cloud Service环境进行检索。 如果IMS组织管理员尚未这样做，将显示一条消息通知他们需要IMS组织管理员角色。

### 在非AEM服务器{#install-the-aem-service-credentials-on-a-non-aem-server}上安装AEM服务凭据

向AEM发出调用的非AEM应用程序应能将AEM作为Cloud Service凭据访问，并将其视为机密。

### 生成JWT令牌并交换访问令牌{#generate-a-jwt-token-and-exchange-it-for-an-access-token}

在调用Adobe的IMS服务时使用凭据创建JWT令牌，以检索有效时间为24小时的访问令牌。

可以使用为此目的设计的客户端库将AEM CS服务凭据交换为访问令牌。 可从[Adobe的公共GitHub存储库](https://github.com/adobe/aemcs-api-client-lib)访问客户端库，其中包含更详细的指南和最新信息。

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

同样的交换可以在能够生成具有正确格式的签名JWT令牌并调用IMS令牌交换API的任何语言中执行。

访问令牌将定义何时过期，通常为24小时。 Git存储库中有一个示例代码，用于管理访问令牌并在其过期前刷新它。

### 调用AEM API {#calling-the-aem-api}

将适当的服务器到服务器API调用作为Cloud Service环境(包括头中的访问令牌)发送到AEM。 因此，对于“Authorization”标头，请使用值`"Bearer <access_token>"`。 例如，使用`curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}中为技术帐户用户设置适当的权限

在AEM中创建技术帐户用户后(在具有相应访问令牌的第一个请求后发生)，技术帐户用户必须在&#x200B;**AEM中正确获得**&#x200B;权限。

请注意，默认情况下，在AEM作者服务中，技术帐户用户将添加到提供读取访问权限AEM的参与者用户组。

可以使用常用方法进一步为AEM中的此技术帐户用户授予权限。

## 开发人员流{#developer-flow}

开发人员可能希望使用其非AEM应用程序（在其笔记本电脑上运行或托管）的开发实例进行测试，该应用程序会作为Cloud Service开发环境向开发AEM发出请求。 但是，由于开发者不一定具有IMS管理员角色权限，我们不能假设他们能够生成常规服务器到服务器流中描述的JWT载体。 因此，我们为开发者提供了一种机制，使其能够直接生成访问令牌，该机制可以在向AEM发出的请求中用作他们可以访问的Cloud Service环境。

有关将AEM用作Cloud Service开发人员控制台所需权限的信息，请参阅[开发人员指南文档](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)。

>[!NOTE]
>
>局部开发访问令牌的有效期最长为24小时，此后必须使用相同方法重新生成。

开发人员可以使用此令牌从其非AEM测试应用程序向AEM发出调用，作为Cloud Service环境。 通常，开发人员会将此令牌与其笔记本电脑上的非AEM应用程序一起使用。 此外，AEM作为云通常是非生产环境。

开发人员流程包括以下步骤：

* 从开发人员控制台生成访问令牌
* 使用该访问令牌调用AEM应用程序。

开发人员还可以对在其本地计算机上运行的AEM项目进行API调用，在这种情况下，不需要访问令牌。

### 生成访问令牌{#generating-the-access-token}

单击“开发人员控制台”中的&#x200B;**获取本地开发令牌**&#x200B;按钮以生成访问令牌。

### 然后使用访问令牌{#call-the-aem-application-with-an-access-token}调用AEM应用程序

将非AEM应用程序的相应服务器到服务器API调用作为Cloud Service环境(包括标头中的访问令牌)发送到AEM。 因此，对于“Authorization”标头，请使用值`"Bearer <access_token>"`。

## 服务凭据吊销{#service-credentials-revocation}

如果需要撤销凭据，您需要使用以下步骤向客户支持提交请求：

1. 在用户界面中禁用Adobe Admin Console的技术帐户用户：
   * 在Cloud Manager中，按&#x200B;**...**&#x200B;按钮。 这将打开产品用户档案页
   * 现在，单击&#x200B;**AEM Users**&#x200B;用户档案，以显示用户的列表
   * 单击&#x200B;**API凭据**&#x200B;选项卡，然后找到相应的技术帐户用户并将其删除
2. 联系客户支持，并请求删除该特定环境的服务凭据
3. 最后，您可以再次生成凭据，如本文档中所述。 另外，请确保创建的新技术帐户用户具有适当的权限。