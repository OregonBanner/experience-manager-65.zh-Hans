---
title: 自定义Adobe Analytics Framework
seo-title: 自定义Adobe Analytics Framework
description: 'null'
seo-description: 'null'
uuid: 444a29c2-3b4e-4d21-adc0-5f317ece2b77
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 11c0aac6-a7f6-4d6b-a080-b04643045a64
translation-type: tm+mt
source-git-commit: 0dc96f07e45ccbfea4edc87431677ada5b1bfa8c

---


# 自定义Adobe Analytics Framework{#customizing-the-adobe-analytics-framework}

Adobe Analytics框架可确定使用Adobe Analytics跟踪的信息。 要自定义默认框架，您可以使用javascript添加自定义跟踪、集成Adobe Analytics插件以及更改用于跟踪的框架中的常规设置。

## 关于为框架生成的javascript {#about-the-generated-javascript-for-frameworks}

当页面与Adobe Analytics框架关联且该页面包含对 [Analytics模块的引用时](/help/sites-administering/adobeanalytics.md)，将自动为该页面生成analytics.sitecatalyst.js文件。

页面中的javascript会创建 `s_gi`一个对象（s_code.js Adobe Analytics库定义的对象），并为其属性分配值。 对象实例的名称为 `s`。 本节中介绍的代码示例对此变量进行了若干 `s` 引用。

以下示例代码与analytics.sitecatalyst.js文件中的代码类似：

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

当您使用自定义javascript代码自定义框架时，您会更改此文件的内容。

## 配置Adobe Analytics属性 {#configuring-adobe-analytics-properties}

Adobe Analytics中有许多预定义变量，可在框架上进行配置。 默认情 **况下**,Set **、** cookieLifetime **、** currencyCharvariables和trackCharvariables在Adobe Analytics Analytics InlineList中包括 **Charvariables的集、cookieLifetime****** 、currencyCode和trackCharvariables。

![aa-22](assets/aa-22.png)

您可以向列表添加变量名和值。 这些预定义变量和您添加的任何变量用于配置analytics.sitecatalyst.js `s` 文件中对象的属性。 以下示例显示了如何在javascript `prop10` 代码中 `CONSTANT` 显示已添加的值属性：

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

请按照以下过程将变量添加到列表中：

1. 在Adobe Analytics框架页面上，展开“常规 **分析设置** ”区域。
1. 在变量列表下，单击添加项以向列表添加新变量。
1. 在左侧单元格中，输入变量的名称，例如 `prop10`。

1. 在右列中，输入变量的值，例如 `CONSTANT`。

1. 要删除变量，请单击该变量旁的(-)按钮。

>[!NOTE]
>
>输入变量和值时，请确保其格式正确且拼写正确，否 **则调用不会与正确的值** /变量对一起发送。 拼写错误的变量和值甚至可以阻止调用的发生。
>
>请咨询Adobe Analytics代表，确保正确设置这些变量。

>[!CAUTION]
>
>此列表中的某些变量是必 **需的** ，以便Adobe Analytics调用能够正确运行(例如， **currencyCode**、 **charSet**)
>
>因此，即使从框架本身中删除了这些组件，在进行Adobe Analytics调用时，它们仍会附加一个默认值。

### 将自定义javascript添加到Adobe Analytics Framework {#adding-custom-javascript-to-an-adobe-analytics-framework}

“常规分析设置”区域中的免 **费的javascript框** ，允许您向Adobe Analytics框架添加自定义代码。

![aa-21](assets/aa-21.png)

您添加的代码将附加到analytics.sitecatalyst.js文件中。 因此，您可以访问 `s` 变量，该变量是中定义 `s_gi` 的javascript对象的实例 `s_code.js`。 例如，添加以下代码等效于添加名为value的 `prop10` 变量 `CONSTANT`，这是上一节中的示例：

`s.prop10= 'CONSTANT';`

analytics.sitecatalyst.js文 [件中的代码](/help/sites-developing/extending-analytics-components.md) （包括Adobe Analytics文件的内容）包 `s-code.js` 含以下代码：

`if (s.usePlugins) s.doPlugins(s)`

以下过程演示了如何使用javascript框自定义Adobe Analytics跟踪。 如果您的javascript需要使用Adobe Analytics插件，请将 [其集成](/help/sites-administering/adobeanalytics.md) 到AEM中。

1. 将以下javascript代码添加到框中，以便 `s.doPlugins` 执行：

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >如果要在Adobe Analytics调用中发送变量，这些变量以某种方式进行了自定义，无法通过基本的拖放界面或通过Adobe Analytics视图中的内联javascript完成。
   >
   >如果自定义变量不在s_doPlugins函数之外，则在Adobe Analytics调用中，这些变量将作为*undefined *发送

1. 在 **s_doPlugins函数中添加javascript代码** 。

以下示例使用“|”的公用分隔符，按分层顺序连接在页面上捕获的数据。

Adobe Analytics框架具有以下配置：

* Adobe `prop2` Analytics变量将映射到站点 `pagedata.sitesection` 属性。

* Adobe `prop3` Analytics变量将映射到站点 `pagedata.subsection` 属性。

* 以下代码将添加到免费的javascript框中：

   ```
   s.usePlugins=true;
    function s_doPlugins(s) {
    s.prop1 = s.prop2+'|'+s.prop3;
    }
    s.doPlugins=s_doPlugins;
   ```

* 当访问使用框架的网页时（或在编辑模式下，重新加载或预览页面），将执行对Adobe Analytics的调用。

例如，Adobe Analytics中会生成以下值：

![aa-20](assets/aa-20.png)

### 为所有Adobe Analytics框架添加全局自定义代码 {#adding-global-custom-code-for-all-adobe-analytics-frameworks}

提供集成到所有Adobe Analytics框架中的自定义javascript代码。 当页面的Adobe Analytics框架不包含自定义自 [由格式的javascript](/help/sites-administering/adobeanalytics.md)，则/libs/cq/analytics/components/sitecatalyst/config.js.jsp脚本生成的javascript将附加到 [analytics.sitecatalyst.js文件中](/help/sites-administering/adobeanalytics.md) 。 默认情况下，脚本不起作用，因为脚本已被注释掉。 代码还设置 `s.usePlugins` 为 `false`:

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

analytics.sitecatalyst.js文件（包括Adobe Analytics s_code.js文件的内容）中的代码包含以下代码：

if(s.usePlugins)s.doPlugins

因此，您的javascript应该设 `s.usePlugins` 置为 `true` 这样，函数中的任何代码 `s_doPlugins` 都将被执行。 要自定义代码，请将config.js.jsp文件与使用您自己的javascript的文件叠加。 如果您的javascript需要使用Adobe Analytics插件，请将 [其集成](/help/sites-administering/adobeanalytics.md) 到AEM中。

>[!NOTE]
>
>请勿编辑/libs/cq/analytics/components/sitecatalyst/config.js.jsp文件。 某些AEM升级或维护任务可以重新安装原始文件，从而删除您所做的更改。

1. 在CRXDE Lite中，创建/apps/cq/analytics/components文件夹结构：

   1. 右键单击/apps文件夹，然后单击创建>创建文件夹。
   1. 指定 `cq` 为文件夹名称，然后单击“确定”。
   1. 同样，创建和 `analytics` 文件 `components` 夹。

1. 右键单击刚创建 `components` 的文件夹，然后单击创建>创建组件。 指定以下属性值：

   * 标签: `sitecatalyst`
   * 标题: `sitecatalyst`
   * 超级类型: `/libs/cq/analytics/components/sitecatalyst`
   * 组: `hidden`

1. 重复单击“下一步”，直到启用“确定”按钮，然后单击“确定”。

   sitecatalyst组件包含自动创建的sitecatalyst.jsp文件。

1. 右键单击sitecatalyst.jsp文件，然后单击删除。

1. 右键单击SiteCatalyst组件，然后单击创建>创建文件。 指定名称，然 `config.js.jsp` 后单击“确定”。

   config.js.jsp文件将自动打开以进行编辑。

1. 将以下文本添加到文件，然后单击“全部保存”:

   ```java
   <%@page session="true"%>
   /* Plugin Config */
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom plugin code here
   }
   s.doPlugins=s_doPlugins;
   ```

   /apps/cq/analytics/components/sitecatalyst/config.js.jsp脚本生成的javascript代码现已插入到analytics.sitecatalyst.js文件中，以供所有使用Adobe Analytics框架的页面使用。

1. 添加要在函数中执行的javascript代码，然 `s_doPlugins` 后单击“全部保存”。

>[!CAUTION]
>
>如果页面框架的自由形式javascript中存在任何文本（甚至只有空白），则config.js.jsp将被忽略。

### 在AEM中使用Adobe Analytics插件 {#using-adobe-analytics-plugins-in-aem}

获取Adobe Analytics插件的javascript代码，并将它们集成到AEM中的Adobe Analytics框架中。 将代码添加到类别的客户端库文件夹，以 `sitecatalyst.plugins` 便自定义javascript代码可以使用这些代码。

例如，如果集成插 `getQueryParams` 件，则可以从自定义javascript的函 `s_doPlugins` 数调用插件。 以下示例代码在触发Adobe Analytics调用时， **从引荐的** URL发送“pid”中的查询字符串 **eVar1**。

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM会安装以下Adobe Analytics插件，以便默认情况下可用：

* getQueryParam()
* getPreviousValue()
* split()

/libs/cq/analytics/clientlibs/sitecatalyst/plugins客户端库文件夹包含sitecatalyst.plugins类别中的这些插件。

>[!NOTE]
>
>为您的插件创建新的客户端库文件夹。 请勿将插件添加到文 `/libs/cq/analytics/clientlibs/sitecatalyst/plugins` 件夹。 此做法可确保在AEM重新安装或 `sitecatalyst.plugins` 升级任务期间不会覆盖您对类别的贡献。

请按照以下过程为插件创建客户端库文件夹。 您只需执行此过程一次。 要将插件添加到客户端库文件夹，请使用后续过程。

1. 在Web浏览器中，打开CRXDE Lite。 ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. 右键单击/apps/my-app/clientlibs文件夹，然后单击创建>创建节点。 输入以下属性值，然后单击确定：

   * 名称：客户端库文件夹的名称，如my-plugins

   * 类型：cq:ClientLibraryFolder

1. 选择刚刚创建的客户端库文件夹，然后使用右下方的属性栏添加以下属性：

   * 名称：类别
   * 类型：字符串
   * 值：sitecatalyst.plugins
   * 多：已选定
   在“编辑”窗口中单击“确定”以确认属性值。

1. 右键单击刚创建的客户端库文件夹，然后单击“创建”>“创建文件”。 对于文件名类型js.txt，然后单击“确定”。

1. 单击“全部保存”。

请按照以下过程获取插件代码，将代码存储在AEM存储库中，然后将代码添加到客户端库文件夹。

1. 使用您 [的Adobe Analytics帐户登录](https://sc.omniture.com) sc.omniture.com。
1. 在登陆页面上，转到帮助>帮助主页。
1. 在左侧的目录中，单击“实施插件”。
1. 单击要添加的插件的链接，当页面打开时，找到插件的javascript源代码，然后选择代码并复制它。

1. 右键单击客户端库文件夹，然后单击“创建”>“创建文件”。 对于文件名，键入要集成的插件的名称，后跟。js，然后单击确定。 例如，如果要集成getQueryParam插件，请将文件命名为getQueryParam.js。

   创建文件时，该文件将打开进行编辑。

1. 将插件javascript代码粘贴到文件中，单击“全部保存”，然后关闭文件。

1. 从客户端库文件夹打开js.txt文件。

1. 在新行中，添加包含插件的文件的名称，例如getQueryParam.js。 然后，单击“全部保存”并关闭文件。

>[!NOTE]
>
>使用插件时，请确保也集成任何支持插件，否则插件javascript将无法识别它对支持插件中的函数所发出的调用。 例如，getPreviousValue()插件需要split()插件才能正常工作。
>
>还需要将支持插件的名称添加到 **js.txt** 。
