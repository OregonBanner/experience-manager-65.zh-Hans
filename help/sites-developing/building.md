---
title: 将标记构建到AEM应用程序
seo-title: 将标记构建到AEM应用程序
description: 以编程方式在自定义AEM应用程序中使用标记或扩展标记
seo-description: 以编程方式在自定义AEM应用程序中使用标记或扩展标记
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
feature: 标记
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---

# 将标记构建到AEM应用程序{#building-tagging-into-an-aem-application}

为了以编程方式在自定义AEM应用程序中使用标记或扩展标记，本页介绍了

* [标记API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

与

* [标记框架](/help/sites-developing/framework.md)

有关标记的相关信息，请参阅：

* [管理](/help/sites-administering/tags.md) 标记以了解有关创建和管理标记以及已对哪些内容应用标记的信息。
* [使用标](/help/sites-authoring/tags.md) 记有关标记内容的信息。

## 标记API {#overview-of-the-tagging-api}概述

在AEM中实施[标记框架](/help/sites-developing/framework.md)后，可以使用JCR API管理标记和标记内容。 TagManager可确保在`cq:tags`字符串数组属性中作为值输入的标记不重复，从而删除指向非现有标记的标记ID，并更新已移动或合并标记的标记ID。 TagManager使用JCR观察侦听器来还原任何不正确的更改。 主类位于[com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html)包中：

* JcrTagManagerFactory — 返回基于JCR的`TagManager`实施。 它是标记API的参考实施。
* `TagManager`  — 允许按路径和名称解析和创建标记。
* `Tag`  — 定义标记对象。

### 获取基于JCR的TagManager {#getting-a-jcr-based-tagmanager}

要检索TagManager实例，您需要具有JCR `Session`并调用`getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在典型的Sling上下文中，您还可以根据`ResourceResolver`中的`TagManager`进行调整：

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 检索标记对象{#retrieving-a-tag-object}

通过解析现有标记或创建新标记，可通过`TagManager`检索`Tag`:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

对于基于JCR的实施（将`Tags`映射到JCR `Nodes`），如果您具有资源（例如`/content/cq:tags/default/my/tag`），则可以直接使用Sling的`adaptTo`机制：

```java
Tag tag = resource.adaptTo(Tag.class);
```

虽然标记只能从*a资源（而非节点）中转换*，但标记可以从*a节点和资源中转换*为：

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>无法直接从`Node`适应到`Tag`，因为`Node`不实施Sling `Adaptable.adaptTo(Class)`方法。

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
>使用的有效`RangeIterator`是：
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

## 在客户端{#tagging-on-the-client-side}上标记

`CQ.tagging.TagInputField` 是用于输入标记的表单小组件。它有一个弹出菜单，用于从现有标记中进行选择，包括自动完成和许多其他功能。 其xtype为`tags`。

## 标记垃圾收集器{#the-tag-garbage-collector}

标记垃圾回收器是一项后台服务，可清理隐藏和未使用的标记。 隐藏和未使用的标记是`/content/cq:tags`下的标记，具有`cq:movedTo`属性，且未在内容节点上使用 — 它们的计数为零。 通过使用此延迟删除过程，内容节点（即`cq:tags`属性）不必在移动或合并操作中进行更新。 更新`cq:tags`属性时，将自动更新`cq:tags`属性中的引用，例如，通过页面属性对话框。

标记垃圾收集器默认每天运行一次。 可在以下位置进行配置：

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 标记搜索和标记列表{#tag-search-and-tag-listing}

搜索标记和标记列表的工作方式如下：

* 搜索TagID会搜索将属性`cq:movedTo`设置为TagID并跟踪到`cq:movedTo` TagID的标记。

* 搜索标记标题仅会搜索没有`cq:movedTo`属性的标记。

## 不同语言的标记{#tags-in-different-languages}

如标签管理文档中的[管理不同语言的标签](/help/sites-administering/tags.md#managing-tags-in-different-languages)部分所述，标签`title`可以用不同的语言定义。 然后，会将语言敏感属性添加到标记节点。 此属性的格式为`jcr:title.<locale>`，例如`jcr:title.fr`表示法文翻译。 `<locale>` 必须是小写的ISO区域设置字符串，并使用“_”而不是“ — ”，例如： `de_ch`.

将&#x200B;**Animals**&#x200B;标记添加到&#x200B;**Products**&#x200B;页面后，值`stockphotography:animals`将添加到节点/content/geometrixx/en/products/jcr:content的属性`cq:tags`中。 转换从标记节点引用。

服务器端API已本地化了与`title`相关的方法：

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle（区域设置）
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle（区域设置）
   * getTitlePath（区域设置）

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath， Locale)
   * createTagByTitle(String tagTitlePath， Locale)
   * resolveByTitle(String tagTitlePath， Locale)

在AEM中，可以从页面语言或用户语言获取语言：

* 要在JSP中检索页面语言，请执行以下操作：

   * `currentPage.getLanguage(false)`

* 要在JSP中检索用户语言，请执行以下操作：

   * `slingRequest.getLocale()`

`currentPage` 和可 `slingRequest` 通过标记在JSP中使 [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) 用。

对于标记，本地化取决于上下文，因为标记`titles`可以以页面语言、用户语言或任何其他语言显示。

### 向“编辑标记”对话框{#adding-a-new-language-to-the-edit-tag-dialog}添加新语言

以下过程介绍如何向&#x200B;**标记编辑**&#x200B;对话框添加新语言（芬兰语）：

1. 在&#x200B;**CRXDE**&#x200B;中，编辑节点`/content/cq:tags`的多值属性`languages`。

1. 添加`fi_fi` — 表示芬兰语区域设置 — 并保存更改。

现在，在&#x200B;**Tagging**&#x200B;控制台中编辑标记时，页面属性的标记对话框和&#x200B;**编辑标记**&#x200B;对话框中都提供了新语言（芬兰语）。

>[!NOTE]
>
>新语言必须是AEM可识别的语言之一，即它需要作为`/libs/wcm/core/resources/languages`下的节点提供。
