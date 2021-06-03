---
title: 智能成像
description: 智能成像功能可应用每位用户独特的观看特性，自动为其体验优化的正确图像提供服务，从而提高性能和参与度。
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: 资产管理，演绎版
role: Business Practitioner, Administrator
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '1917'
ht-degree: 1%

---


# 智能成像 {#smart-imaging}

## 什么是“智能成像”？{#what-is-smart-imaging}

智能成像技术应用了Adobe Sensei AI功能，并与现有的“图像预设”配合使用，通过基于客户端浏览器功能自动优化图像格式、大小和质量，从而提高图像交付性能。

>[!NOTE]
>
>此功能要求您使用与Adobe Experience Manager Dynamic Media捆绑在一起的现成CDN（内容交付网络）。 此功能不支持任何其他自定义CDN。

Smart Imaging还通过与Adobe一流的高级CDN服务完全集成而带来的额外性能提升而受益。 此服务可在服务器、网络和对等点之间找到最佳的Internet路由。 它会找到延迟最低且丢包率最低的路由，而不是使用Internet上的默认路由。

以下图像资产示例介绍了新增的智能成像优化功能：

| 图像<br>(URL) | 缩略图 | 大小<br>(JPEG) | 大小(WebP)<br>（带智能成像） | 减少百分比 |
|---|---|---|---|---|
| [图像1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [图2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [图像3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![图片3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [图像4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | 平均= 51% |

与上述内容类似，Adobe还使用实时客户网站的7009 URL进行测试。 他们平均可以进一步优化JPEG的38%文件大小。 对于具有WebP格式的PNG，他们平均可进一步优化31%的文件大小。 这种优化是由于智能成像的能力而实现的。

<!-- CQDOC-17915 HIDDEN FOR NOW AS OF MAY 28 2021 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible.

### About device pixel ratio optimization {#dpr}

Device pixel ratio (DPR) &ndash; also known as CSS pixel ratio &ndash; is the relation between a device’s physical pixels and logical pixels. Especially with the advent of retina screens, the pixel resolution of modern mobile devices is growing at a fast rate.

Enabling Device Pixel Ratio optimization renders the image at the native resolution of the screen which makes it look crisp.

Turning on Smart Imaging DPR configuration automatically adjusts the requested image based on pixel density of the display the request is being served from. Currently, the pixel density of the display comes from Akamai CDN header values.

| Permitted values in the URL of an image | Description |
|---|---|
| `dpr=off` | Turn off DPR optimization at an individual image URL level.| 
| `dpr=on,dprValue` | Override the DPR value detected by Smart Imaging, with a custom value (as detected by any client-side logic or other means). Permitted value for `dprValue` is any number greater than 0. Specified values of 1.5, 2, or 3 are typical. |

>[!NOTE]
>
>* You can use `dpr=on,dprValue` even if the company level DPR setting as off.
>* Owing to DPR optimization, when the resultant image is greater than the MaxPix Dynamic Media setting, MaxPix width is always recognized by maintaining the image's aspect ratio.

| Requested Image size | DPR value | Delivered image size |
|---|---|---|
| 816x500 | 1 | 816x500 |
| 816x500 | 2 | 1632x1000 |

See also [When working with images](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) and [When working with Smart Crop](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### About network bandwidth optimization {#network-bandwidth-optimization}

Turning on Network Bandwidth automatically adjusts the image quality that is served based on actual network bandwidth. For poor network bandwidth, DPR optimization is automatically turned off, even if it is already on.

If desired, your company can opt out of network bandwidth optimization at the individual image level by appending `network=off` to the URL of the image.

| Permitted value in the URL of an image | Description |
|---|---|
| `network=off` | Turns off network optimization at an individual image URL level. |

>[!NOTE]
>
>DPR and network bandwidth values are based on the detected client-side values of the bundled CDN. These values are sometimes inaccurate. For example, iPhone5 with DPR=2 and iPhone12 with DPR=3, both show DPR=2. Still, for high-resolution devices, sending DPR=2 is better than sending DPR=1. Coming soon: Adobe is working on client-side code to accurately determine an end user's DPR. -->

## 最新的“智能成像”功能有哪些主要优势？{#what-are-the-key-benefits-of-smart-imaging}

由于图像构成页面加载时间的大部分，因此性能改进对业务可能会产生深远影响，例如更高的转化率、网站逗留时间和较低的网站跳出率。

最新版智能成像中的增强功能：

* 利用最新的智能成像功能改进了网页的Google SEO排名。
* 立即提供优化内容（在运行时）。
* 使用Adobe Sensei技术根据图像请求中指定的质量(qlt)进行转换。
* 可以使用“bfc”URL参数关闭智能成像。
* TTL（生存时间）独立。 以前，智能成像的工作TTL必须至少为12小时。
* 以前，原始图像和派生图像都会缓存，而且使缓存失效需分两步进行。 在最新的智能成像中，只缓存派生项，从而允许单步缓存失效过程。
* 在其规则集中使用自定义标头的客户可以从最新的智能成像中受益，因为这些标头不会被阻止，这与以前版本的智能成像不同。 例如，[向图像响应添加自定义标头值|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)中建议的“Timing Allow Origin”、“X-Robot”。

## 是否存在与智能成像相关的许可成本？{#are-there-any-licensing-costs-associated-with-smart-imaging}

否. Smart Imaging包含在您现有的Dynamic Media Classic或Adobe Experience Manager - Dynamic Media(内部部署、AMS和Adobe Experience Manager as aCloud Service)许可证中。

>[!NOTE]
>
>Dynamic Media — 混合型客户无法使用智能成像。

## 智能成像的工作原理是什么？{#how-does-smart-imaging-work}

当消费者请求图像时，智能成像会检查用户特征，并根据使用中的浏览器转换为适当的图像格式。 执行这些格式转换的方式不会降低视觉保真度。 智能成像可根据浏览器功能以下方式自动将图像转换为不同格式。

<!--   * Safari 14.0 +
    * Safari 14 only with iOS 14.0 and above and macOS BigSur and above -->

* 针对以下浏览器自动转换为WebP:
   * 铬黄
   * Firefox
   * Microsoft® Edge
   * Safari（跨iOS、macOS、iPadOS）提供的浏览器和操作系统版本支持WebP
   * Android™
   * Opera
* 旧版浏览器支持以下功能：

   | 浏览器 | 浏览器/操作系统版本 | 格式 |
   | --- | --- | --- |
   | Safari | 早于iOS/iPad 14.0或macOS BigSur | JPEG2000 |
   | Edge | 早于18 | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* 对于不支持这些格式的浏览器，将提供最初请求的图像格式。

如果原始图像大小小于智能成像生成的图像大小，则会提供原始图像。

## 支持哪些图像格式？{#what-image-formats-are-supported}

智能成像支持以下图像格式：

* JPEG
* PNG

<!-- CQDOC-15846 For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## “智能成像”如何与我的现有已使用的图像预设一起使用？{#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

“智能成像”可与您现有的“图像预设”配合使用，如果请求的文件格式为JPEG或PNG，则“智能成像”会检查除质量(`qlt`)和格式(`fmt`)以外的所有图像设置。 对于格式转换，“智能成像”可根据图像预设设置的定义，保持完整的视觉保真度，但文件大小较小。 如果原始图像大小小于智能成像生成的图像大小，则会提供原始图像。

<!-- CQDOC-15846 In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## 我是否必须更改任何URL、图像预设，或在我的网站上部署任何新代码才能进行智能成像？{#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

如果您在现有的自定义域上配置智能成像，则智能成像可以无缝地与您现有的图像URL和图像预设配合使用。 此外，“智能成像”功能不要求您在网站上添加任何代码来检测用户的浏览器。 它都是自动处理的。

如果必须配置新的自定义域才能使用智能成像，则必须更新URL以反映此自定义域。

要了解智能成像的先决条件，请参阅[我是否有资格使用智能成像？](#am-i-eligible-to-use-smart-imaging)

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## 智能成像是否可以使用HTTPS? HTTP/2呢？{#does-smart-imaging-working-with-https-how-about-http}

智能成像可处理通过HTTP或HTTPS传送的图像。 此外，它还可通过HTTP/2运行。

## 我是否有资格使用智能成像？{#am-i-eligible-to-use-smart-imaging}

要使用智能成像，贵公司的Dynamic Media Classic或Dynamic MediaExperience Manager帐户必须满足以下要求：

* 将Adobe捆绑的CDN（内容交付网络）用作许可证的一部分。
* 使用专用域（例如`images.company.com`或`mycompany.scene7.com`），而不使用通用域（例如`s7d1.scene7.com`、`s7d2.scene7.com`或`s7d13.scene7.com`）。

要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

点按&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**&#x200B;查找标有&#x200B;**[!UICONTROL 已发布服务器名称]**&#x200B;的字段。 如果您当前使用的是通用域，则在提交技术支持票证时，可以请求转移到您自己的自定义域作为此过渡的一部分。

使用Dynamic Media许可证，您的第一个自定义域无需额外付费。

## 为我的帐户启用“智能成像”的过程是什么？{#what-is-the-process-for-enabling-smart-imaging-for-my-account}

启动使用智能成像的请求；它不会自动启用。

<!-- CQDOC-17915 HIDDEN FOR NOW AS OF MAY 28 2021 By default, Smart Imaging DPR and network optimization is disabled (turned off) for a Dynamic Media company account. If you want to enable (turn on) one or both of these out-of-the-box enhancements, create a support case as described below.

The release schedule for Smart Imaging DPR and network optimization is as follows:

| Region | Target date |
|---|---|
| North America | 24 May 2021 | 
| Europe, Middle East, Africa | 25 Jun 2021 | 
| Asia-Pacific | 19 Jul 2021 | -->

1. [使用Admin Console创建支持案例。](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
1. 在支持案例中提供以下信息：

   1. 主要联系人姓名、电子邮件、电话。
   1. 要启用智能成像的所有域（即`images.company.com`或`mycompany.scene7.com`）。

      要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

      单击&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**。

      查找标有&#x200B;**[!UICONTROL Published Server Name]**&#x200B;的字段。
   1. 确认您通过Adobe使用CDN，而不是通过直接关系进行管理。
   1. 验证您使用的是专用域（如`images.company.com`或`mycompany.scene7.com`），而不是通用域（如`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com`）。

      要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

      单击&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**。

      查找标有&#x200B;**[!UICONTROL Published Server Name]**&#x200B;的字段。 如果您当前使用的是通用Dynamic Media Classic域，则可以在此过渡中请求转移到您自己的自定义域。
   1. 指示您是否还需要智能成像才能通过HTTP/2运行。

1. Adobe客户关怀团队会根据请求提交的顺序将您添加到智能成像客户等待列表。
1. 当Adobe准备好处理您的请求时，支持您与您联系以协调并设置目标日期。
1. **可选**:在将新功能推送到生产之前，您可以选择在暂存环境中测试智能成像。
1. 客户关怀团队在完成后会通知您。
1. 为了最大限度地提高智能成像的性能，Adobe建议将生存时间(TTL)设置为24小时或更长。 TTL定义CDN缓存资产的时长。 要更改此设置，请执行以下操作：

   1. 如果您使用Dynamic Media Classic，请单击&#x200B;**[!UICONTROL 设置>应用程序设置>发布设置>图像服务器]**。 将&#x200B;**[!UICONTROL 默认客户端缓存时间设置为Live]**&#x200B;值24或更长。
   1. 如果您使用Dynamic Media，请按照[这些说明](config-dynamic.md)操作。 将&#x200B;**[!UICONTROL Expiration]**&#x200B;值设置为24小时或更长。

## 我何时才能通过智能成像启用我的帐户？{#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

请求会按照客户关怀团队收到请求的顺序，根据等待列表进行处理。

>[!NOTE]
>
>启用“智能成像”会涉及Adobe清除缓存，因此前置时间可能较长。 因此，在任何给定时间都只能处理少数客户过渡。

## 切换到使用智能成像有哪些风险？{#what-are-the-risks-with-switching-over-to-use-smart-imaging}

客户网页不存在风险。 但是，过渡到智能成像会清除CDN中的缓存，因为它涉及在Experience Manager上迁移到Dynamic Media Classic或Dynamic Media的新配置。

在初始过渡期间，非缓存图像会直接点击Adobe的源服务器，直到再次重建缓存为止。 因此，Adobe计划一次处理一些客户过渡，以便在从源中提取请求时保持可接受的性能。 对于大多数客户而言，可在约1到2天内在CDN重新完全构建缓存。

## 如何验证智能成像是否按预期工作？{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 在您的帐户配置了智能成像后，请在浏览器上加载Dynamic Media Classic或Adobe Experience Manager - Dynamic Media图像URL。
1. 在浏览器中单击&#x200B;**[!UICONTROL 查看]** > **[!UICONTROL 开发人员]** > **[!UICONTROL 开发人员工具]**&#x200B;以打开Chrome开发人员窗格。 或者，选择您选择的任何浏览器开发人员工具。

1. 确保在开发人员工具打开时禁用缓存。

   * 在Windows®上，导航到开发人员工具窗格中的设置，然后选中&#x200B;**[!UICONTROL 禁用缓存（在开发工具打开时）]**&#x200B;复选框。
   * 在macOS上，在开发人员窗格的&#x200B;**[!UICONTROL Network]**&#x200B;选项卡下，选择&#x200B;**[!UICONTROL 禁用缓存]**。

1. 观察内容类型已转换为相应的格式。 以下屏幕截图显示了在Chrome上动态转换为WebP的PNG图像。
1. 在不同的浏览器和用户条件上重复此测试。

>[!NOTE]
>
>并非所有图像都会转换。 智能成像功能可决定转换是否可以提高性能。 有时，如果没有预期的性能增益或格式不是JPEG或PNG，则不会转换图像。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## 是否可以针对任何请求关闭智能成像？{#turning-off-smart-imaging}

是. 您可以通过向URL添加修饰符`bfc=off`来关闭智能成像。

<!-- CQDOC-17915 HIDDEN FOR NOW AS OF MAY 28 2021 ## Can I request DPR and network optimization to be turned off at the company level? {#dpr-companylevel-turnoff}

Yes. To disable DPR and network optimization at your company, create a support case as described earlier in this topic. -->

## 提供了哪些“调整”功能？ 是否可以定义任何设置或行为？ (#tuning-settings)

目前，您可以选择启用或禁用“智能成像”。 没有其他调整可用。

## 如果“智能成像”管理质量设置，是否有要设置的最小值和最大值？ 例如，是否可以设置“不低于60”和“不大于80质量”？ (#minimum-maximum)

当前的智能映像中没有这种配置功能。

## 有时，JPEG图像会返回到Chrome，而不是WebP图像。 为什么会发生这种变化？ (#jpeg-webp)

“智能成像”可确定转换是否有益。 仅当转换导致文件大小更小且质量相当时，才会返回新图像。

<!-- CQDOC-17915 HIDDEN FOR NOW AS OF MAY 28 2021 ## How does Smart Imaging DPR optimization work with Adobe Experience Manager Sites components and Dynamic Media viewers?

* Experience Manager Sites Core Components are configured by default for DPR optimization. To avoid oversized images owing to server-side Smart Imaging DPR optimization, `dpr=off` is always added to Experience Manager Sites Core Components Dynamic Media images.
* Given Dynamic Media Foundation Component is configured by default for DPR optimization, to avoid oversized images owing to server-side Smart Imaging DPR optimization, `dpr=off` is always added to Dynamic Media Foundation Component images. Even if customer deselects DPR optimization in DM Foundation Component, server-side Smart Imaging DPR does not kick in. In summary, in the DM Foundation Component, DPR optimization comes into effect based on DM Foundation Component level setting only.
* Any viewer side DPR optimization works in tandem with server-side Smart Imaging DPR optimization, and does not result in over-sized images. In other words, wherever DPR is handled by the viewer, such as the main view only in a zoom-enabled viewer, the server-side Smart Imaging DPR values are not triggered. Likewise, wherever viewer elements, such as swatches and thumbnails, do not have DPR handling, the server-side Smart Imaging DPR value is triggered.

See also [When working with images](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) and [When working with Smart Crop](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop). -->
