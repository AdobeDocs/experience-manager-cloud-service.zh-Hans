---
title: AEM 标记框架
description: 标记内容，并使用AEM标记基础架构对其进行分类和整理。
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 0%

---

# AEM标记框架 {#aem-tagging-framework}

标记允许对内容进行分类和整理。 标记可以按命名空间和分类法进行分类。 有关使用标记的详细信息：

* 参见 [使用标记](/help/sites-cloud/authoring/features/tags.md) 有关将内容标记为内容作者的信息。
* 有关创建和管理标记以及已对哪些内容应用标记的信息，请参阅管理标记，这是管理员的视角。

本文重点介绍支持AEM中标记的基础框架以及如何作为开发人员使用它。

## 简介 {#introduction}

要标记内容并使用AEM标记基础结构，请执行以下操作：

* 标记必须作为类型的节点存在 [`cq:Tag`](#cq-tag-node-type) 在 [分类根节点。](#taxonomy-root-node)
* 标记的内容节点的 `NodeType` 必须包括 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin。
* 此 [`TagID`](#tagid) 添加到内容节点的 [`cq:tags`](#cq-tags-property) 属性并解析为类型的节点 [`cq:Tag`.](#cq-tag-node-type)

## cq：Tag节点类型 {#cq-tag-node-type}

标记声明在存储库中捕获的节点类型为 `cq:Tag.`

* 标记可以是一个简单的单词(例如， `sky`)或表示分层分类(例如， `fruit/apple`即普通水果和更具体的苹果)。
* 标记由唯一的 `TagID`.
* 标记具有可选的中继信息，例如标题、本地化的标题和描述。 标题应显示在用户界面中，而不是 `TagID`，如果存在。

标记框架还提供了将作者和网站访客限制为仅使用特定的预定义标记的功能。

### 标记特征 {#tag-characteristics}

* 节点类型为 `cq:Tag`.
* 节点名称是 [`TagID`.](#tagid)
* 此 [`TagID`](#tagid) 始终包括 [命名空间。](#tag-namespace)
* 此 `jcr:title` 属性（UI中显示的标题）是可选的。
* 此 `jcr:description` 属性是可选的。
* 当包含子节点时，称为 [容器标记。](#container-tags)
* 标记存储在存储库中名为的基本路径的下方 [分类根节点。](#taxonomy-root-node)

### 标记 ID {#tagid}

A `TagID` 标识解析为存储库中标记节点的路径。

通常， `TagID` 是一个缩写 `TagID` 以命名空间开头，也可以是绝对的 `TagID` 从 [分类根节点。](#taxonomy-root-node)

标记内容时，如果内容尚不存在，则 [`cq:tags`](#cq-tags-property) 属性将添加到内容节点，并且 `TagID` 添加到属性的 `String` 数组值。

此 `TagID` 包含 [命名空间](#tag-namespace) 随后是本地 `TagID`. [容器标记](#container-tags) 具有表示分类法中层次结构顺序的子标记。 子标记可用于引用与任何本地标记相同的标记 `TagID`. 例如，使用标记内容 `fruit` 允许，即使它是带有子标记的容器标记也是如此，例如 `fruit/apple` 和 `fruit/banana`.

### 分类根节点 {#taxonomy-root-node}

分类根节点是存储库中所有标记的基本路径。 分类根节点必须 *非* 为类型的节点 `cq:Tag`.

在AEM中，基本路径为 `/content/cq:tags` 并且根节点的类型为 `cq:Folder`.

### 标记命名空间 {#tag-namespace}

命名空间允许对事物进行分组。 最典型的使用案例是每个站点或大型应用程序（例如，Sites或Assets）都有一个命名空间（例如公共与内部），但命名空间可用于各种其他需求。 命名空间在用户界面中用于仅显示适用于当前内容的标记（即特定命名空间的标记）的子集。

标记的命名空间是分类子树中的第一级，即紧接在 [分类根节点。](#taxonomy-root-node) 命名空间是类型的节点 `cq:Tag` 其父项不是 `cq:Tag` 节点类型。

所有标记都有一个命名空间。 如果未指定命名空间，则会将标记分配给默认命名空间，即 `TagID` `default`，即 `/content/cq:tags/default`.  标题默认为 `Standard Tags`在这种情况下。

### 容器标记 {#container-tags}

容器标记是类型的节点 `cq:Tag` 包含任意数量和类型的子节点，这使得使用自定义元数据增强标记模型成为可能。

此外，分类法中的容器标记（或超级标记）充当所有子标记的子总和：例如，使用标记的内容 `fruit/apple` 被视为已标记 `fruit` 此外，即搜索刚刚使用标记的内容 `fruit` 也会找到带有以下标记的内容： `fruit/apple`.

### 解析标记ID {#resolving-tagids}

如果标记ID包含冒号(`:`)，则冒号会将命名空间与标记或子分类分开，然后使用普通斜杠(`/`)。 如果标记ID没有冒号，则隐含默认命名空间。

下面是标记的标准位置（且是唯一位置） `/content/cq:tags`.

引用不存在的路径或不指向的路径的标记 `cq:Tag` 节点被视为无效，将被忽略。

下表显示了一些示例 `TagID`s、其元素，以及 `TagID` 解析为存储库中的绝对路径：

| `TagID` | 命名空间 | 本地Id | 容器标记 | 叶标记 | 存储库绝对标记路径 |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (无) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (无) | (无) | (无) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### 标记标题本地化 {#localization-of-tag-title}

当标记包含可选标题字符串时 `jcr:title`，可以通过添加属性来本地化要显示的标题 `jcr:title.<locale>`.

有关更多详细信息，请参阅：

* [不同语言的标签，](tagging-applications.md#tags-in-different-languages) 其中描述如何作为开发人员使用API
* 管理不同语言的标记，其中介绍了如何以管理员身份使用“标记”控制台

### 访问控制 {#access-control}

标记作为节点存在于下的存储库中 [分类根节点。](#taxonomy-root-node) 通过在存储库中设置适当的ACL，可以允许或拒绝作者和网站访客在给定的命名空间中创建标记。

拒绝某些标记或命名空间的读取权限将控制将标记应用于特定内容的能力。

典型做法包括：

* 允许 `tag-administrators` 对所有命名空间的组/角色写入权限(添加/修改 `/content/cq:tags`)。 此组提供开箱即用的AEM。
* 允许用户/作者读取他们应该可以读取的所有命名空间（大多数是所有命名空间）。
* 允许用户/作者写入对标记应由用户/作者自由定义的命名空间的访问权限(`add_node` 下 `/content/cq:tags/some_namespace`)

## 可标记内容：cq：Taggable Mixin {#taggable-content-cq-taggable-mixin}

为了使应用程序开发人员将标记附加到内容类型，节点的注册([CND](https://jackrabbit.apache.org/node-type-notation.html))必须包括 `cq:Taggable` mixin或 `cq:OwnerTaggable` mixin。

此 `cq:OwnerTaggable` mixin，继承自 `cq:Taggable`，用于指示内容可以按所有者/作者进行分类。 在AEM中，它只是 `cq:PageContent` 节点。 此 `cq:OwnerTaggable` 标记框架不需要mixin。

>[!NOTE]
>
>建议仅在聚合内容项目的顶级节点（或在其上）启用标记 `jcr:content` 节点)。 示例包括：
>
>* 页面(`cq:Page`)，其中 `jcr:content`节点属于类型 `cq:PageContent`，其中包括 `cq:Taggable` mixin。
>* 资产(`cq:Asset`)，其中 `jcr:content/metadata` 节点始终具有 `cq:Taggable` mixin。

### 节点类型表示法(CND) {#node-type-notation-cnd}

节点类型定义作为CND文件存在于存储库中。 CND表示法被定义为 [JCR文档。](https://jackrabbit.apache.org/node-type-notation.html).

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

此 `cq:tags` 属性是 `String` 用于存储一个或多个的数组 `TagID`当作者或网站访客将它们应用于内容时。 仅当添加到使用定义的节点时，属性才有意义 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin。

>[!NOTE]
>
>要使用AEM标记功能，自定义开发的应用程序不应定义以外的标记属性 `cq:tags`.

## 移动和合并标记 {#moving-and-merging-tags}

下面说明了使用“标记”控制台移动或合并标记时在存储库中产生的效果。

将标记A移动或合并到标记B中时 `/content/cq:tags`：

* 标记A未删除并接收 `cq:movedTo` 属性。
   * `cq:movedTo` 指向标记B。
   * 此属性表示标记A已移动或合并到标记B中。
   * 移动标记B将相应地更新此属性。
   * 标记A因此而隐藏，并且仅保留在存储库中以解决指向标记A的内容节点中的标记ID。
   * 标记垃圾收集器会删除标记A等标记，内容节点不再指向这些标记。
   * 的特殊值 `cq:movedTo` 属性为 `nirvana`，此变量在删除标记时应用，但无法从存储库中删除，因为存在带有标记的子标记 `cq:movedTo` 必须保留下来。
     >[!NOTE]
     >
     >此 `cq:movedTo` 仅当满足以下任一条件时，属性才会添加到已移动或已合并的标记中：
     >
     > 1. 标记在内容中使用（这意味着它包含引用）。 或
     > 1. 标记具有已移动的子项。
     >
* 创建标记B（如果移动）并接收 `cq:backlinks` 属性。
   * `cq:backlinks` 保持对另一方向的引用，即保留已移动到标记B或与标记B合并的所有标记的列表。
   * 这通常需要保留 `cq:movedTo` 属性是标记B移动/合并/删除或标记B激活时的最新属性，在这种情况下，还必须激活其所有反向链接标记。
     >[!NOTE]
     >
     >此 `cq:backlinks` 仅当满足以下任一条件时，属性才会添加到已移动或已合并的标记中：
     >
     > 1. 标记在内容中使用（这意味着它包含引用）。 或
     > 1. 标记具有已移动的子项。

阅读 `cq:tags` 内容节点的属性涉及以下分辨率：

1. 如果下没有匹配项 `/content/cq:tags`，则不会返回任何标记。
1. 如果标记具有 `cq:movedTo` 属性集内，将后跟引用的标记ID。
   * 只要以下标记具有 `cq:movedTo` 属性。
1. 如果后跟标记不包含 `cq:movedTo` 属性，则读取标记。

要在移动或合并标记后发布更改，请 `cq:Tag` 必须复制节点及其所有反向链接。 当在标记管理控制台中激活标记时，会自动完成此操作。

稍后对页面的 `cq:tags` 属性自动清理旧引用。 由于通过API解析移动的标记会返回目标标记，从而提供目标标记ID，因此会触发此事件。
