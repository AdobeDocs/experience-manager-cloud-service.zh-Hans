---
title: 在 AEM 应用程序中生成标记
description: 以编程方式在自定义AEM应用程序中使用标记或扩展标记
exl-id: a106dce1-5d51-406a-a563-4dea83987343
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---

# 在 AEM 应用程序中生成标记 {#building-tagging-into-aem-applications}

为了以编程方式在自定义AEM应用程序中使用标记或扩展标记，本文档介绍了

* [标记API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

与

* [标记框架](tagging-framework.md)

有关标记的相关信息：

* 请参阅 [使用标记](/help/sites-cloud/authoring/features/tags.md) 有关将内容标记为内容作者的信息。
* 请参阅管理标记，以了解有关创建和管理标记以及已对哪些内容应用标记的管理员观点。

## 标记API概述 {#overview-of-the-tagging-api}

实施 [标记框架](tagging-framework.md) 在AEM中，允许使用JCR API管理标记和标记内容。 `TagManager` 确保在 `cq:tags` 字符串数组属性不重复，会删除 `TagID`指向不存在的标记和更新 `TagID`用于已移动或合并的标记。 `TagManager` 使用JCR观察侦听器，它会还原任何不正确的更改。 主类位于 [com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html) 包：

* `JcrTagManagerFactory`  — 返回基于JCR的 `TagManager`. 它是标记API的参考实施。
* `TagManager`  — 允许按路径和名称解析和创建标记。
* `Tag`  — 定义标记对象。

### 获取基于JCR的TagManager {#getting-a-jcr-based-tagmanager}

检索 `TagManager` 实例，您需要具有JCR `Session` 和 `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在典型的Sling上下文中，您还可以根据 `TagManager` 从 `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 检索标记对象 {#retrieving-a-tag-object}

A `Tag` 可通过 `TagManager`，方法是解析现有标记或创建新标记：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

对于基于JCR的实施，该实施映射 `Tags` 到JCR `Nodes`，您可以直接使用 `adaptTo` 机制(例如， `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

而标记只能被转换 *从* 资源（非节点）、标记可以转换 *to* 节点和资源：

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>直接从 `Node` to `Tag` 不可能，因为 `Node` 不实施Sling `Adaptable.adaptTo(Class)` 方法。

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
>有效 `RangeIterator` 要使用，请执行以下操作：
>
>`com.day.cq.commons.RangeIterator`

### 删除标记 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 复制标记 {#replicating-tags}

可以使用复制服务(`Replicator`)，因为标记的类型为 `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 标记垃圾收集器 {#the-tag-garbage-collector}

标记垃圾回收器是一项后台服务，可清理隐藏和未使用的标记。 隐藏和未使用的标记如下所示 `/content/cq:tags` 具有 `cq:movedTo` 属性和中，不会在内容节点上使用。 他们的数为零。 通过使用此延迟删除过程，内容节点(即 `cq:tags` 属性)，则无需在移动或合并操作中进行更新。 中的引用 `cq:tags` 属性会在 `cq:tags` 属性会进行更新，例如通过页面属性对话框。

标记垃圾收集器默认每天运行一次。 可在以下位置进行配置：

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## 标记搜索和标记列表 {#tag-search-and-tag-listing}

搜索标记和标记列表的工作方式如下：

* 搜索 `TagID` 搜索具有属性的标记 `cq:movedTo` 设置为 `TagID` 并遵循 `cq:movedTo` `TagID`s.
* 搜索标记标题仅会搜索没有 `cq:movedTo` 属性。

## 不同语言的标记 {#tags-in-different-languages}

标记 `title` 可以定义不同语言。 然后，会将语言敏感属性添加到标记节点。 此属性的格式 `jcr:title.<locale>`，例如 `jcr:title.fr` 翻译法文。 `<locale>` 必须是小写的ISO区域设置字符串，并使用下划线(`_`)，而不是连字符/短划线(`-`)，例如： `de_ch`.

例如，当 **动物** 标记会添加到 **产品** 页面，值 `stockphotography:animals` 会添加到资产中 `cq:tags` 的 `/content/wknd/en/products/jcr:content`. 转换从标记节点引用。

服务器端API已本地化 `title`-related方法：

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

对于标记，本地化取决于作为标记的上下文 `titles` 可以以页面语言、用户语言或任何其他语言显示。

### 向“编辑标记”对话框添加新语言 {#adding-a-new-language-to-the-edit-tag-dialog}

以下过程介绍如何向 **标记编辑** 对话框：

1. 在 **CRXDE**，编辑多值属性 `languages` 的 `/content/cq:tags`.
1. 添加 `fi_fi`，表示芬兰语区域设置并保存更改。

现在，芬兰语可在页面属性的标记对话框和 **编辑标记** 对话框中编辑标记时 **标记** 控制台。

>[!NOTE]
>
>新语言必须是AEM认可的语言之一，即需要作为下面的节点提供 `/libs/wcm/core/resources/languages`.
