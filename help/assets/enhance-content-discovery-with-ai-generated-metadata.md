---
title: 在管理员视图中利用AI生成的元数据增强内容发现
description: 了解如何在管理员视图中使用人工智能生成的元数据增强内容发现
feature: Smart Tags,Tagging
role: Admin,User
source-git-commit: 5dbad509f5a5a9addfe6b52c3c3dd7ce5fa3229d
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 8%

---


# 使用AI生成的元数据增强内容发现 {#ai-smart-tags}

| UI | 文章链接 |
| -------- | ---------------------------- |
| 资源视图 | [单击此处](/help/assets/ai-generated-metadata-assets-view.md) |
| 管理员视图 | 本文 |

AI不会依赖手动输入，而是自动将描述性标记分配给数字资产。 这些 AI 生成的标记提高了元数据的质量，使资产更易于搜索、分类和推荐。此方法不仅通过消除手动标记而提高了效率，而且确保了跨大量数字内容的一致性和可扩展性。 例如，如果资产是图像，AI可以识别其中的对象、场景、情感甚至品牌徽标，并生成相关标记，如“日落”、“海滩”、“休假”或“微笑”。 人工智能生成的内容可以通过利用语义和词汇搜索技术增强对资产的搜索。 查看更多[搜索Assets](search-assets.md)。<!--If the asset is a document, AI reads and interprets the text to assign meaningful keywords that summarize its content—such as "climate change," "policy," or "renewable energy.-->

![增强型智能标记](assets/enhanced-smart-tags1.png)

## 如何启用AI生成的元数据？ {#enable-ai-generated-metadata}

要启用AI生成的元数据：

* 所需的最低AEM版本为`20626`。

* 你必须签署GenAI Rider协议。 有关更多信息，请与您的Adobe代表联系。

## 配置人工智能生成的标题 {#configure-ai-generated-titles}

通过AEM，您可以在Asset Browse页面上配置卡片视图或列表视图中的资源标题显示。 您可以选择显示您定义的资产标题、用 AI 生成的标题，或者仅在资产缺少标题时使用 AI 生成的标题。

要配置AI生成的标题：

1. 导航到&#x200B;**[!UICONTROL 工具> Assets > Assets配置>智能标记增强配置]**。

1. 选择以下选项之一：

   * **显示DC标题（默认）**：在资产属性中可用的&#x200B;**[!UICONTROL 标题]**&#x200B;字段中指定标题，以将其显示在卡片视图或列表视图中。 如果未定义资源标题，AEM Assets将显示文件名。

   * **显示人工智能生成的标题**：显示人工智能生成的标题并忽略资产属性中指定的标题。 如果AI生成的标题不适用于某个资源，则AEM Assets会显示其属性中可用的默认资源标题。

   * **仅在DC标题不存在时显示人工智能生成的标题**：仅当没有为资源定义资源标题时，AEM Assets才会显示人工智能生成的标题。

     ![配置 AI 生成的标题](assets/configure-title-ai-generated.png)

## 使用人工智能生成的元数据 {#using-ai-generated-smart-tags}

<!--[!NOTE]
>
>The enhanced smart tags capability is available only for the newly uploaded assets.
-->

要使用增强型智能标记功能，请执行以下步骤：

1. 在[!DNL Experience Manager]界面中，转到所需的文件夹，然后单击&#x200B;**[!UICONTROL 添加Assets]**。 <!--Alternatively, to update enhanced smart tags in an existing content, click **[!UICONTROL reprocess]**.-->兼容的图像文件格式为`png`、`jpg`、`jpeg`、`psd`、`tiff`、`gif`、`webp`、`crw`、`cr2`、`3fr`、`nef`、`arw`和`bmp`。

1. 等待新上传的资源得到处理。 完成后，转到资源属性。

1. 转到&#x200B;**[!UICONTROL AI生成的]**&#x200B;选项卡。 如果[!DNL Experience Manager]版本不兼容或未更新，则此选项卡不可见。 其中包含以下字段：

   * **[!UICONTROL 生成的标题]：**&#x200B;标题提供了简洁明了的标题，其中捕获了已上传资源的核心概念，使其易于一目了然。 添加资源时，如果您提供标题（在`dc:title`中），则该标题将显示在资源浏览视图中。 如果留空，将自动分配AI生成的标题。
   * **[!UICONTROL 生成的描述]：**&#x200B;该描述提供了资产相关内容的简短但信息丰富的摘要，可帮助用户和搜索模块快速掌握其相关性。
   * **[!UICONTROL 生成的关键字]：**&#x200B;关键字是表示资产主题的目标术语，有助于标记和内容筛选。

1. [可选]如果您觉得任何相关标记缺失，可以添加其他标记或创建自己的标记。 为此，请在&#x200B;**[!UICONTROL 生成的关键字]**&#x200B;字段中写入您的标记，然后单击&#x200B;**[!UICONTROL 保存]**。

## 禁用AI生成的元数据 {#disable-ai-generated-metadata}

您可以在文件夹级别禁用AI生成的元数据。 所有子文件夹都从父文件夹继承属性。

要在文件夹级别禁用AI生成的元数据，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL Adobe Experience Manager > Assets >文件]**。

1. 选择文件夹并单击&#x200B;**[!UICONTROL 属性]**。

1. 在&#x200B;**[!UICONTROL 资产处理]**&#x200B;选项卡中，导航到&#x200B;**[!UICONTROL 图像智能标记增强功能]**&#x200B;文件夹。 从下拉列表中选择以下值之一：

   * 已继承 — 文件夹从父文件夹继承启用或禁用选项。

   * 启用 — 为选定的文件夹启用AI生成的元数据。

   * 禁用 — 为选定的文件夹禁用AI生成的元数据。

     ![禁用AI生成的元数据](assets/disable-ai-generated-metadata.png)