---
title: 管理页面
description: 了解如何在AEM中管理网站的页面，包括移动、复制和删除。
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 67%

---


# 管理页面 {#managing-pages}

了解如何在AEM中管理网站的页面，包括移动、复制和删除。

>[!TIP]
>
>在开始管理页面之前，请熟悉 [如何在AEM中组织页面。](/help/sites-cloud/authoring/sites-console/organizing-pages.md)

>[!TIP]
>
>有几个 [键盘快捷键](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) 可以从网站控制台使用，以便更高效地组织页面。

## 访问权限 {#access-privileges}

要在页面上执行创建、复制、移动、编辑和删除等操作，您的帐户需要拥有适当的访问权利和权限。

如果您遇到任何问题，我们建议您与系统管理员联系。

## 打开页面进行编辑 {#opening-a-page-for-editing}

之后 [创建页面](/help/sites-cloud/authoring/sites-console/creating-pages.md) 或使用导航到现有页面 [该 **站点** 控制台，](/help/sites-cloud/authoring/sites-console/introduction.md) 您可以打开它进行编辑。

1. 打开 [该 **站点** 控制台。](/help/sites-cloud/authoring/sites-console/introduction.md)
1. 导航以查找要编辑的页面。
1. 通过以下方式选择您的页面：

   * [快速操作](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-cloud/authoring/basic-handling.md#selecting-resources)和工具栏

1. 点按或单击 **编辑** 图标。

   ![编辑按钮](/help/sites-cloud/authoring/assets/edit.png)

1. 此时会打开页面，您可以根据需要[编辑页面](/help/sites-cloud/authoring/page-editor/edit-content.md)。

## 复制和粘贴页面 {#copying-and-pasting-a-page}

您可以将页面及其所有子页面复制到一个新位置：

1. 打开 [该 **站点** 控制台。](/help/sites-cloud/authoring/sites-console/introduction.md)
1. 导航以查找要复制的页面。
1. 通过以下方式选择您的页面：

   * [快速操作](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-cloud/authoring/basic-handling.md#selecting-resources)和工具栏

1. 点按或单击 **复制** 页面图标。

   ![复制](/help/sites-cloud/authoring/assets/copy.png)

1. 导航到页面的新副本所在的位置。
1. 选择 **粘贴** 图标。

   ![粘贴](/help/sites-cloud/authoring/assets/paste.png)

1. “粘贴”对话框显示了粘贴事务和以下功能的摘要：
   * **新站点名称：**&#x200B;更改已粘贴页面的名称
   * **粘贴(不带子项)：**&#x200B;粘贴时省略选中页面的子页面（默认情况下，粘贴子页面）

   ![“粘贴”对话框](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. 选择 **粘贴** 按钮以确认粘贴事务并创建新页面。

>[!NOTE]
>
>如果您将页面复制到某个位置，而该位置已经存在名称与原始名称相同的页面，则系统将通过附加一个编号来自动生成该名称的变体。例如，如果 `beach` 已存在，则名称为 `beach` 的新页面会变为 `beach1`。

>[!NOTE]
>
>如果您在选择模式中启动粘贴操作，则复制完页面后将自动退出。

## 移动或重命名页面 {#moving-or-renaming-a-page}

移动或重命名页面的过程基本相同，这两项操作都由“移动页面”向导处理。通过此向导，您可以：

* 重命名页面而不移动页面。
* 移动页面而不重命名页面。
* 同时移动和重命名页面。

AEM 还有一项功能是允许您对引用被重命名页面或被移动页面的所有内部链接进行更新。此操作非常灵活，可以一个页面一个页面地执行。

1. 打开 [该 **站点** 控制台。](/help/sites-cloud/authoring/sites-console/introduction.md)
1. 导航以查找要移动的页面。
1. 通过以下方式选择您的页面：

   * [快速操作](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-cloud/authoring/basic-handling.md#selecting-resources)和工具栏

1. 点按或单击 **移动** 页面图标，打开移动页面向导。

   ![“移动”按钮](/help/sites-cloud/authoring/assets/move.png)

1. 从 **重命名** 向导的步骤，您可以：

   * 指定移动页面后您希望页面使用的名称，然后选择 **下一个** 以继续。
   * 单击/点按&#x200B;**取消**&#x200B;可中止该过程。

   ![移动和重命名页面](/help/sites-cloud/authoring/assets/move-page-rename.png)

   * 如果仅移动页面，则页面名称可以保持不变。

   >[!NOTE]
   >
   >如果您将页面移动到某个位置，而该位置已经存在具有相同名称的页面，则系统将通过附加一个编号来自动生成该名称的变体。例如，如果 `beach` 已存在，则名称为 `beach` 的新页面会变为 `beach1`。

1. 从 **选择目标** 向导的步骤，您可以：

   * 使用[列视图](/help/sites-cloud/authoring/basic-handling.md#column-view)导航到页面的新位置：

      * 通过单击目标的缩略图选择目标。
      * 单击&#x200B;**下一步**&#x200B;以继续。

   * 使用&#x200B;**返回**&#x200B;以返回到页面名称指定步骤。

   >[!NOTE]
   >
   >默认情况下，会选择您正在移动或重命名的页面的父页面作为目标。

   ![选择页面移动目标](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >如果您将页面移动到某个位置，而该位置已经存在具有相同名称的页面，则系统将通过附加一个编号来自动生成该名称的变体。例如，如果 `winter` 已存在，则 `winter` 会变为 `winter1`。

1. 如果页面已链接、已引用或者已发布，则详细信息会列在&#x200B;**调整/重新发布**&#x200B;步骤中。

   * 您可以指明哪些页面应当相应地调整和/或重新发布。

   >[!NOTE]
   >
   >如果页面既未链接也未引用，则此步骤将不可用。

   ![移动时重新发布页面](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. 点击或单击 **移动** 以定义何时应执行移动操作。

   * **现在** 将触发 [异步作业](#asynchronous-actions) 以立即移动页面。
   * **稍后** 允许您安排处理移动的日期。

   ![定义移动时间](assets/managing-pages-move-page-now-later.png)

1. 点击或单击 **继续** 以完成页面移动。

>[!NOTE]
>
>如果页面已发布，则移动页面会自动取消发布。默认情况下，页面将在移动完成后重新发布，但通过取消选中&#x200B;**调整/重新发布**&#x200B;步骤中的&#x200B;**重新发布**&#x200B;字段，可以更改这一行为。

>[!NOTE]
>
>重命名页面也需遵循指定新页面名称时用到的[页面命名惯例](#page-naming-conventions)。

>[!NOTE]
>
>页面只能移动到允许使用该页面所基于的模板的位置。请参阅[模板可用性](/help/implementing/developing/components/templates.md#template-availability)以了解更多信息。

### 异步操作 {#asynchronous-actions}

页面移动操作始终以异步方式处理，从而使用户能够不受阻碍地在UI中继续创作。

可以在中检查异步作业的状态 [**异步作业状态** 仪表板](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) 在 **全局导航** > **工具** > **操作** > **作业**

>[!TIP]
>
>有关异步作业处理，以及如何配置页面移动/重命名操作限制的更多信息，请参阅“操作”用户指南中的[异步作业](/help/operations/asynchronous-jobs.md)文档。

### 删除页面 {#deleting-a-page}

1. 打开 [该 **站点** 控制台。](/help/sites-cloud/authoring/sites-console/introduction.md)
1. 导航到要删除的页面。
1. 使用[选择模式](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)选择所需页面，然后使用工具栏中的&#x200B;**删除**。

   ![“删除”按钮](/help/sites-cloud/authoring/assets/delete.png)

1. 将出现一个对话框要求进行确认。

   ![删除对话框](/help/sites-cloud/authoring/assets/delete-page.png)

   * **是否要在删除前存档页面？** - 如果选中此项，则在删除时会创建选定要删除页面的版本。
      * [日后可以恢复这些版本](/help/sites-cloud/authoring/sites-console/page-versions.md)。
      * 无法还原没有先前版本的已删除页面。
1. 点击或单击 **取消** 中止操作或 **删除** 以确认操作。
   * 如果页面没有引用，则页面会被删除。
   * 如果页面包含引用，则会出现一个消息框，通知您 **一个或多个页面被引用。** 您可以选择 **强制删除** 或 **取消**.

>[!NOTE]
>
>如果页面已经发布，则在删除前会自动将其取消发布。

### 锁定页面 {#locking-a-page}

您可以在控制台中或者在编辑单个页面时[锁定/解锁页面](/help/sites-cloud/authoring/page-editor/edit-content.md#locking-a-page)。关于页面是否已被锁定的信息也会显示在这两个位置。

![“锁定”按钮](/help/sites-cloud/authoring/assets/lock.png)
![“解锁”按钮](/help/sites-cloud/authoring/assets/unlock.png)

### 创建新文件夹 {#creating-a-new-folder}

您可以创建文件夹来帮助组织文件和页面。

1. 打开 [该 **站点** 控制台。](/help/sites-cloud/authoring/sites-console/introduction.md)
1. 导航到所需的位置。
1. 要打开选项列表，请从工具栏中选择&#x200B;**创建**
1. 选择&#x200B;**文件夹**&#x200B;以打开对话框。您可在此输入&#x200B;**名称**&#x200B;和&#x200B;**标题**：

   ![创建文件夹](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. 选择&#x200B;**创建**&#x200B;以创建文件夹。

>[!NOTE]
>
>* 文件夹也需遵循在指定新文件夹名称时用到的[页面命名惯例](#page-naming-conventions)。
>* 只有在 **Sites** 下或其他文件夹下才能直接创建文件夹。不能在页面下创建文件夹。
>* 可以对文件夹执行移动、复制、粘贴、删除、发布、取消发布和查看/编辑属性等标准操作。
>* 无法在 Live Copy 中选择文件夹。
