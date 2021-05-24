---
title: 自定义Adobe Analytics框架
seo-title: 自定义Adobe Analytics框架
description: 自定义Adobe Analytics框架
seo-description: 'null'
uuid: 444a29c2-3b4e-4d21-adc0-5f317ece2b77
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 11c0aac6-a7f6-4d6b-a080-b04643045a64
exl-id: ab0d4f2e-f761-4510-ba51-4a2dcea49601
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1624'
ht-degree: 0%

---

# 自定义Adobe Analytics框架{#customizing-the-adobe-analytics-framework}

Adobe Analytics框架可确定与Adobe Analytics一起跟踪的信息。 要自定义默认框架，您可以使用javascript添加自定义跟踪、集成Adobe Analytics插件，以及更改用于跟踪的框架中的常规设置。

## 关于为框架{#about-the-generated-javascript-for-frameworks}生成的Javascript

当页面与Adobe Analytics框架关联，并且该页面包含对Analytics模块](/help/sites-administering/adobeanalytics.md)的[引用时，将自动为该页面生成analytics.sitecatalyst.js文件。

页面中的Javascript会创建一个`s_gi`对象(s_code.js Adobe Analytics库定义了该对象)，并为其属性分配值。 对象实例的名称为`s`。 本节中介绍的代码示例对此`s`变量进行了多项引用。

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

使用自定义Javascript代码自定义框架时，需更改此文件的内容。

## 配置Adobe Analytics属性{#configuring-adobe-analytics-properties}

Adobe Analytics中有许多预定义变量可以在框架上进行配置。 默认情况下，**charset**、**cookieLifetime**、**currencyCode**&#x200B;和&#x200B;**trackInlineStats**&#x200B;变量包含在&#x200B;**“常规Analytics设置”**&#x200B;列表中。

![aa-22](assets/aa-22.png)

您可以向列表添加变量名称和值。 这些预定义变量和您添加的任何变量用于配置analytics.sitecatalyst.js文件中`s`对象的属性。 以下示例显示值`CONSTANT`的已添加`prop10`属性在Javascript代码中的显示方式：

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

请按照以下过程将变量添加到列表：

1. 在Adobe Analytics框架页面上，展开&#x200B;**常规Analytics设置**&#x200B;区域。
1. 在变量列表下，单击添加项目以向列表添加新变量。
1. 在左侧单元格中，输入变量的名称，例如`prop10`。

1. 在右侧列中，输入变量的值，例如`CONSTANT`。

1. 要删除变量，请单击变量旁边的(-)按钮。

>[!NOTE]
>
>输入变量和值时，请确保它们的格式正确且拼写正确，否则将不会发送&#x200B;**调用及正确的值/变量对。**&#x200B;拼写错误的变量和值甚至可以阻止调用的发生。
>
>请咨询您的Adobe Analytics代表，以确保正确设置这些变量。

>[!CAUTION]
>
>为使Adobe Analytics调用能够正常运行，此列表中的某些变量为&#x200B;**必填**(例如，**currencyCode**, **charSet**)
>
>因此，即使从框架本身中删除了这些值，在进行Adobe Analytics调用时，它们仍会附加默认值。

### 向Adobe Analytics框架{#adding-custom-javascript-to-an-adobe-analytics-framework}添加自定义Javascript

使用&#x200B;**常规Analytics设置**&#x200B;区域中的“从Javascript中释放”框，可向Adobe Analytics框架添加自定义代码。

![aa-21](assets/aa-21.png)

您添加的代码会附加到analytics.sitecatalyst.js文件中。 因此，您可以访问`s`变量，该变量是在`s_code.js`中定义的`s_gi` javascript对象的实例。 例如，添加以下代码等同于添加值`CONSTANT`的名为`prop10`的变量，如上一节中的示例：

`s.prop10= 'CONSTANT';`

[analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md)文件(包括Adobe Analytics `s-code.js`文件的内容)中的代码包含以下代码：

`if (s.usePlugins) s.doPlugins(s)`

以下过程演示了如何使用javascript框自定义Adobe Analytics跟踪。 如果您的javascript需要使用Adobe Analytics插件，请[将它们](/help/sites-administering/adobeanalytics.md)集成到AEM中。

1. 将以下javascript代码添加到框中，以便执行`s.doPlugins`:

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >如果要在Adobe Analytics调用中发送已以某种方式自定义的变量，这些变量无法通过基本的拖放界面或通过Adobe Analytics视图中的内联javascript完成，则需要使用此代码。
   >
   >如果自定义变量在s_doPlugins函数之外，它们将在Adobe Analytics调用中作为*undefined *发送

1. 在&#x200B;**s_doPlugins**&#x200B;函数中添加Javascript代码。

以下示例使用通用分隔符“|”按层级顺序连接页面上捕获的数据。

Adobe Analytics框架具有以下配置：

* `prop2` Adobe Analytics变量已映射到`pagedata.sitesection`站点属性。

* `prop3` Adobe Analytics变量已映射到`pagedata.subsection`站点属性。

* 以下代码将添加到“免费使用Javascript”框中：

   ```
   s.usePlugins=true;
    function s_doPlugins(s) {
    s.prop1 = s.prop2+'|'+s.prop3;
    }
    s.doPlugins=s_doPlugins;
   ```

* 当访问使用框架的网页（或在编辑模式下重新加载或预览页面）时，将执行对Adobe Analytics的调用。

例如，以下值在Adobe Analytics中生成：

![aa-20](assets/aa-20.png)

### 为所有Adobe Analytics框架添加全局自定义代码{#adding-global-custom-code-for-all-adobe-analytics-frameworks}

提供可集成到所有Adobe Analytics框架中的自定义Javascript代码。 当页面的Adobe Analytics框架不包含自定义[自由格式的javascript](/help/sites-administering/adobeanalytics.md)时，/libs/cq/analytics/components/sitecatalyst/config.js.jsp脚本生成的javascript将附加到[analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md)文件中。 默认情况下，脚本不起作用，因为它被注释掉。 该代码还会将`s.usePlugins`设置为`false`:

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

analytics.sitecatalyst.js文件(包括Adobe Analytics s_code.js文件的内容)中的代码包含以下代码：

if(s.usePlugins)s.doPlugins

因此，您的Javascript应将`s.usePlugins`设置为`true`，以便执行`s_doPlugins`函数中的任何代码。 要自定义代码，请使用您自己的Javascript文件来叠加config.js.jsp文件。 如果您的javascript需要使用Adobe Analytics插件，请[将它们](/help/sites-administering/adobeanalytics.md)集成到AEM中。

>[!NOTE]
>
>请勿编辑/libs/cq/analytics/components/sitecatalyst/config.js.jsp文件。 某些AEM升级或维护任务可以重新安装原始文件，从而删除您所做的更改。

1. 在CRXDE Lite中，创建/apps/cq/analytics/components文件夹结构：

   1. 右键单击/apps文件夹，然后单击创建>创建文件夹。
   1. 指定`cq`作为文件夹名称，然后单击“确定”。
   1. 同样，创建`analytics`和`components`文件夹。

1. 右键单击刚刚创建的`components`文件夹，然后单击创建>创建组件。 指定以下属性值：

   * 标签: `sitecatalyst`
   * 标题: `sitecatalyst`
   * 超级类型: `/libs/cq/analytics/components/sitecatalyst`
   * 组: `hidden`

1. 反复单击“下一步”直到启用“确定”按钮，然后单击“确定”。

   sitecatalyst组件包含自动创建的sitecatalyst.jsp文件。

1. 右键单击sitecatalyst.jsp文件，然后单击删除。

1. 右键单击sitecatalyst组件，然后单击创建>创建文件。 指定名称`config.js.jsp`，然后单击“确定”。

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

   现在，/apps/cq/analytics/components/sitecatalyst/config.js.jsp脚本生成的Javascript代码将插入到analytics.sitecatalyst.js文件中，用于使用Adobe Analytics框架的所有页面。

1. 添加要在`s_doPlugins`函数中执行的Javascript代码，然后单击“全部保存”。

>[!CAUTION]
>
>如果页面框架的自由格式Javascript中存在任何文本（甚至只有空格），则config.js.jsp将被忽略。

### 在AEM {#using-adobe-analytics-plugins-in-aem}中使用Adobe Analytics插件

获取Adobe Analytics插件的javascript代码，并将它们集成到AEM的Adobe Analytics框架中。 将代码添加到类别`sitecatalyst.plugins`的客户端库文件夹，以便它们可用于您的自定义Javascript代码。

例如，如果集成`getQueryParams`插件，则可以从自定义javascript的`s_doPlugins`函数中调用该插件。 在触发Adobe Analytics调用时，以下示例代码会从反向链接的URL中将&#x200B;**&quot;pid&quot;**&#x200B;中的查询字符串作为&#x200B;**eVar1**&#x200B;发送。

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM会安装以下Adobe Analytics插件，以便默认提供这些插件：

* getQueryParam()
* getPreviousValue()
* split()

/libs/cq/analytics/clientlibs/sitecatalyst/plugins客户端库文件夹的sitecatalyst.plugins类别中包含这些插件。

>[!NOTE]
>
>为插件创建新的客户端库文件夹。 请勿将插件添加到`/libs/cq/analytics/clientlibs/sitecatalyst/plugins`文件夹。 此做法可确保在AEM重新安装或升级任务期间不会覆盖您对`sitecatalyst.plugins`类别的贡献。

请按照以下过程为插件创建客户端库文件夹。 您只需执行一次此过程。 要将插件添加到客户端库文件夹，请使用后续过程。

1. 在Web浏览器中，打开CRXDE Lite。 ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. 右键单击/apps/my-app/clientlibs文件夹，然后单击创建>创建节点。 输入以下属性值，然后单击确定：

   * 名称：您的客户端库文件夹的名称，如my-plugins

   * 类型：cq:ClientLibraryFolder

1. 选择之前创建的客户端库文件夹，然后使用右下方的属性栏添加以下属性：

   * 名称：类别
   * 类型：字符串
   * 值：sitecatalyst.plugins
   * 多：已选

   在“编辑”窗口中单击“确定”以确认属性值。

1. 右键单击刚刚创建的客户端库文件夹，然后单击创建>创建文件。 对于文件名类型js.txt，然后单击“确定”。

1. 单击“全部保存”。

请按照以下过程获取插件代码，将代码存储在AEM存储库中，并将代码添加到您的客户端库文件夹。

1. 使用您的Adobe Analytics帐户登录到[sc.omniture.com](https://sc.omniture.com)。
1. 在登陆页面上，转到帮助>帮助主页。
1. 在左侧的目录中，单击实施插件。
1. 单击要添加的插件的链接，当页面打开时，找到该插件的Javascript源代码，然后选择代码并复制该代码。

1. 右键单击您的客户端库文件夹，然后单击创建>创建文件。 对于文件名，键入要集成的插件的名称，后跟.js ，然后单击确定。 例如，如果要集成getQueryParam插件，请将文件命名为getQueryParam.js。

   创建文件时，会打开进行编辑。

1. 将插件Javascript代码粘贴到文件中，单击“全部保存”，然后关闭该文件。

1. 从客户端库文件夹中打开js.txt文件。

1. 在新行中，添加包含插件的文件的名称，例如getQueryParam.js。 然后，单击“全部保存”并关闭文件。

>[!NOTE]
>
>使用插件时，请确保也集成任何支持插件，否则插件javascript将无法识别其对支持插件中的函数发起的调用。 例如，getPreviousValue()插件要求split()插件才能正常运行。
>
>还需要将支持插件的名称添加到&#x200B;**js.txt**&#x200B;中。
