---
title: 發佈頁面
description: 在您於作者環境中建立並檢閱您的內容後，請將其開放在您的公開網站上使用。
uuid: ab5ffc59-1c41-46fe-904e-9fc67d7ead04
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 46d6bde0-8645-4cff-b79c-8e1615ba4ed4
docset: aem65
exl-id: 3f6aa06e-b5fd-4ab0-9ecc-14250cb3f55e
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 3%

---

# 发布页面{#publishing-pages}

在您於作者環境中建立並檢閱您的內容後，請將其放在您的公共網站（您的發佈環境）上。

這稱為發佈頁面。 當您想要從發佈環境中移除頁面時，會稱為取消發佈。 發佈和取消發佈頁面時，作者環境仍會提供頁面以供進一步變更，直到您刪除為止。

您也可以立即發佈/取消發佈頁面，或在預先定義的未來日期/時間發佈/取消發佈頁面。

>[!NOTE]
>
>某些與發佈相關的辭彙可能會混淆：
>
>* **发布/取消发布**
   >  这些是在发布环境中公开提供（或不公开提供）您的内容的主要操作术语。
>
>* **激活／取消激活**
   >  这两个术语与发布/取消发布同义。
>
>* **复制**
   >  這些是技術術語，說明資料（例如頁面內容、檔案、程式碼、使用者註解）從一個環境移動到另一個環境，例如發佈或反向複製使用者註解時。
>


>[!NOTE]
>
>如果您沒有發佈特定頁面所需的許可權：
>
>* 系統會觸發工作流程，將您要發佈的請求通知適當人員。
>* 將會顯示訊息（短時間內）以通知您此問題。
>


## 發佈頁面 {#publishing-a-page}

啟用頁面的方法有兩種：

* [從網站主控台](#activating-a-page-from-the-websites-console)
* [從頁面本身的sidekick](#activating-a-page-from-sidekick)

>[!NOTE]
>
>您也可以使用啟動多個頁面的子樹狀結構 [啟動樹狀結構](#howtoactivateacompletesectiontreeofyourwebsite) 工具主控台上的。

### 從網站主控台啟動頁面 {#activating-a-page-from-the-websites-console}

您可以在網站主控台中啟動頁面。 開啟頁面並修改其內容後，您會返回「網站」主控台：

1. 在「網站」主控台中，選取您要啟動的頁面。
1. 選取 **啟動**，可從頂端功能表或所選頁面專案上的下拉式功能表取得。

   若要啟用頁面及其所有子頁面的內容，請使用 [**工具** 主控台](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#howtoactivateacompletesectiontreeofyourwebsite).

   ![screen_shot_2012-02-08at13817pm](assets/screen_shot_2012-02-08at13817pm.png)

   >[!NOTE]
   >
   >必要時，AEM會要求您啟動或重新啟動連結至頁面的任何資產。 您可以選取或清除核取方塊以啟動這些資產。

1. 必要時，AEM會要求您啟動或重新啟動連結至頁面的任何資產。 您可以選取或清除核取方塊以啟動這些資產。

   ![chlimage_1-100](assets/chlimage_1-100.png)

1. AEM WCM會啟動選取的內容。 已發佈的一或多個頁面會顯示在 [網站主控台](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) （標籤為綠色），內含啟動內容者以及啟動日期和時間的資訊。

   ![screen_shot_2012-02-08at14335pm](assets/screen_shot_2012-02-08at14335pm.png)

### 從Sidekick啟動頁面 {#activating-a-page-from-sidekick}

您也可以在開啟頁面進行編輯時將其啟動。

開啟頁面並修改其內容後，您可以：

1. 選取 **頁面** tab鍵進入Sidekick。
1. 按一下 **啟動頁面**.
視窗右上方會顯示訊息，確認頁面已啟動。

## 取消發佈頁面 {#unpublishing-a-page}

若要從發佈環境移除頁面，請停用內容。

若要停用頁面：

1. 在「網站」主控台中，選取您要停用的頁面。
1. 選取 **停用**，可從頂端功能表或所選頁面專案上的下拉式功能表取得。 系統會要求您確認刪除。

   ![screen_shot_2012-02-08at14859pm](assets/screen_shot_2012-02-08at14859pm.png)

1. 重新整理 [網站主控台](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) 且內容會以紅色標示，表示其已不再發佈。

   ![screen_shot_2012-02-08at15018pm](assets/screen_shot_2012-02-08at15018pm.png)

## 稍後啟用/停用 {#activate-deactivate-later}

### 以后激活 {#activate-later}

若要排程您的啟動作業以供稍後使用：

1. 在網站主控台中，前往 **啟動** 功能表，然後選取 **稍後啟動**.
1. 在開啟的對話方塊中，您提供啟動日期和時間，然後按一下 **確定**. 這會建立會在指定時間啟動的頁面版本。

   ![screen_shot_2012-02-08at14751pm](assets/screen_shot_2012-02-08at14751pm.png)

稍後啟用會啟動工作流程，以在指定時間啟用此版本的頁面。 反之，稍後停用會啟動工作流程，以在特定時間停用此版本頁面。

若要取消此啟動/停用，請前往 [工作流程主控台](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) 以終止對應的工作流程。

### 稍后取消激活 {#deactivate-later}

若要排程稍後再停用：

1. 在網站主控台中，前往 **停用** 功能表，然後選取 **稍後停用**.

1. 在開啟的對話方塊中，您提供停用的日期和時間，然後按一下 **確定**.

   ![screen_shot_2012-02-08at15129pm](assets/screen_shot_2012-02-08at15129pm.png)

**延遲停用** r會啟動工作流程，以在特定時間停用此版本的頁面。

如果您要取消此停用，請前往 [工作流程主控台](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) 以終止對應的工作流程。

## 已排程的啟用/停用（開啟/關閉時間） {#scheduled-activation-deactivation-on-off-time}

您可以使用排程頁面發佈/取消發佈的時間 **準時** 和 **關閉時間** 可定義於 [頁面屬性](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

### 判斷頁面發佈狀態 {#determining-page-publication-status-classic-ui}

可以從以下位置檢視狀態： [網站主控台](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console). 顏色指示出版狀態。

## 啟用網站的完整區段（樹狀結構） {#activating-a-complete-section-tree-of-your-website}

從 **網站** 標籤您可以啟動個別頁面。 當您輸入或更新了大量內容頁面時 — 所有內容頁面都位於同一個根頁面下 — 可以更輕鬆地在一次動作中啟用整個樹狀結構。 您也可以執行「試用」來模擬啟用，並反白要啟用的頁面。

1. 開啟 **工具** 從控制檯中選取它 **歡迎** 頁面，然後按兩下 **復寫** 以開啟主控台( `https://localhost:4502/etc/replication.html`)。

   ![screen_shot_2012-02-08at125033pm](assets/screen_shot_2012-02-08at125033pm.png)

1. 於 **復寫** 主控台，按一下 **啟動樹狀結構**.

   下列視窗( `https://localhost:4502/etc/replication/treeactivation.html`)將會顯示。

   ![screen_shot_2012-02-08at125033pm-1](assets/screen_shot_2012-02-08at125033pm-1.png)

1. 輸入 **開始路徑**. 這會指定您要啟動（發佈）之區段的根路徑。 系統會將此頁面及其下方的所有頁面視為啟動（或如果選取「試用」，則用於模擬）。
1. 視需要啟動選取條件：

   * **僅限已修改的專案**：僅啟用已修改的頁面。
   * **僅限已啟動**：僅啟動（已）已啟動的頁面。 作為重新啟用的一種形式。
   * **忽略已停用的專案**：忽略任何已停用的頁面。

1. 選取您要執行的動作：

   1. 選取 **練習** 如果您要檢查哪些頁面 *會* 已啟用。 這只是模擬，不會啟用任何頁面。

   1. 選取 **啟動** 如果您想要啟動頁面。
