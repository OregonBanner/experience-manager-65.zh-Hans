---
title: 与 Adobe Target 集成
seo-title: 与 Adobe Target 集成
description: 了解如何将AEM与Adobe Target集成。
seo-description: 了解如何将AEM与Adobe Target集成。
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
exl-id: 2b17d8cd-a43c-4d54-b990-a6f0cb1db22b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 5%

---

# 与 Adobe Target 集成{#integrating-with-adobe-target}

作为Adobe Marketing Cloud的一部分，[Adobe Target](http://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html)允许您通过跨所有渠道进行定位和测量来提高内容相关性。 营销人员使用Adobe Target来设计和执行在线测试、创建即时受众区段（基于行为）并自动定位内容和在线体验。 AEM已采用Adobe Target Standard中使用的定位工作流。 如果您使用Target，则会熟悉AEM中的定位编辑环境。

将您的AEM网站与Adobe Target集成，以个性化页面中的内容：

* 实施内容定位。
* 使用Target受众创建个性化体验。
* 当访客与您的页面进行交互时，将上下文数据提交到Target。
* 跟踪转化率。

要与Target集成，请执行以下任务：

1. [执行先决任务](/help/sites-administering/target-requirements.md):在Adobe Target中注册并配置AEM创作实例的某些方面。您的Adobe Target帐户必须至少具有**审批者**级权限。 此外，您还必须保护发布节点上的活动设置，以便用户无法访问该活动设置。

1. 可以任选其一：

   1. [选择加入Adobe Target](/help/sites-administering/opt-in.md):选择加入向导会获取您的Target帐户信息，并创建Adobe Target云配置和Target框架。该向导还会将您的站点与Target框架关联。 如果向导无法连接到目标，请参阅[连接故障排除](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems)一节。 然后，您可以[修改默认云配置](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations):如有必要，请修改选择加入向导创建的云配置和框架。 例如，修改框架以将其他上下文数据发送到Target。 如果要将Adobe Analytics用作Adobe Target的报表源，您需要修改云配置以指向A4T配置。
   1. [手动与Adobe Target集成](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)。

1. [配置活动](/help/sites-authoring/activitylib.md):将您的活动与Target云配置关联。

>[!NOTE]
>
>另请参阅[使用DTM将AEM与Adobe Target和Adobe Analytics集成](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)。

>[!NOTE]
>
>如果您使用的是具有自定义代理配置的Target，则需要配置两个HTTP客户端代理配置，因为AEM的某些功能使用3.x API，而其他一些功能使用4.x API:
>
>* 3.x配置了[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x配置了[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



>[!CAUTION]
>
>您必须保护发布实例上的活动设置节点&#x200B;**cq:ActivitySettings**，以便普通用户无法访问该节点。 该活动设置节点应当只能由负责将活动同步到 Adobe Target 的服务访问。
>
>有关详细信息，请参阅[与Adobe Target集成的先决条件](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node)。

集成完成后，您可以[创作目标内容](/help/sites-authoring/content-targeting-touch.md)以将访客数据发送到Adobe Target。 请注意，页面组件需要特定代码才能启用内容定位。 （请参阅[为目标内容开发](/help/sites-developing/target.md)。）

>[!NOTE]
>
>在AEM作者中定位某个组件时，该组件会向Adobe Target发起一系列服务器端调用，以注册该促销活动、设置选件和检索Adobe Target区段（如果已配置）。 不会从AEM发布到Adobe Target中进行服务器端调用。

## 背景信息源{#background-information-sources}

将AEM与Adobe Target集成需要了解Adobe Target、AEM活动管理和AEM受众管理。 您应该熟悉以下信息：

* Adobe Target(请参阅[Adobe Target文档](https://docs.adobe.com/content/help/en/target/using/target-home.html))。
* AEM活动控制台（请参阅[管理活动](/help/sites-authoring/activitylib.md)）。
* AEM受众（请参阅[管理受众](/help/sites-authoring/managing-audiences.md)）。

>[!NOTE]
>
>使用Adobe Target时，以下是营销活动中允许的最大工件数：
>
>* 50个位置
>* 2,000个体验
>* 50个量度
>* 50个报告区段

>


