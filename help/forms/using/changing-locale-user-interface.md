---
title: 更改AEM Forms工作区用户界面的区域设置
seo-title: Changing the locale of AEM Forms workspace user interface
description: 如何修改AEM Forms工作区以将文本、折叠的类别、队列和进程以及界面上的日期选取器本地化。
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

# 更改AEM Forms工作区用户界面的区域设置{#changing-the-locale-of-aem-forms-workspace-user-interface}

AEM Forms工作区提供英语、法语、德语和日语的开箱即用支持。 它还提供了将AEM Forms工作区用户界面本地化为任何其他语言的功能。

要将AEM Forms工作区用户界面本地化为您选择的语言，请执行以下操作：

* 将AEM Forms工作区的文本本地化。
* 将折叠的类别、队列和流程本地化。
* 本地化日期选取器

在执行上述步骤之前，请确保按照 [AEM Forms工作区自定义的一般步骤](../../forms/using/generic-steps-html-workspace-customization.md).

>[!NOTE]
>
>要更改AEM Forms工作区的登录屏幕的语言，请参阅 [创建新的登录屏幕](../../forms/using/creating-new-login-screen.md).

## 本地化文本 {#localizing-text}

执行以下步骤以添加对语言的支持 *新建* 和浏览器区域设置代码 *nw*.

1. 登录到CRXDE Lite。
默认CRXDE LiteURL为 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 导航到该位置 `apps/ws/locales` 并创建新文件夹 `nw.`
1. 复制文件 `translation.json`从位置 `/apps/ws/locales/en-US` 到位置 `/apps/ws/locales/nw` .
1. 导航到 `/apps/ws/locales/nw` 打开 `translation.json` 进行编辑。 对translation.json文件进行区域设置特定的更改。

   以下示例包含AEM Forms工作区的英语和法语区域设置的translation.json文件。

   ![translation_json_in_en](assets/translation_json_in_en.png) ![translation_json_in_fr](assets/translation_json_in_fr.png)

## 本地化折叠的类别、队列和进程 {#localizing-collapsed-categories-queues-and-processes}

AEM Forms工作区使用图像来显示类别、队列和流程的标题。 您需要开发包才能将这些标头本地化。 有关创建开发包的详细信息，请参阅 [构建AEM Forms工作区代码。](introduction-customizing-html-workspace.md#building-html-workspace-code)

在以下步骤中，假定新的本地化图像文件是 *Categories_nw.png*, *Queue_nw.png*&#x200B;和 *Processes_nw.png*. 推荐的图像宽度为19像素。

>[!NOTE]
>
>查找浏览器的浏览器语言区域设置代码。 打开 `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![collapsing_panels_image](assets/collapsing_panels_image.png)

执行以下步骤将图像本地化：

1. 使用WebDAV客户端，将图像文件放置在 */apps/ws/images* 文件夹。
1. 导航到 */apps/ws/css*. 打开 *newStyle.css* 编辑和添加以下条目：

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

1. 执行 [工作区自定义](../../forms/using/introduction-customizing-html-workspace.md) 文章。
1. 导航到 *js/runtime/utility* 文件夹，然后打开 *usersession.js* 文件进行编辑。
1. 找到原始代码块中列出的代码并添加条件 *朗！== &#39;nw&#39;* 到if语句：

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

## 本地化日期选取器 {#localizing-date-picker}

您需要开发包才能将 *datepicker* API。 有关创建开发包的详细信息，请参阅 [构建AEM Forms工作区代码](introduction-customizing-html-workspace.md#building-html-workspace-code).

1. 下载并提取 [jQuery UI包](https://jqueryui.com/download/all/)，导航到 *&lt;extracted jquery=&quot;&quot; ui=&quot;&quot; package=&quot;&quot;>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n。
1. 将区域设置代码的jquery.ui.datepicker-nw.js文件新复制到apps/ws/js/libs/jqueryui，并对文件进行区域设置特定的更改。
1. 导航到 `apps/ws/js` 打开 `jquery.ui.datepicker-nw.js` 文件进行编辑。
1. 在main.js文件中，为 `jquery.ui.datepicker-nw.js.` 为创建别名的代码 `jquery.ui.datepicker-nw.js` 文件为：

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. 使用别名 `jqueryuidatepickernw` 包含 `jquery.ui.datepicker-nw.js` 文件。 日期选取器在以下文件中使用：

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   以下示例代码显示如何添加jquery.ui.datepicker-nw.js的条目：

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

1. 在所有使用日期选取器API的文件中，更改默认的日期选取器API设置。 日期选取器API用于以下文件：

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js

   更改以下代码以添加新区域设置：

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
