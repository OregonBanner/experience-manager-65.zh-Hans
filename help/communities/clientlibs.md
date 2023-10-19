---
title: 适用于社区组件的Clientlibs
description: 了解如何将客户端库(clientlibs)添加到页面，以便收集使用情况详细信息并使用社区组件的调试工具。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# 适用于社区组件的Clientlibs {#clientlibs-for-communities-components}

## 简介 {#introduction}

此文档的此部分介绍如何将客户端库(clientlibs)添加到社区组件的页面。

有关基本信息，请参阅以下内容：

* [使用客户端库](/help/sites-developing/clientlibs.md) 其中提供了使用详细信息和调试工具
* [适用于SCF的Clientlibs](/help/communities/client-customize.md#clientlibs) 在自定义SCF组件时，它提供了有用的信息


## 为什么需要Clientlibs {#why-clientlibs-are-required}

组件正常使用(JavaScript)和样式(CSS)需要Clientlibs。

当存在 [社区功能](/help/communities/functions.md) 对于功能，社区站点中会显示所有必需的组件和配置，包括所需的clientlibs。 仅当要向作者提供其他组件时，才必须添加其他clientlibs。

当缺少所需的clientlibs时， [将Communities组件添加到页面](/help/communities/author-communities.md) 可能会导致JavaScript错误和意外显示。

### 示例：置入的审阅没有Clientlibs {#example-placed-reviews-without-clientlibs}

![置入的审核](assets/placed-reviews.png)

### 示例：使用Clientlibs置入审核 {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## 标识所需的Clientlibs {#identifying-required-clientlibs}

面向开发人员的基本功能信息可标识所需的clientlibs。

此外，从AEM实例浏览到 [社区组件指南](/help/communities/components-guide.md) 提供对组件所需的clientlib类别列表的访问。

例如，在 [“审核”页面](https://localhost:4502/content/community-components/en/reviews.html) 列出的所需clientlibs包括

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## 添加所需的Clientlibs {#adding-required-clientlibs}

当需要将Communities组件添加到页面时，如果组件尚不存在，则必须添加该组件所需的clientlibs。

使用 [CRXDE|Lite](#using-crxde-lite) 修改社区站点页面的现有clientlibslist。

要使用为社区站点添加clientlib，请执行以下操作 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)：

* 浏览至 [https://&lt;server>：&lt;port>/crx/de](https://localhost:4502/crx/de).
* 找到 `clientlibslist` 要添加组件的页面的节点：

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* 替换为 `clientlibslist` 选定的节点：

   * 查找字符串[] 属性 `scg:requiredClientLibs`.
   * 选择其 `Value` 以便访问“字符串数组”对话框。

      * 如有必要，向下滚动。
      * 选择+以输入新的客户端库。

         * 重复以上步骤以添加更多客户端库。

         * 选择 **确定**.

   * 选择 **全部保存**.

>[!NOTE]
>
>如果站点不是社区站点，则必须发现用于该站点的客户端库是否存在或位置。

使用 [AEM Communities快速入门](/help/communities/getting-started.md) 例如，其中 `site-name` 是 *参与*，下面显示了添加审阅组件时clientliblist的显示方式：

![review-component](assets/review-component.png)
