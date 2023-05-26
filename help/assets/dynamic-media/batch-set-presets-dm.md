---
title: 批次集预设
description: 了解如何使用 Dynamic Media 中的批次集预设自动创建图像集和旋转集。
contentOwner: Rick Brough
feature: Image Presets,Viewer Presets
role: User
exl-id: 022ee347-54ec-4cec-b808-9eb3a9e51424
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '3442'
ht-degree: 1%

---

# 关于批次集预设 {#about-bsp}

使用 **[!UICONTROL 批次集预设]** 在单独或使用批量摄取将资源文件上传到文件夹时，在图像集或旋转集中创建和组织多个资源。 您可以使预设与计划在其中运行的资产导入作业一起运行 [!DNL Dynamic Media]. 每个预设都是唯一命名的、自包含的一组指令，这些指令定义如何使用与预设方法中定义的命名约定匹配的图像来构建图像集或旋转集。

>[!IMPORTANT]
>
>是否在中使用批次集预设 [!DNL Dynamic Media Classic]，并从迁移 [!DNL Dynamic Media Classic] Adobe Experience Manager as a Cloud Service？ 如果是这样，您必须手动在中重新创建批次集预设定义 [!DNL Adobe Experience Manager as a Cloud Service].

**最佳实践**  — 使用批次集预设时，Adobe建议执行以下工作流程：

1. 创建批次集预设。 参见 [为图像集或旋转集创建批次集预设](#creating-bsp).
1. 创建一个资源文件夹或使用现有的资源文件夹，并确保它已同步到 [!DNL Dynamic Media]. 参见 [创建文件夹](/help/assets/manage-digital-assets.md#creating-folders).
1. 将批次集预设应用于资源文件夹。 参见 [关于将批次集预设应用于文件夹](#apply-bsp).
1. 将图像上传到资源文件夹。 参见 [上传图像集的资产](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets)， [上传旋转集的资产](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets)，或 [将数字资源添加到Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager).
1. 在所需的文件夹中自动生成图像集或旋转集。
1. 发布图像集或旋转集。 参见 [发布Dynamic Media资源](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## 为图像集或旋转集创建批次集预设 {#creating-bsp}

要创建批集预设，最好对正则表达式有一定的了解和理解。

理想情况下，贵公司已定义一个命名约定，用于说明如何将资产分组到一个集中。
为了帮助您了解使用命名约定的重要性，假定您公司定义的命名约定是 `<style>-<color>-<view>`. 并且，集合的基本名称必须始终为 `<style>-<color>`，并将名称扩展设置为 `-SET`. 如果您上传的图像 `0123-RED-01`，则会创建一个名为的集 `0123-RED-SET`. 如果您稍后上传图像 `0123-RED-03` 和 `0123-BLUE-01`，则 `RED-03` 图像将被添加到位于第二个位置的集，因为它的排序低于 `01`. 但是， `BLUE-01` 图像将成为名为的新集的一部分 `0123-BLUE-SET`. 在下次上传资产时，您需要添加文件 `0123-RED-02` 和 `0123-BLUE-02`. 每个资产都将添加到其各自的集中。 此 `RED-02` 图像将自动在现有 `01` 和 `03` 图像（由于排序顺序）。

此 **[!UICONTROL 批次集预设]** 页面位置 [!DNL Dynamic Media] 可创建、编辑或删除批次集预设，以及将批次集预设应用于资源文件夹或从资源文件夹中删除批次集预设。 您可以使用表单字段下拉列表来定义批次集预设，也可以使用 **[!UICONTROL 原始代码]** 字段，用于键入正则表达式语法。

您可以创建多个批集预设，以便涵盖所需的所有资产提取任务。

### 关于资产命名约定

此 **[!UICONTROL 资产命名约定]** 区域 **[!UICONTROL 批次集预设]** 页面包含两个可用于定义批次集预设的元素： **[!UICONTROL 匹配]** 和 **[!UICONTROL 基本名称]**. 这些元素允许您定义命名约定，并标识用于命名包含这些规则的集的约定部分。 <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

公司的单个命名惯例通常使用来自这两个元素中每个元素的一个或多个定义行。 您可以为唯一定义使用任意数量的行，并将它们分组为不同的元素，例如对于“主图像”、“颜色”元素、“替代视图”元素和“样本”元素。

例如，文本匹配正则表达式的语法可能如下所示：

`(\w+)-\w+-\w+`

### 关于序列排序

您可以选择定义在将图像集或旋转集分组到下列位置后图像的显示顺序 [!DNL Dynamic Media]. 默认情况下，您的资产按字母数字排序。 但是，您可以使用逗号分隔的正则表达式列表来定义顺序。

关于序列排序自动化，您可以指定规则以特定方式对资产强制排序（如有必要）。 例如，假定您的第一个资产始终名为 `_main` 你希望它跟着 `_alt1`， `_alt2`， `_alt3`，等等。 在这种情况下，您可以使用以下语法创建序列排序规则：

`.*_main,.*_alt[0-9]`

虽然强制排序序列是可能的，但最好尽可能依靠字母数字编号进行序列排序。 此外，还可以在中使用图像集或旋转集编辑器工具 [!DNL Dynamic Media] 以重新排列资源的顺序，或者使用拖放操作在资源集中添加和删除新资源。

创建完批次集预设后，可将其应用于已创建的一个或多个文件夹。 参见 [关于将批次集预设应用于文件夹](#apply-bsp).

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**要为图像集或旋转集创建批次集预设，请执行以下操作：**

1. 选择Experience Manager徽标并转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 批次集预设]**.

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. 在 **[!UICONTROL 批次集预设]** 页面，右上角附近，选择 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建批次集预设]** 对话框，在 **[!UICONTROL 预设名称]** 文本字段，输入描述性名称。 如果稍后决定更改预设名称，则无法对其进行编辑。

1. 在 **[!UICONTROL 预设类型]** 下拉列表，选择 **[!UICONTROL 图像集]** 或 **[!UICONTROL 旋转集]**. 请确保选择正确的预设类型；该预设类型以后不可编辑。
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 在右侧 **[!UICONTROL 编辑批次集预设]** 页面，在“ ”下设置您需要的可编辑选项 **[!UICONTROL 预设详细信息]** 和 **[!UICONTROL 设置命名约定]** 标题。
要了解有关您可用的可编辑选项的更多信息，请参阅 [预设详细信息、设置命名惯例和规则结果 — RegX选项](#features-options-bsp).

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. 创建一个或多个正则表达式组。

   * 在左侧 **[!UICONTROL 编辑批次集预设]** 页面，下 **[!UICONTROL 匹配]**， **[!UICONTROL 基本名称]**，或 **[!UICONTROL 序列排序]**，选择 **[!UICONTROL 添加组]**.
   * 此 **[!UICONTROL 匹配]** 字段为必填项。 **[!UICONTROL 基本名称]** 仅当满足以下条件时，才为必填项 **[!UICONTROL 匹配]** 字段尚未使用括号分组指定基本名称。 **[!UICONTROL 序列排序]** 是可选的。
   * 使用组表单中的下拉列表和文本框，指定要用于定义图像集或旋转集资源成员的命名条件的表达式组。
      * 当您选择并指定组的表达式时，请注意，实际的正则表达式语法反映在页面右下角的 **[!UICONTROL 规则结果 — RegX]** 标题。 若要查看右下角更新的正则表达式字符串，请选择表单区域之外的任意位置。 这些正则表达式字符串表示要在搜索中匹配的模式 [!DNL Dynamic Media] 资产，以创建图像集或旋转集。
      * 如果已添加组并要删除它，请选择 **[!UICONTROL X]**.
   * 添加两个或更多组时，在 **[!UICONTROL 和]** 下拉列表，选择 **[!UICONTROL 和]** 将新添加的组与之前添加的任何表达式组连接起来。 或者，选择 **[!UICONTROL 或]** 在先前表达式组和您创建的新组之间添加替代。 此 **[!UICONTROL 或]** 操作数通过使用垂直行字符来定义 `|` 正则表达式语法本身。

1. 执行下列操作之一：

   * 要添加另一个新组，请在 **[!UICONTROL 匹配]**， **[!UICONTROL 基本名称]**，或 **[!UICONTROL 排序顺序]**，选择 **[!UICONTROL 添加组]**. 像上一步中所做的那样创建另一个正则表达式组。
   * 在中查看正则表达式语法 **[!UICONTROL 规则结果 — RegX]** 区域。 如果必须更改语法，请在页面左侧的相应组中进行编辑。
   * 如果已完成表达式组的创建，请继续执行下一步。

1. 在页面的右上角，选择 **[!UICONTROL 保存]**.

您现在可以将批次集预设应用到资产文件夹。 然后，将资产上传到该文件夹。 此工作流可自动生成图像集或旋转集。 参见 [关于将批次集预设应用于资源文件夹](#apply-bsp).

### 预设详细信息、设置命名惯例和规则结果 — RegX选项 {#features-options-bsp}

这些选项位于 **[!UICONTROL 编辑批次集预设]** 创建或编辑批次集预设时显示的页面。

参见 [为图像集或旋转集创建批次集预设](#creating-bsp) 或 [编辑批次集预设](#edit-bsp).

| **[!UICONTROL 预设详细信息]** | 描述 |
| --- | --- |
| 预设名称 | 只读. 首次创建批次集时指定的名称。 如果必须重命名预设，则可以复制现有批次集预设并指定新名称。 参见 [复制现有批次集预设](#copy-bsp). |
| 类型 | 只读. 该类型是在您首次创建批次集时指定的。 复制现有批次集预设不允许您更改其 [!UICONTROL 类型]；您必须改为创建预设。 |
| 包括派生的资产 | 可选. 拥有 [!DNL Dynamic Media]的IPS（图像生产系统）包含生成的或“派生”的图像以及旋转集或图像集，请选择 **[!UICONTROL 是]** （默认）。 派生的资产是用户未直接上传的图像。 相反，在上传主控资源时，IPS会生成资源。 例如，在上传PDF时，IPS从PDF中的页面生成的图像资源 [!DNL Dynamic Media]，被视为派生资产。 |
| 目标文件夹 | 可选. 如果定义大量图像集或旋转集，Adobe建议将这些集与包含资源本身的文件夹分开。 因此，请考虑创建图像集或旋转集文件夹，并将应用程序重定向到将批处理集生成的集放置在此处。<br>在这种情况下，请指定Experience Manager Assets文件夹结构中的文件夹(`/content/dam`)激活批次集预设。 确保文件夹已启用 [!DNL Dynamic Media] 同步，以允许将其作为目标文件夹。 参见 [在Dynamic Media中配置文件夹级别的选择性发布](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder).<br>如果通过文件夹的 **[!UICONTROL 属性]**. 参见 [从资源文件夹的“属性”页面应用批次集预设](#apply-bsp-to-folders-via-properties).<br>如果不指定文件夹，将在与上传到的资产文件夹相同的文件夹中创建批次集预设生成的图像集或旋转集。 |
| **[!UICONTROL 设置命名规则]** |  |
| 前缀<br>或<br>后缀 | 可选. 在相应的字段中输入前缀、后缀或两者。<br>通过“前缀”和“后缀”字段，您可以使用特定内容集的替代自定义文件命名惯例来创建许多批次集预设。 当公司定义的默认命名方案有例外时，此方法特别有用。<br>前缀或后缀将添加到 **[!UICONTROL 基本名称]** 您在中定义 **[!UICONTROL 资产命名约定]** 区域。 通过添加前缀或后缀，可确保图像集或旋转集的创建独立于其他资产。 它还可以进一步帮助其他人识别文件类型。 例如，要确定使用的颜色模式，可以添加作为前缀或后缀 `rgb` 或 `cmyk`.<br>虽然指定集命名惯例不是使用批次集预设功能所必需的，但最佳实践建议您使用集命名惯例。 通过此实践，您可以定义命名惯例的任意多个元素，并将这些元素分组到一个集中，以帮助简化批次集的创建。 |
| **[!UICONTROL 规则结果 - RegX]** |  |
| 资产命名约定 — 匹配 | 只读. 根据您选择的匹配表单选项或输入的原始代码显示正则表达式语法。 |
| 资产命名约定 — 基本名称 | 只读. 根据所选的“基本名称”表单选项或输入的原始代码显示正则表达式语法。 |
| 序列排序 — 匹配 | 只读. 根据您选择的表单选项或输入的原始代码显示正则表达式语法。 |

## 关于将批次集预设应用于资源文件夹 {#apply-bsp}

将批次集预设分配给一个或多个资源文件夹时，任何子文件夹都会自动从其父文件夹继承预设。

您可以将多个批次集预设应用于资源文件夹。

为其分配了批量预设的文件夹显示在用户界面中，文件夹中显示的预设名称为 **[!UICONTROL 信息卡]** 视图。

要将批集预设应用于资源文件夹，请使用以下两种方法之一：

* [从“批次集预设”页面将批次集预设应用于资源文件夹](#apply-bsp-to-folders-via-bsp-page)  — 此方法为您提供了最大的灵活性。 您可以将单个预设或多个预设应用于单个文件夹或多个文件夹。
* [从资源文件夹的“属性”页面应用批次集预设](#apply-bsp-to-folders-via-properties)  — 此方法允许您将一个或多个批次集预设应用于单个文件夹。

作为最佳实践，请确保资产文件夹已同步 [!DNL Dynamic Media]，然后应用所需的预设。

如果您遇到以下两种情况之一，请重新处理文件夹中的资产：

* 您想要对已上传资产的现有资产文件夹运行批次集预设。
* 您稍后可以编辑之前应用于资产文件夹的现有批次集预设。

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### 从“批次集预设”页面将批次集预设应用于资源文件夹 {#apply-bsp-to-folders-via-bsp-page}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 批次集预设]**.
1. 在 **[!UICONTROL 批次集预设]** 页面，页面左侧 **[!UICONTROL 预设名称]** 列中，选中要应用于文件夹的每个批次集预设的复选框。
1. 在工具栏中，选择 **[!UICONTROL 将批次预设应用于文件夹]**.
1. 在 **[!UICONTROL 选择文件夹]** 页面上，选中要应用批次集预设的每个文件夹的复选框。
1. 在 **[!UICONTROL 选择文件夹]** 页面，选择 **[!UICONTROL 应用]**.

### 从资源文件夹的“属性”页面应用批次集预设 {#apply-bsp-to-folders-via-properties}

1. 选择Experience Manager徽标并转到 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**.
1. 导航到要在其中应用一个或多个批集预设的文件夹。
1. 在页面上，左侧 **[!UICONTROL 名称]** 列中，选中文件夹的复选框。
1. 在工具栏中，选择 **[!UICONTROL 属性]**.
1. 在文件夹的“属性”页面上，选择 **[!UICONTROL Dynamic Media处理]** 选项卡。

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. 下 **[!UICONTROL 批次集预设]**，来自 **[!UICONTROL 预设名称]** 下拉列表框中，选择要应用的批次集预设的名称。 上面的屏幕快照显示了应用于资源文件夹的两个选定的批次集预设。

   如果批次集预设名称不存在于 **[!UICONTROL 预设名称]** 下拉列表框，这意味着您尚未创建任何批次集预设。 参见 [为图像集或旋转集创建批次集预设](#creating-bsp).

   要删除应用的批次集预设，请选择 **[!UICONTROL X]** 预设类型右侧。

1. 在页面的右上角，选择 **[!UICONTROL 保存并关闭]**.

## 编辑批次集预设 {#edit-bsp}

您可以编辑已创建的现有批次集预设。 您可以更改为资产命名惯例或序列顺序创建的任何表达式组。 如果需要，您还可以更新目标文件夹并设置命名约定。

但是，不能更改预设的名称或预设类型（图像集或旋转集）。 如果有必要更改预设的名称，请复制现有预设并指定新名称。 参见 [复制批次集预设](#copy-bsp).

如果您编辑之前应用于文件夹的批次集预设，则新编辑的批次集预设将仅应用于上传到该文件夹的新资产。

如果您希望将新编辑的预设重新应用于文件夹中的现有资产，则必须重新处理该文件夹。 <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->通过这种方式，现有资产现在将符合成为图像集或旋转集的一部分并进行添加的资格。 此外，图像集或旋转集中已包含的现有资产（基于之前使用的批次集预设）不会被删除并且按原样显示。 此方案假设他们不再符合新编辑的预设的条件。

**要编辑批次集预设，请执行以下操作：**

1. 选择Experience Manager徽标并转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 批次集预设]**.
1. 在 **[!UICONTROL 批次集预设]** 页面，页面左侧 **[!UICONTROL 预设名称]** 列中，选中要更改的批次集预设。
1. 在工具栏中，选择 **[!UICONTROL 编辑批次集预设]**.
1. 根据需要编辑预设。
1. 在 **[!UICONTROL 批次集预设]** 页面，选择 **[!UICONTROL 保存]**.

## 复制现有批次集预设 {#copy-bsp}

您可以复制现有的批次集预设，以避免手动重新创建复杂的预设，或者只需重命名预设。 但是，不能更改使用的预设类型（图像集或旋转集）。

如果复制资产文件夹引用的现有预设，则这些文件夹不会受到影响。

**复制现有批次集预设：**

1. 选择Experience Manager徽标并转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 批次集预设]**.
1. 在 **[!UICONTROL 批次集预设]** 页面，页面左侧 **[!UICONTROL 预设名称]** 列中，选中要复制的批次集预设的复选框。
1. 在工具栏中，选择 **[!UICONTROL 复制]**.
1. 在 **[!UICONTROL 复制批次集预设]** 对话框，在 **[!UICONTROL 标题]** 文本框中，键入预设的新名称。

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. 选择 **[!UICONTROL 复制]**.

## 关于从文件夹中删除批次集预设 {#remove-bsp-from-folder}

从文件夹中删除批次集预设时，上传到这些文件夹的任何新资产都不会应用批次集预设。 文件夹中已经添加到图像集或基于批次集预设（已应用于文件夹）的现有资产 — 继续按原样显示。

如果您想要 *delete* 文件夹中的预设，请参阅 [删除批次集预设](#delete-bsp).

可以使用两种方法从文件夹中删除批次集预设。

* [通过“批次集预设”页面从文件夹中删除批次集预设](#remove-bsp-from-folders-via-bsp-page)  — 此方法为您提供了最大的灵活性。 您可以从单个文件夹或多个文件夹中删除单个预设或多个预设。
* [从文件夹的“属性”页面中删除批次集预设](#remove-bsp-from-folders-via-properties)  — 此方法允许您仅从单个文件夹中删除一个或多个批次集预设。

### 通过“批次集预设”页面从文件夹中删除批次集预设 {#remove-bsp-from-folders-via-bsp-page}

1. 选择Experience Manager徽标并转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 批次集预设]**.
1. 在 **[!UICONTROL 批次集预设]** 页面，页面左侧 **[!UICONTROL 预设名称]** 列中，选中要从一个或多个文件夹中删除的一个或多个批次集预设的复选框。
1. 在工具栏中，选择 **[!UICONTROL 从文件夹中删除批次预设]**.

1. 在 **[!UICONTROL 选择文件夹]** 页面上，选择要从中删除批次集预设的一个或多个文件夹。
1. 在 **[!UICONTROL 选择文件夹]** 页面，选择 **[!UICONTROL 移除]**.

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. 在 **[!UICONTROL 删除配置文件]** 对话框中，选择 **[!UICONTROL 移除]**.

### 从文件夹的“属性”页面中删除批次集预设 {#remove-bsp-from-folders-via-properties}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**.
1. 导航到要将一个或多个批集预设删除到的文件夹。
1. 在页面上，左侧 **[!UICONTROL 名称]** 列中，选中文件夹的复选框。
1. 在工具栏中，选择 **[!UICONTROL 属性]**.
1. 在文件夹的“属性”页面上，选择 **[!UICONTROL Dynamic Media处理]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. 下 **[!UICONTROL 批次集预设]**，选择 **[!UICONTROL X]** 预设类型右侧。

1. 在页面的右上角，选择 **[!UICONTROL 保存并关闭]**.

## 删除批次集预设 {#delete-bsp}

您可以删除批次集预设，以将其永久从 [!DNL Dynamic Media]. 也就是说，它们不再显示在 [!UICONTROL 批次集预设] 页面中也不会显示它们 **[!UICONTROL 批次集预设]** 的下拉列表 **[!UICONTROL Dynamic Media处理]** 选项卡 **[!UICONTROL 属性]** 页面。 因此，在文件夹重新处理时或在文件夹中上传新资产时，预设不会应用于现有资产。

如果删除之前应用于一个或多个文件夹的预设，则从这些文件夹中的资产创建的任何图像集或旋转集将继续按原样显示。

如果您想要 *移除* 文件夹中的预设，请参阅 [从文件夹中删除批次集预设](#remove-bsp-from-folder).

**要删除批集预设，请执行以下操作：**

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 批次集预设]**.
1. 在 **[!UICONTROL 批次集预设]** 页面，页面左侧 **[!UICONTROL 预设名称]** 列中，选中要删除的一个或多个批集预设的复选框。
1. 在工具栏中，选择 **[!UICONTROL 删除批次集预设]**.

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. 在 **[!UICONTROL 删除批次集预设]** 对话框中，选择 **[!UICONTROL 删除]**.

   如果要删除的预设已被某个资产文件夹引用，请选择 **[!UICONTROL 强制删除]** 而是。

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [图像集](/help/assets/dynamic-media/image-sets.md)
>* [旋转集](/help/assets/dynamic-media/spin-sets.md)
>* [在Dynamic Media中配置文件夹级别的选择性发布](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)  — 如果您想了解有关将单个文件夹同步到的更多信息，请参阅主题中的“同步模式” [!DNL Dynamic Media].
>* [在Cloud Services中创建Dynamic Media配置](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)  — 如果您想了解有关将所有文件夹同步到的更多信息，请参阅主题中的“Dynamic Media同步模式” [!DNL Dynamic Media].

