---
title: AEM Forms as a Cloud Service 简介
description: 了解用于创建自适应表单、自动化工作流和管理数字文档的AEM Forms功能。 完整的表单驱动业务流程平台。
landing-page-description: 了解如何使用AEM Forms as a Cloud Service创建自适应表单、处理文档和自动化业务工作流。
keywords: AEM Forms，自适应表单，表单生成器，数字表单，工作流自动化，文档服务，表单数据模型
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
index: false
exl-id: 50d7ce19-7d76-4ea1-a54c-8ca0e5379982
source-git-commit: eca09e1bf2ba4466f54e915e01218cc89cf5b116
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 0%

---

# AEM Forms as a Cloud Service 简介 {#introduction}



Adobe Experience Manager Forms as a Cloud Service为创建、管理和优化数字表单体验提供了一个全面的平台。 企业使用AEM Forms将基于纸面的流程数字化，创建响应式Web窗体，自动化文档工作流，以及大规模提供个性化通信。

该平台将表单创作功能与强大的后端服务相结合，使您能够构建从简单的联系表单到复杂的多步业务应用程序的所有内容。 使用云原生架构，您无需管理基础架构即可获得自动更新、弹性扩展和企业级安全性。

本指南介绍围绕整个表单生命周期（从初始设计到持续优化）组织的核心功能。

## AEM Forms的新增功能 {#whats-new}

**最新发行亮点：**

- **日期和时间输入组件** — 通过日历和时钟接口增强了用户输入，以实现精确的日期和时间选择
- **增强的文件上传安全性** — 自动验证和内容类型检查以防止不支持的文件格式
- **改进的错误处理** — 通过自定义提交操作的特定错误代码更好地调试
- **记录文档增强** — 用于排除隐藏字段的选项，以便生成更干净的文档

**预发行版功能：**

- **AFP格式支持** — 具有通信API的企业级打印功能
- **规则编辑器增强功能** — 现代JavaScript支持、动态变量和上下文感知面板规则
- **增强的验证方法** — 具有更高弹性的面板、字段和表单级验证

[查看完整的发行说明→](/help/release-notes/release-notes-cloud/release-notes-current.md#forms)

## 抢先体验计划 {#early-access}

在尖端的AEM Forms创新技术正式推出之前，先获得这些技术的独家访问权。

**当前早期访问功能：**

- **AEM Forms AI助手** — 用于自动表单创建、面板生成和优化推荐的创作AI
- **涂写签名组件** — 使用鼠标、手写笔或触摸屏在表单中直接捕获签名
- **直接API集成** — 无需设置表单数据模型即可连接到规则编辑器中的API
- **Forms优化** - AI支持的性能分析和转化率改进建议

**加入计划：**
成为首批访问创新并帮助塑造AEM Forms未来的企业之一。

[请求访问→](mailto:aem-forms-ea@adobe.com) | [了解详情→](/help/forms/early-access-ea-features.md)


## 核心功能 {#core-capabilities}

AEM Forms支持从初始创建到持续优化的完整数字表单历程。 每个阶段都以上一个阶段为基础，为表单驱动的业务流程创建一个全面的平台。

**AEM Forms工作流历程：**

    创建→管理→发布→捕获→进程→集成→跟踪→存档→改进
    ↓        ↓        ↓         ↓         ↓         ↓          ↓       ↓        ↓
    设计   审核   部署   收集   句柄   连接   监视器存储   优化
    ↑                                                                              ↓
    ←←←←←←←←←←←←←←←持续改进循环←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←

### 创建：表单设计和开发 {#create}

使用针对不同需求和技术要求的多种创作方法构建自适应表单。

**可视化表单生成器**
使用[核心组件](/help/forms/creating-adaptive-form-core-components.md)、[基础组件](/help/forms/creating-adaptive-form.md)或[Edge Delivery Services](/help/edge/docs/forms/overview.md)通过拖放界面设计响应式表单。 可视编辑器提供即时反馈，同时保持跨设备和辅助技术工作的简洁语义标记。

**基于文档的创作**
通过[Edge Delivery Services](/help/edge/docs/forms/overview.md)使用熟悉的工具(如Microsoft Excel)创建表单。 这种方法使内容创作者无需技术专业知识即可构建高性能表单，同时获得优异的Google Lighthouse分数。

**模板和主题**
使用定义结构和初始内容的预建[模板](/help/forms/template-editor-core-components.md)加速表单创建。 应用与[主题](/help/forms/using-themes-in-core-components.md)一致的品牌，这些主题控制多个表单中的视觉样式，从而确保设计的一致性并缩短开发时间。

**数据集成**
在设计阶段将表单连接到后端系统。 [表单数据模型](/help/forms/create-form-data-models.md)提供了到多个数据源的统一接口，启用了[预填充](/help/forms/prepopulate-adaptive-form-fields.md)、[验证规则](/help/forms/rule-editor-core-components.md)以及表单与业务系统之间的无缝数据流。

**验证和条件逻辑**
实施[条件逻辑](/help/forms/rule-editor-core-components.md)、渐进式披露和自适应验证以引导用户完成复杂流程。 [保存和恢复功能](/help/forms/save-core-component-based-form-as-draft.md)允许用户跨多个会话完成表单。

**HTML5 Forms**
将基于XFA的表单渲染为适用于移动设备和旧版浏览器的[HTML5表单](/help/forms/introductionhtml5.md)。 HTML5 Forms提供了无需插件的原生移动体验，同时维护表单逻辑和原始XDP模板中的验证。

**交互式通信**
使用可视编辑器创建以文档为中心的通信，如语句、发票和通知。 [交互式通信](/help/forms/interactive-communication/create-interactive-communication.md)将静态内容与动态数据相结合，以生成跨打印和数字渠道的个性化通信。

### 管理：审查和法规遵从性 {#govern}

建立监督和批准流程，确保表单满足组织标准和监管要求。

**基于工作流的审批**
通过具有基于角色的分配的多步审阅流程来路由表单设计。 利益相关者可以在发布之前[审核](/help/forms/create-reviews-forms.md)、[评论](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)和批准表单，并使用[AEM工作流](/help/forms/aem-forms-workflow.md)维护质量控制和合规性监督。

**版本管理**
跟踪表单版本并保持审核跟踪以确保法规遵从性。 内置[版本控制](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)确保您可以回滚更改、比较迭代和维护合规性审核的历史记录。

**访问控制和权限**
为表单创建、编辑和发布定义粒度权限。 [基于角色的访问](/help/forms/forms-groups-privileges-tasks.md)确保只有授权用户可以修改表单，同时保持敏感业务流程的职责分离。

### 发布：多渠道分发 {#publish}

跨多个渠道和接触点部署表单，以联系用户随时随地。

**全渠道发布**
将表单发布到[AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)、独立网页、移动应用程序，或[嵌入到第三方系统](/help/forms/embed-adaptive-form-core-components-external-web-page.md)。 单一源发布可确保一致性，同时适应不同的渠道要求。

**本地化和Personalization**
使用[AEM的翻译工作流](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md)以多种语言交付表单，同时支持[从左至右和从右至左的语言](/help/forms/right-left-languages.md)。 与Adobe Target集成以根据用户区段、行为或上下文数据个性化表单体验。

**性能优化**
利用Edge Delivery Services实现快如闪电的表单加载和最佳的SEO性能。 内容交付网络确保以最小的延迟实现全局可访问性。

**Forms门户**
创建集中式表单存储库，用户可以在其中发现、访问和管理表单。 [Forms Portal](/help/forms/configure-forms-portal.md)在统一界面中提供搜索功能、表单分类、草稿管理和提交跟踪，以增强用户体验。

### 捕获：用户体验和数据收集 {#capture}

优化表单填写体验，以最大限度地提高完成率和数据质量。

**响应式设计**
Forms会自动适应不同的屏幕大小和输入方法。 触屏优化控件、键盘导航和屏幕阅读器兼容性确保所有用户类型的[辅助功能](/help/forms/creating-accessible-adaptive-forms.md)。

**数字签名**
集成[Adobe Sign](/help/forms/working-with-adobe-sign.md)，以在表单体验中获取具有法律约束力的电子签名。 用户无需离开表单即可签署文档，从而简化审批流程并减少放弃情况。

**提交操作**
配置[提交操作](/help/forms/configure-submit-actions-core-components.md)以定义用户完成并提交表单时发生的情况。 将数据路由到电子邮件、数据库、工作流或外部系统，同时向用户提供即时反馈和确认。

### 流程：提交处理和路由 {#process}

利用强大的处理、验证和路由功能处理表单提交。

**数据验证和处理**
通过服务器端验证和自动化处理规则确保数据完整性。 在为用户生成回执、确认或跟进资料时，转换、验证和传送提交的数据。

**通信API**
通过[RESTful API](/help/forms/aem-forms-cloud-service-communications-introduction.md)以编程方式生成、处理和保护文档。 创建PDF、打印就绪格式、汇编文档、应用数字签名以及处理企业规模文档工作流的大量[批处理操作](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)。

**记录文档**
自动生成表单提交的PDF记录，以供合规性和用户确认。 [记录文档](/help/forms/generate-document-of-record-core-components.md)创建带提交数据的已填写表单的格式化、可打印版本，为交易和法规要求提供正式文档。

**工作流编排**
根据表单提交触发复杂的业务流程。 通过审批链传送数据，将任务分配给特定用户，并自动执行日常操作，同时保持审核跟踪。

**错误处理和恢复**
内置的重试机制和回退处理可确保不丢失任何提交。 全面的日志记录可帮助排查问题并维护服务级别协议。

### 集成：后端连接 {#integrate}

将表单连接到现有业务系统和数据源，以实现无缝的信息流。

**预建连接器**
与[Salesforce](/help/forms/configure-salesforce.md)、[Microsoft Dynamics](/help/forms/configure-msdynamics.md)、[SharePoint](/help/forms/connect-forms-to-sharepoint-document-library.md)和Adobe Experience Cloud解决方案的本机集成。 预建连接器可在确保可靠数据同步的同时缩短开发时间。

**RESTful API集成**
通过[提交操作](/help/forms/configure-submit-action-restpoint.md)或[数据集成](/help/forms/data-integration.md)，通过RESTful API连接到任何可访问Web的服务。 表单数据模型可抽象出集成的复杂性，从而提供一致的界面，而不管底层系统架构如何。

**实时数据交换**
实现表单与业务系统之间的双向数据流。 通过全面的[数据集成](/help/forms/data-integration.md)提交表单时，从现有记录中预填充表单、验证实时数据并同步更新多个系统。

### 跟踪： Analytics和性能监控 {#track}

通过全面的分析和监控了解表单性能和用户行为。

**表单分析**
通过[Adobe Analytics集成](/help/forms/integrate-aem-forms-with-adobe-analytics.md)跟踪完成率、放弃模式和字段级交互。 识别摩擦点、测量转化漏斗并了解不同区段中的用户行为。

**性能监控**
监控表单加载时间、提交成功率和系统性能。 实时功能板提供对技术运行状况和用户体验量度的洞察。

**Business Intelligence**
生成有关表单使用情况、提交卷和流程效率的报告。 Analytics为容量规划、用户体验优化和业务流程改进提供信息。

**交易报告**
监控AEM Forms部署中的API使用情况、文档生成卷和[可计费事务](/help/forms/transaction-reports-billable-apis.md)。 跟踪消费模式，优化资源分配，并遵守基于使用情况的许可要求。

### 存档：文档管理和法规遵从性 {#archive}

安全地存储和管理表单提交和生成的文档，以实现长期保留和法规遵从性。

**文档存储**
在AEM的数字资产管理系统中存储生成的文档和表单提交，或者与外部文档存储库(如[SharePoint](/help/forms/configure-submit-action-sharepoint.md)、[OneDrive](/help/forms/configure-submit-action-onedrive.md)或[Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md))集成。

**合规性和保留**
实施符合管理法规要求（包括GDPR、CCPA和HIPAA）的数据保留策略。 [自动存档流程](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)确保文档保留所需的时间，并在适当时安全处置。

**安全和访问控制**
将加密、数字签名和[基于角色的访问控制](/help/forms/forms-groups-privileges-tasks.md)应用于已存档的文档。 审核跟踪跟踪对文档访问和修改进行跟踪，以便进行合规性报告和安全监督。

### 改进：优化和增强 {#improve}

通过数据驱动的洞察和测试，持续优化表单性能和用户体验。

**A/B测试集成**
使用Adobe Target测试各种表单布局、字段排列和用户流。 统计分析有助于确定针对不同用户区段和用例的最有效方法。

**Analytics驱动的优化**
分析用户行为数据以确定改进机会。 [查看和了解热映射、字段交互分析和放弃模式识别的分析报告](/help/forms/view-understand-aem-forms-analytics-reports.md)，为迭代设计增强功能提供信息。

**迭代增强**
根据用户反馈、绩效指标和业务要求实施持续改进流程。 [版本控制](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)和回滚功能支持安全实验和快速迭代。

## 快速入门 {#getting-started}

您采取的方法取决于您的当前需求和长期目标。

### 快速入门：简单的Forms {#quick-start}

根据您的技术背景和性能要求选择首选的创作方法：

**可视化表单生成：**

1. **[使用核心组件创建自适应表单](/help/forms/creating-adaptive-form-core-components.md)**，用于新式响应式表单
2. **[配置提交操作](/help/forms/configure-submit-actions-core-components.md)**&#x200B;以处理表单数据
3. **[在AEM Sites中嵌入表单](/help/forms/embed-adaptive-form-aem-sites.md)**&#x200B;或通过直接链接共享

**基于文档的创作：**

1. **[使用Excel生成表单](/help/edge/docs/forms/create-forms.md)**&#x200B;搭配Edge Delivery Services生成高性能表单
2. **[发布到Edge Delivery](/help/edge/docs/forms/publish-forms.md)**&#x200B;以获得最佳加载速度和SEO

**旧表单支持：**

- 针对针对移动设备优化的XFA表单渲染的&#x200B;**[HTML5 Forms](/help/forms/introductionhtml5.md)**

### 高级实施：业务流程 {#advanced-implementation}

对于涉及多个系统、文档生成和批准工作流的复杂需求：

**数据集成和工作流：**

1. **[设置表单数据模型](/help/forms/create-form-data-models.md)**&#x200B;以连接后端系统
2. **[设计工作流流程](/help/forms/aem-forms-workflow.md)**&#x200B;以供审批和路由
3. **[配置Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md)**&#x200B;以测量性能

**文档服务和通信：**

1. **[实施通信API](/help/forms/aem-forms-cloud-service-communications-introduction.md)**&#x200B;以自动生成文档
2. **[创建交互式通信](/help/forms/interactive-communication/create-interactive-communication.md)**&#x200B;以提供个性化的报表和通知
3. **[设置Forms门户](/help/forms/configure-forms-portal.md)**&#x200B;以进行集中表单管理

### 企业部署：规模和治理 {#enterprise-deployment}

对于需要治理、法规遵从性和监控的组织范围的部署：

**架构和管理：**

1. **[查看体系结构模式](/help/forms/aem-forms-cloud-service-architecture.md)**&#x200B;以进行可扩展部署
2. **[配置用户管理](/help/forms/forms-groups-privileges-tasks.md)**&#x200B;和访问控制
3. **[为团队协作设置开发工作流](/help/forms/setup-local-development-environment.md)**

**迁移和监控：**

1. 从现有系统&#x200B;**[规划迁移策略](/help/forms/migrate-to-forms-as-a-cloud-service.md)**
2. **[实施事务监视](/help/forms/transaction-reports-billable-apis.md)**&#x200B;以跟踪使用情况并遵循相关规定

<details>
<summary><strong>❓常见问题</strong></summary>

**什么是表单生成器？**
表单生成器是一种允许您在不编码的情况下创建数字表单的工具。 您可以使用拖放界面设计表单、添加文本框和下拉列表等字段，并联机发布它们以从用户那里收集数据。

**如何创建在线表单？**
借助AEM Forms，您可以通过可视拖放编辑器使用核心组件创建自适应表单、使用Edge Delivery Services构建高性能表单，或将基础组件用于已建立的工作流。 首先，选择模板、添加表单字段、配置数据连接以及跨多个渠道发布。

**什么是好的在线表单？**
良好的在线表单具有移动响应性、加载速度快、标签清晰、使用逻辑字段排序、包含验证以防止错误并在提交时立即向用户反馈。

**能否将表单与其他业务系统集成？**
是的，现代表单生成器提供了广泛的集成功能。 您可以将表单连接到CRM系统、电子邮件营销平台、数据库、云存储以及工作流自动化工具，以简化您的业务流程。

**在线表单是否安全？**
专业表单构建器包括企业级安全功能，如数据加密、安全数据传输、访问控制，以及遵守GDPR 、 HIPAA和CCPA等法规以保护敏感信息。

**如何将电子签名添加到我的表单？**
数字签名可以使用Adobe Sign或其他电子签名提供商直接集成到表单中。 这允许用户在表单体验中签署文档，而无需单独的签名工作流并减少表单放弃。

**表单能否自动生成PDF文档？**
可以，现代化的表单平台可以在提交表单时自动生成PDF收据、确认或记录文档。 这对于法规遵从性、记录保留以及向用户提供即时确认至关重要。

**如何跟踪表单性能和分析？**
表单分析可帮助您了解完成率、放弃模式和用户行为。 与Adobe Analytics等Analytics平台集成后，可以深入了解哪些字段会导致摩擦以及如何优化转化率。

**什么是表单工作流自动化？**
表单工作流自动化通过审批流程传送提交，将任务分配给团队成员，并在其他业务系统中触发操作。 这消除了手动处理并确保了对表单数据的一致处理。

**如何使残障用户能够访问表单？**
[可访问的表单](/help/forms/creating-accessible-adaptive-forms.md)包括正确的标签、键盘导航、屏幕阅读器兼容以及符合WCAG准则。 这可确保所有用户都能完成表单，无论其能力或辅助技术如何。

**窗体生成器的费用是多少？**
AEM Forms as a Cloud Service的定价取决于您的特定要求、使用量和功能需求。 有关详细的定价信息并讨论为贵组织量身定制的解决方案，请联系Adobe销售人员或您的Adobe代表。

</details>

## 后续步骤 {#next-steps}

探索与您当前优先级相匹配的功能：

- **[构建您的第一个表单](/help/forms/creating-adaptive-form-core-components.md)**&#x200B;以体验创作环境
- **[查看架构选项](/help/forms/aem-forms-cloud-service-architecture.md)**&#x200B;以进行部署规划
- **[设置开发环境](/help/forms/setup-local-development-environment.md)**&#x200B;以进行团队协作
- **[浏览用于连接现有系统的集成选项](/help/forms/data-integration.md)**

有关全面的实施指南，请考虑Adobe Professional Services以加快部署并确保从一开始就使用最佳实践。
