---
title: '"[!DNL AEM Forms] as a Cloud Service 发行说明"'
description: '"[!DNL AEM Forms] as a Cloud Service 发行说明"'
exl-id: 35950b81-6e45-4a75-bd27-8c28fd68e42e
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '2024'
ht-degree: 100%

---


# [!DNL Experience Manager Forms] as a Cloud Service 发行说明 {#overview}

Adobe Experience Manager [!DNL AEM Forms] as a Cloud Service 将持续改进。要了解最新动态，请定期访问此页面。 此页面为您提供以下信息：

- 新增功能
- 改进功能
- 预发行版功能
- Beta 版功能
- 错误修复
- 弃用功能
- 特别说明
- 未来变更计划

>[!NOTE]
>
>有关其他所有 AEM as a Cloud Service 版本组件的发行说明，请参阅[最新发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html)。

## 2021.10.0 {#sep-2021-10-0}

### [!DNL Forms] 的新增功能 {#what-is-new-forms-oct-2021}

- **Analytics for Adaptive Forms**：您现在可以通过 Adobe Analytics for Adaptive Forms 捕获和跟踪已登录和未登录（匿名）的行为，从而收集最终用户洞察。这有助于根据数据做出明智的决策，从而改善最终用户体验。

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms-oct-2021}

- **将 AEM Workflow 数据外部化以便安全处理**：您可以将包含敏感个人数据 (SPD) 的进程内 AEM Workflow 数据（AEM Workflow 变量数据）存储在客户管理的存储库中，以便安全处理。数据元素和工作流变量没有存储在 AEM 存储库中，而是在处理工作流时按需从客户管理的存储库中提取。

### [!DNL Forms] 的 Beta 版功能 {#sep-what-is-new-forms-oct-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](aem-forms-cloud-service-communications.md) 可帮助您组合模板和 XML 数据，以生成各种格式的打印文档。该服务允许您以同步模式和批处理模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：

   - 使用 XML 数据填充模板文件（PDF 和 XDP）来生成文档。
   - 生成各种格式的输出表单，包括非交互式 PDF 打印流。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

## 2021.9.0 {#sep-2021-09-0}

### [!DNL Forms] 的新增功能 {#what-is-new-forms-sep-2021}

- **在自适应表单中使用 Adobe Sign 角色**：用于商业和企业服务级别的 Adobe Sign 可让您选择扩展协议接收者的角色（不仅限于签名者），以便更好地匹配他们的工作流要求。您现在可以[允许每个协议接收者在自适应表单中配置自己的角色](working-with-adobe-sign.md#addsignerstoanadaptiveform)，签名者是默认角色。

- **Analytics for Adaptive Forms**：您现在可以[通过 Adobe Analytics for Adaptive Forms 捕获和跟踪最终用户行为](integrate-aem-forms-with-adobe-analytics.md)，从而收集最终用户洞察。这有助于根据数据做出明智的决策，从而改善最终用户体验。

- **轻松地将 AEM Forms 与 Microsoft Dynamics 和 Salesforce 连接**：此服务为 Microsoft Dynamics 和 Salesforce 提供现成的数据源配置和数据模型，使得[开发人员可以更快、更轻松地配置 Microsoft Dynamics 和 Salesforce 作为自适应表单的数据源](configure-msdynamics-salesforce.md)。

- **使用 DocuSign 对自适应表单进行电子签名：**[您可以使用 DocuSign 对自适应表单进行电子签名](integrate-docusign-adaptive-forms.md)。此服务提供了自定义提交操作，可将 DocuSign 与自适应表单结合使用。

### [!DNL Forms] 的 Beta 版功能 {#sep-what-is-new-forms-prerelease}

- **统一存储连接器：**&#x200B;使用统一存储连接器将客户管理的存储库中的进程内数据外部化。例如，您可以将包含敏感个人数据 (SPD) 的进程内 AEM Workflow 数据（AEM Workflow 变量数据）存储在客户管理的存储库中。

   <!--* Enable Forms Portal’s save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

- **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](aem-forms-cloud-service-communications.md) 帮助您组合 XDP 模板和 XML 数据以生成各种格式的打印文档。该服务允许您以同步模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：
   - 使用 XML 数据填充模板文件来生成文档。
   - 生成各种格式的输出表单，包括非交互式 PDF 打印流。
   - 利用 XFA 表单 PDF 和 Adobe Acrobat 表单生成打印版 PDF 文件。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

### 限制 {#limitations}

- Adobe Analytics 只能跟踪经过身份验证的用户的表单指标。

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

### [!DNL Forms] 的新增功能 {#what-is-new-forms-aug-2021}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

- Forms as a Cloud Service 的 AEM Archetype 项目现在包括[用于 Microsoft Dynamics 和 Salesforce 的表单数据模型](setup-local-development-environment.md)。

- **基于 Acroform 的记录文档**：除了基于 XFA 的表单模板，AEM Forms as a Cloud Service 还支持使用 [Adobe Acrobat Form PDF (Acroform PDF)](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 作为记录文档的模板。

- **Microsoft Azure 数据存储连接器**：您现在可以[将表单数据模型连接到 Microsoft Azure Storage](configure-azure-storage.md)。它可让您检索自适应表单数据并将这些数据作为 BLOB 存储到 Microsoft Azure Storage。

### [!DNL Forms] 的 Beta 版功能 {#aug-what-is-new-forms-prerelease}

- **统一存储连接器：**&#x200B;使用统一存储连接器将客户管理的存储库中的进程内数据外部化。例如，您可以

   - 启用 Forms Portal 的保存和恢复功能，将自适应表单草稿存储到客户管理的数据存储库中。
   - 将包含敏感个人数据 (SPD) 的进程内 AEM Workflow 数据（AEM Workflow 变量数据）存储在客户管理的存储库中。

- **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](aem-forms-cloud-service-communications.md) 帮助您组合 XDP 模板和 XML 数据以生成各种格式的打印文档。该服务允许您以同步模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：
   - 使用 XML 数据填充模板文件来生成文档。
   - 生成各种格式的输出表单，包括非交互式 PDF 打印流。
   - 利用 XFA 表单 PDF 和 Adobe Acrobat 表单生成打印版 PDF 文件。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms-aug-2021}

- **在自适应表单中使用 Adobe Sign 角色**：用于商业和企业服务级别的 Adobe Sign 可让您选择扩展协议接收者的角色（不仅限于签名者），以便更好地匹配他们的工作流要求。您现在可以[允许每个协议接收者在自适应表单中配置自己的角色](working-with-adobe-sign.md#addsignerstoanadaptiveform)，签名者是默认角色。

- **Analytics for Adaptive Forms**：您现在可以通过 Adobe Analytics for Adaptive Forms 捕获和跟踪最终用户行为，从而收集最终用户洞察。这有助于根据数据做出明智的决策，从而改善最终用户体验。

- **轻松地将 AEM Forms 与 Microsoft Dynamics 和 Salesforce 连接**：此服务为 Microsoft Dynamics 和 Salesforce 提供现成的数据源配置和数据模型，使得[开发人员可以更快、更轻松地配置 Microsoft Dynamics 和 Salesforce 作为自适应表单的数据源](configure-msdynamics-salesforce.md)。

## 2021.7.0 {#july-2021-07-0}

### [!DNL Forms] 的新增功能 {#july-what-is-new-forms}

- 您现在可以使用 Automated Forms Conversion Service 将[法语、德语和西班牙语版本的 PDF 表单](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model)转换为自适应表单。
- 已向模板编辑器添加一个单独的面板，以显示与自适应表单组件相关的错误。它有助于在一个位置整合所有自适应表单错误并减少解决时间。

### [!DNL Forms] 预发行渠道中提供的新功能 {#july-prerelease-features-forms}

- **基于 Acroform 的记录文档**：除了基于 XFA 的表单模板，您还可以[使用 Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作为记录文档的模板。

- **Microsoft Azure 数据存储连接器**：您现在可以[将表单数据模型连接到 Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它可让您检索自适应表单数据并将这些数据作为 BLOB 存储到 Microsoft Azure Storage。

- **变量数据外部化程序**：您可以将 AEM Workflow 变量的数据保存在由组织管理的外部存储系统上。

### [!DNL Forms] 的 Beta 版功能 {#july-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](aem-forms-cloud-service-communications.md) 帮助您组合 XDP 模板和 XML 数据以生成各种格式的打印文档。该服务允许您以同步模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：
   - 使用 XML 数据填充模板文件来生成文档。
   - 生成各种格式的输出表单，包括非交互式 PDF 打印流。
   - 利用 XFA 表单 PDF 和 Adobe Acrobat 表单生成打印版 PDF 文件。

## 2021.6.0 {#july-2021-06-0}

### [!DNL Forms] 的新增功能 {#june-what-is-new-forms}

- 添加了在 AEM 收件箱中筛选自定义列的功能。
- 添加了使用主题编辑器和自适应表单编辑器的样式层来设置验证码组件样式的功能。
- 提高了自动检测源 PDF 表单中的逻辑部分并将其转换为相应的自适应表单面板的速度和准确性。
- 添加了将 PDF 或 XDP 文件从一个文件夹移动到另一个文件夹的移动操作。

### [!DNL Forms] 的 Beta 版功能 {#june-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**：通信 API 可帮助您组合 XDP 模板和 XML 数据以生成各种格式的打印文档。该服务允许您以同步模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：

   - 使用 XML 数据填充模板文件来生成最终表单文档。
   - 生成各种格式的输出表单，包括非交互式 PDF 打印流。
   - 利用 XFA 表单 PDF 和 Adobe Acrobat 表单 (AcroForm) 生成打印版 PDF。

- **变量数据外部化程序**：您可以将 AEM Workflow 变量的数据保存在由组织管理的外部存储系统上。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

### [!DNL Forms] 中修复的错误 {#june-forms-bugs-fixed}

- 在通过表单数据模型 (FDM) 向后端服务提交数据之前验证字段时，验证成功，但表单数据模型服务无法调用后期验证。
- 在从 Apple iOS 设备提交包含标准 HTML 上传字段的表单时，有时不会发送文件内容，而在另一端会收到一个 0 字节的文件。Apple iOS 15.1 修复了此问题。

## 2021.5.0 {#may-2021-05-0}

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#may-what-is-new-forms}

- **上下文帮助**：添加了自适应表单编辑器、模板编辑器和主题编辑器的上下文帮助，以帮助作者更好地了解各编辑器的各种功能。
- **属性浏览器中的错误消息**：在自适应表单属性浏览器中为每个属性添加了错误消息。这些消息有助于了解字段的允许值。

### 即将推出的 [!DNL Forms] Beta 版功能 {#may-what-is-new-forms-prerelease}

Output as a Cloud Service：Output 服务可帮助您组合 XDP 模板和 XML 数据以生成各种格式的打印文档。该服务允许您以同步和异步批处理模式生成文档。Output 服务使您能够创建应用程序，这些应用程序允许您：

- 使用 XML 数据填充模板文件来生成最终表单文档。
- 生成各种格式的输出表单，包括非交互式 PDF 打印流。
- 从 XFA 表单 PDF 生成打印 PDF。

您可以将电子邮件发送到 formscsbeta@adobe.com 以注册 Beta 项目。

### [!DNL Forms] 中修复的错误 {#may-forms-bugs-fixed}

- 在 AEM Forms Workflows 的“分配任务”步骤中，当您将操作按钮的默认图标替换为珊瑚色图标时，工作流将停止工作并记录异常。使用默认图标时，工作流按预期执行。
- 在版面层中，当您更改列数、打开编辑层并在面板中拖动某些组件时，自适应表单编辑器的内容区域中会开始显示蓝色方形框，并且编辑器将变得无响应。
- 与提供自适应或外部资产的 URL 相关的规则编辑器选项的错误消息太长，并且对用户不友好。

## 2021.4.0 {#april-2021-04-0}

### [!DNL Forms] 的新增功能 {#april-what-is-new-forms}

- **在支持 Adobe Sign 的自适应表单中使用 Government ID 身份验证方法**

   通过先进的机器学习算法，Adobe Sign 的 Government ID 流程让世界各地的公司均可确保高质量地验证其收件人的身份。现在，您可以在支持 Adobe Sign 的自适应表单中使用 Government ID 身份验证方法。

   Government ID 是一种高级的身份验证方法，它指示收件人[上传政府颁发的身份证明文件（驾照、身份证、护照）的图像](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)，然后评估该证明文件以确保真实有效。

- **支持对异步提交自适应表单使用表单内签名体验**

   现在，您可以使用表单内签名体验来异步提交自适应表单。还可将自适应表单嵌入到 [!DNL Experience Manager Sites] 页面中，并使用表单内签名体验提交自适应表单。

- **支持在为“分配任务”步骤预先填充自适应表单时使用变量指定附件**

   在为“分配任务”步骤预先填充自适应表单时，现在可使用文档类型变量为该自适应表单选择输入附件。

- **支持使用字面选项设置 JSON 类型变量的值**

   可在 AEM Workflow 的“设置变量”步骤中使用字面选项设置 JSON 类型变量的值。通过字面选项，可按字符串的形式指定 JSON。

- **使用本地开发环境创建记录文档 (DoR)**

   可在 Cloud Service 实例和 AEM Forms as a Cloud Service SDK（本地开发环境）上使用 XDP 作为文档记录模板。以前仅限 Cloud Service 实例支持这样做。

### [!DNL Forms] 中的错误修复 {#april-bug-fixes-forms}

- 将配置为不生成记录文档的自适应表单提交到配置为生成记录文档的 AEM Workflow 时，不会显示任何错误消息，但任务无法提交。
