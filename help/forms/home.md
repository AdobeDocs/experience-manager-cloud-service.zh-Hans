---
title: ' [!DNL AEM Forms] as a Cloud Service 简介'
description: 探索如何通过 AEM Forms 生成业务就绪表单、创建业务流程工作流以及使用文档服务生成和保护文档。
landing-page-description: 了解如何在 AEM as a Cloud Service 中使用表单。
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
exl-id: aa5ef10c-ba78-4a9d-8b2b-a72a7a306888
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 87%

---


# AEM Forms as a Cloud Service 简介 {#introduction}

<!-- Version Navigation -->
<div class="version-selector">
  <p><strong>正在寻找不同版本的文档？</strong></p>
  <ul>
    <li><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/home.html">AEM 6.5 表单文档</a></li>
    <li><strong>AEM Forms as a Cloud Service</strong>（当前）</li>
  </ul>
</div>

Adobe [!DNL Experience Manager Forms as a Cloud Service] 为企业提供了一个云原生 Platform as a Service (PaaS) 解决方案，用于创建、管理、发布和更新复杂的数字表单，同时将提交的数据与后端流程、业务规则集成，并将数据保存在外部数据存储中。

这项服务始终最新、可用，且在不断学习。企业可以使用 [!DNL AEM Forms] as a Cloud Service，在云中获得所有这些功能，而无需任何本地基础架构。这项服务还将企业从复杂的升级周期中解放出来，因为它会持续更新最新功能。

Adobe [!DNL Experience Manager Forms as a Cloud Service] 是一个以客户为中心的解决方案，可帮助完成客户历程的每一步。

## 适用性和用例

### 保险

## AEM Forms适合保险公司吗？

是。AEM Forms专为企业和法规用例（包括保险）而设计，在这些用例中，安全数据捕获、工作流驱动的处理、文档生成和系统集成至关重要。

## AEM Forms是否用于保险工作流？

是。AEM Forms通常用于将保险流程（如保单申请、理赔接收、客户入职和代理辅助表单提交）数字化。

## AEM Forms是保险运营的企业级吗？

是。AEM Forms提供了企业功能，如基于角色的访问控制、审核跟踪、工作流编排、文档生成和部署灵活性，这些都是保险业务大规模开展所必需的。

## AEM Forms与用于保险的轻量级表单构建器有何不同？

AEM Forms专为企业保险用例而设计，提供轻量级表单构建器通常无法提供的工作流编排、文档生成、可审核性和部署灵活性。

## 保险公司为何选择AEM Forms？

保险公司选择AEM Forms ，通过安全的数据捕获、工作流驱动的处理、文档生成以及与企业系统的深度集成，将复杂的管控流程数字化。

## 数字化和简化注册与登录体验

您可以使用该服务创建和推出交互式且具有吸引力的数字表单。例如，以一家希望将其客户注册过程数字化的企业为例。他们拥有多个包含现有客户数据的数据源，且希望预先填充表单、添加电子签名表单，并将填写的表单存档为 PDF 文件。此外，如果组织有多种打印表单（PDF 表单），他们还希望将其打印表单转换为数字表单。

该企业可使用 [!DNL AEM Forms] as a Cloud Service 创建数字表单、将表单连接到现有数据源、将表单与 [!DNL Adobe Sign] 集成以将电子签名添加到表单、生成记录文档 (DoR)，从而将提交的表单存档为 PDF 文件。该企业还可使用该服务将现有的 PDF 表单转换为数字表单。

在大型企业中，通常只创建表单一次，之后通过将它复制到内容管理系统中来进行重用。将大型表单数据库保持最新并使其易于发现可能是一项相当大的挑战。AEM 提供了一个可自定义的表单门户，确保客户能够通过网页和移动渠道找到并访问所需的表单。您可以自定义表单门户的外观、品牌化方法和徽标，满足您组织的特定要求。

## 提供个性化的通信

高效自助服务数字体验的一个重要组成部分是，及时传达用户可以在任意位置通过任意设备访问的个性化信息。个性化和及时的通信可以提高转化率和用户满意度。

利用 AEM Forms，商业用户可以自定义文档模板并将后端流程中的信息整合到模板中，从而打造引人注目的、个性化的用户体验。一组直观的 API 可帮助企业设置规则，决定何时根据查询或定期批量生成通信。


可以轻松生成个性化的文档，例如收据、欢迎套件和对帐单。组织可以将流量引入个性化的 Web 门户，从而让受众注册或购买额外的服务。


## 自动化后台工作流

使用以表单为中心的工作流可自动处理表单数据，并将这些数据发送给不同的利益相关者（例如，经理或部门），以便进行审查、审批或进一步处理。这些工作流可帮助您的组织最大限度地降低风险，保持合规。为此，它确保以一致且可审核的方式处理表单数据，自动化手动任务，提供基于角色的访问控制，并帮助遵守监管部门的要求。


## 优化表单性能

该服务与 Adobe Analytics 集成，让您能够捕获和跟踪已发布表单的性能指标。分析这些指标的目的在于，根据有关使表单或文档更有用所需的更改的数据做出明智的决策。您可以使用 Adobe Analytics 发现用户在使用自适应表单时遇到的交互模式和问题。


## 开始使用 {#key-features}

AEM Forms as a Cloud Service 提供了一套全面的功能，分为以下几类：

### 表单创建和创作 {#form-creation}

使用各种创作选项创建有吸引力、响应式、数据驱动的表单：

| 功能 | 描述 |
|---|---|
| 自适应表单 | 为您的网站、应用程序和其他数字和打印渠道创建和管理交互式、动态性、响应式、便于移动设备使用和数据驱动的表单： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html"> 创建自适应表单 </a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/themes.html">设置自适应表单的样式</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html?lang=zh-Hans">将自适应表单添加到 AEM Sites 页面</a></li></ul> |
| 用于表单的 Edge Delivery Services | 创建并投放带来卓越用户体验的高性能表单： <ul><li><a href="/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md">使用通用编辑器进行所见即所得的创作</a> - 用于生成表单的强大的可视化界面</li><li><a href="/help/edge/docs/forms/create-forms.md">基于文档的创作</a> - 使用 Microsoft Excel 或 Google Sheets 等熟悉的工具创建表单</li><li>用于创建复杂表单逻辑的高级规则编辑器</li><li>通过优化表单加载获得近乎完美的 Google Lighthouse 分数</li><li>以最少的开发时间更快地部署表单</li></ul> |
| 自动化表单转换服务 | 将基于 PDF 的旧版表单转换为可轻松进行在线管理和分发的自适应表单： <ul><li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html">配置自动化表单转换服务</a></li><li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html?lang=zh-Hans">将 PDF 表单转换为自适应表单</a></li></ul> |

### 文档处理和通信 {#document-processing}

生成、汇编和传递个性化通信：

| 功能 | 描述 |
|---|---|
| 通信 API | 使用 RESTful API 按需或按预定时间间隔自动创建、管理和传递数据驱动的个性化通信： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-generation"> 生成个性化的通信 </a> </li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-manipulation"> 汇编或拆分 PDF 文档 </a> </li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#convert-to-and-validate-pdf%2Fa-compliant-documents">创建符合 PDF/A 标准的文档 </a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html">使用 DocAssurance API 保护您的文档</a></li></ul> |
| 记录文档 | 创建和管理已提交表单的记录，以确保存档和合规： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html"> 创建表单记录以进行长期存档</a></li><li>自定义功能的服务器端可扩展性</li><li>确保防篡改档案的文档记录功能</li></ul> |

### 工作流和流程自动化 {#workflow}

自动业务流程和表单相关的工作流：

| 功能 | 描述 |
|---|---|
| 表单工作流 | 涉及表单和文档服务的自动业务流程： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms.html">发送表单或文件以供审查</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#assign-task-step">创建审批拒绝工作流</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br"> 将数据提交到数据存储或工作流</a></li></ul> |
| 电子签名 | 与 Adobe Sign 和 Adobe Sign Solutions for Government 集成，轻松向用户发送表单和文档以进行电子签名： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html">使用 Adobe Sign 对自适应表单进行电子签名</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#generate-document-of-record-step">将记录文档</a>或<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#sign-document-step">电子签名</a>步骤添加到业务流程</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?lang=zh-Hans#sign-document-step">使用 Adob&#x200B;e Sign 和 AEM 工作流对文档进行电子签名</a></li></ul> |

### 数据集成与分析 {#data-integration}

将表单连接到数据源，洞察表单性能：

| 功能 | 描述 |
|---|---|
| 表单分析 | 使用 Adobe Analytics 获取有关用户行为和偏好设置的有用洞察： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.html">将自适应表单与 Adobe Analytics 连接</a></li></ul> |
| Adobe 集成 | 将表单与其他 Adobe 解决方案连接： <ul><li><a href="/help/forms/submit-adaptive-form-to-workfront-fusion.md">连接到 Adobe Workfront Fusion</a> 并将数据提交到 Workfront 场景</li><li><a href="/help/forms/integrate-form-to-marketo-engage.md">连接到 Adobe Marketo Engage</a> 并<a href="/help/forms/submit-adaptive-form-to-marketo-engage.md">将数据提交到 Marketo</a></li></ul> |
| Microsoft 集成 | 将表单与 Microsoft 服务连接： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=zh-Hans">与 Microsoft® Dynamics 365 连接</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html?lang=zh-Hans">连接到 Microsoft® Azure Blob 存储</a>并<a href="/help/forms/configure-submit-action-azure-blob-storage.md">将数据提交到 Azure Blob 存储</a></li><li><a href="/help/forms/connect-forms-to-sharepoint-document-library.md">连接到 Microsoft® SharePoint 文档库</a>，并<a href="/help/forms/configure-submit-action-sharepoint.md">将数据提交到 SharePoint</a></li><li><a href="/help/forms/configure-submit-action-onedrive.md">连接到 Microsoft® OneDrive</a> 并将数据提交到 OneDrive</li><li><a href="/help/forms/forms-microsoft-power-automate-integration.md">连接到 Microsoft® Power Automate</a> 并在表单提交时触发数据流</li><li><a href="/help/forms/ms-dynamics-odata-configuration.md">连接到 Microsoft® Dynamics OData</a></li></ul> |
| 其他数据源 | 连接到其他数据源和端点： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html?lang=zh-Hans">连接到 RDBMS 或 Rest 端点</a></li><li><a href="/help/forms/aem-forms-salesforce-integration.md">连接到 Salesforce</a> 并将数据提交到 Salesforce</li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#submit-to-rest-endpoint">提交到 REST 端点</a></li></ul> |

## AEM 中的 AI 助手

对于已[满足先决条件](/help/implementing/cloud-manager/ai-assistant-in-aem.md#get-access)的客户，AEM 中的 AI 助手可供其组织的用户使用。参见 [AEM 中的 AI 助手](/help/implementing/cloud-manager/ai-assistant-in-aem.md)。

>[!MORELIKETHIS]
>
>* [创建自适应表单](/help/forms/creating-adaptive-form-core-components.md)
>* [Cloud Service 环境上线](/help/forms/setup-forms-cloud-service.md)
>* [设置本地开发环境](/help/forms/setup-local-development-environment.md)
>* [从 AEM 6.5 Forms 迁移到 Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)
