---
title: 自定义Adobe Analytics框架
seo-title: 自定义Adobe Analytics框架
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
workflow-type: tm+mt
source-wordcount: '1620'
ht-degree: 0%

---


# 自定义Adobe Analytics框架{#customizing-the-adobe-analytics-framework}

Adobe Analytics框架确定与Adobe Analytics一起跟踪的信息。 要自定义默认框架，您可以使用javascript添加自定义跟踪、集成Adobe Analytics插件以及更改用于跟踪的框架中的常规设置。

## 关于框架{#about-the-generated-javascript-for-frameworks}生成的javascript

当页面与Adobe Analytics框架关联且页面包含对Analytics模块](/help/sites-administering/adobeanalytics.md)的[引用时，将为该页面自动生成analytics.sitecatalyst.js文件。

页面中的javascript创建`s_gi`对象(s_code.jsAdobe Analytics库定义)并为其属性赋值。 对象实例的名称为`s`。 本节中介绍的代码示例对此`s`变量进行了若干引用。

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

## 配置Adobe Analytics属性{#configuring-adobe-analytics-properties}

Adobe Analytics内有许多预定义变量，可在框架上进行配置。 默认情况下，**charset**、**cookieLifetime**、**currencyCode**&#x200B;和&#x200B;**trackInlineStats**&#x200B;变量包括在&#x200B;**常规分析设置**&#x200B;列表中。

![aa-22](assets/aa-22.png)

您可以向列表添加变量名和值。 这些预定义变量和您添加的任何变量用于配置analytics.sitecatalyst.js文件中`s`对象的属性。 以下示例显示值`CONSTANT`的已添加`prop10`属性在javascript代码中的表示方式：

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

请按照以下过程向列表添加变量：

1. 在您的Adobe Analytics框架页面上，展开&#x200B;**常规分析设置**&#x200B;区域。
1. 在变量列表下，单击添加项以向列表添加新变量。
1. 在左侧单元格中，输入变量的名称，例如`prop10`。

1. 在右侧列中，输入变量的值，例如`CONSTANT`。

1. 要删除变量，请单击该变量旁的(-)按钮。

>[!NOTE]
>
>输入变量和值时，请确保它们的格式正确且拼写正确，或者&#x200B;**调用不会以正确的值／变量对发送**。 拼写错误的变量和值甚至可以阻止调用的发生。
>
>请咨询您的Adobe Analytics代表，确保正确设置这些变量。

>[!CAUTION]
>
>此列表中的某些变量为&#x200B;**mandatory**，以使Adobe Analytics调用能够正确运行，(例如，**currencyCode**, **charSet**)
>
>因此，即使从框架本身删除它们，在进行Adobe Analytics调用时，它们仍会附加默认值。

### 将自定义javascript添加到Adobe Analytics框架{#adding-custom-javascript-to-an-adobe-analytics-framework}

使用&#x200B;**常规分析设置**&#x200B;区域中的“免费”javascript框，您可以向Adobe Analytics框架添加自定义代码。

![aa-21](assets/aa-21.png)

您添加的代码将附加到analytics.sitecatalyst.js文件。 因此，您可以访问`s`变量，该变量是`s_gi` javascript对象的一个实例，该对象在`s_code.js`中定义。 例如，添加以下代码等同于添加值`CONSTANT`的名为`prop10`的变量，前一节中的示例如下：

`s.prop10= 'CONSTANT';`

[analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md)文件(包括Adobe Analytics`s-code.js`文件的内容)中的代码包含以下代码：

`if (s.usePlugins) s.doPlugins(s)`

以下过程演示了如何使用javascript框自定义Adobe Analytics跟踪。 如果您的javascript需要使用Adobe Analytics插件，[将它们](/help/sites-administering/adobeanalytics.md)集成到AEM中。

1. 将以下javascript代码添加到框中，以执行`s.doPlugins`:

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >如果要在Adobe Analytics调用中发送变量，这些变量以某种方式进行了自定义，无法通过基本的拖放界面或通过Adobe Analytics视图内嵌的javascript完成。
   >
   >如果自定义变量不在s_doPlugins函数之外，则在Adobe Analytics调用中，它们将作为*undefined *发送

1. 在&#x200B;**s_doPlugins**&#x200B;函数中添加javascript代码。

以下示例使用公共分隔符“|”以分层顺序连接在页面上捕获的数据。

Adobe Analytics框架具有以下配置：

* `prop2`Adobe Analytics变量映射到`pagedata.sitesection`站点属性。

* `prop3`Adobe Analytics变量映射到`pagedata.subsection`站点属性。

* 以下代码将添加到免费的javascript框中：

   ```
   s.usePlugins=true;
    function s_doPlugins(s) {
    s.prop1 = s.prop2+'|'+s.prop3;
    }
    s.doPlugins=s_doPlugins;
   ```

* 当访问使用框架的网页时（或在编辑模式下重新加载或预览页面），将执行对Adobe Analytics的调用。

例如，在Adobe Analytics生成以下值：

![aa-20](assets/aa-20.png)

### 为所有Adobe Analytics框架添加全局自定义代码{#adding-global-custom-code-for-all-adobe-analytics-frameworks}

提供集成到所有Adobe Analytics框架中的自定义javascript代码。 当页面的Adobe Analytics框架不包含自定义[自由格式javascript](/help/sites-administering/adobeanalytics.md)时，/libs/cq/analytics/components/sitecatalyst/config.js.jsp脚本生成的javascript将附加到[analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md)文件。 默认情况下，脚本无效，因为脚本已被注释掉。 代码还将`s.usePlugins`设置为`false`:

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

analytics.sitecatalyst.js文件(包括Adobe Analyticss_code.js文件的内容)中的代码包含以下代码：

if(s.usePlugins)s.doPlugins

因此，您的javascript应将`s.usePlugins`设置为`true`，以执行`s_doPlugins`函数中的任何代码。 要自定义代码，请使用您自己的javascript将config.js.jsp文件叠加在一起。 如果您的javascript需要使用Adobe Analytics插件，[将它们](/help/sites-administering/adobeanalytics.md)集成到AEM中。

>[!NOTE]
>
>请勿编辑/libs/cq/analytics/components/sitecatalyst/config.js.jsp文件。 某些AEM升级或维护任务可以重新安装原始文件，删除您所做的更改。

1. 在CRXDE Lite中，创建/apps/cq/analytics/components文件夹结构：

   1. 右键单击/apps文件夹，然后单击“创建”>“创建文件夹”。
   1. 指定`cq`作为文件夹名称，然后单击“确定”。
   1. 同样，创建`analytics`和`components`文件夹。

1. 右键单击刚刚创建的`components`文件夹，然后单击创建>创建组件。 指定以下属性值：

   * 标签: `sitecatalyst`
   * 标题: `sitecatalyst`
   * 超级类型: `/libs/cq/analytics/components/sitecatalyst`
   * 组: `hidden`

1. 重复单击“下一步”，直到启用“确定”按钮，然后单击“确定”。

   sitecatalyst组件包含自动创建的sitecatalyst.jsp文件。

1. 右键单击sitecatalyst.jsp文件，然后单击“删除”。

1. 右键单击sitecatalyst组件，然后单击创建>创建文件。 指定名称`config.js.jsp`，然后单击“确定”。

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

   /apps/cq/analytics/components/sitecatalyst/config.js.jsp脚本生成的javascript代码现在已插入到analytics.sitecatalyst.js文件中，用于使用Adobe Analytics框架的所有页面。

1. 添加要在`s_doPlugins`函数中执行的javascript代码，然后单击“全部保存”。

>[!CAUTION]
>
>如果页面框架的自由形式javascript中存在任何文本（甚至只有空格），则忽略config.js.jsp。

### 在AEM {#using-adobe-analytics-plugins-in-aem}中使用Adobe Analytics插件

获取Adobe Analytics插件的javascript代码，并将它们集成到AEM的Adobe Analytics框架中。 将代码添加到类别`sitecatalyst.plugins`的客户端库文件夹，以便自定义javascript代码可以使用它们。

例如，如果集成`getQueryParams`插件，则可以从自定义javascript的`s_doPlugins`函数调用该插件。 以下示例代码在触发Adobe Analytics调用时，从推荐人的URL以&#x200B;**eVar1**&#x200B;的形式发送&#x200B;**&quot;pid&quot;**&#x200B;中的查询字符串。

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM会安装以下Adobe Analytics插件，以便默认提供它们：

* getQueryParam()
* getPreviousValue()
* split()

/libs/cq/analytics/clientlibs/sitecatalyst/plugins客户端库文件夹在sitecatalyst.plugins类别中包含这些插件。

>[!NOTE]
>
>为插件创建新的客户端库文件夹。 请勿向`/libs/cq/analytics/clientlibs/sitecatalyst/plugins`文件夹添加插件。 此做法可确保您在AEM重新安装或升级类别时不会覆盖您对`sitecatalyst.plugins`任务的贡献。

请按照以下过程为插件创建客户端库文件夹。 您只需执行此过程一次。 要将插件添加到客户端库文件夹，请使用后续过程。

1. 在Web浏览器中，打开CRXDE Lite。 ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. 右键单击/apps/my-app/clientlibs文件夹，然后单击“创建”>“创建节点”。 输入以下属性值，然后单击确定：

   * 名称：客户端库文件夹的名称，如my-plugins

   * 类型：cq:ClientLibraryFolder

1. 选择刚刚创建的客户端库文件夹，并使用右下方的属性栏添加以下属性：

   * 名称：类别
   * 类型：字符串
   * 值：sitecatalyst.plugins
   * 多：已选

   在编辑窗口中单击确定以确认属性值。

1. 右键单击刚刚创建的客户端库文件夹，然后单击“创建”>“创建文件”。 对于文件名类型js.txt，然后单击“确定”。

1. 单击“全部保存”。

请按照以下过程获取插件代码，将代码存储在AEM存储库中，然后将代码添加到客户端库文件夹。

1. 使用您的Adobe Analytics帐户登录到[sc.omniture.com](https://sc.omniture.com)。
1. 在登陆页中，转到“帮助”>“帮助主页”。
1. 在左侧的目录中，单击“实施插件”。
1. 单击要添加的插件的链接，当页面打开时，找到插件的javascript源代码，然后选择代码并复制它。

1. 右键单击客户端库文件夹，然后单击“创建”>“创建文件”。 对于文件名，键入要集成的插件的名称，后跟。js，然后单击“确定”。 例如，如果要集成getQueryParam插件，请将文件命名为getQueryParam.js。

   创建文件时，该文件会打开进行编辑。

1. 将插件javascript代码粘贴到文件中，单击“全部保存”，然后关闭文件。

1. 从客户端库文件夹打开js.txt文件。

1. 在新行中，添加包含插件的文件的名称，例如getQueryParam.js。 然后，单击“全部保存”并关闭文件。

>[!NOTE]
>
>使用插件时，请确保也集成任何支持插件，否则插件javascript将无法识别它对支持插件中的函数所发出的调用。 例如，getPreviousValue()插件需要split()插件才能正常工作。
>
>还需要将支持插件的名称添加到&#x200B;**js.txt**。
