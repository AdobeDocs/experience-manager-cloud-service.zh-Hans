---
title: AEM 标记框架
description: 标记内容并利用AEM标记基础结构以对其进行分类和组织。
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 0%

---

# AEM标记框架 {#aem-tagging-framework}

标记允许对内容进行分类和组织。 标记可以按命名空间和分类进行分类。 有关使用标记的详细信息：

* 请参阅 [使用标记](/help/sites-cloud/authoring/features/tags.md) 有关将内容标记为内容作者的信息。
* 请参阅管理标记，以了解有关创建和管理标记以及已对哪些内容应用标记的管理员观点。

本文重点介绍在AEM中支持标记的基础框架以及如何作为开发人员利用该框架。

## 简介 {#introduction}

要标记内容并利用AEM标记基础结构，请执行以下操作：

* 标记必须作为类型的节点存在 [`cq:Tag`](#cq-tag-node-type) 下 [分类根节点。](#taxonomy-root-node)
* 标记内容节点的 `NodeType` 必须包括 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) 混合。
* 的 [`TagID`](#tagid) 添加到内容节点的 [`cq:tags`](#cq-tags-property) 属性并解析为类型的节点 [`cq:Tag`.](#cq-tag-node-type)

## cq：标记节点类型 {#cq-tag-node-type}

标记声明是在类型节点的存储库中捕获的 `cq:Tag.`

* 标记可以是一个简单的单词(例如， `sky`)或表示分层分类(例如， `fruit/apple`，即通用水果和更具体的苹果)。
* 标记由 `TagID`.
* 标记具有可选的元信息，如标题、本地化标题和描述。 标题应显示在用户界面中，而不是 `TagID`，如果存在。

标记框架还允许限制作者和网站访客仅使用特定的预定义标记。

### 标记特性 {#tag-characteristics}

* 节点类型为 `cq:Tag`.
* 节点名称是 [`TagID`.](#tagid)
* 的 [`TagID`](#tagid) 始终包含 [命名空间。](#tag-namespace)
* 的 `jcr:title` 属性（要在UI中显示的标题）是可选的。
* 的 `jcr:description` 属性为可选。
* 包含子节点时，称为 [容器标记。](#container-tags)
* 标记存储在存储库中名为 [分类根节点。](#taxonomy-root-node)

### 标记 ID {#tagid}

A `TagID` 标识解析为存储库中标记节点的路径。

通常， `TagID` 是速记 `TagID` 从命名空间开始，或者它可以是绝对 `TagID` 从 [分类根节点。](#taxonomy-root-node)

当内容已标记时，如果内容尚不存在，则 [`cq:tags`](#cq-tags-property) 属性会添加到内容节点，并且 `TagID` 添加到资产的 `String` 数组值。

的 `TagID` 由a [命名空间](#tag-namespace) 随后是当地人 `TagID`. [容器标记](#container-tags) 具有表示分类中分层顺序的子标记。 子标记可用于引用与任何本地标记相同的标记 `TagID`. 例如，标记内容时 `fruit` ，即使它是包含子标记的容器标记，例如 `fruit/apple` 和 `fruit/banana`.

### 分类根节点 {#taxonomy-root-node}

分类根节点是存储库中所有标记的基本路径。 分类根节点必须 *not* 是一种 `cq:Tag`.

在AEM中，基本路径为 `/content/cq:tags` 根节点是 `cq:Folder`.

### 标记命名空间 {#tag-namespace}

命名空间允许对事件进行分组。 最典型的用例是为每个站点（例如，公共与内部）或每个大型应用程序（例如，站点或资产）提供命名空间，但命名空间可用于满足各种其他需求。 用户界面中使用命名空间来仅显示适用于当前内容的标记（即特定命名空间的标记）子集。

标记的命名空间是分类子树中的第一个级别，即紧靠 [分类根节点。](#taxonomy-root-node) 命名空间是类型的节点 `cq:Tag` 其父项 `cq:Tag` 节点类型。

所有标记都具有命名空间。 如果未指定命名空间，则会将标记分配给默认的命名空间，该命名空间为 `TagID` `default`，即 `/content/cq:tags/default`.  标题默认为 `Standard Tags`在这种情况下。

### 容器标记 {#container-tags}

容器标记是类型的节点 `cq:Tag` 包含任意数量和类型的子节点，从而可以使用自定义元数据增强标记模型。

此外，分类中的容器标记（或超级标记）用作所有子标记的子总和：例如，标有 `fruit/apple` 被视为标记为 `fruit` 同样，也是搜索刚刚标有 `fruit` 也会找到标记为 `fruit/apple`.

### 解析TagID {#resolving-tagids}

如果标记ID包含冒号(`:`)，冒号将命名空间与标记或子分类分类分隔开，然后使用正斜杠(`/`)。 如果标记ID没有冒号，则表示默认的命名空间。

标记的标准位置和唯一位置如下所示 `/content/cq:tags`.

引用不指向的非现有路径或路径的标记 `cq:Tag` 节点被视为无效，因此被忽略。

下表显示了一些示例 `TagID`s、元素和方式 `TagID` 解析为存储库中的绝对路径：

| `TagID` | 命名空间 | 本地ID | 容器标记 | 叶标记 | 存储库绝对标记路径 |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (无) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (无) | (无) | (无) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### 标记标题的本地化 {#localization-of-tag-title}

当标记包含可选的标题字符串时 `jcr:title`，则可以通过添加属性将标题本地化以显示 `jcr:title.<locale>`.

有关更多详细信息，请参阅：

* [不同语言的标记，](tagging-applications.md#tags-in-different-languages) 其中介绍了API作为开发人员的使用
* 管理不同语言的标记，其中描述了如何以管理员身份使用标记控制台

### 访问控制 {#access-control}

标记作为节点存在于 [分类根节点。](#taxonomy-root-node) 通过在存储库中设置适当的ACL，可以允许或拒绝作者和网站访客在给定命名空间中创建标记。

拒绝某些标记或命名空间的读取权限将控制将标记应用于特定内容的功能。

典型做法包括：

* 允许 `tag-administrators` 组/角色对所有命名空间的写入权限(在 `/content/cq:tags`)。 此组附带现成的AEM。
* 允许用户/作者读取所有应可读取的命名空间（大部分）的读取权限。
* 允许用户/作者对用户/作者应可自由定义标记的命名空间进行写入访问(`add_node` 在 `/content/cq:tags/some_namespace`)

## 可标记内容：cq：可标记的Mixin {#taggable-content-cq-taggable-mixin}

为了让应用程序开发人员将标记附加到内容类型，节点会注册([CND](https://jackrabbit.apache.org/node-type-notation.html))必须包括 `cq:Taggable` mixin或 `cq:OwnerTaggable` 混合。

的 `cq:OwnerTaggable` mixin，继承自 `cq:Taggable`，旨在指示内容可以由所有者/作者分类。 在AEM中，它只是 `cq:PageContent` 节点。 的 `cq:OwnerTaggable` 标记框架不需要mixin。

>[!NOTE]
>
>建议仅在聚合内容项目的顶级节点(或其 `jcr:content` 节点)。 示例包括：
>
>* 页面(`cq:Page`)其中 `jcr:content`节点类型 `cq:PageContent`，其中包括 `cq:Taggable` 混合。
>* 资产(`cq:Asset`)其中 `jcr:content/metadata` 节点始终具有 `cq:Taggable` 混合。


### 节点类型表示法(CND) {#node-type-notation-cnd}

节点类型定义在存储库中以CND文件形式存在。 CND符号定义为 [JCR文档。](https://jackrabbit.apache.org/node-type-notation.html).

AEM中包含的节点类型的基本定义如下：

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## cq:tags属性 {#cq-tags-property}

的 `cq:tags` 属性是 `String` 用于存储一个或多个的阵列 `TagID`适用于作者或网站访客对内容应用的情况。 仅当添加到通过 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) 混合。

>[!NOTE]
>
>要利用AEM标记功能，自定义开发的应用程序不应定义标记属性，而 `cq:tags`.

## 移动和合并标记 {#moving-and-merging-tags}

以下是使用标记控制台移动或合并标记时存储库中的效果描述。

当标记A被移动或合并到 `/content/cq:tags`:

* 未删除标记A，并会收到 `cq:movedTo` 属性。
   * `cq:movedTo` 指向标记B。
   * 此属性表示标记A已移动或合并到标记B中。
   * 移动标记B将相应地更新此属性。
   * 因此，标记A是隐藏的，仅保留在存储库中，以解析指向标记A的内容节点中的标记ID。
   * 标记垃圾回收器会删除标记A等标记，以便不再有内容节点指向它们。
   * 的特殊值 `cq:movedTo` 属性 `nirvana`，在删除标记时应用，但无法从存储库中删除，因为存在具有 `cq:movedTo` 必须保留。

      >[!NOTE]
      >
      >的 `cq:movedTo` 仅当满足以下任一条件时，才会将属性添加到已移动或已合并的标记中：
      >
      > 1. 标记在内容中使用（即它有引用）。 或者
      > 1. 标记的子项已被移动。

* 标记B被创建（如果移动）并接收 `cq:backlinks` 属性。
   * `cq:backlinks` 将引用保留在另一个方向，即保留已移动到标记B或与标记B合并的所有标记的列表。
   * 这通常是保留 `cq:movedTo` 属性。

      >[!NOTE]
      >
      >的 `cq:backlinks` 仅当满足以下任一条件时，才会将属性添加到已移动或已合并的标记中：
      >
      > 1. 标记在内容中使用（即它有引用）。 或者
      > 1. 标记的子项已被移动。


阅读 `cq:tags` 内容节点的属性涉及以下解决方案：

1. 如果下没有匹配项 `/content/cq:tags`，则不会返回任何标记。
1. 如果标记具有 `cq:movedTo` 属性设置时，引用的标记ID会跟在后面。
   * 只要跟随的标记具有 `cq:movedTo` 属性。
1. 如果跟随的标记没有 `cq:movedTo` 属性中，将读取标记。

要在移动或合并标记后发布更改，请 `cq:Tag` 节点及其所有后台链接都必须复制。 当标记在标记管理控制台中激活时，将自动完成此操作。

稍后对页面的 `cq:tags` 属性会自动清除旧引用。 之所以触发此事件，是因为通过API解析移动的标记会返回目标标记，从而提供目标标记ID。
