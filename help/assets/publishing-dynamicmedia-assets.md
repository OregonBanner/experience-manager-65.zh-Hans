---
title: 发布 Dynamic Media 资产
description: 如何发布Dynamic Media资产
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
role: Business Practitioner, Administrator
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: 发布
source-git-commit: 1349d9929fc64ad46fc91f0d189bab54cca9de81
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 12%

---

# 发布 Dynamic Media 资产 {#publishing-dynamic-media-assets}

要发布Dynamic Media资产，请选择已上传的资产，然后点按&#x200B;**[!UICONTROL 发布]**&#x200B;或&#x200B;**[!UICONTROL 快速发布]**。 发布Dynamic Media资产后，您便可以通过URL或在页面上嵌入代码，将这些资产包含在网页中。

您还可以立即发布上传的资产，无需任何用户干预。 请参阅[配置Dynamic Media - Scene7模式](config-dms7.md)。
或者，您也可以使用文件夹级别的**[!UICONTROL 选择性发布]** ，有选择地将资产发布到相互排斥的Dynamic Media或Adobe Experience Manager。 请参阅[使用Dynamic Media中的“选择性发布”](/help/assets/selective-publishing.md)。

在&#x200B;**[!UICONTROL 卡片视图]**&#x200B;中，资产名称的正下方以及日期和时间的左侧会显示一个小地球图标，指示资产已发布。 在&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，**[!UICONTROL 已发布]**&#x200B;列显示已发布的资产和未发布的资产。

>[!NOTE]
>
>如果资产已发布，请使用Experience Manager将资产移动到其他文件夹，然后从新位置重新发布。 原始发布的资产位置以及新重新发布的资产仍可用。 但是，原始已发布的资产将“丢失”到Experience Manager，无法取消发布。 因此，作为最佳实践，请先取消发布资产，然后再将资产移动到其他文件夹。

如果您打算在对视频资产进行编码后立即发布这些资产，请确保编码已完成。 在对视频进行编码时，系统会告知您视频处理工作流正在进行中。 视频编码完成后，您可以预览视频演绎版。 此时，您便可以安全地发布视频，而不会出现任何发布错误。

另请参阅[将 URL 关联到您的 Web 应用程序](linking-urls-to-yourwebapplication.md)。

另请参阅[在网页上嵌入Dynamic Media视频或图像查看器](embed-code.md)

>[!NOTE]
>
>* 要使用 URL，必须先发布资产。如果资产未发布，则复制URL并将其粘贴到Web浏览器中不起作用。
>* 必须激活并发布图像预设和查看器预设才能进行实时交付。

>



有关发布集或资产的详细信息，请参阅[发布资产](manage-assets.md)。

## HTTP/2交付Dynamic Media资产{#http-delivery-of-dynamic-media-assets}

Experience Manager现在支持通过HTTP/2交付所有Dynamic Media内容（图像和视频）。 即，图像或视频的已发布URL或嵌入代码可与接受托管资产的任何应用程序集成。 然后，将通过HTTP/2协议来交付已发布的资产。 这种交付方法改进了浏览器和服务器通信的方式，从而可以缩短所有Dynamic Media资产的响应和加载时间。

要了解更多信息，请参阅[HTTP/2内容交付常见问题解答](/help/sites-administering/scene7-http2faq.md)。
