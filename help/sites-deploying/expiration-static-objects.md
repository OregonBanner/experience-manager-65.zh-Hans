---
title: 靜態物件的到期日
seo-title: Expiration of Static Objects
description: 瞭解如何設定AEM，讓靜態物件不會在合理時間內過期。
seo-description: Learn how to configure AEM so that static objects do not expire (for a reasonable period of time).
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
feature: Configuring
exl-id: bfd5441c-19cc-4fa8-b597-b1221465f75d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# 靜態物件的到期日{#expiration-of-static-objects}

靜態物件（例如圖示）不會變更。 因此，系統應設定為不會過期（在合理的時間段內），並減少不必要的流量。

這會造成下列影響：

* 從伺服器基礎結構解除安裝請求。
* 當瀏覽器快取瀏覽器快取中的物件時，提高頁面載入的效能。

到期日由HTTP標準所指定，內容與檔案的「到期日」有關(請參閱 [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) 「超文字傳輸通訊協定 — HTTP 1.1」)。 此標準會使用標頭來允許使用者端快取物件，直到它們被視為過時；此類物件會快取指定的時間量，而不會對原始伺服器進行任何狀態檢查。

>[!NOTE]
>
>此設定與Dispatcher完全不同（且無法運作）。
>
>Dispatcher的用途是將資料快取到AEM前面。

所有非動態且不會隨著時間改變的檔案，都可以且應該快取。 Apache HTTPD伺服器的設定可能如下所示 — 視環境而定：

>[!CAUTION]
>
>定義將物件視為最新的時段時，您必須小心。 如有 *在指定的時段到期之前不檢查*，使用者端最後可能會從快取中顯示舊內容。

1. **對於作者執行個體：**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   這可讓中繼快取（例如瀏覽器快取）將CSS、Javascript、PNG和GIF檔案儲存一個月，直到檔案過期為止。 這表示它們不需要從AEM或Web伺服器要求，但可以保留在瀏覽器快取中。

   網站的其他區段不應在製作執行個體上快取，因為它們隨時可能變更。

1. **對於發佈執行個體：**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /content>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   <Location /etc/designs>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   ```

   這可讓中繼快取（例如瀏覽器快取）將CSS、Javascript、PNG和GIF檔案儲存在使用者端快取中最多一天。 雖然此範例說明以下所有專案的全域設定 `/content` 和 `/etc/designs`，您應該讓它更精細。

   根據網站更新的頻率，您也可以考慮快取HTML頁面。 一個合理的時間段是1小時：

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

設定靜態物件後，請掃描 `request.log`，同時選取包含這類物件的頁面，以確認沒有對靜態物件發出任何（不必要的）請求。
