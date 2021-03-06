---
title: 自动标记资产 [!DNL Adobe Sensei] 智能服务
description: 使用人为智能的服务标记资产，该服务会应用上下文和描述性业务标记。
contentOwner: AG
feature: Smart Tags,Tagging
role: Admin,User
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
source-git-commit: 5bf764c84d6676b575371bd865538a3f2c13a2ab
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 5%

---


# 向资产中添加智能标记并改进搜索体验 {#smart-tag-assets-for-faster-search}

处理数字资产的组织越来越多地在资产元数据中使用分类控制的词汇。 基本上，它包含一个关键词列表，员工、合作伙伴和客户通常使用该列表来引用和搜索其数字资产。 使用分类控制的词汇标记资产可确保在搜索中轻松识别和检索资产。

与自然语言词汇相比，基于业务分类的标记有助于使资产与公司的业务保持一致，并确保最相关的资产出现在搜索中。 例如，汽车制造商可以使用型号名称标记汽车图像，以便在设计促销活动时只显示相关图像。

在后台，该功能使用人为智能的框架 [Adobe Sensei](https://business.adobe.com/why-adobe/experience-cloud-artificial-intelligence.html) 以根据您的标记结构和业务分类培训其图像识别算法。 然后，可使用此内容智能对不同的资产集应用相关标记。 [!DNL Experience Manager Assets] 默认情况下，会自动将智能标记应用于已上传的资产。

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## 支持的资产类型 {#smart-tags-supported-file-formats}

您可以标记以下类型的资产：

* **图像**:使用Adobe Sensei的智能内容服务标记多种格式的图像。 您 [创建培训模型](#train-model) 然后，将自动标记上传的图像。 智能标记会应用于支持的文件类型，这些文件类型会以JPG和PNG格式生成演绎版。
* **基于文本的资产**: [!DNL Experience Manager Assets] 上传后，会自动为支持的基于文本的资产设置标记。
* **视频资产**:默认情况下，视频标记在 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. [视频已自动标记](/help/assets/smart-tags-video-assets.md) 上传新视频或重新处理现有视频时。

| 图像（MIME类型） | 基于文本的资产（文件格式） | 视频资产（文件格式和编解码器） |
|----|-----|------|
| image/jpeg | CSV | MP4(H264/AVC) |
| image/tiff | DOC | MKV(H264/AVC) |
| image/png | DOCX | MOV(H264/AVC，动态JPEG) |
| image/bmp | HTML | AVI(indeo4) |
| image/gif | PDF | FLV(H264/AVC， vp6f) |
| image/pjpeg | PPT | WMV(WMV2) |
| image/x-portable-anymap | PPTX |  |
| image/x-portable-bitmap | RTF |  |
| image/x-portable-graymap | SRT |  |
| image/x-portable-pixmap | TXT |  |
| image/x-rgb | VTT |  |
| image/x-xbitmap |  |  |
| image/x-xpixmap |  |  |
| image/x-icon |  |  |
| image/photoshop |  |  |
| image/x-photoshop |  |  |
| 图像/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

[!DNL Experience Manager] 默认情况下，会自动将智能标记添加到基于文本的资产和视频。 要自动将智能标记添加到图像，请完成以下任务。

* [了解标记模型和准则](#understand-tag-models-guidelines).
* [训练模型](#train-model).
* [标记数字资产](#tag-assets).
* [管理标记和搜索](#manage-smart-tags-and-searches).

## 了解标记模型和准则 {#understand-tag-models-guidelines}

标记模型是一组与被标记的图像的各种视觉方面相关联的相关标记。 标签与图像的明显不同的视觉方面相关，以便当应用时，标签有助于搜索特定类型的图像。 例如，鞋类收藏集可以具有不同的标记，但所有标记都与鞋类相关，并且可以属于同一标记模型。 应用标记后，有助于查找不同类型的鞋，例如通过设计或使用来查找。 要了解 [!DNL Experience Manager]，将培训模型可视化为顶级实体，该实体由一组手动添加的标记和每个标记的示例图像组成。 每个标记都可以专门应用于图像。

在创建标记模型并培训服务之前，请确定一组唯一的标记，这些标记最好地描述业务环境中图像中的对象。 确保策划集中的资产符合 [培训准则](#training-guidelines).

### 培训准则 {#training-guidelines}

确保培训集中的图像符合以下准则：

**数量和大小：** 每个标记至少10个图像和50个图像。

**一致性**:确保标记的图像在视觉上相似。 最好将具有相同视觉方面的标记（例如图像中相同类型的对象）一起添加到单个标记模型中。 例如，将所有这些图像标记为 `my-party` （用于培训），因为它们在视觉上并不相似。

![示例图像以说明培训准则](assets/do-not-localize/coherence.png)

**覆盖**:培训中的图像应该有足够的多样性。 我们的想法是提供一些比较多样化的例子，以便 [!DNL Experience Manager] 学会专注于正确的事情。 如果您对视觉上不相似的图像应用相同的标记，请至少包含每种类型的五个示例。 例如，对于标记 *模型 — 下姿态*，为服务包含更多与下面突出显示的图像类似的培训图像，以便在标记期间更准确地识别类似图像。

![示例图像以说明培训准则](assets/do-not-localize/coverage_1.png)

**干扰/阻碍**:该服务能够更好地训练分散注意力的图像（突出的背景、不相关的伴奏，如主题的物体/人）。 例如，对于标记 *休闲鞋*&#x200B;第二张图像不是好的训练候选者。

![示例图像以说明培训准则](assets/do-not-localize/distraction.png)

**完整性：**&#x200B;如果图像符合多个标记的条件，请在包含培训图像之前添加所有适用的标记。例如，对于 *Raincoat* 和 *model-side-view* 等标记，在将其加入培训之前，在符合条件的资产上添加这两个标记。

![示例图像以说明培训准则](assets/do-not-localize/completeness.png)

**标记数**:Adobe建议您为每个标记至少使用两个不同的标记和十个不同的图像来训练模型。 在单个标记模型中，请勿添加超过50个标记。

**示例数**:对于每个标记，至少添加十个示例。 但是，Adobe建议使用大约30个示例。 每个标记最多支持50个示例。

**防止误报和冲突**:Adobe建议为单个可视化方面创建单个标记模型。 以避免模型之间重叠标记的方式构建标记模型。 例如，请勿使用 `sneakers` 在两个不同的标记模型名称中 `shoes` 和 `footwear`. 培训过程将覆盖一个已培训的标记模型与另一个已培训的标记模型，以覆盖通用关键字。

**示例**:还有一些指导示例：

* 创建仅包含、

   * 与车型相关的标记。
   * 与成人和儿童外套相关的标签。

* 请勿创建，

   * 一种标记型号，包括2019年和2020年发布的车型。
   * 多个标记模型，其中包含相同的少数车型。

**用于训练的图像**:您可以使用相同的图像来训练不同的标记模型。 但是，请勿将图像与标记模型中的多个标记相关联。 可以使用属于不同标记模型的不同标记来标记同一图像。

您无法撤消培训。 上述准则应有助于您选择要培训的良好图像。

## 为自定义标记培训模型 {#train-model}

要为特定于业务的标记创建和培训模型，请执行以下步骤：

1. 创建必需的标记和相应的标记结构。 在DAM存储库中上传相关图像。
1. 在 [!DNL Experience Manager] 用户界面，访问 **[!UICONTROL 资产]** > **[!UICONTROL 智能标记培训]**.
1. 单击&#x200B;**[!UICONTROL 创建]**。提供 **[!UICONTROL 标题]**, **[!UICONTROL 描述]**.
1. 单击 **[!UICONTROL 标记]** 字段。 随即会打开一个弹出窗口。
1. 从 `cq-tags` 要添加到模型的参数。 单击&#x200B;**[!UICONTROL 下一步]**。

   >[!NOTE]
   >
   >您可以根据 **[!UICONTROL 名称]** （按字母顺序）， **[!UICONTROL 已创建]** 日期，或 **[!UICONTROL 已修改]** 日期。


1. 在 **[!UICONTROL 选择资产]** 对话框，单击 **[!UICONTROL 添加资产]** 标记。 在DAM存储库中搜索或浏览存储库以至少选择10个和50个图像。 选择资产，而不是文件夹。 选择图像后，单击 **[!UICONTROL 选择]**.

   ![查看培训状态](assets/smart-tags-training-status.png)

1. 要预览选定图像的缩略图，请单击标记前面的折叠面板。 您可以通过单击 **[!UICONTROL 添加资产]**. 对选定内容满意后，单击 **[!UICONTROL 提交]**. 用户界面在页面底部显示通知，指示培训已开始。
1. 在 **[!UICONTROL 状态]** 列。 可能的状态包括 [!UICONTROL 待定], [!UICONTROL 受过培训]和 [!UICONTROL 失败].

![用于为智能标记培训标记模型的工作流](assets/smart-tag-model-training-flow.png)

*图：培训工作流中用于培训标记模型的步骤。*

### 查看培训状态和报告 {#training-status}

要检查是否在资产培训集中的标记上对智能标记服务进行了培训，请从报表控制台中查看培训工作流报表。

1. 在 [!DNL Experience Manager] 界面，转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 报表]**.
1. 在 **[!UICONTROL 资产报表]** 页面，单击 **[!UICONTROL 创建]**.
1. 选择 **[!UICONTROL 智能标记培训]** 报表，然后单击 **[!UICONTROL 下一个]** 中。
1. 指定报表的标题和描述。在&#x200B;**[!UICONTROL 计划报告]**&#x200B;下，保持选中&#x200B;**[!UICONTROL 立即]**&#x200B;选项。如果要安排以后的计划报告，请选择&#x200B;**[!UICONTROL 稍后]**，然后指定日期和时间。然后，单击 **[!UICONTROL 创建]** 中。
1. 在&#x200B;**[!UICONTROL 资产报表]**&#x200B;页面中，选择生成的报表。要查看报表，请单击 **[!UICONTROL 查看]** 中。
1. 查看报告的详细信息。 报表显示您培训的标记的培训状态。中的绿色 **[!UICONTROL 培训状态]** 列表示已为标记培训智能标记服务。 黄色表示服务已针对特定标记进行部分培训。 要为标记完全培训服务，请使用特定标记添加更多图像并执行培训工作流。 如果在此报表中未看到标记，请再次执行这些标记的培训工作流。标记
1. 要下载报表，请从列表中选择该报表，然后单击 **[!UICONTROL 下载]** 中。 报表将下载为电子表格。

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

## 使用智能标记标记资产 {#tag-assets}

所有类型的受支持资产都会自动标记为 [!DNL Experience Manager Assets] 上传后。 默认情况下，标记处于启用状态并可正常使用。 [!DNL Experience Manager] 近乎实时地应用相应的标记。 <!-- TBD: You can also apply the tagging workflow on-demand. The workflow applies to both, assets and folders. -->

* 对于图像和视频，智能标记基于某些视觉方面。

* 对于基于文本的资产，智能标记的效果并不取决于资产中的文本数量，而取决于资产文本中存在的相关关键字或实体。 对于基于文本的资产，智能标记是显示在文本中的关键字，但最能描述资产的关键字。 对于受支持的资产， [!DNL Experience Manager] 已经提取文本，该文本随后会编入索引，用于搜索资产。 但是，基于文本中关键字的智能标记提供了专用、结构化和更高优先级的搜索方面。 与搜索索引相比，后者有助于改进资产发现。

## 管理智能标记和资产搜索 {#manage-smart-tags-and-searches}

您可以策划智能标记以删除可能分配给您的品牌资产的任何不准确标记，以便仅显示最相关的标记。

审核智能标记还可确保您的资产显示在最相关标记的搜索结果中，从而帮助优化基于标记的资产搜索。 从根本上说，这有助于消除不相关资产在搜索结果中出现的可能性。

您还可以为标记分配更高的排名，以提高标记与资产的相关性。 提升资产的标记，可增加在基于特定标记执行搜索时，搜索结果中出现资产的可能性。

要审核数字资产的智能标记，请执行以下操作：

1. 在搜索字段中，根据标记搜索数字资产。

1. 要识别您找不到与搜索相关的数字资产，请检查搜索结果。

1. 选择一个资产，然后选择 ![“管理标记”图标](assets/do-not-localize/manage-tags-icon.png) 中。

1. 从 **[!UICONTROL 管理标记]** ，检查标记。 如果您不希望根据特定标记搜索资产，请选择该标记，然后选择 ![“删除”图标](assets/do-not-localize/delete-icon.png) 中。 或者，选择 `X` 符号。

1. 要为标记分配更高的排名，请选择标记并选择 ![提升图标](assets/do-not-localize/promote-icon.png) 中。 您提升的标记将移至 **[!UICONTROL 标记]** 中。

1. 选择 **[!UICONTROL 保存]** 然后选择 **[!UICONTROL 确定]** 关闭 [!UICONTROL 成功] 对话框。

1. 导航到 [!UICONTROL 属性] 页面。 请注意，为您提升的标记分配了高相关性，因此，在搜索结果中显示的较高。

### 了解 [!DNL Experience Manager] 使用智能标记搜索结果 {#understand-search}

默认情况下， [!DNL Experience Manager] 搜索将搜索词与 `AND` 子句。 使用智能标记不会更改此默认行为。 使用智能标记可添加 `OR` 子句来查找所应用智能标记中的任何搜索词。 例如，请考虑搜索 `woman running`. 仅包含 `woman` 或 `running` 默认情况下，元数据中的关键字不会显示在搜索结果中。 但是，标有以下任一项的资产 `woman` 或 `running` 在此类搜索查询中会显示使用智能标记。 所以搜索结果是，

* 资产 `woman` 和 `running` 元数据中的关键词。

* 使用任一关键字标记的资产智能。

首先显示与元数据字段中的所有搜索词匹配的搜索结果，然后显示与智能标记中的任意搜索词匹配的搜索结果。 在上例中，搜索结果的显示大致顺序为：

1. 匹配 `woman running` 在各种元数据字段中。
1. 匹配 `woman running` 在智能标记中。
1. 匹配 `woman` 或 `running` 在智能标记中。

## 与标记相关的限制和最佳实践 {#limitations}

增强型智能标记基于图像及其标记的学习模型。 这些模型并非总能很好地识别标记。 智能标记的当前版本具有以下限制：

* 无法识别图像中的细微差异。 例如，修身衬衫与普通衬衫。
* 无法根据图像的微小模式或部分来识别标记。 例如，衬衫上的徽标。
* 支持标记的语言包括 [!DNL Experience Manager] 支持。 有关语言列表，请参阅 [智能内容服务发行说明](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html#languages).
* 未处理的标记与以下事项相关：

   * 非视觉、抽象的方面。 例如，产品发布的年份或季节、图像引发的情绪或情感，以及视频的主观内涵。
   * 产品中的视觉差异非常显着，例如衬衫上嵌有和不带领，或产品上嵌有小产品标识。

要训练模型，请使用最合适的图像。 无法恢复培训或删除培训模型。 您的标记准确性取决于当前培训，因此请谨慎进行。

<!-- TBD: Add limitations related to text files. -->

要搜索带有智能标记（常规或增强）的文件，请使用 [!DNL Assets] 搜索（全文搜索）。 智能标记没有单独的搜索谓词。

>[!NOTE]
>
>智能标记是否能够在您的标记上进行培训并将其应用于其他图像，取决于您用于培训的图像质量。
>为获得最佳结果，Adobe建议您使用视觉上相似的图像来为每个标记培训服务。

>[!MORELIKETHIS]
>
>* [了解智能标记如何帮助管理数字文件](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [对视频使用智能标记](smart-tags-video-assets.md)

