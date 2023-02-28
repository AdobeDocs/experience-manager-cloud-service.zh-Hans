---
title: ' [!DNL AEM Forms] as a Cloud Service 简介'
description: 探索 AEM Forms 并了解它如何帮助您生成业务就绪的文档和表单内容。了解 Platform-as-a-Service (PaaS)，如何管理企业级数字表单和业务流程，以及如何将 Forms 连接到当前数据源。
landing-page-description: 了解如何在 AEM as a Cloud Service 中使用表单。
exl-id: aa5ef10c-ba78-4a9d-8b2b-a72a7a306888
source-git-commit: c51aa20a37e27252a8c1e6a72d4bc6ffacea46f7
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 25%

---

# 简介 {#introduction}

Adobe [!DNL Experience Manager Forms as a Cloud Service] 提供云原生的Platform as a Service(PaaS)解决方案，供企业创建、管理、发布和更新复杂的数字表单，同时将提交的数据与后端流程、业务规则进行集成，并将数据保存到外部数据存储中。

## 数字化并简化注册和入门体验

您可以使用该服务创建和推出交互式且具有吸引力的数字表单。例如，以一家希望将其客户注册过程数字化的企业为例。他们拥有多个包含现有客户数据的数据源，且希望预先填充表单、添加电子签名表单，并将填写的表单存档为 PDF 文件。此外，该企业有多种打印表单 (PDF 表单)，且还希望将所有打印表单转换为数字表单。

该企业可使用 [!DNL AEM Forms] as a Cloud Service 创建数字表单、将表单连接到现有数据源、将表单与 [!DNL Adobe Sign] 集成以将电子签名添加到表单、生成记录文档 (DoR)，从而将提交的表单存档为 PDF 文件。该企业还可使用该服务将现有的 PDF 表单转换为数字表单。

![数据收集 — 响应式表单设计](/help/forms/assets/data-collection.jpeg){width="40%"}
响应式表单设计

在大型企业中，表单通常只创建一次，然后通过复制到内容管理系统来重复使用。 保持大型表单数据库的最新状态并使其可被发现，可能是一项相当大的挑战。 AEM提供了可自定义的Forms门户，可确保客户通过Web和移动渠道查找和访问所需的表单。

## 个性化通信

高效自助式数字体验的一个重要组成部分是及时地传达个性化信息，供用户从任何位置和任何设备上访问。 个性化且及时的通信可以同时提高转化率和用户满意度。

使用AEM Forms，企业用户可以通过自定义文档模板并将来自后端流程的信息与模板相结合来创建引人入胜的个性化用户体验。 一组初始API可帮助业务集规则，这些规则可根据查询或按批次定期间隔确定何时生成通信。

个性化文档（如收据、欢迎工具包和报表）很容易生成。 组织可以将流量引导至个性化的Web门户，从而导致注册或购买其他服务。


![个性化通信 — 响应式设计](/help/forms/assets/personalized-communication.jpeg){width="40%"}
个性化发票

这项服务始终最新、可用，且在不断学习。组织可以使用 [!DNL AEM Forms] as a Cloud Service，并在云中获取所有这些功能，而无需任何本地基础架构。 这项服务还将企业从复杂的升级周期中解放出来，因为它会持续更新最新功能。

## 关键功能 {#key-features}

|  |  |
|---|---|
| 自适应表单 | 为您的网站、应用程序及其他数字和打印渠道创建和管理交互式、动态、响应式、移动友好且以数据为驱动的表单。 请查看以下内容，以开始、了解和实施注册体验： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html"> 创建自适应表单 </a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/themes.html">自适应表单的样式</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br"> 将数据提交到数据存储或工作流</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html"> 创建表单记录以进行长期存档</a></li></ul> |
| 通信 API | 根据需要或按计划时间间隔（如每月报表和帐户通知）自动创建、管理和提供与RESTful API的个性化数据驱动通信。 请查看以下内容，以开始、了解和创建： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-generation"> 生成个性化通信 </a> </li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-manipulation"> 汇编或拆解PDF文档 </a> </li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#convert-to-and-validate-pdf%2Fa-compliant-documents">创建符合PDF/A的文档 </a></li></ul> |
| automated forms conversion服务 | 将基于PDF的旧版表单转换为可轻松在线管理和分发的自适应Forms。 请查看以下内容以开始使用： <ul><li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html">配置Automated forms conversion服务</a></li><li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html?lang=zh-Hans">将PDF forms转换为自适应表单</a></li></ul> |
| Forms Workflow | 自动化涉及表单和文档服务的业务流程。 在表单和文档在业务流程的不同阶段移动时，分配、传送、审阅和批准这些表单和文档。 请查看以下内容以开始使用：  <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms.html">发送表单或文档以供审阅</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#assign-task-step">创建批准拒绝工作流程</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#generate-document-of-record-step">添加记录文档 </a> 或 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#sign-document-step"> 电子签名 </a> 业务工作流的步骤</a></li></ul> |
| 电子签名 | 与Adobe Sign和DocuSign集成，以便于将Forms和文档发送给用户进行电子签名。 <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html">使用Adobe Sign对自适应表单进行电子签名 </a></li><li></a> <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-docusign-adaptive-forms.html">使用DocuSign对自适应表单进行电子签名 </a></li></ul> |
| Forms Analytics | 使用Adobe Analytics深入了解用户行为和偏好。 <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-aem-forms-with-adobe-analytics.html?lang=en">将自适应表单与Adobe Analytics连接</a></li></ul> |
| 数据源 | 轻松将表单和文档与外部数据源连接起来，以便检索和发送数据。 <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html?lang=en">连接到RDBMS或Rest端点</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=en">连接到Microsoft Dynamics 365或Salesforce云服务</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html?lang=en">连接到Microsoft Azure Blob Storage</a></li></ul> |


