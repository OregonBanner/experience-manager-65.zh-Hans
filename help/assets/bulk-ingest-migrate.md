---
title: 安装功能包18912以批量迁移资产
description: 功能包18912允许您通过FTP批量摄取资产，或将资产从Dynamic Media Classic迁移到AEM上的Dynamic Media。 此可选功能包可从Adobe支持部门获得。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 安装功能包18912以批量迁移资产{#installing-feature-pack-for-bulk-asset-migration}

安装功能包18912是可选 *的*。

功能包18912允许您通过FTP将资产直接批量收录到AEM的Dynamic Media - Scene7模式，或将资产从Dynamic Media Classic迁移到AEM的Dynamic Media - Scene7模式。 该功能包可从 [Adobe Professional Services获得](https://www.adobe.com/experience-cloud/consulting-services.html)。

>[!NOTE]
>
>虽然您可以使用功能包将资产从Dynamic Media Classic批量迁移到Dynamic Media - AEM中的Scene 7模式或使用Dynamic Media Classic中的FTP功能批量迁移资产，但Adobe不建议使用此方法，因为涉及的复杂性 ** 。
>
>因此，只有通过 *Adobe Professional Services* ，迁移项目才支持迁移功能包（如此） [](https://www.adobe.com/experience-cloud/consulting-services.html)。

在安装功能包之前，您必须先创建服务用户并向Adobe支持部门提供该信息。

另请参 [阅配置Dynamic Media - Scene7模式](/help/assets/config-dms7.md)。

**安装功能包18912以批量迁移资产**

1. 在AEM实例中，导航到工具>安 **[!UICONTROL 全性>用户]** ，然后选择 **[!UICONTROL 创建用户]**。 此服务用户必须具 ** 有对 `/content/dam.`
1. 在 **[!UICONTROL ID]** and **[!UICONTROL Password(ID]** 和密码)字段中，输入用户名和密码；例如， **FTP用户**。 此名称以创建资产的用户身份显示在时间轴中。 从FTP上传资产时，当资产上传到FTP服务器并推送到AEM时，系统会考虑创建该资产。
1. 请与 [Adobe Enterprise Customer Care for Experience Manager联系](https://helpx.adobe.com/cn/contact/enterprise-support.ec.html) ，请求访问功能包18912进行下载。 联系支持部门时，您可能需要以下信息：

   * 您的作者实例的服务器IP地址，包括端口号（默认情况下，端口号为4502）。
   * 上一步中的AEM服务用户用户名和密码。

1. AEM的Adobe企业客户关怀为您提供FTP凭据和对功能包18912的访问。
1. 收到功能包18912后，请安装它。

   有关 [在AEM中使用包共享和包的更多信息](/help/sites-administering/package-manager.md) ，请参阅如何使用包。
