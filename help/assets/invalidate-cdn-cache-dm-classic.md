---
title: 通过Dynamic Media Classic使CDN缓存失效
description: 使CDN(内容投放网络)缓存内容失效后，您可以快速更新Dynamic Media Classic交付的资源，而不必等待缓存过期。
uuid: 0fd88e31-9745-4c98-a245-9f5d0766cad4
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e6c9b50b-c27c-48bf-b3c0-9994e7bf6d7e
translation-type: tm+mt
source-git-commit: 54645149dc4968c1c4f85eedb5ce4d71f80c3b64
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 24%

---


# 通过Dynamic Media Classic使CDN缓存失效 {#invalidating-your-cdn-cached-content}

CDN会缓存Dynamic Media资源以快速投放。 但是，当您对资产进行更新时，您可能希望这些更改立即生效。 使CDN(内容投放网络)缓存内容失效后，您可以快速更新Dynamic Media交付的资源，而无需等待缓存过期。

>[!IMPORTANT]
>
>以下步骤仅适用于AEM 6.5、Service Pack 5(AEM 6.5.5)或更早版本中的Dynamic Media。<br>如果您在AEM 6.5、Service Pack 6(AEM 6.5.6)或更高版本中使用Dynamic Media，请按照通过Dynamic Media使 [CDN缓存失效中的步骤操作。](/help/assets/invalidate-cdn-cache-dynamic-media.md)

另请参 [阅Dynamic Media Classic中的缓存概述(Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)。

**要通过Dynamic Media Classic使CDN缓存失效，请执行以下操作：**

1. 执行下列操作之一：

   * 在您的Web浏览器中，登录您的Dynamic Media Classic帐户：

      [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

      您的凭据和登录是在设置时由Adobe提供的。 如果您没有此信息，请与技术支持联系。

   * 打开Dynamic Media Classic应用程序，然后登录您的帐户。

1. 在页面的右上角附近，点按设置>应 **[!UICONTROL 用程序设置>常规设置。]**
1. 在“应用程序常规设置”页的“服务器”组标题下，找到“CDN **[!UICONTROL 失效模板]** ”文本框。

1. 指定用于使CDN(内容投放网络)缓存失效的模板。

   例如，假定您输入引用的图像URL（包括图像预设或修饰符）, `<ID>`而不是像以下示例中所示的特定图像ID:

   `https://server.com/is/image/Company/<ID>?$product$`

   如果模板仅包 `<ID>`含，则Dynamic Media将填 `https://<server>/is/image` 充其中 `<server>` 在常规设置中定义的发布服务器名称，而&lt;ID>是选定要失效的资产。

1. In the lower-right corner of the page, click **[!UICONTROL Close.]**
1. 在Dynamic Media Classic(Scene7)UI中，选择一个或多个资源，然后单击“文件”>“ **[!UICONTROL 使CDN失效”。]** 您将看到一个列表，其中包含从您创建的模板和您选择的资产中生成的一个或多个URL。 它使用“应用程序常规设置”下“已发布服务器名称”下列出的服务器URL。

   例如，在上一步中设置了CDN失效模板后，假定您选择了一个名为的图像资产图像 `Backpack_B`。 单击“文 **[!UICONTROL 件”>“使CDN失效]** ”后，将在CDN失效用户界面中生成以下URL:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 在URL列表框中，单 **[!UICONTROL 击]** “继续”以清除每个特定URL的缓存。 请注意，您可以编辑URL，也可以通过键入URL或将其粘贴到URL列表框中来添加URL;您无需预先设置CDN Invalidate模板。

   单击“继 **[!UICONTROL 续]**”后，将显示一个指示器，估计清除缓存所需的时间。

   如果您选择了多个资产，请单击&#x200B;**[!UICONTROL 文件 > 无效 CDN]**，则每个资产都会在保存的&#x200B;**[!UICONTROL 模板 URL 中引用。]**&#x200B;因此，您可以定义 **[!UICONTROL CDN 无效模板]**，以引用网站上引用的每个 URL 图像预设（如产品详细信息、搜索结果等）。然后，当您从缓存中选择一个或多个要失效的图像时，URL 会自动填充该界面。

   >[!NOTE]
   >
   >当您选择资产，然后单击&#x200B;**[!UICONTROL 文件 > 无效 CDN]** 时，Dynamic Media 会使用无效 CDN 模板从内容交付网络 (CDN) 自动创建 URL。如果 **[!UICONTROL CDN 无效模板]**&#x200B;文本框中没有任何内容，则会显示空白 URL 列表。CDN 上的缓存不是基于资产，而是基于 URL。因此，必须了解您网站上的完整 URL。确定这些 URL 后，可以将其添加到步骤前面的&#x200B;**[!UICONTROL 无效 CDN 模板]**。然后，您可以选择这些资产，并在一个步骤中使 URL 失效。
   >
   >另一种方法是将完整的URL添加 **[!UICONTROL 到Invalidate CDN]** 列表。 如果采用此方法，则不必在Dynamic Media Classic中选择资源，然后再转到“文件”>“使 **[!UICONTROL CDN失效]** ”选项。

