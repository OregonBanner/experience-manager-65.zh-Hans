---
title: 将 URL 关联到您的 Web 应用程序
description: 如何在Dynamic Media中将URL关联到您的Web应用程序
uuid: cf599e66-b1f9-40c0-b572-cea19f2e6793
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: d12e6ea3-aaf4-4672-9679-3c16c76d7d5b
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 24%

---


# 将 URL 关联到您的 Web 应用程序 {#linking-urls-to-your-web-application}

您的网站和应用程序通过URL调用访问Dynamic Media服务。 在您发布资产后，Dynamic Media 会激活引用该资产的 URL 字符串。您可以将这些 URL 粘贴到 Web 浏览器中以进行测试。

仅当&#x200B;*不*&#x200B;使用AEM作为WCM时，才链接到URL。 链接与嵌入——用于以弹出窗口或模态窗口的形式传送视频播放器。 如果您使用AEM作为WCM，则[将资产直接添加到页面。](adding-dynamic-media-assets-to-pages.md)

要将这些URL字符串放置到网页和应用程序中，请从Dynamic Media复制它们。

>[!NOTE]
>
>URL 字符串仅适用于资产的动态演绎版。对于存放在 DAM 中（而非 Dynamic Media 服务器中）的静态资产，目前 URL 字符串不适用。对于静态的演绎版，不会显示 URL 按钮。

另请参阅[在网页上嵌入视频查看器或图像查看器。](embed-code.md)

另请参阅[将 YouTube URL 关联到您的 Web 应用程序。](video.md)

另请参阅[为响应式站点传送优化的图像。](responsive-site.md)

另请参阅[上传资产。](manage-assets.md#uploading-assets)

## 获取资产{#obtaining-a-url-for-an-asset}的URL

您可以获取由图像预设或查看器预设生成的 URL 字符串。复制 URL 后，它会进入剪贴板，然后您可以视需要将其粘贴到网站或应用程序的页面中。

>[!NOTE]
>
>只有在将选定的资产发布后，其 URL 才可供复制。此外，您还必须发布查看器预设或图像预设。
>
>请参阅[发布资产](publishing-dynamicmedia-assets.md)。
>
>请参阅[发布查看器预设](managing-viewer-presets.md#publishing-viewer-presets)。
>
>请参阅[发布图像预设](managing-image-presets.md#publishing-image-presets)。

有多种不同的方法可以获取 URL 字符串。但是，下面的步骤只介绍了一种可用的方法。

**获取资产的URL**

1. 导航到要复制其图像预设URL或查看器预设URL的&#x200B;*已发布*&#x200B;资产，然后点按该资产以将其打开。

   请注意，只有在首次&#x200B;*发布*&#x200B;资产&#x200B;*后*，才可复制 URL。此外，还必须发布查看器预设或图像预设。

   请参阅[发布资产](publishing-dynamicmedia-assets.md)。

   请参阅[发布查看器预设](managing-viewer-presets.md#publishing-viewer-presets)。

   请参阅[发布图像预设](managing-image-presets.md#publishing-image-presets)。

1. 根据您选择的资产，执行以下操作之一：

   * 如果您选择了图像，请在下拉菜单中，点按&#x200B;**[!UICONTROL 演绎版。]**

      在&#x200B;**[!UICONTROL Dynamic]**&#x200B;标题下，点按预设名称，将其演绎版视图到右侧框架中。 您可能需要滚动演绎版列表才能看到动态标题。

      在左边栏的底部，点按&#x200B;**[!UICONTROL URL。]**

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * 如果您在下拉菜单中选择了旋转集、图像集、旋转集或视频，请点按&#x200B;**[!UICONTROL 查看器。]**

      在左边栏中，点按查看器预设名称。预览集或视频将在单独的页面中打开。

      在左边栏的底部，点按&#x200B;**[!UICONTROL URL。]**

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. 选择相应的文本并将其复制到 Web 浏览器中，以预览资产或将其添加到您的 Web 内容页面。

   要退出URL窗口，请点按&#x200B;**[!UICONTROL X]**&#x200B;或点按&#x200B;**[!UICONTROL 关闭。]**

## 获取静态资产{#obtaining-a-url-for-a-static-asset}的URL

Dynamic Media支持静态资产的投放，静态资产是除图像和视频之外的其他资产。 支持的静态资产投放格式包括：

* 3D文件
* 动画GIF
* 音频文件
* CSS
* JavaScript(当公司配置了自己的域时)
* PDF
* SVG
* XML
* ZIP

**获取静态资产的URL**

1. 导航到要复制其URL的&#x200B;*已发布*&#x200B;静态资产，然后点按该资产以将其打开。

   请记住，仅在&#x200B;*之后复制*&#x200B;的URL才可用，您首先已发布&#x200B;*静态资产*。

   请参阅[发布资产](publishing-dynamicmedia-assets.md)。

1. 使用以下任意方法获取已发布静态资产的URL:

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         例如，`https://aem.com/is/content/adobe/image.gif`。
   * 点按&#x200B;**[!UICONTROL 资产>动态演绎版]**，然后点按静态资产的动态演绎版并复制URL。

      更改复制的URL，使其在路径中使用`is/content`，而不是`is/image/`。


## 获取已发布视频演绎版{#obtaining-a-video-url-for-a-published-video-rendition}的视频URL

1. 在AEM中，导航到&#x200B;**[!UICONTROL 工具>部署>云>Cloud Services。]**
1. 在&#x200B;**[!UICONTROL Cloud Services]**&#x200B;页上，向下滚动到&#x200B;**[!UICONTROL Dynamic MediaCloud Services]**&#x200B;标题，然后点按&#x200B;**[!UICONTROL 显示配置。]**
1. 在&#x200B;**[!UICONTROL 可用配置]**&#x200B;下，点按所需配置的名称。

1. 在&#x200B;**[!UICONTROL Dynamic Media Cloud设置]**&#x200B;页面的&#x200B;**[!UICONTROL 视频服务URL]**&#x200B;下，向下复制整个URL路径。 您稍后将需要复制的URL路径。

   例如，URL路径可能与以下内容类似：

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (以上路径仅供说明；它不是您复制的实际路径。)

1. 在&#x200B;**[!UICONTROL 注册 ID]** 下，复制 ID 最后一部分中的客户名称。

   例如，如果注册ID为`87654321|MyCompany`，则客户名称将为`MyCompany`。

1. 在页面的左上角附近，点按&#x200B;**[!UICONTROL Cloud Services]**，然后点按Experience Manager标志并导航到&#x200B;**[!UICONTROL 常规>CRXDE Lite。]**
1. 从JCR（Java内容存储库）中向下复制整个视频再现路径。

   例如，视频的再现路径可能与以下内容类似：

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (以上路径仅供说明；它不是您复制的实际路径。)

1. 按照以下顺序排列复制的信息，以形成完整的URL路径：

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   例如，使用上述步骤中的示例路径和示例客户名称，完整路径显示如下：

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   这是已发布视频演绎版的完整视频URL。

## 获取自适应流播放(HLS){#obtaining-a-video-url-for-adaptive-streaming-hls}的视频URL

1. 在AEM中，导航到&#x200B;**[!UICONTROL 工具>部署>云>Cloud Services。]**
1. 在&#x200B;**[!UICONTROL Cloud Services]**&#x200B;页上，向下滚动到&#x200B;**[!UICONTROL Dynamic MediaCloud Services]**&#x200B;标题，然后点按&#x200B;**[!UICONTROL 显示配置。]**
1. 在&#x200B;**[!UICONTROL 可用配置]**&#x200B;下，点按所需配置的名称。
1. 在&#x200B;**[!UICONTROL Dynamic MediaCloud Services设置]**&#x200B;页面上，执行以下操作：

   * 在&#x200B;**[!UICONTROL 视频服务URL]**&#x200B;下，复制整个URL路径。 在这些步骤之后，您将需要复制的URL路径。 例如，URL路径可能与以下内容类似：

   `https://gateway-na.assetsadobe.com/DMGateway/`

   (以上路径仅供说明；它不是您复制的实际路径。)

   * 在&#x200B;**[!UICONTROL 注册 ID]** 下，复制 ID 最后一部分中的客户名称。在稍后这些步骤中，您将需要复制的客户名称。

      例如，如果注册ID为`87654321|demoCo`，则您复制的客户名称将为`demoCo`。


1. 根据您使用的视频投放协议，复制相应的协议选择器。 在这些步骤的后面，您需要复制的协议选择器。

   | 您使用的视频投放协议 | 要使用的协议选择器 |
   |---|---|
   | HTTP <br>如果您使用HTTP(非安全视频投放)，请确保在之前复制的视频服务URL值中将https更改为http。 | `public/` |
   | HTTPS | `public-ssl/` |

1. 在AEM中复制完整的视频资产路径（由Dynamic Media处理）。 在这些步骤的稍后部分，您将需要此复制的视频资产路径。

   例如：

   `/content/dam/marketing/MyVideo.mp4`

1. 按照以下顺序合并之前复制的所有片段以创建字符串：

   &lt;>>&lt;>>&lt;>>&lt;>>`video asset path``video service URL``protocol selector``customer name`

   例如，使用这些步骤中示例中复制的信息，字符串将显示如下：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. 在字符串末尾附加`.m3u8`以完成URL。 例如，将`.m3u8`追加到上一步中的字符串后，完整的URL路径将显示如下：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## 使用HTTP/2传送Dynamic Media资产{#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、经过更新的Web协议，它改进了浏览器和服务器的通信方式。 它提供更快的信息传输，并减少所需的处理能力。 Dynamic Media资产的投放现在可以通过HTTP/2，从而提供更好的响应和加载时间。

有关Dynamic Media帐户HTTP/2快速入门的完整详细信息，请参阅[内容的HTTP2投放](http2.md)。
