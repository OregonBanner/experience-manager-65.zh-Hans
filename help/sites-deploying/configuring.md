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
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2133'
ht-degree: 1%

---

# 基本配置概念{#basic-configuration-concepts}

Adobe Experience Manager(AEM)随所有参数的默认设置一起安装，这允许其“开箱即用”运行。 但是，您可以根据自己的特定要求配置AEM。

可以配置AEM的许多方面：

* 有些是[通常为每个项目安装配置的](#primary-configuration-considerations)，必须进行审核以确认它们是否适用于您的项目。
* [进一步](#further-configuration-considerations) 配置可能很常见，但并非势在必行；与功能或系统性能和稳定性相关。
* 其他功能仅对AEM的某些可选功能是必需的（这些功能与相应的功能一起记录）。

根据特定配置，可以使用以下任一方式进行这些更改：

* **Adobe CQ Web Console**

   这是配置OSGi包和服务的标准位置。

   有关更多详细信息和建议的实践，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md) 。

* **存储库**

   存储库中提供了OSGi配置的子集。 这可确保复制或复制存储库内容重新创建相同的配置。 您还可以根据运行模式将自己的配置添加到存储库。

   有关更多详细信息，请参阅存储库](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)中的[OSGi配置，特别是[向存储库](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)添加新配置。

* **文件系统**

   文件系统中存在一些配置文件。

* **AEM WCM**

   可以在AEM WCM本身中配置各种方面，许多方面都使用[Tools](/help/sites-administering/tools-consoles.md)控制台；例如，复制代理。

>[!NOTE]
>
>使用Adobe Experience Manager时，可以使用多种方法来管理OSGi服务（控制台或存储库节点）的配置设置。
>
>有关完整的详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md) 。

>[!NOTE]
>
>配置AEM非常简单，但您必须注意：
>
>某些更改可能会对应用程序产生重大影响。 因此，在开始配置AEM之前，请确保您拥有必要的经验和知识，并且只进行您知道需要的更改。 通过OSGi控制台所做的任何更改都将&#x200B;**立即**&#x200B;应用于正在运行的系统（无需重新启动）。

## 主要配置注意事项{#primary-configuration-considerations}

此列表详细列出了每个新项目通常配置的主要区域。 并非所有项目都需要，但必须阅读并审核列表，才能查看适用于您的项目的内容。

该列表简要概述了每个配置方面，以及指向提供完整详细信息的页面的链接。

### 安全检查列表{#security-checklist}

[安全检查表](/help/sites-administering/security-checklist.md)中列出了几个关键配置问题。 请确保您已阅读本文，并对安装采取任何必要的措施。

### 配置默认UI — 触屏优化或经典{#configuring-the-default-ui-touch-optimized-or-classic}

有两个UI可在AEM中使用：

* 触屏优化UI
* 经典 UI

您可以使用[根映射](/help/sites-deploying/osgi-configuration-settings.md)配置所需的UI。

>[!NOTE]
>
>有关选择UI的更多信息，请参阅[选择UI](/help/sites-authoring/select-ui.md)下。

### IPv4和IPv6 {#ipv-and-ipv}

AEM的所有元素（例如存储库、调度程序等）都可以安装在IPv4和IPv6网络中。

操作是无缝的，因为不需要特殊配置，在需要时，您只需使用适合您的网络类型的格式指定IP地址即可。

这意味着当需要指定IP地址时，您可以（根据需要）从以下位置进行选择：

* IPv6地址

   例如`https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4地址

   例如`https://123.1.1.4:4502`

* 服务器名称

   例如，`https://www.yourserver.com:4502`

* 对于IPv4和IPv6网络安装，将解释`localhost`的默认情况

   例如，`http://localhost:4502`

### 版本清除{#version-purging}

在标准安装中，每当您激活页面（更新内容后）时，AEM都会创建页面或节点的新版本。您还可以使用Sidekick的&#x200B;**版本控制**&#x200B;选项卡，根据请求创建其他版本。 所有这些版本都存储在存储库中，并可以在需要时还原。

这些版本从未清除过，因此存储库大小会随着时间的推移而增加，因此需要进行管理。

有关完整的详细信息，请参阅[版本清除](/help/sites-deploying/version-purging.md)，特别是[版本管理器](/help/sites-deploying/version-purging.md#version-manager)，以详细了解如何配置AEM以在创建新版本时清除旧版本。

### 记录 {#logging}

AEM允许您配置：

* 中央日志记录服务的全局参数
* 请求数据记录；请求信息的专用日志记录配置
* 具体设置；例如，单个日志文件和日志消息的格式

有关完整的详细信息，请参阅[日志记录](/help/sites-deploying/configure-logging.md)。

### 运行模式 {#run-modes}

运行模式允许您针对特定目的调整AEM实例；例如，创作或发布、测试、开发或内部网等。

这是通过为每个运行模式定义配置参数集合来完成的。 所有运行模式都应用一组基本的配置参数，然后您可以根据特定环境的目的调整其他集。 然后，会根据需要应用这些值。

所有配置设置都存储在一个存储库中，并通过设置&#x200B;**运行模式**&#x200B;来激活。

有关完整的详细信息，请参阅[运行模式](/help/sites-deploying/configure-runmodes.md)。

### 单点登录{#single-sign-on}

单点登录(SSO)允许用户在提供一次身份验证凭据（如用户名和密码）后访问多个系统。 单独的系统（称为受信任的验证器）执行验证并提供Experience Manager和用户凭据。 Experience Manager检查并强制用户访问权限（即确定允许用户访问哪些资源）。

有关更多详细信息，请参阅[单点登录](/help/sites-deploying/single-sign-on.md) 。

### 资源映射{#resource-mapping}

资源映射用于定义AEM的重定向、虚URL和虚拟主机。

例如，您可以将以下映射用于：

* 为所有请求添加`/content`前缀，以便隐藏网站访客的内部结构。
* 定义重定向，以便所有到网站`/content/en/gateway`页面的请求都被重定向到`https://gbiv.com/`。

有关更多详细信息，请参阅[资源映射](/help/sites-deploying/resource-mapping.md) 。

### 复制、反向复制和复制代理{#replication-reverse-replication-and-replication-agents}

复制代理是AEM的核心，它是用于：

* [将](/help/sites-authoring/publishing-pages.md) 内容从创作发布（激活）到发布环境。
* 显式刷新Dispatcher缓存中的内容。
* 将用户输入（例如，表单输入）从发布环境返回到创作环境（在创作环境的控制下）。

有关更多详细信息，请参阅[Replication](/help/sites-deploying/replication.md)。

### OSGi配置设置{#osgi-configuration-settings}

[](https://www.osgi.org/) OSG是AEM技术堆栈中的一个基本元素。它用于控制AEM的复合包及其配置。

有关与项目实施相关的各种包的列表（按包列出），请参阅[OSGi配置设置](/help/sites-deploying/osgi-configuration-settings.md)。 列出的设置并非都需要调整，其中有些设置可帮助您了解AEM的操作方式。

使用AEM时，可通过多种方法来管理此类服务的配置设置；有关更多详细信息和建议的实践，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md) 。

### 配置LDAP {#configuring-ldap}

要验证存储在（中央）LDAP目录（如Active Directory）中的用户，需要LDAP身份验证。 这有助于减少管理用户帐户所需的工作。

LDAP身份验证在存储库级别进行，因此它由存储库直接处理。 有关更多详细信息，请参阅[使用AEM](/help/sites-administering/ldap-config.md)配置LDAP。

有关AEM中的用户管理（包括访问权限的分配），请参阅[用户管理和安全](/help/sites-administering/security.md)。

### 配置Dispatcher {#configuring-the-dispatcher}

Dispatcher是Adobe Experience Manager的缓存和/或负载平衡工具，可与企业级Web服务器结合使用。

有关完整详细信息，请参阅[Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)，特别是[配置Dispatcher](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html) ，以了解更多配置详细信息。

### 配置AEMLiveCycle连接器{#configuring-aem-livecycle-connector}

随着AEM文档服务和AEM文档安全的发布，我们现在能够调用LiveCycle文档服务来呈现XFA表单、将文档转换为PDF并保护文档的策略。 有关更多详细信息，请阅读[AEMLiveCycle连接器](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html)。

### 作业卸载和拓扑管理{#job-offloading-and-topology-administration}

[](/help/sites-deploying/offloading.md) 卸载在拓扑中分发相当于Experience Manager实例的处理任务。通过卸载，您可以使用特定的Experience Manager实例来执行特定类型的处理。 通过专业化的处理，您可以最大限度地利用可用的服务器资源。

拓扑是参与卸载的松散耦合的Experience Manager群集。 群集由一个或多个Experience Manager服务器实例（单个实例被视为群集）组成。

有关如何查看或修改拓扑成员资格的详细信息，请参阅[管理拓扑](/help/sites-deploying/offloading.md#administering-topologies)一节。

### 配置欢迎控制台{#configuring-the-welcome-console}

经典UI的“欢迎”控制台提供了指向AEM中各种控制台和功能的链接列表。

可以配置可见的链接，有关更多详细信息，请参阅[配置欢迎控制台](/help/sites-developing/customizing-the-welcome-console.md) 。

### 性能{#configuring-for-performance}配置

[](/help/sites-deploying/configuring-performance.md) 性能是您项目的关键。可以对AEM的某些方面（和/或基础存储库）进行配置以优化性能。

有关更多详细信息，请参阅[性能配置](/help/sites-deploying/configuring-performance.md#configuring-for-performance) 。

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### 共享数据存储{#shared-data-store}

存储库数据存储用于将大二进制文件的存储从存储库的适当位置卸载到单独的区域，以便存储库树内同一二进制文件（例如图像）的多个实例只存储一次。

通过将每个存储库的数据存储配置为引用同一共享文件系统位置，可以扩展此“存储一次、多次引用”功能，以便不仅提供单个存储库树，还提供完全独立的存储库。

此类数据存储可以在同一群集中的不同节点、同一安装中的不同发布和/或创作实例之间共享，甚至可以在不同安装中完全独立的实例之间共享。

有关更多信息，请参阅[配置数据存储和节点存储](/help/sites-deploying/data-store-config.md)。

## 进一步配置注意事项{#further-configuration-considerations}

### 通过SSL启用HTTP {#enabling-http-over-ssl}

您可以启用HTTP over SSL以使用与服务器的更安全连接。

有关更多详细信息，请参阅[启用HTTP over SSL](/help/sites-administering/ssl-by-default.md)。

### AEM门户和Portlet {#aem-portals-and-portlets}

门户是一个Web应用程序，它提供个性化、单点登录、来自不同来源的内容集成，并托管信息系统的表示层。 Portlet组件还允许您在页面上嵌入Portlet。 要访问由CQ5 WCM提供的内容，可以为门户服务器安装CQ5门户Director Portlet。 为此，您可以安装、配置Portlet并将其添加到门户页面。

有关更多详细信息，请参阅[Portal和Portlet](/help/sites-administering/aem-as-portal.md) 。

### 静态对象{#expiration-of-static-objects}的过期

静态对象（例如，图标）不会发生更改。 因此，应该配置系统，以便它们不会过期（在合理的时间段内），从而减少不必要的流量。

有关更多详细信息，请参阅[静态对象的过期时间](/help/sites-deploying/expiration-static-objects.md)。

### 在Java进程{#open-files-in-the-java-process}中打开FIle

每个java进程都可以访问文件 — 这需要系统资源。 因此，对允许每个进程同时访问的文件数定义了上限。 如果超出此限制，则可能发生异常错误。

如果AEM进程超出此最大值，则将在`error.log`中看到消息“ `too many open files`”。

要避免此类例外，您需要：

1. 检查您的AEM进程正在使用的打开文件数。

   您如何进行此检查取决于您的实例运行的平台。 可以使用lsof(Unix)或Process Explorer(Windows)等实用程序。

   在开发和测试期间应监控此值，以：

   * 确认文件已根据需要关闭
   * 确定所需的最大值（在各种情况下）

1. 设置允许的最大值。

   新值应同时满足当前需求和未来任何峰值，因此建议将当前需求加倍。

   默认情况下， `serverctl`将`CQ_MAX_OPEN_FILES`配置为`8192`;对于大多数情况，这应该足够了。

### 配置富文本编辑器{#configuring-the-rich-text-editor}

**富文本编辑器**(**RTE**)为作者提供了广泛的[功能](/help/sites-authoring/rich-text-editor.md)来编辑其文本内容；为他们提供图标、选择框和菜单，以体验所见即所得的体验。

有关更多详细信息，请参阅[配置富文本编辑器](/help/sites-administering/rich-text-editor.md) 。

### 为页面编辑配置撤消{#configuring-undo-for-page-editing}

有几个属性可控制用于编辑页面的撤消和重做命令的行为。 有关更多详细信息，请参阅[为页面编辑配置撤消](/help/sites-administering/config-undo.md) 。

### 配置视频组件{#configuring-the-video-component}

[视频组件](/help/sites-authoring/default-components-foundation.md#video)允许您在页面上放置一个预定义的现成视频元素。

为了进行正确转码，您的管理员必须单独[安装 FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg)。它们还可以[配置视频配置文件](/help/sites-administering/config-video.md#configure-video-profiles)以与html5元素一起使用。

### 配置和自定义报表{#configuring-and-customizing-reports}

为帮助您监控和分析实例的状态，CQ提供了一系列默认报表选项，这些报表可根据您的各个要求进行配置：

有关更多详细信息，请参阅[报表自定义基础知识](/help/sites-administering/reporting.md#the-basics-of-report-customization)。

### 配置电子邮件通知{#configuring-email-notification}

CQ会向以下用户发送电子邮件通知：

* 已订阅页面事件，例如修改或复制。
* 已订阅论坛活动。
* 必须在工作流中执行步骤。

有关更多详细信息，请参阅[配置电子邮件通知](/help/sites-administering/notification.md)。

### 启用页面展示次数{#enabling-page-impressions}

页面展示次数显示在经典UI站点管理控制台的&#x200B;**展示次数**&#x200B;列中。 要启用页面展示次数的捕获，您需要配置：

* 在发布实例上：

   * [Day CQ WCM页面统计信息](/help/sites-deploying/osgi-configuration-settings.md)

* 在创作实例上：

   * [Adobe页面展示次数跟踪](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>在创作环境中配置Adobe页面展示次数跟踪器将允许对跟踪服务进行匿名请求。
