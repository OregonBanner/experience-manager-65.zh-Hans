---
title: 從「工作管理員」資料庫中清除記錄
seo-title: Purge records from the Job Manager database
description: 大型程式資料可能會導致AEM表單效能降低。 當不再需要記錄時，清除程式資料是很好的做法。
seo-description: Large process data can result in lower AEM forms performance. It is good practice to purge process data when records are no longer necessary.
uuid: cf214498-36e9-4dcc-b4d4-e7c46f80dbab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 69a406f2-4fa8-40bb-b671-7b0f5b6a2c4c
exl-id: 5279f6c3-5954-472c-9ea0-18e8a7ec860e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 從「工作管理員」資料庫中清除記錄 {#purge-records-from-the-job-manager-database}

叫用長期處理程式時產生的處理程式資料可能會變得太大，導致AEM表單效能降低及使用不必要的磁碟空間。 當不再需要記錄時，清除程式資料是很好的做法。

您可以使用管理主控台來執行一次性永久刪除過時記錄，或排定定期自動永久刪除。 有關清除過時記錄的其他方法，請參閱 [清除程式資料](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**存取「工作清除排程器」頁面**

1. 在Administration Console中，按一下頁面右上角的「健全狀況監視器」 。
1. 按一下「工作清除排程器」頁標。

有關目前排定清除的資訊會顯示在「工作清除排程器資訊」方塊中。

>[!NOTE]
>
>按一下「停止排程器」可停止未來排定的任何永久刪除，但不會停止已經進行的永久刪除工作。

**排程一次性整個清除**

1. 只選取一次。
1. 在「永久刪除完成的記錄篩選」區域中，指定將記錄視為過時並準備永久刪除的天數或周數。

   >[!NOTE]
   >
   >系統不會清除與尚未完成的處理程式相關的記錄，即使這些記錄比指定的期限還舊。

1. 指定何時進行清除。 選取使用目前的日期和時間核取方塊，或清除核取方塊並按一下日曆和時鐘圖示以指定執行清除的日期和時間。

   >[!NOTE]
   >
   >如果您指定的開始日期與時間是過去的時間，則按一下「開始排程器」時，清除會立即發生。

1. 按一下「啟動排程器」。 任何先前排程的排程器設定會取代為新設定。

**設定自動清除排程**

1. 選取遞回間隔並指定兩次清除之間的天數或周數。
1. 在「永久刪除完成的記錄篩選」區域中，指定將記錄視為過時並準備永久刪除的天數或周數。 您不能將值設為 `0`.

   >[!NOTE]
   >
   >系統不會清除與尚未完成的處理程式相關的記錄，即使這些記錄比指定的期限還舊。

1. 指定開始清除的時間。 選取使用目前的日期和時間核取方塊，或清除核取方塊並按一下日曆和時鐘圖示以指定執行清除的日期和時間。

   >[!NOTE]
   >
   >如果您指定的開始日期和時間是過去的時間，AEM forms會根據您指定的日期計算合理的下一個開始日期。 例如，如果您排程從4月7日開始每週進行工作清除，現在為4月9日，則第一次清除會於4月14日進行。

1. 按一下「啟動排程器」。 任何先前排程的排程器設定會取代為新設定。
