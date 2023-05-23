---
title: 員工招聘參考網站逐步說明
seo-title: Employee recruitment
description: AEM Forms參考網站會展示組織如何使用AEM Forms功能來實作員工招募工作流程。
seo-description: AEM Forms reference site showcases how organizations can use AEM Forms features to implement employee recruitment workflow.
uuid: 27e456ba-3c08-4c43-ad54-1ba0070995ad
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f04b13e-ea40-4c86-9168-e020c52435a2
exl-id: bdfc0a20-1e98-47f9-a1d1-5af5b3ef15db
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 0%

---

# 員工招聘參考網站逐步說明 {#employee-recruitment-reference-site-walkthrough}

## 概述 {#overview}

We.Finance是可讓應徵者透過參考網站入口網站申請就業的組織。 組織也會使用入口網站來管理候選人的面試排程、短名單和內部溝通。 網站會管理下列專案：

* 搜尋和申請工作的適用者
* 篩選及甄選候選人
* 面試程式
* 候選者詳細資訊的集合
* 候選背景檢查
* 將優惠方案轉出給選取的候選者

>[!NOTE]
>
>We.Finance和We.Gov參考網站都有員工招募使用案例。 逐步說明中使用的範例、影像和說明使用We.Finance參考網站。 不過，您也可以執行這些使用案例，並使用We.Gov檢閱成品。 若要這麼做，請取代 **we-finance** 替換為 **we-gov** 在提及的URL中。

### 涉及的工作流程模型 {#workflow-models-involved}

員工招募使用案例涉及兩個工作流程：

* 面試前 — 我們財務員工招募工作流程
* 面試後 — 我們財務員工招募面試後工作流程

這些工作流程是在AEM中建立的，可在以下網址找到：

`https://[authorHost]:[authorPort]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models/`

#### 我們為員工招募工作流程提供資金 {#we-finance-employee-recruiting-workflow}

以下是本檔案遵循的「我們財務員工招聘」工作流程模型。

![we-finance-employee-recruitment-workflow](assets/we-finance-employee-recruiting-workflow.png)

#### 我們為員工招聘面試工作流程提供資金 {#we-finance-employee-recruiting-post-interview-workflow}

以下是本檔案中遵循的「我們財務員工面試後招聘」工作流程模型。

![we-finance-employee-recruitment-post-interview-workflow](assets/we-finance-employee-recruiting-post-interview-workflow.png)

### 角色 {#personas}

此情境涉及下列角色：

* Sarah Rose，應徵者正在申請組織內的工作
* 招聘人員John Jacobs
* 招聘經理Gloria Rios
* HR人員John Doe

## Sarah申請工作 {#sarah-applies-for-a-job}

Sarah Rose正在組織中尋找工作機會。 她瀏覽他們的入口網站，並探索「職業」頁面上列出的職缺職位。 她找到相符的工作清單並申請。

![home-page](assets/home-page.png)

We.Finance首頁

![career-page](assets/career-page.png)

We.Finance職涯頁面

Sarah在職缺公告上按一下「套用」 。 工作應用程式表單隨即開啟。 她填寫應用程式中的所有詳細資料並提交它。

![job-application-form](assets/job-application-form.png)

### 運作方式 {#how-it-works}

We.Finance首頁和職涯頁面為AEM Sites頁面。 職涯頁面內嵌最適化表單，此表單會使用可重複的面板，透過服務擷取職缺職位，並在頁面上列出。 您可以造訪以下網址檢視最適化表單： `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/recruitment/jobs.html`.

### 親眼看看 {#see-it-yourself}

前往 `https://[publishHost]:[publishPort]/content/we-finance/global/en.html` 並按一下 **[!UICONTROL 職業]**. 按一下 **[!UICONTROL 搜尋]** 填入工作清單，然後按一下 **[!UICONTROL 套用]** 以取得工作。 填寫表單的詳細資料並提交申請。

請務必在應用程式中指定有效的電子郵件ID，因為透過此逐步說明的任何通訊都會傳送至指定的電子郵件ID。

## John Jacobs將Sarah Rose的設定檔列入篩選名單 {#john-jacobs-shortlists-sarah-rose-s-profile-for-the-hiring-manager-s-screening}

組織會收到Sarah提交的工作申請。 招聘人員John Jacobs被指派稽核Sarah設定檔的任務。 他檢閱其AEM收件匣中的任務，尋找符合工作需求的設定檔，然後按一下短清單。 Sarah的個人檔案會轉送給招聘經理Gloria Rios，等待她核准。

![jjacobs-inbox-1](assets/jjacobs-inbox-1.png)

John的AEM收件匣

![candidate-shortlist](assets/candidate-shortlist.png)

John Jacobs將Sarah Rose的設定檔列入篩選名單

**運作方式**

「工作申請」表單中的提交動作會觸發工作流程，在John Jacob收件匣中建立工作以篩選申請。 當John稽核並甄選申請時，工作流程會在僱用經理Gloria的收件匣中建立任務。

### 親眼看看 {#see-it-yourself-1}

前往 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`和使用jjacobs/密碼登入，作為John Jacobs的使用者名稱/密碼。 開啟「應徵者設定檔複查」作業，並將應徵者加入候選清單。

## Gloria會複查申請並核准應徵者進行面試 {#gloria-reviews-the-application-and-approves-the-applicant-for-an-interview}

招聘經理Gloria會在其AEM收件匣中收到入圍的個人資料作為工作。 她稽核並核准候選人莎拉·羅斯接受面試。

![gloriainbox](assets/gloriainbox.png)

Gloria的AEM收件匣

![gloriaschedulesinterview](assets/gloriaschedulesinterview.png)

Gloria同意Sarah Rose接受訪談

**運作方式**

當Gloria核准面試的候選人時，工作流程會在We.Finance的招聘人員John Doe的AEM收件匣中建立任務。

### 親眼看看 {#see-it-yourself-2}

前往 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 和使用jjacobs/密碼登入，作為John Jacobs的使用者名稱/密碼。 開啟「應徵者設定檔複查」作業，並將應徵者加入候選清單。

前往 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 並使用grios/密碼作為Gloria Rios的使用者名稱/密碼登入。 開啟「應徵者設定檔複查」作業，然後按一下「排程面試」。

## John Doe安排面試 {#john-doe-schedules-an-interview}

John Doe會在收件匣中接收排程面試的任務。 John Doe會選取並開啟工作，並以John Jacob的身分修正面試日期與時間、地點以及負責面試的HR人員。 John Doe按一下「傳送邀請電子郵件」。 系統會傳送電子郵件給Sarah，並指派工作給僱用經理Gloria，以便與Sarah面談。

![johnjacobsaeminbox](assets/johnjacobsaeminbox.png)

John Doe的AEM收件匣

![johndoescheduleinterview](assets/johndoescheduleinterview.png)

John Doe安排面試，並將詳細資料傳送給Sarah Rose

## Sarah Rose收到包含面試排程的電子郵件 {#sarah-rose-receives-the-email-with-interview-schedule}

Sarah Rose會收到包含面試時間表、地點和其他詳細資訊的電子郵件。 她按一下「接受」，表示她同意面試排程和地點。 在精確資訊的指引下，Sarah接受了採訪。

![sarahroseinterviewemail](assets/sarahroseinterviewemail.png)

Sarah Rose收到面試排程

## 面試結束後，「招聘經理」將Sarah Rose列入候選名單 {#after-the-interviews-the-hiring-manager-shortlists-sarah-rose}

在Sarah Rose完成面試並完成面試後，招聘經理Gloria Rios會從收件匣開啟「候選人選擇」工作，然後按一下「選擇」。 Gloria Rios的決定傳達給人力資源人員John Doe，以供進一步處理。

![gloriariosinboxoffer](assets/gloriariosinboxoffer.png)

Gloria的AEM收件匣

![榮耀選取候選](assets/gloriariosselectcandidate.png)

Gloria Rios在面試後挑選Sarah Rose

## John Doe要求更多資訊 {#john-doe-requests-more-information}

要求候選人加入組織之前，必須先檢查其背景。 John Doe會開啟並檢閱選取的應徵者詳細資料，發現其部分就業與教育詳細資料尚未填寫。 John Doe點按需要更多資訊。

![Johndoeinbox](assets/johndoeinbox.png) ![johndoeneedmoreinformation](assets/johndoeneedmoreinformation.png)

John Doe向Sarah Rose索取更多教育與工作經驗的相關資訊

## Sarah Rose收到一封要求進一步資訊的電子郵件 {#sarah-rose-receives-an-email-requesting-further-information}

Sarah Rose收到一封電子郵件，通知她需要進一步的資訊才能處理她的就業申請。 電子郵件包含填寫所需資訊之表單的連結。

![sarahroseemailmoredetails](assets/sarahroseemailmoredetails.png)

Sarah Rose收到一封電子郵件，通知她需要進一步的資訊才能處理其就業申請

Sarah按一下電子郵件中的「提供詳細資訊」連結。 表單隨即出現。 Sarah會根據John Doe的要求填寫必要的教育和就業詳細資訊，然後按一下「提交」。

![additionalinformation1](assets/additionalinformation1.png)

Sarah按一下電子郵件中的連結，開啟其他資訊表單

![additionalinformation2](assets/additionalinformation2.png)

Sarah會根據John Doe的要求填寫其他資訊，然後按一下提交

## John Doe會檢閱選取的候選人設定檔，以取得其他資訊 {#john-doe-reviews-the-selected-candidate-profile-for-the-additional-information-provided}

John Doe會選取候選稽核請求並開啟它。 John Doe發現Sarah已填妥所有必要資訊。 檢閱應用程式後，John Doe按一下「核准」。 經John Doe核准後，對Sarah Rose執行背景檢查的請求會轉寄給John Jacobs。

![johndoeditionainformationinbox](assets/johndoeadditionainformationinbox.png)

John Doe的AEM收件匣

![johndoeditionalinformationreview-copy](assets/johndoeadditionalinformationreview-copy.png)

John Doe會檢閱Sarah提供的其他資訊並加以核准

## John Jacobs會收到背景檢查要求 {#john-jacobs-receives-a-background-check-request}

John Jacobs在收件匣中看到背景檢查要求。 John Jacobs開啟任務並檢閱Sarah Rose提供的資訊。 執行背景檢查後，John Jacobs按一下「繼續」表示背景檢查成功。

![johnjacobsbackgroundcheckinbox](assets/johnjacobsbackgroundcheckinbox.png)

John Jacobs的AEM收件匣

![johnjacobsbackgroundcheckgoahead](assets/johnjacobsbackgroundcheckgoahead.png)

執行背景檢查後，John Jacobs按一下「繼續」

## John Doe將加入信寄給Sarah Rose {#john-doe-sends-out-the-joining-letter-to-sarah-rose}

John Doe會在其AEM收件匣中收到傳送加入信件的要求。 John開啟請求並檢視詳細資料。 John Doe附加加入信件PDF，然後按一下「附加並傳送加入信件」。

![johndoejoiningletterinbox](assets/johndoejoiningletterinbox.png)

John Doe的AEM收件匣

![johndoejoiningletterattachandsend](assets/johndoejoiningletterattachandsend.png)

John Doe寄出加入信件以供簽署

## Sarah Rose收到並簽署加入信件 {#sarah-rose-receives-and-signs-the-joining-letter}

Sarah Rose收到簽署加入信件。 Sarah按一下這裡以檢閱並簽署加入信件。 加入信件PDF會開啟，並附上欄位以簽署檔案。

![sarahrosejoiningletteremail](assets/sarahrosejoiningletteremail.png)

Sarah Rose收到簽署加入信件

Sarah可以選擇輸入、使用draw手寫、插入簽名影像，或使用她的行動觸控熒幕來繪製她的簽名。 Sarah輸入她的名字，按一下「按一下以簽署」，然後下載加入信函的已簽署復本。

![sarahrosejoininglettersign](assets/sarahrosejoininglettersign.png)

Sarah輸入她的名字以簽署加入信件

![sarahrosejoininglettersign2](assets/sarahrosejoininglettersign2.png)

Sarah按一下按一下即可完成簽署加入信
