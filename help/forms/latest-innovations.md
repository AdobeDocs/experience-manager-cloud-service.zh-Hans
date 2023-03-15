---
title: 了解Adobe Experience Manager Formsas a Cloud Service的最新创新。
description: “了解 [!DNL AEM Forms] as a Cloud Service创建、管理和发布企业级表单和业务流程。”
exl-id: 3a90b0aa-369a-4350-9904-79ef656b0f9a
source-git-commit: 7221e240b57bad20dd7a66dc8e8fcb9001f4ed10
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

<!-- # Introduction to [!DNL AEM Forms] as a Cloud Service {#overview}

Adobe Experience Manager Forms as a Cloud Service offers a cloud-native, Platform as a Service (PaaS) solution for businesses to create, manage, publish, and update complex digital forms while integrating submitted data with back-end processes, business rules, and saving data in an external data store. The service is always current, always available, and always learning.

You can use the service to create and rollout  interactive and engaging digital forms. For example, an organization is looking to digitize their customer enrollment journey. They have multiple data sources with existing customer data, they are looking to pre-populate forms, add e-sign their forms, and archive filled forms as PDF files. Besides, the organization has multiple print forms (PDF forms), they are also looking to convert all of their print forms to digital forms.

The organization can use [!DNL AEM Forms] as a Cloud Service to create digital forms, connect forms to existing data sources, integrate forms with [!DNL Adobe Sign] to add e-signatures to forms, and generate Document of Record (DoR) to archive filled forms as PDF files. The organization can also use the service to convert their existing PDF forms to digital forms. 

An organization can sign up for [!DNL AEM Forms] as a Cloud Service and start using all these features without waiting to buy and set up a local infrastructure. The service also frees the organizations from the cycle of upgrades as it is always up to date and always offers the latest feature.  -->


# 顶级Adobe Experience Manager Forms创新 {#latest-innovations}

Adobe Experience Manager Forms的一些顶尖创新包括：

| 创新 | 详细信息 |
|---|---|
| 无头自适应Forms | 创建和管理 [无头自适应Forms](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 在Adobe Experience Manager平台中。 使您的开发人员能够创建、发布和管理可通过API访问和交互的交互式表单，而不是通过传统的图形用户界面。 <br/> <br/> 这些表单旨在无需传统的HTML表单界面即可提交。 换言之，它们允许您通过API或后端代码以编程方式提交表单数据，前端包含任何可见的表单元素，前端不包含任何可见的表单元素。 <br/> ![](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/assets/how-headless-adaprive-forms-work.png?)<br/> 无头表单在多种情况下非常有用，例如在构建单页应用程序、渐进式Web应用程序或移动应用程序时，传统的HTML表单界面可能不是必需的或实用的。 无头表单允许开发人员直接通过API或后端代码提交表单数据，从而帮助简化工作流程并提高Web应用程序的整体性能。 |
| 核心组件 | 的 [自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) 是一组24个符合BEM规范的开源组件，这些组件基于Adobe Experience Manager WCM核心组件构建。 它们专门用于创建自适应Forms，自适应Adaptive Manager是根据用户的设备、浏览器和屏幕大小而调整的表单。 <br/> <br/>利用这些组件，可提供一系列广泛的表单字段选项（包括文本字段、复选框、下拉菜单等）来创建卓越的数据捕获和注册体验。这些功能还包括验证、条件逻辑和响应式设计等功能，可用于创建用户友好且易于使用的表单。 <br/> ![](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/assets/sample-core-components-based-adaptive-form.png?)<br/>此外，由于这些组件是开源的，因此，开发人员能够轻松定制和扩展组件以满足其组织的特定需求。而且，这些组件基于 BEM 方法而构建，这确保了它们可扩展且可维护。 |
| Microsoft PowerAutomate Connector | AEM Forms Power Automate Connector允许您将Adobe Experience Manager(AEM)Forms与Microsoft Power Automate(以前称为Microsoft Flow)相集成。 Power Automate（电源自动化）是一项基于云的服务，它允许您在不同的应用程序和服务之间创建自动工作流。  <br/> <br/> 借助AEM Form Power Automate Connector，您可以创建根据提交自适应表单自动触发的工作流。 例如，您可以创建一个工作流，在用户提交表单时自动向特定人员发送电子邮件通知，或在用户完成表单时在Microsoft Planner中创建任务。  <br/> ![](https://powerusers.microsoft.com/t5/image/serverpage/image-id/182924i17C4BEA1C045D731/image-size/large/is-moderation-mode/true?v=1.0&amp;px=999) <br/> AEM Forms Power Automate Connector是一款功能强大的工具，它使您能够自动化Adaptive Forms并与与Microsoft Power Automate连接的其他应用程序和服务集成，从而允许您使用更多工具。 您可以创建根据您的特定需求量身定制的工作流，并能够添加自定义操作、条件和触发器。 此外，电源自动化提供详细的分析和报告功能，让您能够监控和优化一段时间的工作流。 |
| Microsoft Storage Connectors | AEM Forms Microsoft Storage Connectors for <a href="https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#submit-to-sharedrive">OneDrive</a>, <a href="https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?#submit-to-sharedrive"> SharePoint, </a> 和 <a href="https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?#submit-to-azure-blob-storage"> Azure Blob存储 </a> 是连接器，允许您将Adobe Experience Manager(AEM)Forms与Microsoft OneDrive和SharePoint集成。 使用此连接器，您可以直接从自适应Forms将数据文件和附件上传到OneDrive和SharePoint。 <br/> ![](/help/forms/assets/onedrive-and-sharepoint.jpg) <br/>OneDrive和SharePoint可以与其他业务应用程序集成，如CRM系统、会计软件和项目管理工具。 这使您能够简化业务流程、减少手动数据输入并提高整体效率。 |
| 向导UI | 自适应Forms向导UI是一款功能强大的工具，可快速轻松地创建自适应表单。 其用户友好界面和自定义选项使所有用户都能够访问该界面，而无论其技术专业水平如何。 <br/> <br/> 向导UI通过引导用户逐步完成表单创建过程，简化了创建自适应表单的过程。 向导 — UI分为多个选项卡，每个选项卡都清楚地提供了配置自适应表单的选项。 表单作者以线性方式在选项卡之间进行访问，以选择表单组件的模板、提交操作和数据源等选项。 <br/> ![](/help/release-notes/assets/wizard.png) <br/>向导界面可简化发现自适应表单所有基本选项的过程，并且更便于创建表单，即使对于不熟悉该技术的用户也是如此。 |
| Adobe Analytics，带有Forms的Experience Cloud设置自动化 | 表单分析可通过测量用户参与度、优化转化率、监控表单性能和改善用户体验，为表单性能提供有价值的分析。  通过跟踪用户行为和反馈，分析可以识别表单中导致失望或混淆的区域，从而指导对表单设计和功能的改进。 <br/> <br/> 通过使用，您可以通过翻转几个按钮来启用“Experience Cloud设置自动化”Adobe Analytics。 它允许您将AEM Formsas a Cloud Service与Experience Platform标记和Adobe Analytics连接，以捕获和跟踪已发布表单的性能量度。 <br/> <br/> ![](/help/forms/assets/forms-analytics-report.png) <br/><br/> Formsas a Cloud Service提供了Adobe Analytics报表OOTB。 它有助于您轻松了解表单的性能。 通过表单级别的量度，您可以深入了解表单如何对多个关键绩效指标(KPI)执行操作，如演绎版、访客、提交、平均填充时间。 <br/> <br/> 它还提供有关用户访问面板中字段的上下文内帮助的平均次数的详细信息，以帮助您确定在提供信息之前让用户停止和搜索信息的字段。 您可以进一步简化此类字段或帮助内容以提高转化。 |
| 下一代复合性 | 借助新一代复合功能，您企业中的员工可以在其首选工具(如Microsoft Excel和Google工作表)中创建表单，而无需对新的UI工作流进行广泛的培训。 <br/> <br/> 此外，新一代复合功能旨在以无与伦比的速度加载表单，在实时页面上实现近乎完美的Google灯塔得分，从而保证最佳性能和用户体验。<br/> <br/> ![](/help/forms/assets/web-vitals.jpeg) 此外，由于新一代复合功能提供的简单工具，部署表单从未像现在这样容易、更快。 只需极短的开发时间，您就可以轻松简化上线路，并为客户提供卓越的表单体验。 |
