---
title: 安装功能包18912以批量迁移资产
description: 功能包18912允许您通过FTP批量摄取资源，或将资源从Dynamic Media Classic迁移到AEM上的Dynamic Media。 此可选功能包可从Adobe支持获得。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Asset Management
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# 正在安装功能包18912以进行批量资源迁移{#installing-feature-pack-for-bulk-asset-migration}

功能包18912的安装是&#x200B;*可选*。

功能包18912允许您通过FTP将资产直接批量收录到Dynamic Media - AEM上的Scene7模式，或将资产从Dynamic Media Classic迁移到Dynamic Media - AEM的Scene7模式。 功能包可从[Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)获得。

>[!NOTE]
>
>虽然您可以使用功能包自行将资产从Dynamic Media Classic批量迁移到Dynamic Media — 在AEM中使用Scene 7模式，或使用Dynamic Media Classic中的FTP功能批量迁移资产，但Adobe不&#x200B;*不*&#x200B;建议使用此方法，因为涉及的复杂性。
>
>因此，当通过[Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)完成迁移时，迁移功能包（如此）仅作为迁移项目的一部分受支持&#x200B;**。

在安装功能包之前，必须首先创建服务用户并向Adobe支持提供该信息。

另请参阅[配置Dynamic Media - Scene7模式](/help/assets/config-dms7.md)。

**安装功能包18912以进行批量资源迁移**

1. 在您的AEM实例中，导航到&#x200B;**[!UICONTROL 工具>安全>用户]**&#x200B;并选择&#x200B;**[!UICONTROL 创建用户]**。 此服务用户必须具有&#x200B;*对`/content/dam.`的读/写*&#x200B;权限
1. 在&#x200B;**[!UICONTROL ID]**&#x200B;和&#x200B;**[!UICONTROL 密码]**&#x200B;字段中，输入用户名和密码；例如，**FTP用户**。 此名称以创建资产的用户身份显示在时间轴中。 当资产从FTP上传时，当资产上传到FTP服务器并推送到AEM时，会视为已创建资产。
1. 请联系[Adobe企业客户关怀部门以获取Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support)，请求访问功能包18912以进行下载。 在联系支持人员时，您可能需要以下信息：

   * 您的作者实例的服务器IP地址，包括端口号（默认情况下，端口号为4502）。
   * AEM服务用户的用户名和密码。

1. Adobe Enterprise Customer Care for AEM为您提供FTP凭据和对功能包18912的访问。
1. 收到功能包18912时，请安装它。

   有关在AEM中使用软件分发和软件包的更多信息，请参阅[如何使用软件包](/help/sites-administering/package-manager.md)。
