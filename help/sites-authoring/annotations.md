---
title: 編輯內容頁面時的註解
description: 許多與內容直接相關的元件可讓您新增附註。
uuid: 157be55c-8ab8-472e-be32-0dcc02bfa41d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: aa89326a-ad33-4b0b-8d09-c68c5a5c790a
exl-id: de1ae7e3-db3a-4b5e-8a4f-ae111227181f
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 40%

---

# 編輯頁面時的註解{#annotations-when-editing-a-page}

在實際發佈內容之前，通常需要先進行討論，才能將內容新增至網站的頁面。 為了協助此功能，許多與內容直接相關的元件（例如，與版面配置相反）可讓您新增附註。

註解會在頁面上放置彩色標籤/註解。 您（或其他用户）可以通过注释给其他作者/审阅人留下意见和/或问题。

>[!NOTE]
>
>单个组件类型的定义决定是否可在该组件的实例中添加注释。

>[!NOTE]
>
>在傳統UI中建立的註解將顯示在觸控式UI中。 不過，草圖是UI專屬的，而且只會在建立草圖的UI中顯示。

>[!CAUTION]
>
>刪除資源（例如段落）會刪除附加到該資源的所有註釋和草圖，無論這些註釋和草圖在整個頁面上的位置為何。

>[!NOTE]
>
>根据您的要求，您还可以开发一个工作流，用于在添加、更新或删除注释时发送通知。

## 注释 {#annotations}

这是一种特殊的[模式](/help/sites-authoring/author-environment-tools.md#page-modes)，可用于创建和查看注释。

>[!NOTE]
>
>请不要忘记，[评论](/help/sites-authoring/basic-handling.md#timeline)也可用于在页面中提供反馈。

>[!NOTE]
>
>您可以為各種資源加上註解：
>
>* [為資產加上註釋](/help/assets/manage-assets.md#annotating)
>* [為視訊資產加上註釋](/help/assets/managing-video-assets.md#annotate-video-assets)
>


### 对组件添加注释 {#annotating-a-component}

「註釋」模式可讓您在內容上建立、編輯、移動或刪除註釋：

1. 編輯頁面時，您可以使用工具列（右上方）中的圖示來進入附註模式：

   ![](do-not-localize/screen_shot_2018-03-22at110414.png)

   此时，您可以查看任何现有的注释。

   >[!NOTE]
   >
   >若要退出「註釋」模式，請點選/按一下頂端工具列右側的「註釋」圖示（x符號）。

1. 单击/点按“添加注释”图标（工具栏左侧的加号）以开始添加注释。

   >[!NOTE]
   >
   >若要停止新增註解（並返回檢視），請點選/按一下頂端工具列左側的「取消」圖示（白色圓圈中的x符號）。

1. 按一下/點選所需的元件（可加上註解的元件將以藍色邊框反白顯示）以新增註解，然後開啟對話方塊：

   ![screen_shot_2018-03-22at110606](assets/screen_shot_2018-03-22at110606.png)

   在這裡，您可以使用適當的欄位和/或圖示來：

   * 輸入註釋文字。
   * 创建草图（线和形状）以突出显示组件的某个区域。


      建立草繪時，游標會變成十字線。 您可以绘制多条不同的线。草图线反映注释颜色，可为箭头、圆环或椭圆环。
   ![](do-not-localize/screen_shot_2018-03-22at110640.png)

   * 选择/更改颜色：

   ![](do-not-localize/chlimage_1-19.png)

   * 删除注释。

   ![](do-not-localize/screen_shot_2018-03-22at110647.png)

1. 您可以按一下/點選註釋對話方塊，關閉對話方塊。 隨即顯示截斷的註釋檢視（第一個字）以及任何草圖：

   ![screen_shot_2018-03-22at110850](assets/screen_shot_2018-03-22at110850.png)

1. 完成特定注释编辑之后，您可以：

   * 单击/点按文本标记以打开注释。開啟後，您可以檢視全文、進行變更或刪除註釋。

      * 不能獨立於註釋刪除草圖。
   * 调整文本标记位置。
   * 单击/点按草图线以选择该草图，然后将其拖动到所需位置。
   * 移動或複製元件

      * 任何相關的註釋及其草繪也會移動或複製，而且它們相對於段落的位置將保持不變。


1. 若要退出「註釋」模式並返回先前使用的模式，請點選/按一下頂端工具列右側的「註釋」圖示（x符號）。

>[!NOTE]
>
>无法将注释添加到其他用户已锁定的页面。

### 注释指示器 {#annotation-indicator}

在“编辑”模式下不会显示注释，但工具栏右上方的徽章会显示当前页面存在的注释数。该徽章取代了默认的“注释”图标，但还可用作打开/关闭“注释”模式的快速链接：

![chlimage_1-242](assets/chlimage_1-242.png)
