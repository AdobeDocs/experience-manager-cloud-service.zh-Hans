---
title: 智能标记视频资源
description: 智能标记视频资产通过使用Adobe Sensei服务应用上下文和描述性标记，从而自动化资产标记。
translation-type: tm+mt
source-git-commit: 68fe67617f0d63872f13427b3fbc7b58f2497aca
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 0%

---


# 智能标记视频资源 {#video-smart-tags}

对新内容的不断需求要求减少手动工作，以快速提供引人入胜的数字体验。 [!DNL Adobe Experience Manager] 作为Cloud Service，它支持在人工智能的帮助下自动标记视频资产。 手动标记视频会非常耗时。 但是，Adobe Sensei支持的视频智能标记功能使用人工智能模型来分析视频内容并向视频资产添加标记。 从而缩短DAM用户向客户提供丰富体验的时间。 Adobe的机器学习服务为一个视频生成两组标签。 而一个集合则对应该视频中的对象、场景和属性；另一组则与饮酒、跑步和慢跑等动作有关。

支持智能标记的视频文件格式（及其编解码器）包括MP4(H264/AVC)、MKV(H264/AVC)、MOV(H264/AVC、Motion JPEG)、AVI(indeo4)、FLV(H264/AVC、vp6f)和WMV(WMV2)。 此外，该功能还允许标记最大300 MB的视频。 在上传视频或触发重新处理后，视频资产的自动标记会作为标准资产处理(以及缩略图创建和元数据提取)进行。 智能标记按资产属性中置信度 [得分的降序](#confidence-score-video-tag) 显 [!UICONTROL 示]。 默认情况下，视频标记会 [!DNL Adobe Experience Manager] 作为Cloud Service启用。 但是，您可 [以选择退出文件夹中的视频](#opt-out-video-smart-tagging) 智能标记。

## 上传时智能标记视频 {#smart-tag-assets-on-ingestion}

将视 [频资产上传](add-assets.md#upload-assets)[!DNL Adobe Experience Manager] 为Cloud Service时，视频会进行 ![处理](assets/do-not-localize/assetprocessing.png)。 处理完成后，请参阅资产 [!UICONTROL 属性] 页面的“基 [!UICONTROL 本”选] 项卡。 智能标记会自动添加到“智能标记” [!UICONTROL 下的视频]。 资产计算服务利用Adobe Sensei创建这些智能标签。

![智能标记会添加到视频中，并会在资产属性的“基本”选项卡中显示](assets/smart-tags-added-to-videos.png)

应用的智能标记按置信度得分的降 [序排序](#confidence-score-video-tag)，并在智能标记中组合对象 [!UICONTROL 和操作标记]。

>[!IMPORTANT]
>
>建议您检查这些自动生成的标记，以确保它们符合您的品牌及其价值。

## 在DAM中智能标记现有视频 {#smart-tag-existing-videos}

DAM中已有的视频资产不会自动智能标记。 您需要手动 [!UICONTROL 重新处理资产] ，以为资产生成智能标记。

要智能标记资产存储库中已存在的资产的视频资产或文件夹（包括子文件夹），请执行以下步骤：

1. 选择标 [!DNL Adobe Experience Manager] 志，然后从导航页面 [!UICONTROL 中选择] 资产。

1. 选择 [!UICONTROL 文件] ，以显示资产界面。

1. 导航到要应用智能标记的文件夹。

1. 选择整个文件夹或特定视频资产。

1. 选择 ![重新处理资产](assets/do-not-localize/reprocess-assets-icon.png)[!UICONTROL 图标重新处] 理资产 [!UICONTROL ，然后选择完] 整处理选项。

![重新处理资产以向现有DAM存储库的视频添加标记](assets/reprocess.gif)

完成该过程后，导航到文 [!UICONTROL 件夹中] 任何视频资产的“属性”页面。 自动添加的标记显示在“基 [!UICONTROL 本”选项卡] 的“智 [!UICONTROL 能标记] ”部分。 这些应用的智能标记按置信度得分的降 [序排序](#confidence-score-video-tag)。

## 搜索标记视频 {#search-smart-tagged-videos}

要根据自动生成的智能标记搜索视频资产，请使用 [Omnisearch](search-assets.md#search-assets-in-aem):

1. 选择搜索图标 ![搜索图标](assets/do-not-localize/search_icon.png) ，以显示“全局搜索”字段。

1. 在“全局搜索”字段中，指定尚未显式添加到视频的标记。

1. 根据标记进行搜索。

搜索结果会根据您指定的标记显示视频资产。

搜索结果是元数据中带有搜索关键字的视频资产和带有搜索关键字的智能标记的视频资产的组合。 但是，将首先显示与元数据字段中的所有搜索词匹配的搜索结果，然后显示与智能标记中的任何搜索词匹配的搜索结果。 有关详细信息，请参 [ [!DNL Experience Manager] 阅了解带有智能标记的搜索结果](smart-tags.md#understandsearch)。

## 审核视频智能标记 {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] 允许您将智能标记创建为：

* 删除分配给您的品牌视频的不准确标记。

* 通过确保视频在搜索结果中显示以获得最相关的标记，优化基于标记的视频搜索。 因此，它消除了不相关视频在搜索结果中出现的可能性。

* 为标记指定更高的等级，以提高其与视频的相关性。 提升视频的标记可提高在基于该标记执行搜索时在搜索结果中显示视频的可能性。

要进一步了解如何审核资产的智能标记，请参阅 [管理智能标记](smart-tags.md#manage-smart-tags-and-searches)。

![审核视频智能标记](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>在重新处理资产时，不会记住使用 [管理智能标记](smart-tags.md#manage-smart-tags-and-searches) 中的步骤进行审核的任何标记。 将再次显示原始标记集。

## 选择退出视频智能标记 {#opt-out-video-smart-tagging}

由于自动标记视频与其他资产处理任务(如缩略图创建和元数据提取)并行运行，这可能非常耗时。 要加速资产处理，您可以在选择退出文件夹级别上传视频时智能添加标签。

为上传选择退出到特定文件夹的资产生成自动视频智能标记的步骤：

1. 打开 [!UICONTROL 文件夹属性] 中的“资产处 [!UICONTROL 理”选项卡]。

1. 在“ [!UICONTROL 视频的智能标记] ”菜单 [!UICONTROL 中，默认情况下选] 择“继承”选项，并启用视频智能标记。

   选择“ [!UICONTROL 继承] ”选项后，还会显示继承的文件夹路径以及设置为“启用”或“禁用”时 [!UICONTROL 的]信息。

   ![禁用视频智能标记](assets/disable-video-tagging.png)

1. 选  择禁选择退出用已上传到文件夹的视频的智能标记。

>[!IMPORTANT]
>
>如果您在上传时已选择退出在文件夹上标记视频，并且希望在上传后智能标记视频，则 **[!UICONTROL 从文件夹属性的“资产处理”选项卡]** “启用视频智能标记 [!UICONTROL ”，然后使用“重新处理”][](#smart-tag-existing-videos) 资产选项“”将智能标记添加到视频。

## 信心得分 {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] 对对象和操作智能标记应用最小置信度阈值，以避免每个视频资产的标记过多，从而降低索引速度。 您的资产搜索结果会根据信心分数进行排名，这通常会改善搜索结果，超出对任何视频资产所分配标记的检查所暗示的程度。 不准确的标记通常具有较低的置信度得分，因此它们很少出现在资产的智能标记列表的顶部。

0.7中操作和对象标 [!DNL Adobe Experience Manager] 记的默认阈值（值应介于0和1之间）。 如果某些视频资产未被特定标记标记，则表明该算法对预测的标记信心不足70%。 默认阈值可能并非始终对所有用户是最佳的。 因此，您可以更改OSGI配置中的置信度得分值。

要通过云管理器将置信度得分OSGI配置添加到部署 [!DNL Adobe Experience Manager] 为Cloud Service的项目，请执行以下操作：

* 在项目 [!DNL Adobe Experience Manager] 中(`ui.config` 自Archetype 24或之前) `ui.apps`,OSGi配 `config.author` 置包括一个名为的配置文件， `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` 其中包含以下内容：

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>手动标记的置信度为100%（最大置信度）。 因此，如果有视频资产具有与搜索查询匹配的手动标记，则这些视频资产会显示在与搜索查询匹配的智能标记之前。

## 限制 {#video-smart-tagging-limitations}

* 尚不支持培训智能标记服务（或增强的智能标记）来标记视频资产。

* 不显示标记进度。

* 只有大小不超过300 MB的视频适合标记。 Adobe Sensei服务会智能标记符合此条件的视频，并跳过标记文件夹中的其他视频。

* 只有这些文件格式（和支持的编解码器）的视频：MP4(H264/AVC)、MKV(H264/AVC)、MOV(H264/AVC、Motion JPEG)、AVI(indeo4)、FLV(H264/AVC)64/AVC、vp6f)和WMV(WMV2)-可以标记。

>[!MORELIKETHIS]
>
>* [管理智能标记和资产搜索](smart-tags.md#manage-smart-tags-and-searches)
>* [培训智能标签服务并标记图像](smart-tags.md)

