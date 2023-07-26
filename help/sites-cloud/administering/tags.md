---
title: 管理标记
description: 了解如何管理AEM中的标记以整理您的内容。
source-git-commit: af60a2b8f1e2dd7fc55247ecb0251d7b85f63eb3
workflow-type: tm+mt
source-wordcount: '2272'
ht-degree: 1%

---


# 管理标记 {#administering-tags}

标记是一种对内容进行分类的直观方法。 它们可以被视为关键字或标签（元数据），以便更快地找到内容。

在Adobe Experience Manager (AEM)中，标记可以是以下属性：

* 页面的内容节点
   * 查看文档 [使用标记](/help/sites-cloud/authoring/features/tags.md) 以了解更多信息。
* 资源的元数据节点
   * 查看文档 [管理数字资产的元数据](/help/assets/manage-metadata.md) 以了解更多信息。

>[!TIP]
>
>最佳实践是最大限度地减少与相同想法相关的标记数量。 例如，如果您管理的是户外用品商店的内容，则可能不需要同时使用这两个标签 **鞋类** 和 **鞋子**.

## 标记功能 {#tag-features}

标记提供了用于组织和管理内容的强大功能。

* 标记可以分组到各种命名空间中。
   * 命名空间可以被视为允许构建分类的层次结构。
   * 这些分类在整个AEM中都是全局的。
* 标记可由作者应用并由网站访客使用。
* 无论其创建者如何，在分配给页面或搜索时，所有形式的标记都可供选择。
* 标记由 [列表组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html) 以根据所选标记生成动态列表。

## 标记要求 {#requirements}

创建和管理标记时，请牢记一些技术细节。

* 标记在特定命名空间中必须唯一。
* 标记的名称可能不包括标记分隔符：
   * 冒号(`:`) — 分隔命名空间标记
   * 斜杠(`/`) — 分隔子标记
* 如果标记的标题包含标记分隔符，则将在UI中禁止显示这些分隔符。
* 标记可由以下用户创建，其分类也可由 `tag-administrators` 拥有对下列各项之修改权之本集团及成员： `/content/cq:tags`.
   * 包含子标记的标记称为容器标记。
   * 不是容器标记的标记称为叶标记。
   * 标记命名空间可以是叶标记或容器标记。

有关标记如何工作的更多技术详细信息，请参阅文档 [AEM标记框架。](/help/implementing/developing/introduction/tagging-framework.md)

## 标记控制台 {#tagging-console}

标记控制台用于创建和管理标记及其分类。 您可以使用标记控制台通过以下方式管理标记：

* 将它们分组到命名空间中。
* 在创建新标记之前，审查现有标记的使用情况。
* 重新组织标记而不断开标记与当前引用内容的连接。

要访问标记控制台，请执行以下操作：

1. 使用管理权限登录到创作环境。
1. 在全局导航菜单中，选择 **`Tools`** -> **`General`** ->
   **`Tagging`**。

![AEM中的标记控制台](/help/sites-cloud/administering/assets/tagging-console.png)

## 创建新标记 {#creating-new-tags}

可通过大量步骤来创建并使用标记来整理您的内容。

1. [为标记创建命名空间](#creating-namespaces) （或选择现有模板以重复使用）。
1. [创建新标记。](#creating-tags)
1. [发布标记。](#publishing-tags)

### 创建命名空间 {#creating-namespaces}

命名空间用于组织其他标记。 可以将其视为最低级别的标记，通常用于分组其他标记。

1. 要创建新命名空间，请打开 [标记控制台](#tagging-console) 然后点按或单击 **创建** 工具栏中的按钮，然后 **创建命名空间**.

   ![“添加命名空间”对话框](/help/sites-cloud/administering/assets/add-namespace.png)

1. 提供必要的信息。

   * **标题** - UI中向用户显示的命名空间标题（可选）
   * **名称**  — 如果未指定名称，则会从 **标题**. 查看文档 [AEM标记框架](/help/implementing/developing/introduction/tagging-framework.md#tagid) 以了解更多信息。
   * **描述**  — 命名空间的描述（可选）

1. 输入所需信息后，点击或单击 **创建**.

将创建命名空间。 请注意，在标记控制台中，命名空间位于最低级别（位于控制台的最左列），由文件夹图标表示，这反映了它们作为“容器”或其他标记分组的性质。

您现在可以 [创建新标记](#creating-tags) 在此命名空间中或 [管理现有标记。](#managing-tags)

命名空间不需要包含任何子标记。 由于命名空间本身就是标记，因此可用于将您的内容组织为任何其他标记。 但是，要继续创建结构化标记分类，您可以 [创建子标记](#creating-tags) 在该命名空间中。

### 创建标记 {#creating-tags}

标记通常添加到命名空间。

1. 要创建新标记，请打开 [标记控制台。](#tagging-console)

1. 选择要创建标记的命名空间。 或者选择另一个标记以在其下面创建子标记。

1. 点按或单击 **创建** 工具栏上的按钮，然后 **创建标记**.

1. 此 **创建标记** 对话框打开。 为新标记提供所需信息。

   * **标题**  — 标记的显示标题（必需）
   * **名称**  — 标记的名称（必需）。 如果未指定，则会从 **标题**. 请参阅 [标记ID](/help/implementing/developing/introduction/tagging-framework.md#tagid).
   * **描述**  — 标记的描述
   * **标记路径**  — 默认为在标记控制台中选择的命名空间（或标记）。 通过点按或单击路径选择器图标，可手动更新路径。

   ![“创建标记”对话框](assets/create-tag.png)

1. 点击或单击 **提交**.

将创建标记，并更新控制台以显示新标记。

标记允许根据组织需求灵活创建自己的分类。

* 您可以在创建新标记之前，通过在控制台中选择父标记来创建现有标记的子标记。
* 如果您创建标记但未选择命名空间或其他标记，则实际上会创建一个新的命名空间。

### 发布标记 {#publishing-tags}

与在AEM中创建任何其他内容一样，在创建标记（或命名空间）后，它仅存在于创作环境中。 要让您的标记对用户可用，您必须发布这些标记。

1. 要发布标记，请打开 [标记控制台。](#tagging-console)

1. 选择要发布的一个或多个标记，然后在工具栏中选择 **Publish**.

   ![在控制台中选择标记](assets/select-tags.png)

1. 此 **发布标记** 对话框要求确认发布所选标记。 点按或单击&#x200B;**发布**。

   ![发布标记确认模式](assets/publish-tag.png)

1. 已使用确认发布操作 **成功** 对话框。

   ![发布标记成功对话框](assets/publish-tag-success.png)

选定的标记将排队等待发布。 与页面内容类似，只发布选定的标记，而不管它是否具有子标记。

要发布整个分类（命名空间和子标记），最佳实践是创建 [包](/help/implementing/developing/tools/package-manager.md) 命名空间的(请参阅 [分类根节点](/help/implementing/developing/introduction/tagging-framework.md#taxonomy-root-node))。

<!--
Be sure to [apply permissions](#setting-tag-permissions) to the namespace before creating the package.
-->

## 管理标记 {#managing-tags}

您可以对现有标记和命名空间执行许多操作以管理和组织它们。 只需在 [标记控制台](#tagging-console) 以在工具栏中显示可用的操作。

* [查看属性](#viewing-tag-properties)
* [编辑](#editing-tags)
* [取消发布](#unpublishing-tags)
* [引用](#viewing-tag-references)
* [移动](#moving-tags)
* [合并](#merging-tags)
* [删除](#deleting-tags)

请注意，当工具栏上有足够的可用空间时，省略号图标后面会提供其他选项。

### 查看标记属性 {#viewing-tag-properties}

在标记控制台中选择单个标记、命名空间或其他标记时，所选标记的基本详细信息（如上次编辑时间和上次发布）将显示在标记列左侧的列中。

![标记详细信息列](assets/tag-details-column.png)

您可以查看有关标记的更多详细信息，包括上次发布该标记的人员和发布时间，方法是将控制台切换到 **属性** 视图。

1. 要查看标记的属性，请打开 [标记控制台。](#tagging-console)

1. 选择要查看其属性的标记，然后在左边栏中选择 **属性**.

   ![选择属性视图](assets/view-tag-properties.png)

1. 所选标记的详细属性显示在左边栏中。

   ![查看标记属性](assets/tag-properties.png)

有关选择查看模式和边栏的更多详细信息，请参阅文档 [基本操作。](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

### 编辑标记 {#editing-tags}

标记和命名空间可在创建后进行编辑。

1. 要编辑标记，请打开 [标记控制台。](#tagging-console)

1. 选择要编辑的标记，然后在工具栏中选择 **编辑**.

1. 进行所需的更改。 可以更改以下内容：

   * **标题**
   * **描述**
   * [**本地化**](#managing-tags-in-different-languages)

1. 进行编辑后，点按或单击 **提交**.

有关添加语言翻译的详细信息，请参阅 [管理不同语言的标记](#managing-tags-in-different-languages).

如果对已发布的标记进行了更改，则您可能希望 [重新发布。](#publishing-tags)

### 取消发布标记 {#unpublishing-tags}

要在创作实例上停用标记并将其从发布实例中删除，您可以取消发布它。

1. 要取消发布标记，请打开 [标记控制台。](#tagging-console)

1. 选择要取消发布的一个或多个标记，然后在工具栏中选择 **取消发布**.

   ![在控制台中选择标记](assets/select-tags.png)

1. 此 **取消发布标记** 对话框要求确认发布所选标记。 点按或单击&#x200B;**发布**。

   ![发布标记确认模式](assets/unpublish-tag.png)

1. 已使用确认取消发布操作 **成功** 对话框。

   ![发布标记成功对话框](assets/unpublish-tag-success.png)

选定的标记将排队等待取消发布。 如果所选标记是容器标记，则其所有子标记将在创作环境中停用，并从发布环境中移除。

### 查看标记引用 {#viewing-tag-references}

查看特定标记应用于哪些内容可能很有用。 为此，您可以使用 **引用** 在标记控制台中查看。

1. 要查看标记的引用，请打开 [标记控制台。](#tagging-console)

1. 选择要查看其引用的标记，然后在左边栏中选择 **引用**.

   ![选择属性视图](assets/view-tag-references.png)

1. 所选标记的引用总数会显示在左边栏中。

   ![查看标记引用](assets/tag-references.png)

1. 点按或单击标签引用的数量，可查看分配给标签的内容详细列表。

   ![查看标记引用的详细信息](assets/tag-references-detail.png)

将鼠标悬停在列表中或点按引用内容以显示内容的完整路径。

有关选择查看模式和边栏的更多详细信息，请参阅文档 [基本操作。](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

### 移动标记 {#moving-tags}

可能需要通过将标记移动到新位置或重命名标记来清理或重新组织标记分类。

>[!TIP]
>
>最佳做法是仅允许管理员移动和重命名标记。

1. 要移动或重命名标记，请打开 [标记控制台。](#tagging-console)

1. 选择要移动或重命名的标记，然后点按或单击 **移动** 工具栏中。

1. 在 **移动标记** 对话框，指定要更改的属性。

   * **重命名为**  — 您希望为标记提供的新名称
      * 此字段已预填充为标记的当前名称。
      * 如果只想移动标记而不想重命名它，请保持未修改状态。
   * **移动到**  — 您希望移动标记的位置
      * 此字段已预填充为标记的当前位置。
      * 如果您只想重命名标记而不想移动它，请保持未修改状态。

   ![移动标记](assets/move-tag.png)

1. 点击或单击 **提交**.

标记将重命名和/或移动到其新位置。 如果所选标记是容器标记，则移动标记也将移动所有子标记。

### 合并标记 {#merging-tags}

如果标记分类有重复项或类似的标记，则合并这些标记会很有用。 When标记 `A` 被合并到标记中 `B`，所有带标记页面 `A` 使用标记进行标记 `B` 和标记 `A` 不再适用于作者。

1. 要合并两个标记，请打开 [标记控制台。](#tagging-console)

1. 选择要合并到其他标记的标记，然后点按或单击 **合并** 工具栏中。

1. 在 **合并标记** 对话框，点击或单击 **浏览** 图标 **合并到** 字段，用于指定要将所选标记合并到哪个标记中。

   ![“合并标记”对话框](assets/merge-tag.png)

1. 点击或单击 **提交**.

在控制台中选择的标记将合并到对话框中指定的标记中。 移动或合并引用的标记时，不会实际删除该标记，因此可以保留引用。 请参阅文档 [AEM标记框架](/help/implementing/developing/introduction/tagging-framework.md#moving-and-merging-tags) 以了解更多信息。

### 正在删除标记 {#deleting-tags}

如果您的标记分类发生更改并且使标记或命名空间变得不需要，则可以将其删除。

1. 要删除标记，请打开 [标记控制台。](#tagging-console)

1. 选择要删除的标记，然后点按或单击 **删除** 工具栏中。

1. 此 **删除标记** 对话框要求确认删除所选标记。 点击或单击 **删除**.

   ![删除标记确认模式](assets/delete-tag.png)

1. AEM会检查以确保标记未被引用。

   1. 如果找不到引用，AEM会要求最终确认删除。 点击或单击 **删除**

      ![未找到引用](assets/no-references-found.png)

   1. 如果找到引用，AEM会显示它们并请求最终确认将其删除。

      ![找到个引用](assets/references-found.png)

选定的标记将被删除并从创作环境中永久移除。 如果标记已发布，则也会从发布环境中将其删除。 如果所选标记是容器标记，则也会移除其所有子标记。

<!--

## Setting Tag Permissions {#setting-tag-permissions}

Tag permissions are ['secure (by default)'](/help/sites-administering/production-ready.md); a best practice for the publish environment that requires read permission to be explicitly allowed for tags. Bascially, this is done by creating a package of the Tag Namespace after permissions have been set on author, and installing the package on all publish instances.

* on author instance

    * sign in with administrative privileges
    * access the [Security Console](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

        * for example, browse to http://localhost:4502/useradmin

    * in the left pane, select the group (or user) for which [read permission](/help/sites-administering/security.md#permissions) is to be granted
    * in the right pane, locate the **Path **to the Tag Namespace

        * for example, `/content/cq:tags/mycommunity`

    * select the `checkbox`in the **Read** column
    * select **Save**

![chlimage_1-204](assets/chlimage_1-204.png)

* ensure all publish instances have same permissions

    * one approach is to [create a package](/help/sites-administering/package-manager.md#package-manager) of the namespace on author

        * on `Advanced` tab, for `AC Handling` select `Overwrite`

    * replicate the package

        * choose `Replicate` from package manager

-->

## 管理不同语言的标记 {#managing-tags-in-different-languages}

此 `title` 标记属性可以翻译成多种语言。 一旦翻译，可以根据用户或内容语言显示适当的标记标题。

假设我们有一个名为 `Animals` 我们要把这些语言翻译成德文和法文

1. 打开 [标记控制台。](#tagging-console)

1. 选择要翻译的标记，然后点按或单击 **编辑** 工具栏中。

1. 在 **编辑标记** 对话框，在 **本地化** 列中，选择目标语言，例如德语。

1. 在 **德语** 字段，提供已翻译标题。

1. 对法语重复前两个步骤。

   ![翻译标记标题](assets/translate-tag.png)

1. 点击或单击 **提交**.

对于内容页面，为标记选择的语言将从页面语言中获取（如果可用）。

但是，在创作环境中，AEM使用用户语言设置。 在标记控制台中，对于 `Animals` 标记， `Animaux` 对于在其用户属性中将语言设置为法语的用户，将显示。

要向对话框添加新语言，请参阅文档 [将标记构建到AEM应用程序中](/help/implementing/developing/introduction/tagging-applications.md#adding-a-new-language-to-the-edit-tag-dialog)

>[!TIP]
>
>如果您想了解有关AEM本地化功能的更多信息，请参阅文档 [为多语言站点翻译内容。](/help/sites-cloud/administering/translation/overview.md)
