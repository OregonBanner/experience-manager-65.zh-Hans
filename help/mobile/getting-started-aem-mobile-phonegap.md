---
title: AEM Adobe PhoneGap
seo-title: AEM Adobe PhoneGap
description: AEM与PhoneGap集成，以便您可以使用AEM页面轻松创建应用程序。 关注本页以开始使用Adobe PhoneGap Enterprise。
seo-description: AEM integrates with PhoneGap so that you can easily create apps using AEM pages. Follow this page to get started with Adobe PhoneGap Enterprise.
uuid: bdd90cda-2489-4763-a90a-9c409d6e68ae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: fbcdea8a-72e9-431b-9c32-dc02d4cdb9c8
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

AEM与PhoneGap集成，以便您可以使用AEM页面轻松创建应用程序。 PhoneGap允许用户创建实用工具应用程序，以便用户处理内容。 内容同步允许您创建页面的版本化存档，以便与应用程序捆绑在一起。

通常， ***AEM管理员*** 负责向AEM Mobile目录中添加新应用程序，方法是使用创建向导创建新应用程序，或导入现有应用程序。

从此处开始 ***AEM创作*** (或 *营销人员*)现在可以使用现成的模板和组件来添加和编辑页面、拖放组件以及从DAM添加所有类型的媒体，包括图像、视频和文本片段（内容片段）。

AEM Mobile的真正力量在于 *精明* ***AEM开发人员*** 可以扩展和创建自定义Web模板和组件，以启用 *AEM创作* 创造美妙而引人入胜的移动体验。 这些模板和组件不仅针对移动应用程序世界进行了优化，而且还与设备通信，并与全渠道服务端点的AEM服务器（任何远程服务器）通信。

>[!NOTE]
>
>当 *AEM创作* 确信应用程序已就绪，他们可以首先让利益相关者下载应用程序， **[Adobe验证](/help/mobile/phonegap-mobile-quickstart.md)** （在AppStore和PlayStore中均可用）以供审阅和批准。 一旦他们收到绿灯，就可以通过AEM Mobile ContentSync内容发布管理功能板，直接向其用户发布这些新的或更新后的内容。 一个人可以担任任意数量的角色，具体取决于您和您的治理策略。

## 前提条件 {#prerequisites}

AEM Mobile只是构成整个AEM平台的支柱之一。

在使用AEM Mobile并按照本快速入门指南中的步骤操作之前，用户应该熟悉AEM和AEM Mobile控制中心。 请参阅：

[AEM 快速入门](/help/sites-deploying/deploy.md)

[AEM Mobile控制中心演练](/help/mobile/phonegap-authoring-apps.md)

## 作者的快速链接 {#quicklinks-for-authors}

参见 [在AEM中为Adobe PhoneGap Enterprise创作](/help/mobile/phonegap.md) 了解作者的角色和职责。

## 面向开发人员的快速链接 {#quicklinks-for-developers}

有一些示例应用程序将与AEM Mobile集成并可由开发人员进行自定义。 单击 [使用AEM开发Adobe PhoneGap Enterprise](/help/mobile/developing-in-phonegap.md).

在接下来的章节中，您将了解高级概念，如白色标签设置、应用程序、本地化、国际化、内容同步、定位、分析等。

## 适用于管理员的快速链接 {#quicklinks-for-administrators}

参见 [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md) 以设置和管理您的移动应用程序。

>[!NOTE]
>
>使用混合移动技术，您可以创建丰富的移动应用程序， *脱机运行和联机运行* 事实上，通过AEM Mobile，许多客户会选择创建应用程序，以便检查他们在线或离线时的情况，并做出相应的行为。
