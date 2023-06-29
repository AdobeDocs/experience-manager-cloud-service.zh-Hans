---
title: 在 AEM 应用程序中生成标记
description: 以编程方式使用自定义AEM应用程序中的标记或扩展标记
exl-id: a106dce1-5d51-406a-a563-4dea83987343
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 1%

---

# 在 AEM 应用程序中生成标记 {#building-tagging-into-aem-applications}

为了以编程方式使用自定义AEM应用程序中的标记或扩展标记，本文档介绍了如何使用

* [标记API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

会与

* [标记框架](tagging-framework.md)

有关标记的相关信息：

* 参见 [使用标记](/help/sites-cloud/authoring/features/tags.md) 有关将内容标记为内容作者的信息。
* 有关创建和管理标记以及已对哪些内容应用标记的信息，请参阅管理标记，这是管理员的视角。

## 标记API概述 {#overview-of-the-tagging-api}

实施 [标记框架](tagging-framework.md) 在AEM中，允许使用JCR API管理标记和标记内容。 `TagManager` 确保在 `cq:tags` 字符串数组属性不重复，它将删除 `TagID`s指向不存在的标记和更新 `TagID`s表示移动或合并的标记。 `TagManager` 使用JCR观察侦听器来还原任何不正确的更改。 主类位于 [com.day.cq.tagg](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html) 包：

* `JcrTagManagerFactory`  — 返回基于JCR的 `TagManager`. 它是标记API的参考实施。
* `TagManager`  — 允许按路径和名称解析和创建标记。
* `Tag`  — 定义标记对象。

### 获取基于JCR的TagManager {#getting-a-jcr-based-tagmanager}

检索 `TagManager` 实例，您需要拥有JCR `Session` 并调用 `getTagManager(Session)`：

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在典型的Sling上下文中，您还可以适应 `TagManager` 从 `ResourceResolver`：

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 检索标记对象 {#retrieving-a-tag-object}

A `Tag` 可通过 `TagManager`，通过解析现有标记或创建新标记：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

对于基于JCR的实施，其映射了 `Tags` 转到JCR `Nodes`，您可以直接使用Sling `adaptTo` 机制(如果您有资源，例如 `/content/cq:tags/default/my/tag`)：

```java
Tag tag = resource.adaptTo(Tag.class);
```

虽然只能转换标记 *起始日期* 资源（不是节点），标记可以转换 *到* 节点和资源：

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>直接从 `Node` 到 `Tag` 不可能，因为 `Node` 不实施Sling `Adaptable.adaptTo(Class)` 方法。

### 获取和设置标记 {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### 搜索标记 {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>有效 `RangeIterator` 要使用的是：
>
>`com.day.cq.commons.RangeIterator`

### 删除标记 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 复制标记 {#replicating-tags}

可以使用复制服务(`Replicator`)，因为标记的类型为 `nt:hierarchyNode`：

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 标记垃圾收集器 {#the-tag-garbage-collector}

标记垃圾收集器是一种后台服务，用于清理隐藏和未使用的标记。 隐藏和未使用的标记是以下标记 `/content/cq:tags` 具有 `cq:movedTo` 属性和，而不是在内容节点上使用。 他们数为零。 通过这种延迟删除过程，内容节点(即 `cq:tags` 属性)不必作为移动或合并操作的一部分进行更新。 中的引用 `cq:tags` 属性在以下情况下自动更新： `cq:tags` 例如，通过页面属性对话框更新属性。

默认情况下，标记垃圾回收器每天运行一次。 这可以在以下位置配置：

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## 标记搜索和标记列表 {#tag-search-and-tag-listing}

搜索标记和标记列表的工作方式如下：

* 搜索 `TagID` 搜索具有属性的标记 `cq:movedTo` 设置为 `TagID` 并遵循 `cq:movedTo` `TagID`s.
* 搜索标记标题只会搜索没有的标记 `cq:movedTo` 属性。

## 不同语言的标记 {#tags-in-different-languages}

标记 `title` 可以通过不同的语言进行定义。 然后，将区分语言的属性添加到标记节点。 此属性的格式为 `jcr:title.<locale>`例如， `jcr:title.fr` 法文版的。 `<locale>` 必须为小写ISO区域设置字符串并使用下划线(`_`)而不是连字符/短划线(`-`)，例如： `de_ch`.

例如，当 **动物** 标记将添加到 **产品** 页面，值 `stockphotography:animals` 添加到属性 `cq:tags` 节点的 `/content/wknd/en/products/jcr:content`. 从标记节点引用翻译。

服务器端API已本地化 `title`相关方法：

* [`com.day.cq.tagging.Tag`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths()`
   * `getLocalizedTitles()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

在AEM中，可以从页面语言或用户语言获取语言。

对于标记，本地化取决于作为标记的上下文 `titles` 能够以页面语言、用户语言或任何其他语言显示。

### 向“编辑标记”对话框添加新语言 {#adding-a-new-language-to-the-edit-tag-dialog}

以下过程介绍了如何向添加新语言（例如，芬兰语） **标记编辑** 对话框：

1. In **CRXDE**，编辑多值属性 `languages` 节点的 `/content/cq:tags`.
1. 添加 `fi_fi`，表示芬兰语区域设置，并保存更改。

芬兰语现在可以在页面属性的标记对话框中以及 **编辑标记** 对话框 **标记** 控制台。

>[!NOTE]
>
>新语言需要是AEM认可的语言之一，也就是说，它需要作为以下节点提供 `/libs/wcm/core/resources/languages`.
