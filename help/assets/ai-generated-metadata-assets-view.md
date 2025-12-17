---
title: 使用人工智能生成的元数据增强内容发现
description: 了解如何使用人工智能生成的元数据增强内容发现
source-git-commit: 3f44e74488fc73c406fefb6decc41782859d029b
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 4%

---


# 使用人工智能生成的元数据增强内容发现 {#ai-smart-tags}

AI不会依赖手动输入，而是自动将描述性标记分配给数字资产。 这些 AI 生成的标记提高了元数据的质量，使资产更易于搜索、分类和推荐。此方法不仅通过消除手动标记而提高了效率，而且确保了跨大量数字内容的一致性和可扩展性。 例如，如果资产是图像，AI可以识别其中的对象、场景、情感甚至品牌徽标，并生成相关标记，如“日落”、“海滩”、“休假”或“微笑”。 人工智能生成的内容可以通过利用语义和词汇搜索技术增强对资产的搜索。 查看更多[搜索Assets](search-assets-view.md)。<!--If the asset is a document, AI reads and interprets the text to assign meaningful keywords that summarize its content—such as "climate change," "policy," or "renewable energy.-->

![AI生成的元数据](/help/assets/assets/enhanced-smart-tags.png)

## 如何启用AI生成的元数据？ {#enable-ai-generated-metadata}

要启用AI生成的元数据：

* 所需的最低AEM版本为`20626`。


## 使用人工智能生成的元数据 {#using-ai-generated-smart-tags}

<!--[!NOTE]
>
>The enhanced smart tags capability is available only for the newly uploaded assets.
-->

要使用增强型智能标记功能，请执行以下步骤：

1. 在[!DNL Experience Manager]界面中，转到所需的文件夹，然后单击&#x200B;**[!UICONTROL 添加Assets]**。 <!--Alternatively, to update enhanced smart tags in an existing content, click **[!UICONTROL reprocess]**.-->兼容的图像文件格式为`png`、`jpg`、`jpeg`、`psd`、`tiff`、`gif`、`webp`、`crw`、`cr2`、`3fr`、`nef`、`arw`和`bmp`。

1. 等待新上传的资源得到处理。 完成后，转到资源详细信息。

1. 转到&#x200B;**[!UICONTROL AI生成的]**&#x200B;选项卡。 如果[!DNL Experience Manager]版本不兼容或未更新，则此选项卡不可见。  其中包含以下字段：

   * **[!UICONTROL 生成的标题]：**&#x200B;标题提供了简洁明了的标题，其中捕获了已上传资源的核心概念，使其易于一目了然。 添加资源时，如果您提供标题（在`dc:title`中），则该标题将显示在资源浏览视图中。 如果留空，将自动分配AI生成的标题。
   * **[!UICONTROL 生成的描述]：**&#x200B;该描述提供了资产相关内容的简短但信息丰富的摘要，可帮助用户和搜索模块快速掌握其相关性。
   * **[!UICONTROL 生成的关键字]：**&#x200B;关键字是表示资产主题的目标术语，有助于标记和内容筛选。

1. [可选]如果您觉得任何相关标记缺失，可以添加其他标记或创建自己的标记。 为此，请在&#x200B;**[!UICONTROL 生成的关键字]**&#x200B;字段中写入您的标记，然后单击&#x200B;**[!UICONTROL 保存]**。

有关如何禁用AI生成的元数据的信息，请参阅[禁用AI生成的元数据](/help/assets/enhance-content-discovery-with-ai-generated-metadata.md#disable-ai-generated-metadata)。
