---
title: 智能成像
description: 智能成像利用每个用户的独特查看特性自动提供针对其体验优化的正确图像，从而提高性能和参与度。
uuid: c11e52ba-8d64-4dc5-b30a-fc10c2b704e5
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 智能成像 {#smart-imaging}

## 什么是智能成像？ {#what-is-smart-imaging}

智能成像利用每个用户的独特查看特性自动提供针对其体验优化的正确图像，从而提高性能和参与度。 智能成像可以与现有图像预设配合使用，并在传送的最后一毫秒使用智能功能根据浏览器或网络连接速度进一步减小图像文件大小。

与一流的高级CDN服务完全集成后，智能成像可带来更高的性能提升。 此服务在服务器、网络和对等点之间找到最佳的因特网路由，这些点的延迟和／或数据包丢失率都低于因特网上的默认路由。

## 智能成像有哪些主要优势？ {#what-are-the-key-benefits-of-smart-imaging}

智能成像可根据用户特征自动优化图像文件大小，从而提供更好的图像交付性能。 由于图像占页面加载时间的大部分，因此性能改进可能会对业务KPI产生深远影响，如更高的转化率、网站停留时间、较低的网站跳出率等。 Adobe比较了不同文件格式、浏览器和质量(QLT)设置下默认图像传送与智能成像的性能。 总的来说，根据现有图像预设设置和特定的最终用户特性，您可以预期22-47%的性能改进。

![image2017-11-14_133226](assets/image2017-11-14_133226.png)

## 是否存在与智能成像相关的许可成本？ {#are-there-any-licensing-costs-associated-with-smart-imaging}

否. 智能成像包含在您现有的Dynamic Media Classic(Scene7)或Dynamic media许可证中。 利用此新功能无需额外费用。

## 智能成像的工作原理是什么？ {#how-does-smart-imaging-work}

当消费者第一次请求图像时，我们会检查用户特征并基于浏览器转换为适当的图像格式。 此外，我们还同时创建所有格式转换，然后在CDN中缓存这些转换。 当不同浏览器上的用户随后请求该图像时，会直接从CDN缓存自动提供正确的图像格式。 这些格式转换以无损的方式进行，不会降低视觉保真度。 智能成像根据浏览器功能自动将图像转换为不同格式，如下所示：

* 对于支持WebP格式的浏览器（如Chrome、Android和Opera），自动转换为无损的WebP。
* 对于支持JPEGXR格式的浏览器（如Internet Explorer 9+），自动转换为无损的JPEGXR。
* 对于支持JPEG2000格式的浏览器（如Safari），自动转换为无损的JPEG2000。
* 对于不支持这些格式的浏览器，将提供最初请求的图像格式。

## 支持哪些图像格式？ {#what-image-formats-are-supported}

智能成像支持以下图像格式：

* RGB JPEG
* RGB PNG
* RGB TIFF
* CMYK JPEG
* CMYK TIFF

## 智能成像如何处理我们现有的已使用图像预设？ {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

智能成像可以与现有图像预设配合使用，并且几乎可以观察所有图像设置，如大小、质量、锐化等。 将更改的是图像格式，或者，在网络连接速度较慢的情况下，质量设置。 对于格式转换，我们会根据图像预设设置的定义保持完整的视觉保真度，但文件会更小。

例如，假定图像预设的大小为JPEG格式，大小为500x500,quality=85,USM锐化=0.1,1,5。 当我们检测到用户在Chrome浏览器上时，图像将转换为无损的WebP格式，大小为500x500,quality=85,USM锐化=0.1,1,5。

## 我是否必须更改任何URL、图像预设或在我的网站上部署任何新代码才能进行智能成像？ {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

否. 智能成像可与您的现有图像URL和图像预设无缝协作。 此外，智能成像不要求您在网站上添加任何代码来检测不同的用户特征（浏览器、带宽、设备等）。 所有这一切都由Adobe自动处理。

唯一需要的更改是更新“生 **[!UICONTROL 存时间]** (TTL)”设置。 此设置定义CDN缓存资源的时长。 为最大限度地提高智能成像的性能，Adobe建议将TTL设置为24小时或更长。 要更改此设置：

* 如果您使用的是Dynamic Media Classic，请点按设置>应 **[!UICONTROL 用程序设置>发布设置>图像服务器]**。 将“默 **[!UICONTROL 认客户端缓存时间”设置为“实时]** ”值24或更长。

* 如果您使用的是Dynamic Media，请按照说明配置Dynamic Media图 [像设置](config-dynamic.md)**** ，将Expiration值设置为24小时或更长。

>[!NOTE]
>
>如果设置TTL &lt;= 1小时，则智能成像不起作用。

## 智能成像是否可以与HTTPS一起使用？ HTTP/2如何？ {#does-smart-imaging-working-with-https-how-about-http}

智能成像可处理通过HTTP或HTTPS传送的图像。 此外，它还适用于HTTP/2。

## 我是否有资格使用智能成像？ {#am-i-eligible-to-use-smart-imaging}

要使用智能成像，您公司的AEM帐户上的Dynamic Media Classic或Dynamic Media必须满足以下要求：

* 将Adobe捆绑的CDN（内容交付网络）作为许可的一部分。
* 使用专用域(即或 `images.company.com` ), `mycompany.scene7.com`而不是通用域(即、、、 `s7d1.scene7.com`或 `s7d2.scene7.com``s7d13.scene7.com`)。

   要查找您的域，请登录您的公司帐户或帐户。

   点按 **[!UICONTROL 设置>应用程序设置>常规设置]**。 查找标有“已发布服务 **[!UICONTROL 器名称”的字段]**。 如果您当前使用的是通用域，则可以请求移至您自己的自定义域作为此过渡的一部分。

* 请勿请求CMYK JPEG图像。 作为处理的一部分，智能成像将CMYK JPEG图像转换为RGB。 如果需要获取CMYK JPEG图像，则无法使用智能成像。

## 为我的帐户启用智能成像的过程是什么？ {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

您必须发起使用智能成像的请求；它不会自动启用。

1. 发起技术支持请求(电子邮件：s7support@adobe.com)。
1. 在您的支持请求中提供以下信息：

   1. 主要联系人姓名、电子邮件、电话。
   1. 要启用智能成像的所有域（即images.company.com或mycompany.scene7.com）。

      要查找您的域，请登录您的公司帐户或帐户。

      单击“ **[!UICONTROL 设置”>“应用程序设置”>“常规设置”]**。

      查找标有“已发布服务 **[!UICONTROL 器名称”的字段]**。
   1. 验证您是否正通过Adobe使用CDN，而不是以直接关系进行管理。
   1. 验证您使用的是专用域（如或）, `images.company.com` 而 `mycompany.scene7.com`不是通用域（如、、）) `s7d1.scene7.com``s7d2.scene7.com``s7d13.scene7.com`。

      要查找您的域，请登录您的公司帐户或帐户。

      单击“ **[!UICONTROL 设置”>“应用程序设置”>“常规设置”]**。

      查找标有“已发布服务 **[!UICONTROL 器名称”的字段]**。 如果您当前使用的是通用的Dynamic Media Classic域，则可以请求移动到您自己的自定义域作为此过渡的一部分。
   1. 指示您是否也需要它通过HTTP/2运行

1. 技术支持将根据请求的提交顺序将您添加到智能图像处理客户等待列表。
1. 当Adobe准备好处理您的请求时，支持部门将与您联系以协调和设置目标日期。
1. 可选：在Adobe将新功能推向生产之前，您可以选择在暂存中测试智能成像。
1. 完成后，支持会通知您。
1. 为最大限度地提高智能成像的性能，Adobe建议将“生存时间(TTL)”设置为24小时或更长。 TTL定义CDN缓存资源的时长。 要更改此设置：

   1. 如果您使用Dynamic Media Classic，请单击“设置”>“应 **[!UICONTROL 用程序设置”>“发布设置”>“图像服务器”]**。 将“默 **[!UICONTROL 认客户端缓存时间”设置为“实时]** ”值24或更长。
   1. 如果您使用Dynamic Media，请按照以 [下说明操作](config-dynamic.md)。 将“过 **[!UICONTROL 期]** ”值设置为24小时或更长。

## 我何时可以指望我的帐户启用智能成像？ {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

请求将按技术支持部门收到请求的顺序进行处理，并根据等待列表进行处理。

>[!NOTE]
可能存在较长的提前期，因为启用智能成像涉及清除缓存。 因此，在任何给定时间都只能处理少数客户过渡。

## 切换到使用智能成像有哪些风险？ {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

向智能成像的过渡会清除CDN中的缓存，因为它涉及在AEM上切换到Dynamic Media Classic或Dynamic Media的新配置。

在初始过渡期间，未缓存的图像会直接点击Adobe的源服务器，直到重新构建缓存。 因此，Adobe计划一次处理几个客户过渡，以便在从我们的来源提取请求时保持可接受的性能。 对于大多数客户，在约1到2天内在CDN中重新完全建立缓存。

## 如何验证智能成像是否按预期工作？  {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 在您的帐户配置了智能成像后，请在浏览器上加载Dynamic Media Classic(S7)/Dynamic media图像URL。
1. 在浏览器中单击“查看”>“开发 **[!UICONTROL 人员”>“开发人员工具]** ”，打开Chrome开发人员窗格。 或选择您选择的任何浏览器开发人员工具。

1. 确保在开发人员工具打开时禁用缓存。

   1. 在Windows上，导航到开发人员工具窗格中的设置，然后选中“禁用缓存( **[!UICONTROL 当devtools处于打开状态时)”复选框]** 。
   1. 在Mac上，在开发人员窗格的“网络”选项卡 **[!UICONTROL 下]** ，选择 **[!UICONTROL 禁用缓存]** 。

1. 在初始请求时，图像将不会优化。 通常，如果优化的图像不在CDN缓存中，则返回该图像大约需要15分钟。
1. 观察内容类型将转换为相应的格式。 以下屏幕截图显示了Chrome上将动态转换为WebP的PNG图像。
1. 在不同的浏览器和用户条件上重复此测试。

>[!NOTE]
并非所有图像都已转换。 智能成像决定是否需要转换以提高性能。 在某些情况下，如果没有预期的性能增益，则不会转换图像。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

