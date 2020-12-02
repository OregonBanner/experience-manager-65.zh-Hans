---
title: 设计与设计人员
seo-title: 设计与设计人员
description: 您需要为您的网站创建设计，而在AEM中，您需要使用设计器
seo-description: 您需要为您的网站创建设计，而在AEM中，您需要使用设计器
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# 设计和设计器{#designs-and-the-designer}

>[!CAUTION]
>
>本文介绍如何基于经典UI创建网站。 Adobe建议按照文章[开发AEM Sites](/help/sites-developing/getting-started.md)中的详细说明，为您的网站使用最新的AEM技术。

您需要为您的网站创建设计，而在AEM中，您需要使用设计器来创建。

>[!NOTE]
>
>有关Web辅助功能的详细信息，请参阅[AEM和Web辅助功能指导原则](/help/managing/web-accessibility.md)。

## 使用Designer {#using-the-designer}

您的设计可以在&#x200B;**工具**&#x200B;选项卡的&#x200B;**designs**&#x200B;部分中定义：

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

您可以在此创建存储设计所需的结构，然后上传所需的级联样式表和图像。

设计存储在`/etc/designs`下。 使用`jcr:content`节点的`cq:designPath`属性指定要用于网站的设计的路径。

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>在设计模式下对页面所做的所有更改将保留在站点的设计节点下，并自动应用于具有相同设计的所有页面。

## 您需要{#what-you-will-need}

要实现您的设计，您需要：

**CSS** -层叠样式表定义页面上特定区域的格式。**图像** -用于背景、按钮等功能的任何图像。

### 设计网站{#considerations-when-designing-your-website}时的注意事项

在开发网站时，强烈建议在`/etc/design/<project>`下存储图像和CSS文件，这样您就可以根据当前设计引用您的资源，如以下代码片断所述。

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

前面的示例优惠具有以下几个优点：

* 组件的外观可以根据使用不同设计路径的每个站点而有所不同。
* 只需将设计路径指向站点根部的不同节点（从`design/v1`指向`design/v2.`），即可轻松地重新设计网站

* `/etc/designs` 并且 `/content` 是浏览器看到的唯一外部URL，用于保护您的外部用户对树下的内容产生 `/apps` 好奇。上述URL优势还有助于系统管理员设置更好的安全性，因为您将资产的曝光限制在几个不同的位置。

