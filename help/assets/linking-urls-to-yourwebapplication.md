---
title: 将 URL 关联到您的 Web 应用程序
description: 如何在Dynamic media中将URL关联到Web应用程序
uuid: cf599e66-b1f9-40c0-b572-cea19f2e6793
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: d12e6ea3-aaf4-4672-9679-3c16c76d7d5b
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 将 URL 关联到您的 Web 应用程序 {#linking-urls-to-your-web-application}

您的网站和应用程序通过URL调用访问Dynamic Media服务。 在您发布资产后，Dynamic Media 会激活引用该资产的 URL 字符串。您可以将这些 URL 粘贴到 Web 浏览器中以进行测试。

仅当您未将AEM用作WCM *时* ，才链接到URL。 链接与嵌入——用于将视频播放器作为弹出窗口或模态窗口传送。 如果您使用AEM作为WCM, [则直接在页面上添加资产。](adding-dynamic-media-assets-to-pages.md)

要将这些URL字符串放置到网页和应用程序中，请从Dynamic media复制这些字符串。

>[!NOTE]
>
>URL 字符串仅适用于资产的动态演绎版。对于存放在 DAM 中（而非 Dynamic Media 服务器中）的静态资产，目前 URL 字符串不适用。对于静态的演绎版，不会显示 URL 按钮。

See also [Embedding the Video or Image Viewer on a Web Page.](embed-code.md)

另请参阅[将 YouTube URL 关联到您的 Web 应用程序。](video.md)

See also [Delivering Optimized Images for a Responsive Site.](responsive-site.md)

See also [Uploading Assets.](managing-assets-touch-ui.md#uploading-assets)

## Obtaining a URL for an asset {#obtaining-a-url-for-an-asset}

您可以获取由图像预设或查看器预设生成的 URL 字符串。复制 URL 后，它会进入剪贴板，然后您可以视需要将其粘贴到网站或应用程序的页面中。

>[!NOTE]
>
>只有在将选定的资产发布后，其 URL 才可供复制。此外，您还必须发布查看器预设或图像预设。
>
>请参阅[发布资产](publishing-dynamicmedia-assets.md)。
>
>See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).
>
>See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

有多种不同的方法可以获取 URL 字符串。但是，下面的步骤只介绍了一种可用的方法。

**获取资产的URL**

1. Navigate to the *published* asset whose image preset URL or viewer preset URL you want to copy, and tap the asset to open it.

   请记住，只有在先&#x200B;*发布*&#x200B;资产&#x200B;*之后*，才可复制其 URL。此外，还必须发布查看器预设或图像预设。

   请参阅[发布资产](publishing-dynamicmedia-assets.md)。

   See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).

   See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

1. 根据您选择的资产，执行以下操作之一：

   * 如果您选择了图像，请在下拉菜单中点按演 **[!UICONTROL 绎版]**。

      Under the **[!UICONTROL Dynamic]** heading, tap a preset name to view its rendition in the right frame. 您可能需要滚动演绎版列表才能看到动态标题。

      在左边栏的底部，点按 **[!UICONTROL URL]**。

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * 如果您在下拉菜单中选择了旋转集、图像集、旋转集或视频，请点按查看 **[!UICONTROL 器]**。

      在左边栏中，点按查看器预设名称。集合或视频的预览将在单独的页面中打开。

      In the left rail, at the bottom, tap **[!UICONTROL URL]**.

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. 选择相应的文本并将其复制到 Web 浏览器中，以预览资产或将其添加到您的 Web 内容页面。

   要退出URL窗口，请点按 **[!UICONTROL X]** 或点按 **[!UICONTROL 关闭]**。

## 获取静态资产的URL {#obtaining-a-url-for-a-static-asset}

Dynamic media支持静态资产的交付，静态资产是除图像和视频之外的其他资产。 支持的静态资产格式用于交付包括：

* 动画GIF
* 音频文件
* CSS
* JavaScript（当您的公司配置了自己的域时）
* PDF
* SVG
* XML
* ZIP

**获取静态资产的URL**

1. 导航到要复制其URL的*已发布*静态资产，然后点按资产以将其打开。

   Remember that URLs are only available to copy *after* you have first *published* the static asset.

   请参阅[发布资产](publishing-dynamicmedia-assets.md)。

1. 使用以下任意方法获取已发布静态资产的URL:

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         For example, `https://aem.com/is/content/adobe/image.gif`.
   * 单击 **[!UICONTROL 资产>动态演绎版]**，然后点按静态资产的动态演绎版并复制URL。

      更改复制的URL以在路 `is/content` 径中使用，而不是 `is/image/`。


## 获取已发布视频演绎版的视频URL {#obtaining-a-video-url-for-a-published-video-rendition}

1. 在AEM中，导航到工 **[!UICONTROL 具>部署>云>云服务]**。
1. 在“云 **[!UICONTROL 服务]** ”页面上，向下滚动到“ **[!UICONTROL Dynamic Media Cloud Services”标题]** ，然后点按显示 **[!UICONTROL 配置]**。
1. 在“ **[!UICONTROL 可用配置]**”下，点按所需配置的名称。

1. 在“ **[!UICONTROL Dynamic Media Cloud Settings]** ”页面的“ **[!UICONTROL 视频服务URL”下]**，复制整个URL路径。 您稍后将需要复制的URL路径。

   例如，URL路径可能与以下内容类似：

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (上述路径仅供说明；它不是您复制的实际路径。)

1. 在“ **[!UICONTROL 注册ID]**”下，复制ID最后一部分中找到的客户名称。

   例如，如果注册ID为 `87654321|MyCompany`，则客户名称为 `MyCompany`。

1. 在页面的左上角附近，点按 **[!UICONTROL Cloud Services**，然后点按Experience manager徽标并导航到“常规” **[!UICONTROL >“CRXDE Lite]**”。
1. 从JCR（Java内容存储库）中向下复制整个视频再现路径。

   例如，视频的再现路径可能与以下内容类似：

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (上述路径仅供说明；它不是您复制的实际路径。)

1. 按照以下顺序排列复制的信息，以形成完整的URL路径：

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   例如，使用上述步骤中的示例路径和示例客户名称，完整路径显示如下：

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   这是已发布视频再现的完整视频URL。

## 获取自适应流播放(HLS)的视频URL {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. 在AEM中，导航到工 **[!UICONTROL 具>部署>云>云服务]**。
1. 在“云 **[!UICONTROL 服务]** ”页面上，向下滚动到“ **[!UICONTROL Dynamic Media Cloud Services”标题]** ，然后点按显示 **[!UICONTROL 配置]**。
1. 在“ **[!UICONTROL 可用配置]**”下，点按所需配置的名称。
1. 在“ **[!UICONTROL Dynamic Media Cloud服务设置]** ”页上，执行以下操作：

   * 在“ **[!UICONTROL 视频服务URL]**”下，复制整个URL路径。 在这些步骤的后面，您将需要复制的URL路径。 例如，URL路径可能与以下内容类似：
   `https://gateway-na.assetsadobe.com/DMGateway/`

   (上述路径仅供说明；它不是您复制的实际路径。)

   * 在“ **[!UICONTROL 注册ID]**”下，复制ID最后一部分中找到的客户名称。 在这些步骤的稍后部分，您将需要复制的客户名称。

      例如，如果注册ID是 `87654321|demoCo`，则您复制的客户名称将为 `demoCo`。


1. 根据您使用的视频交付协议，复制相应的协议选择器。 在以下步骤中，您稍后将需要复制的协议选择器。

   | 您使用的视频交付协议 | 要使用的协议选择器 |
   |---|---|
   | HTTP如 <br> 果您使用HTTP（非安全视频交付），请确保在您之前复制的视频服务URL值中将https更改为http。 | `public/` |
   | HTTPS | `public-ssl/` |

1. 在AEM中复制由Dynamic media处理的完整视频资产路径。 在这些步骤的稍后部分，您将需要此复制的视频资产路径。

   例如：

   `/content/dam/marketing/MyVideo.mp4`

1. 按照以下顺序合并之前复制的所有部分以创建字符串：

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   例如，使用这些步骤中示例中复制的信息，字符串将显示如下：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. 在字符串末尾附 `.m3u8` 加以完成URL。 例如，在上一 `.m3u8` 步的字符串后面附加完整的URL路径将显示如下：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## 使用HTTP/2交付Dynamic Media资产 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、更新的Web协议，它改进了浏览器和服务器通信的方式。 它提供了更快的信息传输，并减少了所需的处理能力。 Dynamic media资产的交付现在可以通过HTTP/2进行，从而提供更好的响应和加载时间。

有关 [Dynamic Media帐户的HTTP/2快速入门的完整详细信息，请参阅](http2.md) HTTP2内容交付。
