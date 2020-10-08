---
title: 组件侧传
seo-title: 组件侧传
description: 将网页设计为简单的单页应用程序时，社区组件侧传非常有用，该应用程序会根据站点访客选择的内容动态更改显示的内容
seo-description: 将网页设计为简单的单页应用程序时，社区组件侧传非常有用，该应用程序会根据站点访客选择的内容动态更改显示的内容
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# 组件侧传 {#component-sideloading}

## 概述 {#overview}

将网页设计为简单的单页应用程序时，社区组件侧传非常有用，该应用程序会根据站点访客选择的内容动态更改显示的内容。

当页面模板中不存在社区组件，而是在站点访客选择后动态添加组件时，即可完成此操作。

由于社交组件框架(SCF)具有轻量级存在，因此只注册初始页面加载时存在的SCF组件。 要在页面加载后注册动态添加的SCF组件，必须调用SCF以“侧传”该组件。

当页面设计为侧传社区组件时，可以缓存整个页面。

动态添加SCF组件的步骤有：

1. [将组件添加到DOM](#dynamically-add-component-to-dom)

1. [使用以下两种方法](#sideload-by-invoking-scf) 之一侧传组件：

* [动态包含](#dynamic-inclusion)
   * 启动所有动态添加的组件
* [动态加载](#dynamic-loading)
   * 按需添加一个特定组件

>[!NOTE]
>
>不支持 [对非现有资源](scf.md#add-or-include-a-communities-component) 进行侧传。

## 将组件动态添加到DOM {#dynamically-add-component-to-dom}

无论组件是动态包含的还是动态加载的，都必须先将其添加到DOM中。

添加SCF组件时，最常用的标签是DIV标签，但也可以使用其他标签。 由于SCF仅在页面初始加载时检查DOM，因此在显式调用SCF之前，对DOM的这一添加将不会引起注意。

无论使用什么标签，元素至少必须包含以下两个属性，以符合标准SCF根元素模式：

* **data-component-id**

   添加的组件的有效路径。

* **数据-scf组件**

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

## 通过调用SCF进行侧传 {#sideload-by-invoking-scf}

### 动态包含 {#dynamic-inclusion}

动态包含使用引导请求，这会导致SCF检查DOM并引导页面上找到的所有SCF组件。

要在页面加载后随时初始化SCF组件，只需触发JQuery事件，如下所示：

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### 动态加载 {#dynamic-loading}

动态加载提供对加载SCF组件的控制。

可以指定特定的SCF组件来使用此JavaScript方法加载，而不是引导DOM中找到的所有SCF组件：

`SCF.addComponent(document.getElementById(*someId*));`

其 `someId` 中是属性的 `data-component-id` 值。
