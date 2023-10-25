---
title: 基本配置概念
description: 了解如何根据您自己的特定要求配置Adobe Experience Manager。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
source-git-commit: c7c32130a3257c14c98b52f9db31d80587d7993a
workflow-type: tm+mt
source-wordcount: '2116'
ht-degree: 1%

---

# 基本配置概念{#basic-configuration-concepts}

Adobe Experience Manager (AEM)安装时使用了所有参数的默认设置，这些设置允许它“开箱即用”。 但是，您可以根据自己的特定要求配置AEM。

AEM有许多方面可以配置：

* 有些是 [通常为每个项目安装配置](#primary-configuration-considerations) 并且必须查看以确认它们是否适用于您的项目。
* [其他配置](#further-configuration-considerations) 可能很常见，但不是必须的；与功能或系统性能和稳定性相关。
* 而其他则仅对于AEM的某些可选功能是必需的（这些功能与相应的功能一起进行记录）。

根据特定配置，可以使用以下任一方式作出这些更改：

* **Adobe CQ Web控制台**

  这是配置OSGi捆绑包和服务的标准位置。

  请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解更多详细信息和建议的做法。

* **存储库**

  存储库中提供了OSGi配置的子集。 这可以确保复制或复制存储库内容重新创建相同的配置。 您还可以将自己的配置（取决于运行模式）添加到存储库中。

  请参阅 [存储库中的OSGi配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) 尤其是 [向存储库添加新配置](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) 以了解更多详细信息。

* **文件系统**

  一些配置文件驻留在文件系统中。

* **AEM WCM**

  可以在AEM WCM本身中配置各个方面，其中许多方面使用 [工具](/help/sites-administering/tools-consoles.md) 控制台；例如，复制代理。

>[!NOTE]
>
>使用Adobe Experience Manager时，可通过多种方法管理OSGi服务的配置设置（控制台或存储库节点）。
>
>请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解全部详细信息。

>[!NOTE]
>
>配置AEM非常简单。 但是，请注意，某些更改可能会对应用程序产生重大影响。 因此，在开始配置AEM之前，请确保您拥有必要的经验和知识，并仅做出您知道是必要的更改。 通过OSGi控制台所做的任何更改包括 **立即** 应用于正在运行的系统（无需重新启动）。

## 主要配置注意事项 {#primary-configuration-considerations}

此列表详细列出了每个新项目通常配置的主要区域。 并非所有列表都是必需的，但必须阅读并查看列表以了解哪些内容适用于您的项目。

该列表简要概述了每个配置方面，并提供了指向提供完整详细信息的页面的链接。

### 安全核对清单 {#security-checklist}

中列出了几个关键配置问题 [安全核对清单](/help/sites-administering/security-checklist.md). 请务必阅读本文，并采取安装所需的任何措施。

### 配置默认UI — 触屏优化或经典 {#configuring-the-default-ui-touch-optimized-or-classic}

在AEM中有两个UI可供使用：

* 触控优化的UI
* 经典UI

您可以使用配置所需的UI [根映射](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>有关选择UI的更多信息，请参阅 [选择您的UI](/help/sites-authoring/select-ui.md).

### IPv4和IPv6 {#ipv-and-ipv}

AEM的所有元素（例如，存储库和Dispatcher）都可以安装在IPv4和IPv6网络中。

操作是无缝的，无需特殊配置，需要时您只需使用适合您网络类型的格式指定IP地址即可。

这意味着当必须指定IP地址时，您可以根据需要从以下项中选择：

* IPv6地址

  例如 `https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4地址

  例如 `https://123.1.1.4:4502`

* 服务器名称

  例如， `https://www.yourserver.com:4502`

* 默认大小写 `localhost` 将对IPv4和IPv6网络安装进行解释

  例如， `http://localhost:4502`

### 版本清除 {#version-purging}

在标准安装中，每当激活页面时（更新内容后），AEM都会创建页面或节点的版本。 您还可以使用以下功能根据请求创建其他版本 **版本控制** 替他搭便车。 所有这些版本都存储在存储库中，如有必要，可以恢复。

这些版本永远不会被清除，因此存储库的大小会随着时间的推移而增长，因此必须对其进行管理。

请参阅 [版本清除](/help/sites-deploying/version-purging.md) 详细内容，特别是 [版本管理器](/help/sites-deploying/version-purging.md#version-manager) 了解有关如何配置AEM以在创建新版本时清除旧版本的详细信息。

### 日志记录 {#logging}

通过AEM，您可以配置：

* 中央日志记录服务的全局参数
* 请求数据记录；请求信息的专用记录配置
* 各个服务的特定设置；例如，单个日志文件以及日志消息的格式

请参阅 [记录](/help/sites-deploying/configure-logging.md) 以了解全部详细信息。

### 运行模式 {#run-modes}

运行模式允许您针对特定目的调整AEM实例。 例如，创作或发布、测试、开发或Intranet等。

这是通过为每个运行模式定义配置参数集合来完成的。 基本配置参数集将应用于所有运行模式，然后您可以根据特定环境的目的调整其他配置参数集。 然后根据需要应用这些变量。

所有配置设置都存储在一个存储库中，并通过设置 **运行模式**.

请参阅 [运行模式](/help/sites-deploying/configure-runmodes.md) 以了解全部详细信息。

### 单点登录 {#single-sign-on}

单点登录(SSO)允许用户在提供一次身份验证凭据（如用户名和密码）后访问多个系统。 独立的系统（称为可信验证器）执行验证并向Experience Manager提供用户凭据。 Experience Manager会检查并强制实施用户的访问权限（即确定允许用户访问的资源）。

请参阅 [单点登录](/help/sites-deploying/single-sign-on.md) 以了解更多详细信息。

### 资源映射 {#resource-mapping}

资源映射用于为AEM定义重定向、虚URL和虚拟主机。

例如，您可以使用这些映射执行以下操作：

* 为所有请求添加前缀 `/content` 以便对网站的访客隐藏内部结构。
* 定义一个重定向，以便所有请求都指向 `/content/en/gateway` 您的网站页面将被重定向到 `https://gbiv.com/`.

请参阅 [资源映射](/help/sites-deploying/resource-mapping.md) 以了解更多详细信息。

### 复制、反向复制和复制代理 {#replication-reverse-replication-and-replication-agents}

复制代理在AEM中占有重要地位，因为其机制可用于：

* [发布（激活）](/help/sites-authoring/publishing-pages.md) 内容从创作环境到发布环境。
* 显式刷新Dispatcher缓存中的内容。
* 从发布环境将用户输入（例如，表单输入）返回到创作环境（在创作环境的控制下）。

有关更多详细信息，请参阅 [复制](/help/sites-deploying/replication.md).

### osgi配置设置 {#osgi-configuration-settings}

[osgi](https://www.osgi.org/) 是AEM技术栈栈中的基本元素。 它用于控制AEM的复合捆绑包及其配置。

请参阅 [osgi配置设置](/help/sites-deploying/osgi-configuration-settings.md) 以获取与项目实施相关的各种捆绑包的列表（按捆绑包列出）。 并非列出的所有设置都需要调整，这里提到了一些设置以帮助您了解AEM的运行方式。

使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解更多详细信息和建议的做法。

### 配置LDAP {#configuring-ldap}

要验证存储在（中央）LDAP目录（如Active Directory）中的用户，需要LDAP身份验证。 这有助于减少管理用户帐户所需的工作。

LDAP身份验证在存储库级别进行，因此它直接由存储库处理。 有关更多详细信息，请参阅 [使用AEM配置LDAP](/help/sites-administering/ldap-config.md).

有关AEM中的用户管理（包括访问权限的分配），请参阅 [用户管理和安全性](/help/sites-administering/security.md).

### 配置Dispatcher {#configuring-the-dispatcher}

Dispatcher是Adobe Experience Manager的用于缓存和/或负载平衡的工具。 它可以与企业级Web服务器一起使用。

请参阅 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans) 详细内容，特别是 [配置Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans) 以了解更多配置详细信息。

### 配置AEMLiveCycle连接器 {#configuring-aem-livecycle-connector}

随着AEM Doc Services和AEM Doc Security的发布，AEM现在能够调用LiveCycle文档服务来呈现XFA表单、将文档转换为PDF以及策略保护文档。 请参阅 [AEMLiveCycle连接器](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html) 以了解更多详细信息。

### 作业卸载和拓扑管理 {#job-offloading-and-topology-administration}

[卸载](/help/sites-deploying/offloading.md) 在拓扑中的Experience Manager实例之间分发处理任务。 通过卸载，您可以使用特定的Experience Manager实例来执行特定类型的处理。 专业化的处理使您能够最大限度地利用可用的服务器资源。

拓扑是参与卸载的松散耦合Experience Manager集群。 集群由一个或多个Experience Manager服务器实例组成（单个实例被视为集群）。

有关如何查看或修改拓扑成员资格的详细信息，请参阅 [管理拓扑](/help/sites-deploying/offloading.md#administering-topologies) 部分。

### 配置欢迎控制台 {#configuring-the-welcome-console}

经典UI的欢迎控制台提供了指向AEM中各种控制台和功能的链接列表。

可以配置可见的链接，请参见 [配置欢迎控制台](/help/sites-developing/customizing-the-welcome-console.md) 以了解更多详细信息。

### 配置性能 {#configuring-for-performance}

[性能](/help/sites-deploying/configuring-performance.md) 是您项目的关键。 可以配置AEM的某些方面（和/或底层存储库）以优化性能。

请参阅 [配置性能](/help/sites-deploying/configuring-performance.md#configuring-for-performance) 以了解更多详细信息。

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### 共享数据存储 {#shared-data-store}

存储库数据存储用于将大型二进制文件的存储从存储库中卸载到单独的区域，以便存储库树中同一二进制文件的多个实例（例如图像）只存储一次。

通过将每个存储库的数据存储配置为引用同一共享文件系统位置，可以扩展此“一次存储，多次引用”功能，使其不仅服务于单个存储库树，而且服务于完全不同的存储库。

此类数据存储可以在同一群集中的不同节点、同一安装中的不同发布和/或创作实例之间共享，甚至可以在不同安装中的完全不同的实例之间共享。

有关更多信息，请参阅 [配置数据存储和节点存储](/help/sites-deploying/data-store-config.md).

## 其他配置注意事项 {#further-configuration-considerations}

### 启用HTTP over SSL {#enabling-http-over-ssl}

您可以启用HTTP over SSL以采用与服务器的更安全连接。

请参阅 [启用HTTP over SSL](/help/sites-administering/ssl-by-default.md) 以了解更多详细信息。

### AEM Portals和Portlet {#aem-portals-and-portlets}

门户是一种Web应用程序，它提供个性化、单点登录、来自不同来源的内容集成，并承载信息系统的表示层。 利用portlet组件，还可以在页面上嵌入portlet。 要访问CQ5 WCM提供的内容，可以为门户服务器安装CQ5 Portal Director Portlet。 为此，您可以安装、配置Portlet并将其添加到门户页面。

请参阅 [门户和Portlet](/help/sites-administering/aem-as-portal.md) 以了解更多详细信息。

### 静态对象过期 {#expiration-of-static-objects}

静态对象（例如图标）不会更改。 因此，系统应配置为它们不会过期（在合理的时间段内），从而减少不必要的流量。

请参阅 [静态对象过期](/help/sites-deploying/expiration-static-objects.md) 以了解更多详细信息。

### 在Java™进程中打开文件 {#open-files-in-the-java-process}

每个Java™进程都可以访问文件 — 这需要系统资源。 因此，上限被定义为每个进程可以同时访问的文件数。 如果超出此限制，则可能会发生异常错误。

如果AEM进程超过此最大值，则消息&#39;&#39; `too many open files`”在中显示 `error.log`.

要避免此类例外，请执行以下操作：

1. 检查AEM进程正在使用多少个打开的文件。

   此检查取决于实例运行的平台。 可以使用诸如lsof (UNIX®)或Process Explorer (Windows)之类的实用程序。

   在开发和测试过程中应监控此值，以便：

   * 确认正在根据需要关闭文件
   * 以确定所需的最大值（在各种情况下）

1. 设置允许的最大值。

   新值应同时满足当前需求和任何未来峰值，因此建议将当前需求增加一倍。

   默认情况下， `serverctl` 配置 `CQ_MAX_OPEN_FILES` 到 `8192`；这应该足以满足大多数场景。

### 配置富文本编辑器 {#configuring-the-rich-text-editor}

此 **富文本编辑器** (**RTE**)为作者提供了范围广泛的 [功能](/help/sites-authoring/rich-text-editor.md) 用于编辑其文本内容；为它们提供用于所见即所得体验的图标、选择框和菜单。

请参阅 [配置富文本编辑器](/help/sites-administering/rich-text-editor.md) 以了解更多详细信息。

### 配置撤消以进行页面编辑 {#configuring-undo-for-page-editing}

有几个属性控制用于编辑页面的撤消和重做命令的行为。 这些组件可以配置，请参见 [配置撤消以进行页面编辑](/help/sites-administering/config-undo.md) 以了解更多详细信息。

### 配置视频组件 {#configuring-the-video-component}

此 [视频组件](/help/sites-authoring/default-components-foundation.md#video) 让您能够在页面上放置预定义的、现成的视频元素。

为了进行正确的转码，您的管理员必须 [安装FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) 单独。 他们也可以 [配置您的视频配置文件](/help/sites-administering/config-video.md#configure-video-profiles) 与html5元素一起使用。

### 配置和自定义报表 {#configuring-and-customizing-reports}

为了帮助您监视和分析实例的状态，CQ提供了一系列默认报表，您可以根据自己的要求对这些报表进行配置：

请参阅 [报表自定义的基础知识](/help/sites-administering/reporting.md#the-basics-of-report-customization) 以了解更多详细信息。

### 配置电子邮件通知 {#configuring-email-notification}

CQ会向符合以下条件的用户发送电子邮件通知：

* 已订阅页面事件，例如修改或复制。
* 已订阅论坛活动。
* 必须在工作流中执行步骤。

请参阅 [配置电子邮件通知](/help/sites-administering/notification.md) 以了解更多详细信息。

### 启用页面展示 {#enabling-page-impressions}

页面展示次数显示在 **展示次数** 经典UI siteadmin console的列。 要启用页面展示次数捕获，请配置以下内容：

* 在发布实例上：

   * [Day CQ WCM页面统计信息](/help/sites-deploying/osgi-configuration-settings.md)

* 在创作实例上：

   * [Adobe页面展示次数跟踪器](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>在创作环境中配置Adobe页面展示次数跟踪器可允许匿名请求跟踪服务。
