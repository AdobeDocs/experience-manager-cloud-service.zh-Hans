---
title: AEM 标记框架
description: 标记内容，并使用AEM标记基础架构对其进行分类和整理。
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 0%

---

# AEM标记框架 {#aem-tagging-framework}

标记允许对内容进行分类和组织。 标记可以按命名空间和分类法进行分类。 有关使用标记的详细信息：

* 有关将内容标记为内容作者的信息，请参阅[使用标记](/help/sites-cloud/authoring/sites-console/tags.md)。
* 有关创建和管理标记以及已对哪些内容应用标记的信息，请参阅管理标记。

本文重点介绍支持AEM中标记的基础框架以及如何作为开发人员使用它。

## 简介 {#introduction}

要标记内容并使用AEM标记基础架构，请执行以下操作：

* 标记必须作为类型[`cq:Tag`](#cq-tag-node-type)的节点存在于[分类根节点下。](#taxonomy-root-node)
* 标记的内容节点的`NodeType`必须包含[`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin。
* [`TagID`](#tagid)已添加到内容节点的[`cq:tags`](#cq-tags-property)属性，并解析为类型为[`cq:Tag`.](#cq-tag-node-type)的节点

## cq：Tag节点类型 {#cq-tag-node-type}

标记声明在类型为`cq:Tag.`的节点的存储库中捕获

* 标记可以是一个简单的单词（例如，`sky`），也可以表示层次分类（例如，`fruit/apple`，表示通用水果和更具体的苹果）。
* 标记由唯一的`TagID`标识。
* 标记具有可选的中继信息，例如标题、本地化的标题和描述。 标题应显示在用户界面中，而不是`TagID`中（如果存在）。

标记框架还限制作者和网站访客仅使用特定的预定义标记。

### 标记特征 {#tag-characteristics}

* 节点类型为`cq:Tag`。
* 节点名称是[`TagID`.](#tagid)的组件
* [`TagID`](#tagid)始终包含[命名空间。](#tag-namespace)
* `jcr:title`属性（UI中显示的标题）是可选的。
* `jcr:description`属性是可选的。
* 包含子节点时，称为[容器标记。](#container-tags)
* 标记存储在名为[分类根节点的基本路径下的存储库中。](#taxonomy-root-node)

### 标记 ID {#tagid}

`TagID`标识解析为存储库中标记节点的路径。

通常，`TagID`是以命名空间开头的简写`TagID`，或者可以是从[分类根节点开始的绝对`TagID`。](#taxonomy-root-node)

当标记内容时，如果内容尚不存在，[`cq:tags`](#cq-tags-property)属性将添加到内容节点，而`TagID`将添加到属性的`String`数组值。

`TagID`包含一个[命名空间](#tag-namespace)，后跟本地`TagID`。 [容器标记](#container-tags)具有表示分类中层次结构顺序的子标记。 子标记可用于引用与任何本地`TagID`相同的标记。 例如，允许使用`fruit`标记内容，即使它是一个具有子标记的容器标记，如`fruit/apple`和`fruit/banana`。

### 分类根节点 {#taxonomy-root-node}

分类根节点是存储库中所有标记的基本路径。 分类根节点必须&#x200B;*不是*&#x200B;是`cq:Tag`类型的节点。

在AEM中，基路径为`/content/cq:tags`，根节点的类型为`cq:Folder`。

### 标记命名空间 {#tag-namespace}

命名空间允许您对事物进行分组。 最典型的用例是每个站点或大型应用程序(例如，Sites或Assets)都有一个命名空间（例如，公共与内部），但命名空间可用于各种其他需求。 命名空间在用户界面中用于仅显示适用于当前内容的标记（即特定命名空间的标记）的子集。

标记的命名空间是分类子树中的第一个级别，它是[分类根节点正下方的节点。](#taxonomy-root-node)命名空间是`cq:Tag`类型的节点，其父项不是`cq:Tag`节点类型。

所有标记都具有命名空间。 如果未指定命名空间，则将标记分配给默认命名空间`TagID` `default`，即`/content/cq:tags/default`。 在这种情况下，标题默认为`Standard Tags`。

### 容器标记 {#container-tags}

容器标记是`cq:Tag`类型的节点，包含任意数量的子节点和子节点类型，因此可以使用自定义元数据增强标记模型。

此外，分类法中的容器标记（或超级标记）充当所有子标记的汇总。 例如，使用`fruit/apple`标记的内容也被视为使用`fruit`标记。 也就是说，搜索标记为`fruit`的内容也会找到标记为`fruit/apple`的内容。

### 解析标记ID {#resolving-tagids}

如果标记ID包含冒号(`:`)，则冒号会将命名空间与标记或子分类分开，然后使用普通斜杠(`/`)分隔它们。 如果标记ID不含冒号，则默认为默认命名空间。

标记的标准且唯一位置低于`/content/cq:tags`。

引用不存在的路径或不指向`cq:Tag`节点的路径的标记被视为无效并被忽略。

下表显示了一些示例`TagID`、其元素以及`TagID`如何解析为存储库中的绝对路径：

| `TagID` | 命名空间 | 本地Id | 容器标记 | 叶标记 | 存储库绝对标记路径 |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`，`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | （无） | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | （无） | （无） | （无） | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### 标记标题本地化 {#localization-of-tag-title}

当标记包含可选标题字符串`jcr:title`时，可以通过添加属性`jcr:title.<locale>`来本地化要显示的标题。

有关更多详细信息，请参阅以下内容：

* 不同语言的[标记](tagging-applications.md#tags-in-different-languages)描述作为开发人员使用API
* 管理不同语言的标记，这描述了以管理员身份使用“标记”控制台的情况

### 访问控制 {#access-control}

标记作为[分类根节点下的存储库中的节点存在。](#taxonomy-root-node)通过在存储库中设置适当的ACL，可以允许或拒绝作者和网站访客在给定命名空间中创建标记。

拒绝某些标记或命名空间的读取权限会控制将标记应用于特定内容的能力。

典型实践包括：

* 允许`tag-administrators`组/角色对所有命名空间的写入权限（在`/content/cq:tags`下添加/修改）。 此组提供开箱即用的AEM。
* 允许用户/作者读取对他们应可读取的所有命名空间（大多数是所有）的访问权限。
* 允许用户/作者写入对这些命名空间的访问权限，在这些命名空间中，标记应由用户/作者自由定义（`/content/cq:tags/some_namespace`下的`add_node`）

## 可标记的内容：cq：Taggable Mixin {#taggable-content-cq-taggable-mixin}

对于要将标记附加到内容类型的应用程序开发人员，节点的注册([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html))必须包含`cq:Taggable` mixin或`cq:OwnerTaggable` mixin。

继承自`cq:Taggable`的`cq:OwnerTaggable` mixin旨在指示内容可由所有者/作者分类。 在AEM中，它只是`cq:PageContent`节点的特性。 标记框架不需要`cq:OwnerTaggable` mixin。

>[!NOTE]
>
>建议仅在聚合内容项的顶级节点（或其`jcr:content`节点）上启用标记。 示例包括：
>
>* `jcr:content`节点为`cq:PageContent`类型的页面(`cq:Page`)，其中包括`cq:Taggable` mixin。
>* Assets (`cq:Asset`)，其中`jcr:content/metadata`节点始终具有`cq:Taggable` mixin。

### 节点类型表示法(CND) {#node-type-notation-cnd}

节点类型定义作为CND文件存在于存储库中。 CND表示法定义为[JCR文档](https://jackrabbit.apache.org/jcr/node-type-notation.html)的一部分。

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

## cq：tags属性 {#cq-tags-property}

`cq:tags`属性是一个`String`数组，用于在作者或网站访客将一个或多个属性应用于内容时存储这些属性。 `TagID`仅当添加到使用[`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin定义的节点时，属性才有意义。

>[!NOTE]
>
>要使用AEM标记功能，自定义开发的应用程序不应定义`cq:tags`以外的标记属性。

## 移动和合并标记 {#moving-and-merging-tags}

下面说明了使用“标记”控制台移动或合并标记时在存储库中产生的效果。

将标记A移动或合并到`/content/cq:tags`下的标记B中时：

* 标记A未删除并接收`cq:movedTo`属性。
   * `cq:movedTo`指向标记B。
   * 此属性表示标记A已移动或合并到标记B中。
   * 移动标记B会相应地更新此属性。
   * 因此，标记A是隐藏的，并且仅保留在存储库中，以便它解析指向标记A的内容节点中的标记ID。
   * 标记垃圾回收器会删除标记A之类的标记，内容节点不再指向这些标记。
   * `cq:movedTo`属性的特殊值为`nirvana`，该特殊值在删除标记时应用，但无法从存储库中删除，因为存在必须保留带有`cq:movedTo`的子标记。

     >[!NOTE]
     >
     >只有在满足以下任一条件时，`cq:movedTo`属性才会添加到移动或合并的标记中：
     >
     > 1. 标记在内容中使用（这意味着它有引用）。 OR
     > 1. 标记具有已移动的子项。
     >
* 已创建标记B（如果有移动）并接收`cq:backlinks`属性。
   * `cq:backlinks`将引用保留在另一个方向。 也就是说，它会保留已移至标记B或与标记B合并的所有标记的列表。
   * 在移动/合并/删除标记B或者激活标记B时（如果激活了标记B，则必须同时激活其所有反向链接标记），通常需要此功能才能使`cq:movedTo`属性保持最新。

     >[!NOTE]
     >
     >只有在满足以下任一条件时，`cq:backlinks`属性才会添加到移动或合并的标记中：
     >
     > 1. 标记用在内容中（这意味着它有引用），或
     > 1. 标记具有已移动的子项。

读取内容节点的`cq:tags`属性涉及以下分辨率：

1. 如果`/content/cq:tags`下没有匹配项，则不会返回任何标记。
1. 如果标记设置了`cq:movedTo`属性，则采用引用的标记ID。
   * 只要后续标记具有`cq:movedTo`属性，就重复此步骤。
1. 如果后续标记没有`cq:movedTo`属性，则读取该标记。

要在移动或合并标记时发布更改，必须复制`cq:Tag`节点及其所有反向链接。 当在标记管理控制台中激活标记时，将自动完成此复制。

以后更新页面的`cq:tags`属性会自动清除旧引用。 触发清理的原因是通过API解析移动的标记会返回目标标记，从而提供目标标记ID。
