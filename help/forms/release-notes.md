---
title: '[!DNL AEM Forms] as a Cloud Service发行说明'
description: '[!DNL AEM Forms] as a Cloud Service发行说明'
exl-id: 35950b81-6e45-4a75-bd27-8c28fd68e42e
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2024'
ht-degree: 2%

---


# [!DNL Experience Manager Forms] as a Cloud Service发行说明 {#overview}

Adobe Experience Manager [!DNL AEM Forms] as a Cloud Service不断获得改进。 要了解最新动态，请定期访问此页面。 此页面为您提供以下信息：

- 新增功能
- 改进功能
- 预发行功能
- 测试版功能
- 错误修复
- 弃用功能
- 特别说明
- 未来变更计划

>[!NOTE]
>
>有关所有其他AEMas a Cloud Service发行组件的发行说明，请参阅 [最新发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hans).

## 2021.10.0 {#sep-2021-10-0}

### 的新增功能 [!DNL Forms] {#what-is-new-forms-oct-2021}

- **适用于自适应Forms的Analytics**:现在，您可以通过Adobe Analytics for Adaptive Forms捕获和跟踪已登录和未登录（匿名）的行为，以收集最终用户分析。 它有助于根据数据做出明智的决策，以改善最终用户体验。

### 的新增功能 [!DNL Forms] 预发行渠道 {#prerelease-features-forms-oct-2021}

- **将AEM工作流数据外部化以进行安全处理**:您可以在客户管理的存储库中存储包含敏感个人数据(SPD)元素的正在处理的AEM工作流数据(AEM工作流变量数据)，以便进行安全处理。 数据元素和工作流变量不存储在AEM存储库中，在处理工作流时，它们会根据需要从客户管理的存储库获取。

### 的测试版功能 [!DNL Forms] {#sep-what-is-new-forms-oct-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [通信API](aem-forms-cloud-service-communications.md) 帮助您将模板和XML数据结合起来，以生成各种格式的打印文档。 该服务允许您以同步和批处理模式生成文档。 利用API，可创建应用程序，以便：

   - 使用XML数据填充模板文件(PDF和XDP)，以生成文档。
   - 以各种格式生成输出表单，包括非交互式PDF打印流。

您可以写入 [!DNL formscsbeta@adobe.com] 注册测试版计划。

## 2021.9.0 {#sep-2021-09-0}

### 的新增功能 [!DNL Forms] {#what-is-new-forms-sep-2021}

- **在自适应表单中使用Adobe Sign角色**:Adobe Sign的业务和企业服务级别可以选择扩展协议收件人的角色，而不仅仅是签名者，以更好地满足其工作流要求。 您现在可以 [允许每个协议收件人在自适应表单中配置其角色](working-with-adobe-sign.md#addsignerstoanadaptiveform)，默认角色为签名者。

- **适用于自适应Forms的Analytics**:您现在可以捕获和 [通过Adobe Analytics跟踪最终用户行为](integrate-aem-forms-with-adobe-analytics.md) 以收集最终用户分析。 它有助于根据数据做出明智的决策，以改善最终用户体验。

- **轻松将AEM Forms与Microsoft Dynamics和Salesforce连接起来**:该服务为Microsoft Dynamics和Salesforce提供开箱即用的数据源配置和数据模型，使其成为现成版本 [开发人员可以更快、更轻松地将Microsoft Dynamics和Salesforce配置为自适应表单的数据源](configure-msdynamics-salesforce.md).

- **使用DocuSign对自适应表单进行电子签名：** [您可以使用DocuSign对自适应表单进行电子签名](integrate-docusign-adaptive-forms.md). 该服务提供自定义提交操作，以便将DocuSign与自适应表单结合使用。

### 的测试版功能 [!DNL Forms] {#sep-what-is-new-forms-prerelease}

- **统一存储连接器：** 使用统一存储连接器将客户管理的存储库中的进程中数据外部化。 例如，您可以将包含敏感个人数据(SPD)的正在处理的AEM工作流数据(AEM工作流变量数据)存储在客户管理的存储库中。

   <!--* Enable Forms Portal’s save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [通信API](aem-forms-cloud-service-communications.md) 帮助您结合XDP模板和XML数据，以生成各种格式的打印文档。 该服务允许您以同步模式生成文档。 利用API，可创建应用程序，以便：
   - 使用XML数据填充模板文件，以生成文档。
   - 以各种格式生成输出表单，包括非交互式PDF打印流。
   - 从XFA表单PDF和Adobe Acrobat表单生成打印PDF文件。

您可以写入 [!DNL formscsbeta@adobe.com] 注册测试版计划。

### 限制 {#limitations}

- Adobe Analytics只能跟踪经过身份验证的用户的表单量度。

<!--

### New features available in [!DNL Forms] prerelease channel {#prerelease-features-forms-sep-2021}

* **Forms Portal:**  In a typical forms-centric portal deployment scenario, forms development and portal development are two disjoint activities. While Form Designers design and store forms in a repository, Web Developers create a web application to list forms and handle submission of forms. Forms are copied over to the web tier as there is no communication between the forms repository and the web application.

  Such scenarios often result in management issues and production delays. For example, if there is a newer version of a form available in the repository, you need to replace the form on the web tier, modify the web application, and redeploy the form on the public site. Redeploying the web application might cause some server downtime. Typically, the server downtime is a planned activity and therefore the changes cannot be pushed to the public site instantaneously.

  AEM Forms provides portal components that reduce management overheads and production delays. The components equip Web Developers to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM). The form portal components allow you to add the following functionality:

  * List forms in customized layouts. Out of the box, List view and Card view are provided.

  * List published adaptive forms on an AEM Sites page.

  * Enable searching of forms based on a various criteria, such as form properties, metadata, and tags.

  * Lists drafts and submissions related to Adaptive Form created by end user.

  -->

## 2021.8.0 {#aug-2021-08-0}

### 的新增功能 [!DNL Forms] {#what-is-new-forms-aug-2021}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

- 适用于Formsas a Cloud Service的AEM Archetype项目现在包括 [表单Microsoft Dynamics和Salesforce的数据模型](setup-local-development-environment.md).

- **基于Acroform的记录文档**:AEM Formsas a Cloud Service支持使用 [Adobe Acrobat表单PDF(AcroformPDF)](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 作为记录文档的模板（除基于XFA的表单模板之外）。

- **Microsoft Azure数据存储连接器**:您现在可以 [将表单数据模型连接到Microsoft Azure Storage](configure-azure-storage.md). 它允许您将自适应表单数据检索并存储到Microsoft Azure Storage as a BLOB。

### 测试版功能 [!DNL Forms] {#aug-what-is-new-forms-prerelease}

- **统一存储连接器：** 使用统一存储连接器将客户管理的存储库中的进程中数据外部化。 例如，您可以

   - 启用Forms Portal的保存和恢复功能，并将自适应表单草稿存储在客户管理的数据存储库中。
   - 将包含敏感个人数据(SPD)的正在处理的AEM工作流数据(AEM工作流变量数据)存储在客户管理的存储库中。

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [通信API](aem-forms-cloud-service-communications.md) 帮助您结合XDP模板和XML数据，以生成各种格式的打印文档。 该服务允许您以同步模式生成文档。 利用API，可创建应用程序，以便：
   - 使用XML数据填充模板文件，以生成文档。
   - 以各种格式生成输出表单，包括非交互式PDF打印流。
   - 从XFA表单PDF和Adobe Acrobat表单生成打印PDF文件。

您可以写入 [!DNL formscsbeta@adobe.com] 注册测试版计划。

### 的新增功能 [!DNL Forms] 预发行渠道 {#prerelease-features-forms-aug-2021}

- **在自适应表单中使用Adobe Sign角色**:Adobe Sign的业务和企业服务级别可以选择扩展协议收件人的角色，而不仅仅是签名者，以更好地满足其工作流要求。 您现在可以 [允许每个协议收件人在自适应表单中配置其角色](working-with-adobe-sign.md#addsignerstoanadaptiveform)，默认角色为签名者。

- **适用于自适应Forms的Analytics**:您现在可以通过Adobe Analytics for Adaptive Forms捕获和跟踪最终用户行为，以收集最终用户分析。 它有助于根据数据做出明智的决策，以改善最终用户体验。

- **轻松将AEM Forms与Microsoft Dynamics和Salesforce连接起来**:该服务为Microsoft Dynamics和Salesforce提供开箱即用的数据源配置和数据模型，使其成为现成版本 [开发人员可以更快、更轻松地将Microsoft Dynamics和Salesforce配置为自适应表单的数据源](configure-msdynamics-salesforce.md).

## 2021.7.0 {#july-2021-07-0}

### 的新增功能 [!DNL Forms] {#july-what-is-new-forms}

- 您现在可以使用Automated forms conversion服务 [以法语、德语和西班牙语转换PDF forms语](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) 到自适应表单。
- 在模板编辑器中添加了一个单独的面板，以显示与自适应表单组件相关的错误。 它有助于将所有自适应表单错误整合到一个位置并缩短解决时间。

### 的新增功能 [!DNL Forms] 预发行渠道 {#july-prerelease-features-forms}

- **基于Acroform的记录文档**:您还可以 [使用Adobe Acrobat表单PDF(AcroformPDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作为记录文档的模板（除基于XFA的表单模板之外）。

- **Microsoft Azure数据存储连接器**:您现在可以 [将表单数据模型连接到Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). 它允许您将自适应表单数据检索并存储到Microsoft Azure Storage as a BLOB。

- **变量数据外部器**:您可以在由您的组织管理的外部存储系统上保存AEM Workflow变量的数据。

### 测试版功能 [!DNL Forms] {#july-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [通信API](aem-forms-cloud-service-communications.md) 帮助您结合XDP模板和XML数据，以生成各种格式的打印文档。 该服务允许您以同步模式生成文档。 利用API，可创建应用程序，以便：
   - 使用XML数据填充模板文件，以生成文档。
   - 以各种格式生成输出表单，包括非交互式PDF打印流。
   - 从XFA表单PDF和Adobe Acrobat表单生成打印PDF文件。

## 2021.6.0 {#july-2021-06-0}

### 的新增功能 [!DNL Forms] {#june-what-is-new-forms}

- 添加了在AEM收件箱中过滤自定义列的功能。
- 添加了使用自适应表单编辑器的主题编辑器和样式层来设置验证码组件样式的功能。
- 提高了自动检测源PDF forms中逻辑部分并将这些逻辑部分转换为相应自适应表单面板的速度和准确性。
- 添加了将PDF或XDP文件从一个文件夹移动到另一个文件夹的移动操作。

### 测试版功能 [!DNL Forms] {#june-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**:通信API可帮助您将XDP模板和XML数据结合起来，以生成各种格式的打印文档。 该服务允许您以同步模式生成文档。 利用API，可创建应用程序，以便：

   - 使用XML数据填充模板文件，生成最终表单文档。
   - 以各种格式生成输出表单，包括非交互式PDF打印流。
   - 从XFA表单PDF和Adobe Acrobat表单(AcroForm)中生成打印PDF。

- **变量数据外部器**:您可以在由您的组织管理的外部存储系统上保存AEM Workflow变量的数据。

您可以写入 [!DNL formscsbeta@adobe.com] 注册测试版计划。

### 修复的错误 [!DNL Forms] {#june-forms-bugs-fixed}

- 在通过表单数据模型(FDM)将数据提交到后端服务之前，如果对字段进行了验证，则验证会成功，但表单数据模型服务无法调用后验证。
- 当您从Apple iOS设备提交包含标准HTML上载字段的表单时，有时不会发送文件内容，而在另一端会收到0字节的文件。 Apple iOS 15.1已修复该问题。

## 2021.5.0 {#may-2021-05-0}

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 的新增功能 [!DNL Forms] {#may-what-is-new-forms}

- **上下文帮助**:为自适应表单编辑器、模板编辑器和主题编辑器添加了上下文帮助，以帮助作者更好地了解编辑器的各种功能。
- **属性浏览器中的错误消息**:为自适应Forms属性浏览器中的每个属性添加了错误消息。 这些消息有助于了解字段的允许值。

### 即将推出的测试版功能 [!DNL Forms] {#may-what-is-new-forms-prerelease}

Output as a Cloud Service:输出服务可帮助您将XDP模板和XML数据结合起来，以生成各种格式的打印文档。 该服务允许您以同步和异步批处理模式生成文档。 通过输出服务，您可以创建应用程序，以便：

- 使用XML数据填充模板文件，生成最终表单文档。
- 以各种格式生成输出表单，包括非交互式PDF打印流。
- 从XFA表单PDF中生成打印PDF。

您可以写信至formscsbeta@adobe.com注册测试版计划。

### 修复的错误 [!DNL Forms] {#may-forms-bugs-fixed}

- 在AEM Forms工作流的“分配任务”步骤中，当您将操作按钮的默认图标替换为珊瑚图标时，工作流会停止工作并记录异常。 使用默认图标时，工作流会按预期执行。
- 在布局层中，当更改列数、打开编辑层并将某些组件拖动到面板中时，自适应表单编辑器的内容区域中会开始出现正方形蓝框，且编辑器变得无响应。
- 与提供自适应或外部资产的URL相关的规则编辑器选项的错误消息太长，且用户不友好。

## 2021.4.0 {#april-2021-04-0}

### 的新增功能 [!DNL Forms] {#april-what-is-new-forms}

- **在启用了Adobe Sign的自适应Forms中使用政府ID身份验证方法**

   Adobe Sign的政府ID流程由先进的机器学习算法提供支持，使全球的公司能够确保对其收件人身份的高质量身份验证。 现在，您可以在启用了Adobe Sign的自适应Forms中使用政府ID身份验证方法。

   政府ID是一种高级身份验证方法，可指示收件人 [上传政府颁发的身份证件（驾照、国家身份证、护照）的图像](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)，然后评估该文档以确保其真实。

- **支持将表单内签名体验用于异步自适应表单提交**

   现在，您可以将表单内签名体验用于异步自适应表单提交。 您还可以在 [!DNL Experience Manager Sites] 页面，并使用表单内签名体验来提交自适应表单。

- **支持在为分配任务步骤预填充自适应表单时使用变量指定附件**

   在为“分配任务”步骤预填充自适应表单时，您现在可以使用文档类型变量为自适应表单选择输入附件。

- **支持使用文字选项为JSON类型变量设置值**

   您可以使用文字选项在AEM工作流的设置变量步骤中为JSON类型变量设置值。 利用文本选项，可以指定字符串形式的JSON。

- **使用本地开发环境创建记录文档(DoR)**

   您可以在Cloud Service实例和AEM Formsas a Cloud ServiceSDK（本地开发环境）中将XDP用作记录文档模板。 以前，支持仅限于Cloud Service实例。

### 中的错误修复 [!DNL Forms] {#april-bug-fixes-forms}

- 将配置为未生成记录文档的自适应表单提交到配置为生成记录文档的AEM工作流后，不会显示错误消息，并且任务无法提交。
