---
title: 组件侧加载
seo-title: 组件侧加载
description: 将网页设计为简单的单页应用程序时，如果该应用程序会根据网站访客选择的内容动态更改显示的内容，则社区组件会侧加载非常有用
seo-description: 将网页设计为简单的单页应用程序时，如果该应用程序会根据网站访客选择的内容动态更改显示的内容，则社区组件会侧加载非常有用
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# 组件侧加载{#component-sideloading}

## 概述 {#overview}

当网页设计为简单的单页应用程序时，如果该应用程序会根据网站访客选择的内容动态更改显示的内容，则社区组件会侧加载非常有用。

当页面模板中不存在社区组件，而是在网站访客选择后动态添加组件时，即可完成此操作。

由于社交组件框架(SCF)具有轻量级存在，因此只注册初始页面加载时存在的SCF组件。 对于要在页面加载后注册的动态添加的SCF组件，必须调用SCF以“侧载”该组件。

当页面设计为侧载社区组件时，可以缓存整个页面。

动态添加SCF组件的步骤如下：

1. [将组件添加到DOM](#dynamically-add-component-to-dom)

1. [使用以下](#sideload-by-invoking-scf) 两种方法之一侧载组件：

* [动态包含](#dynamic-inclusion)
   * 引导所有动态添加的组件
* [动态加载](#dynamic-loading)
   * 按需添加一个特定组件

>[!NOTE]
>
>不支持对[非现有资源](scf.md#add-or-include-a-communities-component)进行侧加载。

## 将组件动态添加到DOM {#dynamically-add-component-to-dom}

无论组件是动态包含的还是动态加载的，都必须先将其添加到DOM中。

添加SCF组件时，最常用的标记是DIV标记，但也可能使用其他标记。 由于SCF仅在页面最初加载时才检查DOM，因此在明确调用SCF之前，DOM的这一附加内容不会被注意。

无论使用什么标记，元素都必须至少符合正常的SCF根元素模式，方法是包含以下两个属性：

* **data-component-id**

   添加的组件的有效路径。

* **数据 — scf-component**

   组件的resourceType。

以下是添加的注释组件的一个示例：

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## 通过调用SCF {#sideload-by-invoking-scf}进行侧载

### 动态包含{#dynamic-inclusion}

动态包含使用引导请求，导致SCF检查DOM并引导页面上找到的所有SCF组件。

要在页面加载后的任何时间初始化SCF组件，只需触发如下JQuery事件：

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### 动态加载{#dynamic-loading}

动态加载可以控制对SCF组件的加载。

可以指定特定的SCF组件来使用以下JavaScript方法进行加载，而不是引导DOM中找到的所有SCF组件：

`SCF.addComponent(document.getElementById(*someId*));`

其中`someId`是`data-component-id`属性的值。
