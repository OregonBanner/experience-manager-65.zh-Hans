---
title: AEM 6中的稽核記錄維護
seo-title: Audit Log Maintenance in AEM 6
description: 瞭解AEM中的稽核記錄維護。
seo-description: Lear about Audit Log Maintenance in AEM.
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# AEM 6中的稽核記錄維護{#audit-log-maintenance-in-aem}

符合稽核記錄資格的AEM事件會產生許多封存的資料。 由於複製、資產上傳和其他系統活動，這些資料會隨著時間快速成長。

「稽核記錄維護」包含幾個部分功能，可讓您根據特定原則自動進行稽核記錄維護。

它是作為可設定的每週維護任務實作，並可透過Operations Dashboard監控主控台存取。

如需詳細資訊，請參閱 [操作儀表板檔案](/help/sites-administering/operations-dashboard.md).

「稽核記錄清除」選項有三種型別：

1. [頁面稽核記錄清除](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [DAM稽核記錄清除](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [復寫稽核記錄檔期間](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

每一個都可透過在AEM Web Console中建立規則來設定。 設定完成後，您可以前往 **工具 — 作業 — 維護 — 每週維護視窗** 並執行 **稽核記錄維護任務**.

## 設定頁面稽核記錄清除 {#configure-page-audit-log-purging}

若要設定「稽核記錄永久刪除」，請依照下列步驟執行：

1. 將您的瀏覽器指向，前往Web Console Admin `http://localhost:4502/system/console/configMgr/`

1. 搜尋名為的專案 **頁面稽核記錄清除規則** 並按一下。

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. 接下來，根據您的需求設定清除排程器。 可用的选项为：

   * **規則名稱：** 稽核策略規則的名稱；
   * **內容路徑：** 將套用規則之內容的路徑；
   * **最小年齡：** 需要保留稽核記錄的天數；
   * **稽核記錄型別：** 應清除的稽核記錄型別。

   >[!NOTE]
   >
   >內容路徑僅適用於 `/var/audit/com.day.cq.wcm.core.page` 存放庫中的節點。

1. 儲存規則。
1. 您剛才建立的規則必須顯示在「操作控制面板」中，才能執行。 若要這麼做，請前往 **工具 — 作業 — 維護** 從AEM歡迎畫面。

1. 按下 **每週維護期間** 卡片。

1. 您會發現維護任務已存在於下方 **稽核記錄維護任務** 卡片。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 您可以檢查下一次執行的日期、進行設定，或按播放按鈕手動執行。

在AEM 6.3中，如果排定的維護視窗在「稽核記錄清除」作業完成之前關閉，作業會自動停止。 當下一個維護視窗開啟時，它會繼續。

**使用AEM 6.5**，您可以按一下「 」以手動停止執行中的「稽核記錄清除任務」。 **停止** 圖示。 在下次執行時，工作將安全地繼續。

>[!NOTE]
>
>若要停止維護任務，表示要暫停其執行，而不會失去已進行中工作的追蹤。

## 設定DAM稽核記錄清除 {#configure-dam-audit-log-purging}

1. 瀏覽至「系統主控台」，網址為 *https://&lt;serveraddress>：&lt;serverport>/system/console/configMgr*
1. 搜尋 **DAM稽核記錄清除** 規則並按一下結果。
1. 在下一個視窗中，相應地設定規則。 選項包括：

   * **規則名稱：** 稽核策略規則的名稱；
   * **內容路徑：** 規則將套用到的內容路徑
   * **最小年齡：** 需要保留稽核記錄的時間（天）
   * **稽核記錄Dam事件型別：** 應清除的DAM稽核事件型別。

1. 按一下 **儲存** 以儲存您的設定

## 設定復寫稽核記錄清除  {#configure-replication-audit-log-purging}

1. 瀏覽至「系統主控台」，網址為 *https://&lt;serveraddress>：&lt;serverport>/system/console/configMgr*
1. 搜尋 **復寫稽核記錄清除排程器** 並按一下結果
1. 在下一個視窗中，相應地設定規則。 選項包括：

   * **規則名稱：** 稽核策略規則的名稱
   * **內容路徑：** 規則將套用到的內容路徑
   * **最小年齡：** 需要保留稽核記錄的時間（天）
   * **稽核記錄復寫事件型別：** 應清除的復寫稽核事件型別

1. 按一下 **儲存** 以儲存您的設定。
