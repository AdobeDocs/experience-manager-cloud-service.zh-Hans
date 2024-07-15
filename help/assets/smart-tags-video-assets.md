---
title: 为视频资源添加智能标记
description: Experience Manager使用 [!DNL Adobe Sensei]自动将上下文和描述性智能标记添加到视频。
feature: Smart Tags
role: Admin, User
exl-id: b59043c5-5df3-49a7-b4fc-da34c03649d7
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 3%

---

# 为视频资源添加智能标记 {#video-smart-tags}

由于对新内容的需求不断增加，需要减少手动工作，以便及时提供引人入胜的数字体验。 [!DNL Adobe Experience Manager]作为[!DNL Cloud Service]支持使用人工智能自动标记视频资产。 手动标记视频可能非常耗时。 但是，[!DNL Adobe Sensei]支持的视频智能标记功能使用人工智能模型来分析视频内容并将标记添加到视频资产。 从而减少DAM用户为其客户提供丰富体验的时间。 Adobe的机器学习服务为视频生成两组标记。 而其中一组对应于该视频中的对象、场景和属性；另一组则与饮酒、跑步和慢跑等操作相关。

视频标记在[!DNL Adobe Experience Manager]中默认作为[!DNL Cloud Service]启用。 但是，您可以在文件夹上[选择退出视频智能标记](#opt-out-video-smart-tagging)。 当您上传新视频或重新处理现有视频时，会自动标记视频。 [!DNL Experience Manager]还会创建缩略图并提取视频文件的元数据。 智能标记在资产[!UICONTROL 属性]中按其[置信度分数](#confidence-score-video-tag)的降序显示。

## 上传时智能标记视频 {#smart-tag-assets-on-ingestion}

当您[将视频资产](add-assets.md#upload-assets)作为[!DNL Cloud Service]上传到[!DNL Adobe Experience Manager]时，将处理视频。 处理完成后，请参阅资产[!UICONTROL 属性]页面的[!UICONTROL 基本]选项卡。 智能标记会自动添加到[!UICONTROL 智能标记]下的视频中。 资源微服务使用[!DNL Adobe Sensei]创建这些智能标记。

![智能标记已添加到视频中，并在资产属性的“基本”选项卡中显示](assets/smart-tags-added-to-videos.png)

应用的智能标记在[!UICONTROL 智能标记]中按[置信度分数](#confidence-score-video-tag)的降序排序，对象和操作标记组合在一起。

>[!IMPORTANT]
>
>建议您查看这些自动生成的标记，以确保它们符合您的品牌及其价值。

## 智能标记DAM中的现有视频 {#smart-tag-existing-videos}

DAM中已存在的视频资产不会自动进行智能标记。 您需要手动[!UICONTROL 重新处理Assets]以为其生成智能标记。

要智能标记视频资源或资源存储库中已存在的资源文件夹（包括子文件夹），请执行以下步骤：

1. 选择[!DNL Adobe Experience Manager]徽标，然后从[!UICONTROL 导航]页面中选择资源。

1. 选择[!UICONTROL 文件]以显示Assets界面。

1. 导航到要应用智能标记的文件夹。

1. 选择整个文件夹或特定的视频资产。

1. 选择![重新处理资源图标](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL 重新处理Assets]图标并选择[!UICONTROL 完整处理]选项。

<!-- TBD: Limit size -->

![重新处理资产以将标记添加到现有DAM存储库的视频中](assets/reprocess.gif)

进程完成后，导航到文件夹中任何视频资产的[!UICONTROL 属性]页面。 自动添加的标记显示在[!UICONTROL 基本]选项卡的[!UICONTROL 智能标记]部分中。 这些应用的智能标记按[置信度分数](#confidence-score-video-tag)的降序排序。

## 搜索标记的视频 {#search-smart-tagged-videos}

要根据自动生成的智能标记搜索视频资产，请使用[Omnisearch](search-assets.md#search-assets-in-aem)：

1. 选择搜索图标![搜索图标](assets/do-not-localize/search_icon.png)以显示Omnisearch字段。

1. 在Omnisearch字段中指定尚未显式添加到视频的标记。

1. 基于标记进行搜索。

搜索结果会根据您指定的标记显示视频资产。

您的搜索结果由元数据中具有搜索关键字的视频资源和使用搜索关键字智能标记的视频资源组成。 但是，首先显示与元数据字段中的所有搜索词匹配的搜索结果，随后显示与智能标记中的任何搜索词匹配的搜索结果。 有关详细信息，请参阅[了解带有智能标记的 [!DNL Experience Manager] 搜索结果](smart-tags.md#understand-search)。

## 审核视频智能标记 {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager]允许您组织智能标记以：

* 删除分配给品牌视频的不准确标记。

* 通过确保您的视频显示在最相关标记的搜索结果中，优化基于标记的视频搜索。 因此，它消除了无关视频出现在搜索结果中的机会。

* 为标记分配更高排名，以增加其与视频的相关性。 当基于视频标记执行搜索时，升级该标记会增加搜索结果中出现视频的机会。

要详细了解如何审核资产的智能标记，请参阅[管理智能标记](smart-tags.md#manage-smart-tags-and-searches)。

![审核视频智能标记](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>重新处理资产时，不会记住任何使用[管理智能标记](smart-tags.md#manage-smart-tags-and-searches)中的步骤进行审核的标记。 将再次显示原始标记集。

## 选择退出视频智能标记 {#opt-out-video-smart-tagging}

由于视频的自动标记与其他资产处理任务（如缩略图创建和元数据提取）并行运行，因此可能会非常耗时。 要加快资产处理，您可以在文件夹级别上传时选择退出视频智能标记。

要选择退出为上传到特定文件夹的资产自动生成视频智能标记，请执行以下操作：

1. 在文件夹[!UICONTROL 属性]中打开[!UICONTROL 资产处理]选项卡。

1. 在[!UICONTROL 视频智能标记]菜单中，[!UICONTROL 已继承]选项默认处于选中状态，并且已启用视频智能标记。

   选择[!UICONTROL 继承]选项时，继承的文件夹路径也会与信息一起显示，该信息是设置为[!UICONTROL 启用]还是[!UICONTROL 禁用]。

   ![禁用视频智能标记](assets/disable-video-tagging.png)

1. 选择[!UICONTROL 禁用]以选择退出对上传到文件夹的视频进行智能标记。

>[!IMPORTANT]
>
>如果您在上传时选择不为文件夹中的视频添加标签，并且希望在上传后为视频添加智能标签，则请在文件夹[!UICONTROL 属性]的[!UICONTROL 资产处理]选项卡中&#x200B;**[!UICONTROL 为视频启用智能标签]**，并使用[[!UICONTROL 重新处理资产]选项](#smart-tag-existing-videos)为视频添加智能标签。

## 置信度分数 {#confidence-score-video-tag}

[!DNL Adobe Experience Manager]为object和action智能标记应用最小置信度阈值，以避免每个视频资产的标记过多，这会减慢索引速度。 您的资产搜索结果将根据置信度分数进行排名，这通常会改进搜索结果，其效果超出了任何视频资产的已分配标记检查所显示的范围。 不准确的标记通常具有较低的置信度分数，因此它们很少出现在资产的智能标记列表的顶部。

[!DNL Adobe Experience Manager]中操作和对象标记的默认阈值为0.7（该值应介于0和1之间）。 如果某些视频资源未被特定标记标记，则表明算法对于预测标记的信赖度低于70%。 默认阈值可能并不总是适用于所有用户。 因此，您可以更改OSGI配置中的置信度分数值。

要将置信度分数OSGI配置添加到作为[!DNL Cloud Service]通过[!DNL Cloud Manager]部署到[!DNL Adobe Experience Manager]的项目，请执行以下操作：

* 在[!DNL Adobe Experience Manager]项目（`ui.config`自Archetype 24或以前的`ui.apps`）中，`config.author` OSGi配置包含名为`com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json`的配置文件，该文件包含以下内容：

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

* 您无法使用任何特定视频培训将智能标记应用于视频的服务。 它可与默认[!DNL Adobe Sensei]设置配合使用。

* 不显示标记进度。

* 只有文件大小小于300 MB的视频会被自动标记。 [!DNL Adobe Sensei]服务跳过更大大小的视频文件。

* 只标记[智能标记](/help/assets/smart-tags.md#smart-tags-supported-file-formats)中提到的文件格式视频和受支持的编解码器。

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
>* [训练智能标记服务并标记您的图像](smart-tags.md)
