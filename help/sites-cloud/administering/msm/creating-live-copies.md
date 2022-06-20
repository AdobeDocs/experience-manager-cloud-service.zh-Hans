---
title: 创建并同步 Live Copy
description: 了解如何创建和同步 Live Copy 以在站点中重用您的内容。
feature: Multi Site Manager
role: Admin
exl-id: 53ed574d-e20d-4e73-aaa2-27168b9d05fe
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: ht
source-wordcount: '4274'
ht-degree: 100%

---

# 创建并同步 Live Copy {#creating-and-synchronizing-live-copies}

您可以从页面或 Blueprint 配置创建 Live Copy，以便在站点中重用该内容。管理继承和同步，您可以控制对内容所做的更改的传播方式。

## 管理 Blueprint 配置 {#managing-blueprint-configurations}

Blueprint 配置标识要用作一个或多个 Live Copy 页面的源的现有网站。

>[!TIP]
>
>Blueprint 配置可让您将内容更改推送到 Live Copy。请参阅 [Live Copy – 源、Blueprint 和 Blueprint 配置](overview.md#source-blueprints-and-blueprint-configurations)。

创建 Blueprint 配置时，可以选择定义 Blueprint 的内部结构的模板。默认 Blueprint 模板假定源网站具有以下特征：

* 网站具有根页面。
* 根的直接子页面是网站的语言分支。在创建 Live Copy 时，将语言显示为可选内容，以便包含在副本中。
* 每个语言分支的根均有一个或多个子页面。在创建 Live Copy 时，将显示子页面，以便将其包含在 Live Copy 中。

>[!NOTE]
>
>不同的结构需要不同的 Blueprint 模板。

创建 Blueprint 配置后，可以配置以下属性：

* **名称**：Blueprint 配置的名称
* **源路径**：您用作源的站点根页面的路径 (Blueprint)
* **描述**。（可选）Blueprint 配置的描述，显示在创建站点时可从中进行选择的 Blueprint 配置列表中

在使用您的 Blueprint 配置时，您可以将它与确定源/Blueprint 的 Live Copy 同步方式的转出配置相关联。请参阅[指定要使用的转出配置](live-copy-sync-config.md#specifying-the-rollout-configurations-to-use)。

### 创建和编辑 Blueprint 配置 {#creating-editing-blueprint-configurations}

Blueprint 配置被视为不可变数据，因此在运行时不可编辑。因此，必须使用 CI/CD 管道通过 Git 部署任何配置更改。

有关更多信息，请参阅[对 Adobe Experience Manager (AEM) as a Cloud Service 的重要更改](/help/release-notes/aem-cloud-changes.md)一文。

以下步骤仅可供管理员对本地开发实例执行以进行测试和开发。这些选项在任何 AEMaaCS 云实例中均不可用。

#### 本地创建 Blueprint 配置 {#creating-a-blueprint-configuration}

要创建 Blueprint 配置，请执行以下操作：

1. [导航](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)到&#x200B;**工具**&#x200B;菜单，然后选择&#x200B;**站点**&#x200B;菜单。
1. 选择 **Blueprint** 以打开 **Blueprint 配置**&#x200B;控制台：

   ![Blueprint 配置](../assets/blueprint-configurations.png)

1. 选择&#x200B;**创建**。
1. 选择 Blueprint 模板，然后选择&#x200B;**下一步**&#x200B;以继续。
1. 选择要用作 Blueprint 的源页面；然后选择&#x200B;**下一步**&#x200B;以继续。
1. 定义：

   * **标题**：Blueprint 的强制性标题
   * **描述**：用于提供更多详细信息的可选描述。

1. **创建**&#x200B;将根据您的规范创建 Blueprint 配置。

### 本地编辑或删除 Blueprint 配置{#editing-or-deleting-a-blueprint-configuration}

您可以编辑或删除现有 Blueprint 配置：

1. [导航](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)到&#x200B;**工具**&#x200B;菜单，然后选择&#x200B;**站点**&#x200B;菜单。
1. 选择 **Blueprint** 以打开 **Blueprint 配置**&#x200B;控制台：

   ![Blueprint 配置](../assets/blueprint-configurations.png)

1. 选择所需的 Blueprint 配置 – 可在工具栏中使用相应的操作：

   * **属性**；可以使用此项查看并编辑配置的属性。
   * **删除**

## 创建 Live Copy {#creating-a-live-copy}

可通过大量方式创建 Live Copy。

### 创建页面的 Live Copy {#creating-a-live-copy-of-a-page}

可以创建任何页面或分支的 Live Copy。在创建 Live Copy 时，可以指定要用于同步内容的转出配置：

* 选定的转出配置将应用于 Live Copy 页面及其子页面。
* 如果您未指定任何转出配置，MSM 将确定要使用的转出配置。请参阅[指定要使用的转出配置](live-copy-sync-config.md#specifying-the-rollout-configurations-to-use)。

可以创建任何页面的 Live Copy：

* 由 [Blueprint 配置](#creating-a-blueprint-configuration)引用的页面
* 以及与配置无关联的页面
* 另一个 Live Copy 的页面中的 Live Copy（[嵌套式 Live Copy](overview.md#nested-live-copies)）

唯一的区别是，**转出**&#x200B;命令在源/Blueprint 页面上的可用性取决于 Blueprint 配置是否引用了源：

* 如果从 Blueprint 配置中引用的&#x200B;****&#x200B;源页面创建 Live Copy，则转出命令将适用于源/Blueprint 页面。
* 如果从 Blueprint 配置中未引用的&#x200B;****&#x200B;源页面创建 Live Copy，则转出命令将不适用于源/Blueprint 页面。

要创建 Live Copy，请执行以下操作：

1. 在&#x200B;**站点**&#x200B;控制台中，依次选择&#x200B;**创建**&#x200B;和 **Live Copy**。

   ![创建 Live Copy](../assets/create-live-copy.png)

1. 选择源页面，然后单击或点按&#x200B;**下一步**。例如：

   ![选择 Live Copy 源](../assets/live-copy-from.png)

1. 指定 Live Copy 的目标路径（打开 Live Copy 的父文件夹/页面），然后单击或点按&#x200B;**下一步**。

   ![选择 Live Copy 目标](../assets/live-copy-to.png)

   >[!NOTE]
   >
   >目标路径不能在源路径内。

1. 输入：

   * 页面的&#x200B;**标题**。
   * URL 中使用的&#x200B;**名称**。

   ![Live Copy 属性](../assets/live-copy-properties.png)

1. 使用&#x200B;**排除子页面**&#x200B;复选框：

   * 选中：仅创建所选页面的 Live Copy（浅 Live Copy）
   * 未选中：创建包含所选页面的所有下级的 Live Copy（深 Live Copy）

1. （可选）要指定用于 Live Copy 的一个或多个转出配置，请使用&#x200B;**转出配置**&#x200B;下拉列表来选择它们。所选配置将显示在下拉选择器的下方。
1. 单击或点按&#x200B;**创建**。这将显示一条确认消息，可在其中选择&#x200B;**打开**&#x200B;或&#x200B;**完成**。

### 从 Blueprint 配置创建站点的 Live Copy {#creating-a-live-copy-of-a-site-from-a-blueprint-configuration}

使用 Blueprint 配置创建 Live Copy 可基于 Blueprint（源）内容创建站点。从 Blueprint 配置创建 Live Copy 时，选择要复制的 Blueprint 源的一个或多个语言分支，然后从语言分支中选择要复制的章节。请参阅[创建 Blueprint 配置](#creating-a-blueprint-configuration)。

如果您从 Live Copy 中省略了一些语言分支，则可稍后添加它们。有关详细信息，请参阅[在 Live Copy（Blueprint 配置）中创建 Live Copy](#creating-a-live-copy-inside-a-live-copy-blueprint-configuration)。

>[!CAUTION]
>
>当 Blueprint 源包含以其他分支中的段落为目标的链接和引用时，目标不会在 Live Copy 页面中更新，而是仍指向原始目标。

创建站点时，请提供以下属性的值：

* **初始语言**：要包含在 Live Copy 中的 Blueprint 源的语言分支
* **初始章节**：要包含在 Live Copy 中的 Blueprint 语言分支的子页面
* **目标路径**：Live Copy 站点的根页面的位置
* **标题**：Live Copy 站点的根页面的标题
* **名称**：（可选）存储 Live Copy 的根页面的 JCR 节点的名称（默认值基于标题）
* **站点所有者**：（可选）有关 Live Copy 负责方的信息
* **Live Copy**：选择此选项可与源站点建立实时关系。如果不选择此选项，则尽管会创建 Blueprint 的副本，但该副本随后不会与源同步。
* **转出配置**：（可选）选择一个或多个转出配置以用于同步 Live Copy。默认情况下，转出配置继承自 Blueprint。有关更多详细信息，请参阅[指定要使用的转出配置](live-copy-sync-config.md#specifying-the-rollout-configurations-to-use)。

要从 Blueprint 配置创建站点的 Live Copy，请执行以下操作：

1. 在&#x200B;**站点**&#x200B;控制台中，选择&#x200B;**创建**，然后从下拉选择器中选择&#x200B;**站点**。
1. 选择要用作 Live Copy 源的 Blueprint 配置，然后单击&#x200B;**下一步**&#x200B;以继续：

   ![从 Blueprint 创建站点](../assets/create-site-from-blueprint.png)

1. 使用&#x200B;**初始语言**&#x200B;选择器指定要用于 Live Copy 的 Blueprint 站点的语言。

   默认选择所有可用语言。要删除某种语言，请单击或点按该语言旁边显示的 **X**。

   例如：

   ![创建站点时指定属性](../assets/create-site-properties.png)

1. 使用&#x200B;**初始章节**&#x200B;下拉列表选择要包含在 Live Copy 中的 Blueprint 的部分。虽然默认情况下会包含所有可用章节，但可以删除这些章节。
1. 提供剩余属性的值，然后选择&#x200B;**创建**。在确认对话框中，选择&#x200B;**完成**&#x200B;以返回&#x200B;**站点**&#x200B;控制台，或选择&#x200B;**打开站点**&#x200B;以打开站点的根页面。

### 在 Live Copy（Blueprint 配置）中创建 Live Copy {#creating-a-live-copy-inside-a-live-copy-blueprint-configuration}

在现有 Live Copy（使用 Blueprint 配置创建的）中创建 Live Copy 时，您可以插入最初创建 Live Copy 时未包含的任何语言副本或章节。

## 监控您的 Live Copy {#monitoring-your-live-copy}

### 查看 Live Copy 的状态 {#seeing-the-status-of-a-live-copy}

Live Copy 页面的属性显示有关 Live Copy 的以下信息：

* **源**：Live Copy 页面的源页面
* **状态**：Live Copy 的同步状态，包括 Live Copy 是否与源保持同步、上次同步时间以及同步操作的执行者
* **配置**：

   * 页面是否仍受 Live Copy 继承的约束
   * 配置是否继承自父页面
   * Live Copy 使用的任何转出配置

要查看属性，请执行以下操作：

1. 在&#x200B;**站点**&#x200B;控制台中，选择 Live Copy 页面并打开属性。
1. 选择 **Live Copy** 选项卡。

   例如：

   ![页面属性中的 Live Copy 选项卡](../assets/live-copy-inherit.png)

   有关更多详细信息，请参阅“Live Copy 概述控制台”一文中的[使用 Live Copy 概述](live-copy-overview.md#using-the-live-copy-overview)部分。

### 查看 Blueprint 页面的 Live Copy {#seeing-the-live-copies-of-a-blueprint-page}

Blueprint 页面（在 Blueprint 配置中引用）为您提供使用当前 (Blueprint) 页面作为源的 Live Copy 页面的列表。使用此列表可跟踪 Live Copy。此列表显示在[页面属性](/help/sites-cloud/authoring/fundamentals/page-properties.md)的 **Blueprint** 选项卡上。

![页面属性的 Blueprint 选项卡](../assets/live-copy-blueprint-tab.png)

## 同步您的 Live Copy {#synchronizing-your-live-copy}

可通过大量方式同步您的 Live Copy。

### 转出 Blueprint {#rolling-out-a-blueprint}

转出 Blueprint 页面可将内容更改推送到 Live Copy。**转出**&#x200B;操作执行使用[转出](live-copy-sync-config.md#rollout-triggers)触发器的转出配置。

>[!NOTE]
>
>如果在 Blueprint 分支和从属 Live Copy 分支中都创建了具有相同页面名称的新页面，则可能会发生冲突。
>
>[转出时需要处理和解决此类冲突](rollout-conflicts.md)。

#### 从页面属性转出 Blueprint {#rolling-out-a-blueprint-from-page-properties}

1. 在&#x200B;**站点**&#x200B;控制台中，选择 Blueprint 中的页面并打开属性。
1. 打开 **Blueprint** 选项卡。
1. 选择&#x200B;**转出**。

   ![“转出”按钮](../assets/rollout.png)

1. 指定页面和任何子页面，然后通过复选标记进行确认：

   ![选择要转出的页面](../assets/select-rollout-pages.png)

1. 指定转出作业是应立即执行（**现在**）还是在其他日期/时间执行（**稍后**）。

   ![定义转出时间](../assets/rollout-now-later.png)

转出作为异步作业处理，并且可在[***异步作业状态**&#x200B;页面上进行查看。](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)

#### 从引用边栏转出 Blueprint {#roll-out-a-blueprint-from-the-reference-rail}

1. 在&#x200B;**站点**&#x200B;控制台中，从 Live Copy 中选择此页面，然后从工具栏中打开&#x200B;**[引用](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)**&#x200B;面板。
1. 从列表中选择 **Blueprint** 选项以查看与此页面关联的 Blueprint。
1. 从列表中选择所需的 Blueprint。
1. 单击或点按&#x200B;**转出**。

   ![从引用边栏转出 Blueprint](../assets/rollout-blueprint-from-references.png)

1. 系统会要求您确认转出的详细信息：

   * **转出范围**：

      指定范围是仅针对所选页面，还是应包括子页面。

   * **计划**：

      指定转出作业是应立即执行（**现在**）还是在某个将来日期/时间执行（**稍后**）。

      ![定义转出范围和计划](../assets/rollout-scope-schedule.png)

1. 确认这些详细信息后，选择&#x200B;**转出**&#x200B;以执行此操作。

转出作为异步作业处理，并且可在&#x200B;[**异步作业状态**&#x200B;页面上进行查看。](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)

#### 从 Live Copy 概述转出 Blueprint {#roll-out-a-blueprint-from-the-live-copy-overview}

在选择 Blueprint 页面时，](live-copy-overview.md#using-the-live-copy-overview)也可以从 Live Copy 概述执行&#x200B;[**转出**&#x200B;操作。

1. 打开 [Live Copy 概述](live-copy-overview.md#using-the-live-copy-overview)并选择 Blueprint 页面。
1. 从工具栏中选择&#x200B;**转出**。

   ![Live Copy 概述](../assets/live-copy-overview-actions-blueprint.png)

1. 指定页面和任何子页面，然后通过复选标记进行确认：

   ![选择要转出的页面](../assets/select-rollout-pages.png)

1. 指定转出作业是应立即执行（**现在**）还是在其他日期/时间执行（**稍后**）。

   ![定义转出计划](../assets/rollout-now-later.png)

转出作为异步作业处理，并且可在&#x200B;[**异步作业状态**&#x200B;页面上进行查看。](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)

### 同步 Live Copy {#synchronizing-a-live-copy}

同步 Live Copy 页面以将内容更改从源拉入 Live Copy。

#### 从页面属性同步 Live Copy {#synchronize-a-live-copy-from-page-properties}

同步 Live Copy 以将更改从源拉入 Live Copy。

>[!NOTE]
>
>同步执行使用[转出](live-copy-sync-config.md#rollout-triggers)触发器的转出配置。

1. 在&#x200B;**站点**&#x200B;控制台中，选择 Live Copy 页面并打开属性。
1. 打开 **Live Copy** 选项卡。
1. 单击或点按&#x200B;**同步**。

   ![“同步”按钮](../assets/synchronize.png)

   将请求确认，并使用&#x200B;**同步**&#x200B;以继续。

#### 从 Live Copy 概述同步 Live Copy {#synchronize-a-live-copy-from-the-live-copy-overview}

在选择 Live Copy 页面时，[也可以从 Live Copy 概述执行同步操作](live-copy-overview.md#using-the-live-copy-overview)。

1. 打开 [Live Copy 概述](live-copy-overview.md#using-the-live-copy-overview)并选择 Live Copy 页面。
1. 从工具栏中选择&#x200B;**同步**。
1. 在指定是否要包含以下项后，在对话框中确认&#x200B;**转出**&#x200B;操作：

   * **页面和子页面**
   * **仅页面**

   ![带或不带子页面的转出页面](../assets/rollout-page-and-subpages.png)

## 更改 Live Copy 内容 {#changing-live-copy-content}

要更改 Live Copy 内容，您可以：

* 将段落添加到页面。
* 通过中断任何页面或组件的 Live Copy 继承来更新现有内容。

>[!TIP]
>
>如果您在 Live Copy 中手动创建一个新页面，则该新页面是 Live Copy 的本地页面，这意味着它没有附加到相应的源页面。
>
>要创建作为关系的一部分的本地页面，最佳实践是在源中创建本地页面并执行深度转出。这将在本地创建页面作为 Live Copy。

>[!NOTE]
>
>如果在 Blueprint 分支和从属 Live Copy 分支中都创建了具有相同页面名称的新页面，则可能会发生冲突。
>
>[转出时需要处理和解决此类冲突](rollout-conflicts.md)。

### 向 Live Copy 页面添加组件 {#adding-components-to-a-live-copy-page}

您可以随时向 Live Copy 页面添加组件。Live Copy 及其段落系统的继承状态不会控制您添加组件的能力。

当 Live Copy 页面与源页面同步时，添加的组件保持不变。另请参阅[更改 Live Copy 页面上的组件顺序](#changing-the-order-of-components-on-a-live-copy-page)。

>[!TIP]
>
>在本地对标记为容器的组件所做的更改不会由转出时的 Blueprint 内容覆盖。请参阅 [MSM 最佳实践](best-practices.md#components-and-container-synchronization)以了解更多信息。

### 暂停页面的继承 {#suspending-inheritance-for-a-page}

创建 Live Copy 时，Live Copy 配置将保存在所复制页面的根页面上。根页面的所有子页面将继承 Live Copy 配置。Live Copy 页面上的组件也将继承 Live Copy 配置。

您可以暂停 Live Copy 页面的 Live Copy 继承，以便更改页面属性和组件。当您暂停继承时，页面属性和组件不再与源同步。

>[!TIP]
>
>您也可以从 Live Copy 的 Blueprint [分离 Live Copy](#detaching-a-live-copy) 以删除所有连接。与暂停继承不同，分离操作是永久性且不可逆的。

#### 暂停来自页面属性的继承 {#suspending-inheritance-from-page-properties}

要暂停页面上的继承，请执行以下操作：

1. 使用&#x200B;**站点**&#x200B;控制台的&#x200B;**查看属性**&#x200B;命令或页面工具栏上的&#x200B;**页面信息**&#x200B;来打开 Live Copy 页面的属性。
1. 单击或点按 **Live Copy** 选项卡。
1. 从工具栏中选择&#x200B;**暂停**。之后，您可以选择：

   * **暂停**：仅暂停当前页面。
   * **与子项一起暂停**：暂停当前页面和任何子页面。

1. 在确认对话框上选择&#x200B;**暂停**。

#### 暂停来自 Live Copy 概述的继承 {#suspending-inheritance-from-the-live-copy-overview}

在选择 Live Copy 页面时，[也可以从 Live Copy 概述执行暂停操作](live-copy-overview.md#using-the-live-copy-overview)。

1. 打开 [Live Copy 概述](live-copy-overview.md#using-the-live-copy-overview)并选择 Live Copy 页面。
1. 从工具栏中选择&#x200B;**暂停**。
1. 从以下项中选择适当的选项：

   * **暂停**
   * **与子项一起暂停**

   ![与子项一起暂停](../assets/suspend-with-children.png)

1. 在&#x200B;**暂停 Live Copy** 对话框中确认&#x200B;**暂停**&#x200B;操作：

   ![确认暂停](../assets/confirm-suspend.png)

### 恢复页面的继承 {#resuming-inheritance-for-a-page}

暂停页面的 Live Copy 继承是一项临时操作。在暂停后，**恢复**&#x200B;操作将可用，可让您恢复实时关系。

![恢复继承](../assets/resume-inheritance.png)

当您重新启用继承时，页面不会自动与源同步。如果需要，您可以通过以下方式请求同步：

* 在&#x200B;**恢复**/**还原**&#x200B;对话框中；例如：

   ![恢复和同步](../assets/resume-and-synch.png)

* 在稍后阶段，通过手动选择同步操作。

>[!NOTE]
>
>当您重新启用继承时，页面不会自动与源同步。如果需要，您可以在恢复时或稍后手动请求同步。

#### 恢复来自页面属性的继承 {#resuming-inheritance-from-page-properties}

在[暂停](#suspending-inheritance-from-page-properties)后，**恢复**&#x200B;操作将在页面属性的工具栏中变得可用：

![“恢复”按钮](../assets/resume.png)

选中后，该对话框将出现。如果需要，您可以选择同步，然后确认操作。

#### 从 Live Copy 概述恢复 Live Copy 页面 {#resume-a-live-copy-page-from-the-live-copy-overview}

在选择 Live Copy 页面时，[也可以从 Live Copy 概述执行恢复操作](live-copy-overview.md#using-the-live-copy-overview)。

1. 打开 [Live Copy 概述](live-copy-overview.md#using-the-live-copy-overview)并选择已暂停的 Live Copy 页面。该页面将显示为&#x200B;**继承已取消**。
1. 从工具栏中选择&#x200B;**恢复**。
1. 指示是否要在恢复继承后同步页面，然后在&#x200B;**恢复 Live Copy** 对话框中确认&#x200B;**恢复**&#x200B;操作。

### 更改继承深度（浅/深） {#changing-inheritance-depth-shallow-deep}

在现有 Live Copy 上，您可以更改页面的深度，即是否包含子页面。

* 切换到浅 Live Copy：

   * 将立即生效且不可逆。

   * 从 Live Copy 显式分离子页面。如果撤消，则无法保留对子项所做的进一步修改。

   * 将删除任何下级 `LiveRelationships`，即使存在嵌套式 `LiveCopies` 也是如此。

* 切换到深 Live Copy：

   * 将子页面保持不变。
   * 要查看切换的效果，您可以进行转出，将根据转出配置应用任何内容修改。

* 切换到浅 Live Copy，然后返回深 Live Copy：

   * 将（以前的）浅 Live Copy 的所有子项视为手动创建，因此使用 `[oldname]_msm_moved name` 将其移开。

要指定或更改深度，请执行以下操作：

1. 使用&#x200B;**站点**&#x200B;控制台的&#x200B;**查看属性**&#x200B;命令或页面工具栏上的&#x200B;**页面信息**&#x200B;来打开 Live Copy 页面的属性。
1. 单击或点按 **Live Copy** 选项卡。
1. 在&#x200B;**配置**&#x200B;部分中，根据是否包含子页面来设置或清除 **Live Copy 继承**&#x200B;选项：

   * 选中 – 深 Live Copy（包含子页面）
   * 取消选中 – 浅深 Live Copy（排除子页面）

   >[!CAUTION]
   >
   >切换到浅 Live Copy 将立即生效并且不可逆。
   >
   >有关更多信息，请参阅 [Live Copy – 构图](overview.md#live-copies-composition)。

1. 单击或点按&#x200B;**保存**&#x200B;以持久存储您的更新。

### 取消组件的继承 {#cancelling-inheritance-for-a-component}

取消组件的 Live Copy 继承，以便该组件不再与源组件同步。如果需要，您可以稍后启用继承。

>[!NOTE]
>
>当您重新启用继承时，组件不会自动与源同步。如果需要，您可以手动请求同步。

取消继承可更改组件内容或删除组件：

1. 单击或点按要为其取消继承的组件。

   ![组件工具栏中的继承](../assets/inheritance-toolbar.png)

1. 在组件工具栏上，单击或点按&#x200B;**取消继承**&#x200B;图标。

   ![“取消继承”图标](../assets/cancel-inheritance-icon.png)

1. 在“取消继承”对话框中，单击&#x200B;**是**&#x200B;确认操作。

   这将更新组件工具栏以包含所有（适当的）编辑命令。

### 重新启用组件的继承 {#re-enabling-inheritance-for-a-component}

要启用组件的继承，请单击或点按组件工具栏上的&#x200B;**重新启用继承**&#x200B;图标。

![“重新启用继承”图标](../assets/re-enable-inheritance-icon.png)

### 更改 Live Copy 页面上的组件顺序 {#changing-the-order-of-components-on-a-live-copy-page}

如果 Live Copy 包含属于一个段落系统的组件，则该段落系统的继承将遵循以下规则：

* 即使建立了继承，也可修改继承的段落系统中的组件顺序。
* 在推出时，将从 Blueprint 中恢复组件顺序。如果在推出之前已将新组件添加到 Live Copy，则这些新组件将与其下方的组件一起重新排序。
* 如果取消段落系统的继承，组件的顺序将不会在推出时恢复，并且将在 Live Copy 中保持不变。

>[!NOTE]
>
>在段落系统上恢复取消的继承时，组件的顺序&#x200B;**将不会自动从 Blueprint 恢复**。如果需要，您可以手动请求同步。

使用以下过程可取消段落系统的继承。

1. 打开 Live Copy 页面。
1. 将现有组件拖动到页面上的新位置。
1. 在&#x200B;**取消继承**&#x200B;对话框中，单击&#x200B;**是**&#x200B;确认操作。

### 覆盖 Live Copy 页面的属性 {#overriding-properties-of-a-live-copy-page}

默认情况下，Live Copy 页面的页面属性继承自源页面且不可编辑。

当您需要更改 Live Copy 的属性值时，可以取消属性的继承。链接图标表示为属性启用继承。

![继承的页面属性](../assets/properties-inherited.png)

在取消继承时，可以更改属性值。断开链接图标表示取消继承。

![属性未继承](../assets/properties-not-inherited.png)

如果需要，您可以稍后重新启用属性的继承。

>[!NOTE]
>
>当您重新启用继承时，Live Copy 页面属性不会自动与源属性同步。如果需要，您可以手动请求同步。

1. 使用&#x200B;**站点**&#x200B;控制台的&#x200B;**查看属性**&#x200B;选项或页面工具栏上的&#x200B;**页面信息**&#x200B;图标来打开 Live Copy 页面的属性。
1. 要取消属性的继承，请单击或点按属性右侧显示的链接图标。

   ![“取消继承”按钮](../assets/cancel-inheritance-button.png)

1. 在&#x200B;**取消继承**&#x200B;确认对话框中，单击或点按&#x200B;**是**。

### 还原 Live Copy 页面的属性 {#revert-properties-of-a-live-copy-page}

要为属性启用继承，请单击或点按属性旁边显示的&#x200B;**还原继承**&#x200B;图标。

![“还原继承”按钮](../assets/revert-inheritance-button.png)

### 重置 Live Copy 页面 {#resetting-a-live-copy-page}

您可以重置 Live Copy 页面以：

* 删除所有继承取消并
* 将页面返回到与源页面相同的状态。

重置会影响您对页面属性、段落系统和组件所做的更改。

#### 从页面属性重置 Live Copy 页面 {#reset-a-live-copy-page-from-the-page-properties}

1. 在&#x200B;**站点**&#x200B;控制台中，选择 Live Copy 页面，然后选择&#x200B;**查看属性**。
1. 打开 **Live Copy** 选项卡。
1. 从工具栏中选择&#x200B;**重置**。

   ![“重置”按钮](../assets/reset.png)

1. 在&#x200B;**重置 Live Copy** 对话框中，单击&#x200B;**重置**&#x200B;进行确认。

#### 从 Live Copy 概述重置 Live Copy 页面 {#reset-a-live-copy-page-from-the-live-copy-overview}

在选择 Live Copy 页面时，[**也可以从 Live Copy 概述执行重置**&#x200B;操作](live-copy-overview.md#using-the-live-copy-overview)。

1. 打开 [Live Copy 概述](live-copy-overview.md#using-the-live-copy-overview)并选择 Live Copy 页面。
1. 从工具栏中选择&#x200B;**重置**。
1. 在&#x200B;**重置 Live Copy** 对话框中确认&#x200B;**重置**&#x200B;操作。

   ![确认 Live Copy 重置](../assets/reset-live-copy.png)

## 比较 Live Copy 页面与 Blueprint 页面 {#comparing-a-live-copy-page-with-a-blueprint-page}

要跟踪您所做的更改，您可以在&#x200B;**引用**&#x200B;中查看 Blueprint 页面，并将该页面与其源页面进行比较：

1. 在&#x200B;**站点**&#x200B;控制台中，[导航到 Blueprint 或 Live Copy 页面并将其选定。](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
1. 打开&#x200B;**[引用](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)**&#x200B;面板，并根据上下文选择：

   * **Blueprint**
   * **Live Copy**

1. 选择特定的 Live Copy，并根据上下文选择：

   * **与 Blueprint 比较**
   * **与 Live Copy 比较**

   例如：

   ![比较 Live Copy](../assets/compare-live-copy.png)

1. Live Copy 和 Blueprint 页面将并排打开。

   有关使用比较功能的完整信息，请参阅[页面差异](/help/sites-cloud/authoring/features/page-diff.md)。

## 分离 Live Copy {#detaching-a-live-copy}

分离操作将永久删除 Live Copy 与其源/Blueprint 页面之间的实时关系。将从 Live Copy 中删除所有与 MSM 相关的属性，并且 Live Copy 页面会成为独立副本。

>[!CAUTION]
>
>分离 Live Copy 后，无法恢复实时关系。
>
>要删除实时关系并选择稍后恢复它，您可以为页面[取消 Live Copy 继承](#suspending-inheritance-for-a-page)。

这会对树中使用&#x200B;**分离**&#x200B;的位置产生影响：

* **在 Live Copy 的根页面上分离**

   在 Live Copy 的根页面上执行此操作时，它会删除 Blueprint 的所有页面与其 Live Copy 之间的实时关系。

   对 Blueprint 中页面所做的进一步更改&#x200B;**将不会**&#x200B;影响 Live Copy。

* **在 Live Copy 的子页面上分离**

   在 Live Copy 中的子页面（或分支）上执行此操作时：

   * 将删除该子页面（或分支）的实时关系，并且
   * Live Copy 分支中的（子）页面被视为是手动创建的。

   但是，子页面仍受父分支的实时关系的约束，因此 Blueprint 页面的进一步转出将：

   1. 重命名分离的页面：

      * 这是因为 MSM 将它们视为手动创建的页面，这些页面因具有与它尝试创建的 Live Copy 页面相同的名称而导致发生冲突。
   1. 创建一个具有原始名称的新 Live Copy 页面，其中包含来自转出的更改。

   >[!NOTE]
   >
   >有关此类情况的详细信息，请参阅 [MSM 转出冲突](rollout-conflicts.md)。

### 从页面属性分离 Live Copy 页面 {#detach-a-live-copy-page-from-the-page-properties}

要分离 Live Copy，请执行以下操作：

1. 在&#x200B;**站点**&#x200B;控制台中，选择 Live Copy 页面，然后单击或点按&#x200B;**查看属性**。
1. 打开 **Live Copy** 选项卡。
1. 在工具栏上，选择&#x200B;**分离**。

   ![“分离”按钮](../assets/detach-button.png)

1. 这将显示一个确认对话框，请选择&#x200B;**分离**&#x200B;以完成此操作。

### 从 Live Copy 概述分离 Live Copy 页面 {#detach-a-live-copy-page-from-the-live-copy-overview}

在选择 Live Copy 页面时，[也可以从 Live Copy 概述执行分离操作](live-copy-overview.md#using-the-live-copy-overview)。

1. 打开 [Live Copy 概述](live-copy-overview.md#using-the-live-copy-overview)并选择 Live Copy 页面。
1. 从工具栏中选择&#x200B;**分离**。
1. 在&#x200B;**分离 Live Copy** 对话框中确认&#x200B;**分离**&#x200B;操作：

   ![分离 Live Copy](../assets/detach-live-copy.png)
