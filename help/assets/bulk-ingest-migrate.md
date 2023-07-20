---
title: 安装功能包18912以批量迁移资产
description: 功能包18912允许您通过FTP批量摄取资源，或在Adobe Experience Manager上将资源从Dynamic Media Classic迁移到Dynamic Media。 Adobe支持部门提供了此可选功能包。
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
source-git-commit: fc148a5f5e0fcaac2980dc73004fa92ac3b91fb3
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

---

# 安装功能包18912以批量迁移资产{#installing-feature-pack-for-bulk-asset-migration}

功能包18912的安装是 *可选*.

功能包18912允许您通过FTP将资产直接批量摄取到Dynamic Media - Adobe Experience Manager上的Scene7模式中。 它还允许您在Experience Manager时将资产从Dynamic Media Classic迁移到Dynamic Media - Scene7模式。 功能包可从以下网址获取： [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>您可以使用此功能包，在Experience Manager中自行将资产从Dynamic Media Classic批量迁移到Dynamic Media - Scene7模式。 您还可以使用Dynamic Media Classic中的FTP功能批量迁移资源。 但是，Adobe会 *非* 鉴于其中涉及到的复杂性，建议您使用这两种方法中的任何一种。
>
>因此，此迁移功能包是 *仅限* 作为迁移项目的一部分完成时受支持 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

在安装功能包之前，请创建服务用户并提供该信息以便Adobe支持。

另请参阅[配置 Dynamic Media - Scene7 模式](/help/assets/config-dms7.md).

**要安装功能包18912以批量迁移资产，请执行以下操作：**

1. 在您的Experience Manager实例中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 用户]** 并选择 **[!UICONTROL 创建用户]**. 此服务用户必须具有 *读/写* 权限 `/content/dam.`
1. 在 **[!UICONTROL ID]** 和 **[!UICONTROL 密码]** 字段中，输入用户名和密码；例如， **FTP用户**. 此名称将作为创建资源的用户显示在时间轴中。 从FTP上传资源时，资源会被视为在上传到FTP服务器并被推送到Experience Manager时创建。
1. 联系人 [针对Experience Manager的Adobe客户支持](https://experienceleague.adobe.com/?support-solution=General#support) 以请求访问功能包18912以供下载。 当您联系支持人员时，可能需要以下信息：

   * 创作实例的服务器IP地址，包括端口号（默认情况下，端口号为4502。）
   * Experience Manager上一步中的服务用户用户名和口令。

1. Experience Manager的Adobe客户支持为您提供FTP凭据以及功能包18912的访问权限。
1. 当您收到功能包18912时，请安装它。

   参见 [如何使用包](/help/sites-administering/package-manager.md) 有关在Experience Manager中使用Software Distribution和包的详细信息。
