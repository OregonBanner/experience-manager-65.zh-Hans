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
translation-type: tm+mt
source-git-commit: 8f35717324cd2c1524fb2cf931b3ce21be05729a
workflow-type: tm+mt
source-wordcount: '2132'
ht-degree: 1%

---


# 基本配置概念{#basic-configuration-concepts}

Adobe Experience Manager(AEM)安装了所有参数的默认设置，允许其“开箱即用”。 但是，您可以根据自己的特定要求配置AEM。

可以配置AEM的许多方面：

* 有些是 [为每个项目安装配置的](#primary-configuration-considerations) ，必须进行审核以确认它们是否适用于您的项目。
* [进一步的配置](#further-configuration-considerations) ，可能是常见的，但并非势在必行；与功能或系统性能和稳定性相关。
* 其他功能仅对AEM的某些可选功能是必需的（这些功能与相应的功能一起进行了说明）。

根据特定配置，可以通过以下任一方式进行这些更改：

* **Adobe CQ网络控制台**

   这是用于配置OSGi捆绑套件和服务的标准位置。

   有关更 [多详细信息](/help/sites-deploying/configuring-osgi.md) ，请参阅配置OSGi。

* **存储库**

   OSGi配置的子集在存储库中可用。 这可确保复制或复制存储库内容会重新创建相同的配置。 您还可以根据运行模式将您自己的配置添加到存储库中。

   有关 [更多详细信息](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) ，请参 [阅存储库中的OSGi配置，尤其是向存储库中添加新配置](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) 。

* **文件系统**

   文件系统中有一些配置文件。

* **AEM WCM**

   可以在AEM WCM内配置各种方面，其中许多方面都使用 [工具](/help/sites-administering/tools-consoles.md) 控制台；例如，复制代理。

>[!NOTE]
>
>与Adobe Experience Manager合作时，有几种方法可管理OSGi服务（控制台或存储库节点）的配置设置。
>
>有关完 [整的详细信息](/help/sites-deploying/configuring-osgi.md) ，请参阅配置OSGi。

>[!NOTE]
>
>配置AEM很简单，但您必须知道：
>
>某些更改可能会对应用程序产生重大影响。 因此，在开始配置AEM之前，请确保您拥有必要的经验和知识，并只进行您知道需要的更改。 通过OSGi控制台进行的任何更改 **会立即** 应用于正在运行的系统（无需重新启动）。

## 主要配置注意事项 {#primary-configuration-considerations}

此列表详细列出了每个新项目通常配置的主要区域。 并非所有内容都是必需的，但必须阅读并审阅列表，以查看哪些内容适用于您的项目。

该列表简要概述了每个配置方面，以及指向提供完整详细信息的页面的链接。

### Security Checklist {#security-checklist}

安全清单中列出了几个关 [键配置问题](/help/sites-administering/security-checklist.md)。 请确保您已阅读此文件，并采取安装所需的任何操作。

### 配置默认UI —— 触屏优化或经典 {#configuring-the-default-ui-touch-optimized-or-classic}

有两种UI可用于AEM:

* 触屏优化UI
* 经典 UI

您可以使用根映射配置所需 [的UI](/help/sites-deploying/osgi-configuration-settings.md)。

>[!NOTE]
>
>有关选择UI的更多信息，请参阅 [选择UI](/help/sites-authoring/select-ui.md)。

### IPv4和IPv6 {#ipv-and-ipv}

AEM的所有元素（例如存储库、调度程序等）都可以安装在IPv4和IPv6网络中。

操作是无缝的，因为不需要特殊配置，在需要时，您只需使用适合您的网络类型的格式指定IP地址。

这意味着，当需要指定IP地址时，您可以从以下位置（根据需要）进行选择：

* IPv6地址

   for example `https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4地址

   for example `https://123.1.1.4:4502`

* 服务器名称

   for example, `https://www.yourserver.com:4502`

* 将解释IPv4 `localhost` 和IPv6网络安装的默认情况

   for example, `http://localhost:4502`

### 版本清除 {#version-purging}

在标准安装中，每当您激活页面（在更新内容后）时，AEM都会创建页面或节点的新版本。您还可以使用Sidekick的“版本控制”选项卡在请求时创 **建其** 他版本。 所有这些版本都存储在存储库中，并可在需要时还原。

这些版本从不被清除，因此存储库大小会随着时间的推移而增大，因此需要进行管理。

有关 [如何配置AEM](/help/sites-deploying/version-purging.md) 以在创建新版本时清除旧版本的详细信息，请 [参阅版本清除](/help/sites-deploying/version-purging.md#version-manager) ，尤其是版本管理器。

### 记录 {#logging}

AEM优惠您可以配置：

* 中央日志记录服务的全局参数
* 请求数据记录；请求信息的专用日志记录配置
* 具体设置；例如，单个日志文件和日志消息的格式

有关完整 [的详细信](/help/sites-deploying/configure-logging.md) 息，请参阅日志记录。

### 运行模式 {#run-modes}

运行模式允许您针对特定目的调整AEM实例；例如，创作或发布、测试、开发或内部网等。

为此，请为每个运行模式定义配置参数集合。 基本的配置参数集将应用于所有运行模式，然后您可以根据特定环境的目的调整其他设置。 然后根据需要应用这些值。

所有配置设置都存储在一个存储库中，并通过设置“运行模式” **来激活**。

有关完 [整的详细信](/help/sites-deploying/configure-runmodes.md) 息，请参阅运行模式。

### 单一登录 {#single-sign-on}

单一登录(SSO)允许用户在提供一次身份验证凭据（如用户名和密码）后访问多个系统。 单独的系统（称为受信任的验证器）执行该验证并向Experience Manager提供用户凭据。 Experience Manager检查并强制用户访问权限（即确定允许用户访问哪些资源）。

有关更 [多详细信息](/help/sites-deploying/single-sign-on.md) ，请参阅单一登录。

### 资源映射 {#resource-mapping}

资源映射用于为AEM定义重定向、虚URL和虚拟主机。

例如，您可以使用这些映射：

* 在所有请求前加 `/content` 上前缀，使内部结构在访客到您网站时处于隐藏状态。
* 定义重定向，以便将所有请求重 `/content/en/gateway` 定向到您网站的页面 `https://gbiv.com/`。

有关更 [多详细信息](/help/sites-deploying/resource-mapping.md) ，请参阅资源映射。

### 复制、反向复制和复制代理 {#replication-reverse-replication-and-replication-agents}

复制代理作为用于以下目的的机制对AEM至关重要：

* [将内容从作者](/help/sites-authoring/publishing-pages.md) （激活）发布到发布环境。
* 显式刷新Dispatcher缓存中的内容。
* 将用户输入（例如，表单输入）从发布环境返回到作者环境(在作者环境的控制下)。

For further details see [Replication](/help/sites-deploying/replication.md).

### OSGi配置设置 {#osgi-configuration-settings}

[OSGi是AEM](https://www.osgi.org/) 技术堆栈中的一个基本元素。 它用于控制AEM的复合束及其配置。

请参 [阅与项目实施](/help/sites-deploying/osgi-configuration-settings.md) （根据捆绑包列出）相关的各种捆绑包的列表的OSGi配置设置。 并非所有列出的设置都需要调整，其中有些设置可以帮助您了解AEM的操作方式。

When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

### 配置LDAP {#configuring-ldap}

需要LDAP身份验证才能对存储在（中央）LDAP目录（如Active Directory）中的用户进行身份验证。 这有助于减少管理用户帐户所需的工作。

LDAP身份验证在存储库级别执行，因此由存储库直接处理。 有关更多详细信息，请 [参阅使用AEM配置LDAP](/help/sites-administering/ldap-config.md)。

有关AEM中的用户管理（包括访问权限分配），请参 [阅用户管理和安全](/help/sites-administering/security.md)。

### 配置调度程序 {#configuring-the-dispatcher}

调度程序是Adobe Experience Manager的缓存和／或负载平衡工具，可与企业级Web服务器结合使用。

请参 [阅Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) ，了解完整详细信息， [特别是配置Dispatcher](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html) ，以了解更多配置详细信息。

### 配置AEMLiveCycle连接器 {#configuring-aem-livecycle-connector}

随着AEM文档服务和AEM文档安全的发布，我们现在能够调用LiveCycle文档服务来呈现XFA表单、将文档转换为PDF并保护文档。 请阅读AEM [LiveCycle连接器](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html) ，了解更多详细信息。

### 作业卸载和拓扑管理 {#job-offloading-and-topology-administration}

[卸载](/help/sites-deploying/offloading.md) 在拓扑中分发处理任务占用Experience Manager实例。 通过卸载，您可以使用特定Experience Manager实例执行特定类型的处理。 专用处理使您能够最大限度地利用可用的服务器资源。

拓扑是参与卸载的松耦合Experience Manager群集。 群集由一个或多个Experience Manager服务器实例（单个实例被视为群集）组成。

有关如何视图或修改拓扑成员关系的详细信息，请参阅管理拓 [扑部分](/help/sites-deploying/offloading.md#administering-topologies) 。

### 配置欢迎控制台 {#configuring-the-welcome-console}

经典UI的欢迎控制台提供指向AEM中各控制台和功能的链接列表。

可以配置可见的链接，有关更多详细信 [息，请参阅配置欢](/help/sites-developing/customizing-the-welcome-console.md) 迎控制台。

### 性能配置 {#configuring-for-performance}

[绩效](/help/sites-deploying/configuring-performance.md) 是您的项目的关键。 可以配置AEM（和／或基础存储库）的某些方面以优化性能。

有关更 [多详细信息](/help/sites-deploying/configuring-performance.md#configuring-for-performance) ，请参阅配置性能。

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Shared Data Store {#shared-data-store}

存储库数据存储器用于将大型二进制文件的存储从存储库的适当区域卸载到单独区域，以便在存储库树内存储同一二进制文件（例如图像）的多个实例只存储一次。

此“存储一次、多次引用”功能可扩展为不仅提供单个存储库树，还提供完全独立的存储库，方法是将每个存储库的数据存储配置为引用同一共享文件系统位置。

这样的数据存储可以在同一群集中的不同节点之间共享，在同一安装中可以在不同的发布和／或作者实例之间共享，甚至可以在不同的安装中在完全不同的实例之间共享。

有关详细信息，请参 [阅配置数据存储和节点存储](/help/sites-deploying/data-store-config.md)。

## 更多配置注意事项 {#further-configuration-considerations}

### 启用HTTP over SSL {#enabling-http-over-ssl}

您可以启用HTTP over SSL，以使用更安全的服务器连接。

有关更 [多详细信息，请参](/help/sites-administering/ssl-by-default.md) 阅启用HTTP over SSL。

### AEM门户和Portlet {#aem-portals-and-portlets}

门户是一个Web应用程序，它提供个性化、单一登录、来自不同来源的内容集成，并托管信息系统的表示层。 portlet组件还允许您在页面上嵌入portlet。 要访问CQ5 WCM提供的内容，可以为门户服务器配置CQ5门户Director门户Portlet。 为此，可以通过安装、配置portlet并将portlet添加到门户页面。

有关更 [多详细信息](/help/sites-administering/aem-as-portal.md) ，请参阅门户和Portlet。

### 静态对象的过期 {#expiration-of-static-objects}

静态对象（例如，图标）不会更改。 因此，应配置系统，使其不会过期（在合理的时间段内），从而减少不必要的流量。

有关更 [多详细信息，请参](/help/sites-deploying/expiration-static-objects.md) 阅静态对象过期。

### 在Java进程中打开FIle {#open-files-in-the-java-process}

每个Java进程都可以访问文件——这需要系统资源。 因此，将每个进程允许并发访问的文件数定义为上限。 如果超出此限制，则可能发生异常错误。

如果AEM进程超出此最大值，则消息“ ” `too many open files`将在中显示 `error.log`。

要避免此类例外，您需要：

1. 检查AEM进程正在使用的打开文件数。

   如何进行此检查取决于您的实例运行的平台。 可使用诸如lsof(Unix)或进程资源管理器(Windows)等实用程序。

   在开发和测试过程中应监控此值，以：

   * 确认根据需要关闭文件
   * 确定所需的最大值（在各种情况下）

1. 设置允许的最大值。

   新值应同时满足当前需求和将来的任何高峰，因此最好多次当前需求。

   默认情况 `serverctl` 下， `CQ_MAX_OPEN_FILES` 配置 `8192`为；对于大多数情况，这应该足够。

### 配置富文本编辑器 {#configuring-the-rich-text-editor}

富文 **本编辑器** (**RTE**)为作者提供了各种功能 [来编辑其文](/help/sites-authoring/rich-text-editor.md) 本内容；为他们提供“所见即所得”体验的图标、选择框和菜单。

有关 [更多详细信息，请参阅](/help/sites-administering/rich-text-editor.md) “配置富文本编辑器”。

### 为页面编辑配置撤消 {#configuring-undo-for-page-editing}

有几个属性可控制用于编辑页面的撤消和重做命令的行为。 可以配置这些属性，有关更 [多详细信息，请参阅配置](/help/sites-administering/config-undo.md) “为页面编辑撤消”。

### 配置视频组件 {#configuring-the-video-component}

The [Video component](/help/sites-authoring/default-components-foundation.md#video) allows you to place a predefined, out-of-the-box video element on your page.

为了进行正确转码，您的管理员必须单独[安装 FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg)。They can also [Configure your Video Profiles](/help/sites-administering/config-video.md#configure-video-profiles) for use with html5 elements.

### 配置和自定义报告 {#configuring-and-customizing-reports}

为了帮助您监视和分析实例的状态，CQ提供了一系列默认报告选项，这些报告可以根据您的具体要求进行配置：

有关更多详 [细信息，请参阅报表自定](/help/sites-administering/reporting.md#the-basics-of-report-customization) 义基础知识。

### 配置电子邮件通知 {#configuring-email-notification}

CQ向以下用户发送电子邮件通知：

* 已订阅页面事件，例如修改或复制。
* 已订阅论坛事件。
* 必须在工作流中执行一个步骤。

有关更多 [详细信息，请参阅](/help/sites-administering/notification.md) “配置电子邮件通知”。

### 启用页面展示次数 {#enabling-page-impressions}

页面展示次数显示在经 **典UI** siteadmin控制台的“展示次数”列中。 要启用页面展示次数的捕获，您需要配置：

* 在发布实例上：

   * [Day CQ WCM页面统计信息](/help/sites-deploying/osgi-configuration-settings.md)

* 在作者实例中：

   * [Adobe页面印象跟踪](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>在创作环境上配置Adobe页面印象跟踪器将允许对跟踪服务进行匿名请求。

