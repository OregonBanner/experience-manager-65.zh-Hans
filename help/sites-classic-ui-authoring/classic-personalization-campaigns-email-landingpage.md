---
title: 建立有效的Newsletter登陸頁面
seo-title: Creating an Effective Newsletter Landing Page
description: 有效的Newsletter登陸頁面可協助您讓更多人註冊您的Newsletter （或其他電子郵件行銷活動）。 您可以使用從Newsletter註冊收集到的資訊來取得銷售機會。
seo-description: An effective newsletter landing page helps you get as many people as possible to sign up for your newsletter (or other email marketing campaign). You can use the information you gather from your newsletter sign ups to get leads.
uuid: 0799b954-076b-4e95-8724-3661ae8fddb6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: b41de64a-7d27-4633-a8d5-ac91d47eb1bb
docset: aem65
exl-id: c2fbf858-8815-426e-a2e5-f92bcf909ad0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---

# 建立有效的Newsletter登陸頁面{#creating-an-effective-newsletter-landing-page}

有效的Newsletter登陸頁面可協助您讓更多人註冊您的Newsletter （或其他電子郵件行銷活動）。 您可以使用從Newsletter註冊收集到的資訊來取得銷售機會。

若要建立有效的Newsletter登陸頁面，您需要執行下列動作：

1. 建立Newsletter清單，讓使用者可以訂閱Newsletter。
1. 建立登錄檔單。 執行此操作時，新增工作流程步驟，自動將註冊電子報的人員新增到您的潛在客戶清單中。
1. 建立感謝使用者註冊的「確認」頁面，並可能會提供促銷活動。
1. 新增Teaser。

>[!NOTE]
>
>Adobe不打算進一步增強此功能（管理銷售線索和清單）。
>建議善用 [Adobe Campaign與AEM的整合](/help/sites-administering/campaign.md).

## 建立Newsletter的清單 {#creating-a-list-for-the-newsletter}

建立清單，例如， **Geometrixx電子報**，以取得使用者應訂閱的Newsletter。 建立清單的說明請參閱 [建立清單](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingnewlists).

以下顯示清單的範例：

![mcm_listcreate](assets/mcm_listcreate.png)

## 建立登錄檔單 {#create-a-sign-up-form}

建立電子報登錄檔單，讓使用者訂閱標籤。 範例Geometrixx網站在Geometrixx工具列中提供Newsletter頁面，您可以在其中建立表單。

若要建立您自己的Newsletter表單，請參閱 [Forms檔案](/help/sites-authoring/default-components.md#form). Newsletter使用標籤庫中的標籤。 若要新增其他標籤，請參閱 [標籤管理](/help/sites-authoring/tags.md#tagadministration).

下列範例中的隱藏欄位提供最低限度的資訊（電子郵件）；此外，您可以稍後新增更多欄位，但這會影響轉換率。

以下範例是在https://localhost:4502/cf#/content/geometrixx/en/toolbar/newsletter.html建立的表單。

1. 建立表單。

   ![mcm_newsletterpage](assets/mcm_newsletterpage.png)

1. 按一下 **編輯** 將表單設定為前往「感謝您」頁面(請參閱 [建立感謝頁面](#creating-a-thank-you-page))。

   ![dc_formstart_thankyou](assets/dc_formstart_thankyou.png)

1. 設定「表單」動作（提交表單時就會發生這種情況），並設定群組以將註冊使用者指派給您先前建立的清單（例如geometrixx-newsletter）。

   ![dc_formstart_thankyouadvanced](assets/dc_formstart_thankyouadvanced.png)

### 建立感謝頁面 {#creating-a-thank-you-page}

當使用者按一下 **立即訂閱**，您想要自動開啟「感謝」頁面。 在Geometrixx電子報頁面中建立「感謝您」頁面。 建立Newsletter表單後，編輯表單元件並新增感謝頁面的路徑。

提交請求會將使用者帶到 **感謝您** 頁面，使用者會在頁面之後收到電子郵件。 此「感謝您」頁面建立於/content/geometrixx/en/toolbar/newsletter/thank_you。

![mcm_newsletter_thankyoupage](assets/mcm_newsletter_thankyoupage.png)

### 新增Teaser {#adding-teasers}

新增 [Teasers](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers) 以鎖定特定對象。 例如，您可以將Teaser新增至「感謝您」頁面和Newsletter註冊頁面。

若要新增Teaser以產生有效的Newsletter登陸頁面：

1. 為註冊禮品建立Teaser段落。 選取 **第一個** 作為策略，並加入文字以告知他們將會收到什麼禮物。

   ![dc_teaser_thankyou](assets/dc_teaser_thankyou.png)

1. 為「感謝您」頁面建立Teaser段落。 選取 **第一個** 作為策略，並包含表示贈品即將送出的文字。

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. 使用兩個Teaser建立行銷活動 — 標籤一個有業務，另一個沒有標籤。

### 推送內容給訂閱者 {#pushing-content-to-subscribers}

透過MCM中的Newsletter功能推送對頁面所做的任何變更。 然後，您將更新內容推送至訂閱者。

另請參閱 [傳送電子報](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters).
