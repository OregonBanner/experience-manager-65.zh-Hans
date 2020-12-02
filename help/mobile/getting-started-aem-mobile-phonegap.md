---
title: AEMAdobe PhoneGap
seo-title: AEMAdobe PhoneGap
description: AEM与PhoneGap集成，因此您可以使用AEM页面轻松创建应用程序。 可查看本页以开始使用Adobe PhoneGap企业。
seo-description: AEM与PhoneGap集成，因此您可以使用AEM页面轻松创建应用程序。 可查看本页以开始使用Adobe PhoneGap企业。
uuid: bdd90cda-2489-4763-a90a-9c409d6e68ae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: fbcdea8a-72e9-431b-9c32-dc02d4cdb9c8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 1%

---


# AEMAdobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM与PhoneGap集成，因此您可以使用AEM页面轻松创建应用程序。 PhoneGap允许用户创建实用程序应用程序，以便用户处理内容。 内容同步使您能够创建与应用程序捆绑的页面版本控制存档。

通常，***AEM Administrator***&#x200B;负责通过使用创建向导创建新应用程序或导入现有应用程序将新应用程序添加到AEM Mobile目录。

从此处，***AEM作者***（或&#x200B;*营销人员*）现在可以使用现成的模板和组件来添加和编辑页面、拖放组件以及添加DAM中所有类型的媒体，包括图像、视频和文本片段（内容片段）。

AEM Mobile的真正威力在于，*savv* ***AEM开发人员***&#x200B;可以扩展和创建自定义Web模板和组件，使&#x200B;*AEM作者*&#x200B;能够创建出美妙、引人入胜的移动体验。 这些模板和组件不仅针对移动App世界进行了优化；但可以同时与设备和AEM服务器（任何远程服务器）通信到全渠道服务端点。

>[!NOTE]
>
>当&#x200B;*AEM作者*&#x200B;认为应用程序已就绪时，他们可以首先让利益相关方下载具有&#x200B;**[Adobe验证](/help/mobile/phonegap-mobile-quickstart.md)**（在AppStore和PlayStore中均提供）的应用程序以进行审核和批准。 获得绿灯后，他们可以通过AEM MobileContentSync内容发布管理仪表板直接向用户发布此新内容或更新内容。 一个人可以承担任何角色，这取决于您和您的治理政策。

## 前提条件 {#prerequisites}

AEM Mobile只是构成整个AEM平台的支柱之一。

在与AEM Mobile合作并遵循本入门指南中的步骤之前，用户应熟悉AEM和AEM Mobile控制中心。 请参阅：

[AEM 快速入门](/help/sites-deploying/deploy.md)

[AEM Mobile管制中心漫步](/help/mobile/phonegap-authoring-apps.md)

## 作者的QuickLinks {#quicklinks-for-authors}

请参阅AEM中的[为Adobe PhoneGap企业进行创作](/help/mobile/phonegap.md)以了解作者的角色和职责。

## 开发人员的QuickLinks {#quicklinks-for-developers}

有样例应用程序将与AEM Mobile集成，可由开发人员进行自定义。 单击[使用AEM开发Adobe PhoneGap企业](/help/mobile/developing-in-phonegap.md)。

在后续章节中，您将了解高级概念，如白色标记应用程序、本地化、国际化、内容同步、定位、分析等。

## 管理员{#quicklinks-for-administrators}的QuickLinks

请参阅[为Adobe PhoneGap企业管理包含AEM](/help/mobile/administer-phonegap.md)的内容以设置和管理您的移动应用程序。

>[!NOTE]
>
>使用混合移动技术，您可以创建富移动应用程序，这些应用程序实际上&#x200B;*在AEM Mobile线离线运行，并在线运行。许多客户选择创建应用程序来检查他们在线或离线的时间，并相应地进行操作。*
