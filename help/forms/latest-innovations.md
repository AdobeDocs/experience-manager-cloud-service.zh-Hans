---
title: Adobe Experience Manager Forms as a Cloud Service中有哪些最新创新？
description: 了解 [!DNL AEM Forms] as a Cloud Service创建、管理和发布企业级表单和业务流程的最新功能。
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
exl-id: 3a90b0aa-369a-4350-9904-79ef656b0f9a
source-git-commit: e08318cafacee3bad3eba7f1c51b4e8aa04c0776
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 8%

---

<!-- # Introduction to [!DNL AEM Forms] as a Cloud Service {#overview}

Adobe Experience Manager Forms as a Cloud Service offers a cloud-native, Platform as a Service (PaaS) solution for businesses to create, manage, publish, and update complex digital forms while integrating submitted data with back-end processes, business rules, and saving data in an external data store. The service is always current, always available, and always learning.

You can use the service to create and rollout  interactive and engaging digital forms. For example, an organization is looking to digitize their customer enrollment journey. They have multiple data sources with existing customer data, they are looking to pre-populate forms, add e-sign their forms, and archive filled forms as PDF files. Besides, the organization has multiple print forms (PDF forms), they are also looking to convert their print forms to digital forms.

The organization can use [!DNL AEM Forms] as a Cloud Service to create digital forms, connect forms to existing data sources, integrate forms with [!DNL Adobe Sign] to add e-signatures to forms, and generate Document of Record (DoR) to archive filled forms as PDF files. The organization can also use the service to convert their existing PDF forms to digital forms. 

An organization can sign up for [!DNL AEM Forms] as a Cloud Service and start using all these features without waiting to buy and set up a local infrastructure. The service also frees the organizations from the cycle of upgrades as it is always up to date and always offers the latest feature.  -->


# 顶级 Adobe Experience Manager Forms 创新 {#latest-innovations}

Adobe Experience Manager Forms中的一些热门创新包括：

| 创新 | 详细信息 |
|---|---|
| Edge Delivery | 借助Edge Delivery，企业内的员工可以在他们的首选工具(如Microsoft Excel和Google Sheets)中创建表单，而无需进行有关新UI工作流的广泛培训。<br/> <br/>此外，Edge Delivery旨在以无与伦比的速度加载表单，在实时页面上获得近乎完美的Google Lighthouse分数，从而保证出众的性能和用户体验。<br/> <br/> ![用于创建表单的新一代可组合性工具](/help/forms/assets/web-vitals.jpeg)此外，由于Edge Delivery提供了简单明了的工具，部署表单的过程从未像现在这样简单或快速。 只需最少的开发时间，您就可以轻松地简化上线的路径，并为客户提供卓越的外观体验。 |
| Adobe Workfront Fusion连接器 | [AEM Forms Adobe Workfront Fusion连接器](/help/forms/submit-adaptive-form-to-workfront-fusion.md)支持Adobe Experience Manager (AEM) Forms与Adobe Workfront Fusion之间的无缝集成。 Adobe Workfront作为工作管理应用程序，集中管理整个工作生命周期，而Workfront Fusion作为集成平台，促进Workfront与各种业务应用程序之间的连接。<br/> ![Adobe Workfront](/help/forms/assets/adobe-workfront.png) <br/> 使用 Adobe Workfront Fusion Connector，您可以设计在提交自适应表单时自动触发的工作流程。例如，设想一种场景，启动工作流程，为特定个人分配审查提交数据的任务，允许根据通过自适应表单捕获的信息批准或拒绝申请。这种简化的集成提高了效率，并将工作流过程的自动化水平提高到了一个新的水平。 |
| Headless自适应Forms | 在Adobe Experience Manager平台中创建和管理[Headless自适应Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=zh-Hans)。 使您的开发人员能够创建、发布和管理可通过API（而不是通过传统的图形用户界面）访问和交互的交互式表单。<br/> <br/>这些表单设计为无需传统的HTML表单界面即可提交。 换言之，它们允许您通过API或后端代码以编程方式提交表单数据，无论是否在前端有任何可见表单元素。<br/> <!-- ![Headless adaptive form working](https://experienceleagueadobe.com/docs/experience-manager-headless-adaptive-forms/assets/how-headless-adaprive-forms-work.png?) --><br/> Headless表单在各种情况下都很有用，例如，在构建单页应用程序、渐进式Web应用程序或移动应用程序时，传统的HTML表单界面可能不是必要或实用的。 通过允许开发人员直接通过API或后端代码提交表单数据，Headless表单有助于简化工作流并提高Web应用程序的整体性能。 |
| 核心组件 | [自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans#features)是基于Adobe Experience Manager WCM核心组件构建的一组24个开源、符合BEM的组件。 这些表单专为创建自适应Forms而设计，这些表单适用于用户的设备、浏览器和屏幕大小。<br/> <br/>这些组件可用于通过提供各种表单字段选项（包括文本字段、复选框、下拉菜单等）来创建卓越的数据捕获和注册体验。 它们还包括验证、条件逻辑和响应式设计等功能，可用于创建用户友好且易于使用的表单。<br/> ![核心组件的功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/sample-core-components-based-adaptive-form.png?lang=zh-Hans&)<br/>此外，由于这些组件是开源的，因此开发人员可以轻松自定义和扩展这些组件，以满足其组织的特定需求。 而且，这些组件基于 BEM 方法而构建，这确保了它们可扩展且可维护。 |
| Microsoft PowerAutomate连接器 | 通过AEM Forms Power Automate连接器，您可以将Adobe Experience Manager (AEM) Forms与Microsoft Power Automate(以前称为Microsoft Flow)集成。 Power Automate是一项基于云的服务，允许您在不同应用程序和服务之间创建自动化工作流。 <br/> <br/>借助AEM Form Power Automate连接器，您可以创建基于提交自适应表单自动触发的工作流。 例如，您可以创建一个工作流，在用户提交表单时自动向特定人员发送电子邮件通知，或者在用户完成表单时在Microsoft Planner中创建任务。 <br/> AEM Forms Power Automate Connector是一款功能强大的工具，可让您自动执行自适应Forms，并将其与与Microsoft Power Automate连接的其他应用程序和服务相集成，从而允许您使用更广泛的工具。 您可以创建根据特定需求定制的工作流，并能够添加自定义操作、条件和触发器。 此外，Power Automate提供详细的分析和报告，使您能够随着时间的推移监控和优化工作流。 |
| Microsoft存储连接器 | 适用于<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=zh-Hans#submit-to-sharedrive">OneDrive</a>、<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=zh-Hans&#submit-to-sharedrive"> SharePoint、</a>和<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=zh-Hans&#submit-to-azure-blob-storage"> Azure Blob存储</a>的AEM Forms Microsoft存储连接器允许您将Adobe Experience Manager (AEM) Forms与Microsoft OneDrive和SharePoint集成。 利用此连接器，您可以直接从自适应Forms将数据文件和附件上传到OneDrive和SharePoint。<br/> microsoft onedrive和sharepoint的![图标](/help/forms/assets/onedrive-and-sharepoint.jpg) <br/> OneDrive和SharePoint可以与其他业务应用程序集成，例如CRM系统、会计软件和项目管理工具。 这使您能够简化业务流程，减少手动数据输入，并提高整体效率。 |
| 向导用户界面 | 自适应Forms向导UI是一款用于快速轻松创建自适应表单的强大工具。 其用户友好的界面和自定义选项使所有用户都能够访问它，无论他们拥有何种程度的技术专业知识。<br/> <br/>向导UI通过逐步引导用户完成表单创建过程简化了创建自适应表单的过程。 向导UI分为多个选项卡，每个选项卡都清楚地提供了配置自适应表单的选项。 表单作者以线性方式浏览各个选项卡，以选择模板、提交操作以及表单组件的数据源等选项。<br/> ![表单创建向导的图像](/help/release-notes/assets/wizard.png) <br/>该向导界面简化了发现自适应表单的所有基本选项的过程，并使表单创建更容易，即使是不熟悉技术的用户也是如此。 |
| Adobe Analytics与Experience Cloud Setup Automation for Forms | 表单分析通过测量用户参与度、优化转化率、监控表单性能和改进用户体验，可以提供有关表单性能的宝贵见解。  通过跟踪用户行为和反馈，Analytics可以识别表单中导致挫折或混淆的区域，从而指导改进表单的设计和功能。<br/> <br/>通过使用，您可以[启用带有Experience Cloud Setup Automation的Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.html?lang=zh-Hans)，只需翻动几个按钮即可。 它让您能够将AEM Forms as a Cloud Service与Experience Platform标记和Adobe Analytics连接起来，以捕获和跟踪已发布表单的性能指标。<br/> <br/> ![自适应表单用户参与adobe analytics报告](/help/forms/assets/forms-analytics-report.png) <br/><br/> Forms as a Cloud Service提供Adobe Analytics报告OOTB。 它帮助您轻松地了解您表单的绩效。通过表单级量度，可深入分析表单在多个关键绩效指标(KPI)（如呈现版本、访客、提交、平均填充时间）上的执行情况。<br/> <br/>它还提供用户访问面板中字段的上下文帮助的平均次数详细信息，以帮助您确定在提供信息之前让用户停止和查找信息的字段。 您可以进一步简化此类字段，或帮助内容提高转化率。 |
