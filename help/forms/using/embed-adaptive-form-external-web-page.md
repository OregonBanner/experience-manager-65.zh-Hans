---
title: 将自适应表单嵌入到外部网页中
description: 了解如何在外部网页中嵌入自适应表单
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms
exl-id: 2a237f74-fdfc-4e28-841c-f69afb7b99cf
source-git-commit: 65c5a4442f17e6bc52deaa1588f535a05698083f
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 55%

---

# 将自适应表单嵌入到外部网页中{#embed-adaptive-form-in-external-web-page}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>

您可以[在 AEM Sites 页面中嵌入自适应表单](/help/forms/using/embed-adaptive-form-aem-sites.md)，也可以在 AEM 外部托管的网页中嵌入自适应表单。嵌入的自适应表单功能齐全，用户无需离开页面即可填写并提交表单。它可帮助用户停留在网页上其他元素的上下文中，同时与表单进行交互。

## 前提条件 {#prerequisites}

在将自适应表单嵌入到外部网站之前，请执行以下步骤：

* 发布要嵌入到AEM Forms服务器的发布实例的自适应表单。
* 在您的网站上创建或识别可托管自适应表单的网页。 确保网页可以 [从CDN读取jQuery文件](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) 或嵌入了jQuery的本地副本。 渲染自适应表单需要 jQuery。
* 当AEM服务器和网页位于不同的域时，请执行一节中列出的步骤， [启用AEM Forms以向跨域站点提供自适应表单](#cross-site).

## 嵌入的自适应表单 {#embed-adaptive-form}

您可以通过在网页中插入几行 JavaScript 来嵌入自适应表单。代码中的 API 向 AEM 服务器发送 HTTP 请求以获取自适应表单资源，并将自适应表单注入指定的表单容器中。

要嵌入自适应表单，请执行以下操作：

1. 使用以下代码在网站上创建一个网页：

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
           // options.path refers to the path of the adaptive form
           // For Example: /content/forms/af/ABC, where ABC is the adaptive form
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

1. 在嵌入的代码中：

   * 更改 *选项路径* 变量填充自适应表单的发布URL的路径。 如果 AEM 服务器在某个上下文路径上运行，请确保 URL 包含该上下文路径。始终提及自适应表单的完整名称，包括扩展名。例如，上述代码和自适应来自位于同一AEM Forms服务器上，因此该示例使用的是自适应表单的上下文路径 `/content/forms/af/locbasic.html`.
   * 替换 *options.dataRef* 要与URL一起传递的属性。 您可以使用dataref变量执行以下操作 [预填自适应表单](/help/forms/using/prepopulate-adaptive-form-fields.md).
   * 替换 *options.themePath* 使用非自适应表单中配置的主题的路径。 或者，您可以使用请求属性指定主题路径。
   * CSS_Selector 是将自适应表单嵌入到的表单容器的 CSS 选择器。例如，.customafsection css 类是上面示例中的 CSS 选择器。

自适应表单嵌入到网页中。在嵌入的自适应表单中观察以下内容：

* 原始自适应表单中的页眉和页脚未包含在嵌入表单中。
* 可在 Forms Portal 的草稿和提交选项卡中找到草稿和提交的表单。
* 在原始自适应表单上配置的提交操作将保留在嵌入表单中。
* 自适应表单规则在嵌入表单中保留并完全可用。
* 在原始自适应表单中配置的体验定位和A/B测试在嵌入表单中不起作用。
* 如果在原始表单上配置了Adobe Analytics，则Adobe Analytics服务器将捕获分析数据。 不过，它在表单分析报告中不可用。

## 示例拓扑 {#sample-topology}

嵌入自适应表单的外部网页将请求发送到 AEM 服务器，该服务器通常位于专用网络中的防火墙后面。为了确保将请求安全地定向到 AEM 服务器，建议设置反向代理服务器。

让我们看一个示例，了解如何在不使用Dispatcher的情况下设置Apache 2.4反向代理服务器。 在此示例中，您托管AEM服务器 `/forms` 上下文路径和映射 `/forms` 用于反向代理。 它确保任何请求 `/forms` Apache Server上的代码被定向到AEM实例。 此拓扑有助于减少Dispatcher层的规则数量，因为所有请求都以为前缀 `/forms` 路由到AEM服务器。

1. 打开 `httpd.conf` 配置文件，并取消注释以下代码行。或者，您可以在文件中添加这些代码行。

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 通过在 `httpd-proxy.conf` 配置文件中添加以下代码行来设置代理规则。

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   将 `[AEM_Instance]` 替换为规则中的 AEM 服务器发布 URL。

如果您没有在上下文路径上装载AEM服务器，则Apache层的代理规则如下所示：

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
>列入允许列表如果设置了任何其他拓扑，请确保将提交、预填充和其他URL添加到Dispatcher层的。

## 最佳实践 {#best-practices}

在网页中嵌入自适应表单时，请考虑以下最佳实践：

* 确保网页 CSS 中定义的样式规则不会与表单对象 CSS 发生冲突。要避免冲突，您可以使用AEM客户端库在自适应表单主题中重用网页CSS。 有关在自适应表单主题中使用客户端库的信息，请参阅 [AEM Forms中的主题](../../forms/using/themes.md).
* 使网页中的表单容器占用整个窗口宽度。这将确保为移动设备配置的 CSS 规则能够正常工作，而无需做出任何更改。如果表单容器未采用整个窗口宽度，则必须编写自定义CSS以使表单适应不同的移动设备。
* 使用 `[getData](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API 获取客户端中表单数据的 XML 或 JSON 表示形式。
* 使用 `[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API 从 HTML DOM 卸载自适应表单。
* 设置从AEM服务器发送响应时的访问控制源标头。

## 启用AEM Forms以向跨域站点提供自适应表单 {#cross-site}

1. 在 AEM 发布实例上，转到 AEM Web 控制台配置管理器，网址为 `https://'[server]:[port]'/system/console/configMgr`。
1. 找到并打开 **Apache Sling 反向链接筛选条件**&#x200B;配置。
1. 在“允许的主机”字段中，指定网页所在的域。这将允许主机向 AEM 服务器发出 POST 请求。您也可以使用正则表达式来指定一系列外部应用程序域。
