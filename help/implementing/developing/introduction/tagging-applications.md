---
title: 将标记构建到AEM应用程序
description: 在自定义AEM应用程序中以编程方式使用标签或扩展标签
translation-type: tm+mt
source-git-commit: 6b754a866be7979984d613b95a6137104be05399
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---


# 将标记构建到AEM应用程序{#building-tagging-into-aem-applications}

为了在自定义AEM应用程序中以编程方式使用标签或扩展标签，本文档描述了

* [标记API](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/tagging/package-summary.html)

与

* [标记框架](tagging-framework.md)

有关标记的相关信息：

* 有关将内容标记为内容作者的信息，请参阅[使用标记](/help/sites-cloud/authoring/features/tags.md)。
* 有关创建和管理标记以及已应用哪些内容标记的管理员观点，请参阅管理标记。

## Tagging API {#overview-of-the-tagging-api}概述

在AEM中实现[标记框架](tagging-framework.md)允许使用JCR API管理标记和标记内容。 `TagManager` 确保在string array属性中作为值输 `cq:tags` 入的标记不会重复，它会删 `TagID`除指向非现有标记的标记，并更 `TagID`新已移动或合并的标记。`TagManager` 使用JCR观察侦听器，它还原任何不正确的更改。主类位于[com.day.cq.taging](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/tagging/package-summary.html)包中：

* `JcrTagManagerFactory`  — 返回基于JCR的实 `TagManager`施它是Tagging API的参考实现。
* `TagManager`  — 允许按路径和名称解析和创建标记。
* `Tag`  — 定义标记对象。

### 获取基于JCR的TagManager {#getting-a-jcr-based-tagmanager}

要检索`TagManager`实例，您需要JCR `Session`并调用`getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在典型的Sling上下文中，您还可以根据`ResourceResolver`调整`TagManager`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 检索Tag对象{#retrieving-a-tag-object}

可通过`TagManager`检索`Tag`，方法是解析现有标记或创建新标记：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

对于基于JCR的实现（将`Tags`映射到JCR `Nodes`），如果您有资源（例如`/content/cq:tags/default/my/tag`），则可以直接使用Sling的`adaptTo`机制：

```java
Tag tag = resource.adaptTo(Tag.class);
```

虽然标记只能从&#x200B;*资源（而非节点）转换*，但标记可以将&#x200B;*转换为*&#x200B;节点和资源：

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>无法直接从`Node`调整为`Tag`，因为`Node`不实现Sling `Adaptable.adaptTo(Class)`方法。

### 获取和设置标记{#getting-and-setting-tags}

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
>要使用的有效`RangeIterator`为：
>
>`com.day.cq.commons.RangeIterator`

### 删除标记 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 复制标记{#replicating-tags}

可以将复制服务(`Replicator`)与标记一起使用，因为标记类型为`nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 标记垃圾收集器{#the-tag-garbage-collector}

标记垃圾收集器是一种后台服务，用于清理隐藏和未使用的标记。 隐藏和未使用的标记是`/content/cq:tags`下面的标记，具有`cq:movedTo`属性，不在内容节点上使用。 他们的数为零。 通过使用此延迟删除过程，内容节点（即`cq:tags`属性）不必作为移动或合并操作的一部分进行更新。 在更新`cq:tags`属性时，`cq:tags`属性中的引用会自动更新，例如，通过页面属性对话框。

标记垃圾收集器默认每天运行一次。 可在以下位置进行配置：

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## 标记搜索和标记列表{#tag-search-and-tag-listing}

搜索标记和标记列表的工作方式如下：

* 搜索`TagID`将属性`cq:movedTo`设置为`TagID`并随后搜索`cq:movedTo` `TagID`的标签。
* 搜索标记标题仅搜索没有`cq:movedTo`属性的标记。

## 不同语言的标签{#tags-in-different-languages}

标记`title`可以用不同语言定义。 然后，语言相关属性被添加到标记节点。 此属性的格式为`jcr:title.<locale>`，例如`jcr:title.fr`表示法语翻译。 `<locale>` 必须为小写ISO区域设置字符串，并使`_`用下划线()代替连字`-`符/短划线()，例如： `de_ch`.

例如，将&#x200B;**Animals**&#x200B;标记添加到&#x200B;**Products**&#x200B;页面时，值`stockphotography:animals`将添加到节点`/content/wknd/en/products/jcr:content`的属性`cq:tags`中。 转换从标记节点引用。

服务器端API已本地化`title`相关方法：

* [`com.day.cq.tagging.Tag`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths()`
   * `getLocalizedTitles()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

在AEM中，可以从页面语言或用户语言获取语言。

对于标记，本地化取决于上下文，因为标记`titles`可以以页面语言、用户语言或任何其他语言显示。

### 将新语言添加到“编辑标记”对话框{#adding-a-new-language-to-the-edit-tag-dialog}

以下过程介绍如何向&#x200B;**标记编辑**&#x200B;对话框添加新语言（如芬兰语）：

1. 在&#x200B;**CRXDE**&#x200B;中，编辑节点`/content/cq:tags`的多值属性`languages`。
1. 添加`fi_fi`（表示芬兰语区域设置）并保存更改。

现在，在&#x200B;**标记**&#x200B;控制台中编辑标记时，页面属性的标记对话框和&#x200B;**编辑标记**&#x200B;对话框中均提供芬兰语。

>[!NOTE]
>
>新语言必须是AEM认可的语言之一，即它必须作为`/libs/wcm/core/resources/languages`以下的节点可用。
