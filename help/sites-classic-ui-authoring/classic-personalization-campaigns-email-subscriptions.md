---
title: 管理訂閱
seo-title: Managing Subscriptions
description: 可透過AEM網頁上使用的表單元件，要求使用者訂閱電子郵件服務提供者的郵寄清單。 若要使用登錄檔單準備AEM頁面以訂閱您的電子郵件服務郵寄清單，您必須將對應的服務設定套用至潛在訂閱者將造訪的AEM頁面。
seo-description: Users can be asked to subscribe to Email Service Provider's mailing lists with the help of the Form component used on an AEM web page. To prepare an AEM page with a sign-up form for subscription to your e-mail service mailing lists, you must apply the corresponding service configuration to the AEM page that the potential subscriber will visit.
uuid: b2578a3d-dba1-4114-b21a-5f34c0cccc5a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 295cb0a6-29db-42aa-824e-9141b37b5086
exl-id: add05d22-3a11-49e9-a554-2315962552d5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---

# 管理訂閱{#managing-subscriptions}

>[!NOTE]
>
>Adobe不打算進一步增強此功能（管理銷售線索和清單）。
>建議善用 [Adobe Campaign及其AEM整合](/help/sites-administering/campaign.md).

可要求使用者訂閱 **電子郵件服務提供者的** 郵寄清單的協助 **表單** 用於AEM網頁的元件。 若要使用登錄檔單準備AEM頁面以訂閱您的電子郵件服務郵寄清單，您必須將對應的服務設定套用至潛在訂閱者將造訪的AEM頁面。

## 將電子郵件服務設定套用至頁面 {#applying-email-service-configuration-to-a-page}

若要設定AEM頁面：

1. 導覽至 **網站** 標籤。
1. 選取需要為服務設定的頁面。 以滑鼠右鍵按一下頁面並選取 **屬性**.

1. 選取 **Cloud Services** 則 **新增服務**. 從可用組態清單中選取組態。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 单击&#x200B;**确定**。

## 在AEM頁面上建立用於訂閱/取消訂閱清單的登錄檔單 {#creating-a-sign-up-form-on-an-aem-page-for-subscribing-unsubscribing-to-lists}

若要建立登錄檔單，並設定它以訂閱電子郵件服務提供者的郵寄清單：

1. 開啟使用者將造訪的AEM頁面。
1. 套用電子郵件服務提供者的設定至頁面。

1. 新增 **表單** 從sidekick拖曳元件至頁面。 如果元件無法使用，請切換到設計模式並啟用 **表單** 群組。
1. 按一下 **編輯** 在 **表單的開頭** 列並導覽至 **進階** 標籤。
1. 在 **表單** 下拉式功能表，選取 **電子郵件服務：建立訂閱者** 並新增至清單。
1. 在對話方塊底部，開啟 **動作設定** 下拉式清單，可讓您選取一或多個訂閱清單。
1. 在 **選取清單**，選取您要使用者訂閱的清單。 您可以使用加號按鈕(**新增專案**)。

   ![chlimage_1-10](assets/chlimage_1-10.jpeg)

   >[!NOTE]
   >
   >您的對話方塊可能會因電子郵件服務提供者而異。

1. 在 **表單** 索引標籤中，選取您希望在使用者提交表單後前往的感謝頁面（如果保留空白，表單會在提交時重新顯示）。 单击&#x200B;**确定**。一個 **電子郵件ID** 元件會顯示在表單中，可讓您建立表單，讓使用者提交其電子郵件地址以訂閱或取消訂閱郵寄清單。
1. 新增 **提交** 按鈕元件 **表單** sidekick區段。

   表單已準備就緒。 發佈上述步驟中設定的頁面以及 **感謝您** 頁面至發佈執行個體。 任何造訪頁面的潛在訂閱者都可以填寫表單並訂閱設定中提供的清單。

   >[!NOTE]
   >
   >若要讓表單訂閱功能正確運作， [需要在發佈執行個體上匯出和匯入作者提供的加密金鑰](#exporting-keys-from-author-and-importing-on-publish).

## 從作者匯出金鑰並在發佈時匯入 {#exporting-keys-from-author-and-importing-on-publish}

若要透過發佈執行個體上的登錄檔單來使用電子郵件服務訂閱和取消訂閱，您需要依照以下步驟操作：

1. 在作者執行個體上，導覽至「封裝管理員」。
1. 建立新封裝。 將篩選器設為 `/etc/key`.
1. 建置並下載套件。
1. 導覽至發佈執行個體上的封裝管理員，然後上傳此封裝。
1. 導覽至發佈osgi主控台，然後重新啟動名為的套件組合 **Adobe Granite Crypto支援**.

## 從清單中取消訂閱使用者 {#unsubscribing-users-from-lists}

若要取消訂閱清單中的使用者：

1. 開啟具有登錄檔單的AEM頁面的頁面屬性，以取消訂閱銷售機會。
1. 將服務組態套用至頁面。
1. 在頁面上建立登錄檔單。
1. 設定元件時，選取動作 **電子郵件服務**： **從清單中取消訂閱使用者。**
1. 從下拉式選單中，選取取消訂閱時從中移除使用者的適當清單。

   ![chlimage_1-11](assets/chlimage_1-11.jpeg)

1. 將金鑰從作者匯出至發佈。

## 設定電子郵件服務的自動回覆者電子郵件 {#configuring-auto-responder-emails-for-email-service}

若要為訂閱者設定自動回覆電子郵件：

1. 開啟具有登錄檔單的AEM頁面的頁面屬性，以設定潛在客戶的自動回應。
1. 將ExactTarget設定套用至頁面。

1. 新增 **表單** 從sidekick拖曳元件至頁面。 如果元件無法使用，請切換到設計模式並啟用 **表單** 群組。
1. 按一下 **編輯** 在 **表單的開頭** 列並導覽至 **進階** 標籤。
1. 在 **表單** 下拉式功能表，選取 **電子郵件服務：傳送自動回覆者電子郵件。**
1. **選取電子郵件** （這是以自動回應的電子郵件傳送的郵件）。

1. **選取分類** （此分類用於傳送電子郵件）。
1. 選取 **感謝您** 頁面（使用者提交表單後，會被導向到的頁面）。

   在 **表單** 索引標籤中，選取您希望在使用者提交表單後前往的感謝頁面。 （如果保留為空白，表單會在提交時重新顯示。） 单击&#x200B;**确定**。

1. 將金鑰從作者匯出至發佈。
1. 新增 **提交** 按鈕元件 **表單** sidekick區段。

   登錄檔單已準備就緒。 發佈上述步驟中設定的頁面以及 **感謝您** 頁面至發佈執行個體。 任何造訪頁面的潛在訂閱者皆可填寫表單，且訪客在提交表單時，將會收到填寫了表單之電子郵件ID的自動回覆電子郵件。

   >[!NOTE]
   >
   >若要讓登錄檔單訂閱正確運作， [需要在發佈執行個體上匯出和匯入作者提供的加密金鑰](#exporting-keys-from-author-and-importing-on-publish).

   ![chlimage_1-12](assets/chlimage_1-12.jpeg)
