---
title: 如何向AEM中的资源添加智能标记？
description: 使用可应用上下文和描述性业务标记的人工智能服务，将智能标记添加到AEM中的资源。
contentOwner: AG
feature: Smart Tags,Tagging
role: Admin,User
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2461'
ht-degree: 6%

---


# 将智能标记添加到AEM中的资源 {#smart-tags-assets-aem}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/enhanced-smart-tags.html?lang=en) |
| AEM as a Cloud Service | 本文 |

处理数字资产的组织越来越多地在资产元数据中使用分类控制的词汇。 本质上，它包括员工、合作伙伴和客户通常用于引用和搜索其数字资产的关键字列表。 使用分类控制的词汇标记资产可确保轻松地在搜索中识别和检索资产。

与自然语言词汇相比，基于业务分类法的标记有助于使资产与公司的业务保持一致，并确保最相关的资产出现在搜索中。 例如，汽车制造商可以使用型号名称标记汽车图像，以便在搜索时仅显示相关图像以设计促销活动。

在后台功能采用的是人工智能的框架 [Adobe Sensei](https://business.adobe.com/why-adobe/experience-cloud-artificial-intelligence.html) 根据您的标记结构和业务分类培训其图像识别算法。 然后，此内容智能可用于将相关标记应用到其他资产集。 默认情况下，AEM会自动将智能标记应用于已上传的资源。

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## AEM中智能标记支持的资源类型 {#smart-tags-supported-file-formats}

您可以标记以下类型的资产：

* **图像**：使用Adobe Sensei的智能内容服务对多种格式的图像进行标记。 您 [创建训练模型](#train-model) 然后会自动标记上传的图像。 智能标记将应用于支持的文件类型，这些文件类型会生成JPG和PNG格式的演绎版。
* **基于文本的资源**： [!DNL Experience Manager Assets] 在上传时自动标记支持的基于文本的资产。
* **视频资产**：默认情况下会启用视频标记 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. [视频已自动标记](/help/assets/smart-tags-video-assets.md) 上传新视频或重新处理现有视频时。

| 图像（MIME类型） | 基于文本的资源（文件格式） | 视频资产（文件格式和编解码器） |
|----|-----|------|
| image/jpeg | CSV | MP4 (H264/AVC) |
| image/tiff | DOC | MKV (H264/AVC) |
| image/png | DOCX | MOV (H264/AVC，运动JPEG) |
| image/bmp | HTML | AVI (indeo4) |
| image/gif | PDF | FLV (H264/AVC， vp6f) |
| image/pjpeg | PPT | WMV(WMV2) |
| image/x-portable-anymap | PPTX |  |
| image/x-portable-bitmap | RTF |  |
| image/x-portable-graymap | SRT |  |
| image/x-portable-pixmap | TXT |  |
| image/x-rgb | VTT |  |
| image/x-xbitmap | |  |
| image/x-xpixmap | |  |
| image/x-icon |  |  |
| image/photoshop |  |  |
| image/x-photoshop |  |  |
| image/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

默认情况下，AEM会将智能标记自动添加到基于文本的资源以及视频。 要将智能标记自动添加到图像，请完成以下任务。

* [了解标记模型和准则](#understand-tag-models-guidelines).
* [训练模型](#train-model).
* [标记您的数字资产](#tag-assets).
* [管理标记和搜索](#manage-smart-tags-and-searches).

## 了解标记模型和准则 {#understand-tag-models-guidelines}

标记模型是一组相关标记，这些标记与所标记图像的各种视觉方面相关联。 标记与图像的明显不同视觉方面相关，因此在应用时，标记有助于搜索特定类型的图像。 例如，一个鞋系列可以具有不同的标记，但所有标记都与鞋相关，并可属于同一标记模型。 在应用时，标签有助于查找不同类型的鞋，例如按设计或按使用。 要了解中培训模型的内容表示形式，请执行以下操作 [!DNL Experience Manager]，将训练模型可视化为顶级实体，由一组手动添加的标记和每个标记的示例图像组成。 每个标记可以专门应用于图像。

在创建标记模型并培训服务之前，请确定一组唯一标记，它们最能描述业务环境中图像中的对象。 确保策划集中的资产符合 [培训准则](#training-guidelines).

### 培训准则 {#training-guidelines}

确保培训集中的图像符合以下准则：

**数量和大小：** 每个标记最少10个图像，最多50个图像。

**一致性**：确保标记的图像在视觉上类似。 最好将关于相同视觉方面（例如图像中的同一类型对象）的标记一起添加到单个标记模型中。 例如，将这些图像标记为 `my-party` （用于培训），因为它们视觉上并不相似。

![说明性图像以说明培训准则](assets/do-not-localize/coherence.png)

**覆盖率**：训练中图像应具有足够的多样性。 我们的想法是提供一些合理多样化的示例，以便 [!DNL Experience Manager] 学习关注正确的事情。 如果您要在视觉上不同的图像上应用相同的标记，则请至少包含每种类型的五个示例。 例如，对于标记 *模型向下姿态*，包括更多与下面高亮显示的图像类似的训练图像，以便该服务在标记期间更准确地识别类似图像。

![说明性图像以说明培训准则](assets/do-not-localize/coverage_1.png)

**分心/阻碍**：此服务可更好地培训注意力较少图像（突出的背景、不相关的伴侣，如具有主要主题的物体/人员）。 例如，对于标记 *休闲鞋*，第二幅图像不是很好的候选训练图像。

![说明性图像以说明培训准则](assets/do-not-localize/distraction.png)

**完整性：**&#x200B;如果图像符合多个标记的条件，请在包含培训图像之前添加所有适用的标记。例如，对于 *Raincoat* 和 *model-side-view* 等标记，在将其加入培训之前，在符合条件的资产上添加这两个标记。

![说明性图像以说明培训准则](assets/do-not-localize/completeness.png)

**标记数**：Adobe建议为模型训练使用至少两个不同的标记以及每个标记至少十个不同的图像。 在单个标记模型中，添加的标记不得超过50个。

**示例数量**：对于每个标记，至少添加十个示例。 但是，Adobe推荐了大约30个示例。 每个标记最多支持50个示例。

**防止误报和冲突**：Adobe建议为单个可视方面创建单个标签模型。 以避免标签在模型之间重叠的方式构造标签模型。 例如，不要使用常见的标记，如 `sneakers` 在两个不同的标记模型名称中 `shoes` 和 `footwear`. 训练过程用一个经过训练的标记模型覆盖另一个标记模型，以获取公共关键字。

**示例**：其他指导示例包括：

* 创建仅包含、

   * 与汽车型号相关的标记。
   * 这些标签与成人和儿童的夹克有关。

* 不要创建，

   * 一种标签模型，包括2019年和2020年发布的车型。
   * 多个标签模型包含相同数量的汽车模型。

**用于训练的图像**：您可以使用相同的图像来训练不同的标记模型。 但是，请勿将图像与标签模型中的多个标签相关联。 可以使用属于不同标记模型的不同标记来标记同一图像。

您无法撤消训练。 以上准则应该可以帮助您选择要训练的良好图像。

## 为自定义标记培训模型 {#train-model}

要为特定于业务的标记创建和训练模型，请执行以下步骤：

1. 创建必要的标记和相应的标记结构。 在DAM存储库中上传相关图像。
1. 在 [!DNL Experience Manager] 用户界面，访问 **[!UICONTROL 资产]** > **[!UICONTROL 智能标记训练]**.
1. 单击&#x200B;**[!UICONTROL 创建]**。提供 **[!UICONTROL 标题]**， **[!UICONTROL 描述]**.
1. 单击中的文件夹图标 **[!UICONTROL 标记]** 字段。 随即会打开一个弹出窗口。
1. 从中的现有标记中搜索或选择相应的标记 `cq-tags` 添加到模型中。 单击&#x200B;**[!UICONTROL 下一步]**。

   >[!NOTE]
   >
   >您可以根据 **[!UICONTROL 名称]** （按字母顺序）， **[!UICONTROL 已创建]** 日期，或 **[!UICONTROL 修改时间]** 日期。


1. 在 **[!UICONTROL 选择资源]** 对话框，请单击 **[!UICONTROL 添加资产]** 针对每个标记。 在DAM存储库中搜索或浏览存储库以选择至少10个和最多50个图像。 选择资源而不是文件夹。 选择图像后，单击 **[!UICONTROL 选择]**.

   ![查看培训状态](assets/smart-tags-training-status.png)

1. 要预览所选图像的缩略图，请单击标记前面的折叠面板。 您可以通过单击 **[!UICONTROL 添加资产]**. 在选择内容满意后，单击 **[!UICONTROL 提交]**. 用户界面在页面底部显示通知，指示培训已启动。
1. 在中检查培训的状态 **[!UICONTROL 状态]** 列来表示每个标记模型。 可能的状态包括 [!UICONTROL 待处理]， [!UICONTROL 已培训]、和 [!UICONTROL 失败].

![此工作流用于培训智能标记的标记模型](assets/smart-tag-model-training-flow.png)

*图：培训工作流中用于培训标记模型的步骤。*

### 查看培训状态和报告 {#training-status}

要检查智能标记服务是否针对培训资产集中的标记进行了培训，请从“报表”控制台中查看培训工作流报表。

1. 在 [!DNL Experience Manager] 界面，转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 报表]**.
1. 在 **[!UICONTROL 资产报表]** 页面，单击 **[!UICONTROL 创建]**.
1. 选择 **[!UICONTROL 智能标记训练]** 报表，然后单击 **[!UICONTROL 下一个]** 工具栏中。
1. 指定报表的标题和描述。在&#x200B;**[!UICONTROL 计划报告]**&#x200B;下，保持选中&#x200B;**[!UICONTROL 立即]**&#x200B;选项。如果要安排以后的计划报告，请选择&#x200B;**[!UICONTROL 稍后]**，然后指定日期和时间。然后，单击 **[!UICONTROL 创建]** 工具栏中。
1. 在&#x200B;**[!UICONTROL 资产报表]**&#x200B;页面中，选择生成的报表。要查看报告，请单击 **[!UICONTROL 视图]** 工具栏中。
1. 查看报告的详细信息。 报表显示您培训的标记的培训状态。中的绿色 **[!UICONTROL 培训状态]** 列指示已为标记培训智能标记服务。 黄色表示服务已针对特定标记进行了部分培训。 要为标签全面培训服务，请使用特定标签添加更多图像并执行培训工作流。 如果您未在此报表中看到您的标记，请再次执行这些标记的培训工作流。标记
1. 要下载报表，请从列表中选择该报表，然后单击 **[!UICONTROL 下载]** 工具栏中。 报表将下载为电子表格。

<!--
### Tag assets from the workflow console {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. In the **[!UICONTROL Run Workflow]** dialog, browse to the payload folder containing assets on which you want to apply your tags automatically.
1. Specify a title for the workflow and an optional comment. Click **[!UICONTROL Run]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   *Figure: Navigate to the asset folder and review the tags to verify whether your assets are tagged properly. For details, see [manage smart tags](#manage-smart-tags-and-searches).*

### Tag assets from the timeline {#tagging-assets-from-the-timeline}

1. From the [!DNL Assets] user interface, select the folder containing assets or specific assets to which you want to apply smart tags.
1. From upper-left corner, open the **[!UICONTROL Timeline]**.
1. Open actions from the bottom of the left sidebar and click **[!UICONTROL Start Workflow]**.

   ![start_workflow](assets/start_workflow.png)

1. Select the **[!UICONTROL DAM Smart Tag Assets]** workflow, and specify a title for the workflow.
1. Click **[!UICONTROL Start]**. The workflow applies your tags on assets. Navigate to the asset folder and review the tags to verify that your assets are tagged properly. For details, see [manage smart tags](#manage-smart-tags-and-searches).

>[!NOTE]
>
>In the subsequent tagging cycles, only the modified assets are tagged again with newly trained tags. However, even unaltered assets are tagged if the gap between the last and current tagging cycles for the tagging workflow exceeds 24 hours. For periodic tagging workflows, unaltered assets are tagged when the time gap exceeds six months.

### Tag uploaded assets {#tag-uploaded-assets}

[!DNL Experience Manager] can automatically tag the assets that users upload to DAM. To do so, administrators configure a workflow to add an available step that tags assets. See [how to enable Smart Tags for uploaded assets](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets).
-->

## 在AEM中使用智能标记来标记资源 {#tag-assets}

所有类型的受支持资源均由自动标记 [!DNL Experience Manager Assets] 上传时。 默认情况下，标记处于启用状态并正常工作。 AEM近乎实时地应用相应的智能标记。 <!-- TBD: You can also apply the tagging workflow on-demand. The workflow applies to both, assets and folders. -->

* 对于图像和视频，智能标记基于某些视觉方面。

* 对于基于文本的资产，智能标记的有效性并不取决于资产中的文本数量，而是取决于资产文本中存在的相关关键字或实体。 对于基于文本的资源，智能标记是显示在文本中的关键字，但最能描述该资源的关键字。 对于支持的资产， [!DNL Experience Manager] 已提取文本，然后将其编入索引，并用于搜索资产。 但是，基于文本中关键字的智能标记提供了专用、结构化和更高优先级的搜索方面。 与搜索索引相比，后者有助于改进资产发现。

## 管理智能标记和资产搜索 {#manage-smart-tags-and-searches}

您可以策划智能标记以删除可能分配给品牌资产的任何不准确的标记，以便仅显示最相关的标记。

审核智能标记还可确保您的资产显示在最相关标记的搜索结果中，从而帮助优化基于标记的资产搜索。 基本上，它有助于消除无关资产出现在搜索结果中的机会。

您还可以为标记分配更高的排名，以提高标记与资产的相关性。 当根据特定标记执行搜索时，提升资产的标记会增加资产出现在搜索结果中的机会。

要审核数字资产的智能标记，请执行以下操作：

1. 在搜索字段中，根据标记搜索数字资源。

1. 要识别与搜索不相关的数字资源，请检查搜索结果。

1. 选择资产，然后选择 ![“管理标记”图标](assets/do-not-localize/manage-tags-icon.png) 工具栏中。

1. 从 **[!UICONTROL 管理标记]** 页面，检查标记。 如果您不希望根据特定标记搜索资产，请选择该标记，然后选择 ![“删除”图标](assets/do-not-localize/delete-icon.png) 工具栏中。 或者，选择 `X` 标签旁边的符号。

1. 要为标记分配较高的排名，请选择该标记，然后选择 ![“提升”图标](assets/do-not-localize/promote-icon.png) 工具栏中。 您提升的标记将移至 **[!UICONTROL 标记]** 部分。

1. 选择 **[!UICONTROL 保存]** 然后选择 **[!UICONTROL 确定]** 关闭 [!UICONTROL 成功] 对话框。

1. 导航至 [!UICONTROL 属性] 页面。 请注意，您提升的标记被分配到了较高的相关性，因此显示在搜索结果中的位置较高。

### 了解 [!DNL Experience Manager] 包含智能标记的搜索结果 {#understand-search}

默认情况下， [!DNL Experience Manager] 搜索将搜索词与 `AND` 子句。 使用智能标记不会更改此默认行为。 使用智能标记可添加 `OR` 子句，用于在应用的智能标记中查找任何搜索词。 例如，考虑搜索 `woman running`. 具有的资产 `woman` 或只是 `running` 默认情况下，元数据中的关键字不会出现在搜索结果中。 但是，使用任一标记进行标记的资产 `woman` 或 `running` 使用智能标记会出现在此类搜索查询中。 所以搜索结果是，

* 具有的资产 `woman` 和 `running` 元数据中的关键字。

* 使用任一关键词进行智能标记的资产。

首先显示与元数据字段中的所有搜索词匹配的搜索结果，随后显示与智能标记中的任何搜索词匹配的搜索结果。 在上述示例中，搜索结果的大致显示顺序为：

1. 匹配项 `woman running` 在各个元数据字段中。
1. 匹配项 `woman running` 在智能标记中。
1. 匹配项 `woman` 或 `running` 在智能标记中。

## 与标记相关的限制和最佳实践 {#limitations}

增强的智能标记基于图像及其标记的学习模型。 这些模型在识别标记方面并不总是完美的。 当前版本的智能标记具有以下限制：

* 无法识别图像中的细微差异。 例如，修身衬衫和普通衬衫。
* 无法根据图像的微小图案或部分识别标记。 例如，衬衫上的徽标。
* 在以下语言中支持标记 [!DNL Experience Manager] 支持。
* 未处理的标记与：

   * 非视觉的抽象方面。 例如，产品发布的年份或季节、图像引发的情绪或情感，以及视频的主观内涵。
   * 产品中的细微视觉差异，例如带有领子的衬衫和不带有领子的衬衫或嵌入在产品上的小产品徽标。

要训练模型，请使用最合适的图像。 无法恢复训练或无法删除训练模型。 您的标记准确性取决于当前的训练，因此请仔细操作。

<!-- TBD: Add limitations related to text files. -->

要搜索带有智能标记（常规或增强）的文件，请使用 [!DNL Assets] 搜索（全文搜索）。 智能标记没有单独的搜索谓词。

>[!NOTE]
>
>智能标记培训您的标记并将它们应用于其他图像的能力取决于您用于培训的图像质量。
>为获得最佳结果，Adobe建议您使用视觉上相似的图像，为每个标签培训服务。

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

>[!MORELIKETHIS]
>
>* [了解智能标记如何帮助您管理数字文件](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [对视频使用智能标记](smart-tags-video-assets.md)
