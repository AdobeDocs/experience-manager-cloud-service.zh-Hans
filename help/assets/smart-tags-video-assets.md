---
title: 为视频资源添加智能标记
description: Experience Manager使用以下方式自动将上下文和描述性智能标记添加到视频 [!DNL Adobe Sensei].
feature: Smart Tags,Tagging
role: Admin,User
exl-id: b59043c5-5df3-49a7-b4fc-da34c03649d7
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 3%

---

# 为视频资源添加智能标记 {#video-smart-tags}

由于对新内容的需求不断增加，需要减少手动工作，以便及时提供引人入胜的数字体验。 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 支持使用人工智能自动标记视频资产。 手动标记视频可能非常耗时。 但是， [!DNL Adobe Sensei] 支持的视频智能标记功能使用人工智能模型来分析视频内容并将标记添加到视频资产。 从而减少DAM用户为其客户提供丰富体验的时间。 Adobe的机器学习服务为视频生成两组标记。 而其中一组对应于该视频中的对象、场景和属性；另一组则与饮酒、跑步和慢跑等操作相关。

默认情况下，中的视频标记处于启用状态。 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. 但是，您可以 [选择退出视频智能标记](#opt-out-video-smart-tagging) 在文件夹上。 当您上传新视频或重新处理现有视频时，会自动标记视频。 [!DNL Experience Manager] 还会创建缩略图并提取视频文件的元数据。 智能标记按其降序显示 [置信度分数](#confidence-score-video-tag) 在资产中 [!UICONTROL 属性].

## 上传时智能标记视频 {#smart-tag-assets-on-ingestion}

当您 [上传视频资产](add-assets.md#upload-assets) 到 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]，则会处理视频。 处理完成后，请参阅 [!UICONTROL 基本] 资源的选项卡 [!UICONTROL 属性] 页面。 智能标记会自动添加到下的视频中 [!UICONTROL 智能标记]. 资源微服务使用 [!DNL Adobe Sensei] 以创建这些智能标记。

![智能标记会添加到视频，并显示在资产属性的基本选项卡中](assets/smart-tags-added-to-videos.png)

应用的智能标记按降序排序 [置信度分数](#confidence-score-video-tag)，针对对象和操作标记进行组合，在 [!UICONTROL 智能标记].

>[!IMPORTANT]
>
>建议您查看这些自动生成的标记，以确保它们符合您的品牌及其价值。

## 智能标记DAM中的现有视频 {#smart-tag-existing-videos}

DAM中已存在的视频资产不会自动进行智能标记。 您需要 [!UICONTROL 重新处理资产] 手动为其生成智能标记。

要智能标记视频资源或资源存储库中已存在的资源文件夹（包括子文件夹），请执行以下步骤：

1. 选择 [!DNL Adobe Experience Manager] 徽标，然后从中选择资源 [!UICONTROL 导航] 页面。

1. 选择 [!UICONTROL 文件] 以显示“资产”界面。

1. 导航到要应用智能标记的文件夹。

1. 选择整个文件夹或特定的视频资产。

1. 选择 ![“重新处理资产”图标](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL 重新处理资产] 图标，然后选择 [!UICONTROL 完整流程] 选项。

<!-- TBD: Limit size -->

![重新处理资产以将标记添加到现有DAM存储库的视频](assets/reprocess.gif)

流程完成后，导航到 [!UICONTROL 属性] 文件夹中任何视频资产的页面。 自动添加的标记将显示在 [!UICONTROL 智能标记] 中的部分 [!UICONTROL 基本] 选项卡。 这些应用的智能标记按降序排序 [置信度分数](#confidence-score-video-tag).

## 搜索标记的视频 {#search-smart-tagged-videos}

要根据自动生成的智能标记搜索视频资产，请使用 [Omnisearch](search-assets.md#search-assets-in-aem)：

1. 选择搜索图标 ![搜索图标](assets/do-not-localize/search_icon.png) 以显示Omnisearch字段。

1. 在Omnisearch字段中指定尚未显式添加到视频的标记。

1. 基于标记进行搜索。

搜索结果会根据您指定的标记显示视频资产。

您的搜索结果由元数据中具有搜索关键字的视频资源和使用搜索关键字智能标记的视频资源组成。 但是，首先显示与元数据字段中的所有搜索词匹配的搜索结果，随后显示与智能标记中的任何搜索词匹配的搜索结果。 有关更多信息，请参阅 [了解 [!DNL Experience Manager] 包含智能标记的搜索结果](smart-tags.md#understand-search).

## 审核视频智能标记 {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] 允许您将智能标记组织为：

* 删除分配给品牌视频的不准确标记。

* 通过确保您的视频显示在最相关标记的搜索结果中，优化基于标记的视频搜索。 因此，它消除了无关视频出现在搜索结果中的机会。

* 为标记分配更高排名，以增加其与视频的相关性。 当基于视频标记执行搜索时，升级该标记会增加搜索结果中出现视频的机会。

要详细了解如何审核资产的智能标记，请参阅 [管理智能标记](smart-tags.md#manage-smart-tags-and-searches).

![审核视频智能标记](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>任何已使用中的步骤进行审核的标记 [管理智能标记](smart-tags.md#manage-smart-tags-and-searches) 在重新处理资产时不会被记住。 将再次显示原始标记集。

## 选择退出视频智能标记 {#opt-out-video-smart-tagging}

由于视频的自动标记与其他资产处理任务（如缩略图创建和元数据提取）并行运行，因此可能会非常耗时。 要加快资产处理，您可以在文件夹级别上传时选择退出视频智能标记。

要选择退出为上传到特定文件夹的资产自动生成视频智能标记，请执行以下操作：

1. 打开 [!UICONTROL 资产处理] 选项卡中的文件夹 [!UICONTROL 属性].

1. 在 [!UICONTROL 视频智能标记] 菜单， [!UICONTROL 已继承] 默认选中选项并启用视频智能标记。

   当 [!UICONTROL 已继承] 选项，则继承的文件夹路径以及是否将其设置为的信息也可见 [!UICONTROL 启用] 或 [!UICONTROL 禁用].

   ![禁用视频智能标记](assets/disable-video-tagging.png)

1. 选择 [!UICONTROL 禁用] 以选择退出对上传到文件夹的视频进行智能标记。

>[!IMPORTANT]
>
>如果您在上传时选择不为文件夹中的视频添加标签，并希望在上传后为视频添加智能标签，则 **[!UICONTROL 为视频启用智能标记]** 从 [!UICONTROL 资产处理] 文件夹选项卡 [!UICONTROL 属性] 和使用 [[!UICONTROL 重新处理资产] option](#smart-tag-existing-videos) 将智能标记添加到视频。

## 置信度分数 {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] 为object和action智能标记应用最小置信度阈值，以避免每个视频资产的标记太多，这会减慢索引速度。 您的资产搜索结果将根据置信度分数进行排名，这通常会改进搜索结果，其效果超出了任何视频资产的已分配标记检查所显示的范围。 不准确的标记通常具有较低的置信度分数，因此它们很少出现在资产的智能标记列表的顶部。

中操作和对象标记的默认阈值 [!DNL Adobe Experience Manager] 为0.7（该值应介于0和1之间）。 如果某些视频资源未被特定标记标记，则表明算法对于预测标记的信赖度低于70%。 默认阈值可能并不总是适用于所有用户。 因此，您可以更改OSGI配置中的置信度分数值。

将置信度分数OSGI配置添加到部署到的项目 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 到 [!DNL Cloud Manager]：

* 在 [!DNL Adobe Experience Manager] 项目(`ui.config` 从Archetype 24开始，或之前 `ui.apps`) `config.author` OSGi配置，包含一个名为的配置文件 `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` 包含以下内容：

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>手动标记被指定为100%的置信度（最大置信度）。 因此，如果存在具有匹配搜索查询的手动标记的视频资产，则这些视频资产会在匹配搜索查询的智能标记之前显示。

## 限制 {#video-smart-tagging-limitations}

* 您无法使用任何特定视频培训将智能标记应用于视频的服务。 它适用于默认情况 [!DNL Adobe Sensei] 设置。

* 不显示标记进度。

* 只有文件大小小于300 MB的视频会被自动标记。 此 [!DNL Adobe Sensei] 服务会跳过更大大小的视频文件。

* 仅文件格式中的视频以及中提到的受支持的编解码器 [智能标记](/help/assets/smart-tags.md#smart-tags-supported-file-formats) 已标记。

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [管理智能标记和资产搜索](smart-tags.md#manage-smart-tags-and-searches)
>* [培训智能标记服务并标记您的图像](smart-tags.md)
