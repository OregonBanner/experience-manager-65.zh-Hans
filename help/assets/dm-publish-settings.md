---
title: 配置Dynamic Media发布设置
description: 了解如何在Dynamic Media中设置Publishing。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
hide: true
hidefromtoc: true
exl-id: null
source-git-commit: 1985058faa2a85a4544b35f2a6925670207df9e1
workflow-type: tm+mt
source-wordcount: '3114'
ht-degree: 3%

---


# 配置Dynamic Media发布设置

>[!IMPORTANT]
>
>Dynamic Media发布设置仅在以下情况下可用：
>
>* 您在Scene7模式下运行Dynamic Media。
>* 您拥有 *现有* **[!UICONTROL Dynamic Media配置]** (在 **[!UICONTROL Cloud Services]**)在Adobe Experience Manager 6.5中或在Experience Manageras a Cloud Service中。
>* 您是具有管理员权限的Experience Manager系统管理员。


“Dynamic Media发布设置”页面设置决定了默认情况下如何将资产从Dynamic Media服务器Adobe到网站或应用程序。 如果未指定任何设置，AdobeDynamic Media服务器将根据“发布设置”页面上的默认设置来传送资产。 例如，如果请求传送的图像不包含分辨率属性，则会生成一个图像，其中图像服务器页面上具有默认对象分辨率设置。

管理员可以更改“图像服务器”、“图像渲染器”和“晕影”页面上的默认设置，以建立用于从服务器传送资产的默认设置。

>[!NOTE]
>
>Dynamic Media发布设置适用于经验丰富的网站开发人员和程序员。 AdobeDynamic Media假定更改其中任何默认发布设置的用户熟悉AdobeDynamic Media、HTTP协议标准和惯例以及基本成像技术。

**要配置Dynamic Media发布设置，请执行以下操作：**

1. 在Experience Manager创作模式下，选择Experience Manager徽标以访问全局导航控制台。
1. 在左边栏中，选择工具图标，然后转到 **[!UICONTROL 资产]** > **[!UICONTROL Dynamic Media发布设置]**.
1. 在“图像服务器”页面中，设置图像服务器 — 发布上下文，然后使用五个选项卡配置默认的发布设置。

   * [图像服务器](#image-server)
   * [安全性](#security-tab) 选项卡
   * [目录管理](#catalog-management-tab) 选项卡
   * [请求属性](#request-attributes-tab) 选项卡
   * [常见缩略图属性](#common-thumbnail-attributes-tab) 选项卡
   * [色彩管理属性](#color-management-attributes-tab) 选项卡

   ![Dynamic Media发布设置页面](/help/assets/assets-dm/dm-publish-setup.png)
   *Dynamic Media发布设置页面，其中&#x200B;**[!UICONTROL 请求属性]**选项卡。*<br><br>

1. 完成后，在页面的右上角附近，选择 **[!UICONTROL 保存]**.

## 图像服务器 {#image-server}

“图像服务器”页为从图像服务器传送图像建立了默认设置。 有五个类别提供了设置

| 发布上下文 | 描述 |
| --- | --- |
| 图像服务 | 指定发布设置的上下文。 |
| 提供测试图像 | 指定用于测试发布设置的上下文。<br>请参阅 [在将资产公开之前对其进行测试](#test-assets-before-making-public). |

### “安全”选项卡 {#security-tab}

**[!UICONTROL 客户端地址]**  — 用于指定一个或多个IP地址或IP地址范围。 指定后，对此图像目录的请求将被拒绝，这些请求源自位于未列出IP地址的客户端。 此规则同时适用于图像和已渲染图像的交付。

### “目录管理”选项卡 {#catalog-management-tab}

**[!UICONTROL 规则集定义文件路径]**  — 指定包含图像目录的规则集定义的文件。

另请参阅 [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) 参数。

### “请求属性”选项卡 {#request-attributes-tab}

这些设置与图像的默认外观有关。

| 设置 | 描述 |
| --- | --- |
| **[!UICONTROL 回复图像大小限制]** | 必填.<br>指定返回给客户端的最大回复图像宽度和高度。 如果请求导致返回图像的宽度或高度或两者都大于此设置，则服务器会返回错误。<br>另请参阅 [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) 参数。 |
| **[!UICONTROL 请求混淆模式]** | 如果希望将base64编码应用于有效请求，则启用。<br>另请参阅 [请求模糊处理](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) 参数。 |
| **[!UICONTROL 请求锁定模式]** | 如果您希望请求中包含简单的哈希锁定，则启用。<br>另请参阅 [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) 参数。 |
| **[!UICONTROL 默认请求属性]** |  |
| **[!UICONTROL 默认图像文件后缀]** | 必填.<br>默认数据文件扩展名，如果路径不包含文件后缀，则附加到目录路径和掩码路径字段值中。<br>另请参阅 [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) 参数。 |
| **[!UICONTROL 默认字体名称]** | 指定在文本层请求未提供字体时使用的字体。 如果已指定，则必须是此图像目录的字体映射或默认目录的字体映射中的有效字体名称值。<br>另请参阅 [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) 参数。 |
| **[!UICONTROL 默认图像]** | 提供默认图像以返回，以响应未找到请求图像的请求。<br>另请参阅 [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) 参数。 |
| **[!UICONTROL 默认图像模式]** | 启用滑块框（右侧的滑块）后， **[!UICONTROL 默认图像]** 使用默认图像替换源图像中每个缺失的图层，并照常返回复合。 禁用滑块框（左侧的滑块）后，默认图像会替换整个复合图像，即使缺少的图像只是多个图层中的一个图层。<br>另请参阅 [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) 参数。 |
| **[!UICONTROL 默认视图大小]** | 必填.<br>如果请求未明确使用指定视图大小，则服务器将限制返回图像不得大于此宽度和高度 `wid=`, `hei=`或 `scl=`.<br>另请参阅 [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) 参数。 |
| **[!UICONTROL 默认缩略图大小]** | 必填.<br>使用而不是属性 **[!UICONTROL 默认视图大小]** 对于缩略图请求(`req=tmb`)。 如果缩略图请求(`req=tmb`)未明确使用 `wid=`, `hei=`或 `scl=`.<br>另请参阅 [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) 参数。 |
| **[!UICONTROL 默认背景颜色]** | 指定用于填充不包含实际图像数据的回复图像任何区域的RGB值。<br>另请参阅 [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) 参数。 |
| **[!UICONTROL JPEG 编码属性]** |  |
| **[!UICONTROL 质量]** | 指定JPEG回复图像的默认属性。 的 **[!UICONTROL 质量]** 字段，其定义范围为1 - 100。<br>另请参阅 [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) 参数。 |
| **[!UICONTROL 色度降采样]** | 启用或禁用JPEG编码器采用的以色度进行缩减采样。 |
| **[!UICONTROL 默认重新取样模式]** | 指定用于缩放图像数据的默认重新取样属性和插值属性。在 `resMode` 未在请求中指定。<br>另请参阅 [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) 参数。 |

### “常用缩略图属性”选项卡 {#common-thumbnail-attributes-tab}

这些设置与缩略图图像的默认外观和对齐方式有关。

| 设置 | 描述 |
| --- | --- |
| **[!UICONTROL 缩略图的默认背景颜色]** | 指定用于填充不包含实际图像数据的输出缩略图图像区域的RGB值。 仅用于缩略图请求(`req=tmb`)和时间 **[!UICONTROL 默认缩略图类型]** 设置设置为 **[!UICONTROL 拟合]** 或 **[!UICONTROL 纹理]**.<br>另请参阅 [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) 参数。 |
| **[!UICONTROL 水平对齐]** | 在由指定的回复图像矩形中指定缩略图的水平对齐方式 `wid=` 和 `hei=` 值。<br>仅用于缩略图请求(`req=tmb`)和时间 **[!UICONTROL 默认缩略图类型]** 设置设置为 **[!UICONTROL 拟合]**.<br>有三个水平对齐可供选择： **[!UICONTROL 居中对齐]**, **[!UICONTROL 左对齐]**&#x200B;和 **[!UICONTROL 右对齐]**.<br>另请参阅 [ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) 参数。 |
| **[!UICONTROL 垂直对齐]** | 在由指定的回复图像矩形中指定缩略图图像的垂直对齐方式 `wid=` 和 `hei=` 值。 仅用于缩略图请求(`req=tmb`)和时间 **[!UICONTROL 默认缩略图类型]** 设置设置为 **[!UICONTROL 拟合]**.<br>有三个垂直对齐方式可供选择： **[!UICONTROL 顶部对齐方式]**, **[!UICONTROL 居中对齐]**&#x200B;和 **[!UICONTROL 底部对齐方式]**.<br>另请参阅 [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) 参数。 |
| **[!UICONTROL 默认缓存生存时间]** | 提供默认的有效期时间间隔（以小时为单位），以防特定的目录记录不包含有效的目录有效期值。设置为 `-1` 标记为永不过期。 <br>另请参阅 [过期](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) 参数。 |
| **[!UICONTROL 默认缩略图类型]** | 为缩略图类型提供默认值，以防特定目录记录不包含有效的目录ThumbType值。 仅用于缩略图请求(`req=tmb`)。<br>有三种缩略图类型可供选择： **[!UICONTROL 裁切]**, **[!UICONTROL 拟合]**&#x200B;和 **[!UICONTROL 纹理]**.<br>另请参阅 [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) 参数。 |
| **[!UICONTROL 默认缩略图分辨率]** | 为缩略图对象分辨率提供默认值，以防特定目录记录不包含有效的目录ThumbRes值。 仅用于缩略图请求(`req=tmb`)和 **[!UICONTROL 默认缩略图类型]** 设置设置为 **[!UICONTROL 纹理]**.<br>另请参阅 [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) 参数。 |

### “色彩管理属性”选项卡 {#color-management-attributes-tab}

这些设置决定了图像使用的ICC颜色配置文件。

**颜色转换渲染意图**
颜色转换呈现意图允许覆盖工作配置文件的默认呈现意图以确定如何调整源颜色。 在以下情况下使用：

1. 默认的ICC配置文件之一是颜色转换的目标色彩空间。
1. 输出设备（打印机或显示器）的特征是此配置文件。
1. 而且，指定的渲染意图对此配置文件有效。

不同的渲染意图使用不同的规则来确定如何调整源颜色。

另请参阅 [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) 参数。

>[!NOTE]
>
>通常，最好对所选颜色设置使用默认渲染意图，该设置已通过Adobe测试，符合行业标准。 例如，如果您为北美或欧洲选择颜色设置，则默认颜色转换呈现意图为 **[!UICONTROL 相对色度]**. 如果为“日本”选择颜色设置，则默认颜色转换呈现意图为 **[!UICONTROL 知觉]**.

| 设置 | 特征 |
| --- | --- |
| **[!UICONTROL CMYK默认色彩空间]** | 指定要用作CMYK数据工作配置文件的ICC颜色配置文件的名称。 如果 **[!UICONTROL 未指定]** 选中后，当涉及CMYK源图像时，将禁用此图像目录的色彩管理。 所有CMYK工作空间都依赖于设备，这意味着它们基于实际的油墨和纸张组合。 CMYK工作空间Adobe供应基于标准商业印刷条件。<br> 另请参阅 [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) 参数。 |
| **[!UICONTROL 灰阶默认色彩空间]** | 指定ICC颜色配置文件的名称，以用作灰度数据的工作配置文件。 如果 **[!UICONTROL 未指定]** 选中后，当涉及灰度源图像时，将禁用此图像目录的颜色管理。<br>另请参阅 [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) 参数。 |
| **[!UICONTROL RGB默认色彩空间]** | 指定ICC颜色配置文件的名称，以用作RGB数据的工作配置文件。 如果 **[!UICONTROL 未指定]** 已选择，则在涉及RGB源图像时，将禁用此图像目录的颜色管理。 总的来说，最好选择 **[!UICONTROL Adobe RGB]** 或 **[!UICONTROL sRGB]**，而不是特定设备的配置文件（如监视器配置文件）。 **[!UICONTROL sRGB]** 在为web或移动设备准备图像时，建议使用此参数，因为它定义了用于查看web上图像的标准显示器的颜色空间。 **[!UICONTROL sRGB]** 在处理来自消费者级别的数码相机的图像时，也是一个不错的选择，因为大多数这些相机都使用sRGB作为其默认颜色空间。<br>另请参阅 [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) 参数。 |
| **[!UICONTROL 颜色转换渲染意图]** | **[!UICONTROL 知觉]**  — 旨在保持颜色之间的视觉关系，使人眼认为它是自然的，即使颜色价值本身可能会改变。 此意图适用于具有大量色域外颜色的照片图像。 此设置是日本印刷行业的标准渲染意图。 |
|  | **[!UICONTROL 相对比色]**  — 将源颜色空间的极端高亮与目标颜色空间的极端高亮进行比较，并相应地移动所有颜色。 色域外颜色被移动到目标色彩空间中最接近的可再现颜色。 相对比色在图像中保留的原始颜色多于“感知”。 此设置是在北美和欧洲打印的标准渲染意图。 |
|  | **[!UICONTROL 饱和度]**  — 尝试在图像中生成生动的颜色，但牺牲了颜色的准确性。 此渲染意图适用于图形或图表等商业图形，其中明亮的饱和颜色比颜色之间的确切关系更为重要。 |
|  | **[!UICONTROL 绝对比色]**  — 保留位于目标色域内的颜色不变。 超出色域的颜色会被剪切。 不会将颜色缩放到目标白点。 此目的旨在以保持颜色之间关系为代价来保持颜色准确性，并且适于校样以模拟特定设备的输出。 此意图可用于预览纸张颜色对打印颜色的影响。 |

## 在将资产公开之前对其进行测试 {#test-assets-before-making-public}

安全测试可帮助您定义安全测试环境，并基于一组可配置的IP地址和范围构建强大的企业对企业解决方案。 此功能允许您将AdobeDynamic Media部署与内容管理和业务系统的架构相匹配。

通过安全测试，您可以预览包含未发布内容的网站的暂存版本。

如果需要，请创建暂存环境，而不是公开提供资产，原因如下：

* 在公共启动之前预览网站（暂存网站）。
* 提供需要受限访问的资产，例如在B2B Web应用程序中显示价格的eCatalog。
* 将防火墙后的资产用作产品信息管理系统、客户服务应用程序、培训站点等的一部分。

>[!NOTE]
>
>安全测试不影响对Adobe Dynamic Media Classic的访问。 Adobe Dynamic Media Classic安全性保持一致，需要通常的凭据才能访问Adobe Dynamic Media Classic和相关web服务。

### 安全测试的工作原理 {#how-test-assets-works}

大多数公司都在防火墙的后面运行互联网。 通过某些路由（通常通过有限范围的公共IP地址）可以访问Internet。

从您的公司网络中，您可以使用诸如 [https://www.whatismyip.com](https://www.whatismyip.com/) 或向您的公司IT组织请求此信息。

通过安全测试，AdobeDynamic Media为暂存环境或内部应用程序建立专用的图像服务器。 对此服务器的任何请求都会检查源IP地址。 如果传入的请求不在批准的IP地址列表中，则返回失败响应。 AdobeDynamic Media公司管理员为其公司的安全测试环境配置已批准的IP地址列表。

由于必须确认原始请求的位置，因此安全测试服务的流量不会通过内容分发网络(如公共Dynamic Media图像服务器流量)路由。 与公共的Dynamic Media图像服务器相比，对安全测试服务的请求的滞后时间略高。

未发布的资产可立即从安全测试服务中获取，而无需发布。 这样，您就可以在将资产发布到其面向公众的图像服务器之前，运行预览。

>[!NOTE]
>
>安全测试服务使用配置了内部发布上下文的目录服务器。 因此，如果您的公司配置为发布到安全测试，则AdobeDynamic Media中任何上传的资产都会立即在安全测试服务上可用。 无论资产是否标记为上传后发布，此功能都为true。

安全测试服务当前支持以下资产类型和功能：

* 图像.
* 小插图（渲染服务器请求）。
* 呈现服务器请求（支持，但必须由客户明确请求）。
* 集，包括图像集、eCatalog、渲染集和媒体集。
* 标准AdobeDynamic Media富媒体查看器。
* AdobeDynamic Media OnDemand JSP页。
* 静态内容，如PDF文件和逐步提供的视频。
* HTTP视频流。
* 渐进式视频流。

当前不支持以下资产类型和功能：

* Adobe Dynamic Media Classic信息或eCatalog搜索
* RTMP视频流
* Web-to-print
* UGC（用户生成的内容）服务

>[!IMPORTANT]
>
>对AdobeDynamic Media中新的或现有UGC矢量图像资产的支持于2021年9月30日终止。

### 测试安全测试服务 {#test-secure-testing-service}

要确保安全测试服务按预期工作，请执行以下操作：

#### 准备帐户

1. 请联系Adobe客户关怀团队，要求他们在您的帐户中启用安全测试。
1. 在Adobe Experience Manager中，选择 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL Dynamic Media发布设置]**.
1. 在“图像服务器”页面上的 **[!UICONTROL 发布上下文]** 下拉列表中，选择 **[!UICONTROL 测试图像提供]**.
1. 选择 **[!UICONTROL 安全性]** 选项卡。
1. 对于 **[!UICONTROL 客户端地址]** 过滤器，选择 **[!UICONTROL 添加]**.
1. 在 **[!UICONTROL IP地址]** 字段，键入IP地址。
1. 在 **[!UICONTROL 蒙版]** 字段中，键入网络掩码。

   >[!NOTE]
   >
   >如果添加多个IP地址和网络掩码，则它实际上允许 *全部* IP地址进行资产调用，所有这些IP地址都会显示。

1. 执行下列操作之一：

   * 要添加更多IP地址，请重复前三步。
   * 继续下一步。

1. 在“图像服务器”页面的右上角，选择 **[!UICONTROL 保存]**.
1. 将所需的图像上传到您的AdobeDynamic Media帐户。

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. 确保某些图像被标记为要发布，而其他图像被取消标记，然后提交发布作业。

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. 通过转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL Dynamic Media常规设置]**.
1. 在 **[!UICONTROL 服务器]** 页面，在 **[!UICONTROL 已发布的服务器名称]**.

如果服务器名称缺失或指向服务器的URL不起作用，请联系Adobe关怀。

#### 准备网站变体

您需要链接已发布和未发布资产的网站的两个变体：

* 公共版本 — 使用传统的AdobeDynamic Media URL语法来关联资产。
* 测试版本 — 使用相同语法但具有安全测试网站名称的资产链接。

#### 运行测试

执行以下测试：

1. 检查资产在公司网络中是否可见。

   在由先前定义的IP地址范围标识的公司网络中，网站的暂存版本显示所有图像，无论是否标记为发布。 因此，在预览批准或产品发布之前，您无需意外地使图像可用，即可进行测试。

   确认网站的公共版本显示的资产与以前使用AdobeDynamic Media时一样。

1. 从公司网络外部，验证未发布的资产（即未标记为发布）是否受到第三方访问的保护。

   从外部访问您的网络（例如从家庭计算机或通过4G/5G连接），然后验证网站的公共版本是否显示所有已发布的资产，但不显示任何未发布内容。

   确认暂存版本不显示任何资产，因为您正从未批准的IP地址访问安全测试服务。



