---
title: 批次集预设
description: 了解如何使用Dynamic Media中的批次集预设自动创建图像集和旋转集。
contentOwner: Rick Brough
feature: Image Presets,Viewer Presets
role: User
exl-id: 022ee347-54ec-4cec-b808-9eb3a9e51424
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '3434'
ht-degree: 0%

---

# 关于批次集预设 {#about-bsp}

当您单独或使用批量摄取将资产文件上传到文件夹时，可使用&#x200B;**[!UICONTROL 批次集预设]**&#x200B;在图像集或旋转集中创建和组织多个资产。 您可以将预设与计划在[!DNL Dynamic Media]中执行的资产导入作业一起运行。 每个预设是一个唯一命名的、自包含的指令集，该指令集定义如何使用与预设方法中定义的命名约定匹配的图像来构建图像集或旋转集。

>[!IMPORTANT]
>
>您是否在[!DNL Dynamic Media Classic]中使用批次集预设，并从[!DNL Dynamic Media Classic]迁移到Adobe Experience Manager as a Cloud Service？ 如果是这样，您必须在[!DNL Adobe Experience Manager as a Cloud Service]中手动重新创建批次集预设定义。

**最佳实践** — 在使用批次集预设时，Adobe建议使用以下工作流：

1. 创建批次集预设。 请参阅[为图像集或旋转集创建批次集预设](#creating-bsp)。
1. 创建资产文件夹或使用现有资产文件夹，并确保它已同步到[!DNL Dynamic Media]。 请参阅[创建文件夹](/help/assets/manage-digital-assets.md#creating-folders)。
1. 将批次集预设应用于资产文件夹。 请参阅[关于将批次集预设应用到文件夹](#apply-bsp)。
1. 将图像上传到资产文件夹。 请参阅[上传图像集的资源](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets)、[上传旋转集的资源](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets)或[将数字资源添加到Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager)。
1. 在所需的文件夹中自动生成图像集或旋转集。
1. Publish您的图像集或旋转集。 请参阅[Publish Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 为图像集或旋转集创建批次集预设 {#creating-bsp}

要创建批集预设，最好对正则表达式有一定的熟悉和了解。

理想情况下，您的公司已经为资产在一个集中的分组方式定义了命名约定。
为了帮助您了解使用命名约定的重要性，假定您公司定义的命名约定为`<style>-<color>-<view>`。 并且，集合的基本名称必须始终为`<style>-<color>`，集合的名称扩展名为`-SET`。 如果上载名为`0123-RED-01`的图像，则会创建一个名为`0123-RED-SET`的集。 如果您稍后上载图像`0123-RED-03`和`0123-BLUE-01`，则会在第二个位置将`RED-03`图像添加到该集，因为该图像的排序低于`01`。 但是，`BLUE-01`映像将成为名为`0123-BLUE-SET`的新集的一部分。 在下次上传资产时，您添加了`0123-RED-02`和`0123-BLUE-02`文件。 每个资产都将添加到其各自的集中。 由于排序顺序，`RED-02`图像将在现有`01`和`03`图像之间自动排序。

[!DNL Dynamic Media]中的&#x200B;**[!UICONTROL 批次集预设]**&#x200B;页面允许您创建、编辑或删除批次集预设，以及在资产文件夹中应用或删除批次集预设。 您可以使用表单字段下拉列表来定义批次集预设，或者使用&#x200B;**[!UICONTROL 原始代码]**&#x200B;字段，该字段允许您键入正则表达式语法。

您可以创建多个批集预设，以便涵盖所需的所有资产引入作业。

### 关于资产命名约定

**[!UICONTROL 批次集预设]**&#x200B;页面上的&#x200B;**[!UICONTROL 资产命名约定]**&#x200B;区域包含两个可用于定义批次集预设的元素： **[!UICONTROL 匹配]**&#x200B;和&#x200B;**[!UICONTROL 基本名称]**。 这些元素允许您定义命名约定，并标识用于命名包含这些规则的集的约定部分。<!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

公司的单个命名惯例通常使用来自这两个元素中每个元素的一行或多行定义。 您可以为唯一定义使用尽可能多的行，并将它们分组为不同的元素，例如用于主图像、颜色元素、替代视图元素和样本元素。

例如，文本匹配正则表达式的语法可能如下所示：

`(\w+)-\w+-\w+`

### 关于序列排序

您可以选择定义在将图像集或旋转集分组到[!DNL Dynamic Media]中后图像的显示顺序。 默认情况下，您的资产按字母数字排序。 但是，您可以使用逗号分隔的正则表达式列表来定义顺序。

关于序列排序自动化，您可以根据需要指定规则以特定方式强制对资产排序。 例如，假设您的第一个资产始终名为`_main`，您希望它后跟`_alt1`、`_alt2`、`_alt3`等。 在这种情况下，您可以使用以下语法创建序列排序规则：

`.*_main,.*_alt[0-9]`

虽然强制排序序列是可行的，但最好尽可能依靠字母数字编号进行序列排序。 此外，您还可以使用[!DNL Dynamic Media]中的图像集或旋转集编辑器工具重新排列资源的顺序，或通过拖放操作在图像集中添加和删除新资源。

创建完批次集预设后，可将其应用于已创建的一个或多个文件夹。 请参阅[关于将批次集预设应用到文件夹](#apply-bsp)。

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**要为图像集或旋转集创建批次集预设：**

1. 选择Experience Manager徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批次集预设]**。

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. 在&#x200B;**[!UICONTROL 批次集预设]**&#x200B;页面的右上角附近，选择&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建批次集预设]**&#x200B;对话框的&#x200B;**[!UICONTROL 预设名称]**&#x200B;文本字段中，输入描述性名称。 如果稍后决定更改预设名称，则预设名称将不可编辑。

1. 在&#x200B;**[!UICONTROL 预设类型]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL 图像集]**&#x200B;或&#x200B;**[!UICONTROL 旋转集]**。 请确保选择正确的预设类型；该预设类型以后将无法编辑。
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 编辑批次集预设]**&#x200B;页面的右侧，在&#x200B;**[!UICONTROL 预设详细信息]**&#x200B;和&#x200B;**[!UICONTROL 设置命名约定]**标题下设置您需要的可编辑选项。
要了解有关您可用的可编辑选项的更多信息，请参阅[预设详细信息、设置命名惯例和规则结果 — RegX选项](#features-options-bsp)。

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. 创建一个或多个正则表达式组。

   * 在&#x200B;**[!UICONTROL 编辑批次集预设]**&#x200B;页面的左侧，在&#x200B;**[!UICONTROL 匹配]**、**[!UICONTROL 基本名称]**&#x200B;或&#x200B;**[!UICONTROL 序列顺序]**&#x200B;下，选择&#x200B;**[!UICONTROL 添加组]**。
   * **[!UICONTROL 匹配]**&#x200B;字段为必填项。 仅当&#x200B;**[!UICONTROL 匹配]**&#x200B;字段尚未使用括号分组指定基名时，**[!UICONTROL 基名]**&#x200B;是必需的。 **[!UICONTROL 序列顺序]**&#x200B;是可选的。
   * 使用组表单中的下拉列表和文本框，指定要用于定义图像集或旋转集资源成员的命名条件的表达式组。
      * 选择并指定组的表达式时，请注意实际的正则表达式语法反映在页面右下角的&#x200B;**[!UICONTROL 规则结果 — RegX]**&#x200B;标题下。 要查看右下角更新的正则表达式字符串，请选择表单区域之外的任意位置。 这些正则表达式字符串表示在搜索[!DNL Dynamic Media]个资源以创建图像集或旋转集时要匹配的模式。
      * 如果已添加组且想要将其删除，请选择&#x200B;**[!UICONTROL X]**。
   * 添加两个或更多组后，在&#x200B;**[!UICONTROL And]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL And]**，以将新添加的组与您之前添加的任何表达式组连接起来。 或者，选择&#x200B;**[!UICONTROL 或]**&#x200B;在以前表达式组和您创建的新组之间添加替代。 **[!UICONTROL Or]**&#x200B;操作数是在正则表达式语法本身中使用垂直行字符`|`定义的。

1. 执行下列操作之一：

   * 若要添加另一个新组，请在&#x200B;**[!UICONTROL 匹配]**、**[!UICONTROL 基本名称]**&#x200B;或&#x200B;**[!UICONTROL 排序顺序]**&#x200B;下，选择&#x200B;**[!UICONTROL 添加组]**。 像上一步中所做的那样创建另一个正则表达式组。
   * 查看&#x200B;**[!UICONTROL 规则结果 — RegX]**&#x200B;区域中的正则表达式语法。 如果必须更改语法，请在页面左侧的相应组中进行编辑。
   * 如果您已完成表达式组的创建，请继续执行下一步。

1. 在页面的右上角，选择&#x200B;**[!UICONTROL 保存]**。

您现在可以将批次集预设应用于资产文件夹。 然后，将资产上传到该文件夹。 此工作流可自动生成图像集或旋转集。 请参阅[关于将批次集预设应用到资源文件夹](#apply-bsp)。

### 预设详细信息、设置命名惯例和规则结果 — RegX选项 {#features-options-bsp}

创建或编辑批次集预设时，这些选项在&#x200B;**[!UICONTROL 编辑批次集预设]**&#x200B;页面上可用。

请参阅[为图像集或旋转集创建批次集预设](#creating-bsp)或[编辑批次集预设](#edit-bsp)。

| **[!UICONTROL 预设详细信息]** | 描述 |
| --- | --- |
| 预设名称 | 只读。 您在首次创建批次集时指定的名称。 如果必须重命名预设，则可以复制现有批次集预设并指定新名称。 请参阅[复制现有批次集预设](#copy-bsp)。 |
| 类型 | 只读。 该类型是在您首次创建批次集时指定的。 复制现有批次集预设不允许您更改其[!UICONTROL 类型]；您必须改为创建预设。 |
| 包括派生的资产 | 可选。 若要使[!DNL Dynamic Media]的IPS（图像生产系统）包含使用您的旋转集或图像集生成的或“派生”的图像，请选择&#x200B;**[!UICONTROL 是]**（默认值）。 派生的资产是用户未直接上传的图像。 相反，上传主资产时，IPS会生成资产。 例如，在[!DNL Dynamic Media]中上传PDF时，IPS从PDF中的页面生成的图像资源被视为派生资源。 |
| 目标文件夹 | 可选。 如果定义大量图像集或旋转集，Adobe建议将这些集与包含资源本身的文件夹分开。 因此，请考虑创建图像集或旋转集文件夹，并将应用程序重定向到将批处理集生成的集放置在此处。<br>在这种情况下，请指定Experience Manager Assets文件夹结构(`/content/dam`)中的哪个文件夹激活批次集预设。 请确保该文件夹已启用[!DNL Dynamic Media]同步，以允许将其作为目标文件夹。 请参阅[在Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)中的文件夹级别配置选择性发布。<br>如果通过文件夹的&#x200B;**[!UICONTROL 属性]**&#x200B;应用预设，则可以为多个文件夹分配给定的批次集预设。 请参阅[从资产文件夹的“属性”页面应用批次集预设](#apply-bsp-to-folders-via-properties)。<br>如果未指定文件夹，将在与上传到的资产文件夹相同的文件夹中创建批次集预设生成的图像集或旋转集。 |
| **[!UICONTROL 设置命名约定]** |  |
| 前缀<br>或<br>后缀 | 可选。 在相应的字段中输入前缀、后缀或同时输入两者。<br>前缀和后缀字段允许您使用特定内容集的替代自定义文件命名惯例创建许多批次集预设。 当公司定义的默认命名方案存在例外时，此方法特别有用。<br>前缀或后缀已添加到您在&#x200B;**[!UICONTROL 资产命名约定]**&#x200B;区域中定义的&#x200B;**[!UICONTROL 基本名称]**&#x200B;中。 通过添加前缀或后缀，可确保图像集或旋转集的创建独立于其他资产。 它还可以进一步帮助其他人识别文件类型。 例如，要确定使用的颜色模式，可以添加作为前缀或后缀`rgb`或`cmyk`。<br>虽然使用批次集预设功能不需要指定集命名约定，但最佳实践建议您使用集命名约定。 通过此实践，您可以定义要分组到集合中的命名约定的多个元素，以帮助简化批次集的创建。 |
| **[!UICONTROL 规则结果 — RegX]** |  |
| 资产命名约定 — 匹配 | 只读。 根据您选择的匹配表单选项或输入的原始代码显示正则表达式语法。 |
| 资产命名约定 — 基本名称 | 只读。 根据所选的“基本名称”表单选项或输入的原始代码显示正则表达式语法。 |
| 序列排序 — 匹配 | 只读。 根据所选的表单选项或输入的原始代码显示正则表达式语法。 |

## 关于将批次集预设应用到资源文件夹 {#apply-bsp}

将批次集预设分配给一个或多个资源文件夹时，任何子文件夹都会自动从其父文件夹继承预设。

您可以将多个批次集预设应用到资产文件夹。

在&#x200B;**[!UICONTROL 卡片]**&#x200B;视图的用户界面中，如果文件夹分配了批次预设，则文件夹中会显示该预设的名称。

要将批次集预设应用于资源文件夹，请使用以下两种方法之一：

* [从“批次集预设”页面将批次集预设应用于资产文件夹](#apply-bsp-to-folders-via-bsp-page) — 此方法为您提供了最大的灵活性。 可以将单个预设或多个预设应用于单个文件夹或多个文件夹。
* [从资产文件夹的“属性”页面应用批次集预设](#apply-bsp-to-folders-via-properties) — 此方法允许您将一个或多个批次集预设应用到单个文件夹。

作为最佳实践，请确保资产文件夹已同步[!DNL Dynamic Media]，然后应用所需的预设。

如果您遇到以下两种情况之一，请重新处理文件夹中的资产：

* 要在已上传资产的现有资产文件夹上运行批次集预设。
* 您稍后可以编辑之前应用于资产文件夹的现有批次集预设。

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### 从“批次集预设”页面将批次集预设应用于资产文件夹 {#apply-bsp-to-folders-via-bsp-page}

1. 选择Experience Manager徽标并导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批次集预设]**。
1. 在&#x200B;**[!UICONTROL 批次集预设]**&#x200B;页面的&#x200B;**[!UICONTROL 预设名称]**&#x200B;列左侧，选中要应用于文件夹的每个批次集预设的复选框。
1. 在工具栏中，选择&#x200B;**[!UICONTROL 将批次预设应用到文件夹]**。
1. 在&#x200B;**[!UICONTROL 选择文件夹]**&#x200B;页面上，选中要应用批次集预设的每个文件夹的复选框。
1. 在&#x200B;**[!UICONTROL 选择文件夹]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 应用]**。

### 从资产文件夹的“属性”页面应用批次集预设 {#apply-bsp-to-folders-via-properties}

1. 选择Experience Manager徽标并转到&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 文件]**。
1. 导航到要在其中应用一个或多个批次集预设的文件夹。
1. 在页面上&#x200B;**[!UICONTROL Name]**&#x200B;列的左侧，选中文件夹的复选框。
1. 在工具栏中选择&#x200B;**[!UICONTROL 属性]**。
1. 在文件夹的“属性”页面上，选择&#x200B;**[!UICONTROL Dynamic Media正在处理]**&#x200B;选项卡。

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. 在&#x200B;**[!UICONTROL 批次集预设]**&#x200B;下，从&#x200B;**[!UICONTROL 预设名称]**&#x200B;下拉列表框中，选择要应用的批次集预设的名称。 上面的屏幕截图显示了两个应用于资产文件夹的选定批次集预设。

   如果&#x200B;**[!UICONTROL 预设名称]**&#x200B;下拉列表框中不存在批次集预设名称，则表示您尚未创建任何批次集预设。 请参阅[为图像集或旋转集创建批次集预设](#creating-bsp)。

   要删除应用的批次集预设，请选择预设类型右侧的&#x200B;**[!UICONTROL X]**。

1. 在页面的右上角，选择&#x200B;**[!UICONTROL 保存并关闭]**。

## 编辑批次集预设 {#edit-bsp}

您可以编辑已创建的现有批次集预设。 您可以更改为资产命名惯例或序列顺序创建的任何表达式组。 如果需要，您还可以更新目标文件夹并设置命名约定。

但是，不能更改预设的名称或预设类型（图像集或旋转集）。 如果有必要更改预设的名称，请复制现有预设并指定新名称。 请参阅[复制批次集预设](#copy-bsp)。

如果您编辑之前应用于文件夹的批次集预设，则新编辑的批次集预设将仅应用于上传到该文件夹的新资源。

如果希望将新编辑的预设重新应用于文件夹中的现有资源，则必须重新处理文件夹。 <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->通过这种方式，现有资产将符合成为图像集或旋转集的一部分并进行添加的资格。 此外，已包含在图像集或旋转集中的现有资产（基于之前使用的批次集预设）不会被删除，并且会按原样显示。 此方案假设他们不再符合新编辑的预设的条件。

**要编辑批次集预设：**

1. 选择Experience Manager徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批次集预设]**。
1. 在&#x200B;**[!UICONTROL 批次集预设]**&#x200B;页面的&#x200B;**[!UICONTROL 预设名称]**&#x200B;列的左侧，检查要更改的批次集预设。
1. 在工具栏中选择&#x200B;**[!UICONTROL 编辑批次集预设]**。
1. 根据需要编辑预设。
1. 在&#x200B;**[!UICONTROL 批次集预设]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 保存]**。

## 复制现有批次集预设 {#copy-bsp}

您可以复制现有的批次集预设，以避免必须手动重新创建复杂的预设，或者只需重命名预设即可。 但是，不能更改使用的预设类型（图像集或旋转集）。

如果复制资产文件夹引用的现有预设，则这些文件夹不会受到影响。

**复制现有批次集预设：**

1. 选择Experience Manager徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批次集预设]**。
1. 在&#x200B;**[!UICONTROL 批次集预设]**&#x200B;页面的&#x200B;**[!UICONTROL 预设名称]**&#x200B;列左侧，选中要复制的批次集预设的复选框。
1. 在工具栏中选择&#x200B;**[!UICONTROL 复制]**。
1. 在&#x200B;**[!UICONTROL 复制批次集预设]**&#x200B;对话框的&#x200B;**[!UICONTROL 标题]**&#x200B;文本框中，键入预设的新名称。

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. 选择&#x200B;**[!UICONTROL 复制]**。

## 关于从文件夹中删除批次集预设 {#remove-bsp-from-folder}

从文件夹中删除批次集预设时，您上传到这些文件夹的任何新资产都不会应用批次集预设。 文件夹中已添加到图像集的现有资产或基于批次集且已应用于文件夹 — continue的打印集的现有资产按原样显示。

如果想从文件夹中&#x200B;*删除*&#x200B;预设，请参阅[删除批次集预设](#delete-bsp)。

可以使用两种方法从文件夹中删除批次集预设。

* [通过“批次集预设”页面从文件夹中删除批次集预设](#remove-bsp-from-folders-via-bsp-page) — 此方法为您提供了最大的灵活性。 您可以从单个或多个文件夹中删除单个预设或多个预设。
* [从文件夹的“属性”页面中删除批次集预设](#remove-bsp-from-folders-via-properties) — 此方法允许您仅从单个文件夹中删除一个或多个批次集预设。

### 通过“批次集预设”页面从文件夹中删除批次集预设 {#remove-bsp-from-folders-via-bsp-page}

1. 选择Experience Manager徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批次集预设]**。
1. 在&#x200B;**[!UICONTROL 批次集预设]**&#x200B;页面的&#x200B;**[!UICONTROL 预设名称]**&#x200B;列左侧，选中要从一个或多个文件夹中删除的一个或多个批次集预设的复选框。
1. 在工具栏中，选择&#x200B;**[!UICONTROL 从文件夹中删除批次预设]**。

1. 在&#x200B;**[!UICONTROL 选择文件夹]**&#x200B;页面上，选择要删除批次集预设的一个或多个文件夹。
1. 在&#x200B;**[!UICONTROL 选择文件夹]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 删除]**。

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. 在&#x200B;**[!UICONTROL 删除配置文件]**&#x200B;对话框中，选择&#x200B;**[!UICONTROL 删除]**。

### 从文件夹的“属性”页面中删除批次集预设 {#remove-bsp-from-folders-via-properties}

1. 选择Experience Manager徽标并导航到&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 文件]**。
1. 导航到要移除一个或多个批次集预设的文件夹。
1. 在页面上&#x200B;**[!UICONTROL Name]**&#x200B;列的左侧，选中文件夹的复选框。
1. 在工具栏中选择&#x200B;**[!UICONTROL 属性]**。
1. 在文件夹的“属性”页面上，选择&#x200B;**[!UICONTROL Dynamic Media正在处理]**。

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. 在&#x200B;**[!UICONTROL 批次集预设]**&#x200B;下，选择预设类型右侧的&#x200B;**[!UICONTROL X]**。

1. 在页面的右上角，选择&#x200B;**[!UICONTROL 保存并关闭]**。

## 删除批次集预设 {#delete-bsp}

您可以删除批次集预设以从[!DNL Dynamic Media]中永久删除它们。 即，它们不再显示在[!UICONTROL 批次集预设]页面上，也不显示在文件夹&#x200B;**[!UICONTROL 属性]**&#x200B;页面上的&#x200B;**[!UICONTROL Dynamic Media处理]**&#x200B;选项卡的&#x200B;**[!UICONTROL 批次集预设]**&#x200B;下拉列表中。 因此，在文件夹重新处理时或将新资产上传到文件夹时，预设不会应用于现有资产。

如果删除之前应用于一个或多个文件夹的预设，则从这些文件夹中的资产创建的任何图像集或旋转集将继续按原样显示。

如果要&#x200B;*从文件夹中*&#x200B;删除预设，请参阅[从文件夹删除批次集预设](#remove-bsp-from-folder)。

**要删除批次集预设：**

1. 选择Experience Manager徽标并导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批次集预设]**。
1. 在&#x200B;**[!UICONTROL 批次集预设]**&#x200B;页面的&#x200B;**[!UICONTROL 预设名称]**&#x200B;列左侧，选中要删除的一个或多个批次集预设的复选框。
1. 在工具栏中选择&#x200B;**[!UICONTROL 删除批次集预设]**。

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. 在&#x200B;**[!UICONTROL 删除批次集预设]**&#x200B;对话框中，选择&#x200B;**[!UICONTROL 删除]**。

   如果要删除的预设已被某个资产文件夹引用，请改为选择&#x200B;**[!UICONTROL 强制删除]**。

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [图像集](/help/assets/dynamic-media/image-sets.md)
>* [旋转集](/help/assets/dynamic-media/spin-sets.md)
>* [在Dynamic Media中配置文件夹级别的选择性发布](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder) — 如果您想了解有关将单个文件夹同步到[!DNL Dynamic Media]的更多信息，请参阅主题中的“同步模式”。
>* [在Cloud Service中创建Dynamic Media配置](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) — 如果您想了解有关将所有文件夹同步到[!DNL Dynamic Media]的更多信息，请参阅主题中的“Dynamic Media同步模式”。
