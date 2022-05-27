---
title: 智能成像
description: “智能成像”功能可应用每位用户的独特查看特性，自动为其体验优化的正确图像提供服务，从而提高性能和参与度。
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: Asset Management,Renditions
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
source-git-commit: bb42b5990993b0f8cea95cf1f6c033aed2713c1c
workflow-type: tm+mt
source-wordcount: '3519'
ht-degree: 1%

---

# 智能成像 {#smart-imaging}

## 什么是“智能成像”？ {#what-is-smart-imaging}

智能成像技术应用了Adobe Sensei AI功能，并可与现有的“图像预设”配合使用。 它致力于根据客户端浏览器功能自动优化图像格式、大小和质量，从而提高图像交付性能。

现在，借助AVIF和WebP支持中附带的改进的智能成像功能，为LCP（最大内容绘画）获得更好的Google核心Web重要评分。

>[!IMPORTANT]
>
>智能成像要求您使用与Adobe Experience Manager - Dynamic Media捆绑在一起的现成CDN（内容交付网络）。 此功能不支持任何其他自定义CDN。

与Adobe一流的优质CDN（内容交付网络）服务完全集成后，智能成像可以从性能提升中受益。 此服务可在服务器、网络和对等点之间找到最佳的Internet路由。 它会找到延迟最低且丢包率最低的路由，而不是使用Internet上的默认路由。

以下图像资产示例介绍了新增的智能成像优化功能：

| 图像(URL) | 缩略图 | 大小(JPEG) | 大小(WebP)，带智能成像 | 大小(AVIF)，带智能成像 | 使用WebP减少% | 使用AVIF减少% |
|---|---|---|---|---|---|---|
| [图像1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90.2 KB | 26.89% | 37.79% |
| [图2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16.01% | 72.57% |
| [图像3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![图片3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87.1 KB | 14.47% | 60.58% |
| [图像4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8.25% | 51.85% |

与上述内容类似，Adobe还使用较大的样本集进行测试。 与WebP相比，AVIF格式提供了20%的额外尺寸缩减，而WebP格式提供了27%的JPEG缩减。 视觉质量一致。 AVIF总体而言，与JPEG相比，其平均大小缩减率高达41%。

比较WebP和AVIF与PNG，您可以看到WebP和AVIF的大小分别减少84%和87%。 此外，由于WebP和AVIF格式都支持透明度和多幅图像动画，因此它非常适合替换透明的PNG和GIF文件。

另请参阅 [使用下一代图像格式（WebP和AVIF）优化图像](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## 最新的“智能成像”功能有哪些主要优势？ {#what-are-the-key-benefits-of-smart-imaging}

“智能成像”可根据使用中的客户端浏览器、设备显示和网络条件自动优化图像文件大小，从而提供更好的图像交付性能。 由于图像构成页面加载时间的绝大部分，因此任何性能改进都可能对业务KPI产生深远影响，例如更高的转化率、网站逗留时间和较低的网站跳出率。

最新智能成像的最新主要优势包括：

* 现在支持下一代AVIF格式。
* PNG到WebP和AVIF现在支持有损转换。 由于PNG是无损格式，因此早期交付的WebP和AVIF是无损的。
* 浏览器格式转换(`bfc`)
* 设备像素比率(`dpr`)
* 网络带宽(`network`)

### 关于浏览器格式转换(bfc) {#bfc}

通过附加打开浏览器格式转换 `bfc=on` 到图像URL会自动将JPEG和PNG转换为有损AVIF、有损WebP、有损JPEGXR、有损JPEG2000（对于不同的浏览器）。 对于不支持这些格式的浏览器，“智能成像”将继续提供JPEG或PNG。 除了格式之外，智能成像还会重新计算新格式的质量。

也可以通过附加 `bfc=off` 到图像的URL。

另请参阅 [bfc](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=en) 在Dynamic Media图像提供和渲染API中。

### 关于设备像素比率(dpr)优化 {#dpr}

设备像素比率(DPR)（也称为CSS像素比率）是设备的物理像素与逻辑像素之间的关系。 特别是随着视网膜屏幕的出现，现代移动设备的像素分辨率正以快速的速度增长。

启用“设备像素比率”优化后，图像将以屏幕的本机分辨率呈现，从而使其看起来清晰。

目前，显示屏的像素密度来自Akamai CDN标头值。

| 图像URL中允许的值 | 描述 |
|---|---|
| `dpr=off` | 在单个图像URL级别关闭DPR优化。 |
| `dpr=on,dprValue` | 使用自定义值覆盖由智能成像检测的DPR值（由任何客户端逻辑或其他方式检测）。 的允许值 `dprValue` 是大于0的任意数字。 |

>[!NOTE]
>
>* 您可以使用 `dpr=on,dprValue` 即使公司级别的DPR设置为关闭也是如此。
>* 由于DPR优化，当生成的图像大于MaxPix Dynamic Media设置时，始终通过保持图像的宽高比来识别MaxPix宽度。


| 请求的图像大小 | 设备像素比率(dpr)值 | 传送的图像大小 |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

另请参阅 [使用图像时](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) 和 [使用智能裁剪时](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### 关于网络带宽优化 {#network}

打开网络带宽可根据实际网络带宽自动调整提供的图像质量。 对于网络带宽较差的情况，即使DPR（设备像素比）优化已打开，也会自动关闭。

如果需要，贵公司可以通过附加 `network=off` 到图像的URL。

| 图像URL中允许的值 | 描述 |
|---|---|
| `network=off` | 在单个图像URL级别关闭网络优化。 |

DPR和网络带宽值基于检测到的捆绑CDN的客户端值。 这些值有时不准确。 例如，DPR为2的iPhone5和iPhone12与 `dpr=3`，两个节目 `dpr=2`. 不过，对于高分辨率设备，发送 `dpr=2` 比发送好 `dpr=1`. 但是，要克服这种不准确性，最好的方法是使用客户端DPR为您提供100%的准确值。 它适用于任何设备，无论是Apple还是启动的任何其他设备。 请参阅 [使用具有客户端设备像素比的智能成像](/help/assets/client-side-dpr.md).

### 智能成像的其他主要优势

* 改进了使用最新智能成像的网页的Google SEO排名。
* 立即提供优化内容（在运行时）。
* 使用Adobe Sensei技术根据质量进行转换(`qlt`)。
* TTL（生存时间）独立。 以前，智能成像的工作TTL必须至少为12小时。
* 以前，原始图像和派生图像都会缓存，而且使缓存失效需分两步进行。 在最新的智能成像中，只缓存派生项，从而允许单步缓存失效过程。
* 在其规则集中使用自定义标头的客户可以从最新的智能成像中受益，因为这些标头不会被阻止，这与以前版本的智能成像不同。 例如，“Timing Allow Origin”、“X-Robot”(如 [向图像响应添加自定义标头值|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## 是否存在与智能成像相关的许可成本？ {#are-there-any-licensing-costs-associated-with-smart-imaging}

否. 智能成像功能包含在您的现有许可证中。 对于Dynamic Media Classic或Experience Manager- Dynamic Media(内部部署、AMS和Experience Manageras a Cloud Service)，此规则为true。

>[!NOTE]
>
>Dynamic Media — 混合型客户无法使用智能成像。

## 智能成像的工作原理是什么？ {#how-does-smart-imaging-work}

当消费者请求图像时，智能成像会检查用户特征，并根据使用中的浏览器将其转换为适当的图像格式。 执行这些格式转换的方式不会降低视觉保真度。 智能成像可根据浏览器功能以下方式自动将图像转换为不同格式。

* 如果浏览器支持格式，则自动转换为AVIF
* 如果AVIF转换不利或浏览器不支持AVIF，则自动转换为WebP
* 如果Safari不支持WebP，则自动转换为JPEG2000
* 自动转换为JPEGXR for IE 9及以上版本，或者如果Edge不支持WebP\
   |图像格式 |支持的浏览器 | |—|—| | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) | | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) | |JPEG2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) | | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |
* 对于不支持这些格式的浏览器，将提供最初请求的图像格式。

如果原始图像大小小于智能成像生成的图像大小，则会提供原始图像。

## 支持哪些图像格式？ {#what-image-formats-are-supported}

智能成像支持以下图像格式：

* JPEG
* PNG

对于JPEG图像文件格式，新格式的质量会通过智能成像重新计算。

对于支持PNG等透明度的图像文件格式，您可以配置“智能成像”以交付有损AVIF和WebP。 对于有损格式转换，“智能成像”会使用图像URL中提及的质量，或使用Dynamic Media公司帐户中配置的质量。

## “智能成像”如何与我的现有已使用的图像预设一起使用？ {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

“智能成像”可与您现有的图像预设配合使用，并可观察您的所有图像设置。 更改的内容是图像格式或质量设置，或两者都有。 对于格式转换，“智能成像”可根据图像预设设置的定义，保持完整的视觉保真度，但文件大小较小。

例如，假定图像预设的JPEG格式为，大小为500 x 500，质量=85，钝化蒙版=0.1,1,5。 当智能成像检测到用户在Chrome浏览器上时，图像会转换为WebP格式，大小为500 x 500，且WebP质量上的钝化蒙版=0.1,1,5，该WebP质量与尽可能接近的JPEG质量85相匹配。 将WebP转换的占用空间与JPEG进行比较，并返回两者中较小的。

## 我是否必须更改任何URL、图像预设，或在我的网站上部署任何新代码才能进行智能成像？ {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

否. 智能成像可无缝地与您现有的图像URL和图像预设配合使用。 此外，智能成像功能不要求您向网站添加代码以检测用户的浏览器。 所有此功能都将自动处理。

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## 智能成像是否可以使用HTTPS? HTTP/2呢？ {#does-smart-imaging-working-with-https-how-about-http}

智能成像可处理通过HTTP或HTTPS传送的图像。 此外，它还可通过HTTP/2运行。

## 我是否有资格使用智能成像？ {#am-i-eligible-to-use-smart-imaging}

要使用智能成像，贵公司的Dynamic Media Classic或Dynamic MediaExperience Manager帐户必须满足以下要求：

* 将Adobe捆绑的CDN（内容交付网络）用作许可证的一部分。
* 使用专用域(例如， `images.company.com` 或 `mycompany.scene7.com`)，而不是通用域(例如， `s7d1.scene7.com`, `s7d2.scene7.com`或 `s7d13.scene7.com`)。

要查找您的域，请打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

转到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**. 查找标记为 **[!UICONTROL 已发布的服务器名称]**. 如果您当前使用的是通用域，则可以请求移至您自己的自定义域。 在提交支持案例时，提出此过渡请求。

使用Dynamic Media许可证，您的第一个自定义域无需额外付费。

## 为我的帐户启用“智能成像”的过程是什么？ {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

启动使用智能成像的请求；它不会自动启用。

按如下所述创建支持案例。 在您的支持案例中，请务必提及要在帐户中启用以下哪项智能成像功能（一个或多个）：

* WebP
* AVIF
* DPR和网络带宽优化
* PNG到有损AVIF或有损WebP

如果您已经通过WebP启用了智能成像，但希望获得上述其他新功能，则必须创建一个支持案例。

**要创建支持案例以在您的帐户上启用智能成像，请执行以下操作：**

1. [使用Admin Console开始创建新的支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html).
1. 在支持案例中提供以下信息：

   * 主要联系人姓名、电子邮件、电话。

   * 列出您希望在帐户中启用以下哪些智能成像功能（一个或多个）：
      * WebP
      * AVIF
      * DPR和网络带宽优化
      * PNG到有损AVIF或有损WebP
   * 要启用智能成像的所有域(即 `images.company.com` 或 `mycompany.scene7.com`)。

      要查找您的域，请打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

      转到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**.

      查找标记为 **[!UICONTROL 已发布的服务器名称]**.

   * 确认您通过Adobe使用CDN，而不是通过直接关系进行管理。

   * 验证您使用的是专用域，例如 `images.company.com` 或 `mycompany.scene7.com`，而不是通用域，例如 `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      要查找您的域，请打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

      转到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**.

      查找标记为 **[!UICONTROL 已发布的服务器名称]**. 如果您当前使用的是通用Dynamic Media Classic域，则可以在此过渡中请求移至您自己的自定义域。

   * 指示您是否希望它通过HTTP/2运行。


1. Adobe客户支持根据请求的提交顺序将您添加到智能图像处理客户等待列表。
1. 当Adobe准备好处理您的请求时，客户支持团队会联系您以协调并设置目标日期。
1. **可选**:在Adobe将新功能推送到生产之前，您可以选择在暂存环境中测试智能成像。
1. 客户支持部门在完成后会通知您。
1. 为了最大限度地提高智能成像的性能，Adobe建议将生存时间(TTL)设置为24小时或更长。 TTL定义CDN缓存资产的时长。 要更改此设置，请执行以下操作：

   1. 如果您使用Dynamic Media Classic，请转到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 发布设置]** > **[!UICONTROL 图像服务器]**. 设置 **[!UICONTROL 默认客户端缓存的存留时间]** 值为24或更长时间。
   1. 如果您使用Dynamic Media，请 [这些说明](/help/assets/dm-publish-settings.md#common-thumbnail-attributes-tab). 设置 **[!UICONTROL 过期]** 值24小时或更长时间。

## 我何时才能通过智能成像启用我的帐户？ {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

根据等待列表，将按照客户支持接收请求的顺序来处理请求。

>[!NOTE]
>
>启用“智能成像”会涉及Adobe清除缓存，因此前置时间可能较长。 因此，在任何给定时间都只能处理少数客户过渡。

## 切换到使用智能成像有哪些风险？ {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

客户网页不存在风险。 但是，过渡到智能成像确实会清除CDN缓存。 此操作涉及在Experience Manager上迁移到Dynamic Media Classic或Dynamic Media的新配置。

在初始过渡期间，非缓存图像会直接点击Adobe的源服务器，直到再次重建缓存为止。 因此，Adobe计划一次处理一些客户过渡，以便在从源中提取请求时保持可接受的性能。 对于大多数客户而言，可在约1到2天内在CDN重新完全构建缓存。

## 如何验证智能成像是否按预期工作？{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 在您的帐户配置了“智能成像”功能后，请在浏览器中加载Dynamic Media Classic或Adobe Experience Manager - Dynamic Media图像URL。
1. 通过转到 **[!UICONTROL 查看]** > **[!UICONTROL 开发人员]** > **[!UICONTROL 开发人员工具]** 中。 或者，选择您选择的任何浏览器开发人员工具。

1. 确保在开发人员工具打开时禁用缓存。

   * 在Windows®上，导航到开发人员工具窗格中的设置，然后选择 **[!UICONTROL 禁用缓存（在devtools打开时）]** 复选框。
   * 在macOS上，在开发人员窗格的 **[!UICONTROL 网络]** 选项卡，选择 **[!UICONTROL 禁用缓存]**.

1. 观察内容类型已转换为相应的格式。 以下屏幕截图显示了在Chrome上动态转换为WebP的PNG图像。 如果您的域启用了AVIF，您还可以在内容类型中看到AVIF。
1. 在不同的浏览器和用户条件上重复此测试。

>[!NOTE]
>
>并非所有图像都会转换。 智能成像功能可决定转换是否可以提高性能。 有时，如果没有预期的性能增益或格式不JPEG或PNG，则不会转换图像。

![image2017-11-14_15398](/help/assets/assets/image2017-11-14_15398.png)

## 我如何知道性能的提升？ 是否有办法了解智能成像的好处？ {#benefits}

“智能成像”标头可确定“智能成像”的优势。 启用“智能成像”后，在您请求图像后，位于 **[!UICONTROL 响应标头]** 标题，您可以看到 `-X-Adobe-Smart-Imaging` 如以下突出显示的示例所示：

![智能成像头](/help/assets/assets-dm/smart-imaging-header2.png)

此标题可告知您以下信息：

* Smart Imaging正在为公司工作。
* 正值表示转换成功。 在这种情况下，将返回新的WebP图像。
* 负值表示转换失败。 在这种情况下，将返回原始请求的图像(默认情况下，如果未指定，则JPEG)。
* 正值显示请求的图像与新图像之间的字节差。 在上例中，保存的字节为 `75048` 或大约75 KB。
* 负值表示请求的图像小于新图像。 显示负大小差，但提供的图像仅是原始请求的图像。

>[!NOTE]
>
>**X-Adobe — 智能成像= -1，并提供WebP**
>
>如果的值为 `X-Adobe-Smart-Imaging` 为–1且WebP仍在交付中，这意味着智能成像正在运行，但由于旧缓存，大小优势未计算。 您可以使用 `cache=update` （仅一次）来修复此问题。
>使用修饰符的示例：
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>要使整个缓存失效，必须创建一个支持案例。

## 如何在智能成像中禁用AVIF优化？{#disable-avif}

如果要在默认情况下切换回提供WebP，请为此创建支持案例。 与往常一样，您可以通过添加参数来关闭智能成像 `bfc=off` 到图像的URL。 但是，您无法在用于智能成像的URL修饰符中选择WebP或AVIF。 此功能在您的公司帐户级别进行维护。

## 是否可以针对任何请求关闭智能成像？{#turning-off-smart-imaging}

是。您可以通过添加以下任意修饰符来关闭“智能成像”：

* `bfc=off` 关闭浏览器格式转换。 另请参阅 [浏览器格式转换](#bfc).
* `dpr=off` 关闭设备像素比。 另请参阅 [设备像素比](#dpr).
* `network=off` 关闭网络带宽。 另请参阅 [网络带宽](#network).

## 提供了哪些“调整”功能？ 是否可以定义任何设置或行为？ {#tuning-settings}

“智能成像”有三个选项，您可以启用或禁用。

* [浏览器格式转换](#bfc)
* [设备像素比](#dpr)
* [网络带宽](#network)

## 我在Chrome Web浏览器上有一个URL，其URL为fmt=tif。 但我的请求因ImageServer错误而失败。 为什么？ {#fmt-tif}

如果您的帐户未启用“智能成像”，则不会出现此错误。 智能成像仅适用于JPEG或PNG格式。

要避免出现此错误，您可以：

* 指定JPEG或PNG，或
* 不使用 `fmt` 修饰符，或
* 使用智能成像定义的浏览器首选格式。 例如，您可以对Chrome Web浏览器使用WebP。

## 我想从图像的URL下载TIFF图像。 我该怎么做？ {#download-tif}

添加 `fmt=tif` 和 `bfc=off` 到图像的URL路径。

## “智能成像”是仅管理图像格式，还是还管理图像质量设置以获得最佳效果？

智能成像既使用格式，又使用质量。 如果在图像URL中提出请求，则其余的参数将保持不变。

## 如果“智能成像”确实管理了质量设置，我是否可以设置最小值和最大值？ 换言之，质量不低于60、不大于80? {#quality-setting}

目前没有此类配置。

## “智能成像”会自动调整百分比质量输出设置，还是手动调整的设置，并且该设置适用于所有图像？ 在什么范围内？ {#percent-quality}

智能成像可自动调整质量百分比。 此质量百分比是使用由Adobe开发的机器学习算法确定的。 此百分比不是特定于范围的。

## 使用智能成像，支持或忽略哪些图像服务命令？ {#support-ignore}

唯一被忽略的命令是 `fmt` 和 `qlt`. 支持所有其余命令。

## 是否只有JPEG图像被智能成像所取代？ 如果我请求WebP、PNG或其他内容，该怎么办？ {#replace-request}

此功能仅适用于JPEG和PNG。

## 为什么JPEG图像有时会返回到Chrome而不是WebP? {#jpeg-returned}

“智能成像”可确定转换是否有益。 它只返回转换的新图像才有用。

## 为什么在复合图像中设备像素比率(dpr)功能无法按预期工作？ {#composite-images}

如果复合图像涉及的图层过多，则使用位置修饰符时，dpr功能可能会受到影响。 此问题已知，将在未来版本的智能成像中修复。 如果其他智能成像功能无法按预期工作，您可以创建支持案例来报告问题。

## 为什么Smart Imaging PNG仍然转换为无损的WebP/AVIF? {#convert-to-lossless}

由于PNG是无损格式，因此，早期交付的WebP和AVIF是无损的，因此其大小高于预期。 智能成像现在支持有损转换。 您可以使用修饰符 `cache=update` （仅一次）。 使用此修饰符的示例：

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

要使整个缓存失效，必须创建一个支持案例，请求执行此类操作。

## 在智能成像中，如何继续使用PNG进行无损转换？ {#continue-using}

智能成像现在支持基于质量级别的有损转换。 要继续使用无损转换，您可以使用通过公司设置或通过图像URL设置的100品质 `qlt=100` 在路径中。