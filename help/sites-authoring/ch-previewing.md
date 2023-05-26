---
title: 使用 ContextHub 数据预览页面
seo-title: Previewing Pages Using ContextHub Data
description: ContextHub 工具栏显示 ContextHub 存储区中的数据，并允许您更改存储区数据，该工具栏可用于预览内容
seo-description: The ContextHub toolbar displays data from ContextHub stores and enables you to change store data and  is useful for previewing content
uuid: 0150555a-0a92-4692-a706-bbe59fd34d6a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f281ef8c-0831-470c-acb7-189f20452a50
exl-id: 78673609-8cbc-4b4b-953e-56c31ea1b4ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 30%

---

# 使用 ContextHub 数据预览页面{#previewing-pages-using-contexthub-data}

此 [ContextHub](/help/sites-developing/contexthub.md) 工具栏显示ContextHub存储区中的数据，并允许您更改存储区数据。 ContextHub工具栏可用于预览由ContextHub存储区中的数据确定的内容。

工具栏包含一系列包含一个或多个UI模块的UI模式。

* UI模式是显示在工具栏左侧的图标。 单击或点按图标时，工具栏会显示它包含的UI模块。
* UI模块显示来自一个或多个ContextHub存储的数据。 某些UI模块还允许您操作存储数据。

ContextHub安装多个UI模式和UI模块。 您的管理员可能已 [已配置ContextHub](/help/sites-developing/ch-configuring.md) 以显示不同的标记。

![screen_shot_2018-03-23at093446](assets/screen_shot_2018-03-23at093446.png)

## 显示ContextHub工具栏 {#revealing-the-contexthub-toolbar}

ContextHub工具栏在预览模式下可用。 该工具栏仅在创作实例中且管理员已将其启用后才可用。

![screen_shot_2018-03-23at093730](assets/screen_shot_2018-03-23at093730.png)

1. 在打开页面以进行编辑时，在工具栏上单击或点按“预览”。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 要显示工具栏，请单击或点按 ContextHub 图标。

   ![](do-not-localize/screen_shot_2018-03-23at093621.png)

## UI模块功能 {#ui-module-features}

提供的每个UI模块都是一组不同的功能，但以下类型的功能是通用的。 由于UI模块是可扩展的，因此您的开发人员可以根据需要实施其他功能。

### 工具栏内容 {#toolbar-content}

UI 模块可以在工具栏中显示一个或多个 ContextHub 存储区中的数据。UI 模块使用图标和标题来标识自身。

![screen_shot_2018-03-23at093936](assets/screen_shot_2018-03-23at093936.png)

### 弹出窗口内容 {#popup-content}

某些UI模块在单击或点按时通常会显示弹出窗口。 通常，弹出窗口包含的信息比工具栏上显示的信息要多。

![screen_shot_2018-03-23at094003](assets/screen_shot_2018-03-23at094003.png)

### 弹出Forms {#popup-forms}

模块的弹出窗口叠加可以包含允许您更改ContextHub存储区中数据的表单元素。 如果页面内容由存储区数据决定，则可以使用表单并观察页面内容的更改。

### 全屏模式 {#fullscreen-mode}

弹出窗口叠加图可以包含图标，单击或点按该图标可展开弹出内容以覆盖整个浏览器窗口或屏幕。

![](do-not-localize/chlimage_1-18.png)
