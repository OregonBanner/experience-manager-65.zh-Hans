---
title: We.Finance汽車保險續約參考網站逐步說明
seo-title: We.Finance Auto Insurance Renewal reference site walkthrough
description: We.Finance汽車保險續約參考網站逐步說明
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
exl-id: b6ded6ac-4fb1-49f9-b272-16774c3e89a3
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# We.Finance汽車保險續約參考網站逐步說明{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## We.Finance參考網站案例  {#we-finance-reference-site-scenario}

We.Finance網站是金融服務網站，旨在協助您學習AEM Forms的互動式通訊功能。

閱讀We.Finance汽車保險使用案例的詳細逐步解說，該使用案例展示AEM表單及其與Microsoft Dynamics的整合如何協助個人化金融服務公司的客戶體驗。 互動式逐步解說可簡化複雜數位交易的實作，以及金融公司的客戶通訊。

**歷程從使用案例開始：**

Sarah Rose是We.Finance的現有客戶，並購買汽車保險單。 現在正是她續保的時候。 We.Finance保險代理Gloria Rios向Sarah傳送有關其保單續約的提醒。 Sarah遵循電子郵件中提供的指示，並成功完成程式。

## 自動保險應用程式逐步說明 {#auto-insurance-application-walkthrough}

We.Finance自動保險應用程式案例是針對使用者的視覺敘述，並以兩個角色為基礎：

* We.Finance客戶Sarah Rose
* Gloria Rios，保險代理，We.Finance

### Gloria從We.Finance傳送保單續約通訊 {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria登入AEM執行個體，按一下 **汽車保險續約，** 然後按一下 **開啟代理程式UI。**&#x200B;按一下即可使用Sarah Rose的保單詳細資料預先填入保險檔案。 Gloria點按次數&#x200B;**提交** 而訊息會顯示在「已起始提交」畫面上，然後在數秒內顯示為「已成功提交」。

Sarah收到一封電子郵件，主題為「您的汽車保險續約」。

![代理 UI](assets/agent_ui_email_new.png)

#### 親眼看看 {#see-it-yourself}

前往 **Adobe Experience Manager** > **Forms** > **Forms與檔案** > **We.Finance** > **汽車保險**. 選取自動保險續約 **互動式通訊** 並按一下 **開啟代理程式UI**. 互動式通訊會在Agent UI中開啟。 輸入有效的電子郵件地址，以接收附加原則檔案的電子郵件，然後按一下「提交」。

您可以直接從存取及檢視「汽車保險續約」互動式通訊 `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### Sarah收到We.Finance的保單續約通訊，並決定續約 {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah收到一封包含We.Finance附件的電子郵件，提醒她汽車保險單即將到期。 附件是她的「汽車保險」信函的列印版本。

Sarah點按 **立即續約** 並導向至其汽車保險信件的網頁版本。 Sarah會在此信函上尋找原則到期的剩餘天數。 此頁面會為Sarah提供保單詳細資料的基本概觀，例如保單編號、到期金額以及其他資訊，例如折扣優惠和忠誠度獎勵。 Sarah再次點按 **立即續約** 位於原則底部。

![ref1](assets/ref1.png)

#### 運作方式 {#how-it-works}

您使用互動式通訊的多通道功能，建立汽車保險信函的網頁與列印輸出。

電子郵件中的「立即續訂」按鈕連結至「自動保險續訂」應用程式，這是發佈執行個體上的互動式通訊。

#### 親眼看看 {#see-it-yourself-1}

您必須已收到附加PDF的電子郵件。 此PDF是您車險信函的列印版本。 按一下 **立即續約** 以存取原則的Web版本。 檢查您的個人資訊和原則詳細資料，然後按一下 **立即續約** 它會帶您進入另一個互動式通訊。

此 **立即續約** 電子郵件中的按鈕會將Sarah導向原則的網頁版本。 您可以造訪下列URL：

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

您可以檢查自動保險續約的詳細摘要，然後按一下 **立即續約** 位於頁面底部。

### Sarah到達付款頁面 {#sarah-reaches-the-payment-page}

We.Finance會將Sarah帶往「付款」頁面。 Sarah用她的記錄重新檢查她的保單號碼和到期日。 在頁面的右側，她檢查她續約的付款摘要，並在總金額上提供10%的溢價折扣。

#### 運作方式 {#how-it-works-1}

「立即續約」按鈕會將Sarah導向付款頁面。 付款頁面為最適化表單。

#### 親眼看看 {#see-it-yourself-2}

按一下 **立即續約** 以存取「付款」頁面。 填寫您的信用卡資訊，然後按一下 **進行付款**.

您可以前往撰寫執行個體中的付款頁面：

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah進行付款並完成程式 {#sarah-makes-the-payment-and-completes-the-process}

Sarah填寫她的信用卡詳細資料並按一下 **進行付款**.

#### 運作方式 {#how-it-works-2}

當Sarah填寫信用卡詳細資料並按一下「提交」時，系統就會處理其信用卡付款，且畫面上會顯示以最適化表單設定的感謝訊息。

#### 親眼看看 {#see-it-yourself-3}

按一下「付款」，即可檢視確認訊息。

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
