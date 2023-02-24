---
title: ' [!DNL AEM Forms] as a Cloud Service 简介'
description: 探索 AEM Forms 并了解它如何帮助您生成业务就绪的文档和表单内容。了解 Platform-as-a-Service (PaaS)，如何管理企业级数字表单和业务流程，以及如何将 Forms 连接到当前数据源。
landing-page-description: 了解如何在 AEM as a Cloud Service 中使用表单。
exl-id: aa5ef10c-ba78-4a9d-8b2b-a72a7a306888
source-git-commit: f8e229820bb7aef3923e955c928033ef7d3d9460
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 33%

---

# 简介 {#introduction}

Adobe [!DNL Experience Manager Forms as a Cloud Service] 提供云原生的Platform as a Service(PaaS)解决方案，供企业创建、管理、发布和更新复杂的数字表单，同时将提交的数据与后端流程、业务规则进行集成，并将数据保存到外部数据存储中。 这项服务始终最新、可用，且在不断学习。

您可以使用该服务创建和推出交互式且具有吸引力的数字表单。例如，以一家希望将其客户注册过程数字化的企业为例。他们拥有多个包含现有客户数据的数据源，且希望预先填充表单、添加电子签名表单，并将填写的表单存档为 PDF 文件。此外，该企业有多种打印表单 (PDF 表单)，且还希望将所有打印表单转换为数字表单。

该企业可使用 [!DNL AEM Forms] as a Cloud Service 创建数字表单、将表单连接到现有数据源、将表单与 [!DNL Adobe Sign] 集成以将电子签名添加到表单、生成记录文档 (DoR)，从而将提交的表单存档为 PDF 文件。该企业还可使用该服务将现有的 PDF 表单转换为数字表单。

该企业可以使用 [!DNL AEM Forms] as a Cloud Service，在云中获得所有这些功能，而无需任何本地基础构架。这项服务还将企业从复杂的升级周期中解放出来，因为它会持续更新最新功能。

## 关键功能 {#key-features}

<!-- 
>[!BEGINTABS]

>[!TAB Adaptive Forms]

Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>

>[!TAB Automated Forms Conversion Service]

Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>

>[!TAB Communications API (Document Services)]

Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.

>[!TAB Advanced Analytics]

The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>


>[!ENDTABS] -->

| 自适应表单 | automated forms conversion服务 | 通信 API | Forms Analytics |
|---|---|---|---|
| 自适应Forms使企业能够为其网站和其他数字渠道创建和管理交互式数据驱动表单，以及响应式移动友好表单。 | automated forms conversion服务允许企业将基于PDF的旧式表单转换为可轻松在线管理和分发的交互式数字表单。 | 通信API是一组RESTful API（应用程序编程接口），使企业能够自动创建、管理和交付个性化的数据驱动通信。 | 该服务提供OOTB支持以连接Adobe Analytics。 将表单与Adobe Analytics连接为企业提供了多项好处，包括改进对用户行为的了解、更好地定位营销工作、减少错误状态、提高ROI。 |

<!--
| | |
|---|---|
| Adaptive Forms | Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>|
| Automated Forms Conversion Service | Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>|
| Communications API (Document Services) | Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.|
|Advanced Analytics| The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>|

-->

## 最新创新 {#latest-innovations}

>[!BEGINTABS]

>[!TAB 无头自适应Forms &#x200B;]

[无头自适应Forms](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 是用于在Adobe Experience Manager平台中创建和管理无头web表单的解决方案。 此功能使组织能够创建、发布和管理可通过API访问和交互的交互式表单，而不是通过传统的图形用户界面。 AEM无头自适应Forms允许在表单开发和部署中实现更大的灵活性和可扩展性，并通过根据特定需求定制表单设计和功能的能力改善用户体验。 通过利用AEM和无头技术的功能，此解决方案为创建、管理和部署适用于各种用例和应用程序的Web表单提供了一个强大的平台。


>[!TAB 核心组件]

的 [自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) 是一组24个符合BEM规范的开源组件，这些组件基于Adobe Experience Manager WCM核心组件构建。 它们专门设计用于创建自适应表单，后者是能够适应用户的设备、浏览器和屏幕大小的表单。

利用这些组件，可提供一系列广泛的表单字段选项（包括文本字段、复选框、下拉菜单等）来创建卓越的数据捕获和注册体验。它们还包括验证、条件逻辑和响应式设计等功能，可用于创建用户友好且易用的表单。

此外，由于这些组件是开源的，因此，开发人员能够轻松定制和扩展组件以满足其组织的特定需求。而且，这些组件基于 BEM 方法而构建，这确保了它们可扩展且可维护。


>[!TAB Microsoft PowerAutomate Connector &#x200B;]

Microsoft Power Automate Connector for AEM Forms是一个连接器，它允许您将Adobe Experience Manager(AEM)Forms与Microsoft Power Automate(以前称为Microsoft Flow)相集成。 Power Automate（电源自动化）是一项基于云的服务，它允许您在不同的应用程序和服务之间创建自动工作流。

借助AEM表单的电源自动连接器，您可以创建根据提交自适应表单自动触发的工作流。 例如，您可以创建一个工作流，在用户提交表单时自动向特定人员发送电子邮件通知，或在用户完成表单时在Microsoft Planner中创建任务。

使用AEM Forms的电源自动连接器具有许多好处，包括：

* **自动化**:您可以自动执行日常任务并简化流程，从而节省时间并减少错误。

* **集成**:该连接器允许您将Adobe Experience Manager Forms与其他应用程序和服务集成，从而允许您使用更多工具。

* **自定义**:您可以创建根据您的特定需求量身定制的工作流，并能够添加自定义操作、条件和触发器。

* **Analytics**:电源自动化提供详细的分析和报告，允许您随着时间的推移监控和优化工作流。

总的来说，AEM Forms的Power Automate Connector是一款功能强大的工具，它使您能够将AEM Forms自动化并与其他应用程序和服务集成，从而提高效率和生产效率。

>[!TAB Microsoft Storage Connectors:OneDrive和Sharepoint]

AEM Forms Microsoft OneDrive和SharePoint存储连接器是允许您将Adobe Experience Manager(AEM)Forms与Microsoft OneDrive和SharePoint集成的连接器。 通过这些连接器，您可以在Microsoft基于云的存储解决方案中存储和管理AEM Forms数据和文档。

这些连接器使您能够在Microsoft OneDrive中存储和管理AEM Forms数据和文档。 使用此连接器，您可以直接从AEM Forms将数据文件和附件上传到OneDrive和SharePoint。

使用AEM Forms Microsoft Storage Connectors for OneDrive和SharePoint具有以下几个好处：

* **集成**:这些连接器使您能够将AEM Forms与Microsoft基于云的存储解决方案相集成，从而让您能够利用这些平台的强大功能。

* **协作**:OneDrive和SharePoint是协作平台，使团队成员能够在文件和文档上协同工作。 通过将AEM Forms与这些平台集成，您可以改进协作和团队合作。

* **安全性**:OneDrive和SharePoint提供了强大的安全功能，可确保您的数据和文档的存储和访问安全。

总的来说，AEM Forms Microsoft Storage Connectors for OneDrive和SharePoint是功能强大的工具，使您能够在Microsoft基于云的存储解决方案中存储和管理AEM Forms数据和文档，从而改进协作和安全性。

>[!ENDTABS]

<!--

| | |
|---|---|
| Adaptive Forms | Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>|
| Automated Forms Conversion Service | Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>|
| Communications API (Document Services) | Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.|
|Advanced Analytics| The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>|

Adaptive Forms enable organizations to quickly design and deploy responsive, mobile-friendly forms without the need for extensive coding or development. With Adaptive Forms, businesses can create complex, multi-step forms with conditional logic, validations, and integrations with back-end systems such as CRMs and databases.

Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development.

In addition, AEM Adaptive Forms offer several other features, including:

Advanced workflows for routing, approval, and submission of form data
Real-time validation and error checking to ensure data accuracy
Integration with third-party data sources and APIs for pre-filling form fields or validating data
Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics
Overall, AEM Adaptive Forms provide businesses with a powerful tool for creating and managing complex, interactive forms that can be easily integrated into their digital experiences. |




| Feature/Capability | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms  | 
|---|---|---|
| Cloud-native architecture | &#x2611;  | &#x2612; |
| Auto-scaling based on load | &#x2611;  | &#x2612; |
| Zero downtime for upgrades | &#x2611;  | &#x2612; |
| Feature roll-out frequency | Agile*  | Quarterly |
| CDN (content delivery network) included | &#x2611;  | &#x2612; | 
| Topologies optimized for maximum resilience and efficiency| &#x2611;  | &#x2612; | 
| Cloud-native development environment | &#x2611;  | &#x2612; | 
| Self-Service via Cloud Manager | &#x2611;  | &#x2612; | 
| Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD) | &#x2611;  | &#x2612; | 
| Adaptive Forms | &#x2611; | &#x2611; | 
| Data Integration with multiple data sources| &#x2611; | &#x2611; | 
| Communications APIs (Document Services) | &#x2611;* | &#x2611; | 
| Automated Forms Conversion Service | &#x2611; | &#x2611; | 
| Integration with [!DNL Micosoft Power Automate] | &#x2611; | &#x2612; | 
| Integration with [!DNL Adobe Sign] | &#x2611; | &#x2611; | 
| Integration with [!DNL AEM Sites] | &#x2611; | &#x2611; | 
| Integration with [!DNL Adobe Launch] | &#x2611; | &#x2611; | 
| Integration with [!DNL Adobe Analytics] | &#x2611; | &#x2611; | 
| Easy connectivity with Microsoft Dynamics and Salesforce | &#x2611; | &#x2612; |
| Custom submit action for with [!DNL DocuSign] | &#x2611; | &#x2612; | 
| Microsoft Azure data store connector | &#x2611; | &#x2612; |
| Hardened Rule editor | &#x2611; | &#x2612; | 
| Forms Portal | &#x2611; | &#x2611; | 
| AEM Workflows | &#x2611; | &#x2611; | 
| Document of Record | &#x2611; | &#x2611; | 
| Adaptive Forms Wizard | &#x2611; | &#x2612; | 
| Custom XCI for Document of Record| &#x2611; | &#x2612; |
| Invisible Captcha | &#x2611; | &#x2611; |
| Reusable Form Data Model configurations | &#x2611; | &#x2611; |
| Acroform-based Document of Record | &#x2611; | &#x2611; | 
| Government ID based identity authentication for Adobe Sign enabled Adaptive Forms | &#x2611; | &#x2611; | 
| Document Security | &#x2612; | &#x2611; |


* [Notable changes in comparison to AEM 6.5 Forms](notable-changes.md)
* [Frequently asked questions](faq.md)

-->