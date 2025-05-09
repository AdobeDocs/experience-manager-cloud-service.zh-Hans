---
title: 将AEM Forms与Adobe Experience Platform (AEP)连接 | 数据集成指南
description: 了解如何将AEM Forms与Adobe Experience Platform集成以利用客户档案、提交表单数据和创建个性化体验。 分步指南。
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
source-git-commit: 052f8425c3c7bc2c12882af4f7b88d559ea34fb3
workflow-type: tm+mt
source-wordcount: '1551'
ht-degree: 1%

---


# AEM Forms与Adobe Experience Platform (AEP)的集成 {#aem-forms-aep-integration}

<span class="preview">将Adaptive Forms (AEM Forms)与Adobe Experience Platform (AEP)连接的功能属于早期访问计划。 若要请求访问功能，只需将电子邮件地址发送至[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D)即可。 您还可以访问<a href="/help/forms/early-access-ea-features.md">提前访问计划</a>页面以发现所有可用的创新和功能。. </span>

## 概述 {#overview}

您可以将AEM Forms与Adobe Experience Platform连接起来，以转换您的表单体验。 这种强大的集成使组织能够利用实时客户配置文件提供个性化的表单体验，简化向Experience Platform **提交** AEM Forms数据的过程，并在Adobe生态系统中创建统一的客户记录。 通过将您的自适应表单与Experience Platform强大的数据管理功能相连接，您可以创建更相关的体验并提高转化率，同时为客户数据维护单一的真实来源。

### 什么是Adobe Experience Platform的AEM Forms Connector (AEP)？ {#what-is-connector}

适用于Adobe Experience Platform的AEM Forms Connector (AEP)是由AEM Forms提供的现成(OOTB)连接器，可实现AEM Forms与Adobe Experience Platform (AEP)之间的无缝集成。 利用此集成，可使用AEP中可用的XDM架构创建表单，并将数据提交回AEP以进行个性化和配置文件水化。

## 为什么要将AEM Forms与Adobe Experience Platform (AEP)连接？ {#benefits}

将自适应Forms与Adobe Experience Platform连接可为贵组织和客户带来显着优势：

* **统一客户配置文件** — 使用表单提交数据丰富客户配置文件，创建客户交互和偏好设置的全面视图
* **个性化表单体验** — 利用现有配置文件数据预填充字段并根据已知的客户信息自定义表单
* **简化的数据收集** — 将表单数据直接捕获到AEP数据集，而无需生成自定义连接器或集成代码
* **实时数据激活** — 通过Real-Time CDP将表单提交数据发送到其他Adobe应用程序以立即激活
* **简化的合规性管理** — 通过AEP集中管理同意和数据治理策略
* **缩短开发时间** — 使用遵循最佳实践的预建连接器消除自定义集成工作
* **使用表单数据扩充客户配置文件** — 通过每次提交表单自动更新并增强客户配置文件，从而提供更丰富的客户洞察

## 主要功能 {#key-features}

* 使用AEP XDM架构创建表单
* 将表单数据提交到AEP以进行个性化
* 支持流式数据摄取
* 启用配置文件水合以增强用户体验
* 与AEP用户档案系统集成
* XDM架构与自适应表单集成，用于标准化数据收集
* 支持实时数据处理的AEP表单流连接

以下视频分步说明了先决条件（如创建架构、设置数据配置和身份验证），并展示了如何创建自适应Forms并将其连接到Adobe Experience Platform (AEP)

>[!VIDEO](https://video.tv.adobe.com/v/3457850/)

## 先决条件 {#prerequisites}

在AEM Forms中设置AEP连接器之前，请确保您已在Adobe Experience Platform中完成以下操作：

1. 架构设置
   * [创建XDM架构](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/tutorials/create-schema-ui)
   * [启用架构以进行分析](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)
   * [定义标识字段](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)

2. 数据配置
   * [创建数据集](https://experienceleague.adobe.com/zh-hans/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-datasets)
   * [设置流连接](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/ingestion/tutorials/create-streaming-connection) （稍后需要该流端点URL，因此请立即记下它。）

3. 身份验证
   * 从Adobe Developer Console [生成API凭据](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/landing/platform-apis/api-authentication#generate-credentials)（客户端ID和客户端密钥）


## 实施步骤

### 1.创建AEP云配置

1. 导航到您的&#x200B;**Adobe Experience Manager实例** > **工具** > **云服务** > **Adobe Experience Platform**。
1. 选择&#x200B;**配置容器**&#x200B;以存储配置。
1. 单击&#x200B;**创建**&#x200B;以打开AEP配置向导
1. 输入以下详细信息：
   * 标题
   * 客户端ID（从开发人员控制台获取）
   * 客户端密码（从开发人员控制台获取）
   * OAuth URL（有默认URL，但也可以从开发人员控制台获取）

1. 单击&#x200B;**连接**&#x200B;以建立连接。 建立连接后，配置以下附加设置：
   * 基本URL： platform.adobe.io （这是默认URL，也可以从开发人员控制台获取），将oauth和平台URL默认为生产URL。 在这种情况下，您需要连接到暂存 — 应使用暂存URL。)
   * 组织ID（这与客户端ID/密码一起从开发人员控制台获取）
   * 沙盒名称（开发和生产环境均需要）

### 2.使用XDM架构集成创建表单 {#form-creation}

1. 访问表单创建向导：
   * 导航到您的&#x200B;**Adobe Experience Manager实例** > **Forms** > **Forms和文档**。
   * 单击&#x200B;**创建** > **自适应表单**。
1. 在&#x200B;**源**&#x200B;选项卡中，选择一个模板
1. 在&#x200B;**数据**&#x200B;选项卡中，选择&#x200B;**Adobe Experience Platform**&#x200B;选项。

1. 在属性窗格中，选择您的云配置。 系统会从Adobe Experience Platform加载所有可用的架构

   >[!NOTE]
   >
   >
   > * 仅获取启用配置文件和非系统生成的架构。
   > * 首次设置时，初始架构加载可能需要一些时间。
1. 选择架构的相应/必填字段。 （有关详细步骤，请参阅视频）
1. 在提交选项卡中：
   * 选择&#x200B;**提交到Adobe Experience Platform**&#x200B;提交操作
   * 配置表单提交设置，以便将&#x200B;**AEM Forms数据提交到Experience Platform**
1. 在属性窗格中：
   * 添加流URL(从“AEP源”>“流连接”获取)
   * 添加数据流ID(可在AEP源>流> API使用信息中找到)
1. 单击&#x200B;**保存**。提供表单详细信息：
   * 标题
   * 名称
   * 存储路径
1. 将提交按钮添加到表单。 您的表单已准备好将数据提交到AEP。


## 重要说明 {#important-notes}

* 通过表单提交的数据在大约10-15分钟后会在AEP中可见
* 默认情况下，仅列出启用配置文件的架构
* 虽然数据提交适用于所有架构，但预填充功能仅限于启用个人资料的架构
* 不会使用未启用配置文件的架构中的数据来创建配置文件，即使稍后启用该架构进行性能分析也是如此
* **使用表单数据扩充客户配置文件**&#x200B;需要在XDM架构中正确配置标识字段
* 向Experience Platform提交&#x200B;**AEM Forms数据**&#x200B;使用&#x200B;**AEP表单流式连接**&#x200B;以确保实时数据流

## 最佳实践 {#best-practices}

1. 在启用性能分析之前，仔细规划架构结构
1. 为表单&#x200B;**设置** AEP流连接时，请考虑数据量和系统缩放要求
1. 在生产部署之前彻底测试集成
1. 监测数据摄取和配置文件创建过程
1. 设计您的&#x200B;**XDM架构与自适应表单**&#x200B;的集成，以便仅收集必要的数据
1. 策略性地将&#x200B;**客户配置文件扩充与表单数据**&#x200B;结合使用以增强个性化

## 技术注意事项 {#technical-considerations}

* 连接器使用公共流API提交数据
* 用户档案创建基于身份字段
* 数据统一在AEP中自动发生
* 该集成同时支持新表单创建和现有表单修改
* XDM架构与自适应表单的集成实现了不同接触点数据结构的标准化
* 适用于forms的AEP流连接提供实时数据摄取功能

## 常见问题解答（FAQ） {#faq}

### 一般问题 {#general-questions}

**问：“此连接器是否适用于AEM Forms的多个产品？**
答：不需要，此集成仅适用于AEM Forms as a Cloud Service，并且处于抢先访问计划下。

**问：此连接器是否可同时用于自适应Forms核心组件以及基础组件？**
答：此连接器可同时与自适应Forms核心组件和自适应Forms基础组件配合使用。

**问：能否从单个表单向多个AEP数据集发送数据？**
答：目前，每个表单只能提交到一个数据集。

**问：可处理的表单提交数量是否存在限制？**
答：表单提交受您的AEP流摄取[配额和速率限制](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/data-lifecycle/api/quota)的约束。

<!-- >
**Q: Can form attachments be sent to AEP?**
A: No, form attachments cannot be directly sent to AEP. You would need to store attachments separately and only send metadata to AEP. -->

### 实施问题 {#implementation-questions}

**问：如何解决AEM Forms与AEP之间的连接问题？**
答：验证云配置设置，确保API凭据正确，并检查流端点URL是否正确配置。

**问：能否将自定义XDM架构与此集成一起使用？**
答：是，您可以使用任何自定义XDM架构，前提是已在AEP中正确配置了该架构，并且为用户档案启用了预填充功能。

**问：如何使用AEP配置文件数据启用表单预填充？**
答：确保您的架构启用了配置文件，并且您的表单配置为使用在架构中定义的相同标识字段。

**问：如果在将数据发送到AEP之前需要转换数据，该怎么办？**
答：您可以使用表单规则或自定义函数在提交之前转换数据。 对于复杂的转换，请考虑使用自定义提交操作。

**问：我可以在混合部署模型中使用这个集成吗？**
答：不可以，此集成特定于AEM Forms as a Cloud Service。

## 摘要和后续步骤 {#summary-next-steps}

AEM Forms与Adobe Experience Platform集成使组织能够在表单与更广泛的Experience Platform生态系统之间创建无缝的数据流。 此集成使您能够构建更加个性化的表单体验，简化数据收集，并通过有价值的表单提交数据增强客户配置文件。

要开始使用此集成，请执行以下操作：

1. **请求访问** — 如果您尚未这样做，请联系[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D)以加入抢先访问计划
2. **准备环境** — 确保您在AEM Forms和Adobe Experience Platform中具有必要的权限和配置
3. **执行实施步骤** — 使用上面的指南设置云配置并创建第一个与AEP连接的表单与XDM架构集成
4. **彻底测试** — 在开发环境中验证数据提交和预填充功能
5. **生产计划** — 与您的实施团队合作，计划将AEM Forms数据提交到Experience Platform的生产部署

## 相关资源 {#related-resources}

* [AEM Forms as a Cloud Service文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=zh-Hans)
* [Adobe Experience Platform文档](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html?lang=zh-Hans)
* [XDM系统概述](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans)
* [在Adobe Experience Platform中流式引入](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=zh-Hans)
* [实时客户个人资料概述](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=zh-Hans)
* [AEM Forms抢先访问功能](/help/forms/early-access-ea-features.md)
* [使用核心组件创建自适应Forms](/help/forms/creating-adaptive-form-core-components.md)
* [在AEM Forms中使用表单数据模型](/help/forms/using-form-data-model.md)

<!--
Schema markup for technical documentation
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "headline": "Connect AEM Forms with Adobe Experience Platform (AEP) | Data Integration Guide",
  "description": "Learn how to integrate AEM Forms with Adobe Experience Platform to leverage customer profiles, submit form data, and create personalized experiences.",
  "datePublished": "2025-05-28",
  "author": {
    "@type": "Corporation",
    "name": "Adobe"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Adobe Experience League",
    "logo": {
      "@type": "ImageObject",
      "url": "https://experienceleague.adobe.com/assets/img/favicons/apple-touch-icon.png"
    }
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/aem-forms-aep-connector.html"
  },
  "articleSection": "AEM Forms",
  "keywords": "AEM Forms, Adobe Experience Platform, XDM schema, data integration, form submission, customer profiles, personalization"
}
-->


