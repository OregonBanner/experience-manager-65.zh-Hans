---
title: 編輯啟動
description: 為您的頁面（或一組頁面）建立啟動後，您可以編輯頁面啟動副本中的內容。
uuid: 1f2c2e53-73a3-4bd7-b2c7-425491bc0118
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 30aa3177-bcf4-4260-8f64-e73bc907942a
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 2d441820-b394-47c8-b4ca-a8aede590937
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 38%

---

# 编辑启动项{#editing-launches}

## 編輯啟動頁面 {#editing-launch-pages}

為某個頁面（或一組頁面）建立啟動後，您可以編輯頁面啟動副本中的內容。

1. [从“引用”（站点控制台）中访问启动项](/help/sites-authoring/launches.md#launches-in-references-sites-console)以显示可用的操作。
1. 選取 **前往頁面** 以開啟頁面進行編輯。

>[!NOTE]
>
>您不能在启动项中移动页面。尝试此操作将触发警告消息：
>
>* 警告：此页面是启动项的源。不允许移动此页面。


### 编辑基于 Live Copy 的启动页面 {#editing-launch-pages-subject-to-a-live-copy}

如果您的啟動是根據 [即時副本](/help/sites-administering/msm.md) 然後您會：

* 編輯元件（內容和/或屬性）時，請參閱鎖定元件（小掛鎖）。
* 請參閱 **即時副本** 定位於 **頁面屬性**

Live Copy 用于将&#x200B;**&#x200B;源分支&#x200B;**&#x200B;中的内容同步到启动分支（以使启动项与源中所做的更改保持最新）。

您可以使用與編輯標準即時副本相同的方式進行變更；例如：

* 按一下已關閉的掛鎖將會中斷此同步處理，並允許您對啟動項中的內容進行新的更新。 一旦解除鎖定（開啟掛鎖），您所做的變更將不會被來源分支內相同位置所做的任何變更覆寫。
* 特定页面的&#x200B;**暂停**（和&#x200B;**继续**）继承。

另請參閱 [變更即時副本內容](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) 以取得進一步資訊。

## 比較啟動頁面與其來源頁面 {#comparing-a-launch-page-to-its-source-page}

要跟踪您所做的更改，您可以在&#x200B;**引用**&#x200B;中查看启动项，并将启动页面与其源页面进行比较：

1. 在 **網站** 主控台， [導覽至啟動項的來源頁面並加以選取](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources).
1. 開啟 **[引用](/help/sites-authoring/basic-handling.md#references)** 面板並選取 **啟動**.
1. 選取您的特定啟動，然後 **與來源比較**：

   ![screen-shot_2019-03-05at121952](assets/screen-shot_2019-03-05at121952.png)

1. 兩個頁面（啟動項和來源）將並排開啟。

   如需關於使用此功能的完整資訊，請參閱 [頁面差異](/help/sites-authoring/page-diff.md).

## 變更使用的來源頁面 {#changing-the-source-pages-used}

您可以随时向启动项的源页面范围中添加页面或从中删除页面：

1. 从以下任一位置访问并选择启动项：

   * 此 [啟動主控台](/help/sites-authoring/launches.md#the-launches-console)：

      * 选择&#x200B;**编辑**。
   * [引用（網站主控台）](/help/sites-authoring/launches.md#launches-in-references-sites-console) 若要顯示可用的動作：

      * 选择&#x200B;**编辑启动项**。

   將顯示來源頁面。

1. 进行所需的更改，然后使用&#x200B;**保存**&#x200B;进行确认。

   >[!NOTE]
   >
   >若要將頁面新增至啟動項，這些頁面必須位於共同語言根之下；即在單一網站內。

## 編輯Launch設定 {#editing-a-launch-configuration}

您可以随时编辑启动项的属性：

1. 从以下任一位置访问并选择启动项：

   * 此 [啟動主控台](/help/sites-authoring/launches.md#the-launches-console)：

      * 選取 **屬性**.
   * [引用（網站主控台）](/help/sites-authoring/launches.md#launches-in-references-sites-console) 若要顯示可用的動作：

      * 选择&#x200B;**编辑属性**。

   將顯示詳細資料。

1. 进行所需的更改，然后使用&#x200B;**保存**&#x200B;进行确认。

   有关启 [动日期和生产就绪字段的用途和交互的信息](/help/sites-authoring/launches.md#launches-the-order-of-events)******** ，请参阅启动项——事件的顺序。

## 探索頁面的啟動狀態 {#discovering-the-launch-status-of-a-page}

當您從「參考」標籤中選取特定啟動時，會顯示狀態(請參閱 [在參照（網站主控台）中啟動](/help/sites-authoring/launches.md#launches-in-references-sites-console))。

![screen-shot_2019-03-05at121901](assets/screen-shot_2019-03-05at121901.png)
