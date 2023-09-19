---
title: 主屏幕
description: AEM Forms应用程序主屏幕的组件描述
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
source-git-commit: 65c5a4442f17e6bc52deaa1588f535a05698083f
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 主屏幕{#home-screen}

登录AEM Forms应用程序时，您将被重定向到主屏幕。

## 默认主屏幕 {#default-home-screen}

默认情况下，主屏幕会显示所有表单，包括起点和任务(如果连接的服务器启用了AEM Forms Workflow)，以及关联的缩略图。 您可以在AEM Forms服务器中指定缩略图。

下图在默认的“主页”屏幕上用重要组件的标注进行注释。

![Forms应用程序主屏幕](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **菜单按钮**：点按 **菜单** 按钮以导航到“任务”、“Forms”、“发件箱”和“设置”。 如果您的AEM Forms应用程序已连接到AEM Forms JEE服务器，则可以看到任务选项。 “任务”选项还存储从进程中的任务创建的草稿。 对于AEM Forms OSGi服务器，任务选项是隐藏的。 Outbox在与服务器同步之前存储已保存的表单和草稿。 当应用程序处于以下状态时，发件箱中所有保存的表单和草稿都将上传到AEM Forms服务器 [与服务器同步](../../forms/using/sync-app.md). 有关设置的信息，请参阅 [更新常规设置](../../forms/using/update-general-settings.md).
1. **任务或表单**：点按列出的要处理的任务或表单。
1. **水平省略号**：表示操作对表单可用。 点按省略号会显示作者提供的操作和描述。 此 **删除草稿** 和 **完成** 选项在点击省略号时可见。
1. **“刷新”图标**：点按刷新图标，以便您可以将应用程序与AEM Forms服务器同步。

### 自定义主屏幕 {#customizing-the-home-screen}

![常规设置](assets/gen-settings.png)

您可以从以下位置更改应用程序的默认主屏幕： **[常规设置](../../forms/using/update-general-settings.md)** ，或从应用程序 **首选项** HTML选项卡。

对应用程序上的主屏幕设置所做的更改会影响当前登录用户或当前移动设备上的用户的主屏幕。

但是，在HTML工作区中所做的更改将会影响登录到AEM Forms服务器的所有AEM Forms应用程序用户。
