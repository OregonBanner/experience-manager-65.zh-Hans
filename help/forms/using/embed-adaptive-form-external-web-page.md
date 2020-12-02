---
title: 在外部网页中嵌入自适应表单
seo-title: 在外部网页中嵌入自适应表单
description: 了解如何在外部网页中嵌入自适应表单
seo-description: 了解如何在外部HTML网页中嵌入自适应表单
uuid: d81032dd-af80-4f4b-a717-ee1b89fd3d3d
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
discoiquuid: d739c6da-3b41-4452-8728-d7cd1a3ae20b
docset: aem65
translation-type: tm+mt
source-git-commit: ade3747ba608164a792a62097b82c55626245891
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---


# 在外部网页中嵌入自适应表单{#embed-adaptive-form-in-external-web-page}

您可以[将自适应表单嵌入到AEM Sites页面](/help/forms/using/embed-adaptive-form-aem-sites.md)或AEM外托管的网页中。 嵌入的自适应表单功能齐全，用户无需离开页面即可填写和提交表单。 它帮助用户保持在网页上其他元素的上下文中并同时与表单交互。

## 前提条件 {#prerequisites}

在将自适应表单嵌入到外部网站之前，请执行以下步骤

* 发布要嵌入到AEM Forms服务器发布实例的自适应表单。
* 在您的网站上创建或标识网页以托管自适应表单。 确保网页可以[从CDN](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js)读取jQuery文件，或包含嵌入的jQuery的本地副本。 需要jQuery才能渲染自适应表单。
* 当AEM服务器和网页位于不同的域上时，请执行部分中列出的步骤，[使AEM Forms能够向跨域站点](#cross-site)提供自适应表单。

## 嵌入自适应表单{#embed-adaptive-form}

通过在网页中插入几行JavaScript，可以嵌入自适应表单。 代码中的API向AEM服务器发送HTTP请求以获得自适应表单资源，并在指定的表单容器中插入自适应表单。

要嵌入自适应表单，请执行以下操作：

1. 在您的网站上使用以下代码创建网页：

   ```html
   <!doctype html>
   <html>
     <head>
       <title>This is the title of the webpage!</title>
       <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
     </head>
     <body>
     <div class="customafsection"/>
       <p>This section is replaced with the adaptive form.</p>
   
    <script>
    var options = {path:"/content/forms/af/locbasic.html", dataRef:"", themepath:"", CSS_Selector:".customafsection"};
    alert(options.path);
    var loadAdaptiveForm = function(options){
    //alert(options.path);
       if(options.path) {
           // options.path refers to the publish URL of the adaptive form
           // For Example: https:myserver:4503/content/forms/af/ABC, where ABC is the adaptive form
           // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path
           var path = options.path;
           path += "/jcr:content/guideContainer.html";
           $.ajax({
               url  : path ,
               type : "GET",
               data : {
                   // Set the wcmmode to be disabled
                   wcmmode : "disabled"
                   // Set the data reference, if any
                  // "dataRef": options.dataRef
                   // Specify a different theme for the form object
                 //  "themeOverride" : options.themepath
               },
               async: false,
               success: function (data) {
                   // If jquery is loaded, set the inner html of the container
                   // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not evaluate the script tag in HTML as per the HTML5 spec
                   // For example: document.getElementById().innerHTML
                   if(window.$ && options.CSS_Selector){
                       // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the script tag.
                       $(options.CSS_Selector).html(data);
                   }
               },
               error: function (data) {
                   // any error handler
               }
           });
       } else {
           if (typeof(console) !== "undefined") {
               console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
           }
       }
    }(options);
   
    </script>
     </body>
   </html>
   ```

1. 在嵌入代码中：

   * 使用自适应表单的发布URL路径更改&#x200B;*options.path*&#x200B;变量的值。 如果AEM服务器在上下文路径上运行，请确保URL包含上下文路径。 始终提及自适应表单的完整名称（包括扩展名）。   例如，上述代码和adaptive from驻留在同一AEM forms服务器上，因此该示例使用自适应表单/content/forms/af/locbasic.html的上下文路径。
   * 将&#x200B;*options.dataRef*&#x200B;替换为要随URL传递的属性。 您可以使用dataref变量[预填自适应表单](/help/forms/using/prepopulate-adaptive-form-fields.md)。
   * 将&#x200B;*options.themePath*&#x200B;替换为除自适应表单中配置的主题之外的主题的路径。 或者，也可以使用request属性指定主题路径。
   * CSS_Selector是嵌入自适应表单的表单容器的CSS选择器。 例如，.customafsection css类是上例中的CSS选择器。

自适应表单嵌入到网页中。 在嵌入的自适应表单中观察以下内容：

* 原始自适应表单中的页眉和页脚不包括在嵌入的表单中。
* 草稿和提交的表单可在Forms门户的“草稿和提交”选项卡中找到。
* 在原始自适应表单上配置的提交操作将保留在嵌入式表单中。
* 自适应表单规则在嵌入式表单中保留并具有完全功能。
* 在原始自适应表单中配置的体验定位和A/B测试在嵌入式表单中不起作用。
* 如果Adobe Analytics在原始表单上进行配置，则分析数据会在Adobe Analytics服务器中捕获。 但是，Forms分析报告中不提供该功能。

## 示例拓扑{#sample-topology}

嵌入自适应表单的外部网页会向AEM服务器发送请求，服务器通常位于专用网络中的防火墙后。 为确保请求被安全地定向到AEM服务器，建议设置反向代理服务器。

让我们看一个示例，如何设置不带调度程序的Apache 2.4反向代理服务器。 在此示例中，您将承载具有`/forms`上下文路径的AEM服务器，并映射`/forms`作为反向代理。 它确保Apache服务器上对`/forms`的任何请求都定向到AEM实例。 此拓扑有助于减少调度程序层的规则数，因为所有预装了`/forms`的请求都会路由到AEM服务器。

1. 打开`httpd.conf`配置文件并取消以下代码行的注释。 或者，也可以在文件中添加这些代码行。

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 通过在`httpd-proxy.conf`配置文件中添加以下几行代码来设置代理规则。

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   将规则中的`[AEM_Instance]`替换为AEM服务器发布URL。

如果不在上下文路径上装载AEM服务器，Apache层的代理规则将如下：

```text
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json

ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>如果设置了任何其他拓扑，请确保将提交、预填和其他URL添加允许列表到调度程序层的。

## 最佳实践{#best-practices}

在网页中嵌入自适应表单时，请考虑以下最佳实践：

* 确保网页CSS中定义的样式规则与表单对象CSS不冲突。 为避免冲突，您可以使用AEM客户端库在自适应表单主题中重用网页CSS。 有关在自适应表单主题中使用客户端库的信息，请参见AEM Forms](../../forms/using/themes.md)中的[主题。
* 使网页中的表单容器使用整个窗口宽度。 它确保为移动设备配置的CSS规则能够正常工作，而无需进行任何更改。 如果表单容器不占用整个窗口宽度，您需要编写自定义CSS以使表单适应不同的移动设备。
* 使用`[getData](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API获取客户端表单数据的XML或JSON表示形式。
* 使用`[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API从HTML DOM中卸载自适应表单。
* 从AEM服务器发送响应时设置访问控制来源头。

## 使AEM Forms能够向跨域站点{#cross-site}提供自适应表单

1. 在AEM创作实例上，转到位于`https://'[server]:[port]'/system/console/configMgr`的AEM Web Console Configuration Manager。
1. 找到并打开&#x200B;**Apache Sling推荐人过滤器**&#x200B;配置。
1. 在“允许的主机”字段中，指定网页所在的域。 它使主机能够向AEM服务器发出POST请求。 您还可以使用常规表达式指定一系列外部应用程序域。

