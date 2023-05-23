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

此 [ContextHub](/help/sites-developing/contexthub.md) 工具列會顯示ContextHub存放區中的資料，並可讓您變更存放區資料。 ContextHub工具列可用於預覽由ContextHub存放區中的資料所決定的內容。

工具列包含一系列包含一或多個UI模組的UI模式。

* UI模式是出現在工具列左側的圖示。 按一下或點選圖示時，工具列會顯示其中的UI模組。
* UI模組會顯示一或多個ContextHub存放區的資料。 有些UI模組也可讓您操控存放區資料。

ContextHub會安裝數個UI模式和UI模組。 您的管理員可能會 [已設定的ContextHub](/help/sites-developing/ch-configuring.md) 以顯示不同的值。

![screen_shot_2018-03-23at093446](assets/screen_shot_2018-03-23at093446.png)

## 顯示ContextHub工具列 {#revealing-the-contexthub-toolbar}

ContextHub工具列可在「預覽」模式下使用。 该工具栏仅在创作实例中且管理员已将其启用后才可用。

![screen_shot_2018-03-23at093730](assets/screen_shot_2018-03-23at093730.png)

1. 在打开页面以进行编辑时，在工具栏上单击或点按“预览”。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 要显示工具栏，请单击或点按 ContextHub 图标。

   ![](do-not-localize/screen_shot_2018-03-23at093621.png)

## UI模組功能 {#ui-module-features}

提供的每個UI模組都是一組不同的功能，但以下型別的功能很常見。 由於UI模組是可擴充的，因此您的開發人員可以根據需要實作其他功能。

### 工具列內容 {#toolbar-content}

UI 模块可以在工具栏中显示一个或多个 ContextHub 存储区中的数据。UI 模块使用图标和标题来标识自身。

![screen_shot_2018-03-23at093936](assets/screen_shot_2018-03-23at093936.png)

### 弹出窗口内容 {#popup-content}

有些UI模組在點選或點選時通常會顯示快顯視窗。 通常，弹出窗口包含的信息比工具栏上显示的信息要多。

![screen_shot_2018-03-23at094003](assets/screen_shot_2018-03-23at094003.png)

### 快顯視窗Forms {#popup-forms}

模組的彈出式覆蓋圖可包含可讓您變更ContextHub存放區中資料的表單元素。 如果頁面內容由商店資料決定，您可以使用表單並觀察頁面內容的變更。

### 全屏模式 {#fullscreen-mode}

彈出式覆蓋圖可包含您按一下或點選以展開彈出式內容的圖示，以涵蓋整個瀏覽器視窗或熒幕。

![](do-not-localize/chlimage_1-18.png)
