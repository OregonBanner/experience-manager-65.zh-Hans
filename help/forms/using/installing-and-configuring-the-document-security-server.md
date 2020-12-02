---
title: 安装和配置文档安全服务器
seo-title: 安装和配置文档安全服务器
description: '使用文档安全性安全地分发您以支持的格式保存的任何信息。 只有授权用户才能访问受保护的文档。 '
seo-description: '使用文档安全性安全地分发您以支持的格式保存的任何信息。 只有授权用户才能访问受保护的文档。 '
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---


# 安装和配置文档安全服务器{#installing-and-configuring-the-document-security-server}

使用文档安全性安全地分发您以支持的格式保存的任何信息。 只有授权用户才能访问受保护的文档。

Adobe Experience Manager Forms文档安全确保只有授权用户才能使用您的文档。 使用文档安全性，您可以安全地分发以支持的格式保存的任何信息。 支持的文件格式包括Adobe可移植文档格式(PDF)和Microsoft Word、Excel和PowerPoint文件。

您可以使用策略保护文档。 您在策略中指定的机密性设置决定了收件人如何使用您应用策略的文档。 例如，您可以指定收件人是否可以打印或复制文本、编辑文本，或向受保护的文档添加签名和注释。

策略存储在文档安全服务器上；您可以通过客户端应用程序将策略应用于文档。 对文档应用策略时，策略中指定的机密性设置将保护文档包含的信息。 您可以将受策略保护的文档分发给受策略授权的收件人。

文档安全性还为客户端、查看器和索引器提供保护，保护文档、视图保护文档和索引受保护文档。 有关文档安全的详细信息，请参见[关于文档安全](/help/forms/using/admin-help/document-security.md)。

## 部署拓扑{#deployment-topology}

文档安全功能仅在JEE的AEM Forms可用。 您只需在JEE上使用AEM Forms的单个实例。 如有必要，您还可以创建AEM Forms服务器的群集或群。 以下拓扑是指示性拓扑，用于运行文档安全功能。 有关拓扑的详细信息，请参见[AEM Forms](aem-forms-architecture-deployment.md)的架构和部署拓扑。

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

下图显示了AEM Forms文档安全的典型架构：

![](do-not-localize/document-security-typical-environment.png)

## 在JEE上安装AEM Forms{#installing-aem-forms-on-jee}

执行以下步骤在JEE上安装和配置AEM Forms:

1. 从[Adobe授权许可网站(LWS)](https://licensing.adobe.com/)下载AEM 6.5Forms的JEE安装程序。 您需要签订有效的维护和支持合同才能下载安装程序。
1. 请阅读[AEM Forms在JEE支持的平台上的文档](/help/forms/using/aem-forms-jee-supported-platforms.md)，并确保已准备好在JEE上安装软件、硬件、操作系统、应用程序服务器、数据库、JDK和其他基础架构。
1. （仅限Non-Turnkey安装）阅读[准备安装AEM Forms单服务器](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64)或[准备安装AEM Forms服务器群集](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64)，并准备环境在JEE上安装和配置AEM Forms。
1. 根据您的环境和应用程序服务器，选择以下文档之一，然后按照说明完成安装

   * [在JEE上使用JBoss统包安装和部署AEM Forms](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [在JEE上安装和部署JBoss的AEM Forms](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [在WebLogic的JEE上安装和部署AEM Forms](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [在WebSphere的JEE上安装和部署AEM Forms](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [在JBoss群集上在JEE上配置AEM Forms](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [在WebLogic群集上在JEE上配置AEM Forms](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [在WebSphere群集上的JEE上配置AEM Forms](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >在JEE配置管理器上的AEM Forms的“模块选择”屏幕上，选择“文档安全”选项。 “文档安全性”选项不需要选择任何其他模块。

## 后续步骤{#next-steps}

* [配置客户端和服务器选项](/help/forms/using/admin-help/configuring-client-server-options.md)
* [创建和管理策略](/help/forms/using/admin-help/creating-policies.md)
* [创建和管理策略集](/help/forms/using/admin-help/creating-policy-sets.md)
