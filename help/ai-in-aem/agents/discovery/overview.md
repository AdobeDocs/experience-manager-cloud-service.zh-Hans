---
title: 发现代理概述
description: 了解如何使用发现代理，通过自然的对话提示来按需提供相关的AEM内容，从而提供简化的、点击式的免费发现体验。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 676300cd-b799-4c53-a58e-043e58a2cbc5
source-git-commit: 5488fdb1ffc9c65ef2b569627f9a2ef414181290
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 1%

---

# 发现代理 {#discovery-agent}

Discovery Agent通过自然的对话提示按需提供AEM内容，从而提供简洁的点击式免费发现体验。 它可以跨Assets、内容片段和自适应Forms进行智能搜索，以交付相关材料，如图像、视频、PDF文档、文章和表单模板。 使用自然语言，您可以搜索内容，而无需在AEM Assets界面中构建复杂查询或应用过滤器。 根据您的提示，代理会返回策划的结果以及资产元数据和投放URL，以便可以嵌入到其他应用程序中。

Discovery Agent的一些主要优势包括：

* **统一内容发现**：从单一对话界面访问所有类型的AEM内容，如图像、视频、PDF文档、文章和表单。

* **更快的活动规划**：快速收集电子邮件、Web和社交渠道中营销活动的视觉效果和表单。

* **增强的生产力**：通过基于意图的自动搜索减少浏览存储库或过滤元数据所花费的时间。

* **内容利用率一致**：确保重复使用已批准的资源和片段，维护跨渠道的品牌一致性。

>[!IMPORTANT]
>
>AI生成的响应可能不准确或具有误导性。 请务必仔细检查建议的修复和响应。
>
>另请参阅[Adobe Experience Cloud Generative AI用户指南](https://www.adobe.com/cn/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)。

>[!VIDEO](https://video.tv.adobe.com/v/3479983)

## 技能 {#skills-discovery-agent}

Discovery Agent提供以下技能：

* **自然语言内容发现**\
  发现代理使用户能够使用简单的自然语言提示在Adobe Experience Manager (AEM)中查找相关资源、内容片段和自适应表单，而无需复杂的搜索查询。

* **基于标记的资源发现**

  发现代理使用自然语言提示来查找与AEM存储库中的特定标记关联的资源，从而帮助用户快速访问根据组织分类编排或未编排的内容。

* **基于文件夹的内容发现：**\
  发现代理可以通过解释引用AEM中文件夹名称的自然语言提示来识别资源。 用户只需在提示中提及文件夹，无需手动浏览存储库，即可显着减少找到正确内容所需的点击次数。

## 角色 {#personas-discovery-agent}

### 营销活动经理 {#campaign-managers}

Discovery Agent使Campaign Manager能够快速识别并重用受信任的高性能内容作为构思。

### 渠道营销人员 {#channel-marketers}

发现代理允许渠道营销人员高效地查找相关资产以创建一致的多渠道体验。

### DAM库管理员 {#dam-librarians}

DAM库管理员可以标记缺少组织设置的元数据标准的资产，从而支持一致的治理，并确保资产保持完整并可供跨渠道使用。

### 机构和合作伙伴 {#agencies-partners}

代理和合作伙伴可以在Content Hub中轻松找到获得品牌批准的资源并重复使用它们，以加快创意工作，同时与品牌标准保持一致。

## 如何访问发现代理？ {#access-discovery-agent}

您可以通过AI助手访问AEM中的代理。 登录到experience.adobe.com ，您可以通过使用搜索框以自然语言指定提示来开始与AI Assistant交互：

![访问发现代理](/help/ai-in-aem/agents/discovery/assets/access-discovery-agent.png)

有关用于访问发现代理的MCP端点的信息，请与Adobe支持部门联系。

## 常见用例和示例提示 {#use-cases-prompts}

### Assets {#discovery-agent-use-cases-assets}

**基于标记的资源发现**

Discovery Agent使用自然语言提示来查找与AEM存储库中的特定标记相关的资源，从而帮助用户快速访问根据其组织的分类整理的内容。

示例提示：

显示文件夹`office`中标记为`WKND`的图像。

**基于文件夹的内容发现：**\
发现代理可以通过解释引用AEM中文件夹名称的自然语言提示来识别资源。 用户只需在提示中提及文件夹，无需手动浏览存储库，即可显着减少找到正确内容所需的点击次数。

示例提示：

* 文件夹`WKND`中是否有任何svg？
* 显示在文件夹`Nov 1 2025`中的`WKND`之后修改的资源。
* 在文件夹`lifestyle`中列出`WKND`图像。

**基于格式的资源发现**

Discovery Agent可以识别满足特定质量要求的资产（如文件格式），使用户能够快速找到产品视觉效果，以便跨渠道进行高质量交付和重用。

示例提示：

查找产品包装PNG图像。

**基于方向的内容发现**

发现代理可以通过识别视觉属性（如人员的存在和图像的方向）来过滤资产。 这允许用户快速将内容缩小到最相关的视觉效果，而无需在AEM中手动应用多个过滤器。

示例提示：

以横向显示带人员的资产。

### 内容片段 {#discovery-agent-use-cases-content-fragments}

发现代理通过解释对营销活动名称、产品品牌、发布状态和最近创建活动的自然语言引用，帮助用户快速找到正确的内容片段。 它允许团队显示营销活动就绪片段和查看品牌特定内容，所有这些操作都不需要在AEM中手动浏览文件夹或应用多个过滤器。

示例提示：

* 显示用于创建WKND优惠活动的内容片段。

* 显示美国饮料的内容片段。

* 显示WKND饮料的所有已发布内容片段。

* 列出过去2周内创建的所有内容片段。

### Forms {#discovery-agent-use-cases-forms}

发现代理可帮助您使用自然语言提示快速查找自适应表单。 它会搜索表单内容和元数据，以根据提示中的关键字查找匹配项。 这意味着即使您的搜索词不在表单的标题或描述中，您也可以成功发现相关表单。

示例提示：

* 显示所有贷款申请表。
* 查找要申请工作的表单。
* 查找联系人表单。
* 我在找员工入职表。
* 给我看信用卡申请表。

注意：表单发现当前仅支持Edge Delivery Services表单，并且基于标记的搜索目前不适用于表单。

## 搜索结果 {#discovery-agent-search-results}

### Assets {#discovery-agent-search-results-assets}

发现代理返回每个查询的前几个结果，按相关性排序，以确保首先显示完全匹配的结果。 Agent将元数据驱动的查询与语义搜索相结合，组成一组集中的可能匹配项，然后使用LLM根据用户意图对它们进行排名。 这种混合方法提供了精确的上下文感知结果，完全不依赖于直接的关键字匹配。

每个结果都包含资源名称以及关键资源元数据，例如资源路径、创建者、创建日期、标题、描述、格式、上次修改时间、上次修改日期、文件大小、维度、[Dynamic Media URL](/help/assets/dynamic-media/dynamic-media.md)和相关标记。 如果资产处于已批准状态，则结果还包括具有OpenAPI URL [的](/help/assets/dynamic-media-open-apis-overview.md)Dynamic Media。

您可以单击资源路径以无缝导航到AEM中的资源位置。

![使用发现代理搜索资源](/help/ai-in-aem/agents/discovery/assets/search-results-discovery-agent.png)

您可以使用这些资产详细信息快速评估资产是否满足要求，而无需导航到每个资产来查看这些详细信息。

>[!NOTE]
>
>仅当已发布资产并且您拥有有效的Dynamic Media许可证时，[Dynamic Media URL](/help/assets/dynamic-media/dynamic-media.md)字段才会显示在搜索结果中。 同样，仅当您具有有效的Dynamic Media许可证并且已为您的AEM as a Cloud Service实例启用了具有OpenAPI的Dynamic Media时，才会显示[具有OpenAPI URL的Dynamic Media &#x200B;](/help/assets/dynamic-media-open-apis-overview.md)字段。

### 内容片段 {#discovery-agent-search-results-content-fragments}

发现代理为内容片段提供全文搜索功能，返回与指定提示最匹配的前几个结果。 每个结果都包括内容片段名称以及关键元数据字段，例如内容片段路径、创建者、创建日期、变体、上次修改时间和上次修改日期字段。

![使用发现代理搜索内容片段](/help/ai-in-aem/agents/discovery/assets/search-content-fragments-discovery-agent.png)

您可以单击内容片段路径以无缝导航到AEM中的内容片段位置。

## 提示最佳实践 {#prompting-best-practices-discovery-agent}

以自然语言提示指定简洁的详细信息，以便代理可以返回准确且相关的结果。 您越清楚地描述要查找的内容，代理程序就越能优化和缩小输出范围。 例如，您可以：

* 在提示中定义资源元数据，例如标记、文件夹名称、创建日期、发布状态、作者名称，以筛选资源。

* 使用特定于您的组织的元数据，例如类别（跑鞋、电子产品）、季节（秋季、春季）、事件（黑色星期五、产品发布）和渠道（Web、电子邮件、打印）来进一步筛选内容。

## 限制 {#limitations-discovery-agent}

发现代理仅支持对图像和SVG格式类型使用基于维度的提示。 例如 `Find images wider than 1080px`。
