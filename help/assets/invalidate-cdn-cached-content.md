---
title: 使CDN缓存内容无效
description: 使您的CDN（内容交付网络）缓存内容失效后，您可以快速更新由Dynamic media交付的资产，而不是等待缓存过期。
uuid: 0fd88e31-9745-4c98-a245-9f5d0766cad4
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e6c9b50b-c27c-48bf-b3c0-9994e7bf6d7e
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 使CDN缓存内容无效 {#invalidating-your-cdn-cached-content}

CDN会缓存Dynamic Media资源，以便快速交付。 但是，当您对资产进行更新时，您可能希望这些更改立即生效。 使您的CDN（内容交付网络）缓存内容失效后，您可以快速更新由Dynamic media交付的资产，而不是等待缓存过期。

另请参 [阅Dynamic Media Classic(Scene7)中的缓存概述](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)。

**要使CDN缓存内容无效，请执行以下操作：**

1. 登录到Dynamic Media Classic(Scene7)帐户：

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   您的凭据和登录是在配置时由Adobe提供的。 如果您没有此信息，请与技术支持联系。

1. 单击“ **[!UICONTROL 设置”>“应用程序设置”>“常规设置”]**。
1. 在“应用程序常规设置”页面的“服务器”组标题下，找到“ **[!UICONTROL CDN失效模板]** ”文本框。

1. 指定用于使CDN（内容交付网络）缓存失效的模板。

   例如，假定您输入引用的图像URL（包括图像预设或修饰符） `<ID>`，而不是像以下示例中所示的特定图像ID:

   `https://server.com/is/image/Company/<ID>?$product$`

   如果模板仅包 `<ID>`含，则Dynamic Media会填充其中的 `https://<server>/is/image``<server>` “发布服务器名称”（在“常规设置”中定义），而&lt;ID>是选定要失效的资产。

1. 在页面的右下角，单击“关 **[!UICONTROL 闭”]**。
1. 在Dynamic Media Classic(Scene7)UI中，选择一个或多个资源，然后单击“文 **[!UICONTROL 件”>“使CDN失效]**”。 您将看到一个列表，其中包含从您创建的模板和您选择的资产生成的一个或多个URL。 它使用“应用程序常规设置”下“已发布的服务器名称”下列出的服务器URL。

   例如，在上一步中设置了CDN失效模板后，假定您选择了一个名为的图像资产图像 `Backpack_B`。 单击“文 **[!UICONTROL 件”>“使CDN失效]** ”后，将在CDN失效用户界面中生成以下URL:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 在URL列表框中，单击“继 **[!UICONTROL 续]** ”以清除每个特定URL的缓存。 请注意，您可以编辑URL，也可以通过键入URL或将其粘贴到URL列表框中来添加URL;您无需预先设置CDN失效模板。

   单击“继 **[!UICONTROL 续]**”后，将显示一个指示器，用于估算清除缓存所需的时间。

   如果您选择了多个资产，然后单击“ **[!UICONTROL 文件”>“使CDN失效]**”，则每个资产都会在保存的模板 **[!UICONTROL URL中引用]**。 因此，您可以定义引用网站上引用的每个URL图像预设（如产品详细信息、搜索结果等）的 **** CDN失效模板。 然后，当您从缓存中选择一个或多个要失效的图像时，URL会自动填充该界面。

   >[!NOTE]
   >
   >当您选择资源，然后单击“ **[!UICONTROL 文件”>“使CDN无效]**”时，Dynamic media会使用失效的CDN模板从内容交付网络(CDN)自动创建失效的URL。 如果“ **[!UICONTROL CDN Invalidate模板]** ”文本框中没有任何内容，则会显示空白URL列表。 CDN上的缓存不基于资产；它基于URL。 因此，必须了解您网站上的完整URL。 确定这些URL后，可以在步骤的前面将其添加 **[!UICONTROL 到“Invalidate CDN模板]** ”文本框中。 然后，您可以选择这些资产，并在一个步骤中使URL失效。
   >
   >另一种方法是将完整的URL添加到“ **[!UICONTROL Invalidate CDN]** ”列表。 如果遵循此方法，则不必在Dynamic Media Classic中选择资源，然后再转到“文件” **[!UICONTROL >“使CDN失效]** ”选项。

