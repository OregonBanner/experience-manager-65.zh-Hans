---
title: 智能成像
description: “智能成像”功能可应用每位用户的独特查看特性，自动为其体验优化的正确图像提供服务，从而提高性能和参与度。
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: 资产管理，演绎版
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
source-git-commit: 4b8369de9e6a10b73115d53358ce98729d92ed44
workflow-type: tm+mt
source-wordcount: '2633'
ht-degree: 1%

---


# 智能成像 {#smart-imaging}

## 什么是“智能成像”？ {#what-is-smart-imaging}

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

在移动网络上，挑战因以下两个因素而加剧：

* 多种不同外形规格和高分辨率显示器的设备。
* 网络带宽受限。

在图像方面，目标是尽可能高效地提供最优质的图像。

### 关于设备像素比例优化 {#dpr}

设备像素比率(DPR)（也称为CSS像素比率）是设备的物理像素与逻辑像素之间的关系。 特别是随着视网膜屏幕的出现，现代移动设备的像素分辨率正以快速的速度增长。

启用“设备像素比率”优化后，图像将以屏幕的本机分辨率呈现，从而使其看起来清晰。

打开智能成像DPR配置可根据请求所提供的显示器的像素密度自动调整请求的图像。 目前，显示屏的像素密度来自Akamai CDN标头值。

| 图像URL中允许的值 | 描述 |
|---|---|
| `dpr=off` | 在单个图像URL级别关闭DPR优化。 |
| `dpr=on,dprValue` | 使用自定义值覆盖由智能成像检测的DPR值（由任何客户端逻辑或其他方式检测）。 `dprValue`的允许值是大于0的任意数字。 指定的值1.5、2或3是典型值。 |

>[!NOTE]
>
>* 即使关闭公司级别DPR设置，您也可以使用`dpr=on,dprValue`。
>* 由于DPR优化，当生成的图像大于MaxPix Dynamic Media设置时，始终通过保持图像的宽高比来识别MaxPix宽度。


| 请求的图像大小 | DPR值 | 传送的图像大小 |
|---|---|---|
| 816x500 | 1 | 816x500 |
| 816x500 | 2 | 1632x1000 |

另请参阅[使用图像](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images)和[使用智能裁剪](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop)时。

### 关于网络带宽优化 {#network-bandwidth-optimization}

打开网络带宽可根据实际网络带宽自动调整提供的图像质量。 对于较差的网络带宽，即使DPR优化已打开，DPR优化也会自动关闭。

如有需要，贵公司可以通过在图像的URL后附加`network=off` ，在单个图像级别选择退出网络带宽优化。

| 图像URL中允许的值 | 描述 |
|---|---|
| `network=off` | 在单个图像URL级别关闭网络优化。 |

>[!NOTE]
>
>DPR和网络带宽值基于检测到的捆绑CDN的客户端值。 这些值有时不准确。 例如，DPR=2的iPhone5和DPR=3的iPhone12，都显示DPR=2。 但是，对于高分辨率设备，发送DPR=2比发送DPR=1要好。 即将推出：Adobe正在使用客户端代码来准确确定最终用户的DPR。

## 最新的“智能成像”功能有哪些主要优势？ {#what-are-the-key-benefits-of-smart-imaging}

由于图像构成页面加载时间的大部分，因此性能改进对业务可能会产生深远影响，例如更高的转化率、网站逗留时间和较低的网站跳出率。

最新版智能成像中的增强功能：

* 针对使用最新智能成像的网页，改进了Google SEO排名。
* 立即提供优化内容（在运行时）。
* 使用Adobe Sensei技术根据图像请求中指定的质量(qlt)进行转换。
* 可以使用“bfc”URL参数关闭智能成像。
* TTL（生存时间）独立。 以前，智能成像的工作TTL必须至少为12小时。
* 以前，原始图像和派生图像都会缓存，而且使缓存失效需分两步进行。 在最新的智能成像中，只缓存派生项，从而允许单步缓存失效过程。
* 在其规则集中使用自定义标头的客户可以从最新的智能成像中受益，因为这些标头不会被阻止，这与以前版本的智能成像不同。 例如，[向图像响应添加自定义标头值|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)中建议的“Timing Allow Origin”、“X-Robot”。

## 是否存在与智能成像相关的许可成本？ {#are-there-any-licensing-costs-associated-with-smart-imaging}

否. Smart Imaging包含在您现有的Dynamic Media Classic或Adobe Experience Manager - Dynamic Media(内部部署、AMS和Adobe Experience Manager as aCloud Service)许可证中。

>[!NOTE]
>
>Dynamic Media — 混合型客户无法使用智能成像。

## 智能成像的工作原理是什么？ {#how-does-smart-imaging-work}

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

## 支持哪些图像格式？ {#what-image-formats-are-supported}

智能成像支持以下图像格式：

* JPEG
* PNG

<!-- CQDOC-15846 For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## “智能成像”如何与我的现有已使用的图像预设一起使用？ {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

“智能成像”可与您现有的“图像预设”配合使用，如果请求的文件格式为JPEG或PNG，则“智能成像”会检查除质量(`qlt`)和格式(`fmt`)以外的所有图像设置。 对于格式转换，“智能成像”可根据图像预设设置的定义，保持完整的视觉保真度，但文件大小较小。 如果原始图像大小小于智能成像生成的图像大小，则会提供原始图像。

<!-- CQDOC-15846 In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## 我是否必须更改任何URL、图像预设，或在我的网站上部署任何新代码才能进行智能成像？ {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

如果您在现有的自定义域上配置智能成像，则智能成像可以无缝地与您现有的图像URL和图像预设配合使用。 此外，“智能成像”功能不要求您在网站上添加任何代码来检测用户的浏览器。 它都是自动处理的。

如果必须配置新的自定义域才能使用智能成像，则必须更新URL以反映此自定义域。

要了解智能成像的先决条件，请参阅[我是否有资格使用智能成像？](#am-i-eligible-to-use-smart-imaging)

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## 智能成像是否可以使用HTTPS? HTTP/2呢？ {#does-smart-imaging-working-with-https-how-about-http}

智能成像可处理通过HTTP或HTTPS传送的图像。 此外，它还可通过HTTP/2运行。

## 我是否有资格使用智能成像？ {#am-i-eligible-to-use-smart-imaging}

要使用智能成像，贵公司的Dynamic Media Classic或Dynamic MediaExperience Manager帐户必须满足以下要求：

* 将Adobe捆绑的CDN（内容交付网络）用作许可证的一部分。
* 使用专用域（例如`images.company.com`或`mycompany.scene7.com`），而不使用通用域（例如`s7d1.scene7.com`、`s7d2.scene7.com`或`s7d13.scene7.com`）。

要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

导航至&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**&#x200B;查找标有&#x200B;**[!UICONTROL 已发布服务器名称]**&#x200B;的字段。 如果您当前使用的是通用域，则在提交技术支持票证时，可以请求转移到您自己的自定义域作为此过渡的一部分。

使用Dynamic Media许可证，您的第一个自定义域无需额外付费。

## 为我的帐户启用“智能成像”的过程是什么？ {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

启动使用智能成像的请求；它不会自动启用。

默认情况下，对于Dynamic Media公司帐户，会禁用（关闭）智能成像DPR和网络优化。 如果要启用（打开）其中一个或两个现成增强功能，请按如下所述创建一个支持案例。

智能成像DPR和网络优化的发布计划如下：

| 区域 | 目标日期 |
|---|---|
| 北美 | 实时 |
| 欧洲、中东、非洲 | 2021年8月13日 |
| 亚太 | 2021年7月22日 |

1. [使用Admin Console创建支持案例](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)。
1. 在支持案例中提供以下信息：

   1. 主要联系人姓名、电子邮件、电话。
   1. 要启用智能成像的所有域（即`images.company.com`或`mycompany.scene7.com`）。

      要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

      导航到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**。

      查找标有&#x200B;**[!UICONTROL Published Server Name]**&#x200B;的字段。
   1. 确认您通过Adobe使用CDN，而不是通过直接关系进行管理。
   1. 验证您使用的是专用域（如`images.company.com`或`mycompany.scene7.com`），而不是通用域（如`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com`）。

      要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

      导航到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**。

      查找标有&#x200B;**[!UICONTROL Published Server Name]**&#x200B;的字段。 如果您当前使用的是通用Dynamic Media Classic域，则可以在此过渡中请求转移到您自己的自定义域。
   1. 指示您是否还需要智能成像才能通过HTTP/2运行。

1. Adobe客户关怀团队会根据请求提交的顺序将您添加到智能成像客户等待列表。
1. 当Adobe准备好处理您的请求时，支持您与您联系以协调并设置目标日期。
1. **可选**  — 在Adobe将新功能推送到生产之前，您可以选择在暂存环境中测试智能成像。
1. 客户关怀团队在完成后会通知您。
1. 为了最大限度地提高智能成像的性能，Adobe建议将生存时间(TTL)设置为24小时或更长。 TTL定义CDN缓存资产的时长。 要更改此设置，请执行以下操作：

   1. 如果您使用Dynamic Media Classic，请导航到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 发布设置]** > **[!UICONTROL 图像服务器]**。 将&#x200B;**[!UICONTROL 默认客户端缓存时间设置为Live]**&#x200B;值24或更长。
   1. 如果您使用Dynamic Media，请按照[这些说明](config-dynamic.md)操作。 将&#x200B;**[!UICONTROL Expiration]**&#x200B;值设置为24小时或更长。

## 我何时才能通过智能成像启用我的帐户？ {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

请求会按照客户关怀团队收到请求的顺序，根据等待列表进行处理。

>[!NOTE]
>
>启用“智能成像”会涉及Adobe清除缓存，因此前置时间可能较长。 因此，在任何给定时间都只能处理少数客户过渡。

## 切换到使用智能成像有哪些风险？ {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

客户网页不存在风险。 但是，过渡到智能成像会清除CDN中的缓存，因为它涉及在Experience Manager上迁移到Dynamic Media Classic或Dynamic Media的新配置。

在初始过渡期间，非缓存图像会直接点击Adobe的源服务器，直到再次重建缓存为止。 因此，Adobe计划一次处理一些客户过渡，以便在从源中提取请求时保持可接受的性能。 对于大多数客户而言，可在约1到2天内在CDN重新完全构建缓存。

## 如何验证智能成像是否按预期工作？{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 在您的帐户配置了智能成像后，请在浏览器上加载Dynamic Media Classic或Adobe Experience Manager - Dynamic Media图像URL。
1. 在浏览器中，通过导航到&#x200B;**[!UICONTROL View]** > **[!UICONTROL Developer]** > **[!UICONTROL Developer Tools]**&#x200B;打开Chrome开发人员窗格。 或者，选择您选择的任何浏览器开发人员工具。

1. 确保在开发人员工具打开时禁用缓存。

   * 在Windows®上，导航到开发人员工具窗格中的设置，然后选中&#x200B;**[!UICONTROL 禁用缓存（在开发工具打开时）]**&#x200B;复选框。
   * 在macOS上，在开发人员窗格的&#x200B;**[!UICONTROL Network]**&#x200B;选项卡下，选择&#x200B;**[!UICONTROL 禁用缓存]**。

1. 观察内容类型已转换为相应的格式。 以下屏幕截图显示了在Chrome上动态转换为WebP的PNG图像。
1. 在不同的浏览器和用户条件上重复此测试。

>[!NOTE]
>
>并非所有图像都会转换。 智能成像功能可决定转换是否可以提高性能。 有时，如果没有预期的性能增益或格式不是JPEG或PNG，则不会转换图像。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## 是否可以针对任何请求关闭智能成像？ {#turning-off-smart-imaging}

是. 您可以通过向URL添加修饰符`bfc=off`来关闭智能成像。

## 我是否可以请求在公司级别关闭DPR和网络优化？ {#dpr-companylevel-turnoff}

是. 要在贵公司禁用DPR和网络优化，请创建一个支持案例，如本主题前面所述。

## 提供了哪些“调整”功能？ 是否可以定义任何设置或行为？ (#tuning-settings)

目前，您可以选择启用或禁用“智能成像”。 没有其他调整可用。

## 如果“智能成像”管理质量设置，是否有要设置的最小值和最大值？ 例如，是否可以设置“不低于60”和“不大于80质量”？ (#minimum-maximum)

当前的智能映像中没有这种配置功能。

## 有时，JPEG图像会返回到Chrome，而不是WebP图像。 为什么会发生这种变化？ (#jpeg-webp)

“智能成像”可确定转换是否有益。 仅当转换导致文件大小更小且质量相当时，才会返回新图像。

## 智能成像DPR优化如何与Adobe Experience Manager Sites组件和Dynamic Media查看器一起使用？

* Experience Manager站点核心组件默认配置以进行DPR优化。 为避免因服务器端智能成像DPR优化而出现超大图像，应始终将`dpr=off`添加到Experience Manager站点核心组件Dynamic Media图像中。
* 默认情况下，为了优化DPR，配置了Dynamic Media Foundation组件，以避免因服务器端智能成像DPR优化而出现过大的图像，将始终向Dynamic Media Foundation组件图像中添加`dpr=off`。 即使客户在DM Foundation组件中取消选择DPR优化，服务器端智能成像DPR也不会生效。 总之，在DM Foundation组件中，DPR优化仅基于DM Foundation组件级别设置生效。
* 任何查看器端DPR优化都与服务器端智能成像DPR优化协同工作，并且不会导致图像过大。 换言之，无论DPR由查看器处理（例如仅在启用了缩放功能的查看器中的主视图），都不会触发服务器端智能成像DPR值。 同样，无论查看器元素（如色板和缩略图）没有DPR处理，都会触发服务器端智能成像DPR值。

另请参阅[使用图像](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images)和[使用智能裁剪](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop)时。
