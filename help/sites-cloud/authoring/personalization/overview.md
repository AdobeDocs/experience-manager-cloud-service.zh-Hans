---
title: 个性化和内容定位
description: 了解如何使用AEM创建个性化的目标内容
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: 635a9e577f03c865cdb31f539598fb8fe034d7b7
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 12%

---


# 个性化和内容定位 {#personalization-and-content-targeting}

个性化您向客户提供的Web内容，意味着根据客户的兴趣和需求定制这些体验。 你可以根据你掌握的关于他们的信息来做到这一点；例如，购物摘要、年龄、性别、地理等。

使用Adobe Experience Manager as a Cloud Service(AEM)，您可以创建一系列内容，然后指定哪些受众（最终用户群组）将看到各个体验。 这意味着您要定位特定受众的个性化体验。

当您的读者联机时，您的定位引擎将查看有关最终用户的可用信息，并将其与体验定义进行比较。 然后引擎 *&quot;decigned&quot;* 应该显示哪个个性化体验。

AEM提供了以下工具框架：

* 根据可用的客户信息，创作适合各种受众的目标内容。
* 定义用于根据受众定义解析已知用户信息的规则。
* 配置页面以呈现有针对性的个性化体验；以呈现适用于当前最终用户的特定内容。

以下概述介绍了在AEMas a Cloud Service中用于个性化的一些术语，然后是建议的操作顺序。

## 体验 {#experience}

体验是您希望向最终用户显示的内容。

## 个性化体验 {#personalized-experience}

个性化体验是指向有限受众显示的体验。 受众由您定义，并且仅在有关当前最终用户的已知信息与该受众定义相对应时，才显示内容。

在创建页面时，您可以定义多个体验，每个体验都解析为一个（或多个）受众。 如果未解析受众，则会显示默认体验。

### 提供 {#offer}

<!-- not clear - needs clarification -->
<!-- is an offer a personalized experience, or an activity? -->

选件是个性化体验，通常在有限的时间段内提供。

例如，来自示例网站的页面可以使用选件作为显示在页面顶部的Teaser图像。 30岁以上的人员和30岁以下的人员将看到不同的选件作为体验预告。

## 受众 {#audience}

受众是一组最终用户，您想要通过个性化内容进行定位。 当访客打开网页时，页面逻辑会根据已知信息确定他们所属的受众。 基于该评估AEM显示您为该受众创建的内容。

受众基于营销区段。 它们是在AEM或Adobe Target中创建的；您可以使用“受众”控制台直接在AEM中创建Adobe Target受众。

### 区段 {#segment}

在AEM ContextHub中，受众根据规则（条件）定义为区段。 然后，将解析这些内容以渲染所需内容。

## 活动 {#activity}

活动：

* 定义特定受众（区段）与特定体验的映射
* 定义应用定位的时间段
* 标识 [定位引擎](#targeting-engine) 您的页面使用

<!-- an example for each of the two types would be good -->

活动可以是个性化活动或A/B测试活动(对于AEM和Adobe Target个性化工作流)。

例如，活动可以为两个不同的受众定义体验：30岁以上的人和30岁以下的人。 随后，网站的某个页面可能会针对每个受众显示不同的产品。

或者，再举一个示例，您的产品目录可能包含关注季节性产品的Teaser。 因此，夏季体育活动可以定义Teaser在夏季月份定位的受众。

使用 [活动控制台](/help/sites-cloud/authoring/personalization/activities.md) 创建和管理 [品牌](#brand). 您还可以在创作活动时创建活动 [目标内容](/help/sites-cloud/authoring/personalization/targeted-content.md) with [定位模式](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode).

### 品牌 {#brand}

品牌包含一系列营销活动和区域。

使用“活动”控制台创建品牌时，该品牌也会显示在“选件”控制台中。

### 区域 {#area}

区域是品牌的分支。

## 定位模式 {#targeting-mode}

创作时，这是用于激活和配置个性化组件的编辑模式。

您可以 [创作目标内容](/help/sites-cloud/authoring/personalization/targeted-content.md) 使用AEM的“定位”模式。 定位模式和 Target 组件提供了一些工具，用于为您的营销活动体验创建内容。

## 体验片段 {#experience-fragments}

构成体验的分组组件集。

[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) 由内容和信息（样式等）构成，用于创建体验；在页面创作时可直接使用这些参数。 它们可以被视为AEM页面的子集。 它们允许内容作者跨渠道重复使用内容，包括站点页面和第三方系统。

对于个性化示例，可以将标题、图像、描述和行动动员按钮组合在一起，以形成Teaser体验。 使用体验片段是使用Adobe Target个性化的一个关键部分。

## 定位引擎 {#targeting-engine}

定位引擎是解析目标内容逻辑的机制。 [活动](/help/sites-cloud/authoring/personalization/activities.md)会配置为使用以下两个可用的定位引擎之一：AEM 和 Adobe Target。

定位引擎是决定要使用哪个个性化系统的平台或机制。

当前AEM可以使用：

* [AEM ContextHub](#aem-contexthub) (标准AEM)
* the [Adobe Target](#adobe-target) 个性化引擎

>[!CAUTION]
>
>单个AEM页面不能同时使用两个引擎。
>
>您可以在同一网站的不同页面上同时使用这两个引擎。

### AEM ContextHub {#aem-contexthub}

AEM提供内置定位引擎ContextHub，用于处理页面请求并确定要显示的内容。 使用 AEM 定位引擎时，您仅可使用在 AEM 中创建的区段来定义体验受众。

### Adobe Target {#adobe-target}

Adobe Target 定位引擎允许从 Adobe Target 中跟踪的页面访问收集信息。

* 使用此定位引擎时，您可以使用从 Adobe Target 导入的区段来定义体验受众。
* 使用 Adobe Target 引擎的活动会[同步到 Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target)。

您可以在 [与Adobe Target集成](/help/sites-cloud/integrating/integration-adobe-target-ims.md).

## 如何设置个性化内容 {#how-to-setup-personalized-content}

提供个性化内容需要执行各种步骤和定义：

1. 将AEM与您的定位引擎集成。

1. 配置受众。

   1. 根据您的定位引擎，定义受众或区段，以及规则。

1. 创建您的品牌和活动。

1. 创作您要向各个受众显示的所选体验。

1. 通过将这些体验定位到特定受众（区段），将其个性化。