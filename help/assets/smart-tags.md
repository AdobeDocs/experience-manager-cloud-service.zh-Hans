---
title: 使用人工智能服务标记图像。
description: 使用人为智能服务标记图像，这些服务使用Adobe Sensei服务应用上下文和描述性商业标签。
contentOwner: AG
translation-type: tm+mt
source-git-commit: cc24b16cf17f146e773e7974c649adae1bd10ddf
workflow-type: tm+mt
source-wordcount: '2401'
ht-degree: 5%

---


# 培训智能标签服务并标记图像 {#train-service-tag-assets}

处理数字资产的组织越来越多地在资产元数据中使用分类控制的词汇。 本质上，它包含一列表关键字，员工、合作伙伴和客户通常使用这些关键字来引用和搜索其数字资产。 使用分类控制的词汇标记资产可确保通过基于标签的搜索轻松识别和检索资产。

与自然语言词汇相比，基于业务分类的标签有助于使资产与公司的业务保持一致，并确保最相关的资产出现在搜索中。 例如，汽车制造商可以用型号名称标记汽车图像，以便在搜索时只显示相关图像以设计促销活动。

在后台，Smart Tags使用Adobe Sensei的人工智能 [框架](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) ，根据标签结构和业务分类培训其图像识别算法。 然后，此内容智能用于对另一组资产应用相关标记。

<!-- TBD: Create a similar flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

要使用智能标记，请完成以下任务:

* [将Experience Manager与Adobe Developer Console集成](#integrate-aem-with-aio)。
* [了解标签模型和准则](#understand-tag-models-guidelines)。
* [训练模型](#train-model)。
* [标记您的数字资产](#tag-assets)。
* [管理标记和搜索](#manage-smart-tags-and-searches)。

智能标记仅适用于 [!DNL Adobe Experience Manager Assets] 客户。 智能标记可作为加载项购买 [!DNL Experience Manager]。

<!-- TBD: Is there a link to buy SCS or initiate a sales call. How are AIO services sold? -->

## 与Adobe [!DNL Experience Manager] Developer Console集成 {#integrate-aem-with-aio}

您可以使 [!DNL Adobe Experience Manager] 用Adobe开发人员控制台与智能标记集成。 使用此配置从中访问智能标记服务 [!DNL Experience Manager]。

请参 [阅配置Experience Manager以智能标记资产](smart-tags-configuration.md) ，以便任务配置智能标记。 在后端，服务器在将 [!DNL Experience Manager] 您的请求转发到智能标记服务之前，使用Adobe开发人员控制台网关验证您的服务凭据。

## 了解标签模型和准则 {#understand-tag-models-guidelines}

标记模型是一组相关标记，这些标记通过图像的视觉方面进行。 例如，鞋类集合可以有不同的标签，但所有标签都与鞋类相关，并且可以属于同一标签模型。 标签只能与图像的不同视觉方面相关。 要了解中培训模型的内容表示 [!DNL Experience Manager]形式，请将培训模型可视化为由一组手动添加的标记和每个标记的示例图像组成的顶级实体。 每个标记都可以专门应用于图像。

无法实际处理的标记与以下内容相关：

* 非可视、抽象的方面，如产品的发布年份或季节、由图像引起的情绪或情绪。
* 产品（如衬衫和衬衫，无领子或小产品徽标嵌入产品）中的细微视觉差异。

在创建标签模型并培训服务之前，请确定一组唯一标签，它们最能描述业务环境中图像中的对象。 确保精选集中的资产符合培 [训准则](#training-guidelines)。

### 培训指南 {#training-guidelines}

培训集中的图像应符合以下准则：

**数量和大小：** 每个标签最少10张图像和最多50张图像。

**一致性**: 标记的图像应在视觉上相似。 最好将与相同视觉方面（如图像中相同类型的对象）相关的标签一起添加到单个标签模型中。 例如，将所有这些图像标记为（用于培训）并不是一个好 `my-party` 主意，因为它们在视觉上并不相似。

![说明性图像为培训准则的例证](assets/do-not-localize/coherence.png)

**覆盖**: 培训中的图像应该有足够的多样性。 其思想是提供几个但相当多样化的示例，以便AEM学习将精力集中在正确的事情上。 如果要对视觉上不相似的图像应用同一标签，请至少包含每种类型的五个示例。 例如，对于标签下 *模式姿势*，为服务包括更多与下面突出显示的图像相似的培训图像，以便在标记过程中更准确地识别类似图像。

![说明性图像为培训准则的例证](assets/do-not-localize/coverage_1.png)

**干扰／阻碍**: 该服务更好地训练那些分散注意力的图像（突出的背景、不相关的伴奏，如有主题的物体／人）。 例如，对于标签 *休闲鞋*，第二幅图像不是很好的培训候选者。

![说明性图像为培训准则的例证](assets/do-not-localize/distraction.png)

**完整性：**&#x200B;如果图像符合多个标记的条件，请在包含培训图像之前添加所有适用的标记。例如，对于 *Raincoat* 和 *model-side-view* 等标记，在将其加入培训之前，在符合条件的资产上添加这两个标记。

![说明性图像为培训准则的例证](assets/do-not-localize/completeness.png)

**标记数**: Adobe建议您使用至少两个不同的标签和至少10个不同的图像来培训模型。 在单个标记模型中，不要添加50个以上的标记。

**示例数**: 对于每个标记，至少添加10个示例。 但是，Adobe建议使用大约30个示例。 每个标签最多支持50个示例。

**防止误报和冲突**: Adobe建议为单个可视方面创建单个标签模型。 以避免模型之间重叠标签的方式构建标签模型。 例如，请勿使用常见标记，如在两个不 `sneakers` 同的标记模型名称和中 `shoes` 使用 `footwear`。 培训过程为公共关键字将一个经过培训的标记模型与另一个覆盖。

**示例**: 更多指导示例包括：

* 创建包含、
   * 只有与车型相关的标签。
   * 仅与衬衫颜色相关的标记。
   * 只有男女外套的标签。
* 不要创建，
   * 一种标签模型，包括2019年和2020年发布的车型。
   * 包含相同少数几款车型的多个标签型号。

**用于培训的图像**: 您可以使用相同的图像训练不同的标签模型。 但是，不会将图像与标签模型中的多个标签相关联。 因此，可以用属于不同标签模型的不同标签标记同一图像。

您无法撤消培训。 以上准则应帮助您选择要培训的优质图像。

## 为自定义标记培训模型 {#train-model}

要创建并培训业务特定标签的模型，请执行以下步骤：

1. 创建必要的标记和相应的标记结构。 在DAM存储库中上传相关图像。
1. 在用 [!DNL Experience Manager] 户界面中，访问 **[!UICONTROL “资产]** ”>“ **[!UICONTROL 智能标记培训]**”。
1. 单击&#x200B;**[!UICONTROL 创建]**。提供标 **[!UICONTROL 题]**、 **[!UICONTROL 说明]**。
1. 浏览并选择要培训模型的 `cq:tags` 现有标记中的标记。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 在选择 **[!UICONTROL 资产对话框中]** ，单击每 **[!UICONTROL 个标记]** 对应的“添加资产”。 在DAM存储库中搜索或浏览存储库以选择至少10张和最多50张图像。 选择资产，而不是文件夹。 选择图像后，单击“选 **[!UICONTROL 择]**”。
1. 要预览选定图像的缩览图，请单击标记前面的折叠面板。 您可以通过单击添加资产来修 **[!UICONTROL 改您的选择]**。 对选择满意后，单击“提 **[!UICONTROL 交”]**。 用户界面在页面底部显示通知，指示已开始培训。
1. 检查每个标记模型的“状 **[!UICONTROL 态]** ”列中培训的状态。 可能的状态 [!UICONTROL 有]“待 [!UICONTROL 定”]、“已 [!UICONTROL 培训”]。

![为智能标记培训标记模型的工作流](assets/smart-tag-model-training-flow.png)

*图： 培训工作流中用于培训标记模型的步骤。*

### 视图培训状态和报告 {#training-status}

要检查是否已针对资产培训集中的标记对智能标记服务进行了培训，请从“报告”控制台查看培训工作流报告。

1. 在界 [!DNL Experience Manager] 面中，转到工 **[!UICONTROL 具>资产>报表]**。
1. In the **[!UICONTROL Asset Reports]** page, click **[!UICONTROL Create]**.
1. Select the **[!UICONTROL Smart Tags Training]** report, and then click **[!UICONTROL Next]** from the toolbar.
1. 指定报表的标题和描述。在&#x200B;**[!UICONTROL 计划报告]**&#x200B;下，保持选中&#x200B;**[!UICONTROL 立即]**&#x200B;选项。如果要安排以后的计划报告，请选择&#x200B;**[!UICONTROL 稍后]**，然后指定日期和时间。Then, click **[!UICONTROL Create]** from the toolbar.
1. 在&#x200B;**[!UICONTROL 资产报表]**&#x200B;页面中，选择生成的报表。To view the report, click **[!UICONTROL View]** from the toolbar.
1. 查看报告的详细信息。 报表显示您培训的标记的培训状态。The green color in the **[!UICONTROL Training Status]** column indicates that the Smart Tags service is trained for the tag. 黄色表示服务未针对特定标记进行完整培训。在这种情况下，使用特定标记添加更多图像并运行培训工作流以在标签上完整地培训服务。如果此报告中未显示标记，请再次运行这些标记的培训工作流。标记
1. 要下载报告，请从列表中选择它，然后单击工 **[!UICONTROL 具栏]** 中的下载。 报告以Microsoft Excel电子表格的形式下载。

## 标记资源 {#tag-assets}

在培训了智能标记服务后，您可以触发标记工作流以自动对另一组类似资产应用适当的标记。 您可以定期或在需要时应用标记工作流。 标记工作流同时适用于资产和文件夹。

### 从工作流控制台标记资产 {#tagging-assets-from-the-workflow-console}

1. 在Experience Manager界面中，转到工 **[!UICONTROL 具>工作流>模型]**。
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 在运行 **[!UICONTROL 工作流]** ，浏览至包含要自动应用标记的资产的有效负荷文件夹。
1. 指定工作流的标题和可选注释。 单击“ **[!UICONTROL 运行]**”。

   ![tagging_dialog](assets/tagging_dialog.png)

   导航到资产文件夹并检查标记，以验证您的资产是否已正确标记。 有关详细信息，请参 [阅管理智能标记](#manage-smart-tags-and-searches)。

### 从时间轴标记资产 {#tagging-assets-from-the-timeline}

1. 从资产用户界面中，选择包含要应用智能标记的资产或特定资产的文件夹。
1. 从左上角打开时间 **[!UICONTROL 轴]**。
1. 从左侧提要栏底部打开操作，然后单击“ **[!UICONTROL 开始工作流]**”。

   ![开始工作流](assets/start_workflow.png)

1. 选择DAM **[!UICONTROL 智能标记资产工作流]** ，然后为工作流指定标题。
1. 单击 **[!UICONTROL 开始]**。 该工作流会对资产应用您的标记。 导航到资产文件夹并检查标记，以验证您的资产是否已正确标记。 有关详细信息，请参 [阅管理智能标记](#manage-smart-tags-and-searches)。

>[!NOTE]
>
>在随后的标记周期中，只有修改后的资产会再次使用经过新培训的标记进行标记。但是，如果标记工作流的上一个标记周期与当前标记周期之间的间隔超过24小时，即使资产未更改也会进行标记。 对于定期标记工作流，当时间间隔超过6个月时，将标记未更改的资产。

### 标记已上传的资产 {#tag-uploaded-assets}

Experience Manager可以自动标记用户上传到DAM的资产。 为此，管理员配置工作流，以向智能标记资产添加可用步骤。 了解 [如何为已上传的资产启用智能标记](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets)。

## 管理智能标记和图像搜索 {#manage-smart-tags-and-searches}

您可以创建智能标记以删除可能分配给您的品牌图像的任何不准确标记，以便只显示最相关的标记。

调节智能标签还可确保图像显示在最相关标签的搜索结果中，从而帮助优化基于标签的图像搜索。 从根本上说，它有助于消除不相关图像在搜索结果中出现的可能性。

您还可以为标记分配更高的等级，以提高其与图像的相关性。 提升图像的标记可提高当基于特定标记执行搜索时在搜索结果中出现图像的可能性。

1. 在“全局搜索”框中，根据标记搜索资产。
1. 检查搜索结果以识别与搜索不相关的图像。
1. 选择图像，然后单击工 **[!UICONTROL 具栏中的]** “管理标记”图标。
1. 从“管 **[!UICONTROL 理标记]** ”页面检查标记。 如果不希望根据特定标记搜索图像，请选择该标记，然后单击工具栏中的删除图标。 或者，单 `X` 击标签旁边显示的符号。
1. 要为标记分配更高的等级，请选择标记，然后单击工具栏中的提升图标。 您提升的标记将移到“标记 **[!UICONTROL ”部]** 分。
1. Click **[!UICONTROL Save]**, and then click **[!UICONTROL OK]** to close the Success dialog.
1. 导航到图像的属性页面。 请注意，您提升的标记具有较高的相关性，因此在搜索结果中显示得更高。

### 使用智能标记了解AEM搜索结果 {#understandsearch}

默认情况下，AEM搜索将搜索词与子句 `AND` 组合。 使用智能标记不会更改此默认行为。 使用智能标记可添加 `OR` 一个附加子句，以在应用智能标记中查找任何搜索词。 For example, consider searching for `woman running`. 默认情况下， `woman` 元数据 `running` 中仅包含关键字的资产不会显示在搜索结果中。 但是，在此类搜索查询中， `woman` 会显 `running` 示带有或使用智能标记的资产。 搜索结果是，

* 元数据 `woman` 中 `running` 包含和关键字的资产。

* 使用任一关键字标记的资产智能。

首先显示与元数据字段中所有搜索词匹配的搜索结果，然后显示与智能标记中任何搜索词匹配的搜索结果。 在上例中，搜索结果的近似显示顺序为：

1. 的匹配 `woman running` 项。
1. 智能标 `woman running` 记中的匹配项。
1. 智能标 `woman` 签的 `running` 匹配项或匹配项。

### 标记限制 {#limitations}

增强的智能标签基于品牌图像及其标签的学习模型。 这些模型并不总是能够完美地识别标记。 智能标记的当前版本具有以下限制：

* 无法识别图像中的细微差异。 比如，修身与普通衬衫。
* 无法根据图像的微小图案／部分识别标记。 例如，T恤上的徽标。
* 在支持AEM的语言环境中支持标记。 有关列表语言，请参阅 [智能标记发行说明](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html)。

要使用智能标记（常规或增强）搜索资产，请使用资产搜索（全文搜索）。 智能标记没有单独的搜索谓词。

>[!NOTE]
>
>智能标记是否能够训练您的标记并将它们应用于其他图像，取决于您用于培训的图像质量。
>为获得最佳效果，Adobe建议您使用视觉上相似的图像来针对每个标签培训服务。

>[!MORELIKETHIS]
>
>* [配置Experience Manager以进行智能标记](smart-tags-configuration.md)
>* [了解智能标记如何帮助管理资产](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)

