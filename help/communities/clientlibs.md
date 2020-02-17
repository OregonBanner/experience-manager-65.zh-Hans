---
title: Clientlibs for Communities组件
seo-title: Clientlibs for Communities组件
description: 社区的客户端库
seo-description: 社区的客户端库
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Clientlibs for Communities组件{#clientlibs-for-communities-components}

## 简介 {#introduction}

文档的本节介绍如何将客户端库(clientlibs)添加到Communities组件的页面。

有关基本信息，请访问：

* [使用客户端库](/help/sites-developing/clientlibs.md) ，它提供使用详细信息和调试工具
* [SCF的客户端库](/help/communities/client-customize.md#clientlibs) ，它在自定义SCF组件时提供有用信息
* [博客：AEM客户端库（示例说明）](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## 为何需要Clientlibs {#why-clientlibs-are-required}

需要Clientlibs才能正常运行组件(JavaScript)和样式(CSS)。

当某个功能存 [在社区功能](/help/communities/functions.md) ，所有必需的组件和配置（包括所需的clientlib）都将出现在社区站点中。 只有当作者可以使用其他组件时，才需要添加其他clientlib。

当缺少所需的clientlib时， [向页面添加Communities组件可能会导致javascript错误](/help/communities/author-communities.md) ，并导致意外外观。

### 示例：无Clientlibs的置入审阅 {#example-placed-reviews-without-clientlibs}

![chlimage_1-132](assets/chlimage_1-132.png)

### 示例：使用Clientlibs置入的审阅 {#example-placed-reviews-with-clientlibs}

![chlimage_1-133](assets/chlimage_1-133.png)

## 识别所需的Clientlib {#identifying-required-clientlibs}

开发人员的基本功能信息标识了所需的客户端库。

此外，从AEM实例中，浏览到“社区组件指南” [](/help/communities/components-guide.md) ，您可以访问组件所需的clientlib类别列表。

例如，在“审阅”页面的最 [顶部](https://localhost:4502/content/community-components/en/reviews.html) ，列出的所需客户端库

* cq.ckeditor
* cq.social.hbs.reviews

![chlimage_1-134](assets/chlimage_1-134.png)

## 添加必需的Clientlibs {#adding-required-clientlibs}

当需要向页面添加社区组件时，如果组件不存在，则需要为该组件添加所需的客户端库。

使 [用CRXDE|Lite](#using-crxde-lite) ，为社区站点页面修改现有clientlibslist。

要使用 [CRXDE lite为社区站点添加clientlib，请执行以下操作](/help/sites-developing/developing-with-crxde-lite.md) :

* 浏览 [到https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* 找到 `clientlibslist` 要添加组件的页面的节点

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* 已选 `clientlibslist` 择节点

   * 查找字符串属性[] 。 `scg:requiredClientLibs`
   * 选择其 `Value` 以访问字符串数组对话框

      * 根据需要向下滚动
      * 选择+以进入新的客户端库

         * 重复以添加更多客户端库
      * 选择**确定**
   * 选择 **全部保存**



>[!NOTE]
>
>如果站点不是社区站点，则需要发现站点使用的客户端库的存在或位置。

使用AEM Communities [快速入门示例](/help/communities/getting-started.md) (其 `site-name` 中为Engage **)，添加审阅组件时，clientliblist的显示方式如下：

![chlimage_1-135](assets/chlimage_1-135.png)

