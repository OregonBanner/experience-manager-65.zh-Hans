---
title: 電子郵件行銷
seo-title: E-mail Marketing
description: 電子郵件行銷（例如電子報）是任何行銷活動的重要部分，因為您會使用電子郵件行銷活動將內容推播給潛在客戶。 在AEM中，您可以從現有AEM內容建立電子報，也可以新增電子報專屬的新內容。
seo-description: E-mail marketing (for example, newsletters) are an important part of any marketing campaign as you use them to push content to your leads. In AEM, you can create newsletters from existing AEM content as well as add new content, specific to the newsletters.
uuid: 565943bf-fe37-4d5c-98c3-7c629c4ba264
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 69ca5acb-83f9-4e1b-9639-ec305779c931
docset: aem65
exl-id: a1d8b74e-67eb-4338-9e8e-fd693b1dbd48
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 1%

---

# 電子郵件行銷{#e-mail-marketing}

>[!NOTE]
>
>Adobe不打算進一步增強AEM SMTP服務所傳送開啟/彈回（無法傳遞）的電子郵件追蹤。
>建議為 [善用Adobe Campaign以及與AEM的整合](/help/sites-administering/campaign.md).

電子郵件行銷（例如電子報）是任何行銷活動的重要部分，因為您會使用電子郵件行銷活動將內容推播給潛在客戶。 在AEM中，您可以從現有AEM內容建立電子報，也可以新增電子報專屬的新內容。

建立後，您可以立即或在另一個排程時間（透過使用工作流程）將電子報傳送給特定使用者群組。 此外，使用者可以選擇格式訂閱電子報。

此外，AEM可讓您管理新聞稿功能，包括維護主題、封存新聞稿和檢視新聞稿統計資料。

>[!NOTE]
>
>在Geometrixx中，電子報範本會自動開啟電子郵件編輯器。 您可以在想要傳送電子郵件的其他範本（例如邀請）中使用電子郵件編輯器。 電子郵件編輯器會在頁面繼承自時隨即顯示 **mcm/components/newsletter/page**.

本檔案說明在AEM中建立電子報的基本概念。 如需如何使用電子郵件行銷的詳細資訊，請參閱下列檔案：

* [建立有效的Newsletter登陸頁面](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-landingpage.md)
* [管理訂閱](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-subscriptions.md)
* [發佈電子郵件給電子郵件服務提供者](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-newsletters.md)
* [追蹤退信電子郵件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-tracking-bounces.md)

>[!NOTE]
>
>如果您更新電子郵件提供者、進行快速測試或傳送電子報，如果電子報未先發佈至發佈執行個體，或發佈執行個體無法使用，則這些作業會失敗。 請務必發佈您的Newsletter，並確保Publish執行個體已啟動且執行中。

## 建立Newsletter體驗 {#creating-a-newsletter-experience}

>[!NOTE]
>
>需要透過osgi設定來設定電子郵件通知。 另請參閱 [設定電子郵件通知。](/help/sites-administering/notification.md)

1. 在左窗格中選取新的行銷活動，或在右窗格中連按兩下。

1. 使用圖示選取清單檢視：

   ![](do-not-localize/mcm_icon_listview-1.png)

1. 按一下 **新增……**

   您可以指定 **標題**， **名稱** 以及要建立的體驗型別；在此案例中為Newsletter。

   ![mcm_createnewsletter](assets/mcm_createnewsletter.png)

1. 单击&#x200B;**创建**。

1. 隨即會立即開啟新的對話方塊。 您可以在此處輸入Newsletter的屬性。

   此 **預設收件者清單** 為必填欄位，因為這會形成電子報的接觸點(請參閱 [使用清單](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists) 以取得清單的詳細資訊)。

   ![mcm_newsletterdialog](assets/mcm_newnewsletterdialog.png)

   * **發件人名稱**
應顯示為Newsletter寄件者的名稱。

   * **寄件者地址**
應顯示為Newsletter寄件者的郵件地址。

   * **主旨**
Newsletter的主題。

   * **回覆**
郵件地址，負責處理已傳送Newsletter的回覆。

   * **說明**
Newsletter的說明。

   * **準時**
傳送Newsletter的準時。

   * **預設收件者清單**
應接收Newsletter的預設清單。
   這些可在稍後階段從 **屬性……** 對話方塊。

1. 按一下 **確定** 以儲存。

## 新增內容至電子報 {#adding-content-to-newsletters}

您可以像在任何AEM元件中一樣新增內容（包括動態內容）至您的電子報。 在Geometrixx中， Newsletter範本有某些元件可用於新增和修改電子報的內容。

1. 在MCM中，按一下 **行銷活動** 索引標籤並連按兩下您要新增內容到或編輯的新聞稿。 電子報隨即開啟。

1. 如果元件未顯示，請前往「設計」檢視並啟用必要的元件（例如Newsletter元件），然後再開始編輯。
1. 視需要輸入任何新文字、影像或其他元件。 在Geometrixx範例中，有4個元件可供使用：文字、影像、標題和2欄。 視您的設定方式而定，您的Newsletter可能有更多或更少的元件。

   >[!NOTE]
   >
   >您可以使用變數個人化電子報。 在Geometrixx電子報中，變數可在文字元件中使用。 變數的值繼承自使用者設定檔中的資訊。

   ![mcm_newsletter_content](assets/mcm_newsletter_content.png)

1. 若要插入變數，請從清單中選取變數，然後按一下 **插入**. 變數會從設定檔填入。

## 個人化電子報 {#personalizing-newsletters}

您可以在Geometrixx電子報的文字元件中插入預先定義的變數，以個人化電子報。 變數的值繼承自使用者設定檔中的資訊。

您也可以使用使用者端內容並載入設定檔，以類比電子報的個人化方式。

個人化電子報並模擬其外觀：

1. 從MCM開啟您想要自訂設定的Newsletter。

1. 開啟您要個人化的文字元件。

1. 將游標放在您要變數出現的位置，並從下拉式清單中選取變數，然後按一下 **插入**. 視需要對任意數量的變數執行此動作，然後按一下 **確定**.

   ![mcm_newsletter_variables](assets/mcm_newsletter_variables.png)

1. 若要模擬變數在傳送時的外觀，請按下CTRL+ALT+c以開啟使用者端內容，然後選取 **載入**. 從清單中選取您要載入其設定檔的使用者，然後按一下 **確定**.

   您載入的設定檔資訊已填入變數。

   ![mc_newsletter_testvariables](assets/mc_newsletter_testvariables.png)

## 在不同電子郵件使用者端測試電子報 {#testing-newsletters-in-different-e-mail-clients}

>[!NOTE]
>
>在傳送電子報之前，請檢查Day CQ Link Externalizer的OSGi設定，網址為 `https://localhost:4502/system/console/configMgr`.
>
>依預設，引數的值為 `localhost:4502` 如果執行中執行個體的連線埠已變更，則無法完成和作業。

在常用的电子邮件客户端之间切换，查看您的新闻稿在潜在客户端的外观如何。依預設，您的Newsletter會開啟，且未選取任何電子郵件使用者端。

目前，您可以在下列電子郵件使用者端中檢視電子報：

* Yahoo郵件
* Gmail
* Hotmail
* Thunderbird
* Microsoft Outlook 2007
* Apple Mail

若要在使用者端之間切換，請按一下對應的圖示以檢視該電子郵件使用者端中的Newsletter：

1. 從MCM開啟您想要自訂設定的Newsletter。

1. 按一下頂端列中的電子郵件使用者端，檢視該使用者端中的Newsletter外觀。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 對您要檢視的其他電子郵件使用者端重複此步驟。

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 自訂Newsletter設定 {#customizing-newsletter-settings}

雖然只有授權使用者才能傳送電子報，但您應自訂下列內容：

* 主旨列，讓使用者想要開啟您的電子郵件，並確保您的電子報最終不會標示為垃圾訊息。
* 寄件者地址，例如noreply@geometrixx.com，可讓使用者接收來自指定地址的電子郵件。

若要自訂Newsletter設定：

1. 從MCM開啟您想要自訂設定的Newsletter。

   ![mcm_newsletter_open](assets/mcm_newsletter_open.png)

1. 在Newsletter頂端按一下 **設定**.

   ![mcm_newsletter_settings](assets/mcm_newsletter_settings.png)
1. 輸入 **從** 電子郵件地址

1. 修改 **主旨** 電子郵件的URL名稱（如有必要）。

1. 選取 **預設收件者清單** 下拉式清單中的。

1. 单击&#x200B;**确定**。

   當您測試或傳送Newsletter時，收件者會收到包含指定電子郵件地址和主旨的電子郵件。

## 飛行測試電子報 {#flight-testing-newsletters}

雖然飛行測試並非強制性，但在您傳送電子報之前，您可能需要先測試它，以確保它以您想要的方式顯示。

飛行測試可讓您進行下列工作：

* 檢視中的Newsletter [所有目標使用者端](#testing-newsletters-in-different-e-mail-clients).
* 驗證郵件伺服器是否已正確設定。
* 判斷您的電子郵件是否被標籤為垃圾訊息。 （請確定您已將自己加入收件者清單。）

>[!NOTE]
>
>如果您更新電子郵件提供者、進行快速測試或傳送電子報，如果電子報未先發佈至發佈執行個體，或發佈執行個體無法使用，則這些作業會失敗。 請務必發佈您的Newsletter，並確保Publish執行個體已啟動且執行中。

若要試飛電子報：

1. 從MCM，開啟您要測試並傳送的電子報。

1. 在Newsletter頂端按一下 **測試** ，以在傳送前進行測試。

   ![mcm_newsletter_testsettings](assets/mcm_newsletter_testsettings.png)

1. 輸入您要傳送Newsletter的測試郵件地址，然後按一下 **傳送**. 如果要變更設定檔，請在使用者端內容中載入另一個設定檔。 若要這麼做，請按下CTRL+ALT+c並選取「載入」並載入設定檔。

## 傳送電子報 {#sending-newsletters}

>[!NOTE]
>
>Adobe不打算進一步增強AEM SMTP服務所傳送開啟/彈回（無法傳遞）的電子郵件追蹤。
>建議為 [善用Adobe Campaign以及與AEM的整合](/help/sites-administering/campaign.md).

您可以從Newsletter或清單傳送Newsletter。 兩個程式都進行了說明。

>[!NOTE]
>
>在傳送電子報之前，請檢查Day CQ Link Externalizer的OSGi設定，網址為 `https://localhost:4502/system/console/configMgr`.
>
>依預設，引數的值為 `localhost:4502` 如果執行中執行個體的連線埠已變更，則無法完成和作業。

>[!NOTE]
>
>如果您更新電子郵件提供者、進行快速測試或傳送電子報，如果電子報未先發佈至發佈執行個體，或發佈執行個體無法使用，則這些作業會失敗。 請務必發佈您的Newsletter，並確保Publish執行個體已啟動且執行中。

### 從行銷活動傳送電子報 {#sending-newsletters-from-a-campaign}

若要從行銷活動內傳送電子報：

1. 從MCM開啟您要傳送的Newsletter。

   >[!NOTE]
   >
   >在傳送之前，請確定您已自訂電子報的主旨和原始電子郵件地址 [自訂其設定](#customizing-newsletter-settings).
   >
   >
   >[飛行測試](#flight-testing-newsletters) 建議您在傳送前先傳送Newsletter。

1. 在Newsletter頂端按一下 **傳送**. Newsletter精靈開啟。

1. 在收件者清單中，選取您要接收Newsletter的清單並按一下 **下一個**.

   ![mcm_newslettersend](assets/mcm_newslettersend.png)

1. 已確認設定完成。 按一下 **傳送** 以實際傳送Newsletter。

   ![mcm_newslettersendconfirm](assets/mcm_newslettersendconfirm.png)

   >[!NOTE]
   >
   >請確定您是收件者之一，這樣您才能確保已收到Newsletter。

### 從清單傳送電子報 {#sending-newsletters-from-a-list}

若要從清單傳送Newsletter：

1. 在MCM中，按一下 **清單** 在左窗格中。

   >[!NOTE]
   >
   >在傳送之前，請確定您已自訂電子報的主旨和原始電子郵件地址 [自訂其設定](#customizing-newsletter-settings). 如果您從清單傳送Newsletter，則無法進行測試；您可以 [試飛](#flight-testing-newsletters) 若您從Newsletter傳送，則為。

1. 選取您要傳送Newsletter的目標銷售機會清單旁的核取方塊。

1. 在 **工具** 功能表，選取 **傳送Newsletter**. 此 **傳送Newsletter** 視窗隨即開啟。

   ![mcm_newslettersendfromlist](assets/mcm_newslettersendfromlist.png)

1. 在 **電子報** 欄位中，選取您要傳送的Newsletter，然後按一下 **下一個**.

   ![mcm_newslettersenddialog](assets/mcm_newslettersenddialog.png)

1. 已確認設定完成。 按一下 **傳送** 將選取的Newsletter傳送至指定的潛在客戶清單。

   ![mcm_newslettersenddialog_confirmation](assets/mcm_newslettersenddialog_confirmation.png)

   您的Newsletter已傳送給所選的收件者。

## 訂閱電子報 {#subscribing-to-a-newsletter}

本節說明如何訂閱電子報。

### 訂閱電子報 {#subscribing-to-a-newsletter-1}

訂閱Newsletter (以Geometrixx網站為例)：

1. 按一下 **網站** 並導覽至Geometrixx **工具列** 並開啟。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 在Geometrixx電子報中 **註冊** 欄位，輸入您的電子郵件地址，然後按一下 **註冊**. 您現已訂閱電子報。
