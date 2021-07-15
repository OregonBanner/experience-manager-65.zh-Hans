---
title: 安装用于批量资产迁移的功能包18912
description: 功能包18912允许您通过FTP批量摄取资产，或将资产从Dynamic Media Classic迁移到Adobe Experience Manager上的Dynamic Media。 此可选功能包可从Adobe支持中获取。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: 资产管理
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: 471f9e99078a1e0af60024d439afd42ae77cba8c
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# 安装用于批量资产迁移的功能包18912{#installing-feature-pack-for-bulk-asset-migration}

功能包18912的安装是&#x200B;*可选*。

功能包18912允许您通过FTP将资产直接批量摄取到Adobe Experience Manager上的Dynamic Media - Scene7模式。 它还允许您在Experience Manager上将资产从Dynamic Media Classic迁移到Dynamic Media - Scene7模式。 该功能包位于[Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)。

>[!IMPORTANT]
>
>您可以在Experience Manager中使用功能包，自行将资产从Dynamic Media Classic批量迁移到Dynamic Media - Scene7模式。 您还可以使用Dynamic Media Classic中的FTP功能批量迁移资产。 但是，Adobe *not*&#x200B;建议您使用以下任一方法，因为涉及的复杂性。
>
>因此，通过[Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)完成迁移后，此迁移功能包仅作为迁移项目的一部分支持&#x200B;**。

在安装该功能包之前，请创建Service用户，并提供该信息以Adobe支持。

另请参阅[配置Dynamic Media - Scene7模式](/help/assets/config-dms7.md)。

**要安装用于批量资产迁移的功能包18912，请执行以下操作：**

1. 在您的Experience Manager实例中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用户]**，然后选择&#x200B;**[!UICONTROL 创建用户]**。 此服务用户必须具有&#x200B;*读/写*&#x200B;权限，即`/content/dam.`
1. 在&#x200B;**[!UICONTROL ID]**&#x200B;和&#x200B;**[!UICONTROL Password]**&#x200B;字段中，输入用户名和密码；例如， **FTP用户**。 此名称以创建资产的用户身份显示在时间轴中。 从FTP上传资产后，当资产上传到FTP服务器并推送到Experience Manager时，会考虑创建该资产。
1. 请联系[Adobe企业客户关怀以获取Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support) ，以请求访问功能包18912以进行下载。 在联系支持人员时，您可能需要以下信息：

   * Author实例的服务器IP地址，包括端口号（默认情况下，端口号为4502）。
   * Experience Manager服务上一步中的用户用户名和密码。

1. Adobe企业客户关怀团队提供FTP凭据和对功能包18912的访问。
1. 收到功能包18912后，请安装它。

   请参阅[如何使用包](/help/sites-administering/package-manager.md) ，以了解有关在Experience Manager中使用软件分发和包的详细信息。
