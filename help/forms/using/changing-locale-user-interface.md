---
title: 更改AEM Forms工作区用户界面的区域设置
seo-title: 更改AEM Forms工作区用户界面的区域设置
description: 如何修改AEM Forms工作区以本地化文本、折叠的类别、队列和进程，以及界面上的日期选取器。
seo-description: 如何修改AEM Forms工作区以本地化文本、折叠的类别、队列和进程，以及界面上的日期选取器。
uuid: c89ff150-a36e-45cc-99a6-8768dbe58eab
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 89f9d666-28e2-4201-8467-ae90693ca5d2
docset: aem65
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0

---


# 更改AEM Forms工作区用户界面的区域设置{#changing-the-locale-of-aem-forms-workspace-user-interface}

AEM Forms工作区提供针对英语、法语、德语和日语的开箱即用支持。 它还提供了将AEM Forms工作区用户界面本地化为任何其他语言的功能。

要将AEM Forms Workspace用户界面本地化为您选择的语言，请执行以下操作：

* 本地化AEM Forms工作区的文本。
* 本地化折叠的类别、队列和流程。
* 本地化日期选取器

在执行上述步骤之前，请确保遵循AEM Forms工作区自定 [义的常规步骤中列出的步骤](../../forms/using/generic-steps-html-workspace-customization.md)。

>[!NOTE]
>
>要更改AEM Forms工作区的登录屏幕的语言，请参阅 [创建新的登录屏幕](../../forms/using/creating-new-login-screen.md)。

## 文本本地化 {#localizing-text}

请执行以下步骤以添加对新语言和浏览器区 *域设置* 代码的 *支持*。

1. 登录到CRXDE Lite。
CRXDE Lite的默认URL为 `https://'[server]:[port]'/lc/crx/de/index.jsp`。
1. 导览至该位置并 `apps/ws/locales` 创建新文件夹 `nw.`
1. 将文件从 `translation.json`位置复制 `/apps/ws/locales/en-US` 到位置 `/apps/ws/locales/nw` 。
1. 导航到并 `/apps/ws/locales/nw` 打开以 `translation.json` 进行编辑。 对translation.json文件进行特定于区域设置的更改。

   以下示例包含AEM Forms工作区的英语和法语区域设置的translation.json文件。

   ![translation_json_in_en](assets/translation_json_in_en.png) ![translation_json_in_fr](assets/translation_json_in_fr.png)

## 对折叠的类别、队列和进程进行本地化 {#localizing-collapsed-categories-queues-and-processes}

AEM Forms工作区使用图像显示类别、队列和进程的标题。 您需要开发包来本地化这些标题。 有关创建开发包的详细信息，请参 [阅构建AEM Forms工作区代码。](introduction-customizing-html-workspace.md#building-html-workspace-code)

在以下步骤中，假定新的本地化图像文件是 *类别_nw.png*、 *Queue_nw.png*&#x200B;和 *Processes_nw.png*。 建议的图像宽度为19px。

>[!NOTE]
>
>查找浏览器的浏览器语言区域设置代码。 打开 `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![collapsing_panels_image](assets/collapsing_panels_image.png)

执行以下步骤来本地化图像：

1. 使用WebDAV客户端，将图像文件放在 */apps/ws/images文件夹中* 。
1. 导航到 */apps/ws/css*。 打开 *newStyle.css* ，进行编辑并添加以下条目：

   ```
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

1. 执行工作区自定义文章中列出的所 [有语义更改](../../forms/using/introduction-customizing-html-workspace.md) 。
1. 导览至 *js/runtime/utility文件夹* ，然后打开 ** usersession.js文件进行编辑。
1. 找到原始代码块中列出的代码并添加条 *件lang !== &#39;nw&#39;* to if语句：

   ```
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

   ```
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

## 本地化日期选取器 {#localizing-date-picker}

您需要开发包来本地化 *datepicker* API。 有关创建开发包的详细信息，请参 [阅构建AEM Forms工作区代码](introduction-customizing-html-workspace.md#building-html-workspace-code)。

1. 下载并解压 [缩jQuery UI包](https://jqueryui.com/download/all/)，导航到 *&lt;解压缩jquery UI包>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n。
1. 将区域设置代码的jquery.ui.datepicker-nw.js文件复制到apps/ws/js/libs/jqueryui中，并对文件进行特定于区域设置的更改。
1. 导览至 `apps/ws/js` 并打开要编 `jquery.ui.datepicker-nw.js` 辑的文件。
1. 在main.js文件中，为文件创建别 `jquery.ui.datepicker-nw.js.``jquery.ui.datepicker-nw.js` 名的代码为：

   ```
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. 使用别 `jqueryuidatepickernw` 名将文件包含 `jquery.ui.datepicker-nw.js` 在使用datepicker的所有文件中。 datepicker用于以下文件：

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`
   以下示例代码显示如何添加jquery.ui.datepicker-nw.js条目：

   ```
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

   ```
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

1. 在使用datepicker API的所有文件中，更改默认的datepicker API设置。 datepicker API用于以下文件：

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js
   更改以下代码以添加新区域设置：

   ```
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

   ```
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
