---
title: 将 URL 关联到您的 Web 应用程序
description: 如何将URL链接到Dynamic Media中的Web应用程序
uuid: cf599e66-b1f9-40c0-b572-cea19f2e6793
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: d12e6ea3-aaf4-4672-9679-3c16c76d7d5b
role: User, Admin
exl-id: d62275f0-02a4-48c9-bfb1-e23d63b618c9
feature: Configuration
source-git-commit: 78aa7aac838dabc1c4f0329520092e4755541322
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 6%

---

# 将 URL 关联到您的 Web 应用程序 {#linking-urls-to-your-web-application}

您的网站和应用程序通过URL调用访问Dynamic Media服务。 发布资源后，Dynamic Media会激活引用资源的URL字符串。 您可以将这些URL粘贴到Web浏览器中以进行测试。

仅当满足以下条件时，才可以链接到URL： *非* 将Experience Manager用作WCM。 当您希望将视频播放器作为弹出窗口或模式窗口交付时，可使用链接（而不是嵌入）。 如果您使用Experience Manager作为WCM， [直接在页面上添加资产](adding-dynamic-media-assets-to-pages.md).

要将这些URL字符串放置在网页和应用程序中，请从Dynamic Media复制它们。

>[!NOTE]
>
>URL字符串仅适用于资产的动态演绎版。 它们当前不可用于驻留在DAM而不是Dynamic Media服务器中的静态资产。 对于静态的演绎版，不会显示URL按钮。

另请参阅 [在网页上嵌入视频查看器或图像查看器](embed-code.md).

另请参阅 [将YouTube URL链接到您的Web应用程序](video.md).

另请参阅 [为响应式网站投放优化图像](responsive-site.md).

另请参阅 [上传资产](manage-assets.md#uploading-assets).

## 获取资产的URL {#obtaining-a-url-for-an-asset}

您可以获取由图像预设或查看器预设生成的URL字符串。 复制URL后，该URL将登陆剪贴板，以便您可以根据需要将其粘贴到网站或应用程序中的页面。

>[!NOTE]
>
>在发布所选资源之前，无法复制该URL。 此外，还必须发布查看器预设或图像预设。
>
>参见 [发布资产](publishing-dynamicmedia-assets.md).
>
>参见 [发布查看器预设](managing-viewer-presets.md#publishing-viewer-presets).
>
>参见 [发布图像预设](managing-image-presets.md#publishing-image-presets).

您可以通过多种不同的方式获取URL字符串。 但是，以下步骤只向您显示一种您可以使用的方法。

**要获取资产的URL，请执行以下操作：**

1. 导航到 *已发布* 要复制其图像预设URL或查看器预设URL的资产，然后选择要打开的资产。

   请注意，只有在首次&#x200B;*发布*&#x200B;资产&#x200B;*后*，才可复制 URL。此外，还必须发布查看器预设或图像预设。

   参见 [发布资产](publishing-dynamicmedia-assets.md).

   参见 [发布查看器预设](managing-viewer-presets.md#publishing-viewer-presets).

   参见 [发布图像预设](managing-image-presets.md#publishing-image-presets).

1. 根据您选择的资产，执行以下操作之一：

   * 如果您选择了图像，请在下拉菜单中选择 **[!UICONTROL 演绎版]**.

      在 **[!UICONTROL 动态]** 标题，选择预设名称以在右侧框架中查看其演绎版。 如有必要，请滚动“演绎版”列表以查看动态标题。

      在左边栏底部，选择 **[!UICONTROL URL]**.

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * 如果您在下拉菜单中选择了旋转集、图像集、轮播集或视频，请选择 **[!UICONTROL 查看器]**.

      在左边栏中，选择一个查看器预设名称。 该集或视频的预览将在单独的页面中打开。

      在左边栏的底部，选择 **[!UICONTROL URL]**.

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. 选择文本并将其复制到Web浏览器，以便预览资源或将其添加到Web内容页面。

   要退出URL窗口，请选择 **[!UICONTROL X]** 或选择 **[!UICONTROL 关闭]**.

## 获取静态资源的URL {#obtaining-a-url-for-a-static-asset}

Dynamic Media支持静态资源的交付，静态资源是除图像和视频之外的其他资源。 支持的静态资产交付格式包括：

* 三维文件
* 动画GIF
* 音频文件
* CSS
* JavaScript（当您的公司配置了自己的域时）
* PDF
* SVG
* XML
* ZIP

**要获取静态资源的URL，请执行以下操作：**

1. 导航到 *已发布* 要复制其URL的静态资源，然后选择要打开的资源。

   请记住，URL仅可供复制 *之后* 您拥有 *已发布* 静态资源。

   参见 [发布资产](publishing-dynamicmedia-assets.md).

1. 使用以下任意方法获取已发布的静态资源的URL：

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         例如：`https://aem.com/is/content/adobe/image.gif`。
   * 选择 **[!UICONTROL 资产]** > **[!UICONTROL 动态演绎版]**，然后选择静态资源的动态演绎版并复制URL。

      更改复制的URL以使用 `is/content` 路径中而不是 `is/image/`.


## 获取已发布视频演绎版的视频URL {#obtaining-a-video-url-for-a-published-video-rendition}

1. 在Experience Manager中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 云]** > **[!UICONTROL Cloud Services]**.
1. 在 **[!UICONTROL Cloud Services]** 页面，向下滚动到 **[!UICONTROL Dynamic MediaCloud Services]** 标题，然后选择 **[!UICONTROL 显示配置]**.
1. 下 **[!UICONTROL 可用配置]**，选择所需配置的名称。

1. 在 **[!UICONTROL Dynamic Media Cloud设置]** 页面，下 **[!UICONTROL 视频服务URL]**，向下复制整个URL路径。 稍后在步骤中，您需要使用复制的URL路径。

   例如，URL路径可能类似于以下内容：

   `https://s7athens.macromedia.com:9090/DMGateway/`

   （以上路径只是一个示例；它不是您复制的实际路径。）

1. 在&#x200B;**[!UICONTROL 注册 ID]** 下，复制 ID 最后一部分中的客户名称。

   例如，如果注册ID为 `87654321|MyCompany`，则客户名称将为 `MyCompany`.

1. 在页面的左上角附近，选择 **[!UICONTROL Cloud Services]**，然后选择Experience Manager徽标并导航到 **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.
1. 从JCR (Java™内容存储库)中向下复制整个视频演绎版路径。

   例如，视频的演绎版路径可能类似于以下内容：

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   （以上路径只是一个示例；它不是您复制的实际路径。）

1. 按照以下顺序排列复制的信息，以使其形成完整的URL路径：

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   例如，使用上述步骤中的示例路径和示例客户名称，完整路径如下所示：

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   此示例是已发布视频演绎版的完整视频URL。

## 获取用于自适应比特率流的视频URL（DASH或HLS） {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. 在Experience Manager中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 云]** > **[!UICONTROL Cloud Services]**.
1. 在 **[!UICONTROL Cloud Services]** 页面，向下滚动到 **[!UICONTROL Dynamic MediaCloud Services]** 标题，然后选择 **[!UICONTROL 显示配置]**.
1. 下 **[!UICONTROL 可用配置]**，选择所需配置的名称。
1. 在 **[!UICONTROL Dynamic MediaCloud Services设置]** 页面，请执行以下操作：

   * 下 **[!UICONTROL 视频服务URL]**，复制整个URL路径。 在稍后这些步骤中，您需要复制的URL路径。 例如，URL路径可能类似于以下内容：

   `https://gateway-na.assetsadobe.com/DMGateway/`

   （以上路径只是一个示例；它不是您复制的实际路径。）

   * 在&#x200B;**[!UICONTROL 注册 ID]** 下，复制 ID 最后一部分中的客户名称。在稍后这些步骤中，您需要复制的客户名称。

      例如，如果注册ID为 `87654321|demoCo`，则您复制的客户名称为 `demoCo`.


1. 根据您使用的视频交付协议，复制各自的协议选择器。 在稍后的这些步骤中，您需要复制的协议选择器。

   | 您正在使用的视频投放协议 | 要使用的协议选择器 |
   |---|---|
   | HTTP <br> 如果您使用的是HTTP（非安全视频交付），请确保在之前复制的视频服务URL值中将https更改为http。 | `public/` |
   | HTTPS | `public-ssl/` |

1. 复制Experience Manager中的完整视频资源路径，由Dynamic Media处理。 在稍后这些步骤中，您需要此复制的视频资产路径。

   例如：

   `/content/dam/marketing/MyVideo.mp4`

1. 合并您之前复制的所有片段，按以下顺序创建字符串：

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   例如，使用这些步骤中示例复制的信息，字符串将如下所示：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. 通过附加来完成URL `.m3u8` 到字符串的结尾。 例如，附加 `.m3u8` 对于上一步中的字符串，完整的URL路径如下所示：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## 使用HTTP/2交付您的Dynamic Media资源 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、更新的Web协议，它改进了浏览器和服务器的通信方式。 它提供了更快的信息传输并减少了所需的处理能力。 Dynamic Media资源的交付现在可以通过HTTP/2进行，从而提供更好的响应和加载时间。

参见 [HTTP2内容交付](http2.md) ，以了解有关开始将HTTP/2用于Dynamic Media帐户的完整详细信息。
