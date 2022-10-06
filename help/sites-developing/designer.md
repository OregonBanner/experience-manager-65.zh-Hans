---
title: 设计和设计人员
seo-title: Designs and the Designer
description: 您需要为网站创建设计，而在AEM中，使用Designer来创建设计
seo-description: You will need to create a design for your website and in AEM, you do so by using the Designer
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
exl-id: c81c5910-b6c9-41bd-8840-a6782792701f
source-git-commit: adbdff9ff5b5bd8f5f6b22fb724a0e5273072de2
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 设计和设计人员{#designs-and-the-designer}

>[!CAUTION]
>
>本文介绍了如何基于经典UI创建网站。 Adobe建议将最新的AEM技术用于您的网站，如文章中所述 [开发入门AEM Sites](/help/sites-developing/getting-started.md).

设计器用于使用 [经典UI](/help/release-notes/touch-ui-features-status.md) 在AEM中。

>[!NOTE]
>
>有关Web辅助功能的更多信息，请参阅 [AEM和Web无障碍准则](/help/managing/web-accessibility.md).

## 使用设计器 {#using-the-designer}

您的设计可在 **设计** 部分 **工具** 选项卡：

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

在此，您可以创建存储设计所需的结构，然后上传所需的级联样式表和图像。

设计存储在 `/apps/<your-project>`. 要用于网站的设计路径，使用 `cq:designPath` 属性 `jcr:content` 节点。

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>在设计模式下对页面所做的所有更改都会保留在网站设计节点下方，并自动应用于具有相同设计的所有页面。

## 您需要的 {#what-you-will-need}

要实现您的设计，您需要：

**CSS**  — 层叠样式表定义页面上特定区域的格式。
**图像**  — 用于背景、按钮等功能的任何图像。

### 设计网站时的注意事项 {#considerations-when-designing-your-website}

在开发网站时，强烈建议在 `/apps/<your-project>` 这样，您就可以根据当前设计引用资源，如以下代码片段所述。

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

上例提供了以下几项优势：

* 组件的外观可能因使用不同设计路径的每个网站而异。
* 只需将设计路径指向网站根目录的其他节点(从 `design/v1` to `design/v2.`

* `/etc/designs` 和 `/content` 是浏览器唯一看到的外部URL，用于保护您的外部用户对您下面的内容有所了解 `/apps` 树。 上述URL优势还有助于系统管理员设置更好的安全性，因为您将资产的泄露限制在几个不同的位置。
