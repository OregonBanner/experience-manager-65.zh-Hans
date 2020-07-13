---
title: 安装功能包18912以进行批量资产迁移
description: 功能包18912允许您通过FTP批量摄取资产，或将资产从Dynamic Media经典迁移到AEM上的Dynamic Media。 此可选功能包可从Adobe支持部门获得。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
translation-type: tm+mt
source-git-commit: d6ae8bffa2d9d59f5656b9344d8826128f12885c
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# 安装功能包18912以进行批量资产迁移{#installing-feature-pack-for-bulk-asset-migration}

安装功能包18912是可选 *的*。

功能包18912允许您通过FTP将资产直接批量收录到AEM上的Dynamic Media- Scene7模式，或将资产从Dynamic Media经典迁移到Dynamic Media-在AEM上的Scene7模式。 可从Adobe Professional Services获 [得该功能包](https://www.adobe.com/experience-cloud/consulting-services.html)。

>[!NOTE]
>
>虽然您可以使用功能包将资产从Dynamic Media经典批量迁移到Dynamic Media- AEM中的Scene 7模式或使用Dynamic Media经典中的FTP功能批量迁移资产，但Adobe不建议使用此方 *法* ，因为涉及的复杂性。
>
>因此，迁移功能包（如本包）仅 *在通过* Adobe Professional Services完成时 [，作为迁移项目的一部分](https://www.adobe.com/experience-cloud/consulting-services.html)受支持。

在安装该功能包之前，必须先创建服务用户并向Adobe支持人员提供该信息。

另请参 [阅配置Dynamic Media- Scene7模式](/help/assets/config-dms7.md)。

**安装功能包18912进行批量资产迁移**

1. 在AEM实例中，导航到工 **[!UICONTROL 具>安全>用户]** ，然后选 **[!UICONTROL 择创建用户]**。 此服务用户必 *须具有读／写* /写权限 `/content/dam.`
1. 在ID **[!UICONTROL 和]****[!UICONTROL Password]** 字段中输入用户名和密码； 例如， **FTP用户**。 此名称以创建资产的用户身份显示在时间轴中。 当资产从FTP上传时，当资产上传到FTP服务器并推送到AEM时，会视为已创建资产。
1. 请与 [Adobe企业客户关怀部门联系以获取Experience Manager](https://helpx.adobe.com/cn/contact/enterprise-support.ec.html) ，请求访问功能包18912以供下载。 在联系支持人员时，可能需要以下信息：

   * 您的作者实例的服务器IP地址，包括端口号（默认情况下，端口号为4502）。
   * 上一步中的AEM服务用户用户名和密码。

1. AEM的Adobe企业客户关怀团队为您提供FTP凭据和功能包18912的访问权限。
1. 收到功能包18912后，请安装它。

   有关 [在AEM中使用软件分发](/help/sites-administering/package-manager.md) 和软件包的更多信息，请参阅如何使用软件包。
