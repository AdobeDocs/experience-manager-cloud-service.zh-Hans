---
title: 如何使用Formsas a Cloud Service将数据与XDP和PDF模板合并，或生成PCL、ZPL和PostScript格式的输出？
description: 自动将数据与 XDP 和 PDF 模板合并，或以 PCL、ZPL 和 PostScript 格式生成输出
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
feature: Adaptive Forms,APIs & Integrations
role: Admin, Developer, User
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 6%

---


# 使用同步处理 {#sync-processing-introduction}

Formsas a Cloud Service — 通信API允许您创建、汇编和提供面向品牌的个性化通信，例如业务往来函、文档、报表、索赔处理信函、福利通知、索赔处理信函、每月账单和欢迎套件。 您可以使用Communications API将模板(XFA或PDF)与客户数据相结合，生成PDF、PS、PCL、DPL、IPL和ZPL格式的文档。

假设您有一个或多个模板，并且每个模板有多个XML数据记录。 您可以使用Communications API为每个记录生成打印文档。 <!-- You can also combine the records into a single document. -->结果为非交互式PDF文档。 非交互式PDF文档不允许用户在其字段中输入数据。

Formsas a Cloud Service — 通信提供了用于计划文档生成的按需和批处理API（异步API）：

* 同步API适用于按需、低延迟和单记录文档生成用例。 这些 API 更适用于基于用户操作的用例。例如，在用户填写表单后生成文档。

* 批处理API（异步API）适用于计划的高吞吐量多文档生成用例。 这些 API 会批量生成文档。例如，每月生成的电话帐单、信用卡对帐单和收益对帐单。

## 使用同步操作 {#batch-operations}

同步操作是以线性方式生成文档的过程。 这些API分为单租户API和多租户API：

### 单租户API

* 文档生成API
* 文档操作API

<!-- 
### Multi-tenant APIs

* Document utility APIs -->


### 验证单租户API

单租户API操作支持两种类型的身份验证：

* **基本身份验证**：基本身份验证是内置到HTTP协议中的简单身份验证方案。 客户端使用Authorization标头发送HTTP请求，该标头包含单词Basic，后跟空格和base64编码的字符串username：password。 例如，若要授权为管理员/管理员，客户端将发送基本[base64编码的字符串用户名]： [base64编码的字符串密码]。

* **基于令牌的身份验证：**&#x200B;基于令牌的身份验证使用访问令牌（持有者身份验证令牌）向Experience Manageras a Cloud Service发出请求。 AEM Formsas a Cloud Service提供API以安全检索访问令牌。 要检索并使用令牌对请求进行身份验证，请执行以下操作：

   1. [从Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html)检索Experience Manageras a Cloud Service凭据。
   1. [在环境中安装Experience Manageras a Cloud Service凭据](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html)。 (应用程序服务器、Web服务器或其他非AEM服务器)配置为向（调用）云服务发送请求。
   1. [生成JWT令牌并与Adobe IMS API交换访问令牌](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html)。
   1. 将访问令牌作为持有者身份验证令牌运行Experience ManagerAPI。
   1. [在Experience Manager环境中为技术帐户用户设置适当的权限](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem)。

  >[!NOTE]
  >
  >Adobe建议在生产环境中使用基于令牌的身份验证。

<!-- 

### Authenticate a multi-tenant API

#### Authentication Headers

Every inbound HTTP API call to the multi-tenant API must contain these three headers:


* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

The values which should be sent in the `x-api-key` and `x-gw-ims-org-id` headers are provided in the Credentials details screen in the [Adobe Developer Console](https://developer.adobe.com/console). The value of the `x-api-key` header is the Client ID and the value for the `x-gw-ims-org-id` header is the Organization ID.

#### Configure Adobe Developer console to generate an access token

To set up authentication APIs, create a project in Adobe Developer Console and add Communication APIs to the project on Adobe Developer Console. The integration generates API Key, Client Secret, Payload (JWT):

1. Contact you Adobe Developer Console administrator. Ask the administrator to add as a developer.
1. Log in to `https://developer.adobe.com/console/`. Use your developer account that your administrator has provisioned to log in to Adobe Developer Console.
1. Select your organization from the top-right corner. If you do not know your organization, contact your administrator.
1. Select **[!UICONTROL Create new project]**. A screen to get started with your new project appears. Select **[!UICONTROL Add API]**. A screen with list of all the APIs enabled for your account appears.
1. Select **[!UICONTROL AEM Forms - Communications]** and select **[!UICONTROL Next]**. A screen to configure the API appears.
1. Select **[!UICONTROL OPTION 1 Generate a key pair]** and select **[!UICONTROL Generate keypair]**. It creates and downloads the configuration file. The downloaded configuration file contains all your app settings, along with the only copy of your private key. Adobe does not record your private key, make sure to securely store the downloaded file. Select **[!UICONTROL Next]**.
1. Select **[!UICONTROL Integrations - Cloud Service]** and select **[!UICONTROL Save configured API]**. Select **[!UICONTROL Service Account (JWT)]** to view the API Key, Client Secret, and other information required to access the APIs. You set to use the token to access the APIs.

#### Programmatically generate and use an access token

To programmatically generate an access token, generate a JSON Web Token (JWT) and exchange it with the Adobe Identity Management Service (IMS) for an access token.

Use the following keys, referred to as claims, to construct JWT JSON object:


* `exp`- the requested expiration of the access token, expressed as several seconds since January 1, 1970 GMT. For most use cases, this is a relatively small value. For example, 5 minutes, for five minutes from now, this value should be 1670923791.
* `iss` - the Organization ID from the Adobe Developer Console project, in the format org_ident@AdobeOrg.
* `sub` - the Technical Account ID from the Adobe Developer Console integration, in the format: id@techacct.adobe.com.
* `aud` - the Client ID from the Adobe Developer Console integration prepended with `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing` - set to the literal value `true`

This JSON object must be then base64 encoded and signed using the private key for the project. Finally, the encoded value is sent in the body of a POST request to `https://ims-na1.adobelogin.com/ims/exchange/jwt` along with the Client ID and Client Secret for the project.

##### Example

```JSON

    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache

```

#### Language Support for JWT

While it is possible to do the entire JWT generation and exchange process in custom code, it is more common to use a higher-level library to do so. A number of such libraries are listed on the [Adobe I/O JWT Documentation](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

-->

### （仅适用于文档生成API）配置资源和权限

要使用同步API，需要满足以下条件：

* 具有Experience Manager管理员权限的用户
* 将模板和其他资源上传到Experience Manager FormsCloud Service实例

### （仅适用于Document Generation API）将模板和其他资源上传到Experience Manager实例

组织通常有多个模板。 例如，信用卡对帐单、福利对帐单和报销申请都使用一个模板。 将所有此类XDP和PDF模板上传到您的Experience Manager实例。 要上传模板，请执行以下操作：

1. 打开您的Experience Manager实例。
1. 转到Forms > Forms和文档
1. 单击“创建”>“文件夹”，然后创建一个文件夹。 打开文件夹。
1. 单击“创建”>“文件上载”并上载模板。

### 调用API

[API参考文档](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)提供了有关API提供的所有参数、身份验证方法和各种服务的详细信息。 API参考文档还提供了.yaml格式的API定义文件。 您可以下载.yaml文件并将其上传到[Postman](https://www.postman.com/)，以检查API的功能。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>只有forms-users组的成员才能访问Communications API。

>[!MORELIKETHIS]
>
>* [AEM Formsas a Cloud Service通信简介](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* 自适应AEM Forms和通信API的[Formsas a Cloud Service架构](/help/forms/aem-forms-cloud-service-architecture.md)
>* [通信处理 — 同步API](/help/forms/aem-forms-cloud-service-communications.md)
>* [通信处理 — 批处理API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)