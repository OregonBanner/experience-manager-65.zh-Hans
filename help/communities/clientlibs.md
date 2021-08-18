---
title: 适用于社区组件的Clientlibs
seo-title: 适用于社区组件的Clientlibs
description: 社区的客户端库
seo-description: 社区的客户端库
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 适用于社区组件的Clientlibs {#clientlibs-for-communities-components}

## 简介 {#introduction}

文档的此部分介绍如何将客户端库(clientlibs)添加到社区组件的页面。

有关基本信息，请访问：

* [使用客户端库，](/help/sites-developing/clientlibs.md) 该库提供使用详细信息以及调试工具
* [SCF的Clientlib在自定](/help/communities/client-customize.md#clientlibs) 义SCF组件时提供有用信息


## 为何需要Clientlibs {#why-clientlibs-are-required}

组件正常运行(JavaScript)和样式(CSS)需要Clientlibs。

当某个功能存在[社区函数](/help/communities/functions.md)时，所有必需的组件和配置（包括所需的clientlib）都将出现在社区站点中。 只有当其他组件可供作者使用时，才需要添加其他clientlib。

当缺少所需的clientlib时， [将社区组件添加到页面](/help/communities/author-communities.md)可能会导致javascript错误以及意外外观。

### 示例：未使用Clientlibs进行审阅 {#example-placed-reviews-without-clientlibs}

![置入审阅](assets/placed-reviews.png)

### 示例：使用Clientlibs进行审阅 {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## 确定所需的Clientlib {#identifying-required-clientlibs}

面向开发人员的基本功能信息可识别所需的客户端库。

此外，从AEM实例浏览到[社区组件指南](/help/communities/components-guide.md)可访问组件所需的clientlib类别列表。

例如，在[Reviews页面](https://localhost:4502/content/community-components/en/reviews.html)的最顶部列出了所需的clientlib

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs reviews](assets/clientlibs-reviews.png)

## 添加必需的Clientlibs {#adding-required-clientlibs}

当需要向页面添加社区组件时，如果组件尚不存在，则需要为该组件添加所需的clientlib。

使用[CRXDE|Lite](#using-crxde-lite)修改社区站点页面的现有clientlibslist。

要使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)为社区站点添加clientlib，请执行以下操作：

* 浏览到[https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)。
* 在要添加组件的页面上找到`clientlibslist`节点：

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* 选择`clientlibslist`节点后：

   * 找到字符串[]属性`scg:requiredClientLibs`。
   * 选择其`Value`以访问字符串数组对话框。

      * 根据需要向下滚动。
      * 选择+以输入新的客户端库。

         * 重复以添加更多客户端库。

         * 选择&#x200B;**确定**。
   * 选择&#x200B;**全部保存**。


>[!NOTE]
>
>如果网站不是社区网站，则需要发现网站正在使用的客户端库的存在或位置。

使用[AEM Communities](/help/communities/getting-started.md)快速入门示例（其中`site-name`为&#x200B;*engage*），添加reviews组件时，clientliblist的显示方式如下：

![审阅组件](assets/review-component.png)
