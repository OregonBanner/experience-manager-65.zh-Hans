---
title: 设计和设计人员
seo-title: 设计和设计人员
description: 您需要为网站创建设计，并在AEM中使用Designer实现
seo-description: 您需要为网站创建设计，并在AEM中使用Designer实现
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
exl-id: c81c5910-b6c9-41bd-8840-a6782792701f
source-git-commit: adbdff9ff5b5bd8f5f6b22fb724a0e5273072de2
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# 设计和设计器{#designs-and-the-designer}

>[!CAUTION]
>
>本文介绍了如何基于经典UI创建网站。 Adobe建议为您的网站利用最新的AEM技术，详情请参阅[AEM Sites开发入门](/help/sites-developing/getting-started.md)一文。

Designer用于使用AEM中的[经典UI](/help/release-notes/touch-ui-features-status.md)为您的网站创建设计。

>[!NOTE]
>
>有关Web无障碍的更多信息，请参阅[AEM和Web无障碍准则](/help/managing/web-accessibility.md)。

## 使用Designer {#using-the-designer}

可以在&#x200B;**工具**&#x200B;选项卡的&#x200B;**designs**&#x200B;部分中定义您的设计：

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

在此，您可以创建存储设计所需的结构，然后上传所需的级联样式表和图像。

设计存储在`/apps/<your-project>`下。 要用于网站的设计路径是使用`jcr:content`节点的`cq:designPath`属性指定的。

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>在设计模式下对页面所做的所有更改都会保留在网站设计节点下方，并自动应用于具有相同设计的所有页面。

## 您需要的{#what-you-will-need}

要实现您的设计，您需要：

**CSS**  — 层叠样式表定义页面上特定区域的格式。**图像**  — 用于背景、按钮等功能的任何图像。

### 设计网站{#considerations-when-designing-your-website}时的注意事项

在开发网站时，强烈建议在`/apps/<your-project>`下存储图像和CSS文件，以便您能够根据当前设计（如以下代码片段所述）引用资源。

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

上例提供了以下几项优势：

* 组件的外观可能因使用不同设计路径的每个网站而异。
* 只需将设计路径指向站点根目录下从`design/v1`到`design/v2.`的其他节点，即可轻松完成网站的重新设计

* `/etc/designs` 和是 `/content` 浏览器唯一看到保护您的外部用户的外部URL，外部用户对树下的内容感到 `/apps` 好奇。上述URL优势还有助于系统管理员设置更好的安全性，因为您将资产的泄露限制在几个不同的位置。
