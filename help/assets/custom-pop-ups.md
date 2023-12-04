---
title: 使用 Quickview 创建自定义弹出窗口
description: 默认概览用于电子商务体验，其中显示带有产品信息的弹出窗口，以推动购买。 您可以触发要在弹出窗口中显示的自定义内容。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4bcab3f4-500f-432e-b16b-cdc26b9bab4d
feature: Viewers
role: User, Admin
exl-id: 4e7f17ea-6985-4644-b91c-2c1299d01321
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 2%

---

# 使用 Quickview 创建自定义弹出窗口 {#using-quickviews-to-create-custom-pop-ups}

默认概览用于电子商务体验，其中显示带有产品信息的弹出窗口，以推动购买。 但是，您可以触发要在弹出窗口中显示的自定义内容。 根据查看器的不同，此功能允许用户在热点、缩略图图像或图像映射上进行选择，以查看信息或相关内容。

Dynamic Media中的以下查看器支持概览：

* 交互式图像（可点击热点）
* 交互式视频（视频播放期间可单击的缩略图图像）
* 轮播横幅（可点击热点或图像映射）

虽然每个查看器的功能不同，但创建概览的过程在所有三个受支持的查看器中是相同的。

**要使用Quickview创建自定义弹出窗口，请执行以下操作：**

1. 为上传的资源创建快速视图。

   通常，在编辑资产以用于使用的查看器的同时，创建概览也会同时进行。

   <table>
    <tbody>
    <tr>
    <td><strong>您正在使用的查看器</strong></td>
    <td><strong>如果要创建概览，请完成这些步骤</strong></td>
    </tr>
    <tr>
    <td>交互式图像</td>
    <td><a href="/help/assets/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">将热点添加到图像横幅</a>.</td>
    </tr>
    <tr>
    <td>交互式视频</td>
    <td><a href="/help/assets/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">向视频添加交互性</a>.</td>
    </tr>
    <tr>
    <td>传送横幅</td>
    <td><a href="/help/assets/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">将热点或图像映射添加到横幅</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. 获取查看器嵌入代码以在您的网站中集成查看器。

   <table>
    <tbody>
    <tr>
    <td><strong>您正在使用的查看器</strong><br /> </td>
    <td><strong>如果要将查看器与您的网站集成，请完成这些步骤</strong></td>
    </tr>
    <tr>
    <td>交互式图像</td>
    <td><a href="/help/assets/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">将交互式图像与您的网站集成</a>.<br /> </td>
    </tr>
    <tr>
    <td>交互式视频<br /> </td>
    <td><a href="/help/assets/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">将交互式视频与您的网站集成</a>.<br /> </td>
    </tr>
    <tr>
    <td>传送横幅</td>
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">将轮播横幅添加到您的网站页面</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. 您使用的查看器必须知道如何使用概览。

   查看器使用名为的处理程序 `QuickViewActive`.

   **示例**
假设您在网页上对交互式图像使用以下示例嵌入代码：

   ![chlimage_1-291](assets/chlimage_1-291.png)

   使用以下方式将处理程序加载到查看器中 `setHandlers`：

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **以上面的示例嵌入代码为例，提供了以下代码：**

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

   了解有关 `setHandlers()` 方法：

   * 交互式图像查看器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * 交互式视频查看器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. 配置 `quickViewActivate` 处理程序。

   此 `quickViewActivate` 处理程序控制查看器中的概览视图。 该处理程序包含用于概览的变量列表和函数调用。 嵌入代码提供在概览和示例中设置SKU变量的映射 `loadQuickView` 函数调用。

   **变量映射**
将网页中使用的变量映射到概览中包含的SKU值和通用变量：

   `var *variable1*= inData.*quickviewVariable*`

   提供的嵌入代码具有SKU变量的映射示例：

   `var sku=inData.sku`

   也从概览中映射其他变量，如下所示：

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **函数调用**
该处理程序还需要函数调用才能使概览正常工作。 假定主机页面可以访问函数。 嵌入代码提供了一个示例函数调用：

   `loadQuickView(sku)`

   示例函数调用假定使用函数 `loadQuickView()` 存在并且可以访问。

   了解有关 `quickViewActivate` 方法：

   * 交互式图像查看器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * 交互式视频查看器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * 交互式视频查看器中的交互式数据支持： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. 执行以下操作：

   * 取消注释嵌入代码的setHandlers部分。
   * 映射概览中包含的任何其他变量。

      * 更新 `loadQuickView(sku,*var1*,*var2*)` 如果要添加其他变量，请调用。

   * 创建简单的 `loadQuickView` ()功能在页面上，在查看器之外。

     例如，下面会将SKU的值写入浏览器控制台：

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * 将测试HTML页上传到Web服务器并打开。

     在映射概览中的变量并就地调用函数后，浏览器控制台使用提供的示例函数将变量值写入浏览器控制台。

1. 现在，您可以使用函数在概览中调用简单的弹出窗口。 以下示例使用 `DIV` 弹出窗口。
1. 设置弹出窗口的样式 `DIV` 以下列方式进行。 根据需要添加您自己的其他样式。

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. 放置弹出窗口 `DIV` 在HTML页正文中。

   其中一个元素设置了ID，当用户调用概览时，该ID会使用SKU值更新。 该示例还包括一个简单按钮，用于在弹出窗口变为可见后再次隐藏弹出窗口。

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. 添加一个函数，以便您可以在弹出窗口中更新SKU值；通过替换步骤5中创建的简单函数使弹出窗口可见。 ，如下所示：

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. 将测试HTML页上传到Web服务器并打开。 查看器显示弹出窗口 `DIV` 用户调用概览时。
1. **如何以全屏模式显示自定义弹出窗口**

   某些查看器（例如交互式视频查看器）支持全屏模式显示。 但是，如上一步所述使用弹出窗口，会在全屏模式下将其显示在查看器后面。

   要使弹出式菜单同时以标准模式和全屏模式显示，请将弹出式菜单附加到查看器容器。 使用第二个处理程序方法， `initComplete`.

   此 `initComplete` 在初始化查看器后调用处理程序。

   ```xml
   "initComplete":function() { code block }
   ```

   了解有关 `init()` 方法：

   * 交互式图像查看器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * 交互式视频查看器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. 要将前面步骤中描述的弹出窗口附加到查看器，请使用以下代码：

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   在上面的代码中，进行了以下操作：

   * 已识别自定义弹出窗口。
   * 已从DOM中删除它。
   * 已标识查看器容器。
   * 已将弹出窗口附加到查看器容器。

1. 您的整个setHandlers代码类似于以下内容（使用了交互式视频查看器）：

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

1. 加载处理程序后，可初始化查看器：

   `*viewerInstance.*init()`

   **示例**
此示例使用交互式图像查看器。

   `s7interactiveimageviewer.init()`

   将查看器嵌入主机页面后，请确保先创建查看器实例，并加载处理程序，然后再使用调用查看器 `init()`.
