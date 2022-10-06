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
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

---

# 安装用于批量资产迁移的功能包18912{#installing-feature-pack-for-bulk-asset-migration}

功能包18912的安装是 *可选*.

功能包18912允许您通过FTP将资产直接批量摄取到Adobe Experience Manager上的Dynamic Media - Scene7模式。 它还允许您在Experience Manager上将资产从Dynamic Media Classic迁移到Dynamic Media - Scene7模式。 功能包可从 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>您可以在Experience Manager中使用功能包，自行将资产从Dynamic Media Classic批量迁移到Dynamic Media - Scene7模式。 您还可以使用Dynamic Media Classic中的FTP功能批量迁移资产。 但是，Adobe会 *not* 由于涉及的复杂性，建议您使用以下任一方法。
>
>因此，此迁移功能包为 *仅* 在完成 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

在安装该功能包之前，请创建Service用户，并提供该信息以Adobe支持。

另请参阅[配置 Dynamic Media - Scene7 模式](/help/assets/config-dms7.md).

**要安装用于批量资产迁移的功能包18912，请执行以下操作：**

1. 在您的Experience Manager实例中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 用户]** 选择 **[!UICONTROL 创建用户]**. 此服务用户必须 *读/写* 权限 `/content/dam.`
1. 在 **[!UICONTROL ID]** 和 **[!UICONTROL 密码]** 输入用户名和密码；例如， **FTP用户**. 此名称以创建资产的用户身份显示在时间轴中。 从FTP上传资产后，当资产上传到FTP服务器并推送到Experience Manager时，会考虑创建该资产。
1. 联系人 [Adobe客户支持以Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support) 请求访问功能包18912以进行下载。 在联系支持人员时，您可能需要以下信息：

   * Author实例的服务器IP地址，包括端口号（默认情况下，端口号为4502）。
   * Experience Manager服务上一步中的用户用户名和密码。

1. Adobe客户Experience Manager支持为您提供FTP凭据和功能包18912的访问权限。
1. 收到功能包18912后，请安装它。

   请参阅 [如何使用包](/help/sites-administering/package-manager.md) 有关在Experience Manager中使用Software Distribution和包的更多信息。
