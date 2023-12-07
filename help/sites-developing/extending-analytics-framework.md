---
title: 自定义Adobe Analytics框架
description: 了解如何为Adobe Experience Manager自定义Adobe Analytics框架。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: ab0d4f2e-f761-4510-ba51-4a2dcea49601
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# 自定义Adobe Analytics框架{#customizing-the-adobe-analytics-framework}

Adobe Analytics框架确定使用Adobe Analytics跟踪的信息。 要自定义默认框架，请使用JavaScript添加自定义跟踪，集成Adobe Analytics插件，以及更改用于跟踪的框架中的常规设置。

## 关于为框架生成的JavaScript {#about-the-generated-javascript-for-frameworks}

当页面与Adobe Analytics框架关联时，该页面包括 [对Analytics模块的引用](/help/sites-administering/adobeanalytics.md)，会自动为页面生成analytics.sitecatalyst.js文件。

页面中的JavaScript将创建 `s_gi`对象(s_code.js Adobe Analytics库定义)并将值分配给其属性。 对象实例的名称为 `s`. 本节中介绍的代码示例对此进行了多处引用 `s` 变量。

以下示例代码类似于analytics.sitecatalyst.js文件中的代码：

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";

/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

使用自定义JavaScript代码自定义框架时，将更改此文件的内容。

## 配置Adobe Analytics属性 {#configuring-adobe-analytics-properties}

Adobe Analytics中有多个预定义变量可以在一个框架中进行配置。 此 **charset**， **cookieLifetime**， **currencyCode** 和 **trackInlineStats** 变量包含在 **常规Analytics设置** 默认列表。

![aa-22](assets/aa-22.png)

您可以将变量名称和值添加到列表中。 这些预定义变量和您添加的任何变量用于配置 `s` 对象。 以下示例说明如何添加 `prop10` 值属性 `CONSTANT` 在JavaScript代码中表示：

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.prop10= 'CONSTANT';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";
```

请按下列步骤将变量添加到列表中：

1. 在Adobe Analytics Framework页面上，展开 **常规Analytics设置** 区域。
1. 在变量列表下方，单击添加项目以向列表中添加新变量。
1. 在左侧单元格中，输入变量的名称，例如， `prop10`.

1. 在右侧列中，输入变量的值，例如， `CONSTANT`.

1. 要删除变量，请单击变量旁边的(-)按钮。

>[!NOTE]
>
>输入变量和值时，请确保格式和拼写正确，或者 **将不会发送呼叫** 具有正确的值/变量对。 拼写错误的变量和值甚至可能会阻止调用的发生。
>
>请咨询您的Adobe Analytics代表，以确保正确设置这些变量。

>[!CAUTION]
>
>此列表中的某些变量为 **必需** 以使Adobe Analytics调用正常运行(例如， **currencyCode**， **charSet**)
>
>因此，即使将它们从框架中删除，在进行Adobe Analytics调用时，它们仍会附加一个默认值。

### 将自定义JavaScript添加到Adobe Analytics框架 {#adding-custom-javascript-to-an-adobe-analytics-framework}

中的免费JavaScript框 **常规Analytics设置** 区域用于将自定义代码添加到Adobe Analytics框架。

![aa-21](assets/aa-21.png)

您添加的代码会附加到analytics.sitecatalyst.js文件中。 因此，您可以访问 `s` 变量，它是 `s_gi` 在中定义的JavaScript对象 `s_code.js`. 例如，添加以下代码等同于添加名为的变量 `prop10` 值 `CONSTANT`，这是上一节中的示例：

`s.prop10= 'CONSTANT';`

中的代码 [analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md) 文件(包括Adobe Analytics的内容) `s-code.js` 文件)包含以下代码：

`if (s.usePlugins) s.doPlugins(s)`

以下过程演示了如何使用JavaScript框自定义Adobe Analytics跟踪。 如果您的JavaScript需要使用Adobe Analytics插件， [集成它们](/help/sites-administering/adobeanalytics.md) 进入AEM。

1. 将以下JavaScript代码添加到框中，以便 `s.doPlugins` 执行：

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >如果您要在Adobe Analytics调用中发送变量，而这些变量已按照某种方式进行了自定义，而无法通过基本拖放界面或通过Adobe Analytics视图中的内联JavaScript来完成，则需要此代码。
   >
   >如果自定义变量在s_doPlugins函数之外，则将在Adobe Analytics调用中以*未定义*的形式发送它们

1. 将您的JavaScript代码添加到 **s_doPlugins** 函数。

以下示例使用常用分隔符“|”按层级顺序连接页面上捕获的数据。

Adobe Analytics框架具有以下配置：

* 此 `prop2` Adobe Analytics变量已映射到 `pagedata.sitesection` 站点属性。

* 此 `prop3` Adobe Analytics变量已映射到 `pagedata.subsection` 站点属性。

* 以下代码将添加到免费JavaScript框中：

  ```
  s.usePlugins=true;
   function s_doPlugins(s) {
   s.prop1 = s.prop2+'|'+s.prop3;
   }
   s.doPlugins=s_doPlugins;
  ```

* 当访问使用该框架的网页时（或者在编辑模式下重新加载或预览该页面时），将执行对Adobe Analytics的调用。

例如，Adobe Analytics中生成以下值：

![aa-20](assets/aa-20.png)

### 为所有Adobe Analytics框架添加全局自定义代码 {#adding-global-custom-code-for-all-adobe-analytics-frameworks}

提供集成到所有Adobe Analytics框架中的自定义JavaScript代码。 当页面的Adobe Analytics框架不包含自定义时 [自由格式的JavaScript](/help/sites-administering/adobeanalytics.md)，则/libs/cq/analytics/components/sitecatalyst/config.js.jsp脚本生成的JavaScript将附加到 [analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md) 文件。 默认情况下，该脚本无效，因为它已被注释掉。 代码还会设置 `s.usePlugins` 到 `false`：

```
/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

analytics.sitecatalyst.js文件中的代码(包括Adobe Analytics s_code.js文件的内容)包含以下代码：

如果(s.usePlugins) s.doPlugins(s)

因此，您的JavaScript应将 `s.usePlugins` 到 `true` 因此任何在 `s_doPlugins` 函数被执行。 要自定义代码，请使用使用您自己的JavaScript的文件来叠加config.js.jsp文件。 如果您的JavaScript需要使用Adobe Analytics插件， [集成它们](/help/sites-administering/adobeanalytics.md) 进入AEM。

>[!NOTE]
>
>请勿编辑/libs/cq/analytics/components/sitecatalyst/config.js.jsp文件。 某些AEM升级或维护任务可以重新安装原始文件，从而删除更改。

1. 在CRXDE Lite中，创建/apps/cq/analytics/components文件夹结构：

   1. 右键单击/apps文件夹，然后单击“创建”>“创建文件夹”。
   1. 指定 `cq` 作为文件夹名称，然后单击“确定”。
   1. 同样，创建 `analytics` 和 `components` 文件夹。

1. 右键单击 `components` 创建文件夹，然后单击“创建”>“创建组件”。 指定以下属性值：

   * 标签： `sitecatalyst`
   * 标题： `sitecatalyst`
   * 超级类型： `/libs/cq/analytics/components/sitecatalyst`
   * 组： `hidden`

1. 反复单击“Next（下一步）” ，直到启用“OK（确定）”按钮，然后单击“OK（确定）”。

   sitecatalyst组件包含自动创建的sitecatalyst.jsp文件。

1. 右键单击sitecatalyst.jsp文件，然后单击删除。

1. 右键单击sitecatalyst组件，然后单击“创建”>“创建文件”。 指定名称 `config.js.jsp` 然后单击“确定”。

   config.js.jsp文件会自动打开以进行编辑。

1. 将以下文本添加到文件中，然后单击“全部保存”：

   ```java
   <%@page session="true"%>
   /* Plugin Config */
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom plugin code here
   }
   s.doPlugins=s_doPlugins;
   ```

   现在，对于使用Adobe Analytics框架的所有页面，/apps/cq/analytics/components/sitecatalyst/config.js.jsp脚本生成的JavaScript代码将插入analytics.sitecatalyst.js文件中。

1. 添加要在中执行的JavaScript代码 `s_doPlugins` 函数，然后单击“全部保存”。

>[!CAUTION]
>
>如果页面框架的自由格式JavaScript中存在任何文本（即使只是空白），则会忽略config.js.jsp。

### 在AEM中使用Adobe Analytics插件 {#using-adobe-analytics-plugins-in-aem}

获取Adobe Analytics插件的JavaScript代码，并将它们集成到AEM中的Adobe Analytics框架中。 将代码添加到类别的客户端库文件夹中 `sitecatalyst.plugins` 以便它们可用于您的自定义JavaScript代码。

例如，如果您将 `getQueryParams` 插件，您可以从以下位置调用插件： `s_doPlugins` 自定义JavaScript函数。 以下示例代码在中发送查询字符串 **&quot;pid&quot;** 从反向链接的URL中查找 **EVAR1**：触发Adobe Analytics调用时。

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM会安装以下Adobe Analytics插件，以便默认情况下可以使用：

* getQueryParam()
* getPreviousValue()
* split()

/libs/cq/analytics/clientlibs/sitecatalyst/plugins客户端库文件夹中的sitecatalyst.plugins类别中包含这些插件。

>[!NOTE]
>
>为插件创建客户端库文件夹。 请勿将插件添加到 `/libs/cq/analytics/clientlibs/sitecatalyst/plugins` 文件夹。 这种做法可确保您对 `sitecatalyst.plugins` 在AEM重新安装或升级任务期间，不会覆盖类别。

使用以下过程可为插件创建客户端库文件夹。 您只需执行一次此过程。 要将插件添加到客户端库文件夹，请使用以下步骤。

1. 在Web浏览器中，打开CRXDE Lite。 ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. 右键单击/apps/my-app/clientlibs文件夹，然后单击“创建”>“创建节点”。 输入以下属性值，然后单击“确定”：

   * 名称：客户端库文件夹的名称，如my-plugins

   * 类型：cq：ClientLibraryFolder

1. 选择您创建的客户端库文件夹，并使用右下方的属性栏添加以下属性：

   * 名称：类别
   * 类型：字符串
   * 值： sitecatalyst.plugins
   * 多：已选择

   在“编辑”窗口中单击“确定”以确认属性值。

1. 右键单击您创建的客户端库文件夹，然后单击“创建”>“创建文件”。 对于文件名，请键入js.txt ，然后单击“确定”。

1. 单击“全部保存”。

使用以下过程可获取插件代码，将该代码存储在AEM存储库中，并将它添加到您的客户端库文件夹中。

1. 登录 [sc.omniture.com](https://sc.omniture.com/login/) 使用您的Adobe Analytics帐户。
1. 在登陆页面上，转到“帮助”>“帮助主页”。
1. 在左侧的目录中，单击“Implementation Plug-ins”（实施插件）。
1. 单击要添加插件的链接，并在打开页面时，找到该插件的JavaScript源代码，然后选择该代码并复制它。

1. 右键单击您的客户端库文件夹，然后单击“创建”>“创建文件”。 对于文件名，请键入要集成的插件的名称，后跟.js，然后单击“确定”。 例如，如果要集成getQueryParam插件，请将文件命名为getQueryParam.js。

   创建文件时，将打开该文件以进行编辑。

1. 将插件JavaScript代码粘贴到文件中，单击“全部保存”，然后关闭该文件。

1. 从客户端库文件夹中打开js.txt文件。

1. 在新行中，添加包含插件的文件的名称，例如getQueryParam.js。 然后，单击“全部保存”并关闭文件。

>[!NOTE]
>
>在使用插件时，请确保也集成任何支持插件，否则插件JavaScript将无法识别它对支持插件中的函数进行的调用。 例如，getPreviousValue()插件需要split()插件才能正常运行。
>
>需要将支持插件的名称添加到 **js.txt** 也一样。
