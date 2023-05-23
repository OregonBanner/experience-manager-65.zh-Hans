---
title: 將標籤建置到AEM應用程式中
seo-title: Building Tagging into an AEM Application
description: 以程式設計方式使用自訂AEM應用程式中的標籤或擴展標籤
seo-description: Programmatically work with tags or extending tags within a custom AEM application
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
feature: Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---

# 將標籤建置到AEM應用程式中{#building-tagging-into-an-aem-application}

為了以程式設計方式使用自訂AEM應用程式內的標籤或擴展標籤，本頁面說明如何使用

* [標籤API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

會與

* [標籤框架](/help/sites-developing/framework.md)

如需關於標籤的相關資訊，請參閱：

* [管理標籤](/help/sites-administering/tags.md) 以取得關於建立和管理標籤以及已對哪些內容標籤套用的資訊。
* [使用標籤](/help/sites-authoring/tags.md) 以取得關於標籤內容的資訊。

## 標籤API概觀 {#overview-of-the-tagging-api}

實作 [標籤框架](/help/sites-developing/framework.md) AEM允許使用JCR API管理標籤和標籤內容。 TagManager會確保在 `cq:tags` 字串陣列屬性不會重複，它會移除指向非現有標籤的TagID，並更新已移動或合併標籤的標籤ID。 TagManager會使用JCR觀察接聽程式來回覆任何不正確的變更。 主要類別位於 [com.day.cq.tagg](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) 封裝：

* JcrTagManagerFactory — 傳回JCR型實作 `TagManager`. 這是標籤API的參考實作。
* `TagManager`  — 允許依照路徑和名稱解析和建立標籤。
* `Tag`  — 定義標籤物件。

### 取得以JCR為基礎的標籤管理員 {#getting-a-jcr-based-tagmanager}

若要擷取TagManager執行個體，您需要有JCR `Session` 和以呼叫 `getTagManager(Session)`：

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

雖然標籤只能從*資源（非節點）轉換*而來，但標籤可以轉換為*節點和資源：

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

可以使用復寫服務( `Replicator`)與標籤，因為標籤的型別為 `nt:hierarchyNode`：

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 在使用者端上標籤 {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` 是用於輸入標籤的表單Widget。 它有一個快顯功能表，可從現有標籤中選取，包括自動完成和許多其他功能。 其xtype為 `tags`.

## 標籤記憶體回收器 {#the-tag-garbage-collector}

標籤垃圾回收程式是一項背景服務，可清除隱藏和未使用的標籤。 隱藏和未使用的標籤是底下的標籤 `/content/cq:tags` 具有 `cq:movedTo` 屬性和，而不是在內容節點上使用 — 它們的計數為零。 藉由使用此延遲刪除程式，內容節點(即 `cq:tags` 屬性)，不必隨著移動或合併作業進行更新。 中的參照 `cq:tags` 屬性會在以下情況時自動更新： `cq:tags` 屬性已更新，例如透過頁面屬性對話方塊。

標籤記憶體回收行程預設為每天執行一次。 這可以在以下位置設定：

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 標籤搜尋和標籤清單 {#tag-search-and-tag-listing}

搜尋標籤和標籤清單的運作方式如下：

* 搜尋TagID會搜尋具有屬性的標籤 `cq:movedTo` 設定為TagID並遵循 `cq:movedTo` 標籤ID。

* 搜尋標籤Title只會搜尋沒有 `cq:movedTo` 屬性。

## 不同語言的標籤 {#tags-in-different-languages}

如管理標籤的檔案一節中所述 [管理不同語言的標籤](/help/sites-administering/tags.md#managing-tags-in-different-languages)，標籤 `title`能以不同語言定義。 然後，語言敏感屬性會新增至標籤節點。 此屬性的格式為 `jcr:title.<locale>`，例如 `jcr:title.fr` 法文翻譯版。 `<locale>` 必須為小寫ISO地區設定字串，並使用「_」而非「 — 」，例如： `de_ch`.

當 **動物** 標籤已新增至 **產品** 頁面，值 `stockphotography:animals` 已新增至屬性 `cq:tags` /content/geometrixx/en/products/jcr：content節點的 已從標籤節點參考翻譯。

伺服器端API已本地化 `title`相關方法：

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle（地區設定）
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle（地區設定）
   * getTitlePath（地區設定）

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath， Locale)
   * createTagByTitle(String tagTitlePath， Locale)
   * resolveByTitle(String tagTitlePath， Locale)

在AEM中，可以從頁面語言或使用者語言取得語言：

* 若要擷取JSP中的頁面語言：

   * `currentPage.getLanguage(false)`

* 若要擷取JSP中的使用者語言：

   * `slingRequest.getLocale()`

`currentPage` 和 `slingRequest` 可在JSP中使用，透過 [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) 標籤之間。

對於標籤，本地化取決於作為標籤的內容設定 `titles`能以頁面語言、使用者語言或任何其他語言顯示。

### 新增語言至編輯標籤對話方塊 {#adding-a-new-language-to-the-edit-tag-dialog}

下列程式說明如何新增語言（芬蘭文）至 **標籤編輯** 對話方塊：

1. 在 **CRXDE**，編輯多值屬性 `languages` 節點的 `/content/cq:tags`.

1. 新增 `fi_fi`  — 代表芬蘭語言環境 — 並儲存變更。

新語言（芬蘭文）現在可在頁面屬性的標籤對話方塊和 **編輯標籤** 對話方塊 **標籤** 主控台。

>[!NOTE]
>
>新語言必須是AEM認可的語言之一，也就是說，它必須可作為以下節點提供 `/libs/wcm/core/resources/languages`.
