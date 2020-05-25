---
title: 在AEM应用程序中构建标记
seo-title: 在AEM应用程序中构建标记
description: 在自定义AEM应用程序中以编程方式使用标记或扩展标记
seo-description: 在自定义AEM应用程序中以编程方式使用标记或扩展标记
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
translation-type: tm+mt
source-git-commit: 1493b301ecf4c25f785495e11ead352de600ddb7
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---


# 在AEM应用程序中构建标记{#building-tagging-into-an-aem-application}

为了在自定义AEM应用程序中以编程方式使用标记或扩展标记，本页介绍了

* [标记API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

与

* [标记框架](/help/sites-developing/framework.md)

有关标记的相关信息，请参阅：

* [管理标记](/help/sites-administering/tags.md) ，以了解有关创建和管理标记以及已应用哪些内容标记的信息。
* [使用标记](/help/sites-authoring/tags.md) ，以了解有关标记内容的信息。

## Tagging API概述 {#overview-of-the-tagging-api}

在AEM中实 [施标记框](/help/sites-developing/framework.md) 架允许使用JCR API管理标记和标记内容。 TagManager可确保在字符串数组属性中作为值输 `cq:tags` 入的标记不会重复，它会删除指向非现有标记的TagID，并为移动或合并的标记更新TagID。 TagManager使用JCR观察监听器来还原任何不正确的更改。 主类位于com.day.cq.ta [日志包](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) :

* JcrTagManagerFactory —— 返回基于JCR的实施 `TagManager`。 它是Tagging API的参考实现。
* `TagManager` -允许按路径和名称解析和创建标记。
* `Tag` -定义标记对象。

### 获取基于JCR的TagManager {#getting-a-jcr-based-tagmanager}

要检索TagManager实例，您需要有JCR并 `Session` 调用 `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在典型的Sling环境中，您还可以适应以 `TagManager` 下内容 `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 检索标记对象 {#retrieving-a-tag-object}

通过 `Tag` 解析现有标 `TagManager`签或创建新标签，可以通过检索：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

对于映射到JCR的基于JCR `Tags` 的实 `Nodes`施，如果您有资源(如 `adaptTo``/content/cq:tags/default/my/tag`:

```java
Tag tag = resource.adaptTo(Tag.class);
```

虽然标记只能从*a资源（非节点）转换*，但标记可以*转换为*节点和资源：

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>由于不实 `Node` 现Sling `Tag` 方法，因此无 `Node` 法直接适应 `Adaptable.adaptTo(Class)` 。

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
>有效 `RangeIterator` 使用方式为：
>
>`com.day.cq.commons.RangeIterator`

### 删除标记 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 复制标记 {#replicating-tags}

可以将复制服务()与标 `Replicator`记一起使用，因为标记类型 `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 在客户端添加标签 {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` 是用于输入标记的表单构件。 它有一个弹出菜单，用于从现有标记中进行选择，包括自动完成和许多其他功能。 它的xtype是 `tags`。

## 标记垃圾收集器 {#the-tag-garbage-collector}

标记垃圾收集器是一种后台服务，用于清除隐藏和未使用的标记。 隐藏和未使用的标记是 `/content/cq:tags` 下面具有属 `cq:movedTo` 性且不在内容节点上使用的标记——它们的计数为零。 通过使用此延迟删除过程，内容节点(即 `cq:tags` 属性)不必作为移动或合并操作的一部分进行更新。 属性中的引 `cq:tags` 用在属性更新时 `cq:tags` 会自动更新，例如，通过页面属性对话框。

标记垃圾收集器默认每天运行一次。 可在以下位置进行配置：

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 标记搜索和标记列表 {#tag-search-and-tag-listing}

搜索标记和标记列表的工作方式如下：

* 搜索TagID会搜索属性设置为TagID并 `cq:movedTo` 随后跟踪TagID的 `cq:movedTo` 标记。

* 搜索标记标题仅搜索没有属性的标 `cq:movedTo` 记。

## Tags in Different Languages {#tags-in-different-languages}

如管理标记的文档所述，在管理不同语言 [的标记部分](/help/sites-administering/tags.md#managing-tags-in-different-languages)，可以 `title`使用不同的语言定义标记。 然后，语言相关属性被添加到标记节点。 此属性具有 `jcr:title.<locale>`格式，如 `jcr:title.fr` 法语翻译。 `<locale>` 必须是小写的ISO区域设置字符串，并使用“_”而不是“-”，例如： `de_ch`.

将Animals **标签添加** 到“产品”页面后 **，该值将** 添加到节点 `stockphotography:animals``cq:tags` /content/geometrixx/cn/products/jcr:content的属性中。 转换从标记节点引用。

服务器端API具有与本地化相关 `title`的方法：

* [com.day.cq.taging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle（区域设置）
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle（区域设置）
   * getTitlePath（区域设置）

* [com.day.cq.taging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle（String tagTitlePath, Locale区域设置）
   * createTagByTitle（String tagTitlePath，区域设置）
   * resolveByTitle（String tagTitlePath，区域设置）

在AEM中，可以从页面语言或用户语言获取该语言：

* 要在JSP中检索页面语言，请执行以下操作：

   * `currentPage.getLanguage(false)`

* 要在JSP中检索用户语言，请执行以下操作：

   * `slingRequest.getLocale()`

`currentPage` 和 `slingRequest` 在JSP中通过&lt;cq: [definedObjects>标签提供](/help/sites-developing/taglib.md) 。

对于标记，本地化取决于上下文，因 `titles`为标记可以以页面语言、用户语言或任何其他语言显示。

### 向“编辑标记”对话框添加新语言 {#adding-a-new-language-to-the-edit-tag-dialog}

以下过程介绍如何向“标记编辑”对话框添加新 **语言** （芬兰语）:

1. 在 **CRXDE**&#x200B;中，编辑节点的 `languages` 多值属性 `/content/cq:tags`。

1. 添 `fi_fi` 加（表示芬兰语区域设置）并保存更改。

现在，在“标记”控制台中编辑标记时，页面属性的标记对话框和“编 **辑标记** ”对话框中都提供新 **语言** （芬兰语）。

>[!NOTE]
>
>新语言必须是AEM认可的语言之一，即它需要作为以下节点可用 `/libs/wcm/core/resources/languages`。

