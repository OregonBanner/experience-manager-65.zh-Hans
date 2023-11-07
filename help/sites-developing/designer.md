---
title: 设计和设计器
description: 了解如何使用设计器为您的网站和AEM创建设计。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: c81c5910-b6c9-41bd-8840-a6782792701f
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 设计和设计器{#designs-and-the-designer}

>[!CAUTION]
>
>本文介绍了如何基于经典UI创建网站。 Adobe建议为您的网站使用最新的AEM技术，如文章中详述 [AEM Sites开发入门](/help/sites-developing/getting-started.md).

可使用设计器为您的网站创建设计 [经典UI](/help/release-notes/touch-ui-features-status.md) 在AEM中。

>[!NOTE]
>
>有关Web辅助功能的详细信息，请参阅 [AEM和Web无障碍准则](/help/managing/web-accessibility.md).

## 使用设计器 {#using-the-designer}

您的设计可以在以下位置定义： **设计** 的部分 **工具** 选项卡：

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

您可以在此处创建存储设计所需的结构，然后上载所需的层叠样式表和图像。

设计存储在下 `/apps/<your-project>`. 使用指定用于网站的设计的路径 `cq:designPath` 的属性 `jcr:content` 节点。

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>在设计模式下对页面所做的所有更改将保留在网站的设计节点下，并自动应用于具有相同设计的所有页面。

## 您将需要什么 {#what-you-will-need}

要实现您的设计，您需要：

**CSS**  — 层叠样式表定义页面上特定区域的格式。
**图像**  — 用于特征（如背景、按钮）的任何图像。

### 设计网站时的注意事项 {#considerations-when-designing-your-website}

在开发网站时，强烈建议将图像和CSS文件存储在 `/apps/<your-project>` 因此，您可以根据当前设计引用资源，如以下代码片段所述。

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

上述示例提供了多种好处：

* 组件可以使用不同的设计路径根据每个站点具有不同的外观。
* 网站的重新设计可以简单地通过将设计路径指向位于网站根目录中的不同节点来完成 `design/v1` 到 `design/v2.`

* `/etc/designs` 和 `/content` 是浏览器看到的唯一外部URL，当外部用户对 `/apps` 树。 上述URL好处还可帮助系统管理员设置更好的安全性，因为您将资产暴露限制在几个不同的位置。
