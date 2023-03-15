---
title: 为图像服务器配置Dynamic Media发布设置
description: 了解如何在Dynamic Media中设置发布。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: c86e79c4-e887-4ee3-bb54-eeffb34a33c2
source-git-commit: 8561eb8b4b5164188ebf387c8f0344b462b830ec
workflow-type: tm+mt
source-wordcount: '3467'
ht-degree: 4%

---

# 为图像服务器配置Dynamic Media发布设置

只有符合以下条件时，才能配置Dynamic Media发布设置：

* 您正在以Scene7模式运行Dynamic Media。 参见 [在Scene7模式下启用Dynamic Media](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* 您有一个 *现有* **[!UICONTROL Dynamic Media配置]** (in **[!UICONTROL Cloud Services]**)在Adobe Experience Manager 6.5.11或更高版本中。 参见 [在Cloud Services中创建Dynamic Media配置](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* 您是具有管理员权限的Experience Manager系统管理员。

Dynamic Media发布设置旨在供经验丰富的网站开发人员和程序员使用。 AdobeDynamic Media建议更改这些发布设置的用户熟悉AdobeDynamic Media、HTTP协议标准和惯例，以及基本成像技术。

“Dynamic Media发布设置”页面可建立默认设置，以确定如何将资源从AdobeDynamic Media服务器传递到网站或应用程序。 如果未指定设置，则AdobeDynamic Media服务器会根据“Dynamic Media发布设置”页面上配置的默认设置交付资源。

另请参阅 [可选 — 设置和配置Dynamic Media - Scene7模式设置](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) 了解更多可选配置任务。

>[!NOTE]
>
>在Adobe Experience Manager上从Dynamic Media Classic升级到Dynamic Media？ 此 [常规设置](/help/assets/dm-general-settings.md) Dynamic Media中的“页面和发布设置”页面已预填充从您的Dynamic Media Classic帐户中获取的值。 例外情况是 **[!UICONTROL 默认上传选项]** 区域。 这些值已在Experience Manager中。 因此，您对以下内容所做的任何更改 **[!UICONTROL 默认上传选项]**&#x200B;通过Experience Manager用户界面，这五个选项卡中的任何一个都会反映在Dynamic Media中，而不是Dynamic Media Classic中。 所有其他设置和值 [常规设置](/help/assets/dm-general-settings.md) 页面和“发布设置”页面在Dynamic Media Classic和Dynamic MediaExperience Manager时维护。

**要配置Dynamic Media发布设置图像服务器，请执行以下操作：**

1. 在Experience Manager创作模式下，选择Experience Manager徽标以访问全局导航控制台。
1. 在左边栏中，选择工具图标，然后转到 **[!UICONTROL 资产]** > **[!UICONTROL Dynamic Media发布设置]**.
1. 在“图像服务器”页面中，设置图像服务器 — 发布上下文，然后使用五个选项卡配置默认发布设置。

   * [图像服务器](#image-server)
   * [安全性](#security-tab) 选项卡
   * [目录管理](#catalog-management-tab) 选项卡
   * [请求属性](#request-attributes-tab) 选项卡
   * [通用缩略图属性](#common-thumbnail-attributes-tab) 选项卡
   * [颜色管理属性](#color-management-attributes-tab) 选项卡

   ![Dynamic Media发布设置页面](/help/assets/assets-dm/dm-publish-setup.png)
   *Dynamic Media发布设置页面，使用&#x200B;**[!UICONTROL 请求属性]**已选择选项卡。*<br><br>

1. 完成后，在页面的右上角附近，选择 **[!UICONTROL 保存]**.

## 图像服务器 {#image-server}

“图像服务器”页面建立了从图像服务器传送图像的默认设置。 设置分为五个类别

| 发布上下文 | 描述 |
| --- | --- |
| 图像服务 | 指定发布设置的上下文。 |
| 提供测试图像 | 指定用于测试发布设置的上下文。<br>仅对于新的Dynamic Media帐户，默认为 **[!UICONTROL 客户端地址]** 字段设置为 `127.0.0.1` 自动。<br>参见 [在公开资产之前测试资产](#test-assets-before-making-public). |

### “安全”选项卡 {#security-tab}

**[!UICONTROL 客户端地址]**  — 用于指定一个或多个IP地址或IP地址范围。 指定后，将拒绝从未列出的IP地址上的客户端对此图像目录发起的请求。 此规则适用于交付图像和渲染的图像。

![“安全”选项卡&#x200B;](/help/assets/assets-dm/dm-ipallowlist.png)<br>*显示IP“允许”字段的“安全”选项卡。*

### “目录管理”选项卡 {#catalog-management-tab}

**[!UICONTROL 规则集定义文件路径]**  — 指定包含图像目录的规则集定义的文件。

另请参阅 [规则集文件](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) 参数(在Dynamic Media查看器参考指南中)。

>[!NOTE]
>
>如果您的Dynamic Media Classic帐户已 **[!UICONTROL 规则集定义文件路径]** 选定（如下所设置） **[!UICONTROL 设置]** > **[!UICONTROL 应用程序]** > **[!UICONTROL 发布设置]**，下 **[!UICONTROL 目录管理]** 组)，则您的Dynamic MediaExperience Manager帐户将从Dynamic Media Classic中获取文件。 然后，当您打开 **[!UICONTROL Dynamic Media发布设置]** 第一次翻页。

### “请求属性”选项卡 {#request-attributes-tab}

这些设置与图像的默认外观相关。

| 设置 | 描述 |
| --- | --- |
| **[!UICONTROL 回复图像大小限制]** | 必填.<br>仅对于新的Dynamic Media帐户，默认大小限制会自动设置为宽度： `3000` 和高度： `3000` （对于两者） **[!UICONTROL 图像服务]** 和 **[!UICONTROL 测试图像服务]**.<br>指定返回给客户端的最大回复图像宽度和高度。 如果请求导致回复图像的宽度和/或高度大于此设置，则服务器会返回错误。<br>另请参阅 [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 请求混淆模式]** | 如果希望将base64编码应用于有效请求，则启用。<br>另请参阅 [请求模糊处理](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 请求锁定模式]** | 如果希望在请求中包含简单哈希锁，则启用。<br>另请参阅 [Requestlock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 默认请求属性]** |  |
| **[!UICONTROL 默认图像文件后缀]** | 必填.<br>如果路径不包含文件后缀，则附加到目录Path和MaskPath字段值的默认数据文件扩展名。<br>另请参阅 [默认分机](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 默认字体名称]** | 指定在文本图层请求未提供任何字体时使用哪种字体。 如果指定，则它必须是此图像目录的字体映射或默认目录的字体映射中的有效字体名称值。<br>另请参阅 [默认字体](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 默认图像]** | 提供一个默认图像，为响应未找到所请求图像的请求而返回。<br>另请参阅 [默认图像](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) 参数(在Dynamic Media查看器参考指南中)。<br>**注意**：如果您的Dynamic Media Classic帐户已经拥有 **[!UICONTROL 默认图像]** 选定（如下所设置） **[!UICONTROL 设置]** > **[!UICONTROL 应用程序]** > **[!UICONTROL 发布设置]**，下 **[!UICONTROL 默认请求属性]** 组)，则您的Dynamic MediaExperience Manager帐户将从Dynamic Media Classic中获取文件。 然后，当您打开 **[!UICONTROL Dynamic Media发布设置]** 第一次翻页。 |
| **[!UICONTROL 默认图像模式]** | 启用滑块框（右侧的滑块）后， **[!UICONTROL 默认图像]** 将源图像中的每个缺失图层替换为默认图像，然后照常返回复合图像。 禁用滑块框（左侧滑块）后，默认图像将替换整个复合图像，即使缺少的图像只是多个图层中的一个图层也是如此。<br>另请参阅 [默认图像模式](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 默认视图大小]** | 必填.<br>仅对于新的Dynamic Media帐户，默认视图大小会自动设置为宽度： `1280` 和高度： `1280` （对于两者） **[!UICONTROL 图像服务]** 和 **[!UICONTROL 测试图像服务]**.<br>如果请求未明确使用指定视图大小，服务器将限制回复图像不超过此宽度和高度 `wid=`， `hei=`，或 `scl=`.<br>另请参阅 [Defaultpix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 默认缩略图大小]** | 必填.<br>已使用而不是属性 **[!UICONTROL 默认视图大小]** 对于缩略图请求(`req=tmb`)。 如果缩略图请求(`req=tmb`)不会使用显式指定大小 `wid=`， `hei=`，或 `scl=`.<br>另请参阅 [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 默认背景颜色]** | 指定用于填充不包含实际图像数据的回复图像的任意区域的RGB值。<br>另请参阅 [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL JPEG 编码属性]** |  |
| **[!UICONTROL 质量]** | <br>指定JPEG回复图像的默认属性。<br>仅对于新的Dynamic Media帐户， **[!UICONTROL 质量]** 默认值自动设置为 `80` （对于两者） **[!UICONTROL 图像服务]** 和 **[!UICONTROL 测试图像服务]**.<br>此字段在1 - 100的范围内定义。<br>另请参阅 [Jpeg品质](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 色度降采样]** | 启用或禁用JPEG编码器使用的色度缩减像素采样。 |
| **[!UICONTROL 默认重新取样模式]** | 指定用于缩放图像数据的默认重新取样属性和插值属性。使用时机 `resMode` 未在请求中指定。<br>仅对于新的Dynamic Media帐户，默认重新取样模式会自动设置为 `Sharp2` （对于两者） **[!UICONTROL 图像服务]** 和 **[!UICONTROL 测试图像服务]**.<br>另请参阅 [解析模式](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) 参数(在Dynamic Media查看器参考指南中)。 |

### “常用缩略图属性”选项卡 {#common-thumbnail-attributes-tab}

这些设置与缩略图图像的默认外观和对齐有关。

| 设置 | 描述 |
| --- | --- |
| **[!UICONTROL 缩略图的默认背景颜色]** | 指定用于填充不包含实际图像数据的输出缩略图图像的区域的RGB值。 仅用于缩略图请求(`req=tmb`)和时间 **[!UICONTROL 默认缩略图类型]** 设置已设置为 **[!UICONTROL 适合]** 或 **[!UICONTROL 纹理]**.<br>另请参阅 [ThumbbkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 水平对齐方式]** | 指定由指定的回复图像矩形中的缩略图图像的水平对齐方式 `wid=` 和 `hei=` 值。<br>仅用于缩略图请求(`req=tmb`)和时间 **[!UICONTROL 默认缩略图类型]** 设置已设置为 **[!UICONTROL 适合]**.<br>有三种水平对齐方式可供选择： **[!UICONTROL 居中对齐]**， **[!UICONTROL 左对齐]**、和 **[!UICONTROL 右对齐]**.<br>另请参阅 [缩略图](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 垂直对齐方式]** | 指定由指定的回复图像矩形中的缩略图图像的垂直对齐方式 `wid=` 和 `hei=` 值。 仅用于缩略图请求(`req=tmb`)和时间 **[!UICONTROL 默认缩略图类型]** 设置已设置为 **[!UICONTROL 适合]**.<br>有三种垂直对齐方式可供选择： **[!UICONTROL 顶部对齐]**， **[!UICONTROL 居中对齐]**、和 **[!UICONTROL 底部对齐]**.<br>另请参阅 [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 默认缓存生存时间]** | 提供默认的有效期时间间隔（以小时为单位），以防特定的目录记录不包含有效的目录有效期值。设置为 `-1` 标记为永不过期。 <br>另请参阅 [过期](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 默认缩略图类型]** | 提供特定目录记录中不包含有效目录ThumbType值时的缩略图类型默认值。 仅用于缩略图请求(`req=tmb`)。<br>有三种缩略图类型可供选择： **[!UICONTROL 裁切]**， **[!UICONTROL 适合]**、和 **[!UICONTROL 纹理]**.<br>另请参阅 [缩略图类型](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 默认缩略图分辨率]** | 提供特定目录记录中不包含有效目录ThumbRes值时的缩略图对象分辨率默认值。 仅用于缩略图请求(`req=tmb`)，并且当 **[!UICONTROL 默认缩略图类型]** 设置已设置为 **[!UICONTROL 纹理]**.<br>另请参阅 [缩略图](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) 参数(在Dynamic Media查看器参考指南中)。 |

### “颜色管理属性”选项卡 {#color-management-attributes-tab}

这些设置确定用于图像的ICC颜色配置文件。

**颜色转换调色**
颜色转换渲染方法允许覆盖工作配置文件的默认渲染方法，以确定如何调整源颜色。 在以下情况下使用：

1. 默认ICC配置文件之一是颜色转换的目标颜色空间。
1. 输出设备（打印机或显示器）的特点就是此配置文件。
1. 并且，指定的渲染方法对此配置文件有效。

不同的渲染意图使用不同的规则来确定如何调整源颜色。

另请参阅 [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) 参数(在Dynamic Media查看器参考指南中)。

>[!NOTE]
>
>通常，最好对选定的颜色设置使用默认的渲染方法，该设置已经过Adobe测试以符合行业标准。 例如，如果您为北美或欧洲选择颜色设置，则默认的颜色转换渲染方法为 **[!UICONTROL 相对比色]**. 如果您为日本选择了颜色设置，则默认的颜色转换渲染方法为 **[!UICONTROL 可感知]**.

| 设置 | 特征 |
| --- | --- |
| **[!UICONTROL CMYK 默认颜色空间]** | 指定要用作CMYK数据的工作配置文件的ICC颜色配置文件的名称。 如果 **[!UICONTROL 未指定]** 选择，则在涉及CMYK源图像时对此图像目录禁用颜色管理。 所有CMYK工作空间都取决于设备，这意味着它们基于实际的油墨和纸张组合。 CMYK工作空间的Adobe供应基于标准商业印刷条件。<br> 另请参阅 [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 灰度默认色彩空间]** | 指定要用作灰度数据工作配置文件的ICC颜色配置文件的名称。 如果 **[!UICONTROL 未指定]** 选择，则在涉及灰度源图像时对此图像目录禁用颜色管理。<br>另请参阅 [Icc配置文件灰色](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL RGB 默认颜色空间]** | 指定要用作RGB数据的工作配置文件的ICC颜色配置文件的名称。 如果 **[!UICONTROL 未指定]** 选择，则在涉及RGB源图像时对此图像目录禁用颜色管理。 一般来说，最好选择 **[!UICONTROL Adobe RGB]** 或 **[!UICONTROL sRGB]**，而不是特定设备（如监视器配置文件）的配置文件。 **[!UICONTROL sRGB]** 在为Web或移动设备准备图像时，建议使用此选项，因为它定义了用于在Web上查看图像的标准监视器的颜色空间。 **[!UICONTROL sRGB]** 在处理消费者级数码相机的图像时也是一个很好的选择，因为大多数数码相机都使用sRGB作为默认颜色空间。<br>另请参阅 [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) 参数(在Dynamic Media查看器参考指南中)。 |
| **[!UICONTROL 颜色转换调色]** | **[!UICONTROL 可感知]**  — 旨在保持颜色之间的视觉关系，以便人眼认为它是自然的，即使颜色价值本身可能会改变。 此意图适用于具有大量超出色域颜色的照片图像。 该设置是日本印刷业的标准渲染方法。 |
|  | **[!UICONTROL 相对比色]**  — 将源颜色空间的极高亮度和目标颜色空间的极高亮度进行比较，并相应地移动所有颜色。 将色域外颜色移动到目标色彩空间中最接近的可再现颜色。 相对比色在图像中保留的原始颜色比感知颜色多。 此设置是北美和欧洲打印的标准渲染方法。 |
|  | **[!UICONTROL 饱和度]**  — 尝试在图像中生成鲜艳的颜色，而牺牲颜色的准确性。 此渲染方法适用于图形或图表等商业图形，其中明亮饱和颜色比颜色之间的确切关系更重要。 |
|  | **[!UICONTROL 绝对比色]**  — 将落在目标色域内的颜色保持不变。 超出色域的颜色会被剪切。 不执行将颜色缩放到目标白点的操作。 此意图旨在以保持颜色之间的关系为代价来保持颜色的准确性，并且适用于模拟特定设备的输出的校样。 此意图对于预览纸张颜色对打印颜色的影响非常有用。 |

## 在公开资产之前测试资产 {#test-assets-before-making-public}

Secure Testing可帮助您定义安全的测试环境，并根据一组可配置的IP地址和范围构建强大的企业对企业解决方案。 此功能可让您将AdobeDynamic Media部署与内容管理和业务系统的架构相匹配。

通过Secure Testing，您可以预览包含未发布内容的网站暂存版本。

如果需要，请创建暂存环境，而不是公开资产，原因如下：

* 在公开启动之前预览网站（测试网站）。
* 提供需要受限访问的资产，例如在B2B Web应用程序中显示价格的eCatalog。
* 使用防火墙后的资产作为产品信息管理系统、客户服务应用程序、培训网站等的一部分。

>[!NOTE]
>
>安全测试不会影响对Adobe Dynamic Media Classic的访问。 Adobe Dynamic Media Classic安全性将保持一致，并且需要使用常规凭据来访问Adobe Dynamic Media Classic和相关Web服务。

### 安全测试的工作原理 {#how-test-assets-works}

大多数公司都在防火墙后运行互联网。 可以通过特定路由访问Internet，通常是通过有限的公共IP地址范围访问。

通过公司网络，您可以使用以下网站确定公共IP地址 [https://www.whatismyip.com](https://www.whatismyip.com/) 或向您的公司IT部门索取此信息。

通过Secure Testing，AdobeDynamic Media为暂存环境或内部应用程序建立了专用的映像服务器。 对此服务器的任何请求都会检查原始IP地址。 如果传入请求不在已批准的IP地址列表中，则会返回失败响应。 AdobeDynamic Media Company Administrator为公司的Secure Testing环境配置经过批准的IP地址列表。

由于必须确认原始请求的位置，因此Secure Testing服务的流量不会像公共Dynamic Media Image Server流量那样通过内容分发网络进行路由。 向Secure Testing服务发出的请求与向公共Dynamic Media图像服务器发出的请求相比，具有略高的延迟。

未发布的资产可以立即从Secure Testing服务中使用，而无需发布。 通过这种方式，您可以在将资产发布到其面向公众的图像服务器之前运行预览。

>[!NOTE]
>
>Secure Testing Services使用配置了内部发布上下文的目录服务器。 因此，如果贵公司配置为发布到Secure Testing，则在AdobeDynamic Media中上传的任何资源都将立即可在Secure Testing服务中使用。 不论资产是否在上传时标记为发布，此功能都为true。

Secure Testing服务当前支持以下资产类型和功能：

* 图像.
* 晕影（渲染服务器请求）。
* 渲染服务器请求（受支持，但必须由客户明确请求）。
* 集，包括图像集、eCatalog、渲染集和媒体集。
* 标准AdobeDynamic Media富媒体查看器。
* AdobeDynamic Media OnDemand JSP页。
* 静态内容，例如PDF文件和逐步提供的视频。
* HTTP视频流。
* 渐进式视频流。

当前不支持以下资产类型和功能：

* Adobe Dynamic Media Classic信息或eCatalog搜索
* RTMP视频流
* Web打印
* UGC（用户生成的内容）服务

>[!IMPORTANT]
>
>对AdobeDynamic Media中新增或现有UGC矢量图像资源的支持已于2021年9月30日终止。

### 测试Secure Testing service {#test-secure-testing-service}

要确保Secure Testing服务按预期工作，请执行以下操作：

#### 准备帐户

1. 联系Adobe客户关怀部门，要求他们在您的帐户上启用安全测试。
1. 在Adobe Experience Manager中，选择 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL Dynamic Media发布设置]**.
1. 在“图像服务器”页面的 **[!UICONTROL 发布上下文]** 下拉列表，选择 **[!UICONTROL 测试图像服务]**.
1. 选择 **[!UICONTROL 安全性]** 选项卡。
1. 对于 **[!UICONTROL 客户端地址]** 过滤器，选择 **[!UICONTROL 添加]**.
1. 在 **[!UICONTROL IP地址]** 字段，键入IP地址。
1. 在 **[!UICONTROL 蒙版]** 字段，键入网络掩码。

   >[!NOTE]
   >
   >如果添加多个IP地址和网络掩码，它将有效地允许 *所有* 用于发起资产调用的IP地址，这些地址都会显示。

1. 执行下列操作之一：

   * 要添加更多IP地址，请重复前三个步骤。
   * 继续下一步骤。

1. 在“图像服务器”页面的右上角，选择 **[!UICONTROL 保存]**.
1. 将所需的图像上传到您的AdobeDynamic Media帐户。

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. 确保将某些图像标记为发布，将其他图像标记为未标记，然后提交发布作业。

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. 通过转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL Dynamic Media常规设置]**.
1. 在 **[!UICONTROL 服务器]** 页面上，在的右侧查找服务器名称 **[!UICONTROL 已发布的服务器名称]**.

如果Adobe名称缺失或指向服务器的URL不起作用，请联系服务器关怀团队。

#### 准备网站变体

您需要链接已发布和未发布资产的网站的两个变体：

* 公共版本 — 使用传统的AdobeDynamic Media URL语法链接资源。
* 暂存版本 — 使用相同的语法但使用安全测试站点名称链接资产。

#### 运行测试

执行以下测试：

1. 检查资产是否在公司网络中可见。

   从以前定义的IP地址范围标识的公司网络内，网站的暂存版本会显示所有图像，无论是否标记为发布。 因此，您可以在测试时避免在预览批准或产品发布之前意外使图像可用。

   确认您的网站的公共版本显示已发布的资源，就像以前在AdobeDynamic Media时所做的那样。

1. 在公司网络之外，验证未发布的资产（即未标记为发布的资产）是否受到第三方访问的保护。

   从外部访问您的网络（例如，从您的家庭计算机或通过4G/5G连接），然后验证公共版本的网站是否显示所有已发布的资产，但不显示任何未发布的内容。

   确认暂存版本未显示任何资产，因为您正从未批准的IP地址访问Secure Testing服务。
