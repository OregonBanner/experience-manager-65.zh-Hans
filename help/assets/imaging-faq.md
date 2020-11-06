---
title: 智能成像
description: 智能图像处理利用每个用户独特的查看特性自动提供为其体验优化的正确图像，从而获得更好的性能和参与度。
uuid: c11e52ba-8d64-4dc5-b30a-fc10c2b704e5
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
translation-type: tm+mt
source-git-commit: b4b500cc80c6d498baaabe3a6863a3843b904f9b
workflow-type: tm+mt
source-wordcount: '2085'
ht-degree: 1%

---


# 智能图像处理 {#smart-imaging}

## 什么是“智能成像”? {#what-is-smart-imaging}

智能成像技术利用Adobe Sensei人工智能功能并与现有的“图像预设”配合，通过基于客户浏览器功能自动优化图像格式、大小和质量来增强图像投放性能。

Smart Imaging还可以与Adobe一流的高级CDN服务完全集成，从而增强性能。 此服务在服务器、网络和对等点之间找到最佳的因特网路由，这些点的延迟和／或数据包丢失率低于因特网上的默认路由。

以下图像资产示例描述了添加的智能成像优化：

| Image<br>(URL) | 缩略图 | 大小<br> (JPEG) | 大小(WebP)<br> （带智能成像） | 减少 |
|---|---|---|---|---|
| [图像1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [图像2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [图像3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [图像4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | 平均= 51% |

与上面所示相似，Adobe还通过来自实时客户站点的7009个URL运行测试，并且由于具备智能成像功能，平均可对JPEG进行38%的文件大小优化，对WebP格式的PNG进行31%的文件大小进一步优化。

## 最新的智能成像有哪些主要优势？ {#what-are-the-key-benefits-of-smart-imaging}

由于图像占页面加载时间的大部分，因此性能改进可能会对业务KPI产生深远影响，如更高的转化率、在网站上停留的时间以及更低的网站弹出率。

最新版智能成像中的增强功能：

* 立即提供优化内容（在运行时）。
* 使用Adobe Sensei技术根据图像请求中指定的质量(qlt)进行转换。
* 使用“bfc”URL参数可以关闭智能成像。
* TTL（生存时间）独立。 以前，智能成像的最低TTL为12小时是工作必备条件。
* 以前，原始图像和衍生图像都被缓存，而使缓存失效的过程是2步。 在最新的智能成像中，只缓存衍生项，从而允许单步缓存失效过程。
* 使用其规则集中的自定义标头(例如，向图像响应添加自定义标头值|Dynamic [Media Classic中建议的“定时允许来源”、“X-Robot”](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html))的客户将从最新的智能成像中受益，因为这些标头不会被阻止，这与以前版本的智能成像不同。

## 是否存在与智能成像相关的许可成本？ {#are-there-any-licensing-costs-associated-with-smart-imaging}

否. 您现有的Dynamic Media Classic(Scene7)或AEM Dynamic Media(作为Cloud Service，在Prem、AMS和AEM上)许可证中包含智能成像。

>[!NOTE]
>
>Dynamic Media - Hybrid客户不可使用智能成像。


## 智能成像的工作原理是什么？ {#how-does-smart-imaging-work}

当用户请求图像时，我们会检查用户特征并根据使用中的浏览器转换为适当的图像格式。 以不降低视觉保真度的方式进行这些格式转换。 智能成像根据浏览器功能按以下方式自动将图像转换为不同格式。

* 自动转换为以下浏览器的WebP:
   * 铬黄
   * Firefox
   * Microsoft Edge
   * Safari 14.0 +
      * 仅带iOS 14.0及更高版本和macOS BigSur及更高版本的Safari 14
   * Android
   * Opera
* 对以下内容的传统浏览器支持：

   | 浏览器 | 浏览器／操作系统版本 | 格式 |
   | --- | --- | --- |
   | Safari | iOS 14.0或更早版本 | JPEG2000 |
   | Edge | 18或更早版本 | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* 对于不支持这些格式的浏览器，将提供最初请求的图像格式。

如果原始图像大小小于智能成像生成的图像大小，则会显示原始图像。

## 支持哪些图像格式？ {#what-image-formats-are-supported}

智能成像支持以下图像格式：
* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## 智能成像如何处理我们现有的已使用的图像预设？ {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

Smart Imaging可与您现有的“图像预设”配合使用，如果请求的文件格式为JPEG或PNG，则除了质量(qlt)和格式(fmt)外，还会观察您的所有图像设置。 对于格式转换，我们会根据图像预设设置的定义保持完全的视觉保真度，但文件大小会更小。 如果原始图像大小小于智能成像所生成的图像大小，则会显示原始图像。

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## 我是否必须更改任何URL、图像预设，或在我的网站上部署任何用于智能成像的新代码？ {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

如果您在现有自定义域上配置智能成像，则智能成像可以与您的现有图像URL和图像预设无缝协作。 此外，智能成像不要求您在网站上添加任何代码来检测用户的浏览器。 所有这些都是自动处理的。

如果您需要配置新的自定义域以使用智能成像，则需要更新URL以反映此自定义域。

另外，请参 [阅我是否有资格使用智能成像？](#am-i-eligible-to-use-smart-imaging) 了解智能成像的先决条件。

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## 智能成像是否可以与HTTPS一起使用？ HTTP/2如何？ {#does-smart-imaging-working-with-https-how-about-http}

智能成像可处理通过HTTP或HTTPS传送的图像。 此外，它还可通过HTTP/2运行。

## 我是否有资格使用智能成像？ {#am-i-eligible-to-use-smart-imaging}

要使用智能成像，您的公司的AEM帐户上的Dynamic Media Classic或Dynamic Media必须满足以下要求：

* 将Adobe捆绑的CDN(内容投放网络)作为许可的一部分。
* 使用专用域(例如， `images.company.com` 或 `mycompany.scene7.com`)，而不是通用域(例如， `s7d1.scene7.com`、 `s7d2.scene7.com`或 `s7d13.scene7.com`)。

要查找您的域，请登录到您的公司帐户或帐户。

Tap **[!UICONTROL Setup > Application Setup > General Settings.]** 查找标有“已发布服 **[!UICONTROL 务器名称”的字段。]** 如果您当前使用的是通用域，则在提交技术支持票证时，可以请求移至您自己的自定义域作为本过渡的一部分。

Dynamic Media许可证不需要支付任何额外费用即可获得您的第一个自定义域。

## 为我的帐户启用智能成像的过程是什么？ {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

您必须启动使用智能成像的请求；它不会自动启用。

1. [使用Admin Console创建支持案例。](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
1. 在您的支持案例中提供以下信息：

   1. 主要联系人姓名、电子邮件、电话。
   1. 要启用智能成像的所有域(即 `images.company.com` 或 `mycompany.scene7.com`)。

      要查找您的域，请登录您的公司帐户或帐户。

      Click **[!UICONTROL Setup > Application Setup > General Settings.]**

      查找标有“已发布服 **[!UICONTROL 务器名称”的字段。]**
   1. 验证您是否通过Adobe使用CDN，而不是直接管理。
   1. 验证您使用的是专用域(如 `images.company.com` 或 `mycompany.scene7.com`)，而不是通用域(如 `s7d1.scene7.com`、 `s7d2.scene7.com``s7d13.scene7.com`)。

      要查找您的域，请登录您的公司帐户或帐户。

      Click **[!UICONTROL Setup > Application Setup > General Settings.]**

      查找标有“已发布服 **[!UICONTROL 务器名称”的字段。]** 如果您当前使用的是通用的Dynamic Media Classic域，则可以请求移至您自己的自定义域作为此过渡的一部分。
   1. 指示您是否也需要它才能通过HTTP/2使用。

1. 技术支持将根据请求的提交顺序将您添加到智能图像处理客户等待列表。
1. 当Adobe准备好处理您的请求时，支持人员将与您联系以协调和设置目标日期。
1. **可选**:在Adobe将新功能推向生产之前，您可以选择在暂存中测试智能成像。
1. 完成后，支持会通知您。
1. 为最大限度地提高智能成像的性能，Adobe建议将生存时间(TTL)设置为24小时或更长。 TTL定义CDN缓存资源的时长。 要更改此设置：

   1. 如果您使用Dynamic Media Classic，请单击“设 **[!UICONTROL 置”>“应用程序设置”>“发布设置”>“图像服务器”。]** 将“默 **[!UICONTROL 认客户端缓存时间”设置为]** “实时”值24或更长。
   1. 如果您使用Dynamic Media，请按照 [以下说明](config-dynamic.md)。 将“过 **[!UICONTROL 期]** ”值设置为24小时或更长。

## 我希望何时启用智能映像？ {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

请求将按技术支持人员接收请求的顺序进行处理，并根据等待列表。

>[!NOTE]
启用智能成像需要Adobe清除缓存，因此可能需要较长的准备时间。 因此，在任何给定时间都只能处理少数客户过渡。

## 改用智能成像有哪些风险？ {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

客户网页不存在风险。 但是，您应该注意到，智能成像过渡会清除CDN中的缓存，因为它涉及到在AEM上切换到新的Dynamic Media Classic或Dynamic Media配置。

在初始过渡期间，非缓存图像直接点击Adobe的来源服务器，直到重新构建缓存。 因此，Adobe计划一次处理几个客户过渡，以便在从来源处理请求时保持可接受的性能。 对于大多数客户，在1到2天内在CDN重新完全建立缓存。

## 如何验证智能成像是否按预期工作？  {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 在您的帐户配置了智能成像后，请在浏览器上加载Dynamic Media Classic(Scene7)/Dynamic Media图像URL。
1. 在浏览器中单击“视图”>“开 **[!UICONTROL 发人员”>“开发人员工具]** ”，打开Chrome开发人员窗格。 或者，选择您选择的任何浏览器开发人员工具。

1. 确保在开发人员工具打开时禁用缓存。

   * 在Windows上——导航到开发人员工具窗格中的设置，然后选 **[!UICONTROL 择“禁用缓存（当设备工具打开时）]** ”复选框。
   * On Mac – in the developer pane, under the **[!UICONTROL Network]** tab, select **[!UICONTROL disable cache]** .

1. 观察内容类型将转换为适当的格式。 以下屏幕截图显示了在Chrome上将动态转换为WebP的PNG图像。
1. 在不同的浏览器和用户条件上重复此测试。

>[!NOTE]
并非所有图像都经过转换。 智能成像决定是否需要转换才能提高性能。 在某些情况下，如果没有预期的性能增益，或者格式不是JPEG或PNG，则不会转换图像。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## 我如何知道性能的提高？ 是否有方法可以注意智能成像的优势？ {#performance-gain}

**关于智能成像头**

智能映像头值仅在非缓存请求到现在才起作用。 这样做是为了保持当前缓存的兼容性，并避免当通过缓存服务图像时需要计算。

要使用智能成像头，您需要在请求中添`cache=off`加修饰符。 请参[阅Dynamic Media图像服务和渲染API中的缓存](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-cache.html)。

使用示 `cache=off` 例（仅用于说明）:

`https://domain.scene7.com/is/image/companyName/imageName?cache=off` 

在使用此类请求后，在“响应标题”部分，您可以看到 `-x-adobe-smart-imaging` 标题。 查看以下高亮显示的 `-x-adobe-smart-imaging` 屏幕截图。

![智能成像头](/help/assets/assets-dm/smart-imaging-header2.png) 

此标题值表示：

* Smart Imaging正在为公司提供帮助。
* 正值(>=0)表示转换成功。 在这种情况下，将返回新图像（此处为webP）。
* 负值(&lt;0)表示转换失败。 在这种情况下，将返回原始请求的图像（默认情况下为JPEG，如果未指定）。
* 该值表示请求的图像与新图像之间的字节差。 在这种情况下，保存的字节为75048，对于一个映像，这大约为75 KB。 
   * 负值表示请求的图像小于新图像。 我们确实显示了负大小差，但所提供的图像只是原始请求的图像

**何时使用智能成像头？**

智能映像响应头可用于调试目的，或在突出显示智能映像的优点时启用。 在正`cache=off`常情况下使用会显着影响加载时间。

## 是否可以关闭智能成像以请求任何请求？ {#turning-off-smart-imaging}

是. 您可以通过向URL添加修饰符来关闭 `bfc=off` 智能成像。

## 提供哪些“调整”? 是否可以定义任何设置或行为？ (#tuning-settings)

目前，您可以选择启用或禁用智能成像。 没有其他调整可用。

## 如果“智能成像”管理质量设置，我们是否可以设置最低和最高值？ 例如，是否可以设置“不低于60”和“不高于80质量”? (#minimum-maximum)

当前智能映像中不存在此类配置功能。

## 在某些情况下，JPEG图像会返回到Chrome而不是WebP图像。 为什么会发生这种事？ (#jpeg-webp)

智能成像确定转换是否有益。 仅当转换导致文件大小更小且质量相当时，才会返回新图像。
