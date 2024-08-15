---
title: 为服务器端API生成访问令牌（旧版）
description: 了解如何通过生成安全JWT令牌来促进第三方服务器和AEM as a Cloud Service之间的通信
hidefromtoc: true
exl-id: 6561870c-cbfe-40ef-9efc-ea75c88c4ed7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 0%

---

# 为服务器端API生成访问令牌（旧版） {#generating-access-tokens-for-server-side-apis-legacy}

某些体系结构依赖于从AEM基础架构之外的服务器上托管的应用程序来调用AEM as a Cloud Service。 例如，调用服务器然后向AEM as a Cloud Service发出API请求的移动应用程序。

下面介绍了服务器到服务器流程，以及简化的开发流程。 AEM as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console)用于生成身份验证过程所需的令牌。

<!-- ERROR: Not Found (HTTP error 404)
>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## 服务器到服务器流 {#the-server-to-server-flow}

具有IMS组织管理员角色并且也是AEM Author上的AEM用户或AEM管理员产品配置文件成员的用户可以生成AEM as a Cloud Service凭据。 随后，具有AEM as a Cloud Service环境管理员角色的用户可以检索该凭据，并且这些凭据应安装在服务器上，需要小心地将其视为密钥。 此JSON格式文件包含与AEM as a Cloud Service API集成所需的全部数据。 该数据用于创建已签名的JWT令牌，该令牌与IMS交换以获得IMS访问令牌。 然后，可将此访问令牌用作持有者身份验证令牌，以向AEM as a Cloud Service发出请求。 默认情况下，凭据在一年后过期，但可在需要时刷新，请参阅[刷新凭据](#refresh-credentials)。

服务器到服务器流涉及以下步骤：

* 从Developer Console获取AEM as a Cloud Service的凭据
* 在调用AEM的非AEM服务器上安装AEM as a Cloud Service的凭据
* 生成JWT令牌并使用Adobe的IMS API交换该令牌作为访问令牌
* 使用访问令牌作为持有者身份验证令牌调用AEM API
* 在AEM环境中为技术帐户用户设置适当的权限

### 获取AEM as a Cloud Service凭据 {#fetch-the-aem-as-a-cloud-service-credentials}

有权访问AEM as a Cloud Service开发人员控制台的用户将看到给定环境的Developer Console中的集成选项卡和两个按钮。 具有AEM as a Cloud Service环境管理员角色的用户可以单击&#x200B;**生成服务凭据**&#x200B;按钮以生成和显示服务凭据json。 json包含非AEM服务器所需的所有信息，包括客户端ID、客户端密钥、私钥、证书以及环境创作层和发布层的配置，而不考虑面板选择。

![JWT生成](assets/JWTtoken3.png)

输出类似于以下内容：

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

生成凭据后，稍后可通过在同一位置按&#x200B;**获取服务凭据**&#x200B;按钮来检索凭据。

>[!IMPORTANT]
>
>IMS组织管理员(通常是通过Cloud Manager配置环境的用户)也可以是AEM Author上的AEM用户或AEM管理员产品配置文件的成员，负责访问Developer Console。 然后，他们必须单击&#x200B;**生成服务凭据**&#x200B;按钮，以便生成凭据，然后由对AEM as a Cloud Service环境具有管理员权限的用户检索。 如果IMS组织管理员未完成此任务，则会有消息通知他们需要IMS组织管理员角色。

### 在非AEM服务器上安装AEM服务凭据 {#install-the-aem-service-credentials-on-a-non-aem-server}

对AEM进行调用的非AEM应用程序应能够访问AEM as a Cloud Service的凭据，并将其视为机密。

### 生成JWT令牌并将其交换为访问令牌 {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

在调用Adobe的IMS服务时，使用凭据创建JWT令牌以检索访问令牌，该令牌的有效时间为24小时。

可以使用为此目的而设计的客户端库交换AEM CS服务凭据以换取访问令牌。 可从[Adobe的公共GitHub存储库](https://github.com/adobe/aemcs-api-client-lib)中使用客户端库，其中包含更详细的指导和最新信息。

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

可以用能够生成具有正确格式的签名JWT令牌并调用IMS令牌交换API的任何语言执行相同的交换。

访问令牌定义其过期时间，通常为24小时。 Git存储库中存在用于管理访问令牌的示例代码，可在令牌过期前对其进行刷新。

### 调用AEM API {#calling-the-aem-api}

对AEM as a Cloud Service环境进行适当的服务器到服务器API调用，包括标头中的访问令牌。 因此，对于“授权”标头，请使用值`"Bearer <access_token>"`。 例如，使用`curl`：

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在AEM中为技术帐户用户设置适当的权限 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

在AEM中创建技术帐户用户后（在第一个使用相应访问令牌的请求之后发生），必须在&#x200B;**AEM中正确授予技术帐户用户**&#x200B;权限。

默认情况下，在AEM Author服务上，技术帐户用户将添加到提供读取权限AEM的参与者用户组。

可以使用常规方法进一步为AEM中的此技术帐户用户设置权限。

## 开发人员流程 {#developer-flow}

开发人员应使用非AEM应用程序（在其笔记本电脑上运行或托管）的开发实例进行测试，该实例会向AEM as a Cloud Service开发环境发出请求。 但是，由于开发人员不一定具有IMS管理员角色权限，因此Adobe不能假设他们能够生成常规服务器到服务器流中描述的JWT载体。 因此，Adobe为开发人员提供了一种直接生成访问令牌的机制，该令牌可用于对其有权访问的AEM as a Cloud Service环境的请求中。

有关使用AEM as a Cloud Service开发人员控制台所需权限的信息，请参阅[开发人员指南文档](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)。

>[!NOTE]
>
>本地开发访问令牌的有效期最长为24小时，之后必须使用相同方法重新生成该令牌。

开发人员可以使用此令牌从其非AEM测试应用程序向AEM as a Cloud Service环境进行调用。 通常，开发人员会将此令牌与非AEM应用程序一起用在他们自己的笔记本电脑上。 此外，AEM as a Cloud通常是非生产环境。

开发人员流程涉及以下步骤：

* 从Developer Console生成访问令牌
* 使用访问令牌调用AEM应用程序。

开发人员还可以对其本地计算机上运行的AEM项目进行API调用，在这种情况下，不需要访问令牌。

### 生成访问令牌 {#generating-the-access-token}

要生成访问令牌，请在Developer Console中单击&#x200B;**获取本地开发令牌**。

### 然后使用访问令牌调用AEM应用程序 {#call-the-aem-application-with-an-access-token}

从非AEM应用程序对AEM as a Cloud Service环境进行适当的服务器到服务器API调用，包括标头中的访问令牌。 因此，对于“授权”标头，请使用值`"Bearer <access_token>"`。

## 刷新凭据 {#refresh-credentials}

默认情况下，AEM as a Cloud Service上的凭据在一年后过期。 为确保服务连续性，开发人员可以选择刷新凭据，将其可用性延长一年。 在Developer Console的&#x200B;**集成**&#x200B;选项卡中使用&#x200B;**刷新服务凭据**，如下所示。

![凭据刷新](assets/credential-refresh.png)

按下按钮后，将生成一组新的凭据。 您可以使用新凭据更新机密存储，并验证它们是否按预期工作。

>[!NOTE]
>
> 单击&#x200B;**刷新服务凭据**&#x200B;按钮后，旧凭据将保持注册状态，直到过期，但在任何时候只能从Developer Console查看最新的凭据集。

## 服务凭据吊销 {#service-credentials-revocation}

如果必须吊销凭据，则必须使用以下步骤向客户支持提交请求：

1. 在用户界面中禁用Adobe Admin Console的技术帐户用户：
   * 在Cloud Manager中，按环境旁边的&#x200B;**...**&#x200B;按钮。 此操作将打开产品配置文件页面
   * 现在，单击&#x200B;**AEM Users**&#x200B;配置文件以显示用户列表
   * 单击&#x200B;**API凭据**&#x200B;选项卡，然后查找相应的技术帐户用户并将其删除
2. 请联系客户支持，并请求删除该特定环境的服务凭据
3. 最后，您可以再次生成凭据，如本文档中所述。 另外，请确保创建的新技术帐户用户具有适当的权限。
