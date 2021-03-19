---
title: 基本配置概念
seo-title: 基本配置概念
description: 了解如何配置AEM。
seo-description: 了解如何配置AEM。
uuid: edcdd4bd-5917-417e-8913-40d488383ea9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 2673ea92-1651-4b1b-9aac-f4ba8b36782e
feature: 配置
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2133'
ht-degree: 1%

---


# 基本配置概念{#basic-configuration-concepts}

Adobe Experience Manager(AEM)随所有参数的默认设置一起安装，允许其“开箱即用”。 但是，您可以根据自己的特定要求配置AEM。

可以配置AEM的许多方面：

* 某些组件[通常针对每个项目安装](#primary-configuration-considerations)进行配置，必须进行审核以确认它们是否适用于您的项目。
* [进一步](#further-configuration-considerations) 配置可能是常见的，但并非当务之急；与功能或系统性能和稳定性相关。
* 其他只有AEM的某些可选功能才需要（这些功能与相应的功能一起进行了说明）。

根据特定配置，可以通过以下任一方式进行这些更改：

* **Adobe CQ Web Console**

   这是用于配置OSGi包和服务的标准位置。

   有关更多详细信息和建议的做法，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)。

* **存储库**

   存储库中提供了OSGi配置的子集。 这可确保复制或复制存储库内容会重新创建相同的配置。 您还可以根据运行模式将您自己的配置添加到存储库。

   有关更多详细信息，请参阅存储库](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)中的[ OSGi配置，特别是[向存储库](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)添加新配置。

* **文件系统**

   文件系统中存在一些配置文件。

* **AEM WCM**

   可以在AEM WCM内部配置各种方面，许多方面使用[工具](/help/sites-administering/tools-consoles.md)控制台；例如，复制代理。

>[!NOTE]
>
>使用Adobe Experience Manager时，有多种方法可管理OSGi服务（控制台或存储库节点）的配置设置。
>
>有关完整的详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)。

>[!NOTE]
>
>配置AEM很简单，但您必须注意：
>
>某些更改可能会对应用程序产生重大影响。 因此，在开始配置AEM之前，请确保您拥有必要的经验和知识，并且只做出所需的更改。 通过OSGi控制台所做的任何更改都应用于正在运行的系统（不需要重新启动）。****

## 主要配置注意事项{#primary-configuration-considerations}

此列表详细列出了每个新项目通常配置的主要区域。 并非所有项目都需要，但必须阅读并审阅列表，以查看哪些项目适用。

该列表简要概述了每个配置方面，以及指向提供完整详细信息的页面的链接。

### 安全清单{#security-checklist}

[安全清单](/help/sites-administering/security-checklist.md)中列出了几个关键配置问题。 请确保您已阅读此文件，并采取安装所需的任何操作。

### 配置默认UI — 触屏优化或经典{#configuring-the-default-ui-touch-optimized-or-classic}

有两种UI可用于AEM:

* 触屏优化UI
* 经典 UI

您可以使用[根映射](/help/sites-deploying/osgi-configuration-settings.md)配置所需的UI。

>[!NOTE]
>
>有关选择UI的更多信息，请参阅[选择UI](/help/sites-authoring/select-ui.md)。

### IPv4和IPv6 {#ipv-and-ipv}

AEM的所有元素（例如存储库、调度程序等）都可以安装在IPv4和IPv6网络中。

操作是无缝的，因为不需要特殊配置，在需要时，您只需使用适合您的网络类型的格式指定IP地址即可。

这意味着，当需要指定IP地址时，您可以从以下位置（根据需要）进行选择：

* IPv6地址

   例如`https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4地址

   例如`https://123.1.1.4:4502`

* 服务器名称

   例如，`https://www.yourserver.com:4502`

* `localhost`的默认情况将解释为IPv4和IPv6网络安装

   例如，`http://localhost:4502`

### 版本清除{#version-purging}

在标准安装中，每当您激活页面（在更新内容后）时，AEM都会创建页面或节点的新版本。您还可以使用Sidekick的&#x200B;**版本控制**&#x200B;选项卡在请求时创建其他版本。 所有这些版本都存储在存储库中，并可在需要时还原。

这些版本从不清除，因此随着时间推移，存储库的大小会增大，因此需要进行管理。

有关完整的详细信息，请参阅[版本清除](/help/sites-deploying/version-purging.md)，特别是[版本管理器](/help/sites-deploying/version-purging.md#version-manager)，了解如何配置AEM在创建新版本时清除旧版本的详细信息。

### 记录 {#logging}

AEM优惠您可以配置：

* 中央日志记录服务的全局参数
* 请求数据记录；请求信息的专用日志记录配置
* 具体设置；例如，单个日志文件和日志消息的格式

有关完整的详细信息，请参阅[日志记录](/help/sites-deploying/configure-logging.md)。

### 运行模式 {#run-modes}

运行模式允许您针对特定目的调整AEM实例；例如，创作或发布、测试、开发或内部网等。

为此，请为每个运行模式定义配置参数的集合。 所有运行模式都会应用一组基本的配置参数，然后您可以根据您的特定环境调整其他配置参数。 然后，将根据需要应用这些值。

所有配置设置都存储在一个存储库中，并通过设置&#x200B;**运行模式**&#x200B;激活。

有关完整的详细信息，请参阅[运行模式](/help/sites-deploying/configure-runmodes.md)。

### 单点登录{#single-sign-on}

单点登录(SSO)允许用户在提供一次身份验证凭据（如用户名和密码）后访问多个系统。 单独的系统（称为受信任验证器）执行该验证并向Experience Manager提供用户凭据。 Experience Manager检查并强制用户访问权限（即确定允许用户访问哪些资源）。

有关更多详细信息，请参阅[单点登录](/help/sites-deploying/single-sign-on.md)。

### 资源映射{#resource-mapping}

资源映射用于定义AEM的重定向、虚URL和虚拟主机。

例如，您可以使用这些映射来：

* 在所有请求前面添加`/content`前缀，以使内部结构在访客到您网站时处于隐藏状态。
* 定义重定向，以便将发往网站`/content/en/gateway`页面的所有请求重定向到`https://gbiv.com/`。

有关更多详细信息，请参阅[资源映射](/help/sites-deploying/resource-mapping.md)。

### 复制、反向复制和复制代理{#replication-reverse-replication-and-replication-agents}

复制代理是AEM的中心，作为用于：

* [将内容从作](/help/sites-authoring/publishing-pages.md) 者发布（激活）到发布环境。
* 显式刷新Dispatcher缓存中的内容。
* 将用户输入（例如，表单输入）从发布环境返回到作者环境(在作者环境的控制下)。

有关详细信息，请参阅[复制](/help/sites-deploying/replication.md)。

### OSGi配置设置{#osgi-configuration-settings}

[OSG](https://www.osgi.org/) 是AEM技术堆栈中的一个基本元素。它用于控制AEM的复合束及其配置。

有关与项目实施相关的各种包的列表（按包列出），请参阅[OSGi配置设置](/help/sites-deploying/osgi-configuration-settings.md)。 并非列出的所有设置都需要调整，其中某些设置可帮助您了解AEM的操作方式。

使用AEM时，有多种方法可管理此类服务的配置设置；请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)以了解更多详细信息和建议的做法。

### 配置LDAP {#configuring-ldap}

需要LDAP身份验证才能对存储在（中央）LDAP目录（如Active Directory）中的用户进行身份验证。 这有助于减少管理用户帐户所需的工作。

LDAP身份验证发生在存储库级别，因此由存储库直接处理。 有关详细信息，请参阅[使用AEM](/help/sites-administering/ldap-config.md)配置LDAP。

有关AEM中的用户管理（包括访问权限的分配），请参阅[用户管理和安全](/help/sites-administering/security.md)。

### 配置调度程序{#configuring-the-dispatcher}

Dispatcher是Adobe Experience Manager的缓存和/或负载平衡工具，可与企业级Web服务器结合使用。

有关完整的详细信息，请参阅[Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)，特别是[配置Dispatcher](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html)以了解更多配置详细信息。

### 配置AEM LiveCycle连接器{#configuring-aem-livecycle-connector}

随着AEM文档服务和AEM文档安全性的发布，我们现在能够调用LiveCycle文档服务来呈现XFA表单、将文档转换为PDF以及策略保护文档。 有关详细信息，请阅读[AEM LiveCycle Connector](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html)。

### 作业卸载和拓扑管理{#job-offloading-and-topology-administration}

[分](/help/sites-deploying/offloading.md) 散处理任务在拓扑中分布大量Experience Manager实例。通过卸载，您可以使用特定的Experience Manager实例执行特定类型的处理。 专用处理使您能够最大限度地利用可用的服务器资源。

拓扑是参与卸载的松耦合Experience Manager群集。 群集由一个或多个Experience Manager服务器实例（单个实例被视为群集）组成。

有关如何视图或修改拓扑成员关系的详细信息，请参阅[管理拓扑](/help/sites-deploying/offloading.md#administering-topologies)部分。

### 配置欢迎控制台{#configuring-the-welcome-console}

经典UI的“欢迎”控制台提供了指向AEM中各个控制台和功能的链接列表。

可以配置可见的链接，有关更多详细信息，请参阅[配置欢迎控制台](/help/sites-developing/customizing-the-welcome-console.md)。

### 配置性能{#configuring-for-performance}

[性](/help/sites-deploying/configuring-performance.md) 能是项目的关键。可以配置AEM（和/或基础存储库）的某些方面以优化性能。

有关更多详细信息，请参阅[配置性能](/help/sites-deploying/configuring-performance.md#configuring-for-performance)。

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### 共享数据存储{#shared-data-store}

存储库数据存储器用于卸载从存储库本体到单独区域的大型二进制文件的存储，以便存储库树内相同二进制的多个实例（例如图像）只存储一次。

此“存储一次、引用多次”功能可扩展为不仅服务于单个存储库树，而且服务于完全独立的存储库，方法是将每个存储库的数据存储配置为引用同一共享文件系统位置。

这样的数据存储可以在同一群集中的不同节点之间共享，在同一安装中的不同发布和/或作者实例之间共享，甚至在不同安装中完全独立的实例之间共享。

有关详细信息，请参阅[配置数据存储和节点存储](/help/sites-deploying/data-store-config.md)。

## 其他配置注意事项{#further-configuration-considerations}

### 通过SSL启用HTTP {#enabling-http-over-ssl}

您可以启用HTTP over SSL以使用与服务器的更安全连接。

有关更多详细信息，请参阅[启用HTTP over SSL](/help/sites-administering/ssl-by-default.md)。

### AEM门户和Portlet {#aem-portals-and-portlets}

门户是一个Web应用程序，它提供个性化、单一登录、来自不同来源的内容集成，并托管信息系统的表示层。 Portlet组件还允许您在页面上嵌入Portlet。 要访问CQ5 WCM提供的内容，可以为门户服务器安装CQ5 Portal Director Portlet。 为此，可以通过安装、配置Portlet并将其添加到门户页面。

有关更多详细信息，请参阅[门户和Portlet](/help/sites-administering/aem-as-portal.md)。

### 静态对象{#expiration-of-static-objects}的过期

静态对象（例如，图标）不会更改。 因此，应配置系统，使其不会过期（在合理的时间段内），从而减少不必要的流量。

有关更多详细信息，请参阅[静态对象的过期](/help/sites-deploying/expiration-static-objects.md)。

### 在Java进程{#open-files-in-the-java-process}中打开FIle

每个Java进程都可以访问文件 — 这需要系统资源。 因此，对每个进程允许同时访问的文件数定义了上限。 如果超出此限制，则可能发生异常错误。

如果AEM进程超出此最大值，则消息“ `too many open files`”将在`error.log`中显示。

要避免此类例外，您需要：

1. 检查您的AEM进程正在使用的打开文件数。

   您如何进行此检查取决于您的实例运行的平台。 可以使用lsof(Unix)或Process Explorer(Windows)等实用程序。

   在开发和测试过程中应监测此值，以：

   * 根据需要确认正在关闭文件
   * 确定所需的最大值（在各种情况下）

1. 设置允许的最大值。

   新值应同时满足当前需求和未来任何峰值，因此最好多次当前需求。

   默认情况下，`serverctl`将`CQ_MAX_OPEN_FILES`配置为`8192`;对于大多数情况，这应该足够。

### 配置富文本编辑器{#configuring-the-rich-text-editor}

**富文本编辑器**(**RTE**)为作者提供了范围广泛的[功能](/help/sites-authoring/rich-text-editor.md)来编辑其文本内容；为他们提供图标、选择框和菜单，以实现所见即所得的体验。

有关更多详细信息，请参阅[配置富文本编辑器](/help/sites-administering/rich-text-editor.md)。

### 为页面编辑配置撤消{#configuring-undo-for-page-editing}

有几个属性可控制编辑页面的撤消和重做命令的行为。 可以配置这些属性，有关更多详细信息，请参阅[为页面编辑配置撤消](/help/sites-administering/config-undo.md)。

### 配置视频组件{#configuring-the-video-component}

[视频组件](/help/sites-authoring/default-components-foundation.md#video)允许您在页面上放置一个预定义的现成视频元素。

为了进行正确转码，您的管理员必须单独[安装 FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg)。还可以[配置视频用户档案](/help/sites-administering/config-video.md#configure-video-profiles)以用于html5元素。

### 配置和自定义报表{#configuring-and-customizing-reports}

为了帮助您监视和分析实例的状态，CQ提供了一系列默认报告，这些报告可以根据您的具体要求进行配置：

有关更多详细信息，请参阅[报表自定义基础知识](/help/sites-administering/reporting.md#the-basics-of-report-customization)。

### 配置电子邮件通知{#configuring-email-notification}

CQ向以下用户发送电子邮件通知：

* 已订阅页面事件，例如修改或复制。
* 已订阅论坛事件。
* 必须在工作流中执行一个步骤。

有关更多详细信息，请参阅[配置电子邮件通知](/help/sites-administering/notification.md)。

### 启用页面展示次数{#enabling-page-impressions}

页面展示次数显示在经典UI站点管理控制台的&#x200B;**展示次数**&#x200B;列中。 要启用页面展示次数的捕获，您需要配置：

* 在发布实例上：

   * [Day CQ WCM页面统计信息](/help/sites-deploying/osgi-configuration-settings.md)

* 在作者实例中：

   * [Adobe页面展示次数跟踪](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>在创作环境上配置Adobe页面展示次数跟踪器将允许对跟踪服务进行匿名请求。

