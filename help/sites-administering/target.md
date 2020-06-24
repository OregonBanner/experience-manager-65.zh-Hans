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
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 5%

---


# 与 Adobe Target 集成{#integrating-with-adobe-target}

作为Adobe Marketing Cloud的一部分， [Adobe Target](http://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) 允许您通过在所有渠道中进行定位和衡量来提高内容相关性。 Adobe Target由营销人员用来设计和执行在线测试、创建实时受众细分（基于行为）以及自动定位内容和在线体验。 AEM已采用在Adobe Target标准中使用的定位工作流。 如果您使用Target，您将熟悉AEM中的定位编辑环境。

将AEM站点与Adobe Target集成，以个性化页面中的内容：

* 实施内容定位。
* 使用Target受众创造个性化体验。
* 当Target与您的页面交互时，向访客提交上下文数据。
* 跟踪转化率。

要与Target集成，请执行以下任务:

1. [执行入门任务](/help/sites-administering/target-requirements.md): 向Adobe Target注册并配置AEM作者实例的某些方面。 您的Adobe Target帐户必须至少具有**审批者**级别权限。 此外，还必须保护发布节点上的活动设置，以便用户无法访问它。

1. 可以任选其一：

   1. [选择加入Adobe Target](/help/sites-administering/opt-in.md): 选择加入向导将获取您的Target帐户信息并创建Adobe Target云配置和Target框架。 该向导还将您的站点与Target框架相关联。 如果向导无法连接到目标，请参阅“连接 [故障拍摄”](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) 部分。 然后，您可 [以修改默认云配置](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations): 如有必要，请修改选择加入向导创建的云配置和框架。 例如，修改框架以向Target发送其他上下文数据。 如果要将AdobeAnalytics用作Adobe Target的报告源，您需要修改云配置以指向A4T配置。
   1. [手动与Adobe Target集成](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)。

1. [配置活动](/help/sites-authoring/activitylib.md): 将活动与Target云配置关联。

>[!NOTE]
>
>另请参 [阅使用DTM将AEM与Adobe Target和AdobeAnalytics集成](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)。

>[!NOTE]
>
>如果您正在使用自定义代理配置的Target，则需要配置两个HTTP客户端代理配置，因为AEM的某些功能使用3.x API，而其他一些功能则使用4.x API:
>
>* 3.x已配置为 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x配置为 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



>[!CAUTION]
>
>You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. 该活动设置节点应当只能由负责将活动同步到 Adobe Target 的服务访问。
>
>See [Prerequisites for Integrating with Adobe Target](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) for detailed information.

集成完成后，您可以创作 [目标内容](/help/sites-authoring/content-targeting-touch.md) ，将访客数据发送给Adobe Target。 请注意，页面组件需要特定代码才能启用内容定位。 (请参 [阅为目标内容进行开发](/help/sites-developing/target.md)。)

>[!NOTE]
>
>在AEM作者中目标组件时，该组件会向Adobe Target发出一系列服务器端调用，以注册活动、设置优惠和检索Adobe Target段（如果已配置）。 AEM发布到Adobe Target时不会进行任何服务器端调用。

## 背景信息源 {#background-information-sources}

将AEM与Adobe Target集成需要了解Adobe Target、AEM活动管理和AEM受众管理。 您应该熟悉以下信息：

* Adobe Target(请参阅 [Adobe Target文档](https://docs.adobe.com/content/help/en/target/using/target-home.html))。
* AEM活动控制台(请参 [阅管理活动](/help/sites-authoring/activitylib.md))。
* AEM受众(请参 [阅管理受众](/help/sites-authoring/managing-audiences.md))。

>[!NOTE]
>
>使用Adobe Target时，以下是活动中允许的最大伪数：
>
>* 50个地点
>* 2,000次体验
>* 50个指标
>* 50个报告细分

>



