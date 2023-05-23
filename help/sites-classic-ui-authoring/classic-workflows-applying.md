---
title: 将工作流应用于页面
description: 工作流程可以從「網站」主控台啟動，或在編輯頁面時從Sidekick啟動。
uuid: 55f6f1d7-da54-4732-b9ff-b7479622db51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 22712b73-90f2-4329-b32f-dbb7ce802d1d
exl-id: d8b604c5-a6da-47c4-9422-b519e224c7ca
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 11%

---

# 将工作流应用于页面{#applying-workflows-to-pages}

套用工作流程時，請指定下列資訊：

* 要应用的工作流。

   您可以应用任何工作流（您有权访问，由 AEM 管理员分配）。
* 選擇性：

   * 提供啟動工作流程之原因相關資訊的註解。
   * 有助於識別使用者收件匣中工作流程例項的標題。

>[!NOTE]
>
>AEM管理員可以使用以下專案開始工作流程： [其他幾個方法](/help/sites-administering/workflows-starting.md).

## 套用工作流程 {#applying-workflows}

工作流程可以從「網站」主控台啟動，或在編輯頁面時從Sidekick啟動。

此 **狀態** 中的欄 **網站** console會指出工作流程是否已套用至頁面：

![workflowstatus](assets/workflowstatus.png)

### 從網站主控台啟動工作流程 {#starting-a-workflow-from-the-websites-console}

1. 開啟網站主控台。 ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. 在網站樹狀結構中，選取您要套用工作流程的頁面的父頁面。
1. 在頁面清單中，選取頁面，然後按一下「工作流程」。
1. 在「開始工作流程」對話方塊中，選取要套用的工作流程。 或者，輸入評論和標題。 然後，按一下「開始」。

### 使用Sidekick啟動工作流程 {#starting-a-workflow-using-sidekick}

1. 開啟網站主控台。
1. 開啟必要頁面。
1. 從Sidekick中選取「工作流程」標籤。
1. 展開 **工作流程** 對話方塊，讓您選取 **工作流程** 並選擇性地輸入 **工作流程標題** 和 **註解**.

   ![workflowstartsidekick](assets/workflowstartsidekick.png)

1. 按一下 **開始工作流程** 以啟動新的工作流程例項，其中包含您設定的屬性以及目前頁面作為裝載。 現在工作流程正在執行中。
