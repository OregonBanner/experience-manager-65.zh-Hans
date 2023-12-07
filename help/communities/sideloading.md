---
title: 组件侧载
description: 当网页设计为一个简单的单页面应用程序时，Communities组件旁加载会非常有用，该应用程序会根据网站访客选择的内容动态更改显示的内容
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# 组件侧载 {#component-sideloading}

## 概述 {#overview}

当网页设计为一个简单的单页面应用程序时，Communities组件旁加载会非常有用，该应用程序会根据网站访客选择的内容来动态更改显示的内容。

当页面模板中不存在Communities组件，而是根据网站访客的选择动态添加组件时，即可实现此目的。

由于社交组件框架(SCF)具有轻量级存在，因此仅注册初始页面加载时存在的SCF组件。 对于要在页面加载后注册的动态添加的SCF组件，必须调用SCF以“侧载”该组件。

当页面设计为侧载Communities组件时，可以缓存整个页面。

动态添加SCF组件的步骤如下：

1. [将组件添加到DOM](#dynamically-add-component-to-dom)

1. [侧载组件](#sideload-by-invoking-scf) 使用以下两种方法之一：

* [动态包含](#dynamic-inclusion)
   * 引导所有动态添加的组件
* [动态加载](#dynamic-loading)
   * 按需添加一个特定组件

>[!NOTE]
>
>侧载 [非现有资源](scf.md#add-or-include-a-communities-component) 不受支持。

## 将组件动态添加到DOM {#dynamically-add-component-to-dom}

无论组件是动态包含还是动态加载，都必须首先将其添加到DOM。

添加SCF组件时，最常用的标记是DIV标记，但也可以使用其他标记。 由于SCF仅在最初加载页面时检查DOM，因此，在显式调用SCF之前，不会注意到对DOM的此添加。

无论使用什么标记，至少元素都必须通过包含这两个属性来符合正常的SCF根元素模式：

* **data-component-id**

  所添加组件的有效路径。

* **data-scf-component**

  组件的resourceType。

以下是已添加注释组件的示例：

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## 通过调用SCF进行侧载 {#sideload-by-invoking-scf}

### 动态包含 {#dynamic-inclusion}

动态包含使用引导请求，该请求会导致SCF检查DOM并引导页面上的所有SCF组件。

要在页面加载后随时初始化SCF组件，只需触发如下所示的JQuery事件：

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### 动态加载 {#dynamic-loading}

动态加载提供对SCF组件的加载控制。

可以使用此JavaScript方法指定要加载的特定SCF组件，而不是引导在DOM中找到的所有SCF组件：

`SCF.addComponent(document.getElementById(*someId*));`

位置 `someId` 的值为 `data-component-id` 属性。
