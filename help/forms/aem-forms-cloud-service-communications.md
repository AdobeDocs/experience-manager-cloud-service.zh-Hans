---
title: AEM Formsas a Cloud Service — 通信
description: 自动将数据与XDP和PDF模板合并，或以PCL、ZPL和PostScript格式生成输出
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 20e54ff697c0dc7ab9faa504d9f9e0e6ee585464
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 1%

---


# 使用同步处理 {#sync-processing-introduction}

Formsas a Cloud Service — 通信API允许您创建、组合和提供面向品牌的个性化通信，如业务信函、文档、报表、理赔处理信函、福利通知、理赔处理信函、每月账单和欢迎资料包。 您可以使用通信API将模板(XFA或PDF)与客户数据结合，以PDF、PS、PCL、DPL、IPL和ZPL格式生成文档。

假设您有一个或多个模板以及每个模板的多个XML数据记录。 您可以使用通信API为每个记录生成打印文档。 <!-- You can also combine the records into a single document. --> 结果会生成一个非交互式PDF文档。 非交互式PDF文档不允许用户在其字段中输入数据。

Formsas a Cloud Service — 通信为计划文档生成提供了按需API和批量API（异步API）：

* 同步API适用于按需、低延迟和单记录文档生成用例。 这些API更适合基于用户操作的用例。 例如，在用户填写表单后生成文档。

* 批处理API（异步API）适用于计划的高吞吐量多文档生成用例。 这些API可批量生成文档。 例如，每月生成的电话账单、信用卡报表和福利报表。

## 使用同步操作 {#batch-operations}

同步操作是以线性方式生成文档的过程。 这些API被分类为单租户API和多租户API:

### 单租户API

* 文档生成API
* 文档操作API

### 多租户API

* 文档实用程序API

### 验证单租户API

单租户API操作支持两种类型的身份验证：

* **基本身份验证**:基本身份验证是内置于HTTP协议中的简单身份验证方案。 客户端使用Authorization标头发送HTTP请求，该标头中包含Basic一词，后跟一个空格和一个base64编码的字符串username:password。 例如，要授权为管理员/管理员，客户端会发送基本 [base64编码的字符串用户名]: [base64编码的字符串密码].

* **基于令牌的身份验证：** 基于令牌的身份验证使用访问令牌（载体身份验证令牌）发出请求以Experience Manageras a Cloud Service。 AEM Forms as a Cloud Service提供了用于安全检索访问令牌的API。 要检索并使用令牌来验证请求，请执行以下操作：

   1. [从开发人员控制台中检索Experience Manageras a Cloud Service凭据](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [在您的环境中安装Experience Manageras a Cloud Service凭据](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (应用程序服务器、Web服务器或其他非AEM服务器)，配置为向云服务发送请求（发出调用）。
   1. [生成JWT令牌，并与Adobe IMS API交换该令牌以获取访问令牌](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. 将访问令牌作为载体身份验证令牌运行Experience ManagerAPI。
   1. [在Experience Manager环境中为技术帐户用户设置适当的权限](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

   >[!NOTE]
   >
   >Adobe建议在生产环境中使用基于令牌的身份验证。

### 验证多租户API

#### 身份验证标头

对Cloud Manager API的每个入站HTTP API调用必须包含以下三个标头：

* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

应在 `x-api-key` 和 `x-gw-ims-org-id` 标题在 [Adobe Developer控制台](https://developer.adobe.com/console). 的值 `x-api-key` 标头是客户端ID和的值 `x-gw-ims-org-id` 标题是组织ID。

#### 配置Adobe Developer控制台以生成访问令牌

要设置身份验证API，请在Adobe Developer控制台中创建一个项目，并将通信API添加到Adobe Developer控制台上的项目。 集成会生成API密钥、客户端密钥、有效负载(JWT):

1. 与Adobe Developer Console管理员联系。 要求管理员以开发人员身份添加。
1. 登录到 `https://developer.adobe.com/console/`. 使用您的管理员配置的开发人员帐户登录Adobe Developer Console。
1. 从右上角选择您的组织。 如果您不了解您的组织，请与管理员联系。
1. 点按 **[!UICONTROL 创建新项目]**. 此时会显示一个用于开始新项目的屏幕。 点按 **[!UICONTROL 添加API]**. 此时会显示一个屏幕，其中包含为您的帐户启用的所有API的列表。
1. 选择 **[!UICONTROL AEM Forms — 通信]** 点按 **[!UICONTROL 下一个]**. 此时会显示用于配置API的屏幕。
1. 选择 **[!UICONTROL 选项1生成键对]** 点按 **[!UICONTROL 生成密钥对]**. 它会创建并下载配置文件。 下载的配置文件包含您的所有应用程序设置，以及您的私钥的唯一副本。 Adobe不会记录您的私钥，请确保安全地存储下载的文件。 点按 **[!UICONTROL 下一个]**.
1. 选择 **[!UICONTROL 集成 — Cloud Service]** 点按 **[!UICONTROL 保存配置的API]**. 点按 **[!UICONTROL 服务帐户(JWT)]** 查看API密钥、客户端密钥和访问API所需的其他信息。 您设置为使用令牌访问API。

#### 以编程方式生成和使用访问令牌

要以编程方式生成访问令牌，请生成JSON Web令牌(JWT)，并将其与AdobeIdentity Management服务(IMS)交换以获取访问令牌。

使用以下键（称为声明）构建JWT JSON对象：

* `exp` — 请求的访问令牌过期时间，以自1970年1月1日（格林威治标准时间）起的秒数表示。 对于大多数用例，此值相对较小。 例如，5分钟，从现在开始5分钟，此值应为1670923791。
* `iss` - Adobe Developer控制台项目中的组织ID，格式为org_ident@AdobeOrg。
* `sub` -Adobe Developer控制台集成中的技术帐户ID，格式为：id@techacct.adobe.com。
* `aud` -Adobe Developer Console集成中的客户端ID前面预置 `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing`  — 设置为文字值 `true`

然后，此JSON对象必须使用项目的私钥进行base64编码和签名。 最后，编码值将发送到POST请求的正文中 `https://ims-na1.adobelogin.com/ims/exchange/jwt` 以及项目的客户端ID和客户端密钥。

##### 示例

```JSON
    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache
```

#### JWT的语言支持

虽然可以在自定义代码中执行整个JWT生成和交换过程，但使用更高级别的库执行此操作比较常见。 在 [Adobe I/OJWT文档](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

### （仅限文档生成API）配置资产和权限

要使用同步API，需要满足以下条件：

* 具有Experience Manager管理员权限的用户
* 将模板和其他资产上传到Experience Manager FormsCloud Service实例

### （仅适用于文档生成API）将模板和其他资产上传到Experience Manager实例

组织通常具有多个模板。 例如，信用卡报表、福利报表和索赔申请各有一个模板。 将所有此类XDP和PDF模板上传到Experience Manager实例。 要上传模板，请执行以下操作：

1. 打开Experience Manager实例。
1. 转到Forms > Forms和文档
1. 单击创建>文件夹，然后创建文件夹。 打开该文件夹。
1. 单击创建>文件上传，然后上传模板。

### 调用API

的 [API参考文档](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) 提供有关API提供的所有参数、身份验证方法和各种服务的详细信息。 API引用文档还提供了.yaml格式的API定义文件。 您可以下载.yaml文件并将其上传到 [Postman](https://www.postman.com/) 来检查API的功能。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>只有表单用户组的成员才能访问通信API。
