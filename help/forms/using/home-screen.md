---
title: 主屏幕
seo-title: 主屏幕
description: AEM Forms应用程序主页屏幕的组件说明
seo-description: AEM Forms应用程序主页屏幕的组件说明
uuid: abc95e58-a685-42a9-82ab-4990155945d3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: ba79479b-4159-4a39-95eb-2285e7ece9d4
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 主屏幕{#home-screen}

当您登录到AEM Forms应用程序时，您将被重定向到主屏幕。

## 默认主页屏幕 {#default-home-screen}

默认情况下，主屏幕显示所有表单，包括起点和任务（如果连接的服务器启用了AEM Forms Workflow）以及关联的缩略图。 您可以在AEM Forms服务器中指定缩略图。

下图注释了默认“主页”屏幕上对基本组件的调用。

![表单应用程序主屏幕](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **菜单按钮**:点按菜 **单按钮** ，导航到任务、表单、发件箱和设置。 如果您的AEM Forms应用程序已连接到AEM Forms JEE服务器，则可以看到任务选项。 任务选项还存储从进程中的任务创建的草稿。 对于AEM Forms OSGi服务器，任务选项处于隐藏状态。 发件箱存储保存的表单和草稿，然后再与服务器同步。 当应用程序与服务器同步时，输出框中保存的所有表单和草稿将上传到AEM [表单服务器](../../forms/using/sync-app.md)。 有关设置的信息，请参阅更 [新常规设置](../../forms/using/update-general-settings.md)。
1. **任务或表单**:点按列出的任务或要处理的表单。
1. **水平省略号**:表示可对表单执行操作。 点击省略号会显示作者提供的操作和描述。 点 **击省略号时** ，将显 **** 示“删除草稿和完成”选项。
1. **刷新图标**:点按刷新图标以将应用程序与AEM Forms服务器同步。

### 自定义主屏幕 {#customizing-the-home-screen}

![常规设置](assets/gen-settings.png)

您可以从应用程序的“常规设置”或HTML工作区的“首 **[选项](../../forms/using/update-general-settings.md)******”选项卡中更改应用程序的默认“主页”屏幕。

对应用程序上的“主页”屏幕设置所做的更改会影响当前已记录的用户或当前移动设备上的用户的“主页”屏幕。

但是，在HTML Workspace中所做的更改会影响所有登录到AEM Forms服务器的AEM Forms应用程序用户。
