---
title: 在 AEM 应用程序中生成标记
description: 以程式設計方式使用自訂AEM應用程式中的標籤或擴展標籤
exl-id: a106dce1-5d51-406a-a563-4dea83987343
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 1%

---

# 在 AEM 应用程序中生成标记 {#building-tagging-into-aem-applications}

為了以程式設計方式使用自訂AEM應用程式內的標籤或擴展標籤，本檔案將說明如何使用

* [標籤API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

會與

* [標籤框架](tagging-framework.md)

有關標籤的相關資訊：

* 另請參閱 [使用標籤](/help/sites-cloud/authoring/features/tags.md) 有關將內容標籤為內容作者的資訊。
* 請參閱管理標籤，以取得管理員對於建立和管理標籤以及已對哪些內容套用的觀點。

## 標籤API概觀 {#overview-of-the-tagging-api}

實作 [標籤框架](tagging-framework.md) AEM允許使用JCR API管理標籤和標籤內容。 `TagManager` 確保標籤輸入為 `cq:tags` 字串陣列屬性不會重複，它會移除 `TagID`指向不存在的標籤和更新的 `TagID`s代表移動或合併的標籤。 `TagManager` 會使用JCR觀察接聽程式來回覆任何不正確的變更。 主要類別位於 [com.day.cq.tagg](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html) 封裝：

* `JcrTagManagerFactory`  — 傳回JCR型實作 `TagManager`. 這是標籤API的參考實作。
* `TagManager`  — 允許依照路徑和名稱解析和建立標籤。
* `Tag`  — 定義標籤物件。

### 取得以JCR為基礎的標籤管理員 {#getting-a-jcr-based-tagmanager}

擷取 `TagManager` 執行個體，您必須有JCR `Session` 和以呼叫 `getTagManager(Session)`：

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在一般Sling情境中，您也可以適應 `TagManager` 從 `ResourceResolver`：

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 擷取標籤物件 {#retrieving-a-tag-object}

A `Tag` 可透過 `TagManager`，解析現有標籤或建立新標籤：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

對於以JCR為基礎的實作，其會 `Tags` 至JCR `Nodes`，您可以直接使用Sling `adaptTo` 機制(如果您有資源，例如 `/content/cq:tags/default/my/tag`)：

```java
Tag tag = resource.adaptTo(Tag.class);
```

雖然標籤只能轉換 *從* 資源（不是節點），標籤可以轉換 *至* 節點和資源：

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>直接改寫自 `Node` 至 `Tag` 不可能，因為 `Node` 不實作Sling `Adaptable.adaptTo(Class)` 方法。

### 取得和設定標籤 {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### 搜尋標籤 {#searching-for-tags}

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

### 刪除標籤 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 複製標籤 {#replicating-tags}

可以使用復寫服務(`Replicator`)與標籤，因為標籤的型別為 `nt:hierarchyNode`：

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 標籤記憶體回收器 {#the-tag-garbage-collector}

標籤垃圾回收程式是一項背景服務，可清除隱藏和未使用的標籤。 隱藏和未使用的標籤是底下的標籤 `/content/cq:tags` 具有 `cq:movedTo` 屬性和，而不是在內容節點上使用。 它們的計數為零。 藉由使用此延遲刪除程式，內容節點(即 `cq:tags` 屬性)，不必隨著移動或合併作業進行更新。 中的參照 `cq:tags` 屬性會在以下情況時自動更新： `cq:tags` 屬性會更新，例如，透過頁面屬性對話方塊。

標籤記憶體回收行程預設為每天執行一次。 這可以在以下位置設定：

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## 標籤搜尋和標籤清單 {#tag-search-and-tag-listing}

搜尋標籤和標籤清單的運作方式如下：

* 搜尋 `TagID` 搜尋具有屬性的標籤 `cq:movedTo` 設定為 `TagID` 並遵循 `cq:movedTo` `TagID`s.
* 搜尋標籤標題只會搜尋沒有欄位的標籤。 `cq:movedTo` 屬性。

## 不同語言的標籤 {#tags-in-different-languages}

標籤 `title` 能以不同語言定義。 然後，語言敏感屬性會新增至標籤節點。 此屬性的格式為 `jcr:title.<locale>`例如， `jcr:title.fr` 法文翻譯版。 `<locale>` 必須為小寫ISO地區設定字串，並使用底線(`_`)而非連字型大小/破折號(`-`)，例如： `de_ch`.

例如，當 **動物** 標籤已新增至 **產品** 頁面，值 `stockphotography:animals` 已新增至屬性 `cq:tags` 節點的 `/content/wknd/en/products/jcr:content`. 已從標籤節點參考翻譯。

伺服器端API已本地化 `title`相關方法：

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

在AEM中，可以從頁面語言或使用者語言取得語言。

對於標籤，本地化視上下文為標籤而定 `titles` 能以頁面語言、使用者語言或任何其他語言顯示。

### 新增語言至編輯標籤對話方塊 {#adding-a-new-language-to-the-edit-tag-dialog}

下列程式說明如何將新語言（例如，芬蘭語）新增至 **標籤編輯** 對話方塊：

1. 在 **CRXDE**，編輯多值屬性 `languages` 節點的 `/content/cq:tags`.
1. 新增 `fi_fi`，代表芬蘭語言環境，並儲存變更。

現在可以在頁面屬性的標籤對話方塊和 **編輯標籤** 對話方塊 **標籤** 主控台。

>[!NOTE]
>
>新語言必須是AEM認可的語言之一，也就是說，它必須可作為以下節點提供 `/libs/wcm/core/resources/languages`.
