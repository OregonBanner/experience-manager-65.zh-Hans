---
title: We.Gov參考網站FOIA逐步說明
seo-title: We.Gov reference site FOIA walkthrough
description: 請參閱We.Gov參考網站逐步說明，瞭解AEM Forms如何協助政府接收和傳授個人根據資訊自由法案所要求的資訊。
seo-description: See the We.Gov reference site walkthrough to understand how AEM Forms helps governments receive and impart information requested by individuals under the Freedom of Information Act.
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
exl-id: 57b5ce89-6b01-4087-a485-6d9696f06378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# We.Gov參考網站FOIA逐步說明 {#we-gov-reference-site-foia-walkthrough}

## 參考網站資訊自由法案情境 {#reference-site-freedom-of-information-act-scenario}

We.Gov是國家營運的組織，如果養父母收養了孩子，可讓他們註冊子女撫養費。 We.Gov也可讓家長根據資訊自由法案，向下列政府部門索取資訊：

* 國防後勤局
* 國防部監察長辦公室
* 司法部 — 資訊政策辦公室
* 海軍部
* 環境保護局

如需資訊自由法的詳細資訊，請參閱 [www.foia.gov](https://www.foia.gov).

此情境涉及下列角色：

* Sarah Rose，在下要求資訊的人
* 處理請求的人John Jacobs會將請求轉送給適當的部門
* Gloria Rios，根據要求提供資訊的政府職員

## Sarah根據FOIA提出資訊請求 {#sarah-initiates-request-for-information-under-foia}

根據《資訊自由法》，Sarah要求2013年至2016年兒童與家庭行政案件記錄副本(FY)。 Sarah將此要求提交給司法部 — 資訊局政策處，同時表示她願意支付高達100美元的印刷和郵資費用。

### 運作方式 {#how-it-works}

### 親眼看看 {#see-it-yourself}

在您的瀏覽器中，開啟 `https://<hostname>:<PublishPort>/wegov`. 在We.Gov網站中，點選「應用程式>所有應用程式」。 在「所有應用程式」頁面中，點選「FOIA要求的應用程式」下的「套用」。

## Sarah開始申請FOIA下的資訊 {#sarah-starts-her-application-for-information-under-foia}

Sarah點按 **套用** 而在資訊自由法案申請表頁面中，Sarah會輸入以下資訊：

* **機構：** Sarah指定要求所針對的機構為司法部 — 資訊政策辦公室。

* **將支付最高至**：Sarah表示願意支付最高100美元的列印和郵資費用。
* **詳細說明請求**：Sarah指定「要求2013至2016會計年度兒童和家庭管理個案記錄副本」。

![索取2013至2016會計年度兒童及家庭管理局個案記錄副本](assets/sarahfiosform.png)

索取2013至2016會計年度兒童及家庭管理局個案記錄副本

Sarah隨時都可以點選「儲存」以儲存表單草稿，稍後再回來填寫表單並提交它。 Sarah提交表單。

>[!NOTE]
>
>從電子郵件恢復工作流程僅適用於登入的使用者。 在參考網站案例中，確定已新增使用者Sarah Rose。 Sarah的登入憑證為 `srose/password`.

## John Jacobs接收並核准該申請 {#john-jacobs-receives-and-approves-the-application}

John Jacobs會收到要求，並將其路由給合適的人。 AEM收件匣可讓她在一個位置檢視所有提交的應用程式。

### 運作方式 {#how-it-works-1}

當Sarah填寫並提交FOIA應用程式時，應用程式的記錄會傳送到John Jacobs的收件匣。 John Jacobs可以檢視提交的應用程式，並接受或拒絕它。

### 親眼看看 {#see-it-yourself-1}

您可以在https://存取AEM收件匣&lt;***主機名稱***>：&lt;***發佈連線埠***>/content/we-finance/global/en/login.html？resource=/aem/inbox.html. 使用jjacobs/密碼作為John Jacobs的使用者名稱/密碼登入AEM收件匣，並檢視FOIA應用程式。 如需使用AEM收件匣處理以表單為中心的工作流程工作的相關資訊，請參閱 [在AEM收件匣中管理Forms應用程式和工作](/help/forms/using/manage-applications-inbox.md).

![約翰雅各布](assets/johnjacobs.png)

John Jacobs可以從應用程式儀表板檢視、核准或拒絕應用程式。 John Jacobs會選取並開啟請求詳細資訊，並在檢閱請求後予以核准。

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah收到確認電子郵件</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

在John Jacobs核准申請後，Sarah會收到來自We.Gov網站的確認電子郵件。 系統會通知Sarah處理申請所需的費用和時間。 電子郵件也包含電子郵件和電話詳細資料，Sarah可以聯絡以取得應用程式的更新資訊。

![薩拉赫羅塞梅爾](assets/sarahroseemail.png)

## Gloria會收到FOIA的第二層核准要求 {#gloria-receives-the-foia-request-for-second-level-approval}

在John Jacobs填寫必填資訊並核准Sarah的請求後，該請求將轉至Gloria Rios進行最終核准。 Gloria會稽核附加的記錄檔案並核准請求。

![gloriariosinbox](assets/gloriariosinbox.png)

### 運作方式 {#how-it-works-2}

當John Jacobs核准FOIA請求時，應用程式的PDF或記錄檔案會建立並傳送到Gloria Rios的收件匣。 Gloria可以檢視已提交的請求，並核准或拒絕該請求。

### 自行檢視 {#see-for-yourself}

您可以在https://存取AEM收件匣&lt;***主機名稱***>：&lt;***發佈連線埠***>/content/we-finance/global/en/login.html？resource=/aem/inbox.html. 以Gloria Rios的使用者名稱/密碼登入AEM收件匣，並檢視FOIS要求。

Gloria會開啟要求，並檢查FOIA要求的詳細資料。 在檢閱請求的詳細資訊並檢查提供所需檔案的可行性後，Gloria核准了請求。

![gloriariosapproves](assets/gloriariosapproves.png)

## Sarah會收到請求獲得核准的通知 {#sarah-receives-notification-that-her-request-is-approved}

Gloria核准FOIA要求後，Sarah會收到電子郵件，通知她要求已核准。 此電子郵件也包含提供檔案的暫定時間表相關資訊，以及跟進請求的聯絡人詳細資訊。

![sarahroseemailapproval](assets/sarahroseemailapproval.png)
