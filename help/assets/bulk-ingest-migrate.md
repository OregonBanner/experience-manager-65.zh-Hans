---
title: 安装用于批量资产迁移的功能包18912
description: 功能包18912允许您通过FTP批量摄取资产，或将资产从Dynamic Media Classic迁移到AEM上的Dynamic Media。 此可选功能包可从Adobe支持中获取。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: 资产管理
role: Business Practitioner, Administrator
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# 安装批量资产迁移功能包18912{#installing-feature-pack-for-bulk-asset-migration}

功能包18912的安装是&#x200B;*可选*。

功能包18912允许您通过FTP将资产直接批量摄取到AEM上的Dynamic Media - Scene7模式，或将资产从Dynamic Media Classic迁移到AEM上的Dynamic Media - Scene7模式。 该功能包位于[Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)。

>[!NOTE]
>
>虽然您可以使用功能包自行将资产从Dynamic Media Classic批量迁移到Dynamic Media — 在AEM中为Scene 7模式或使用Dynamic Media Classic中的FTP功能批量迁移资产，但由于涉及的复杂性，Adobe不建议使用&#x200B;*not*&#x200B;此方法。
>
>因此，通过[Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)完成迁移后，迁移功能包（例如此功能包）仅&#x200B;*作为迁移项目的一部分受支持。*

在安装该功能包之前，必须先创建服务用户并提供该信息以Adobe支持。

另请参阅[配置Dynamic Media - Scene7模式](/help/assets/config-dms7.md)。

**安装用于批量资产迁移的功能包18912**

1. 在AEM实例中，导航至&#x200B;**[!UICONTROL 工具>安全>用户]**，然后选择&#x200B;**[!UICONTROL 创建用户]**。 此服务用户必须具有&#x200B;*读/写*&#x200B;权限，即`/content/dam.`
1. 在&#x200B;**[!UICONTROL ID]**&#x200B;和&#x200B;**[!UICONTROL Password]**&#x200B;字段中，输入用户名和密码；例如， **FTP用户**。 此名称以创建资产的用户身份显示在时间轴中。 从FTP上传资产后，当资产上传到FTP服务器并推送到AEM时，会考虑创建该资产。
1. 请联系[Adobe企业客户关怀以获取Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support) ，以请求访问功能包18912以进行下载。 在联系支持人员时，您可能需要以下信息：

   * Author实例的服务器IP地址，包括端口号（默认情况下，端口号为4502）。
   * AEM服务用户用户名和密码。

1. Adobe企业客户关怀团队为您提供FTP凭据和功能包18912的访问权限。
1. 收到功能包18912后，请安装它。

   请参阅[如何使用包](/help/sites-administering/package-manager.md) ，以了解有关在AEM中使用Software Distribution和包的详细信息。
