---
title: 在AEM应用程序中生成标记
description: 以编程方式处理自定义AEM应用程序中的标记或扩展标记
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
feature: Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# 在AEM应用程序中生成标记{#building-tagging-into-an-aem-application}

对于以编程方式使用自定义AEM应用程序中的标记或扩展标记，本页介绍如何使用

* [标记API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/package-summary.html)

那个和

* [标记框架](/help/sites-developing/framework.md)

有关标记的相关信息，请参阅：

* [管理标记](/help/sites-administering/tags.md) 有关创建和管理标记以及已对哪些内容应用标记的信息。
* [使用标记](/help/sites-authoring/tags.md) 以了解有关标记内容的信息。

## 标记API概述 {#overview-of-the-tagging-api}

实施 [标记框架](/help/sites-developing/framework.md) 允许在AEM中使用JCR API管理标记和标记内容。 TagManager可确保在 `cq:tags` 字符串数组属性不会重复，它会删除指向不存在的标记的TagID，并更新已移动或合并标记的标记ID。 TagManager使用JCR观察侦听器来还原任何不正确的更改。 主类位于 [com.day.cq.tagg](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/package-summary.html) 包：

* JcrTagManagerFactory — 返回基于JCR的 `TagManager`. 它是标记API的参考实施。
* `TagManager`  — 允许按路径和名称解析和创建标记。
* `Tag`  — 定义标记对象。

### 获取基于JCR的标签管理器 {#getting-a-jcr-based-tagmanager}

要检索TagManager实例，您必须具有JCR `Session` 并调用 `getTagManager(Session)`：

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

A `Tag` 可通过 `TagManager`，通过解析现有标记或创建现有标记：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

对于基于JCR的实施，其映射了 `Tags` 转到JCR `Nodes`，您可以直接使用Sling `adaptTo` 机制(如果您有资源，例如 `/content/cq:tags/default/my/tag`)：

```java
Tag tag = resource.adaptTo(Tag.class);
```

虽然标记只能从*资源（而非节点）进行转换，但标记可以同时*转换*为节点和资源：

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>直接从 `Node` 到 `Tag` 是不可能的，因为 `Node` 不实施Sling `Adaptable.adaptTo(Class)` 方法。

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

可以使用复制服务( `Replicator`)，因为标记的类型为 `nt:hierarchyNode`：

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 在客户端标记 {#tagging-on-the-client-side}

表单构件 `CQ.tagging.TagInputField` 用于输入标记。 它有一个弹出菜单，用于从现有标记中进行选择，包括自动完成和许多其他功能。 其xtype为 `tags`.

## 标记垃圾收集器 {#the-tag-garbage-collector}

标记垃圾收集器是一种后台服务，用于清理隐藏和未使用的标记。 隐藏和未使用的标记是以下标记 `/content/cq:tags` 具有 `cq:movedTo` 属性且未在内容节点上使用 — 它们的计数为零。 通过使用这种延迟删除流程，内容节点(即 `cq:tags` 属性)不必作为移动或合并操作的一部分进行更新。 中的引用 `cq:tags` 属性在以下情况下自动更新 `cq:tags` 例如，通过页面属性对话框更新属性。

默认情况下，标记垃圾回收器每天运行一次。 您可以在以下位置配置它：

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 标记搜索和标记列表 {#tag-search-and-tag-listing}

搜索标记和标记列表的工作方式如下：

* 搜索TagID会搜索具有属性的标记 `cq:movedTo` 设置为TagID并遵循 `cq:movedTo` 标记ID。

* 搜索标记“标题”只会搜索没有 `cq:movedTo` 属性。

## 不同语言的标记 {#tags-in-different-languages}

如有关管理标记的文档中所述，请参阅部分 [管理不同语言的标记](/help/sites-administering/tags.md#managing-tags-in-different-languages)，标记 `title`可以用不同的语言定义。 然后，将区分语言的属性添加到标记节点。 此属性的格式为 `jcr:title.<locale>`例如， `jcr:title.fr` 法文版的。 此 `<locale>` 必须为小写的ISO区域设置字符串，并使用“_”而不是“ — ”，例如： `de_ch`.

当 **动物** 标记将添加到 **产品** 页面，值 `stockphotography:animals` 添加到属性 `cq:tags` /content/geometrixx/en/products/jcr：content节点的。 将从标记节点中引用翻译。

服务器端API已本地化 `title`相关方法：

* [com.day.cq.tagging.Tag](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle（区域设置）
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle（区域设置）
   * getTitlePath（区域设置）

* [com.day.cq.tagging.TagManager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath， Locale)
   * createTagByTitle(String tagTitlePath， Locale)
   * resolveByTitle(String tagTitlePath， Locale)

在AEM中，可以从页面语言或用户语言获取语言：

* 要在JSP中检索页面语言，请执行以下操作：

   * `currentPage.getLanguage(false)`

* 要在JSP中检索用户语言，请执行以下操作：

   * `slingRequest.getLocale()`

此 `currentPage` 和 `slingRequest` 可在JSP中通过 [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) 标记之前。

对于标记，本地化取决于作为标记的上下文 `titles`能够以页面语言、用户语言或任何其他语言显示。

### 向“编辑标记”对话框添加新语言 {#adding-a-new-language-to-the-edit-tag-dialog}

以下过程介绍了如何将语言（芬兰语）添加到 **标记编辑** 对话框：

1. 在 **CRXDE**，编辑多值属性 `languages` 节点的 `/content/cq:tags`.

1. 添加 `fi_fi`  — 表示芬兰语言环境 — 并保存更改。

新语言（芬兰语）现在可在页面属性的标记对话框中以及 **编辑标记** 对话框。 **标记** 控制台。

>[!NOTE]
>
>新语言必须是AEM认可的语言之一。 也就是说，它必须作为以下节点提供 `/libs/wcm/core/resources/languages`.

>[!CAUTION]
>
>安装Service Pack会将/content/cq：tags节点的languages属性重置为默认值。 因此，在安装之前，必须从属性中添加它。
