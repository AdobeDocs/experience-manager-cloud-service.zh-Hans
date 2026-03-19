---
title: 内容发现代理
description: 了解如何使用内容发现代理，通过自然的对话提示来按需提供相关的AEM内容，从而提供简化的免费点击发现体验。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 676300cd-b799-4c53-a58e-043e58a2cbc5
source-git-commit: 10a4b44fde65ae865d2e6d908e9e442752326fcd
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 0%

---


# 内容发现代理 {#discovery-agent}

作为AEM [Content Advisor代理](/help/ai-in-aem/agents/content-advisor/overview.md)的一部分，内容发现代理通过自然的对话提示按需提供AEM内容，从而提供简化的免费点击发现体验。 它可以跨Assets、内容片段、AEM Sites页面和自适应Forms进行智能搜索，以交付相关材料，如图像、视频、PDF文档、文章和表单模板。 使用自然语言，您可以搜索内容，而无需在AEM Assets界面中构建复杂查询或应用过滤器。 根据您的提示，代理会返回策划的结果以及资产元数据和投放URL，以便可以嵌入到其他应用程序中。

内容发现代理的一些主要优势包括：

* **统一内容发现**：从单一对话界面访问所有类型的AEM内容，如图像、视频、PDF文档、文章、页面和表单。

* **更快的活动规划**：快速收集电子邮件、Web和社交渠道中营销活动的视觉效果和表单。

* **增强的生产力**：通过基于意图的自动搜索减少浏览存储库或过滤元数据所花费的时间。

* **内容利用率一致**：确保重复使用已批准的资源和片段，维护跨渠道的品牌一致性。

>[!VIDEO](https://video.tv.adobe.com/v/3479983)

>[!IMPORTANT]
>
>AI生成的响应可能不准确或具有误导性。 请务必仔细检查建议的修复和响应。
>
>另请参阅[Adobe Experience Cloud Generative AI用户准则。](https://www.adobe.com/cn/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)

## 技能 {#skills-discovery-agent}

内容发现代理提供以下技能：

* **自然语言内容发现**

  内容发现代理使用户能够使用简单的自然语言提示在Adobe Experience Manager (AEM)中查找相关资源、内容片段、自适应表单和AEM Sites页面，而无需复杂的搜索查询。

* **基于元数据的资源发现**

  内容发现代理使用自然语言提示，根据可用于AEM中的资源的元数据来查找资源。 用户可以使用元数据发现资源，例如标记、作者或发布者电子邮件ID、发布或修改日期、MIME类型、资源类型、状态、Assets视图或管理员视图中的元数据表单中定义的自定义元数据属性等。 请参阅[常见用例和示例提示](#use-cases-prompts)以了解完整列表。

  您还可以在单个提示中组合多个元数据筛选器以优化搜索结果。

* **基于文件夹的内容发现：**\
  内容发现代理可以通过解释引用AEM中文件夹名称的自然语言提示来识别资源。 用户只需在提示中提及文件夹，无需手动浏览存储库，即可显着减少找到正确内容所需的点击次数。

## 角色 {#personas-content-discovery}

### 营销活动经理 {#campaign-managers}

内容发现代理使营销活动经理能够快速识别并重用受信任的高性能内容作为构思。

### 渠道营销人员 {#channel-marketers}

内容发现代理允许渠道营销人员高效地查找相关资产，以创建一致的多渠道体验。

### DAM库管理员 {#dam-librarians}

DAM库管理员可以标记缺少组织设置的元数据标准的资产，从而支持一致的治理，并确保资产保持完整并可供跨渠道使用。

### 机构和合作伙伴 {#agencies-partners}

代理和合作伙伴可以在Content Hub中轻松找到获得品牌批准的资源并重复使用它们，以加快创意工作，同时保持与品牌标准保持一致。

## 如何访问 {#access}

您可以通过AI Assistant访问AEM中的内容发现代理。 登录到[`experience.adobe.com`](https://experience.adobe.com)，可以通过使用搜索框以自然语言指定提示来开始与AI助手交互：

![访问内容发现代理](/help/ai-in-aem/agents/content-advisor/assets/access-discovery-agent.png)

有关访问内容发现代理的MCP端点的信息，请联系Adobe支持。

## 常见用例和示例提示 {#use-cases-prompts}

### Assets {#discovery-agent-use-cases-assets}

**基于元数据的资源发现**

内容发现代理使用自然语言提示，根据可用于AEM中的资源的元数据来查找资源。 用户可以使用以下元数据属性发现资源：标记、按电子邮件ID创建、按电子邮件ID修改、按电子邮件ID发布、创建日期、修改日期、发布日期、MIME类型、资源类型、状态、文件格式、文件大小、图像宽度、图像高度以及在单个提示内使用多个元数据过滤器。

内容发现代理还会为管理员视图搜索元数据架构中可用的自定义属性，并为Assets视图搜索元数据表单。 您可以相应地修改提示，以搜索这些自定义资源属性中可用的值。

>[!NOTE]
>
>为了提高发现性能，请索引相关的自定义元数据属性。 当用户在其提示中包含匹配内容时，索引属性使代理能够更快地检索这些内容。


示例提示：

* **基于标记进行搜索**：在文件夹`office`中显示标记为`WKND`的图像。
* **根据文件格式、资源类型、资源状态和按电子邮件ID发布**&#x200B;进行搜索：以`.PNG`格式显示`approved`和`published by <user email ID>`的图像。
* **根据文件格式、资源类型、资源状态和电子邮件ID创建**&#x200B;进行搜索：以`.mp4`格式显示已批准的视频和`created by <user email ID>`视频。
* **基于文件格式、资源类型、资源状态和创建日期进行搜索**：以`.PNG`格式显示2025年1月1日和`published by <user email ID>`之后创建的图像
* **基于MIME类型、创建日期和发布者电子邮件ID**&#x200B;进行搜索：节目`image/jpeg`在`January 1, 2025`和`published by <user email ID>`之后创建。
* **基于文件格式和自定义元数据属性进行搜索**：以`.JPEG`格式显示具有`Product SKU ID = <SKU value>`的图像（必须使用元数据属性=值格式）。

* **搜索缺少元数据的资源**：显示过去90天内创建的包含`<Name of metadata property including custom properties>`的资源为空。

* **使用文件大小、图像宽度和图像高度搜索资源**：显示大于5 MB、宽度大于2000像素且高度大于1200像素的图像。


**基于文件夹的内容发现：**\
内容发现代理可以通过解释引用AEM中文件夹名称的自然语言提示来识别资源。 用户只需在提示中提及文件夹，无需手动浏览存储库，即可显着减少找到正确内容所需的点击次数。

示例提示：

* 文件夹`WKND`中是否有任何svg？
* 显示在文件夹`Nov 1 2025`中的`WKND`之后修改的资源。
* 在文件夹`lifestyle`中列出`WKND`图像。

**启用基于文件夹的内容发现的其他问题**

当提示中包含文件夹名称（没有完整的资产路径）时，内容发现代理将首先在根路径`/content/dam/<folder-name>`处检查匹配的文件夹。

如果在根级别未找到匹配的文件夹，代理会建议在存储库中存在指定文件夹名称的备用文件夹路径。 这有助于用户快速识别正确的位置，而无需手动浏览文件夹结构。

例如，未找到路径`/content/dam/<folder-name>`。 你是说这些吗？

* 选项1

* 选项2

**基于格式的资源发现**

内容发现代理可以识别满足特定质量要求（如文件格式）的资产，使用户能够快速找到产品视觉效果，以便跨渠道高质量交付和重新使用。

示例提示：

查找产品包装PNG图像。

**基于方向的内容发现**

内容发现代理可以通过识别视觉属性（例如人员的存在和图像的方向）来过滤资产。 这允许用户快速将内容缩小到最相关的视觉效果，而无需在AEM中手动应用多个过滤器。

示例提示：

以横向显示带人员的资产。

**正在展开搜索结果**

内容发现代理会针对提示返回每个内容类型前20个最相关的结果。 如果还有其他匹配结果可用，则用户可以通过输入后续提示（如`show me more`）来请求下一个集合。 然后，代理从原始搜索中检索下一组结果，使用户能够逐步浏览更大的结果集而不优化提示。

**查找类似的资源**

内容发现代理允许用户查找与搜索结果中返回的特定结果类似的资产。 在代理显示提示的前几个结果后，您可以通过引用项目在结果列表中的位置来请求类似的资源。 例如，诸如`find assets similar to the 3rd result`之类的提示将指示代理识别并返回与该项目相关的其他相关资源。 这有助于用户快速发现相关内容，而无需创建新的搜索提示。

**对搜索结果排序**

内容发现代理允许用户直接在其自然语言提示中对搜索结果进行排序。 用户可以指定排序标准，如修改日期、创建日期或资源名称，并选择升序或降序。

示例提示：

* 查找按修改日期降序排序的山地图像（首先显示最近修改的资源）。

* 显示按名称升序排序的山地图像（显示以字母A开头，后跟B的图像名称，依此类推）。

### AEM Sites页面 {#content-discovery-agent-aem-sites-pages}

内容发现代理通过解释引用页面主题、营销活动或其他上下文关键字的自然语言提示，帮助用户快速找到相关的AEM Sites页面。 代理根据提示中的关键词执行全文搜索，以识别AEM存储库中的匹配页面，而无需手动浏览站点结构。

示例提示：

* 查找夏季促销活动的所有AEM Sites页面。

* 查找包含咖啡主题的AEM Sites页面。

### 内容片段 {#discovery-agent-use-cases-content-fragments}

内容发现代理通过解释对营销活动名称、产品品牌、发布状态和最近创建活动的自然语言引用，帮助用户快速找到正确的内容片段。 它允许团队显示营销活动就绪片段和查看品牌特定内容，所有这些操作都不需要在AEM中手动浏览文件夹或应用多个过滤器。

示例提示：

* 显示用于创建WKND优惠活动的内容片段。

* 显示美国饮料的内容片段。

* 显示WKND饮料的所有已发布内容片段。

* 列出过去2周内创建的所有内容片段。

### Forms {#discovery-agent-use-cases-forms}

内容发现代理可帮助您使用自然语言提示快速查找自适应表单。 它会搜索表单内容和元数据，以根据提示中的关键字查找匹配项。 这意味着即使您的搜索词不在表单的标题或描述中，您也可以成功发现相关表单。

示例提示：

* 显示所有贷款申请表。
* 查找要申请代理的表单。
* 查找联系人表单。
* 我在找员工入职表。
* 给我看信用卡申请表。

注意：表单发现当前仅支持Edge Delivery Services表单，并且基于标记的搜索目前不适用于表单。

## 搜索结果 {#discovery-agent-search-results}

### Assets {#discovery-agent-search-results-assets}

内容发现代理返回每个查询的前几个结果，按相关性排序，以确保首先显示完全匹配项。 该代理将元数据驱动的查询与语义搜索相结合，组装出一组重点突出的可能匹配项，然后使用LLM根据用户意图对它们进行排名。 这种混合方法提供了精确的上下文感知结果，完全不依赖于直接的关键字匹配。

每个结果都包含资源名称以及关键资源元数据，例如资源路径、创建者、创建日期、标题、描述、格式、上次修改时间、上次修改日期、文件大小、维度、[Dynamic Media URL](/help/assets/dynamic-media/dynamic-media.md)和相关标记。 如果资产处于已批准状态，则结果还包括具有OpenAPI URL [的](/help/assets/dynamic-media-open-apis-overview.md)Dynamic Media。

您可以单击资源路径以无缝导航到AEM中的资源位置。

![使用内容发现代理搜索资源](/help/ai-in-aem/agents/content-advisor/assets/search-results-discovery-agent.png)

您可以使用这些资产详细信息快速评估资产是否满足要求，而无需导航到每个资产来查看这些详细信息。

>[!NOTE]
>
>仅当已发布资产并且您拥有有效的Dynamic Media许可证时，[Dynamic Media URL](/help/assets/dynamic-media/dynamic-media.md)字段才会显示在搜索结果中。 同样，仅当您具有有效的Dynamic Media许可证并且已为您的AEM as a Cloud Service实例启用了具有OpenAPI的Dynamic Media时，才会显示[具有OpenAPI URL的Dynamic Media ](/help/assets/dynamic-media-open-apis-overview.md)字段。

### 内容片段 {#discovery-agent-search-results-content-fragments}

内容发现代理为内容片段提供全文搜索功能，返回与指定提示最匹配的前几个结果。 每个结果都包括内容片段名称以及关键元数据字段，例如内容片段路径、创建者、创建日期、变体、上次修改时间和上次修改日期字段。

![使用内容发现代理搜索内容片段](/help/ai-in-aem/agents/content-advisor/assets/search-content-fragments-discovery-agent.png)

您可以单击内容片段路径以无缝导航到AEM中的内容片段位置。

## 提示最佳实践 {#prompting-best-practices-discovery-agent}

以自然语言提示指定简洁的详细信息，以便代理可以返回准确且相关的结果。 您越清楚地描述要查找的内容，代理程序就越能优化和缩小输出范围。 例如，您可以：

* 在提示中定义资源元数据，例如标记、文件夹名称、创建日期、发布状态、作者名称，以筛选资源。

* 使用特定于您的组织的元数据，例如类别（跑鞋、电子产品）、季节（秋季、春季）、事件（黑色星期五、产品发布）和渠道（Web、电子邮件、打印）来进一步筛选内容。

## 限制 {#limitations-discovery-agent}

* 内容发现代理仅支持针对图像和SVG格式类型的基于维度的提示。 例如 `Find images wider than 1080px`。

* Content Hub管理员可以使用Content Hub门户访问内容发现代理，但是，结果只能从AEM创作实例中检索。 Content Hub Limited用户目前无法获得Content Discovery Agent的优势（即将推出）。

* “查找类似”功能仅适用于具有[智能标记增强功能](/help/assets/ai-generated-metadata-assets-view.md)的图像。
