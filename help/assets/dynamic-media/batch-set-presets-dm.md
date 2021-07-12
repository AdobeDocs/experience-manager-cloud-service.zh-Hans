---
title: 批次集预设
description: 了解如何使用 Dynamic Media 中的批次集预设自动创建图像集和旋转集。
contentOwner: Rick Brough
feature: 图像预设，查看器预设
role: User
exl-id: 022ee347-54ec-4cec-b808-9eb3a9e51424
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '3446'
ht-degree: 1%

---

# 关于批集预设 {#about-bsp}

在您将资产文件单独或使用批量摄取将资产文件上传到文件夹时，使用&#x200B;**[!UICONTROL 批量集预设]**&#x200B;创建并组织图像集或旋转集中的多个资产。 您可以在[!DNL Dynamic Media]中计划的资产导入作业旁边运行预设。 每个预设都是一组唯一命名的自包含说明，这些说明定义了如何使用与预设方法中定义的命名约定相匹配的图像来构建图像集或旋转集。

>[!IMPORTANT]
>
>您是否在[!DNL Dynamic Media Classic]中使用批量集预设，并从[!DNL Dynamic Media Classic]迁移到Adobe Experience Manager作为Cloud Service? 如果存在，则必须在[!DNL Adobe Experience Manager as a Cloud Service]中手动重新创建批集预设定义。

**最佳实践**  — 使用批集预设时，Adobe建议执行以下工作流：

1. 创建批集预设。 请参阅[为图像集或旋转集](#creating-bsp)创建批集预设。
1. 创建资产文件夹或使用现有的资产文件夹，并确保它与[!DNL Dynamic Media]同步。 请参阅[创建文件夹](/help/assets/manage-digital-assets.md#creating-folders)。
1. 将批集预设应用到资产文件夹。 请参阅[关于将批集预设应用到文件夹](#apply-bsp)。
1. 将图像上传到资产文件夹。 请参阅[上传图像集的资产](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets)、[上传旋转集的资产](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets)或[将数字资产添加到Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager)。
1. 图像集或旋转集将在所需的文件夹中自动生成。
1. 发布图像集或旋转集。 请参阅[发布Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 为图像集或旋转集创建批集预设 {#creating-bsp}

要创建批集预设，您应该对正则表达式有一些熟悉和了解。

理想情况下，您的公司已经为资产分组方式定义了命名约定。
为了帮助您了解使用命名约定的重要性，请假定贵公司定义的命名约定为`<style>-<color>-<view>`。 而且，集的基本名称必须始终为`<style>-<color>`，集的名称扩展名为`-SET`。 如果上传名为`0123-RED-01`的图像，则会创建一个名为`0123-RED-SET`的图像集。 如果稍后上传图像`0123-RED-03`和`0123-BLUE-01`，则会将`RED-03`图像添加到第二个位置的集中，因为它的排序顺序低于`01`。 但是，`BLUE-01`图像将属于名为`0123-BLUE-SET`的新集。 为进行下次资产上传，您需要添加文件`0123-RED-02`和`0123-BLUE-02`。 每个资产都将添加到其各自的集合中。 由于排序顺序，`RED-02`图像将在现有`01`和`03`图像之间自动排序。

通过[!DNL Dynamic Media]中的&#x200B;**[!UICONTROL 批集预设]**&#x200B;页面，您可以创建、编辑或删除批集预设，以及在资产文件夹中应用或删除批集预设。 您可以使用表单字段下拉列表来定义批处理集预设，也可以使用&#x200B;**[!UICONTROL Raw Code]**&#x200B;字段，该字段允许您键入正则表达式语法。

您可以创建许多批集预设，以涵盖所需的所有资产摄取作业。

### 关于资产命名约定

**[!UICONTROL 批集预设]**&#x200B;页面上的&#x200B;**[!UICONTROL 资产命名约定]**&#x200B;区域有两个元素，可用于定义批集预设：**[!UICONTROL 匹配]**&#x200B;和&#x200B;**[!UICONTROL 基本名称]**。 通过这些元素，您可以定义命名约定并标识用于命名包含这些约定的集合的约定部分。<!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

公司的单个命名约定通常使用这两个元素中每个元素的一行或多行定义。 您可以为唯一定义使用任意多行的线条，并将它们分组为不同的元素，如“主图像”、“颜色”元素、“替代视图”元素和“色板”元素。

例如，文本匹配正则表达式的语法可能如下所示：

`(\w+)-\w+-\w+`

### 关于序列排序

您可以选择定义在图像集或旋转集分组到[!DNL Dynamic Media]后图像的显示顺序。 默认情况下，您的资产按字母数字顺序排序。 但是，您可以使用逗号分隔的正则表达式列表来定义顺序。

关于序列排序自动化，您可以指定规则，以便在必要时以特定方式强制对资产进行排序。 例如，假定您的第一个资产始终名为`_main`，并且您希望其后跟`_alt1`、`_alt2`、`_alt3`等。 在这种情况下，您可以使用以下语法创建序列排序规则：

`.*_main,.*_alt[0-9]`

虽然可以强制排序序列，但最好依赖字母数字编号来排序序列。 此外，您还可以使用[!DNL Dynamic Media]中的图像集或旋转集编辑器工具来重新排列资产的顺序，或通过拖放操作在资产集中添加和删除新资产。

创建完批集预设后，您可以将其应用到已创建的一个或多个文件夹。 请参阅[关于将批集预设应用到文件夹](#apply-bsp)。

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**要为图像集或旋转集创建批集预设，请执行以下操作：**

1. 选择Experience Manager徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 批量集预设]**。

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. 在&#x200B;**[!UICONTROL 批量集预设]**&#x200B;页面右上角附近，选择&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建批集预设]**&#x200B;对话框的&#x200B;**[!UICONTROL 预设名称]**&#x200B;文本字段中，输入描述性名称。 如果您稍后决定更改预设名称，则该预设名称将不可编辑。

1. 在&#x200B;**[!UICONTROL 预设类型]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL ImageSet]**&#x200B;或&#x200B;**[!UICONTROL SpinSet]**。 确保选择正确的预设类型；以后无法编辑。
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 编辑批集预设]**&#x200B;页面右侧的&#x200B;**[!UICONTROL 预设详细信息]**&#x200B;和&#x200B;**[!UICONTROL 设置命名约定]**标题下，设置所需的可编辑选项。
要了解有关可供您使用的可编辑选项的更多信息，请参阅[预设详细信息、设置命名约定和规则结果 — RegX选项](#features-options-bsp)。

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. 创建一个或多个正则表达式组。

   * 在“**[!UICONTROL 编辑批集预设]**”页左侧的“**[!UICONTROL 匹配]**”、“**[!UICONTROL 基本名称]**”或“**[!UICONTROL 序列排序]**”下，选择“**[!UICONTROL 添加组]**”。
   * **[!UICONTROL Match]**&#x200B;字段为必填字段。 **[!UICONTROL 只有]** 在匹配字段尚未通 **** 过括号分组指定基本名称时，“基本名称”才是必需的。**[!UICONTROL 序列]** 排序是可选的。
   * 使用组表单中的下拉列表和文本框，指定要用于为图像集或旋转集资产成员定义命名标准的表达式组。
      * 当您选择并指定组的表达式时，请注意实际正则表达式语法反映在页面右下方的&#x200B;**[!UICONTROL 规则结果 — RegX]**&#x200B;标题下。 要查看在右下方更新的正则表达式字符串，请选择表单区域外的任意位置。 这些正则表达式字符串表示您要在搜索[!DNL Dynamic Media]资产以创建图像集或旋转集时匹配的模式。
      * 如果已添加组并要删除该组，请选择&#x200B;**[!UICONTROL X]**。
   * 添加两个或多个组时，在&#x200B;**[!UICONTROL 和]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL 和]**&#x200B;将新添加的组与之前添加的任何表达式组连接起来。 或者，选择&#x200B;**[!UICONTROL Or]**&#x200B;以在上一个表达式组与您创建的新组之间添加交替。 **[!UICONTROL Or]**&#x200B;操作数由在正则表达式语法本身中使用垂直行字符`|`来定义。

1. 执行下列操作之一：

   * 要添加另一个新组，请在&#x200B;**[!UICONTROL Match]**、**[!UICONTROL Base Name]**&#x200B;或&#x200B;**[!UICONTROL Sequencing Order]**&#x200B;下，选择&#x200B;**[!UICONTROL Add Group]**。 创建另一个正则表达式组（与上一步中的操作相同）。
   * 查看&#x200B;**[!UICONTROL 规则结果 — RegX]**&#x200B;区域中的正则表达式语法。 如果必须更改语法，请在页面左侧的相应组中进行编辑。
   * 如果已创建完表达式组，请继续下一步。

1. 在页面的右上角，选择&#x200B;**[!UICONTROL Save]**。

现在，您可以将批集预设应用到资产文件夹。 然后，您将资产上传到该文件夹。 此工作流会自动生成图像集或旋转集。 请参阅[关于将批集预设应用到资产文件夹](#apply-bsp)。

### 预设详细信息、设置命名约定和规则结果 — RegX选项 {#features-options-bsp}

创建或编辑批集预设时，“编辑批集预设”]**页面上提供了这些选项。**[!UICONTROL 

请参阅[为图像集、旋转集](#creating-bsp)或[创建批集预设](#edit-bsp)编辑批集预设。

| **[!UICONTROL 预设详细信息]** | 描述 |
| --- | --- |
| 预设名称 | 只读. 首次创建批处理集时指定的名称。 如果必须重命名预设，则可以复制现有的批次集预设并指定新名称。 请参阅[复制现有批集预设](#copy-bsp)。 |
| 类型 | 只读. 首次创建批处理集时指定了类型。 复制现有的批集预设不会更改其[!UICONTROL 类型];您必须改为创建预设。 |
| 包括派生的资产 | 可选。要使[!DNL Dynamic Media]的IPS（图像生成系统）包含旋转集或图像集中生成或“派生”的图像，请选择&#x200B;**[!UICONTROL 是]**（默认）。 派生资产是指用户未直接上传的图像。 资产由IPS在上传主控资产时生成。 例如，在[!DNL Dynamic Media]中上传PDF时，IPS从PDF中的页面生成的图像资产被视为派生资产。 |
| 目标文件夹 | 可选。如果您定义大量图像集或旋转集，Adobe建议您将这些集与包含资产本身的文件夹分开。 因此，请考虑创建图像集或旋转集文件夹，并重定向应用程序以将批量集生成的集放置在此处。<br>在这种情况下，请指定Experience Manager资产文件夹结构(`/content/dam`)中的哪个文件夹激活了批集预设。确保已启用文件夹进行[!DNL Dynamic Media]同步，以允许将其作为目标文件夹。 请参阅[在Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)的文件夹级别配置选择性发布。<br>如果您通过文件夹的“属性”来应用预设，则可以为多个文件夹分配给定的批集 **[!UICONTROL 预设]**。请参阅[从资产文件夹的“属性”页面](#apply-bsp-to-folders-via-properties)应用批集预设。<br>如果您没有指定文件夹，则会在与上传到的资产文件夹相同的文件夹中创建批量集预设生成的图像集或旋转集。 |
| **[!UICONTROL 设置命名规则]** |  |
| 前缀<br>或<br>后缀 | 可选。在相应的字段中输入前缀、后缀或两者。<br>使用前缀和后缀字段，您可以为特定内容集使用替代的自定义文件命名约定来创建许多批次集预设。当公司定义的默认命名方案存在例外时，此方法特别有用。<br>前缀或后缀会添加到您在资产命 **[!UICONTROL 名约定]** 区域中定义的基 **[!UICONTROL 本名称]** 中。通过添加前缀或后缀，您可以确保仅以独立于其他资产的方式创建图像集或旋转集。 它还可用于进一步帮助他人识别文件类型。 例如，要确定所使用的颜色模式，可以添加作为前缀或后缀`rgb`或`cmyk`。<br>虽然使用批量集预设功能不需要指定集命名约定，但最佳实践建议您使用集命名约定。通过此实践，您可以定义要分组到一组中的命名约定中的任意多个元素，以帮助简化批量集创建过程。 |
| **[!UICONTROL 规则结果 - RegX]** |  |
| 资产命名约定 — 匹配 | 只读. 根据您选择的“匹配”表单选项或您输入的原始代码显示正则表达式语法。 |
| 资产命名约定 — 基本名称 | 只读. 根据您选择的“基本名称”表单选项或您输入的原始代码显示正则表达式语法。 |
| 序列排序 — 匹配 | 只读. 根据您选择的表单选项或您输入的原始代码显示正则表达式语法。 |

## 关于将批集预设应用到资产文件夹 {#apply-bsp}

当您将批集预设分配给一个或多个资产文件夹后，该文件夹中的所有子文件夹都会自动继承父文件夹的预设。

您可以将多个批次集预设应用到资产文件夹。

如果文件夹已经分配了批量预设，则会在用户界面的&#x200B;**[!UICONTROL 卡片]**&#x200B;视图中显示该预设的名称。

要将批集预设应用到资产文件夹，请使用以下两种方法之一：

* [从“批集预设”页面将批集预设应用到资产文件夹](#apply-bsp-to-folders-via-bsp-page)  — 此方法为您提供了最大的灵活性。您可以将单个或多个预设应用到一个或多个文件夹。
* [从资产文件夹的“属性”页面应用批集预设](#apply-bsp-to-folders-via-properties)  — 此方法允许您将一个或多个批集预设应用到单个文件夹。

作为最佳实践，请确保资产文件夹已同步[!DNL Dynamic Media]，然后应用所需的预设。

如果您遇到以下两种情况之一，请重新处理文件夹中的资产：

* 您想要在已上传资产的现有资产文件夹中运行批量集预设。
* 您稍后会编辑以前应用于资产文件夹的现有批集预设。

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### 从“批集预设”页面将批集预设应用到资产文件夹 {#apply-bsp-to-folders-via-bsp-page}

1. 选择Experience Manager徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 批量集预设]**。
1. 在&#x200B;**[!UICONTROL 批集预设]**&#x200B;页面的&#x200B;**[!UICONTROL 预设名称]**&#x200B;列左侧，选中要应用于文件夹的每个批集预设的复选框。
1. 在工具栏中，选择&#x200B;**[!UICONTROL 将批量预设应用到文件夹]**。
1. 在&#x200B;**[!UICONTROL 选择文件夹]**&#x200B;页面上，选中要应用批集预设的每个文件夹的复选框。
1. 在&#x200B;**[!UICONTROL 选择文件夹]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 应用]**。

### 从资产文件夹的“属性”页面应用批集预设 {#apply-bsp-to-folders-via-properties}

1. 选择Experience Manager徽标，然后转到&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**。
1. 导航到要在其中应用一个或多个批集预设的文件夹。
1. 在页面的&#x200B;**[!UICONTROL 名称]**&#x200B;列左侧，选中文件夹的复选框。
1. 在工具栏中，选择&#x200B;**[!UICONTROL 属性]**。
1. 在文件夹的“属性”页面上，选择&#x200B;**[!UICONTROL Dynamic Media处理]**&#x200B;选项卡。

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. 在&#x200B;**[!UICONTROL 批集预设]**&#x200B;下，从&#x200B;**[!UICONTROL 预设名称]**&#x200B;下拉列表框中，选择要应用的批集预设的名称。 上面的屏幕截图显示了两个选定的批次集预设，这些预设将应用于资产文件夹。

   如果“**[!UICONTROL 预设名称]**”下拉列表框中不存在批集预设名称，则表示您尚未创建任何批集预设。 请参阅[为图像集或旋转集](#creating-bsp)创建批集预设。

   要删除应用的批集预设，请选择预设类型右侧的&#x200B;**[!UICONTROL X]**。

1. 在页面的右上角，选择&#x200B;**[!UICONTROL 保存并关闭]**。

## 编辑批集预设 {#edit-bsp}

您可以编辑已创建的现有批集预设。 您可以更改为资产命名约定或序列顺序创建的任何表达式组。 如果需要，您还可以更新目标文件夹并设置命名约定。

但是，您无法更改预设的名称或预设类型（图像集或旋转集）。 如果需要更改预设的名称，请复制现有预设并指定新名称。 请参阅[复制批集预设](#copy-bsp)。

如果您编辑之前已应用于文件夹的批次集预设，则新编辑的批次集预设将仅应用于上传到该文件夹的新资产。

如果您希望将新编辑的预设重新应用于文件夹中的现有资产，则必须重新处理该文件夹。 <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->这样，现有资产现在就有资格成为图像集或旋转集的一部分并进行添加。此外，图像集或旋转集中已包含的现有资产（基于之前使用的批集预设）不会被删除并按原样显示。 此方案假定他们不再基于新编辑的预设进行资格鉴定。

**要编辑批集预设，请执行以下操作：**

1. 选择Experience Manager徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 批量集预设]**。
1. 在&#x200B;**[!UICONTROL 批集预设]**&#x200B;页面的&#x200B;**[!UICONTROL 预设名称]**&#x200B;列左侧，选中要更改的批集预设。
1. 在工具栏中，选择&#x200B;**[!UICONTROL 编辑批集预设]**。
1. 根据需要编辑预设。
1. 在&#x200B;**[!UICONTROL 批量集预设]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 保存]**。

## 复制现有批集预设 {#copy-bsp}

您可以复制现有的批集预设，以避免手动重新创建复杂的预设，或者只需重命名预设即可。 但是，您无法更改使用的预设类型（图像集或旋转集）。

如果复制由资产文件夹引用的现有预设，则这些文件夹不会受到影响。

**复制现有的批集预设：**

1. 选择Experience Manager徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 批量集预设]**。
1. 在&#x200B;**[!UICONTROL 批集预设]**&#x200B;页面的&#x200B;**[!UICONTROL 预设名称]**&#x200B;列左侧，选中要复制的批集预设复选框。
1. 在工具栏中，选择&#x200B;**[!UICONTROL Copy]**。
1. 在&#x200B;**[!UICONTROL 复制批量集预设]**&#x200B;对话框的&#x200B;**[!UICONTROL 标题]**&#x200B;文本框中，为预设键入新名称。

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. 选择&#x200B;**[!UICONTROL Copy]**。

## 关于从文件夹中删除批集预设 {#remove-bsp-from-folder}

当您从文件夹删除批集预设时，您上传到这些文件夹的任何新资产都不会对这些资产应用批次集预设。 文件夹中已添加到图像集或基于批量集预设（已应用于文件夹）的现有资产会继续按原样显示。

如果要改为从文件夹中&#x200B;*删除*&#x200B;预设，请参阅[删除批集预设](#delete-bsp)。

可使用两种方法从文件夹中删除批集预设。

* [通过“批集预设”页面从文件夹删除批集预设](#remove-bsp-from-folders-via-bsp-page)  — 此方法为您提供了最大的灵活性。您可以从一个或多个文件夹中删除一个或多个预设。
* [从文件夹的“属性”页面中删除批集预设](#remove-bsp-from-folders-via-properties)  — 此方法允许您仅从单个文件夹中删除一个或多个批集预设。

### 通过“批集预设”页面从文件夹删除批集预设 {#remove-bsp-from-folders-via-bsp-page}

1. 选择Experience Manager徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 批量集预设]**。
1. 在&#x200B;**[!UICONTROL 批集预设]**&#x200B;页面的&#x200B;**[!UICONTROL 预设名称]**&#x200B;列左侧，选中您要从一个或多个文件夹中删除的一个或多个批集预设的复选框。
1. 在工具栏中，选择&#x200B;**[!UICONTROL 从文件夹中删除批量预设]**。

1. 在&#x200B;**[!UICONTROL 选择文件夹]**&#x200B;页面上，选择一个或多个要删除批集预设的文件夹。
1. 在&#x200B;**[!UICONTROL 选择文件夹]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 删除]**。

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. 在&#x200B;**[!UICONTROL 删除配置文件]**&#x200B;对话框中，选择&#x200B;**[!UICONTROL 删除]**。

### 从文件夹的“属性”页面中删除批集预设 {#remove-bsp-from-folders-via-properties}

1. 选择Experience Manager徽标，然后导航到&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 文件]**。
1. 导航到要删除一个或多个批集预设的文件夹。
1. 在页面的&#x200B;**[!UICONTROL 名称]**&#x200B;列左侧，选中文件夹的复选框。
1. 在工具栏中，选择&#x200B;**[!UICONTROL 属性]**。
1. 在文件夹的“属性”页面上，选择&#x200B;**[!UICONTROL Dynamic Media处理]**。

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. 在&#x200B;**[!UICONTROL 批量集预设]**&#x200B;下，选择预设类型右侧的&#x200B;**[!UICONTROL X]**。

1. 在页面的右上角，选择&#x200B;**[!UICONTROL 保存并关闭]**。

## 删除批集预设 {#delete-bsp}

您可以删除批集预设，以从[!DNL Dynamic Media]中永久删除这些预设。 也就是说，它们不再显示在文件夹&#x200B;**[!UICONTROL 属性]**&#x200B;页面的&#x200B;**[!UICONTROL Dynamic Media处理]**&#x200B;选项卡的[!UICONTROL 批集预设]页面上，也不显示在&#x200B;**[!UICONTROL 批集预设]**&#x200B;下拉列表中。 因此，重新处理文件夹时或在文件夹中上传新资产时，预设不会应用于现有资产。

如果删除之前应用于一个或多个文件夹的预设，则从这些文件夹中的资产创建的任何图像集或旋转集将继续按原样显示。

如果您希望从文件夹中&#x200B;*删除*&#x200B;预设，请参阅[从文件夹中删除批集预设](#remove-bsp-from-folder)。

**要删除批集预设，请执行以下操作：**

1. 选择Experience Manager徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 批量集预设]**。
1. 在&#x200B;**[!UICONTROL 批集预设]**&#x200B;页面的&#x200B;**[!UICONTROL 预设名称]**&#x200B;列左侧，选中一个或多个要删除的批集预设的复选框。
1. 在工具栏中，选择&#x200B;**[!UICONTROL 删除批集预设]**。

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. 在&#x200B;**[!UICONTROL 删除批集预设]**&#x200B;对话框中，选择&#x200B;**[!UICONTROL 删除]**。

   如果要删除的预设被资产文件夹引用，请改为选择&#x200B;**[!UICONTROL 强制删除]**。

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [图像集](/help/assets/dynamic-media/image-sets.md)
* [旋转集](/help/assets/dynamic-media/spin-sets.md)
* [在Dynamic Media中在文件夹级别配置选择性发布](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)  — 如果要了解有关将单个文件夹同步到的更多信息，请参阅主题中的“同步模式”  [!DNL Dynamic Media]。
* [在Cloud Services中创建Dynamic Media配置](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)  — 如果您想了解有关将所有文件夹同步到的更多信息，请参阅主题中的“Dynamic Media同步模式” [!DNL Dynamic Media]。

