---
title: We.Gov和We.Finance參考網站逐步說明
seo-title: We.Gov and We.Finance reference site walkthrough
description: 使用虛構的使用者和群組，透過We.Gov和We.Finance示範套件執行AEM Forms工作。
seo-description: Use fictitious users and groups to perform AEM Forms tasks using We.Gov and We.Finance demo package.
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
exl-id: 288d5459-bc69-4328-b6c9-4b4960bf4977
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 1%

---

# We.Gov和We.Finance參考網站逐步說明 {#we-gov-reference-site-walkthrough}

## 先決條件 {#pre-requisites}

依照中的說明設定參考網站 [設定和設定We.Gov和We.Finance參考網站](../../forms/using/forms-install-configure-gov-reference-site.md).

## 使用者劇本 {#user-story}

* AEM Forms

   * 自动化表单转换
   * 创作
   * 表單資料模型/資料來源

* AEM Forms

   * 資料擷取
   * （選用）資料整合(MS Dynamics)
   * （選用） Adobe Sign

* 工作流
* 电子邮件通知
* （可選）客戶通訊

   * 打印渠道
   * Web 渠道

* Adobe Analytics
* 資料來源整合

### 虛構的使用者和群組 {#fictitious-users-and-groups}

We.Gov示範套件隨附下列內建虛構的使用者：

* **譚雅**：有資格從政府機構獲得服務的公民

![虛構的使用者](/help/forms/using/assets/aya_tan_new.png)

* **郎宇威**： We.Gov代理商業務分析師

![虛構的使用者](/help/forms/using/assets/george_lang.png)

* **卡蜜拉·桑托斯**： We.Gov Agency CX銷售機會

![虛構的使用者](/help/forms/using/assets/camila_santos.png)

此外也包含下列群組：

* **We.Gov Forms使用者**

   * George Lang （會員）
   * Camila Santos （會員）

* **We.Gov使用者**

   * George Lang （會員）
   * Camila Santos （會員）
   * 譚雅（會員）

### 示範概觀術語圖例 {#demo-overview-terms-legend}

1. **模擬**：AEM示範中的已定義使用者和群組。
1. **按鈕**：彩色矩形或圓圈箭頭用於導覽。
1. **按一下**：在使用者劇本中執行動作。
1. **連結**：位於We.Gov網站中主要功能表的頂端。
1. **使用者指示**：導覽使用者劇本時應遵循的一組數值步驟。
1. **Forms入口網站**： *https://&lt;aemserver>：&lt;port>/content/we-gov/formsportal.html*
1. **行動檢視**：We.Gov使用者，可使用重新調整大小的瀏覽器來復寫行動檢視。
1. **案頭檢視**： We.gov使用者可在筆記型電腦或桌上型電腦上檢視示範。
1. **預先篩選表單**：We.Gov網站首頁上的表單。
1. **最適化表單**：We.gov示範的註冊應用程式表單。

   *https://&lt;aemserver>：&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **AdobeWe.Gov網站**： *https://&lt;aemserver>：&lt;port>/content/we-gov/home.html*
1. **Adobe收件匣**：位於上方功能表列 [鈴鐺圖示](assets/bell.svg) 在AEM後端。

   *https://&lt;aemserver>：&lt;port>/aem/start.html*

1. **電子郵件使用者端**：檢視您電子郵件的偏好方式(Gmail、Outlook)
1. **CTA**：行動號召
1. **導覽**：在瀏覽器頁面上尋找特定參考點。
1. **AFC**：Automated forms conversion

## automated forms conversion（卡蜜拉） {#automated-forms-conversion}

**本節**：CX銷售機會的Camila擁有現有的PDF式表單，此表單是紙張式流程的一部分。 在現代化工作中，她想要使用此PDF表單來自動建立新的現代化Adaptive Forms。

### automated forms conversion- We.Gov （卡蜜拉） {#automated-forms-conversion-wegov}

1. 導覽至 *https://&lt;aemserver>：&lt;port>/aem/start.html*

1. 登入方式：
   * **使用者**：camila.santos
   * **密碼**：密碼
1. 從首頁面選取「Forms > Forms &amp; Documents > AEM Forms We.gov Forms > AFC」。
1. Camila會將PDF上傳至AEM Forms。

   ![上傳表單](assets/aftia-upload-form.jpg)

1. Camilla接著選取PDF表單並按一下 **開始自動轉換** 以開始轉換程式。 您可能需要按一下 **覆寫轉換** 如果您已轉換表單。

   >[!NOTE]
   >
   >請注意，AFC中的設定已預先設定給一般使用者，這表示這些設定不應變更。

   * **可選**：如果您想要使用無障礙的Ultramine主題，只要按一下「指定最適化表單主題」 ，然後選取出現在選項清單中的Accessible-Ultramine主題。

   ![開始轉換](assets/aftia-start-conversion.jpg)

   ![超海洋主題](assets/aftia-upload-conversion-settings.jpg)

   轉換期間會顯示完成百分比狀態。 狀態顯示後 **已轉換**，按一下 **輸出** 資料夾，選取最適化表單並按一下 **編輯** 以開啟轉換後的表單。

1. 接著Camilla會檢閱表單，並確認所有欄位都存在

   ![檢閱轉換](assets/aftia-review-conversion.jpg)

1. 然後Camilla開始編輯表單。 她選取「根面板」>「編輯（扳手）」>「從面板配置下拉式選單中選取「索引標籤在頂端」>「選取核取方塊」。

   ![檢閱屬性](assets/aftia-review-properties.jpg)

1. 然後Camilla會新增所有必要的CSS和欄位變更，以產生最終產品。

   ![新增CSS](assets/aftia-add-css.jpg)

### 表單資料模型與資料來源(Camila) {#data-sources}

**本節**：一旦檔案轉換並產生最適化表單後，Camila就需要將最適化表單連結到資料來源。

1. Camila會在已轉換的表單上開啟屬性 [automated forms conversion- We.Gov](#automated-forms-conversion-wegov).

1. Camila接著會選取「表單模型」>從「選取自」下拉式清單中選取「表單資料模型」>從選項清單中選取「We.gov註冊FDM」。

1. 按一下儲存並關閉按鈕。

   ![FDM選擇](assets/aftia-select-fdm.jpg)

1. Camila按一下 **輸出** 資料夾，選取最適化表單並按一下 **編輯** 以開啟已完成的We.Gov表單。
1. Camila選取最適化表單欄位並按一下 ![設定圖示](assets/configure-icon.svg). 她使用建立表單資料模型實體的繫結 **繫結參考** 欄位。 她會對最適化表單中的所有欄位重複此步驟。

### 表單協助工具測試(Camila) {#form-accessibility-testing}

Camila也會驗證建立的內容是否已根據企業標準正確建置且完全可存取。

1. Camila按一下 **輸出** 資料夾，選取最適化表單並按一下 **預覽** 以開啟已完成的We.Gov表單。

1. 在Chrome開發人員工具中開啟「稽核」標籤。

1. 執行協助工具檢查以驗證最適化表單。

   ![協助工具檢查](assets/aftia-accessibility.jpg)

## 最適化表單行動檢視示範(Aya) {#mobile-view-demo}

**此區段必須在示範之前執行。**

**使用者指示：**

1. 導覽至： *https://&lt;aemserver>：&lt;port>/content/we-gov/home.html*
1. 登入方式：

   1. **使用者**： aya.tan
   1. **密碼**：密碼

1. 重新調整瀏覽器視窗大小，或使用瀏覽器的模擬器來複製行動裝置大小。

### We.Gov網站(Aya) {#aya-user-story-we-gov-website}

![虛構的使用者](/help/forms/using/assets/aya_tan_new-1.png)

**本節**：綾是市民。 她從朋友那裡得知她可能有資格獲得政府機構提供的服務。 Aya從行動電話瀏覽至We.Gov網站，進一步瞭解她有資格使用的服務。

### We.Gov前置熒幕(Aya) {#aya-user-story-we-gov-pre-screener}

Aya在行動電話上填寫簡短的最適化表格，回答幾個問題以確認其資格。

**使用者指示：**

1. 在每個下拉式欄位中進行選取。

   >[!NOTE]
   >
   >如果使用者每年的收入超過$200,000，則不符合資格。

1. 按一下「**我符合資格嗎？**&quot; 按钮.
1. 按一下「**立即套用**」按鈕以繼續。

   ![立即套用連結](/help/forms/using/assets/apply_now_link.png)

### We.Gov最適化表單(Aya) {#aya-user-story-we-gov-adaptive-form}

Aya發現她符合資格，便開始填寫應用程式，以便在行動裝置上請求服務。

Aya需要先在家中檢閱一些檔案，才能完成服務請求申請。 她儲存並從行動裝置退出應用程式。

**使用者指示：**

1. 填寫「基本資訊」欄位，以下是必填欄位和下拉式清單：

   1. 基本信息

      1. 名字
      1. 姓氏
      1. 出生日期
      1. 电子邮件

1. 使用下列專案 **動態邏輯** 使用示範動態功能 **家庭狀態** 下拉式清單：

   1. **單一**：顯示親屬面板
   1. **已婚**：顯示婚姻相依面板
   1. **離婚**：顯示親屬面板
   1. **喪偶**：顯示親屬面板
   1. **您有孩子嗎？**：（是/否）顯示子項相依面板的單選按鈕。

      1. （新增/移除）按鈕可新增/移除多個子項相依面板。

1. 按一下灰色選單列中的向右箭頭。
1. 按一下底部的「儲存」按鈕。

   ![最適化表單詳細資料](/help/forms/using/assets/adaptive_form.png)

## 案頭示範 {#desktop-demo}

**本節：** 回到家後，Aya找到她需要的資訊，並從她的案頭繼續執行應用程式。 Aya會導覽至線上表單入口網站，以繼續執行其應用程式。 代理商也可以透過一些簡單的自訂功能，自動產生連結並以電子郵件方式繼續使用應用程式。

### 續式最適化表單(Aya) {#aya-user-story-continued-adaptive-form}

**使用者指示：**

1. 導覽至 *https://&lt;aemserver>：&lt;port>/content/we-gov/home.html*
1. 在導覽列中，選取「按一下」**線上服務**「。
1. 從「草稿Forms」面板中，選取現有的「健康權益註冊應用程式」。

   ![健康權益的註冊申請](/help/forms/using/assets/enrollment_application.png)

   外觀和感覺相同，她不需要重新輸入任何資料。

   **使用者指示：**

1. 按一下右鍵「圓CTA」以移動到下一個截面。

   ![右圓形CTA](/help/forms/using/assets/right_circle_cta_new.png)

   表單會填入至Aya的最後一個專案點。 Aya已輸入所有資訊並準備提交。

   ![提交最適化表單](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >當Aya填寫電話號碼欄位時，她必須填寫為連續11位數的數字，不含破折號、空格或連字型大小。

   提交之後，Aya會收到「感謝」頁面。 或者，她也會收到電子郵件，以便開啟該電子郵件，以電子方式與Adobe Sign簽署記錄檔案。

### 可選：Adobe Sign (Aya) {#adobe-sign}

**使用者指示：**

1. 導覽至您的電子郵件使用者端，並找到Adobe Sign電子郵件。
1. 按一下Adobe Sign連結。

   ![Adobe簽署連結](/help/forms/using/assets/adobe_sign_link.png)

**使用者指示：**

1. 檢查&quot;**我同意**「 」方塊。
1. 按一下「**Accept**「。
1. 捲動至已檢閱檔案的底部。
1. 按一下醒目提示的黃色標籤以簽署檔案。

   ![簽署檔案](/help/forms/using/assets/sign_document_new.png) ![簽署測試檔案](/help/forms/using/assets/sign_test_document.png)

## 政府人員(George) {#government-agent-george}

![政府代理商George](/help/forms/using/assets/george_lang-1.png)

**本節：** George是政府機構業務分析師Aya向請求服務。 George有一個儀表板，他可以在其中檢視已指派給他審閱的所有服務請求應用程式。

### AEM收件匣(George) {#george-user-story-aem-inbox}

**使用者指示：**

1. 導覽至 *https://&lt;aemserver>：&lt;port>/aem/start.html*
1. 按一下使用者圖示（右上角）並使用&quot;**登出**「或」**模擬為**&quot;功能表選項（如果您目前是以管理使用者登入）。

   1. 登入方式：

      1. **使用者：** george.lang
      1. **密碼：** 密碼
   1. 或模擬：

      1. 型別&quot;**George**「」中的「」**模擬為**「欄位。

      1. 按一下「確定」以模擬。


1. 從右上角，按一下通知（鈴鐺）圖示。
1. 按一下「**檢視全部**」以導覽至「收件匣」。
1. 從收件匣開啟最新的»**健康狀態福利應用程式複查**」任務。

   ![健康狀態福利應用程式複查](/help/forms/using/assets/health_benefits.png)

### 可選：AEM收件匣與MS Dynamics (George) {#george-user-story-aem-inbox-and-ms-dynamics}

由於資料整合和自動化工作流程，Aya的應用程式會與提交資料時自動產生的CRM記錄一起出現。

**使用者指示：**

1. 開啟並檢查唯讀的最適化表單。
1. 按一下「**開啟MS Dynamics**」按鈕，在新視窗中開啟MS Dynamics記錄。
1. 在CRM中，您可以看到所有資訊都可以更新

   1. 選擇性地直接在Dynamics中新增一些稽核附註。

1. 關閉並返回AEM收件匣。

   ![MS Dynamics記錄](/help/forms/using/assets/ms_dynamics.png)

### 返回AEM收件匣(George) {#george-user-story-back-to-aem-inbox}

George會核准Aya的申請，而由於現有的自動化工作流程，也會傳送確認電子郵件給Aya。

**使用者指示：**

1. 導覽至左上角並按一下「**核准**」以核准應用程式。
1. 在強制回應視窗中，您可以為CX銷售機會留下訊息。
1. 按一下「完成」。
1. （公民角色）開啟您的電子郵件使用者端以檢視傳送至Aya的電子郵件。

   ![檢視傳送至Aya的電子郵件](/help/forms/using/assets/email_client.png)

## CX銷售機會(Camila) {#cx-lead-camila}

![Camila （CX主管）](/help/forms/using/assets/camila_santos-1.png)

**本節：** CX業務負責人Camila與Aya建立歡迎電話，說明如何使用她獲批的政府服務。

### （選用） AEM收件匣與MS Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**使用者指示：**

1. 導覽至 *https://&lt;aemserver>：&lt;port>/aem/start.html*
1. 按一下使用者圖示（右上角）並使用&quot;**登出**「或」**模擬為**&quot;功能表選項（如果您目前是以管理使用者登入）。

   1. 登入方式：

      1. **使用者**：camila.santos
      1. **密碼**：密碼
   1. 或模擬：

      1. 型別&quot;**卡蜜拉**「」中的「」**模擬為**「欄位。

      1. 按一下「確定」以模擬。


1. 從右上角，按一下「通知」（鈴鐺）圖示。
1. 按一下「**檢視全部**」以導覽至「收件匣」。
1. 從收件匣開啟最新的»**新連絡人核准**」任務。

![新連絡人核准](/help/forms/using/assets/new_contact_approval.png)

**（選用）使用者指示：**

1. 開啟並檢查唯讀的最適化表單。
1. 按一下「**開啟MS Dynamics**」按鈕，在新視窗中開啟MS Dynamics記錄。
1. 在CRM中，您可以看到所有資訊都可以更新

   1. 選擇性地直接在Dynamics中新增新的呼叫活動。
   1. 開啟&quot;**活動**「 」區段。
   1. 按一下「**新電話**」選項。
   1. 新增電話詳細資料。
   1. 儲存並關閉視窗。

1. 返回AEM，導覽至左上角並按一下「**提交**」以提交申請。
1. 在強制回應視窗中，您可以留下訊息。
1. 按一下「完成」。

   ![活動標籤](/help/forms/using/assets/activities_tab.png) ![確認新連絡人](/help/forms/using/assets/confirm_new_contact.png)

## （可選）歡迎套件公民(Aya) {#welcome-kit-citizen-aya}

**本節：** Aya會收到一封電子郵件，其中包含互動式通訊的連結，其中摘要了她的權益，並包含要填寫的表單欄位。 附帶PDF權益宣告及郵件中互動式通訊信函的連結（主題/品牌與互動式通訊相同）。

### 電子郵件使用者端通知(Aya) {#aya-user-story-email-client}

**使用者指示：**

1. 找到並開啟歡迎套件電子郵件。
1. 捲動至頁面底部的PDF附件。
1. 按一下以開啟PDF附件。
1. 在電子郵件使用者端中向上捲動並按一下「**線上檢視歡迎套件**「。

   1. 這將會開啟相同檔案的Web channel版本。

1. 如需直接PDF的快速參考：

   *https://&lt;aemserver>：&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. 若要直接快速參考積體電路，請執行下列動作：

   *https://&lt;aemserver>：&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr：content？channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![歡迎權益手冊](/help/forms/using/assets/welcome_benefits_handbook.png) ![互動式通訊連結](/help/forms/using/assets/interactive_communication.png)

## 續約提醒市民(Aya) {#renewal-reminder-citizen-aya}

**本節：** Camila也安排了一年後的溝通提醒。 （自動化/執行及電子郵件的「工作流程步驟」）。

### 電子郵件使用者端通知(Aya) {#aya-user-story-email-client-updated}

**使用者指示：**

1. 導覽至您的電子郵件使用者端。
1. 找到並開啟續約提醒電子郵件。
1. 按一下「**提交新的申請**」按鈕以開啟最適化表單。

   1. 本節刻意留空，以支援階段2的資料預填。

   ![續約提醒電子郵件](/help/forms/using/assets/renewal_reminder_email.png)

## （選用）表單資料模型(Camila) {#form-data-model}

**本節**： Camila會導覽至AEM Forms資料整合，在那裡她可以執行快速測試，以檢視透過Form Data Model整合傳送至外部資料來源的資訊確實存在。

### 表單資料模型(Camila) {#form-data-model-camila}

**本節**：Camila會導覽至「資料來源」頁面，驗證伺服器在Derby資料庫中復寫的資料。

1. 使用者體驗完成且使用者提交完成後，Camila會導覽至AEM Forms中的「資料來源」索引標籤(**Forms** > **資料整合**)

1. Camila接著選取AEM Forms **We.gov FDM** 然後編輯 **We.gov註冊FDM**.

1. 然後Camila選取 **連絡人** > **讀取服務** 待測試。

   ![連絡讀取服務](assets/aftia-contact-read-service.jpg)

1. 然後Camila提供連絡人id的測試服務，然後按一下「測試」按鈕。 例如，1或2 （如果您已提交表單）。 如果您尚未提交表單，則不會傳回任何資料。

   ![連絡讀取服務](assets/aftia-test-service.jpg)

1. 然後Camila可以驗證資料是否已成功插入資料來源。

   * Derby DS中的資料類似於以下格式：

   ```xml
      [
         {
         "ADDRESS_COUNTRY": "USA",
         "LAST_NAME": "Tan",
         "ADDRESS_CITY": "New York",
         "FIRST_NAME": "Aya",
         "ADDRESS_STATE": "AL",
         "ADDRESS_LINE1": "123 Street crescent",
         "GENDER_CODE": "2",
         "ADDRESS_LINE2": "123 Street crescent",
         "ADDRESS_POSTAL_CODE": "90210",
         "BIRTH_DATE": "1991-12-12",
         "CONTACT_ID": 1,
         "MIDDLE_NAME": "M",
         "HAS_CHILDREN_CODE": "0"
         }
   ]
   ```

## （選用） Analytics (Camila) {#analytics-cx-lead-camila}

**本節：** Camila會導覽至儀表板，她可以看到跨機構KPI的資訊，例如%的公民開始填寫服務請求表單並放棄、從請求提交到核准/拒絕回應的平均時間長度，以及她已傳送給公民的福利手冊的參與統計資料。

### Adobe Analytics Sites報告(Camila) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. 導覽至 *https://&lt;aemserver>：&lt;port>/sites.html/content*
1. 選取&quot;**AEM Forms We.Gov網站**」以檢視網站頁面。
1. 選取其中一個網站頁面（例如「首頁」），然後選擇「**Analytics與Recommendations**「。

   ![分析和建議](/help/forms/using/assets/analytics_recommendation.jpg)

1. 在此頁面上，您會看到從Adobe Analytics擷取的與AEM Sites頁面相關的資訊(注意：根據設計，此資訊會定期從Adobe Analytics重新整理，不會即時顯示)。

   ![Adobe Analytics關鍵量度](/help/forms/using/assets/analytics_key_metrics.jpg)

1. 回到頁面檢視頁面（在步驟3存取），您也可以透過變更顯示設定來檢視頁面檢視資訊，以檢視「**清單檢視**「。
1. 找到&quot;**檢視**「下拉式選單並選取」**清單檢視**「。

   ![「檢視」下拉式選單中的清單檢視](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. 從相同功能表選取「**檢視設定**」並從「 」中選取您要顯示的欄&#x200B;**分析**「 」區段。

   ![設定欄顯示](/help/forms/using/assets/view_setting_analytics.jpg)

1. 按一下「**更新**」以讓新欄可用。

   ![讓新欄可供使用](/help/forms/using/assets/new_columns_available.jpg)

### Adobe Analytics Forms報告(Camila) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. 导航至

   *https://&lt;aemserver>：&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. 選取&quot;**健康權益的註冊申請**&quot;最適化表單並選取&quot;**Analytics報表**」選項。

   ![健康權益的註冊申請](/help/forms/using/assets/analytics_report_benefits.jpg)

1. 等候頁面載入，並檢視Analytics報表資料。

   ![Analytics報表資料](/help/forms/using/assets/analytics_report_data_updated.jpg)
