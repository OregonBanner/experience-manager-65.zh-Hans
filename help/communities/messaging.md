---
title: 設定傳訊
seo-title: Configuring Messaging
description: Communities傳訊
seo-description: Communities messaging
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
role: Admin
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 1%

---

# 設定傳訊 {#configure-messaging}

## 概述 {#overview}

AEM Communities的傳訊功能可讓登入的網站訪客（成員）傳送訊息，讓彼此在登入網站時可存取。

透過以下步驟勾選方塊，為社群網站啟用傳訊： [社群網站建立](/help/communities/sites-console.md).

此頁面包含預設設定和可能調整的相關資訊。

如需開發人員的其他資訊，請參閱 [傳訊要點](/help/communities/essentials-messaging.md).

## 傳訊操作服務 {#messaging-operations-service}

設定 [AEM Communities傳訊操作服務](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) 會識別處理傳訊相關請求的端點、服務應用來儲存郵件的資料夾，以及如果郵件可能包含檔案附件，則允許哪些檔案型別。

針對使用建立的社群網站 `Communities Sites console`，服務的執行個體已存在，且收件匣設為 `/mail/inbox`.

### 社群傳訊操作服務 {#community-messaging-operations-service}

如下所示，使用建立的網站有此服務的設定 [網站建立精靈](/help/communities/sites-console.md). 選取設定旁邊的鉛筆圖示，即可檢視或編輯設定。

![傳訊作業](assets/messaging-operations.png)

### 添加新的配置 {#add-new-configuration}

若要新增設定，請選取加號&#39;**+**&#39;服務名稱旁的圖示：

* **訊息欄位允許清單**

   指定使用者可編輯及保留的撰寫訊息元件屬性。 如果新增了新表單元素，那麼如果需要儲存於SRP，則需要新增元素ID。 預設為兩個專案： *主旨* 和 *內容*.

* **訊息方塊大小限制**

   每位使用者訊息方塊中的最大位元組數。 預設為 *1073741824* (1 GB)。

* **訊息計數限制**

   每個使用者允許的訊息總數。 值–1表示允許無限數量的訊息，受訊息方塊大小限制。 預設為 *10000* (10k)。

* **通知傳遞失敗**

   如果勾選，則在郵件傳遞給某些收件者失敗時通知寄件者。 預設為 *已核取*.

* **失敗傳遞寄件者ID**

   顯示在傳送失敗訊息中的寄件者名稱。 預設為 *failureNotifier*.

* **失敗訊息範本路徑**

   傳遞失敗訊息範本根的絕對路徑。 預設為 */etc/notification/messaging/default*.

* **重試次數**

   嘗試重新傳送無法傳遞的訊息的次數。 預設為 *3*.

* **重試之間等待**

   在傳送失敗時嘗試重新傳送訊息之間等待的秒數。 預設為 *100* （秒）。

* **計算更新集區大小**

   用於計數更新的並行執行緒數目。 預設為 *10*.

* **收件匣路徑**

   (*必填*)相對於使用者節點(/home/users/)的路徑&#x200B;*使用者名稱*)，以用於 `inbox` 資料夾。 路徑不能以尾端正斜線&#39;/&#39;結尾。 預設為 */mail/inbox*.

* **已傳送專案路徑**

   (*必填*)相對於使用者節點(/home/users/)的路徑&#x200B;*使用者名稱*)，以用於 `sent items` 資料夾。 路徑不能以尾端正斜線&#39;/&#39;結尾。 預設為 */mail/sentitems* .

* **支援附件**

   如果勾選，使用者可以將附件新增至其郵件。 預設為 *已核取*.

* **啟用群組訊息**

   如果選取，註冊的使用者可以傳送大量訊息給一組成員。 預設為 *已取消選取*.

* **最大數量 收件者總數**

   如果已啟用群組訊息，請指定一次可傳送群組訊息的最大收件者數量。 預設為 *100*.

* **批量大小**

   傳送給大量收件者時，要一起批次傳送的訊息數。 預設為 *100*.

* **附件總大小**

   如果勾選supportAttachments，此值會指定所有附件允許的總大小上限（以位元組為單位）。 預設為 *104857600* (100 MB)。

* **附件型別封鎖清單**

   副檔名的封鎖清單，前置詞為「**.**&#39;，系統將會拒絕該專案。 如果未列入封鎖清單，則允許該擴充功能。 擴充功能可使用「**+**&#39;和&#39;**-**&#39;圖示。

* **允許的附件型別**

   **(*需要動作*)** 副檔名的允許清單，與封鎖清單相反。 若要允許所有副檔名（已列入封鎖清單者除外），請使用「**-**&#39;圖示可移除單一空白專案。

* **服务选择器**

   (*必填*)呼叫服務時所使用的絕對路徑（端點） （虛擬資源）。 所選路徑的根必須包含在 *執行路徑* OSGi設定的組態設定 [ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)，例如 `/bin/`， `/apps/`、和 `/services/`. 若要為網站的訊息功能選取此設定，此端點會提供為 **`Service selector`** 的值 `Message List and Compose Message components` (請參閱 [訊息功能](/help/communities/configure-messaging.md))。

   預設值為 */bin/messaging* .

* **欄位允許清單**

   使用 **訊息欄位允許清單**.

>[!CAUTION]
>
>每次 `Messaging Operations Service` 設定已開啟以供編輯，如果 `allowedAttachmentTypes.name` 已移除，則會重新新增空白專案，讓屬性可供設定。 單一空白專案會有效停用檔案附件。
>
>若要允許所有副檔名（已列入封鎖清單者除外），請使用「**-**&#39;圖示以（再次）在按一下前移除單一空白專案 **儲存**.

## 群組訊息 {#group-messaging}

若要允許註冊的使用者大量傳送直接訊息給使用者群組，請確定 **啟用群組訊息** 在以下兩個例項中 **傳訊操作服務** 設定：

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**訊息操作服務：社交主控台**

![social-console-op-service](assets/social-console-op-service.png)

**訊息操作服務：社交訊息**

![social-message-op-service](assets/social-message-op-service.png)

## 疑难解答 {#troubleshooting}

疑難排解的一種方法是啟用 [偵錯記錄檔中的訊息。](/help/sites-administering/troubleshooting.md)

另請參閱 [個別服務的記錄器及寫入器](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

要監視的套件是 `com.adobe.cq.social.messaging`.
