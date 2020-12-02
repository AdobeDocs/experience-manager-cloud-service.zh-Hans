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

* 有关将内容标记为内容作者的信息，请参阅[使用标记](/help/sites-cloud/authoring/features/tags.md)。
* 有关创建和管理标记以及已应用哪些内容标记的管理员观点，请参阅管理标记。

本文重点介绍支持AEM中标记的底层框架以及如何将其作为开发人员使用。

## 简介 {#introduction}

要标记内容并利用AEM Tagging基础结构：

* 标记必须作为[分类根节点下类型[`cq:Tag`](#cq-tag-node-type)的节点存在。](#taxonomy-root-node)
* 标记内容节点的`NodeType`必须包含[`cq:Taggable`](#taggable-content-cq-taggable-mixin)混音。
* [`TagID`](#tagid)被添加到内容节点的[`cq:tags`](#cq-tags-property)属性，并解析到类型为[`cq:Tag`的节点。](#cq-tag-node-type)

## cq：标记节点类型{#cq-tag-node-type}

标记声明在`cq:Tag.`类型的节点中的存储库中捕获

* 标记可以是简单的单词(例如，(例如，`sky`，表示通用水果和更具体的苹果)。`fruit/apple`
* 标记由唯一`TagID`标识。
* 标记具有可选的元信息，如标题、本地化标题和说明。 标题应显示在用户界面中，而不是`TagID`（如果存在）。

标记框架还允许限制作者和站点访客仅使用特定的预定义标记。

### 标记特性{#tag-characteristics}

* 节点类型为`cq:Tag`。
* 节点名称是[`TagID`的组件。](#tagid)
* [`TagID`](#tagid)始终包含[命名空间。](#tag-namespace)
* `jcr:title`属性（要在UI中显示的标题）是可选的。
* `jcr:description`属性是可选的。
* 包含子节点时，称为[容器标签。](#container-tags)
* 标记存储在名为[分类根节点的基本路径下的存储库中。](#taxonomy-root-node)

### 标记 ID {#tagid}

`TagID`标识解析到存储库中标记节点的路径。

通常，`TagID`是以命名空间开头的速记`TagID`，也可以是从[分类根节点开始的绝对`TagID`。](#taxonomy-root-node)

标记内容时，如果内容尚不存在，则[`cq:tags`](#cq-tags-property)属性将添加到内容节点，`TagID`将添加到属性的`String`数组值。

`TagID`由[命名空间](#tag-namespace)和本地`TagID`组成。 [容器](#container-tags) 标语子标签，表示分类中的分层顺序。子标签可用于引用与任何本地`TagID`相同的标签。 例如，允许用`fruit`标记内容，即使它是具有子标签（如`fruit/apple`和`fruit/banana`）的容器标签。

### 分类根节点{#taxonomy-root-node}

分类根节点是存储库中所有标记的基本路径。 分类根节点必须&#x200B;*不*&#x200B;是类型`cq:Tag`的节点。

在AEM中，基路径为`/content/cq:tags`，根节点的类型为`cq:Folder`。

### 标记命名空间{#tag-namespace}

命名空间允许将事物分组。 最典型的用例是每个站点（例如，公共和内部）或每个较大的应用程序（例如，站点或资产）都有命名空间，但命名空间可用于各种其他需求。 命名空间在用户界面中用于仅显示适用于当前内容的标记子集(即特定命名空间的标记)。

标记的命名空间是分类子树中的第一级，该子树是紧挨[分类根节点的节点。](#taxonomy-root-node) 命名空间是父代不是节 `cq:Tag` 点类型的节 `cq:Tag` 点类型。

所有标记均具有命名空间。 如果未指定命名空间，则标记将分配给默认命名空间，即`TagID` `default`，即。`/content/cq:tags/default`。  在这种情况下，“标题”默认为`Standard Tags`。

### 容器标记{#container-tags}

容器标记是`cq:Tag`类型的节点，包含任意数量和类型的子节点，这使得可以使用自定义元数据增强标记模型。

此外，分类中的容器标签（或超级标签）用作所有子标签的子总和：例如，使用`fruit/apple`标记的内容也被视为使用`fruit`标记，即搜索仅使用`fruit`标记的内容也会找到使用`fruit/apple`标记的内容。

### 解析TagID {#resolving-tagids}

如果标记ID包含冒号(`:`)，则冒号将命名空间与标记或子分类分开，然后用正斜杠(`/`)分开。 如果标记ID没有冒号，则默示默认命名空间。

标记的标准和唯一位置低于`/content/cq:tags`。

引用不指向`cq:Tag`节点的非现有路径或路径的标记被视为无效并被忽略。

下表显示了一些示例`TagID`s、其元素，以及`TagID`如何解析为存储库中的绝对路径：

| `TagID` | 命名空间 | 本地ID | 容器标记 | Leaf标签 | 存储库绝对标记路径 |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (无) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (无) | (无) | (无) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### 标记标题本地化{#localization-of-tag-title}

当标记包含可选的标题字符串`jcr:title`时，可以通过添加属性`jcr:title.<locale>`来本地化要显示的标题。

有关详细信息，请参阅：

* [不同语言的标](tagging-applications.md#tags-in-different-languages) 签，描述API作为开发人员的使用
* 管理不同语言的标记，其中描述了以管理员身份使用标记控制台

### 访问控制 {#access-control}

标记作为节点存在于[分类根节点下的存储库中。](#taxonomy-root-node) 允许或拒绝作者和站点访客在给定命名空间中创建标记，可以通过在存储库中设置适当的ACL。

拒绝某些标记或命名空间的读取权限将控制将标记应用于特定内容的能力。

典型做法包括：

* 允许`tag-administrators`组／角色对所有命名空间进行写入访问（在`/content/cq:tags`下添加／修改）。 这个组随附AEM即装即用。
* 允许用户／作者读取应可读的所有命名空间（大多数）。
* 允许用户／作者对用户／作者可自由定义标记的命名空间进行写入访问（`/content/cq:tags/some_namespace`下的`add_node`）

## 可标记内容：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

为了使应用程序开发人员将标记附加到内容类型，节点的注册([CND](https://jackrabbit.apache.org/node-type-notation.html))必须包括`cq:Taggable`混音或`cq:OwnerTaggable`混音。

继承自`cq:Taggable`的`cq:OwnerTaggable`混音旨在指示内容可由所有者／作者分类。 在AEM中，它只是`cq:PageContent`节点的属性。 标记框架不需要`cq:OwnerTaggable`混音。

>[!NOTE]
>
>建议仅在聚集内容项（或其`jcr:content`节点）的顶级节点上启用标记。 示例包括：
>
>* 页(`cq:Page`)，其中`jcr:content`节点类型为`cq:PageContent`，其中包括`cq:Taggable`混音。
>* 资产(`cq:Asset`)，其中`jcr:content/metadata`节点始终具有`cq:Taggable`混音。


### 节点类型表示法(CND){#node-type-notation-cnd}

节点类型定义作为CND文件存在在存储库中。 CND记号定义为[JCR文档的一部分。](https://jackrabbit.apache.org/node-type-notation.html)。

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

## cq:tags属性{#cq-tags-property}

`cq:tags`属性是`String`数组，当作者或站点访客将`TagID`应用于内容时，它们用于存储一个或多个&lt;a2/>。 仅当添加到使用[`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin定义的节点时，该属性才有意义。

>[!NOTE]
>
>要利用AEM标记功能，自定义开发的应用程序不应定义`cq:tags`以外的标记属性。

## 移动和合并标记{#moving-and-merging-tags}

以下是使用标记控制台移动或合并标记时存储库中效果的说明。

当标记A被移动或合并到`/content/cq:tags`下的标记B中时：

* 未删除标记A并接收`cq:movedTo`属性。
   * `cq:movedTo` 指向标记B。
   * 此属性表示标记A已被移动或合并到标记B中。
   * 移动标记B将相应地更新此属性。
   * 因此，标记A是隐藏的，它仅保存在存储库中以解析指向标记A的内容节点中的标记ID。
   * 标记垃圾收集器删除标记（如标记A），不再有内容节点指向它们。
   * `cq:movedTo`属性的特殊值为`nirvana`，当删除标记时将应用该值，但无法从存储库中删除该值，因为必须保留具有`cq:movedTo`的子标记。

      >[!NOTE]
      >
      >仅当满足以下任一条件时，`cq:movedTo`属性才会添加到已移动或合并的标记：
      >
      > 1. 标记用于内容（即它有引用）。 或者
      > 1. 标签包含已移动的子项。


* 创建标记B（在移动时）并接收`cq:backlinks`属性。
   * `cq:backlinks` 使引用保持在另一个方向，即保留已移动到标记B或与标记B合并的所有标记的列表。
   * 当标记B被移动／合并／删除或标记B被激活时，这通常要求使`cq:movedTo`属性保持最新，在这种情况下，必须同时激活其所有反向链接标记。

      >[!NOTE]
      >
      >仅当满足以下任一条件时，`cq:backlinks`属性才会添加到已移动或合并的标记：
      >
      > 1. 标记用于内容（即它有引用）。 或者
      > 1. 标签包含已移动的子项。


读取内容节点的`cq:tags`属性涉及以下分辨率：

1. 如果`/content/cq:tags`下没有匹配项，则不返回标记。
1. 如果标记设置了`cq:movedTo`属性，则引用的标记ID将随后显示。
   * 只要后面的标签具有`cq:movedTo`属性，就重复此步骤。
1. 如果后面的标记没有`cq:movedTo`属性，则读取标记。

要在标记被移动或合并时发布更改，必须复制`cq:Tag`节点及其所有反向链接。 在标记管理控制台中激活标记时，系统会自动执行此操作。

稍后对页面`cq:tags`属性的更新会自动清除旧引用。 这是由于通过API解析移动的标记会返回目标标记，从而提供目标标记ID而触发的。
