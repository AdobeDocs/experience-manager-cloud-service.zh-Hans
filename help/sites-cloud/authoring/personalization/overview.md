---
title: 个性化和内容定位
description: 了解如何使用 AEM 创建个性化、有针对性的内容
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: f2466cb5cda759f0c97cd69810d208d47fb73b98
workflow-type: ht
source-wordcount: '1056'
ht-degree: 100%

---


# 个性化和内容定位 {#personalization-and-content-targeting}

您向客户提供的 Web 内容的个性化服务，即根据客户的兴趣和需求定制这些体验。 您可以根据掌握的关于客户的信息达成目标；例如，购物摘要、年龄、性别、地理位置等。

借助 Adobe Experience Manager as a Cloud Service (AEM)，您可以创建一系列内容，然后指定哪些受众（最终用户组）将看到每个单独的体验。这意味着您将针对特定受众提供个性化体验。

当您的读者在线时，您的定位引擎将查看有关最终用户的可用信息，并将其与体验定义进行比较。然后引擎&#x200B;*“决定”*&#x200B;应显示哪些个性化体验。

AEM 提供了用于以下情形的工具框架：

* 根据可用的客户信息，创作适合一系列受众的有针对性的内容。
* 定义用于根据受众定义解析已知用户信息的规则。
* 配置您的页面以呈现有针对性的个性化体验；呈现适用于当前最终用户的特定内容。

以下概述介绍了 AEM as a Cloud Service 中用于个性化的一些术语，以及推荐的操作顺序。

## 体验 {#experience}

体验是您希望向最终用户展示的内容。

## 个性化体验 {#personalized-experience}

个性化体验是向有限受众展示的体验。 受众由您定义，只有当有关当前最终用户的已知信息符合该受众定义时，才会显示内容。

创建页面时，您定义了多种体验，每种体验都针对一个（或多个）受众。 如果未解析任何受众，则会显示默认体验。

### 提供 {#offer}

优惠是一种个性化的体验，通常在有限的时间内提供。

例如，示例网站的页面可以使用选件作为在页面顶部显示的 Teaser 图像。30 岁以上的人和 30 岁以下的人将看到不同的优惠作为体验 Teaser。

## 受众 {#audience}

受众是您希望使用个性化内容定位的一组最终用户。 当访问者打开网页时，页面逻辑会根据已知信息确定他们所属的受众。 根据该评估，AEM 会显示您为该受众创建的内容。

受众基于营销市场细分。 它们是在 AEM 或 Adobe Target 中创建的；您可以使用受众控制台直接在 AEM 中创建 Adobe Target 受众。

### 市场细分 {#segment}

在 AEM ContextHub 中，受众被定义为基于规则（条件）的细分群体。 然后解析这些规则以呈现所需的内容。

## 活动 {#activity}

活动：

* 定义具有特定体验的特定受众（细分群体）的映射
* 定义应用定位的时间段
* 识别您页面使用的[定位引擎](#targeting-engine)

该活动可以是个性化活动，也可以是 A/B 测试活动（在 AEM 和 Adobe Target 个性化工作流程的情况下）。

例如，某项活动可定义针对两类不同受众的体验：30 岁以上的人群和 30 岁以下的人群。 网站页面可能会针对每类受众显示不同的产品。

或者，例如，您的产品目录可能包含关注季节性产品的 Teaser。 因此，夏季体育活动可能定义 Teaser 在夏季月份中定位的受众。

使用[“活动”控制台](/help/sites-cloud/authoring/personalization/activities.md)可为您的[品牌](#brand)创建和管理活动。 您还可以在使用[定位模式](/help/sites-cloud/authoring/personalization/targeted-content.md)创作[目标内容](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode)时创建活动。

### 品牌 {#brand}

品牌拥有一系列营销活动和区域。

当您使用“活动”控制台创建品牌时，它也会出现在“优惠”控制台中。

### 区域 {#area}

区域是品牌的细分市场。

## 定位模式 {#targeting-mode}

创作时，这是用于激活和配置个性化组件的编辑模式。

您[可使用 AEM 的定位模式创作目标内容。](/help/sites-cloud/authoring/personalization/targeted-content.md) 定位模式和 Target 组件提供了一些工具，用于为您的营销活动体验创建内容。

## 体验片段 {#experience-fragments}

构成体验的一组组件。

[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment)由内容和信息（样式等）组成以创造体验；它们可以在页面创作时直接使用。 它们可以视为 AEM 页面的子集。支持内容创作者可在渠道（包括 Sites 页面和第三方系统）间重用内容。

对于个性化示例，可以组合标题、图像、描述和号召性用语按钮以形成 Teaser 体验。使用体验片段是使用 Adobe Target 个性化的关键部分。

## 定位引擎 {#targeting-engine}

定位引擎是解析目标内容逻辑的机制。 [活动](/help/sites-cloud/authoring/personalization/activities.md)会配置为使用以下两个可用的定位引擎之一：AEM 和 Adobe Target。

定位引擎是决定使用哪个个性化系统的平台或机制。

目前 AEM 可以使用：

* [AEM ContextHub](#aem-contexthub)（标准 AEM）
* [Adobe Target](#adobe-target) 个性化引擎

>[!CAUTION]
>
>单个 AEM 页面无法同时使用两个引擎。
>
>您可以在同一站点的不同页面上使用这两个引擎。

### AEM ContextHub {#aem-contexthub}

AEM 提供了一个内置定位引擎 [ContextHub](/help/implementing/developing/personalization/contexthub.md)，用于处理页面请求并确定要显示的内容。 使用 AEM 定位引擎时，您仅可使用在 AEM 中创建的区段来定义体验受众。

### Adobe Target {#adobe-target}

[Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) 定位引擎允许从 Adobe Target 中跟踪的页面访问收集信息。

* 使用此定位引擎时，您可以使用从 Adobe Target 导入的区段来定义体验受众。
* 使用 Adobe Target 引擎的活动会[同步到 Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target)。

[与 Adobe Target 集成后](/help/sites-cloud/integrating/integrating-adobe-target.md)，您便可以使用此引擎。

## 如何设置您的个性化内容 {#how-to-setup-personalized-content}

交付个性化内容需要多个步骤和定义：

1. 通过以下任一方式设置您的定位引擎：

   1. 配置 [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md)
   1. 与 [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) 集成

1. 配置受众。

   1. 根据您的定位引擎，定义[目标受众](https://experienceleague.adobe.com/docs/target/using/audiences/target.html)或者 [ContextHub 区段](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)，以及规则。

1. 创建您的[品牌与活动](/help/sites-cloud/authoring/personalization/activities.md)。

1. 创作您希望向不同受众展示的体验选择。

1. 通过[定位](/help/sites-cloud/authoring/personalization/targeted-content.md)特定受众（细分市场），个性化这些体验。