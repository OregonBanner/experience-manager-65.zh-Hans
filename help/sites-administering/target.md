---
title: 与 Adobe Target 集成
seo-title: Integrating with Adobe Target
description: 了解如何将Adobe Experience Manager与Adobe Target集成。
seo-description: Learn about integrating AEM with Adobe Target.
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
exl-id: 2b17d8cd-a43c-4d54-b990-a6f0cb1db22b
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 66%

---

# 与 Adobe Target 集成{#integrating-with-adobe-target}

作为 Adobe Marketing Cloud 的一部分，[Adobe Target](https://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) 允许您通过在所有渠道中进行定位和衡量来提高内容相关性。营销人员使用 Adobe Target 来设计和执行在线测试、创建动态受众区段（基于行为）以及自动定位内容和在线体验。AEM采用了Adobe Target Standard中使用的定位工作流。 如果使用Target，您将熟悉AEM中的定位编辑环境。

将 AEM Sites 与 Adobe Target 集成以个性化页面中的内容：

* 实施内容定位。
* 使用 Target 受众创建个性化体验。
* 在访客与您的页面交互时，将上下文数据提交到 Target。
* 跟踪转化率。

要与 Target 集成，请执行以下任务：

1. [执行必备任务](/help/sites-administering/target-requirements.md)：向 Adobe Target 注册并配置 AEM 创作实例的某些方面。您的Adobe Target帐户必须至少具有**审批者**级别的权限。 此外，您必须保护发布节点上的活动设置，以便用户无法访问。

1. 可以任选其一：

   1. [选择加入Adobe Target](/help/sites-administering/opt-in.md)：选择加入向导会获取您的Target帐户信息，并创建Adobe Target云配置和Target框架。 该向导还会将您的站点与Target框架相关联。 如果向导无法连接到目标，请参阅 [连接故障排除](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) 部分。 您可以 [修改默认云配置](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations)：如有必要，请修改选择加入向导创建的云配置和框架。 例如，修改框架以将其他上下文数据发送到Target。 如果要使用Adobe Analytics作为Adobe Target的报表源，则需要修改云配置以指向A4T配置。
   1. [手动与Adobe Target集成](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [配置活动](/help/sites-authoring/activitylib.md)：将您的活动与 Target 云配置相关联。

>[!NOTE]
>
>另请参阅 [使用DTM将AEM与Adobe Target和Adobe Analytics集成](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>如果您将 Target 与自定义代理配置一起使用，则需要配置 HTTP 客户端代理配置，因为 AEM 的某些功能使用的是 3.x API，而其他一些功能使用的是 4.x API：
>
>* 3.x 通过 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) 进行配置
>* 4.x 通过 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) 进行配置
>

>[!CAUTION]
>
>您必须确保发布实例中的活动设置节点 **cq:ActivitySettings** 安全，以使其不可由普通用户访问。该活动设置节点应当只能由负责将活动同步到 Adobe Target 的服务访问。
>
>请参阅[与 Adobe Target 集成的先决条件](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node)，以了解详细信息。

在集成完成后，您可以[创作目标内容](/help/sites-authoring/content-targeting-touch.md)来将访客数据发送到 Adobe Target。请注意，页面组件需要特定代码才能启用内容定位。（请参阅[针对目标内容进行开发](/help/sites-developing/target.md)。））

>[!NOTE]
>
>在 AEM 创作实例中定位组件时，该组件会对 Adobe Target 进行一系列的服务器端调用，以便注册活动、设置选件和检索 Adobe Target 区段（如果已配置）。没有从 AEM Publish 到 Adobe Target 的服务器端调用。

## 背景信息源 {#background-information-sources}

将AEM与Adobe Target集成需要Adobe Target、AEM Activities管理和AEM Audiences管理的知识。 您应熟悉以下信息：

* Adobe Target（请参阅 [Adobe Target 文档](https://experienceleague.adobe.com/docs/target/using/target-home.html)）。
* AEM 活动控制台（请参阅[管理活动](/help/sites-authoring/activitylib.md)）。
* AEM 受众（请参阅[管理受众](/help/sites-authoring/managing-audiences.md)）。

>[!NOTE]
>
>使用 Adobe Target 时，以下是活动中允许的最大构件数：
>
>* 50 个位置
>* 2,000 个体验
>* 50 个量度
>* 50 个报告区段
>
