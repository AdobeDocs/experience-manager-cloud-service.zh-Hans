---
title: 将MSM用于资产重用资产
description: 跨从父资产派生并链接到父资产的多个页面／文件夹使用资产。 资产与主副本保持同步，单击几下即可从父资产接收更新。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# 将MSM用于资产重用资产{#reuse-assets-using-msm-for-assets}

Adobe Experience Manager(AEM)中的多站点管理器(MSM)功能使用户能够重复使用一次创作的内容，并在多个Web位置间重复使用。 数字资产与MSM的“资产”功能相同。 使用MSM for Assets，您可以：

* 只需创建一次资产，即可复制这些资产，以便在站点的其他区域重复使用。
* 在同步过程中保留多个副本，并更新一次原始主副本，以将更改推送到子副本。
* 通过临时或永久暂停父资产和子资产之间的链接来进行本地更改。

## 了解优势和概念 {#concepts}

### 工作方式和优势 {#how-it-works-and-the-benefits}

AEM在原始资产及其链接的副本之间保留一个链接，称为Live Copy(LC)。 维护的链接允许将集中的更改推送到许多Live Copy。 这样可以在消除管理重复副本的限制的同时，更快地进行更新。 更改的传播是无错误的，并且是集中的。 该功能允许仅限于选定Live Copy的更新空间。 用户可以分离链接（即中断继承），并进行本地编辑，这些编辑在下次更新主副本并转出更改时不会被覆盖。 可以对若干选定的元数据字段或整个资产进行分离。 它允许灵活地本地更新最初从主副本继承的资产。

MSM在源资产与其Live Copy之间保持实时关系，以便：

* 对源资产所做的更改也会应用（转出）到Live Copy，即Live Copy与源同步。
* 您可以通过暂停Live Relationship来更新Live Copy，或删除几个有限字段的继承。 对源的修改不再应用于Live Copy。

### MSM资产术语表 {#glossary}

**来源** ：原始资产或文件夹。 从中派生Live Copy的主副本。

**Live Copy** 与其源同步的源资产／文件夹的副本。 Live Copy可以是其他Live Copy的源。 了解如何创建LC。

**继承** Live Copy资产／文件夹与其源之间的链接／引用，系统使用它来记住将更新发送到的位置。 继承存在于元数据字段的粒度级别。 可以为选择性元数据字段删除继承，同时保留源与其Live Copy之间的Live关系。

**转出** ：将修改推送到源的下游Live Copy的操作。 可以使用转出操作一次性更新一个或多个Live Copy。 请参阅转出。

**确定要同步的属性** 、方式和时间的转出配置规则。 创建Live Copy时会应用这些配置；稍后可以编辑；并且子项可以从其父资产继承转出配置。 对于MSM for Assets，请仅使用标准转出配置。 其他转出配置对于资产不可用于MSM。

**Synchronize** Another action, and on the rollout, that is action actions the surce and its Live Copy by send the updates from source to live copy. 将为特定Live copy启动同步，并且操作会从源中提取更改。 使用此操作，只能更新其中一个Live Copy。 请参阅同步操作。

**暂停** 暂时删除Live copy与其源资产／文件夹之间的Live关系。 你可以恢复关系。 请参阅暂停操作。

**恢复** 恢复Live关系，以便Live copy再次开始从源接收更新。 请参阅恢复操作。

**重置** “重置”操作通过覆盖任何本地更改，使Live copy再次成为源的复制副本。 它还会删除继承取消，并重置所有元数据字段的继承。 要在将来进行本地修改，您必须再次取消特定字段的继承。 请参阅对LC的本地修改。

**分离** -不可撤消地删除Live copy资产／文件夹的Live关系。 分离操作后，Live Copy永远无法从源接收更新，并且不再是Live Copy。 请参阅删除关系。

## 创建资产的Live Copy {#createlc}

要从一个或多个源资产或文件夹创建Live Copy，请执行以下任一操作：

* 方法1:选择源资产，然后从顶 **[!UICONTROL 部的工具栏中单击创建]** > Live Copy。

* 方法2:在AEM用户界面中，单 **[!UICONTROL 击界面右上角的创建]** > Live Copy。

您可以一次创建资产或文件夹的Live Copy。 您可以创建从资产或作为Live copy本身的文件夹派生的Live Copy。  内容片段(CF)不支持用例。 在尝试创建其Live Copy时，CF会按原样复制，而不会与任何关系。 复制的CF是及时的快照，在更新原始CF时不更新。

要使用第一种方法创建Live Copy，请执行以下步骤：

1. 选择源资产或文件夹。 在工具栏中，单击 **[!UICONTROL 创建> Live Copy]**。

   ![从AEM界面创建Live Copy](assets/create_lc1.png)

   从AEM界面创建Live Copy

1. 选择目标文件夹。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 提供标题和名称。 资产没有子项。 创建文件夹的Live Copy时，您可以选择包括或排除子项。
1. 选择转出配置。 单击&#x200B;**[!UICONTROL 创建]**。

要使用第二种方法创建Live Copy，请执行以下步骤：

1. 在AEM界面中，从右上角单击“创 **[!UICONTROL 建”>“Live Copy]**”。

   ![从AEM界面创建Live Copy](assets/create_lc2.png)

   从AEM界面创建Live Copy

1. 选择源资产或文件夹。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 选择目标文件夹。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 提供标题和名称。 资产没有子项。 创建文件夹的Live Copy时，您可以选择包括或排除子项。
1. 选择转出配置。 单击&#x200B;**[!UICONTROL 创建]**。

>[!NOTE]
>
>移动源或Live copy时，将保留关系。 删除Live copy后，将删除关系。

## 查看源和Live copy的各种属性和状态 {#properties}

您可以从AEM用户界面的各个区域查看Live copy的信息和MSM相关状态，如关系、同步、转出等。

以下两种方法适用于资产和文件夹：

* 选择Live copy资产，并在其“属性”页面中查找信息。
* 选择源文件夹，然后从Live Copy控制台中查找每个Live Copy的详细信息。

**提示**:要检查几个单独的Live Copy的状态，请使用第一个方法，即“属性”页。 要检查多个Live Copy的状态，请使用第二种方法，即，请参阅“关系状 **[!UICONTROL 态]** ”页。

### Live Copy的信息和状态 {#statuslcasset}

要检查Live copy资产或文件夹的信息和状态，请执行以下步骤。

1. 选择Live copy资产或文件夹。 Click **[!UICONTROL Properties]** from the toolbar. 或者，使用键盘快捷键 `p`。
1. 单击 **[!UICONTROL Live Copy]**。 您可以检查源的路径、暂停状态、同步状态、上次转出日期以及上次转出的用户。

   ![Live copy信息和状态显示在控制台的“属性”中](assets/lcfolder_info_properties.png)

   Live copy信息和状态

1. 在子资产借用Live copy配置时，可以启用或禁用。

1. 您可以选择Live Copy的选项以从父项继承转出配置或更改配置。

### 文件夹所有Live Copy的信息和状态 {#statuslcfolder}

AEM提供了一个控制台，用于检查源文件夹的所有Live Copy的状态。 此控制台显示所有子资产的状态。

1. 选择源文件夹。 Click **[!UICONTROL Properties]** from the toolbar. 或者，使用键盘快捷键 `p`。
1. 单击 **[!UICONTROL Live copy源]**。 要打开控制台，请单击“ **[!UICONTROL Live copy概述”]**。 此功能板提供所有子资产的顶级状态。

   ![在源的Live Copy控制台中查看Live Copy的状态](assets/livecopy_statuses.png)

   在源的Live Copy控制台中查看Live Copy的状态

1. 要查看Live copy文件夹中每个资产的详细信息，请选择一个资产，然后单击工具栏中 **[!UICONTROL 的关系状]** 态。

   ![文件夹中Live copy子资产的详细信息和状态](assets/livecopy_relationship_status.png)

   文件夹中Live copy子资产的详细信息和状态

**提示**:您可以快速查看其他文件夹的Live Copy状态，而无需浏览太多。 只需更改Live copy概述界面中上半部分弹出列表中的 **[!UICONTROL 文件夹]** 。

### 从源的“引用”边栏中快速执行操作 {#refrailsource}

对于源资产或文件夹，您可以看到以下信息，并直接从引用边栏中执行以下操作：

* 请参阅Live Copy的路径。
* 在AEM用户界面中打开或显示特定Live Copy。
* 将更新同步到特定Live Copy。
* 暂停关系或更改特定Live Copy的转出配置。
* 访问Live copy概述控制台。

选择源资产或文件夹，打开左边栏，然后单击“引 **[!UICONTROL 用”]**。 或者，选择一个资产或文件夹，然后使用键盘快捷键 `Alt + 4`。  ![所选源的“引用”边栏中可用的操作和信息](assets/referencerail_source.png)

所选源的“引用”边栏中可用的操作和信息

对于特定Live Copy，单击编辑 **[!UICONTROL Live Copy]** ，以暂停关系或更改转出配置。

![对于特定Live Copy，在选择源资产时，可从引用边栏访问暂停关系或更改转出配置的选项](assets/referencerail_editlc_options.png)

暂停关系或更改特定Live Copy的转出配置

### 从Live Copy的“引用”边栏中快速执行操作 {#refraillc}

对于Live copy资产或文件夹，您可以看到以下信息，并直接从引用边栏中执行以下操作：

* 查看其源的路径。
* 在AEM用户界面中打开或显示特定Live Copy。
* 推出更新。

选择Live copy资产或文件夹，打开左边栏，然后单击引用 ****。 或者，选择一个资产或文件夹，然后使用键盘快捷键 `Alt + 4`。  ![所选Live Copy的“引用”边栏中的可用操作](assets/referencerail_livecopy.png)

所选Live Copy的“引用”边栏中的可用操作

## 将修改从源传播到Live Copy {#rolloutsync}

修改源后，可以使用同步操作或转出操作将更改传播到Live Copy。 要了解这两种操作之间的差异，请参阅术 [语表](#glossary)。

### 转出操作 {#rollout}

您可以从源资产中启动转出操作，并更新所有或几个选定的Live Copy。

1. 选择Live copy资产或文件夹。 Click **[!UICONTROL Properties]** from the toolbar. 或者，使用键盘快捷键 `p`。
1. 单击 **[!UICONTROL Live copy源]**。 从顶 **[!UICONTROL 部的工具栏]** ，单击转出。

1. 选择要更新的Live Copy。 单击 **[!UICONTROL 转出]**。

   要转出对子资产进行的更新，请选择转出 **[!UICONTROL 源和所有子资产]**。

   ![将源的修改转出为几个或所有Live Copy](assets/livecopy_rollout_page.png)

   将源的修改转出为几个或所有Live Copy

>[!NOTE]
>
>在源资产中所做的修改仅转出到直接相关的Live Copy。 如果Live Copy是从其他Live copy派生的，则修改不会转出到派生的Live Copy。

或者，您也可以在选择特定Live Copy后，从引用边栏启动转出操作。 有关详细信息，请参 [阅Live Copy的“引用”边栏中的快速操作](#refraillc)。 在此转出方法中，只更新选定的Live Copy及其子项（可选）。

![将源的修改转出到选定的Live Copy](assets/livecopy_rollout_dialog.png)

将源的修改转出到选定的Live Copy

### 关于同步操作 {#aboutsync}

同步操作只将修改从源提取到选定的Live Copy。 同步操作会尊重并维护在取消继承后完成的本地修改。 不会覆盖本地修改，也不会重新建立取消的继承。 可以通过三种方式启动同步操作。

<table>
 <tbody>
  <tr>
   <th><strong>在AEM界面中的位置</strong><br /> </th>
   <th><strong>何时及为何使用</strong><br /> </th>
   <th><strong>如何使用</strong><br /> </th>
  </tr>
  <tr>
   <td>引用边栏</td>
   <td>在已选择源时快速同步。<br /> </td>
   <td>请参 <a href="#refrailsource">阅源的“引用”边栏中的快速操作</a></td>
  </tr>
  <tr>
   <td>工具栏<br /> </td>
   <td>在您已打开Live copy属性时启动同步。<br /> </td>
   <td>请参 <a href="#synclc">阅同步Live Copy</a></td>
  </tr>
  <tr>
   <td>Live copy概述控制台</td>
   <td>选择源文件夹或Live copy概述控制台已打开时，快速同步多个资产（不一定全部）。 同步操作会一次为一个资产启动，但这是一次为多个资产执行同步的更快方法。<br /> </td>
   <td>请参 <a href="#bulkactions">阅对Live copy文件夹中的许多资产的操作</a></td>
  </tr>
 </tbody>
</table>

### 同步Live Copy {#synclc}

要开始同步操作，请打开Live **[!UICONTROL Copy的]** “属性”页，单击 **[!UICONTROL Live Copy]** ，然后单击工具栏中所需的操作。

要查看与同步操作相关的状态和信息，请参 [阅Live Copy的信息和状态](#statuslcasset) ，以 [及文件夹所有Live Copy的信息和状态](#statuslcfolder)。

![“同步”操作会提取对源所做的更改](assets/livecopy_sync.png)

“同步”操作会提取对源所做的更改

>[!NOTE]
>
>如果关系被挂起，则同步操作在工具栏中不可用。 虽然同步操作在引用边栏中可用，但即使成功转出，修改也不会传播。

## 暂停和恢复关系 {#suspendresume}

您可以临时暂停关系，以防止Live copy接收对源资产或文件夹所做的修改。 还可以恢复关系，以便Live copy开始从源接收修改。

要暂停或继续，请打 **[!UICONTROL 开Live Copy的]** “属性”页，单击 **[!UICONTROL Live Copy]** ，然后从工具栏中单击所需的操作。

或者，您也可以从Live copy概述控制台快速暂停或恢复Live copy文件夹中多个资 **[!UICONTROL 产的关系]** 。 请参 [阅对Live copy文件夹中的许多资产执行操作](#bulkactions)。

## 对Live Copy进行本地修改 {#localmods}

Live Copy是创建时原始源的副本。 Live Copy的元数据值是从源继承的。 元数据字段单独维护与源资产的各个字段的继承。

但是，您可以灵活地对Live Copy进行本地修改，以更改一些选定的属性。 要进行本地修改，请取消所需属性的继承。 取消一个或多个元数据字段的继承后，资产的实时关系和其他元数据字段的继承将保留。 任何同步或转出不会覆盖本地修改。 为此，请打开Live copy资 **[!UICONTROL 产的“属性]** ”页面，单击元数 **[!UICONTROL 据字段旁的“取消继承]** ”图标。

您可以撤消所有本地修改并将资产还原到其源的状态。 不可撤消且即时地重置操作将覆盖所有本地修改，并在所有元数据字段上重新建立继承。 要还原 **[!UICONTROL ，请从Live copy资产的]** 属性页面中 **[!UICONTROL ，单击工具]** 栏中的重置。

![重置操作会覆盖本地编辑，并部分地将Live Copy与其源相关联。](assets/livecopy_reset.png)

重置操作会覆盖本地编辑，并部分地将Live Copy与其源相关联。

## 删除实时关系 {#detach}

您可以使用分离操作完全删除源与Live copy之间的关系。 Live copy在分离后将成为独立的资产或文件夹。 它在分离后立即在AEM界面中显示为新资产。 要将Live copy从其源中分离出来，请执行以下步骤。

1. 选择Live copy资产或文件夹。 Click **[!UICONTROL Properties]** from the toolbar. 或者，使用键盘快捷键 `p`。

1. 单击 **[!UICONTROL Live Copy]**。 单击 **[!UICONTROL 工具栏中]** 的分离。 单击 **[!UICONTROL 显示的]** “从对话框分离”。

   ![分离操作会完全消除源和Live copy之间的关系](assets/livecopy_detach.png)

   分离操作会完全消除源和Live copy之间的关系

   >[!CAUTION]
   >
   >单击对话框中的“分离”( **[!UICONTROL Detach]** )后，该关系将立即删除。 无法通过单击“属性”页 **[!UICONTROL 面上的]** “取消”来撤消此操作。

或者，您也可以从Live copy概述控制台中快速分离Live copy文件夹中 **[!UICONTROL 的多个资产]** 。 请参 [阅对Live copy文件夹中的许多资产执行操作](#bulkactions)。

## 对Live copy文件夹中的许多资产执行操作 {#bulkactions}

如果Live copy文件夹中有多个资产，则启动每个资产的操作可能会很繁琐。 您可以从Live Copy控制台快速对许多资产启动基本操作。 以上方法继续适用于单个资产。

1. 选择源文件夹。 Click **[!UICONTROL Properties]** from the toolbar. 或者，使用键盘快捷键 `p`。
1. 单击 **[!UICONTROL Live copy源]**。 要打开控制台，请单击“ **[!UICONTROL Live copy概述”]**。

1. 在此功能板中，从Live copy文件夹中选择Live copy资产。 单击工具栏中的所需操作。 可用的操作有同步 **[!UICONTROL 、重置]**、暂 **[!UICONTROL 停和分]**********&#x200B;离等。

   您可以快速对任意数量的Live copy文件夹中的任何资产启动这些操作，这些文件夹与选定的源文件夹处于Live关系中。

   ![从Live copy概述控制台轻松更新Live copy文件夹中的许多资产](assets/livecopyconsole_update_many_assets.png)

   从Live copy概述控制台轻松更新Live copy文件夹中的许多资产

<!--
## Extend MSM for Assets {#extendapi}

AEM allows you to extend the functionality using the MSM Java APIs. For Assets, the extending works just the same as it works with MSM for Site. For details, see [Extending the MSM](/help/sites-developing/extending-msm.md) and the following for information about specific tasks:

* [Overview of APIs](/help/sites-developing/extending-msm.md#overview-of-the-java-api)

* [Create a new synchronization action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)
* [Create a new rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration)

* [Create and use a simple LiveActionFactory class](/help/sites-developing/extending-msm.md#creating-and-using-a-simple-liveactionfactory-class)

>[!NOTE]
>
>* Blueprint in MSM for Site is called Live Copy source in MSM for Assets.
>* Removing the chapters step in the create site wizard is not supported in MSM for Assets.
>* Configuring MSM locks on page properties (Touch-enabled UI) is not supported in MSM for Assets.

-->

## 资产管理任务对Live copy的影响 {#manageassets}

Live Copy和源是可以作为数字资产在一定程度上进行管理的资产或文件夹。 AEM中的某些资产管理任务对Live Copy具有特定影响。

* 复制Live Copy时，将创建一个Live copy资产，其源与第一个Live copy相同。
* 当您移动源或其Live Copy时，Live Relationship将保留。
* 编辑操作不适用于Live copy资产。 如果Live copy的源本身是Live Copy，则编辑操作不适用。
* Live copy资产不提供签出操作。
* 对于源文件夹，可使用创建审阅任务的选项。
* 在列表视图和列视图中查看资产列表时，Live copy资产或文件夹会针对其显示“Live Copy”。 这有助于您轻松识别文件夹中的Live Copy。

## 比较资产和站点的MSM {#comparison}

在更多情况下，“资产”为MSM，与“站点”为MSM的行为相匹配。 需要注意的主要区别是：

* 在MSM for Site中，Blueprint称为Live copy源，在MSM中，它用于资产。
* 在站点中，您可以比较Blueprint及其Live Copy，但是在资产中无法将源与其Live copy进行比较。
* 您无法在资产中编辑Live Copy。
* 网站通常有子项，但资产则没有。 创建单个资产的Live Copy时，不提供包含或排除子项的选项。
* MSM for Assets不支持删除创建站点向导中的章节步骤。
* 对于资产，MSM不支持在页面属性（触屏优化UI）上配置MSM锁。
* 对于MSM for Assets，仅使用 **[!UICONTROL Standard转出配置]**。 其他转出配置对于资产不可用于MSM。

## Best practices {#bestpractices}

MSM的一些最佳实践是：

* 在开始实施之前，计划资产和内容流的父子关系。
* 

## MSM资产的限制和已知问题 {#limitations}

以下是MSM对资产的限制。

* 内容片段(CF)不支持用例。 在尝试创建其Live Copy时，CF会按原样复制，而不会与任何关系。 复制的CF是及时的快照，在更新原始CF时不更新。

