---
title: AEM Tagging Framework
description: 标记内容并利用AEM Tagging基础结构，以便对其进行分类和组织。
translation-type: tm+mt
source-git-commit: 4bf023068aa69fb6b69c6f2443703ea2bbbf7d42
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 0%

---


# AEM Tagging Framework {#aem-tagging-framework}

标记允许对内容进行分类和组织。 标记可以按命名空间和分类进行分类。 有关使用标记的详细信息：

* 有关 [将内容标记为](/help/sites-cloud/authoring/features/tags.md) （作为内容作者）的信息，请参阅使用标记。
* 有关创建和管理标记以及已应用哪些内容标记的管理员观点，请参阅管理标记。

本文重点介绍支持AEM中标记的底层框架以及如何将其作为开发人员使用。

## 简介 {#introduction}

要标记内容并利用AEM Tagging基础结构：

* 标记必须作为分类根节点下的类 [`cq:Tag`](#cq-tag-node-type) 型 [节点存在。](#taxonomy-root-node)
* 标记内容节点必 `NodeType` 须包含混 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) 音。
* 该 [`TagID`](#tagid) 属性将添加到内容节点的属 [`cq:tags`](#cq-tags-property) 性并解析到类型的节点 [`cq:Tag`。](#cq-tag-node-type)

## cq：标记节点类型 {#cq-tag-node-type}

标记声明在存储库中的类型节点中捕获 `cq:Tag.`

* 标记可以是简单的单词(例如， `sky`)或表示分层分类(例如， `fruit/apple`，表示普通水果和更具体的苹果)。
* 标记由唯一标记标 `TagID`识。
* 标记具有可选的元信息，如标题、本地化标题和说明。 标题应当在用户界面中显示，而 `TagID`不是（如果存在）。

标记框架还允许限制作者和站点访客仅使用特定的预定义标记。

### 标签特性 {#tag-characteristics}

* 节点类型为 `cq:Tag`。
* 节点名称是的组件 [`TagID`。](#tagid)
* 始终 [`TagID`](#tagid) 包含一个 [命名空间。](#tag-namespace)
* 属 `jcr:title` 性（要在UI中显示的标题）是可选的。
* 该属 `jcr:description` 性是可选的。
* 包含子节点时，称为 [容器标记。](#container-tags)
* 标记存储在名为分类根节点的基本路径 [下的存储库中。](#taxonomy-root-node)

### 标记 ID {#tagid}

标识 `TagID` 解析到存储库中的标记节点的路径。

通常， `TagID` 命名空间是以 `TagID` 开头的速记，也可以是从分类根节 `TagID` 点开始的 [绝对值。](#taxonomy-root-node)

标记内容时，如果内容尚不存在， [`cq:tags`](#cq-tags-property) 则将属性添加到内容节点，并 `TagID` 将属性添加到属性的数 `String` 组值中。

它 `TagID` 由一个 [命名空间](#tag-namespace) ，后跟本地 `TagID`。 [容器标](#container-tags) 签具有子标签，这些子标签表示分类中的分层顺序。 子标记可用于引用与任何本地标记相同的标记 `TagID`。 例如，允许 `fruit` 用标记内容，即使它是带有子标记的容器标记， `fruit/apple` 如和 `fruit/banana`。

### 分类根节点 {#taxonomy-root-node}

分类根节点是存储库中所有标记的基本路径。 分类根节点不 *能* 是类型的节点 `cq:Tag`。

在AEM中，基路径 `/content/cq:tags` 为，根节点为类型 `cq:Folder`。

### 标记命名空间 {#tag-namespace}

命名空间允许将事物分组。 最典型的用例是每个站点（例如，公共和内部）或每个较大的应用程序（例如，站点或资产）都有命名空间，但命名空间可用于各种其他需求。 命名空间在用户界面中用于仅显示适用于当前内容的标记子集(即特定命名空间的标记)。

标记的命名空间是分类子树中的第一级，该子树是紧挨分类根节点 [的节点。](#taxonomy-root-node) 命名空间是父代不是节 `cq:Tag` 点类型的节 `cq:Tag` 点类型。

所有标记均具有命名空间。 如果未指定命名空间，则标记将分配给默认命名空间，即 `TagID` , `default`即， `/content/cq:tags/default`.  在这种情况下， `Standard Tags`标题默认为。

### 容器标记 {#container-tags}

容器标签是包含任意数 `cq:Tag` 量和子节点类型的节点，它使用自定义元数据增强标签模型成为可能。

此外，分类中的容器标签（或超级标签）用作所有子标签的子总和：例如，被标记 `fruit/apple` 的内容也被视为被 `fruit` 标记，即，搜索仅被标记的内容也会 `fruit` 找到被标记的内容 `fruit/apple`

### 解析标记ID {#resolving-tagids}

如果标记ID包含冒号(`:`)，则冒号将命名空间与标记或子分类分开，然后用正斜杠()分`/`开。 如果标记ID没有冒号，则默示默认命名空间。

标记的标准和唯一位置如下所示 `/content/cq:tags`。

引用不指向节点的非现有路径或路径的标 `cq:Tag` 记被视为无效并被忽略。

下表显示了一些示 `TagID`例、其元素，以及如何将 `TagID` 其解析为存储库中的绝对路径：

| `TagID` | 命名空间 | 本地ID | 容器标记 | Leaf标签 | 存储库绝对标记路径 |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (无) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (无) | (无) | (无) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### 标记标题本地化 {#localization-of-tag-title}

当标记包含可选的标 `jcr:title`题字符串时，可以通过添加属性来本地化要显示的标题 `jcr:title.<locale>`。

有关详细信息，请参阅：

* [不同语言的标签](tagging-applications.md#tags-in-different-languages) ，描述API作为开发人员的使用
* 管理不同语言的标记，其中描述了以管理员身份使用标记控制台

### 访问控制 {#access-control}

标记作为节点存在于分类根节 [点下的存储库中。](#taxonomy-root-node) 允许或拒绝作者和站点访客在给定命名空间中创建标记，可以通过在存储库中设置适当的ACL。

拒绝某些标记或命名空间的读取权限将控制将标记应用于特定内容的能力。

典型做法包括：

* 允许对 `tag-administrators` 所有命名空间（在下添加／修改）进行组／角色写入 `/content/cq:tags`访问。 这个组随附AEM即装即用。
* 允许用户／作者读取应可读的所有命名空间（大多数）。
* 允许用户／作者对用户／作者可自由定义标记的命名空间进行写入`add_node` 访问( `/content/cq:tags/some_namespace`下)

## 可标记内容：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

为了使应用程序开发人员将标记附加到内容类型，节点的注册([CND](https://jackrabbit.apache.org/node-type-notation.html))必须包含 `cq:Taggable` 混合或混 `cq:OwnerTaggable` 合。

继承 `cq:OwnerTaggable` 自的混音旨在 `cq:Taggable`指示内容可由所有者／作者进行分类。 在AEM中，它只是节点的属 `cq:PageContent` 性。 标 `cq:OwnerTaggable` 记框架不需要混合。

>[!NOTE]
>
>建议仅在聚集内容项的顶级节点（或其节点）上启用 `jcr:content` 标记。 示例包括：
>
>* 节点类`cq:Page`型的页 `jcr:content`面(包 `cq:PageContent`括混合 `cq:Taggable` 内容)。
>* 资产(`cq:Asset`)节点始 `jcr:content/metadata` 终具有混合的 `cq:Taggable` 资产。


### 节点类型表示法(CND) {#node-type-notation-cnd}

节点类型定义作为CND文件存在在存储库中。 CND记号被定义为JCR文档 [的一部分](https://jackrabbit.apache.org/node-type-notation.html)。

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

该属 `cq:tags` 性是一个数 `String` 组，当作者或站点访客将一 `TagID`个或多个应用于内容时，它们用于存储。 仅当添加到使用mixin定义的节点时，该属性才具有 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) 意义。

>[!NOTE]
>
>要利用AEM标记功能，自定义开发的应用程序不应定义标记属性 `cq:tags`。

## 移动和合并标记 {#moving-and-merging-tags}

以下是使用标记控制台移动或合并标记时存储库中效果的说明。

当标记A移动或合并到标记B时，位于 `/content/cq:tags`:

* 标记A未被删除，并且接收 `cq:movedTo` 属性。
   * `cq:movedTo` 指向标记B。
   * 此属性表示标记A已被移动或合并到标记B中。
   * 移动标记B将相应地更新此属性。
   * 因此，标记A是隐藏的，它仅保存在存储库中以解析指向标记A的内容节点中的标记ID。
   * 标记垃圾收集器删除标记（如标记A），不再有内容节点指向它们。
   * 属性的特殊值 `cq:movedTo` 是 `nirvana`在删除标记时应用的，但无法从存储库中删除，因为存在必须保留带有 `cq:movedTo` 子标记的子标记。

      >[!NOTE]
      >
      >仅当 `cq:movedTo` 满足以下任一条件时，属性才会添加到已移动或合并的标记：
      >
      > 1. 标记用于内容（即它有引用）。 或者
      > 1. 标签包含已移动的子项。


* 创建标记B（在移动时）并接收属 `cq:backlinks` 性。
   * `cq:backlinks` 使引用保持在另一个方向，即保留已移动到标记B或与标记B合并的所有标记的列表。
   * 这主要是为了在移 `cq:movedTo` 动／合并／删除标记B或激活标记B时使属性保持最新而必需的，在这种情况下，还必须激活其所有背景链接标记。

      >[!NOTE]
      >
      >仅当 `cq:backlinks` 满足以下任一条件时，属性才会添加到已移动或合并的标记：
      >
      > 1. 标记用于内容（即它有引用）。 或者
      > 1. 标签包含已移动的子项。


读取内 `cq:tags` 容节点的属性涉及以下分辨率：

1. 如果下面没有匹配项， `/content/cq:tags`则不返回任何标记。
1. 如果标记设置了 `cq:movedTo` 属性，则引用的标记ID会随后显示。
   * 只要后跟的标记具有属性，则重复此 `cq:movedTo` 步骤。
1. 如果后面的标记没有属 `cq:movedTo` 性，则会读取标记。

要在标记被移动或合并时发布更改，必须 `cq:Tag` 复制节点及其所有反向链接。 在标记管理控制台中激活标记时，系统会自动执行此操作。

以后对页面属性的更 `cq:tags` 新会自动清除旧引用。 这是由于通过API解析移动的标记会返回目标标记，从而提供目标标记ID而触发的。
