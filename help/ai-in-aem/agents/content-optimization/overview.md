---
title: 内容优化代理
description: 了解如何使用内容优化代理来转变用户如何通过应用自然语言说明创建渠道就绪型变体来优化和调整资产。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: ad027974400bdce3428ce96e8804abfe087b48da
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 0%

---


# 内容优化代理 {#content-optimization-agent}

内容优化代理通过应用自然语言指令创建渠道就绪变体，转变用户优化和调整资源的方式。 无论是为特定数字渠道生成新演绎版、调整视觉属性、更改背景还是准备资源，代理都会自动解释用户意图并执行复杂的编辑任务。 它与Discovery Agent无缝协作，利用其找到的资产并使用核心[Dynamic Media （具有OpenAPI功能](/help/assets/dynamic-media-open-apis-overview.md)）生成优化的变体，从而满足品牌、渠道和促销活动要求，而无需手动设计。

内容优化的一些主要优势包括：

* **轻松转换资产**：将简单、对话式的提示转换为精确的图像操作，例如调整大小、锐化、镜像或重新着色，从而无需专门的编辑工具。

* **渠道优化输出**：快速生成针对特定平台（如Instagram故事、Web横幅或其他营销接触点）的演绎版，确保资产随时可供立即使用。

* **大规模Creative增强功能**：应用视觉调整和增强功能，如背景更改或图形叠加，以支持大量创意工作流程，而不会减慢团队的工作速度。

* **[与发现代理无缝协作](/help/ai-in-aem/agents/discovery/overview.md)**：基于发现代理标识的资源进行构建，通过自然对话实现端到端资源检索和优化。

>[!IMPORTANT]
>
>AI生成的响应可能不准确或具有误导性。 请务必仔细检查建议的修复和响应。
>
>另请参阅[Adobe Experience Cloud Generative AI用户指南](https://www.adobe.com/cn/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)。

## 先决条件 {#prerequisites-content-optimization-agent}

要为图像资源生成变体或优化，请执行以下操作： 您必须具有：

* 有效的Dynamic Media许可证

* 在AEM as a Cloud Service环境中启用了OpenAPI的Dynamic Media 。

* AEM as a Cloud Service环境中处于[批准状态](/help/assets/manage-organize-assets-view.md#manage-asset-status)的资源。


## 技能 {#skills-content-optimization-agent}

内容优化代理提供以下技能：

* **通过自然语言了解意图**

  内容优化代理从自然语言提示、渠道、营销活动和受众上下文解释用户意图，以确定最相关的优化操作。

* **生成动态内容变体**

  内容优化代理创建优化的变体作为为不同渠道和格式类型定制的动态URL。

* **优化图像内容**

  内容优化代理应用格式转换、分辨率调整、裁剪和锐化等增强功能以提高图像质量。

* **多变体资源优化**

  内容优化代理可以使用单个自然语言提示从发现代理返回的资产生成多个优化的图像变体，使用户能够快速高效地生成适用于渠道的演绎版。

## 角色 {#personas-content-optimization-agent}

渠道营销人员（内容优化代理的关键角色）可以选择正确的高分辨率源内容，并请求针对其渠道和受众区段定制的优化格式。

区域营销人员和机构工作人员还可以使用内容优化代理快速生成可用于渠道的图像变体，从而支持更快、更一致的内容生产。

## 如何访问内容优化代理？ {#access-content-optimization-agent}

您可以通过AI助手访问AEM中的代理。 登录到experience.adobe.com ，通过使用`Ask AI Assistant anything`字段以自然语言指定提示开始与AI Assistant交互：

![访问发现代理](/help/ai-in-aem/agents/discovery/assets/access-discovery-agent.png)

## 常见用例和示例提示 {#use-cases-prompts}

通过[发现代理](/help/ai-in-aem/agents/discovery/overview.md)搜索正确的资源以使用内容优化提示。 一旦相关图像浮出水面，用户就可以直接从搜索结果为一个或多个资源生成优化或特定于渠道的变体。 这一工作流程确保高质量的投入和持续更好的优化结果。 [查看可用优化的完整列表](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/)。

* **高分辨率演绎版创建**

  代理可以按指定的分辨率和质量级别生成资产的新演绎版，从而无需手动编辑即可轻松准备渠道就绪的变体。


  示例提示：

  创建具有`2000px`质量的`JPEG`演绎版作为`80%`。

  使用[发现代理](/help/ai-in-aem/agents/discovery/overview.md)搜索正确的资源，然后在出现多个搜索结果时使用以下提示：

  对于第3个搜索结果，创建具有`2000px`质量的`JPEG`演绎版作为`80%`。

  OR

  对于`Asset ID`，生成质量为`JPEG`的2000px演绎版作为`80%`

* **图像增强功能**

  代理可以应用视觉效果（例如锐化）来确保资产在用于各种活动之前看上去清晰明了，并且定义良好。

  示例提示：

  锐化图像。


* **背景颜色调整**

  代理可以更新或替换透明资产中的背景颜色，从而支持品牌特定的颜色方案或营销活动驱动的视觉主题。

  示例提示：

  将`PNG`的背景颜色更改为`#ff8932`。

* **方向转换**

  该代理可以翻转或镜像视觉以符合布局需求或创作方向，而无需外部编辑工具。

  示例提示：

  水平镜像映像。

* **渠道优化的演绎版**

  该代理可以针对平台特定的要求（如Instagram故事）生成演绎版，确保资产自动符合格式、比例和质量准则。

  示例提示：

  为`Instagram`故事创建演绎版。

* **标记叠加和复合生成**

  代理可以将促销图形、叠加或徽章精确放置到现有资源上，从而支持快速创建营销活动就绪的合成内容。

  示例提示：

  将带有`30%`折扣图表的图像覆盖在促销横幅上，从中心放置`100px`。

  >[!NOTE]
  >
  >叠加位置可能不准确。


## 优化结果 {#content-optimization-agent-results}

指定优化提示时，内容优化代理会根据资源类型返回增强型资源以及便捷的访问选项：

* **图像**：响应包括缩略图预览和用于打开Dynamic Media URL或下载优化图像的选项。

* **PDF文档**：响应包括缩略图预览和用于打开Dynamic Media URL或下载优化文件的选项。

* **视频**：响应提供了打开Dynamic Media URL或下载优化视频的选项。

![内容优化结果](/help/ai-in-aem/agents/content-optimization/assets/download-content-optimization.png)

利用这些结果，可以轻松查看优化输出并立即在下游渠道或工作流中使用。

<!--


## Prompting best Practices {#prompting-best-practices-content-optimization-agent}

The following are some of the prompting best practices:

* Be explicit about the enhancement you want the Content Optimization Agent to apply. Clearly state the transformation or adjustment you expect. Precise instructions help the agent produce accurate and predictable results. For example, Instead of `Make it good quality`, specify `Create a JPEG image with 90% quality`.

* Provide detailed parameters whenever possible. The more context you give, such as dimensions, format, quality, placement, or color values, the more tailored the output is.

-->
