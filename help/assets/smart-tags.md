---
title: 使用AI生成的标记自动标记资源
description: 使用人工智能服务标记资产，这些服务使用 [!DNL Adobe Sensei] 服务应用上下文和描述性业务标记。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a1213a1694a50d174b4ad1e7e4ba7c71944b861a
workflow-type: tm+mt
source-wordcount: '2800'
ht-degree: 6%

---


# 为资产添加智能标记以改善搜索体验{#smart-tag-assets-for-faster-search}

处理数字资产的组织越来越多地在资产元数据中使用分类控制的词汇。 本质上，它包含一列表关键字，员工、合作伙伴和客户通常使用这些关键字来引用和搜索其数字资产。 使用分类控制的词汇标记资产可确保在搜索中轻松识别和检索资产。

与自然语言词汇相比，基于业务分类的标记有助于使资产与公司的业务相协调，并确保最相关的资产出现在搜索中。 例如，汽车制造商可以用型号名称标记汽车图像，以便在搜索时只显示相关图像以设计促销活动。

在后台，该功能使用人为智能的[Adobe Sensei](https://www.adobe.com/cn/sensei/experience-cloud-artificial-intelligence.html)框架来训练其关于标签结构和业务分类的图像识别算法。 然后，此内容智能可用于对不同的资产集应用相关标记。

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

您可以标记以下类型的资产：

* **图像**:使用Adobe Sensei的智能内容服务标记多种格式的图像。您[创建一个培训模型](#train-model)，然后[将智能标签](#tag-assets)应用到图像。
* **视频资产**:默认情况下，视频标记 [!DNL Adobe Experience Manager] 为启用 [!DNL Cloud Service]。[在您上传新视频或](/help/assets/smart-tags-video-assets.md) 重新处理现有视频时，视频会自动标记。
* **基于文本的资产**: [!DNL Experience Manager Assets] 上传时，会自动为支持的基于文本的资产添加标记。了解有关[标记基于文本的资产](#smart-tag-text-based-assets)的更多信息。

## 支持的资源类型{#smart-tags-supported-file-formats}

“智能标签”将应用于支持的文件类型，这些文件类型以JPG和PNG格式生成再现。 以下类型的资产支持该功能：

| 图像（MIME类型） | 基于文本的资产（文件格式） | 视频资源（文件格式和编解码器） |
|----|-----|------|
| image/jpeg | CSV | MP4(H264/AVC) |
| image/tiff | DOC | MKV(H264/AVC) |
| image/png | DOCX | MOV(H264/AVC， Motion JPEG) |
| image/bmp | HTML | AVI(indeo4) |
| image/gif | JSON | FLV(H264/AVC， vp6f) |
| image/pjpeg | PDF | WMV(WMV2) |
| image/x-portable-anymap | PPT |  |
| image/x-portable-bitmap | PPTX |  |
| image/x-portable-graymap | RTF |  |
| image/x-portable-pixmap | SRT |  |
| image/x-rgb | TXT |  |
| image/x-xbitmap | VTT |  |
| image/x-xpixmap | XML |  |
| image/x-icon |  |  |
| image/photoshop |  |  |
| image/x-photoshop |  |  |
| image/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

[!DNL Experience Manager] 默认情况下，自动将智能标记添加到基于文本的资产和视频中。要自动向图像添加智能标签，请完成以下任务。

* [ [!DNL Adobe Experience Manager] 使用 Adobe 开发人员控制台进行集成](#integrate-aem-with-aio).
* [了解标签模型和准则](#understand-tag-models-guidelines)。
* [训练模型](#train-model)。
* [标记您的数字资产](#tag-assets)。
* [管理标记和搜索](#manage-smart-tags-and-searches)。

>[!TIP]
>
>智能标记仅适用于[!DNL Adobe Experience Manager Assets]客户。 可以购买智能标记作为[!DNL Experience Manager]的附加组件。

<!-- TBD: Is there a link to buy SCS or initiate a sales call. How are AIO services sold? Provide a CTA here to buy or contacts Sales team. -->

## 使用智能标记{#smart-tag-text-based-assets}标记基于文本的资产

上传时，支持的基于文本的资产会由[!DNL Experience Manager Assets]自动标记。 默认情况下为启用状态。 智能标记的效果不取决于资产中的文本数量，而取决于资产文本中显示的相关关键字或实体。 对于基于文本的资产，智能标记是显示在文本中的关键字，但是最能描述资产的关键字。 对于支持的资产，[!DNL Experience Manager]已提取文本，然后对其进行索引并用于搜索资产。 但是，基于文本中关键字的智能标记提供了专用的、结构化的和更高优先级的搜索彩块，与完整搜索索引相比，该彩块用于改进资产发现。

相比之下，对于图像和视频，智能标签是基于某些视觉方面派生的。

## 将[!DNL Experience Manager]与Adobe Developer Console {#integrate-aem-with-aio}集成

>[!IMPORTANT]
>
>默认情况下，新的[!DNL Experience Manager Assets]部署与[!DNL Adobe Developer Console]集成。 它有助于更快地配置智能标签功能。 在旧版部署中，管理员可以手动[配置智能标签集成](/help/assets/smart-tags-configuration.md#aio-integration)。

您可以使用[!DNL Adobe Developer Console]将[!DNL Adobe Experience Manager]与智能标签集成。 使用此配置可从[!DNL Experience Manager]中访问智能标记服务。 请参阅[configure [!DNL Experience Manager] 以标记资产](smart-tags-configuration.md)，以了解配置智能标记的任务。 在后端，[!DNL Experience Manager]服务器在将请求转发到Smart Tags服务之前，使用Adobe Developer Console网关验证您的服务凭据。

## 了解标签模型和准则{#understand-tag-models-guidelines}

标签模型是一组相关标签，这些标签与被标记的图像的各种视觉方面相关联。 标签与图像的明显不同的可视方面相关，以便在应用标签时有助于搜索特定类型的图像。 例如，鞋类集合可以有不同的标签，但所有标签都与鞋类相关，并且可以属于同一标签模型。 应用这些标签后，可帮助查找不同类型的鞋，例如按颜色、设计或使用情况。 要了解[!DNL Experience Manager]中培训模型的内容表示形式，请将培训模型可视化为由一组手动添加的标记和每个标记的示例图像组成的顶级实体。 每个标签可以专门应用于图像。

在创建标签模型并培训服务之前，请确定一组唯一标签，这些标签最能描述业务环境中图像中的对象。 确保您所选集合中的资源符合[培训准则](#training-guidelines)。

### 培训指南{#training-guidelines}

确保培训集中的图像符合以下准则：

**数量和大小：每** 个标签最少10张图像和最多50张图像。

**一致**:确保标签的图像在视觉上相似。最好将与相同的可视方面（如图像中的相同类型对象）相关的标签一起添加到单个标签模型中。 例如，将所有这些图像标记为`my-party`（用于培训）并不是个好主意，因为它们在视觉上并不相似。

![说明性图像以说明培训准则](assets/do-not-localize/coherence.png)

**覆盖**:培训中的图像应该有足够的多样性。我们的想法是提供一些比较多样的例子，以便AEM学会专注于正确的事情。 如果要对视觉上不同的图像应用相同的标签，请至少包含每种类型的五个示例。 例如，对于标签&#x200B;*model-down-pose*，包含更多与下面突出显示的图像相似的培训图像，以便服务在标记期间更准确地识别类似图像。

![说明性图像以说明培训准则](assets/do-not-localize/coverage_1.png)

**分散注意力/妨碍**:该服务对分散注意力的图像（突出的背景、不相关的伴奏，如与主题有关的物体/人）进行了更好的培训。例如，对于标签&#x200B;*休闲鞋*，第二幅图像不是好的培训候选者。

![说明性图像以说明培训准则](assets/do-not-localize/distraction.png)

**完整性：**&#x200B;如果图像符合多个标记的条件，请在包含培训图像之前添加所有适用的标记。例如，对于 *Raincoat* 和 *model-side-view* 等标记，在将其加入培训之前，在符合条件的资产上添加这两个标记。

![说明性图像以说明培训准则](assets/do-not-localize/completeness.png)

**标记数**:Adobe建议您使用至少两个不同的标签和至少十个不同的图像来训练模型。在单个标记模型中，不要添加50个以上的标记。

**示例数**:对于每个标记，至少添加十个示例。但是，Adobe建议使用大约30个示例。 每个标签最多支持50个示例。

**防止误报和冲突**:Adobe建议为单个可视方面创建单个标签模型。以一种避免模型之间重叠标签的方式构建标签模型。 例如，请勿在两个不同的标签模型名称`shoes`和`footwear`中使用`sneakers`等常用标签。 训练过程将一个训练过的标签模型与另一个覆盖一个公共关键字。

**示例**:一些指导示例包括：

* 创建包含、
   * 只有与车型相关的标签。
   * 只有与衬衫颜色相关的标签。
   * 只有与男女夹克相关的标签。
* 不要创建，
   * 一种标签模型，包括2019年和2020年发布的车型。
   * 包含相同少数几款车型的多个标签模型。

**用于培训的图像**:您可以使用相同的图像来训练不同的标签模型。但是，不要将图像与标签模型中的多个标签相关联。 可以使用属于不同标签模型的不同标签来标记同一图像。

您无法撤消培训。 上述准则应有助于您选择要培训的优质图像。

## 为自定义标签{#train-model}培训模型

要为业务特定标签创建和培训模型，请执行以下步骤：

1. 创建必要的标记和适当的标记结构。 在DAM存储库中上传相关图像。
1. 在[!DNL Experience Manager]用户界面中，访问&#x200B;**[!UICONTROL 资产]** > **[!UICONTROL 智能标签培训]**。
1. 单击&#x200B;**[!UICONTROL 创建]**。提供&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 说明]**。
1. 浏览并从`cq:tags`中要为模型训练的现有标签中选择标签。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL 选择资产]**&#x200B;对话框中，单击每个标记对应的&#x200B;**[!UICONTROL 添加资产]**。 在DAM存储库中搜索或浏览存储库以选择至少10个和最多50个图像。 选择资产，而不是文件夹。 选择图像后，单击&#x200B;**[!UICONTROL 选择]**。

   ![视图培训状态](assets/smart-tags-training-status.png)

1. 要预览选定图像的缩览图，请单击标记前面的折叠面板。 您可以通过单击&#x200B;**[!UICONTROL 添加资产]**&#x200B;来修改您的选择。 对选择满意后，单击&#x200B;**[!UICONTROL 提交]**。 用户界面在页面底部显示通知，指示已启动培训。
1. 检查每个标签模型的&#x200B;**[!UICONTROL Status]**&#x200B;列中培训的状态。 可能的状态为[!UICONTROL 挂起]、[!UICONTROL 已培训]和[!UICONTROL 失败]。

![为智能标签培训标签模型的工作流](assets/smart-tag-model-training-flow.png)

*图：培训工作流中用于培训标记模型的步骤。*

### 视图培训状态和报告{#training-status}

要检查是否在资产培训集中的标记上对智能标记服务进行了培训，请从“报告”控制台中查看培训工作流报告。

1. 在[!DNL Experience Manager]接口中，转至**[!UICONTROL 工具] > **[!UICONTROL 资产] > **[!UICONTROL 报表]**。
1. 在&#x200B;**[!UICONTROL 资产报表]**&#x200B;页面中，单击&#x200B;**[!UICONTROL 创建]**。
1. 选择&#x200B;**[!UICONTROL 智能标记培训]**&#x200B;报告，然后单击工具栏中的&#x200B;**[!UICONTROL 下一步]**。
1. 指定报表的标题和描述。在&#x200B;**[!UICONTROL 计划报告]**&#x200B;下，保持选中&#x200B;**[!UICONTROL 立即]**&#x200B;选项。如果要安排以后的计划报告，请选择&#x200B;**[!UICONTROL 稍后]**，然后指定日期和时间。然后，单击工具栏中的&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 资产报表]**&#x200B;页面中，选择生成的报表。要视图报表，请单击工具栏中的&#x200B;**[!UICONTROL 视图]**。
1. 查看报告的详细信息。 报表显示您培训的标记的培训状态。**[!UICONTROL 培训状态]**&#x200B;列中的绿色表示已为标记培训智能标记服务。 黄色表示服务未针对特定标记进行完整培训。在这种情况下，使用特定标记添加更多图像并运行培训工作流以在标签上完整地培训服务。如果此报表中未显示标记，请再次运行这些标记的培训工作流。标记
1. 要下载报告，请从列表中选择它，然后单击工具栏中的&#x200B;**[!UICONTROL 下载]**。 报告以[!DNL Microsoft Excel]电子表格的形式下载。

## 标记资源{#tag-assets}

在培训了智能标记服务后，您可以触发标记工作流以自动对另一组类似资产应用适当的标记。 您可以定期或在需要时应用标记工作流。 标记工作流同时适用于资产和文件夹。

### 从工作流控制台{#tagging-assets-from-the-workflow-console}中标记资源

1. 在[!DNL Experience Manager]接口中，转至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 在&#x200B;**[!UICONTROL 工作流模型]**&#x200B;页面中，选择&#x200B;**[!UICONTROL DAM智能标记资产]**&#x200B;工作流，然后单击工具栏中的&#x200B;**[!UICONTROL 开始工作流]**。

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 在&#x200B;**[!UICONTROL 运行工作流]**&#x200B;对话框中，浏览至包含要自动应用标记的资产的有效负荷文件夹。
1. 指定工作流的标题和可选注释。 单击&#x200B;**[!UICONTROL 运行]**。

   ![tagging_dialog](assets/tagging_dialog.png)

   *图：导航到资产文件夹并检查标记，以验证您的资产是否已正确标记。有关详细信息，请参阅[管理智能标签](#manage-smart-tags-and-searches)。*

### 从时间轴{#tagging-assets-from-the-timeline}标记资源

1. 从[!DNL Assets]用户界面中，选择包含要应用智能标记的资产或特定资产的文件夹。
1. 从左上角，打开&#x200B;**[!UICONTROL 时间轴]**。
1. 从左侧栏底部打开操作，然后单击&#x200B;**[!UICONTROL 开始工作流]**。

   ![开始_workflow](assets/start_workflow.png)

1. 选择&#x200B;**[!UICONTROL DAM智能标记资产]**&#x200B;工作流，然后为工作流指定标题。
1. 单击&#x200B;**[!UICONTROL 开始]**。 该工作流会对资产应用您的标记。 导航到资产文件夹并检查标记，以验证您的资产是否已正确标记。 有关详细信息，请参阅[管理智能标签](#manage-smart-tags-and-searches)。

>[!NOTE]
>
>在随后的标记周期中，只有修改后的资产再次被标记为新训练的标记。 但是，如果标记工作流的上次和当前标记周期之间的间隙超过24小时，即使是未更改的资产也会被标记。 对于定期添加标签的工作流，当时间间隔超过六个月时，将标记未更改的资产。

### 标记已上载的资产{#tag-uploaded-assets}

[!DNL Experience Manager] 可以自动标记用户上传到DAM的资产。为此，管理员需要配置一个工作流，以添加一个可用的步骤来标记资产。 请参阅[如何为已上传的资产启用智能标记](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets)。

## 管理智能标记和资产搜索{#manage-smart-tags-and-searches}

您可以创建智能标记来删除可能已分配给您的品牌资产的任何不准确标记，以便仅显示最相关的标记。

调节智能标记还可确保您的资产显示在最相关标记的搜索结果中，从而帮助优化基于标记的资产搜索。 本质上，它有助于消除不相关资产出现在搜索结果中的可能性。

您还可以为标记分配更高的排名，以提高标记与资产的相关性。 提升资产的标记可提高在基于特定标记执行搜索时在搜索结果中显示资产的可能性。

要审核资产的智能标记，请执行以下操作：

1. 在搜索字段中，根据标记搜索资产。

1. Inspect搜索结果以标识您找不到与搜索相关的资产。

1. 选择资产，然后从工具栏中选择![管理标记图标](assets/do-not-localize/manage-tags-icon.png)。

1. 在&#x200B;**[!UICONTROL 管理标记]**&#x200B;页中，检查标记。 如果您不希望根据特定标记搜索资产，请选择该标记，然后从工具栏中选择![删除图标](assets/do-not-localize/delete-icon.png)。 或者，选择标签旁的`X`符号。

1. 要为标记指定更高的等级，请选择该标记，然后从工具栏中选择![提升图标](assets/do-not-localize/promote-icon.png)。 您提升的标记将移至&#x200B;**[!UICONTROL Tags]**&#x200B;部分。

1. 选择&#x200B;**[!UICONTROL 保存]**，然后选择&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭[!UICONTROL 成功]对话框。

1. 导航到资产的[!UICONTROL 属性]页面。 请注意，您提升的标记已分配高相关性，因此会在搜索结果中显示得更高。

### 使用智能标签{#understandsearch}了解AEM搜索结果

默认情况下，AEM搜索将搜索词与`AND`子句组合。 使用智能标签不会更改此默认行为。 使用智能标记可添加`OR`子句，以查找所应用智能标记中的任何搜索词。 例如，考虑搜索`woman running`。 默认情况下，元数据中仅包含`woman`或`running`关键字的资产不会显示在搜索结果中。 但是，此类搜索查询中会显示使用智能标签标记为`woman`或`running`的资产。 搜索结果是，

* 元数据中具有`woman`和`running`关键字的资产。

* 使用任一关键字标记的资产智能。

首先显示与元数据字段中所有搜索词匹配的搜索结果，然后显示与智能标记中任何搜索词匹配的搜索结果。 在上例中，搜索结果的大致显示顺序为：

1. `woman running`的匹配项。
1. smart标签中`woman running`的匹配项。
1. smart标签中`woman`或`running`的匹配项。

## 标记限制和最佳实践{#limitations}

增强的智能标记基于图像及其标记的学习模型。 这些模型并不总是能够完美地识别标签。 智能标记的当前版本具有以下限制：

* 无法识别图像中的细微差异。 比如，修身与普通衬衫。
* 无法根据图像的微小图案/部分识别标记。 例如，T恤上的徽标。
* [!DNL Experience Manager]支持的语言支持标记。 有关语言列表，请参阅[智能内容服务发行说明](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html#languages)。
* 未实际处理的标记与以下内容相关：

   * 非可视、抽象方面。 例如，产品发布的年份或季节、由图像引发的情绪或情绪、视频的主观内涵等。
   * 产品（如衬衫、衬衫和衬衫等）的细微视觉差异，或嵌入产品中的小产品徽标。

<!-- TBD: Add limitations related to text-based assets. -->

要使用智能标记（常规或增强）搜索资产，请使用[!DNL Assets]搜索（全文搜索）。 智能标记没有单独的搜索谓词。

>[!NOTE]
>
>智能标签是否可以对您的标签进行培训并将它们应用于其他图像取决于您用于培训的图像质量。
>为获得最佳效果，Adobe建议您使用视觉上相似的图像来针对每个标签培训服务。

>[!MORELIKETHIS]
>
>* [配 [!DNL Experience Manager] 置智能标记](smart-tags-configuration.md)
>* [了解智能标记如何帮助管理资产](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [智能标记视频资产](smart-tags-video-assets.md)

