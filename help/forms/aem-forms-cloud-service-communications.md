---
title: AEM Formsas a Cloud Service — 通信
description: 自动将数据与XDP和PDF模板合并，或以PCL、ZPL和PostScript格式生成输出
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: a3c817dedbf20b21e609ad0e5bfd0d3c4fa9a431
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 0%

---


# 使用同步处理 {#sync-processing-introduction}

通信允许您创建、组合和提供以品牌为导向的个性化通信，如商务信函、文档、报表、理赔处理信函、福利通知、理赔处理信函、每月账单和欢迎资料包。 您可以使用通信API将模板(XFA或PDF)与客户数据结合，以PDF、PS、PCL、DPL、IPL和ZPL格式生成文档。

假设您有一个或多个模板以及每个模板的多个XML数据记录。 您可以使用通信API为每个记录生成打印文档。 <!-- You can also combine the records into a single document. --> 结果会生成一个非交互式PDF文档。 非交互式PDF文档不允许用户在其字段中输入数据。


通信为按需和计划的文档生成提供了API。 您可以将同步API用于按需API和批量API（异步API），以进行计划文档生成：

* 同步API适用于按需、低延迟和单记录文档生成用例。 这些API更适合基于用户操作的用例。 例如，在用户填写表单后生成文档。

* 批处理API（异步API）适用于计划的高吞吐量多文档生成用例。 这些API可批量生成文档。 例如，每月生成的电话账单、信用卡报表和福利报表。

## 使用同步操作 {#batch-operations}

同步操作是以线性方式生成文档的过程。 可以使用单独的API:

* 从模板生成PDF文档，并将数据合并到该文档。
* 从XDP文件或PDF文档生成PostScript(PS)、打印机命令语言(PCL)、Zebra打印语言(ZPL)文档。
* 组合PDF文档
* 反汇编PDF文档
* 将文档转换为符合PDF/A规范的文档
* 验证符合PDF/A的文档


### 验证API调用

同步操作支持两种类型的身份验证：

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


### （仅限文档生成API）配置资产和权限

要使用同步API，需要满足以下条件：

* PDF或XDP模板
* [要与模板合并的数据](#form-data)
* 具有Experience Manager管理员权限的用户
* 将模板和其他资产上传到Experience Manager FormsCloud Service实例

### （仅适用于文档生成API）将模板和其他资产上传到Experience Manager实例

组织通常具有多个模板。 例如，信用卡报表、福利报表和索赔申请各有一个模板。 将所有此类XDP和PDF模板上传到Experience Manager实例。 要上传模板，请执行以下操作：

1. 打开Experience Manager实例。
1. 转到Forms > Forms和文档
1. 单击创建>文件夹，然后创建文件夹。 打开该文件夹。
1. 单击创建>文件上传，然后上传模板。


### 调用API

的 [API参考文档](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/Communications-Services) 提供有关API提供的所有参数、身份验证方法和各种服务的详细信息。 API引用文档还提供了.yaml格式的API定义文件。 您可以下载.yaml文件并将其上传到Postman，以检查API的功能。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>只有表单用户组的成员才能访问通信API。
