---
title: 主屏幕
seo-title: 主屏幕
description: AEM Forms应用程序主屏幕组件的描述
seo-description: AEM Forms应用程序主屏幕组件的描述
uuid: abc95e58-a685-42a9-82ab-4990155945d3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: ba79479b-4159-4a39-95eb-2285e7ece9d4
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 主屏幕{#home-screen}

登录AEM Forms应用程序后，您将被重定向到主屏幕。

## 默认主屏幕{#default-home-screen}

默认情况下，主屏幕显示所有表单，包括起点和任务(如果连接的服务器启用了AEM Forms工作流)以及关联的缩略图。 您可以在AEM Forms服务器中指定缩略图。

下图用默认主屏幕上基本组件的标注进行了说明。

![Forms应用程序主屏幕](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **菜单按钮**:点按菜 **** 单按钮，导航到任务、Forms、发件箱和设置。如果您的AEM Forms应用程序已连接到AEM Forms JEE服务器，则可以看到任务选项。 “任务”选项还存储从进程中的任务创建的草稿。 对于AEM Forms OSGi服务器，任务选项处于隐藏状态。 发件箱在与服务器同步之前会存储保存的表单和草稿。 当应用程序与服务器](../../forms/using/sync-app.md)同步时，发件箱中保存的所有表单和草稿都会上传到AEM Forms服务器。 [有关“设置”的信息，请参阅[更新常规设置](../../forms/using/update-general-settings.md)。
1. **任务或表单**:点按要处理的列出任务或表单。
1. **水平省略号**:表示操作可用于表单。点按省略号会显示作者提供的操作和描述。 点按省略号时，将显示&#x200B;**删除草稿**&#x200B;和&#x200B;**完成**&#x200B;选项。
1. **“刷新”图标**:点按刷新图标，将您的应用程序与AEM Forms服务器同步。

### 自定义主屏幕{#customizing-the-home-screen}

![常规设置](assets/gen-settings.png)

您可以从应用程序的&#x200B;**[常规设置](../../forms/using/update-general-settings.md)**&#x200B;或HTML工作区的&#x200B;**首选项**&#x200B;选项卡中更改应用程序的默认主屏幕。

对应用程序上的主屏幕设置所做的更改会影响当前已记录用户或当前移动设备用户的主屏幕。

但是，在HTML工作区中所做的更改会影响所有登录到AEM Forms服务器的AEM Forms应用程序用户。
