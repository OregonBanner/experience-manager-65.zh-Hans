---
title: 智能成像
description: 智能成像应用每个用户独特的查看特性，自动提供针对其体验而优化的正确图像，从而提高性能和参与度。
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: Asset Management,Renditions
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
source-git-commit: ea983b24da66edd02f86614690f8bc5e1e2499d9
workflow-type: tm+mt
source-wordcount: '3624'
ht-degree: 1%

---

# 智能成像 {#smart-imaging}

## 什么是“智能成像”？ {#what-is-smart-imaging}

智能成像技术可应用Adobe Sensei AI功能，并与现有“图像预设”配合使用。 它致力于通过基于客户端浏览器功能自动优化图像格式、大小和质量来增强图像投放性能。

现在，通过改进的智能成像（现在同时支持AVIF和WebP），获得更好的Google Core Web Vital分数（最大内容绘制）。

>[!IMPORTANT]
>
>智能成像要求您使用随Adobe Experience Manager - Dynamic Media捆绑的现成CDN（内容分发网络）。 此功能不支持任何其他自定义CDN。

>[!TIP]
>
>尝试使用Dynamic Media并探索Dynamic Media图像修饰符和智能成像的好处 [_快照_](https://snapshot.scene7.com/).
>
> Snapshot是一种可视化演示工具，旨在说明Dynamic Media在优化和动态图像投放方面的强大功能。 试验测试图像或Dynamic Media URL，以可视化方式观察各种Dynamic Media图像修饰符的输出，并对以下内容进行智能图像优化：
>* 文件大小（通过WebP和AVIF投放）
>* 网络带宽
>* DPR（设备像素比率）
>
>要了解使用快照有多容易，请播放 [快照培训视频](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=en) （3分17秒）。

智能成像技术与Adobe一流的高级CDN（内容交付网络）服务完全集成，从而进一步提高了性能。 此服务可找到服务器、网络和对等点之间的最佳Internet路由。 它可以找到具有最低延迟和最低数据包丢失率的路由，而不使用Internet上的默认路由。

以下图像资产示例描述了添加的智能成像优化：

| 图像(URL) | 缩略图 | 大小(JPEG) | 使用智能成像调整大小(WebP) | 使用智能成像调整大小(AVIF) | 使用WebP降低% | AVIF降低% |
|---|---|---|---|---|---|---|
| [图像1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90.2 KB | 26.89% | 37.79% |
| [图像2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16.01% | 72.57% |
| [图像3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87.1 KB | 14.47% | 60.58% |
| [图像4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8.25% | 51.85% |

与上述类似，Adobe还运行了包含较大样本集的测试。 AVIF格式比WebP尺寸额外减少20%，比JPEG减少27%。 视觉质量都一样。 总的来说，与JPEG相比，AVIF的平均大小缩减率高达41%。

将WebP和AVIF与PNG进行比较，可以看到WebP的大小减少了84%，AVIF的大小减少了87%。 而且，由于WebP和AVIF格式都支持透明度和多种图像动画，因此非常适合替代透明的PNG和GIF文件。

另请参阅 [使用新一代图像格式（WebP和AVIF）优化图像](https://blog.developer.adobe.com/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## 最新智能成像的主要优势是什么？ {#what-are-the-key-benefits-of-smart-imaging}

智能成像可根据正在使用的客户端浏览器、设备显示和网络条件自动优化图像文件大小，从而提供更好的图像投放性能。 由于图像构成了页面加载时间的大部分，因此任何性能改进都会对业务KPI产生深远的影响，例如转化率提高、网站逗留时间和网站跳出率降低。

最新智能成像的最新主要优势包括：

* 现在支持下一代AVIF格式。
* PNG到WebP和AVIF现在支持有损转换。 由于PNG是一种无损格式，因此传送的早期WebP和AVIF是无损的。
* 浏览器格式转换(`bfc`)
* 设备像素比率(`dpr`)
* 网络带宽(`network`)

### 关于浏览器格式转换(bfc) {#bfc}

通过附加来打开浏览器格式转换 `bfc=on` 对于图像URL，自动将JPEG和PNG转换为有损AVIF、有损WebP、有损JPEGXR、有损JPEG2000（对于不同的浏览器）。 对于不支持这些格式的浏览器，智能成像将继续提供JPEG或PNG。 与格式一起，新格式的质量由智能成像重新计算。

智能成像也可以通过附加来关闭 `bfc=off` 到图像的URL。

另请参阅 [BFC](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=en) 在Dynamic Media图像服务和渲染API中。

### 关于设备像素比(dpr)优化 {#dpr}

设备像素比率(DPR)，也称为CSS像素比率，是设备的物理像素与逻辑像素之间的关系。 特别是随着视网膜屏幕的出现，现代移动设备的像素分辨率正以更快的速度增长。

启用“设备像素比”优化将以屏幕的本机分辨率渲染图像，从而使图像更加锐利。

目前，显示器的像素密度来自Akamai CDN标头值。

| 图像URL中允许的值 | 描述 |
|---|---|
| `dpr=off` | 在单个图像URL级别关闭DPR优化。 |
| `dpr=on,dprValue` | 使用自定义值（由任何客户端逻辑或其他方法检测到）覆盖智能成像检测到的DPR值。 允许的值 `dprValue` 是大于0的任何数字。 |

>[!NOTE]
>
>* 您可以使用 `dpr=on,dprValue` 即使公司级别的DPR设置为“关闭”。
>* 由于DPR优化，当合成图像大于MaxPix Dynamic Media设置时，始终通过保持图像的宽高比来识别MaxPix宽度。


| 请求的图像大小 | 设备像素比率(dpr)值 | 交付的图像大小 |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

另请参阅 [使用图像时](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) 和 [使用智能裁剪时](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### 关于网络带宽优化 {#network}

启用“网络带宽”可根据实际网络带宽自动调整所提供的图像质量。 对于较差的网络带宽，DPR（设备像素比）优化会自动关闭，即使它已经打开。

如有需要，贵公司可以通过追加以下内容来选择退出个别映像级别的网络带宽优化 `network=off` 到图像的URL。

| 图像URL中允许的值 | 描述 |
|---|---|
| `network=off` | 关闭单个图像URL级别的网络优化。 |

DPR和网络带宽值基于捆绑的CDN所检测到的客户端值。 这些值有时不准确。 例如，DPR=2的iPhone5和DPR为2的iPhone12 `dpr=3`，都显示 `dpr=2`. 但是，对于高分辨率设备，发送 `dpr=2` 比发送好 `dpr=1`. 但是，克服这种不准确性的最佳方法是使用客户端DPR为您提供100%准确的值。 它适用于任何设备，无论是Apple还是任何其他已启动的设备。 参见 [使用具有客户端设备像素比的智能成像](/help/assets/client-side-dpr.md).

### 智能成像的其他主要优势

* 改进了使用最新智能成像的网页的Google SEO排名。
* 立即提供优化的内容（在运行时）。
* 使用Adobe Sensei技术根据质量(`qlt`)。
* TTL（生存时间）独立。 以前，智能成像必须至少12小时的TTL才能正常工作。
* 以前，原始图像和派生图像都被缓存，缓存失效分为两步。 在最新的智能成像中，仅缓存衍生品，从而允许执行单步缓存失效过程。
* 在规则集中使用自定义标头的客户可以从最新的智能成像中受益，因为与以前的智能成像版本不同，这些标头不会受到阻止。 例如，“计时允许来源”、“X-Robot”，如中所示 [向图像响应添加自定义标头值|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## 智能成像是否有任何许可成本？ {#are-there-any-licensing-costs-associated-with-smart-imaging}

否. 智能成像包含在您的现有许可证中。 此规则适用于Dynamic Media Classic或Experience Manager - Dynamic Media(内部部署、AMS和Experience Manageras a Cloud Service)。

>[!NOTE]
>
>智能成像不适用于Dynamic Media — 混合型客户。

## 智能成像如何工作？ {#how-does-smart-imaging-work}

当用户请求图像时，智能成像会检查用户特征，并根据使用的浏览器将其转换为相应的图像格式。 这些格式转换以不降低视觉保真度的方式进行。 智能成像根据浏览器功能，通过以下方式自动将图像转换为不同格式。

* 如果浏览器支持格式，则自动转换为AVIF
* 如果AVIF转换无益或浏览器不支持AVIF，则自动转换为WebP
* 如果Safari不支持WebP，则自动转换为JPEG2000
* 自动转换为IE 9及以上版本的JPEGXR，或Edge不支持WebP\
   |图像格式 |支持的浏览器 | |—|—| |阿维夫 | [https://caniuse.com/avif](https://caniuse.com/avif) | | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) | |JPEG2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) | | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |
* 对于不支持这些格式的浏览器，将提供最初请求的图像格式。

如果原始图像大小小于智能成像生成的尺寸，则提供原始图像。

## 支持哪些图像格式？ {#what-image-formats-are-supported}

智能成像支持以下图像格式：

* JPEG
* PNG

对于JPEG图像文件格式，新格式的质量由智能成像重新计算。

对于支持PNG等透明度的图像文件格式，您可以配置智能成像以传递有损的AVIF和WebP。 对于有损格式转换，智能成像使用图像URL中提到的品质，或者使用Dynamic Media公司帐户中配置的品质。

## 智能成像如何与已使用的现有图像预设一起使用？ {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

智能成像可与您现有的图像预设结合使用，并观察您的所有图像设置。 更改的是图像格式或质量设置，或同时更改两者。 对于格式转换，智能成像将保持图像预设设置所定义的完整视觉保真度，但文件大小较小。

例如，假设定义了图像预设，其中JPEG格式为，大小为500 x 500，质量为85，钝化蒙版为0.1,1，5。 当智能成像检测到用户在Chrome浏览器上时，图像将转换为WebP格式，大小为500 x 500。 而且，钝化蒙版=0.1、1、5的WebP质量与JPEG质量尽可能接近85。 将WebP转换的占地面积与JPEG进行比较，并返回两者中的较小者。

## 我是否需要更改任何URL、图像预设，或在我的网站上部署任何用于智能成像的新代码？ {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

否. 智能成像可与您现有的图像URL和图像预设无缝配合使用。 此外，智能成像不要求您向网站添加代码以检测用户的浏览器。 所有这些功能都会自动处理。

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## 智能成像是否适用于HTTPS？ HTTP/2呢？ {#does-smart-imaging-working-with-https-how-about-http}

智能成像处理通过HTTP或HTTPS交付的图像。 此外，它还适用于HTTP/2。

## 我是否有资格使用智能成像？ {#am-i-eligible-to-use-smart-imaging}

要使用智能成像，您公司的Dynamic Media Classic或Dynamic MediaExperience Manager帐户必须满足以下要求：

* 将Adobe捆绑的CDN（内容分发网络）用作许可证的一部分。
* 使用专用域(例如， `images.company.com` 或 `mycompany.scene7.com`)，而不是通用域(例如， `s7d1.scene7.com`， `s7d2.scene7.com`，或 `s7d13.scene7.com`)。

要查找您的域，请打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

转到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**. 查找标记为的字段 **[!UICONTROL 已发布的服务器名称]**. 如果您当前使用通用域，则可以请求迁移到您自己的自定义域。 在提交支持案例时提出此过渡请求。

使用Dynamic Media许可证，您的第一个自定义域不会产生额外费用。

## 为我的帐户启用智能成像的过程是怎样的？ {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

您启动了一个使用智能成像的请求；它不会自动启用。

创建支持案例，如下所述。 在您的支持案例中，请务必提及要在帐户中启用的以下智能成像功能（一项或多项）：

* WebP
* AVIF
* DPR和网络带宽优化
* PNG到有损AVIF或有损WebP

如果您已经为WebP启用了智能成像，但希望获得上面列出的其他新功能，则必须创建一个支持案例。

**要创建支持案例以在您的帐户上启用智能成像，请执行以下操作：**

1. [使用Admin Console开始创建新的支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html).
1. 在您的支持案例中提供以下信息：

   * 主要联系人姓名、电子邮件、电话。

   * 列出要在帐户中启用的以下智能成像功能（一个或多个）：
      * WebP
      * AVIF
      * DPR和网络带宽优化
      * PNG到有损AVIF或有损WebP
   * 要启用智能成像的所有域(即， `images.company.com` 或 `mycompany.scene7.com`)。

      要查找您的域，请打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

      转到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**.

      查找标记为的字段 **[!UICONTROL 已发布的服务器名称]**.

   * 验证您是否通过Adobe使用CDN，而不是通过直接关系进行管理。

   * 验证您是否使用专用域，例如 `images.company.com` 或 `mycompany.scene7.com`，而不是通用域，例如 `s7d1.scene7.com`， `s7d2.scene7.com`， `s7d13.scene7.com`.

      要查找您的域，请打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

      转到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**.

      查找标记为的字段 **[!UICONTROL 已发布的服务器名称]**. 如果您当前使用的是通用Dynamic Media Classic域，则可以请求在此过渡中转移到您自己的自定义域。

   * 指示您是否希望它通过HTTP/2工作。


1. Adobe客户支持根据提交请求的顺序将您添加到智能成像客户等待列表。
1. 当Adobe准备好处理您的请求时，客户支持将联系您进行协调并设置目标日期。
1. **可选**：在Adobe将新功能推送到生产环境之前，您可以选择在“测试”中测试智能成像。
1. 客户支持团队会在完成后通知您。
1. 为了最大限度地提高智能成像的性能，Adobe建议将生存时间(TTL)设置为24小时或更长。 TTL定义CDN缓存资产的时长。 要更改此设置，请执行以下操作：

   1. 如果您使用Dynamic Media Classic，请转到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 发布设置]** > **[!UICONTROL 图像服务器]**. 设置 **[!UICONTROL 默认客户端缓存生存时间]** 值为24或更长。
   1. 如果您使用Dynamic Media，请关注 [这些说明](/help/assets/dm-publish-settings.md#common-thumbnail-attributes-tab). 设置 **[!UICONTROL 过期]** 值为24小时或更长时间。

## 我何时才能使用智能成像启用帐户？ {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

根据等待列表，请求将按照客户支持收到请求的顺序进行处理。

>[!NOTE]
>
>由于启用智能成像需要Adobe清除缓存，因此可能会存在较长的准备时间。 因此，在任何给定时间只能处理少数客户过渡。

## 切换使用智能成像有什么风险？ {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

客户网页没有风险。 但是，过渡到智能成像确实会清除CDN缓存。 此操作涉及在Experience Manager时迁移到Dynamic Media Classic或Dynamic Media的新配置。

在初始过渡期间，非缓存的图像直接点击Adobe的原始服务器，直到再次重建缓存。 因此，Adobe计划一次处理一些客户过渡，以便在从源拉取请求时保持可接受的性能。 对于大多数客户而言，CDN会在大约1 - 2天内再次完全构建缓存。

## 如何验证智能成像是否按预期工作？{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 为您的帐户配置了智能成像后，在浏览器上加载Dynamic Media Classic或Adobe Experience Manager - Dynamic Media图像URL。
1. 打开Chrome开发人员窗格，方法是转到 **[!UICONTROL 视图]** > **[!UICONTROL 开发人员]** > **[!UICONTROL 开发人员工具]** 在浏览器中。 或者，选择您选择的任何浏览器开发人员工具。

1. 确保在打开开发人员工具时禁用缓存。

   * 在Windows®上，导航到开发人员工具窗格中的设置，然后选择 **[!UICONTROL 禁用缓存（当devtools打开时）]** 复选框。
   * 在macOS上，在开发人员窗格中的 **[!UICONTROL 网络]** 选项卡，选择 **[!UICONTROL 禁用缓存]**.

1. 请注意，内容类型已转换为相应的格式。 以下屏幕截图显示了在Chrome上动态转换为WebP的PNG图像。 如果您的域启用了AVIF，则还可能会在“内容类型”中看到AVIF。
1. 在不同的浏览器和用户条件下重复此测试。

>[!NOTE]
>
>并非所有图像都会被转换。 智能成像决定转换是否可以改善性能。 有时，如果没有预期的性能提升，或者格式不是JPEG或PNG，则图像不会转换。

![image2017-11-14_15398](/help/assets/assets/image2017-11-14_15398.png)

## 我如何知道性能提升？ 是否有办法了解智能成像的好处？ {#benefits}

智能成像页眉决定了智能成像的好处。 启用智能成像后，请求图像后，在 **[!UICONTROL 响应标头]** 标题，您会看到 `-X-Adobe-Smart-Imaging` 如以下高亮显示的示例中所示：

![智能成像页眉](/help/assets/assets-dm/smart-imaging-header2.png)

此标头说明以下内容：

* Smart Imaging为公司服务。
* 正值表示转换成功。 在这种情况下，将返回一个新的WebP图像。
* 负值表示转换不成功。 在这种情况下，将返回原始请求的图像(如果未指定，则默认为JPEG)。
* 正值显示所请求图像与新图像之间的字节数差异。 在上述示例中，保存的字节为 `75048` 或75 KB左右。
* 负值表示所请求的图像小于新图像。 显示负大小差异，但提供的图像仅为原始请求的图像。

>[!NOTE]
>
>**XAdobe智能成像= -1，正在交付WebP**
>
>如果 `X-Adobe-Smart-Imaging` 为–1，并且仍在提供WebP，这意味着智能成像正在工作，但由于缓存过旧，未计算大小优势。 您可以使用 `cache=update` （仅限一次）以修复此问题。
>使用修饰符的示例：
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>要使整个缓存失效，必须创建一个支持案例。

## 如何在智能成像中禁用AVIF优化？{#disable-avif}

如果您希望默认情况下切换回为WebP提供服务，请为其创建支持案例。 与往常一样，您可以通过添加参数来关闭智能成像 `bfc=off` 到图像的URL。 但是，您不能在用于智能成像的URL修饰符中选择WebP或AVIF。 此功能在您的公司帐户级别进行维护。

## 是否可以为任何请求关闭智能成像？{#turning-off-smart-imaging}

是。您可以通过添加以下任何修饰符来关闭智能成像：

* `bfc=off` 以关闭“浏览器格式转换”。 另请参阅 [浏览器格式转换](#bfc).
* `dpr=off` 以关闭“设备像素比”。 另请参阅 [设备像素比率](#dpr).
* `network=off` 关闭网络带宽。 另请参阅 [网络带宽](#network).

## 提供了哪些“调整”功能？ 是否可定义任何设置或行为？ {#tuning-settings}

“智能成像”有三个选项，您可以启用或禁用。

* [浏览器格式转换](#bfc)
* [设备像素比率](#dpr)
* [网络带宽](#network)

## 我在Chrome Web浏览器上有一个使用fmt=tif的URL。 但我的请求失败，并出现ImageServer错误。 为什么？ {#fmt-tif}

如果您的帐户未启用智能成像，则不会发生此错误。 智能成像仅适用于JPEG或PNG格式。

要避免此错误，您可以：

* 指定JPEG或PNG，或
* 不使用 `fmt` 修改者，或
* 使用由智能成像定义的浏览器首选格式。 例如，您可以为Chrome Web浏览器使用WebP。

## 我希望从图像的URL下载TIFF图像。 我该怎么做？ {#download-tif}

添加 `fmt=tif` 和 `bfc=off` 到图像的URL路径。

## 智能成像是只管理图像格式，还是同时管理图像质量设置以获得最佳效果？

智能成像同时使用格式和质量。 其余参数保持不变（如果图像的URL中有请求）。

## 如果智能成像管理质量设置，是否可以设置最小值和最大值？ 换句话说，一个不小于60且不大于80的品质？ {#quality-setting}

目前没有此类配置。

## 智能成像是自动调整百分比质量输出设置，还是手动调整并应用于所有图像的设置？ 在什么范围内？ {#percent-quality}

智能成像可自动调整质量百分比。 该质量百分比由Adobe开发的机器学习算法确定。 此百分比不特定于范围。

## 对于智能成像，支持或忽略哪些图像服务命令？ {#support-ignore}

唯一被忽略的命令是 `fmt` 和 `qlt`. 支持所有其余命令。

## 是否只有JPEG图像被智能成像取代？ 如果我请求WebP、PNG或其他什么怎么办？ {#replace-request}

此功能仅适用于JPEG和PNG。

## 为何JPEG图像有时会返回到Chrome而不是WebP？ {#jpeg-returned}

智能成像可确定转换是否有效。 它只返回新图像，表示转换是有益的。

## 为什么设备像素比(dpr)功能无法按预期用于复合图像？ {#composite-images}

如果复合图像涉及太多图层，则在使用position修饰符时，dpr功能可能会受到影响。 此问题已知，将在未来版本的智能成像中修复。 如果其他智能成像功能无法按预期工作，您可以创建一个支持案例来报告问题。

## 为什么智能成像PNG仍会转换为无损WebP/AVIF？ {#convert-to-lossless}

由于PNG是一种无损格式，因此传送的早期WebP和AVIF是无损的，从而导致比预期更大的大小。 智能成像现在支持有损转换。 您可以使用修改量 `cache=update` （仅限一次）来修复此问题。 使用此修饰符的示例：

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

要使整个缓存失效，您必须创建一个请求此类工作的支持案例。

## 如何在智能成像中继续使用PNG无损转换？ {#continue-using}

智能成像现在支持基于质量级别的有损转换。 要继续使用无损转换，您可以使用通过公司设置或通过图像的URL设置的100品质，使用 `qlt=100` 在路径中。