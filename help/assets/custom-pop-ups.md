---
title: 使用概览创建自定义弹出窗口
seo-title: 使用概览创建自定义弹出窗口
description: 默认的Quickview用于电子商务体验中，通过该体验将显示一个包含产品信息的弹出窗口来推动购买。 您可以触发要在弹出窗口中显示的自定义内容。
seo-description: 默认的Quickview用于电子商务体验中，通过该体验将显示一个包含产品信息的弹出窗口来推动购买。 您可以触发要在弹出窗口中显示的自定义内容。
uuid: b906cfff-ac44-4989-b6da-8a9bbf02af03
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4bcab3f4-500f-432e-b16b-cdc26b9bab4d
feature: Viewers
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 3%

---


# 使用概览创建自定义弹出窗口 {#using-quickviews-to-create-custom-pop-ups}

默认的Quickview用于电子商务体验中，通过该体验将显示一个包含产品信息的弹出窗口来推动购买。 但是，您可以触发要在弹出窗口中显示的自定义内容。 根据您使用的查看器，此功能允许用户单击热点、缩略图或图像映射以查看信息或相关内容。

Dynamic Media中的以下查看器支持快速查看：

* 交互式图像（可单击的热点）
* 交互式视频（视频播放期间可单击的缩略图图像）
* 传送横幅（可单击的热点或图像映射）

虽然每个查看器的功能不同，但创建概览的过程在所有三个支持的查看器中是相同的。

**使用快速视图创建自定义弹出窗口**

1. 为已上传的资产创建概览。

   通常，在编辑资产以用于所使用的查看器时，会同时创建概览。

   <table>
    <tbody>
    <tr>
    <td><strong>您正在使用的查看器</strong></td>
    <td><strong>完成这些步骤以创建Quickview</strong></td>
    </tr>
    <tr>
    <td>交互式图像</td>
    <td><a href="/help/assets/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">将热点添加到图像横幅</a>.</td>
    </tr>
    <tr>
    <td>交互式视频</td>
    <td><a href="/help/assets/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">为视频添加交互性</a>.</td>
    </tr>
    <tr>
    <td>传送横幅</td>
    <td><a href="/help/assets/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">向横幅添加热点或图像映射</a>。<br /> </td>
    </tr>
    </tbody>
   </table>

1. 获取查看器嵌入代码，将查看器集成到您的网站中。

   <table>
    <tbody>
    <tr>
    <td><strong>您正在使用的查看器</strong><br /> </td>
    <td><strong>完成这些步骤，将查看器与网站集成</strong></td>
    </tr>
    <tr>
    <td>交互式图像</td>
    <td><a href="/help/assets/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">将交互式图像与您的网站集成</a>。<br /> </td>
    </tr>
    <tr>
    <td>交互式视频<br /> </td>
    <td><a href="/help/assets/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">将交互式视频集成到您的网站</a>。<br /> </td>
    </tr>
    <tr>
    <td>传送横幅</td>
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">将传送横幅添加到您的网站页面</a>。<br /> </td>
    </tr>
    </tbody>
   </table>

1. 您现在使用的查看器需要知道如何使用Quickview。

   为此，查看器使用一个名为`QuickViewActive`的处理函数。

   **示**
例假设您在网页上对交互式图像使用了以下示例嵌入代码：

   ![chlimage_1-291](assets/chlimage_1-291.png)

   处理程序使用`setHandlers`加载到查看器中：

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **使用上面的示例嵌入代码示例，我们有以下代码：**

   ```xml
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   有关`setHandlers()`方法的详细信息，请访问：

   * 交互式图像查看器：[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * 交互式视频查看器：[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. 您现在需要配置`quickViewActivate`处理函数。

   `quickViewActivate`处理程序控制查看器中的Quickview。 该处理函数包含用于Quickview的变量列表和函数调用。 嵌入代码为Quickview中设置的SKU变量以及示例`loadQuickView`函数调用提供映射。

   **变**
量映射在网页中使用的变量映射到概览中包含的SKU值和通用变量：

   `var *variable1*= inData.*quickviewVariable*`

   提供的嵌入代码具有SKU变量的示例映射：

   `var sku=inData.sku`

   也可以从Quickview映射其他变量，如下所示：

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **函**
数调用处理函数还要求对Quickview进行函数调用。假定主机页面可以访问该函数。 嵌入代码提供示例函数调用：

   `loadQuickView(sku)`

   示例函数调用假定函数`loadQuickView()`存在且可访问。

   有关`quickViewActivate`方法的详细信息，请访问：

   * 交互式图像查看器：[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * 交互式视频查看器：[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * 交互式视频查看器中的交互式数据支持：[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. 执行以下操作：

   * 取消嵌入代码的setHandlers部分的注释。
   * 映射Quickview中包含的任何其他变量。

      * 如果要添加其他变量，请更新`loadQuickView(sku,*var1*,*var2*)`调用。
   * 在查看器外部的页面上创建一个简单的`loadQuickView`()函数。

      例如，以下内容会将sku的值写入浏览器控制台：

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * 将测试HTML页上传到Web服务器并打开。

      映射Quickview中的变量并就地调用函数后，浏览器控制台将使用提供的示例函数将变量值写入浏览器控制台。



1. 您现在可以使用函数在概览中调用一个简单的弹出窗口。 以下示例使用`DIV`作为弹出窗口。
1. 按以下方式设置弹出窗口`DIV`的样式。 根据需要添加您自己的其他样式。

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. 将弹出窗口`DIV`放在HTML页面的正文中。

   其中一个元素设置有一个ID，当用户调用概览时，该ID会随sku值更新。 该示例还包括一个简单按钮，用于在弹出窗口可见后再次隐藏它。

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. 在弹出窗口中添加更新sku值的函数；通过替换在步骤5中创建的简单函数使弹出窗口可见。 ，具体如下：

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. 将测试HTML页上传到Web服务器并打开。 当用户调用Quickview时，查看器将显示弹出窗口`DIV`。
1. **如何以全屏模式显示自定义弹出窗口**

   某些查看器（如交互式视频查看器）支持以全屏模式显示。 但是，如前面步骤所述，使用弹出窗口会导致它在全屏模式下显示在查看器后面。

   要在标准和全屏模式下显示弹出窗口，请将弹出窗口附加到查看器容器。 要实现此目的，可以使用第二个处理函数方法`initComplete`。

   查看器初始化后将调用`initComplete`处理器。

   ```xml
   "initComplete":function() { code block }
   ```

   有关`init()`方法的详细信息，请访问：

   * 交互式图像查看器：[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * 交互式视频查看器：[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. 要将上述步骤中介绍的弹出窗口附加到查看器，请使用以下代码：

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   在上面的代码中，我们已执行以下操作：

   * 已识别我们的自定义弹出窗口。
   * 已从DOM中删除它。
   * 已识别查看器容器。
   * 已将弹出窗口附加到查看器容器。

1. 您的整个setHandlers代码现在应类似于以下内容（使用了交互式视频查看器）：

   ```xml
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. 加载处理函数后，您将初始化查看器：

   `*viewerInstance.*init()`

   **示**
例此示例使用交互式图像查看器。

   `s7interactiveimageviewer.init()`

   将查看器嵌入到主机页面后，请确保在使用`init()`调用查看器之前已创建查看器实例并加载了处理函数。

