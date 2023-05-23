---
title: 變更AEM Forms工作區使用者介面的地區設定
seo-title: Changing the locale of AEM Forms workspace user interface
description: 如何修改AEM Forms工作區，以將文字、摺疊的類別、佇列和程式，以及介面上的日期選擇器本地化。
seo-description: How to modify the AEM Forms workspace to localize text, collapsed categories, queues, and processes, and the date picker on the interface.
uuid: c89ff150-a36e-45cc-99a6-8768dbe58eab
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 89f9d666-28e2-4201-8467-ae90693ca5d2
docset: aem65
exl-id: 9a069486-02a8-4058-adfb-4e0e49d8c0cf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# 變更AEM Forms工作區使用者介面的地區設定{#changing-the-locale-of-aem-forms-workspace-user-interface}

AEM Forms工作區提供英文、法文、德文和日文語言的立即可用支援。 它還提供將AEM Forms工作區使用者介面本地化為任何其他語言的功能。

將AEM Forms工作區使用者介面本地化為您選擇的語言：

* 將AEM Forms工作區的文字當地語系化。
* 將摺疊的類別、佇列和程式當地語系化。
* 將日期選擇器本地化

在執行上述步驟之前，請務必遵循下列步驟操作： [AEM Forms工作區自訂的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md).

>[!NOTE]
>
>若要變更AEM Forms工作區的登入畫面語言，請參閱 [建立新的登入畫面](../../forms/using/creating-new-login-screen.md).

## 本地化文字 {#localizing-text}

執行以下步驟以新增對語言的支援 *新增* 和瀏覽器地區代碼 *nw*.

1. 登入CRXDE Lite。
CRXDE Lite的預設URL為 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 導覽至該位置 `apps/ws/locales` 並建立新資料夾 `nw.`
1. 複製檔案 `translation.json`從位置 `/apps/ws/locales/en-US` 目標位置 `/apps/ws/locales/nw` .
1. 導覽至 `/apps/ws/locales/nw` 並開啟 `translation.json` 進行編輯。 對translation.json檔案進行地區設定的特定變更。

   下列範例包含AEM Forms工作區中英文與法文地區設定的translation.json檔案。

   ![translation_json_in_en](assets/translation_json_in_en.png) ![translation_json_in_fr](assets/translation_json_in_fr.png)

## 本地化摺疊的類別、佇列和程式 {#localizing-collapsed-categories-queues-and-processes}

AEM Forms工作區使用影像來顯示類別、佇列和程式的標題。 您需要開發套件將這些標頭當地語系化。 如需建立開發套件的詳細資訊，請參閱 [正在建置AEM Forms工作區程式碼。](introduction-customizing-html-workspace.md#building-html-workspace-code)

在下列步驟中，假設新的當地語系化影像檔案為 *Categories_nw.png*， *Queue_nw.png*、和 *Processes_nw.png*. 建議的影像寬度為19px。

>[!NOTE]
>
>尋找瀏覽器的瀏覽器語言地區設定代碼。 打开 `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![collapsing_panels_image](assets/collapsing_panels_image.png)

執行以下步驟將影像當地語系化：

1. 使用WebDAV使用者端，將影像檔案置於 */apps/ws/images* 資料夾。
1. 導覽至 */apps/ws/css*. 開啟 *newStyle.css* 編輯及新增下列專案：

   ```css
   #categoryListBar .content.nw {
        background: #3e3e3e url(../images/Categories_nw.png) no-repeat 10px 10px;
    }
   
   #filterListBar .content.nw {
       background: #3e3e3e url(../images/Queues_nw.png) no-repeat 10px 10px;
   }
   
   #processNameListBar .content.nw {
       background: #3e3e3e url(../images/Processes_nw.png) no-repeat 10px 10px;
   }
   ```

1. 執行中列出的所有語意變更 [工作區自訂](../../forms/using/introduction-customizing-html-workspace.md) 文章。
1. 導覽至 *js/runtime/utility* 資料夾並開啟 *usersession.js* 檔案進行編輯。
1. 找出原始程式碼區塊中列出的程式碼並新增條件 *lang ！== &#39;nw&#39;* 至if陳述式：

   ```javascript
   // Orignal code
   setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

   ```javascript
   //new code
    setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP' && lang !== 'nw')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

## 將日期選擇器本地化 {#localizing-date-picker}

您需要開發套件才能將 *日期選取器* API。 如需建立開發套件的詳細資訊，請參閱 [建立AEM Forms工作區程式碼](introduction-customizing-html-workspace.md#building-html-workspace-code).

1. 下載並解壓縮 [jQuery UI套件](https://jqueryui.com/download/all/)，導覽至 *&lt;extracted jquery=&quot;&quot; ui=&quot;&quot; package=&quot;&quot;>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n。
1. 將地區設定代碼的jquery.ui.datepicker-nw.js檔案複製到apps/ws/js/libs/jqueryui，並對檔案進行地區設定特定變更。
1. 導覽至 `apps/ws/js` 並開啟 `jquery.ui.datepicker-nw.js` 檔案進行編輯。
1. 在main.js檔案中建立別名 `jquery.ui.datepicker-nw.js.` 為建立別名的程式碼 `jquery.ui.datepicker-nw.js` 檔案為：

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. 使用別名 `jqueryuidatepickernw` 以包含 `jquery.ui.datepicker-nw.js` 檔案中選取的日期選取器。 日期選擇器用於下列檔案中：

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   以下程式碼範例說明如何新增jquery.ui.datepicker-nw.js專案：

   ```json
   //Original Code
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, slimScroll, UserSearch, LogManager, Logger) {
   ```

   ```json
   // Code with Date Picker alias for new language
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'jqueryuidatepickernw', // Date Picker alias
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, jQueryUIDatePickerNW, slimScroll, UserSearch, LogManager, Logger) {
   ```

1. 在所有使用日期選擇器API的檔案中，變更預設的日期選擇器API設定。 下列檔案會使用datepicker API：

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js

   變更下列程式碼以新增地區設定：

   ```javascript
   if (locale === 'ja-JP') {
      $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
      $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
      $.datepicker.setDefaults($.datepicker.regional.fr);
   } else {
      $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```

   ```javascript
   if (locale === 'ja-JP') {
       $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
       $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
       $.datepicker.setDefaults($.datepicker.regional.fr);
   } else if (locale === 'nw') {
       $.datepicker.setDefaults($.datepicker.regional.nw);
   } else {
       $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```
