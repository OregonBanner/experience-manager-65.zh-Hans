---
title: 部署和维护
seo-title: Deploying and Maintaining
description: 了解如何开始安装AEM。
seo-description: Learn how to get started with the AEM installation.
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
source-git-commit: bb8dbb9069c4575af62a4d0b21195cee75944fea
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 8%

---

# 部署和维护{#deploying-and-maintaining}

在此页中，您将找到：

* [基本概念](#basic-concepts)

   * [什么是 AEM?](#what-is-aem)
   * [典型部署](#typical-deployment-scenarios)

      * [内部部署](#on-premise)
      * [Managed Services使用Cloud Manager](#managed-services-using-cloud-manager)

* [快速入门](#getting-started)

   * [前提条件](#prerequisites)
   * [获取软件](#getting-the-software)
   * [默认本地安装](#default-local-install)
   * [创作和发布安装](#author-and-publish-installs)
   * [未打包的安装目录](#unpacked-install-directory)
   * [启动和停止](#starting-and-stopping)

熟悉这些基础知识后，您将在以下子页面中找到更高级的详细信息：

* [技术要求](/help/sites-deploying/technical-requirements.md)
* [推荐的部署](/help/sites-deploying/recommended-deploys.md)
* [自定义独立安装](/help/sites-deploying/custom-standalone-install.md)
* [应用程序服务器安装](/help/sites-deploying/application-server-install.md)
* [疑难解答](/help/sites-deploying/troubleshooting.md)
* [命令行启动和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [配置](/help/sites-deploying/configuring.md)
* [升级到AEM 6.5](/help/sites-deploying/upgrade.md)
* [电子商务](/help/commerce/cif-classic/deploying/ecommerce.md)
* [配置操作方法文章](/help/sites-deploying/ht-deploy.md)
* [Web 控制台](/help/sites-deploying/web-console.md)
* [复制故障诊断](/help/sites-deploying/troubleshoot-rep.md)
* [最佳实践](/help/sites-deploying/best-practices.md)
* [部署社区](/help/communities/deploy-communities.md)
* [AEM平台简介](/help/sites-deploying/platform.md)
* [性能准则](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile 入门](/help/mobile/getting-started-aem-mobile.md)
* [什么是AEM Screens?](https://docs.adobe.com/content/help/zh-Hans/experience-manager-screens/user-guide/aem-screens-introduction.html)

## 基本概念 {#basic-concepts}

### 什么是 AEM? {#what-is-aem}

Adobe Experience Manager 是基于 Web 的客户端服务器系统，可用于构建、管理和部署商业网站及相关服务。它将多个基础架构级别和应用程序级别的功能整合到一个集成包中。

在基础架构级别， AEM提供以下功能：

* **Web应用程序服务器**:AEM可以以独立模式（包括集成的Jetty Web服务器）部署，也可以作为第三方应用程序服务器内的Web应用程序部署。
* **Web应用程序框架**:AEM整合了Sling Web应用程序框架，该框架简化了RESTful、面向内容的Web应用程序的编写。
* **内容存储库**:AEM包括Java内容存储库(JCR)，这是一种专门为非结构化和半结构化数据而设计的分层数据库。 存储库不仅存储面向用户的内容，还存储应用程序使用的所有代码、模板和内部数据。

在此基础上，AEM还提供了许多应用程序级功能，用于管理：

* **网站**
* **移动设备应用程序**
* **数字出版物**
* **表单**
* **数字资产**
* **社区**
* **在线商务**

最后，客户可以使用这些基础架构和应用程序级构建块，通过构建自己的应用程序来创建自定义的解决方案。

AEM服务器为 **基于Java** 并且在支持该平台的大多数操作系统上运行。 与AEM的所有客户端交互均通过 **Web浏览器**.

### 典型部署方案 {#typical-deployment-scenarios}

在AEM术语中，“实例”是在服务器上运行的AEM的副本。 AEM安装通常至少涉及两个实例，通常在不同的计算机上运行：

* **作者**:用于创建、上传和编辑内容以及管理网站的AEM实例。 内容准备就绪后，即会复制到发布实例。
* **发布**:向公众提供已发布内容的AEM实例。

这些实例与已安装软件相同。 它们仅通过配置进行区分。 此外，大多数安装都使用调度程序：

* **Dispatcher**:静态Web服务器(Apache httpd、Microsoft IIS等) 增强了AEM调度程序模块。 它会缓存由发布实例生成的网页，以提高性能。

此设置有许多高级选项和阐述，但大多数部署的核心是创作、发布和调度程序的基本模式。 首先，我们将专注于一个相对简单的机构。 随后将讨论高级部署选项。

以下各节介绍了两种情况：

* **内部部署**:AEM在您的公司环境中部署和管理。

* **Managed Services — 适用于Adobe Experience Manager的Cloud Manager**:AEM由Adobe Managed Services部署和管理。

### 内部部署 {#on-premise}

您可以在公司环境中的服务器上安装AEM。 典型的安装实例包括：开发、测试和发布环境。 请参阅 [快速入门](/help/sites-deploying/deploy.md#getting%20started) 部分，以了解有关如何将AEM软件安装到本地的基本详细信息。

要进一步了解典型的内部部署，请参阅 [推荐的部署](/help/sites-deploying/recommended-deploys.md).

### Managed Services使用Cloud Manager {#managed-services-using-cloud-manager}

AEM Managed Services是用于数字体验管理的完整解决方案。 它提供了云中体验交付解决方案的优势，同时保留了内部部署的所有控制、安全和自定义优势。 AEM Managed Services让客户能够通过在云上进行部署，并依赖Adobe的最佳实践和支持来加快启动速度。 组织和业务用户可以在最短的时间内吸引客户、推动市场份额，并专注于创建创新的营销活动，同时减轻IT负担。

通过AEM Managed Services，客户可以实现以下好处：

**更快的上市时间：** 借助Adobe Managed Services的灵活云基础架构，组织可以快速规划、启动和优化成功的数字体验。 Adobe无需额外的资金、硬件或软件即可管理云架构，Adobe的客户成功工程师也可以管理云架构，为连接到后端应用程序和上线最佳实践提供AEM架构、配置、自定义方面的帮助。

**性能更高：** 通过四个服务可用性选项（99.5%、99.9%、99.95%和99.99%）为您的业务提供可靠的数字体验。 此外，它还允许自动备份和多模式灾难恢复模型，以帮助确保可靠性和应急管理。

**优化了IT成本：** 前瞻性指导和专业知识可帮助组织保持最新版本的AEM。 Adobe白金维护和支持自动包含在AMS企业/基础的新部署中，提供技术专业知识和操作经验，以帮助组织维护其关键应用程序。 免费的基本Analytics或Target功能可提供额外的价值，尤其是对于对分析和个性化需求有限的中端市场组织而言。

**最高安全性：** 通过在受限访问设施中、防火墙系统后面或虚拟专用云中托管客户应用程序，可确保企业级物理、网络和数据安全。 它包括单租户虚拟机，具有强大的数据存储加密、抗病毒和数据隔离功能。

**Cloud Manager**:Cloud Manager是Adobe Experience Manager Managed Services产品的一部分，是一个自助门户，进一步允许组织在云中自行管理Adobe Experience Manager。 它包括一流的连续集成和连续交付(CI/CD)管道，使IT团队和实施合作伙伴能够在不影响性能或安全性的情况下加快自定义或更新的交付。 Cloud Manager仅适用于Adobe托管服务客户。

要详细了解Cloud Manger及其资源，请参阅 [**Cloud Manager用户指南**](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html).

## 快速入门 {#getting-started}

### 前提条件 {#prerequisites}

虽然生产实例通常在运行正式支持的操作系统的专用计算机上运行(请参阅 [技术要求](/help/sites-deploying/technical-requirements.md))，则Experience Manager服务器将实际在支持 [**Java标准版8**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

为了熟悉和在AEM上进行开发，通常使用安装在运行Apple OS X或Microsoft Windows或Linux桌面版的本地计算机上的实例。

在客户端，AEM可与所有新式浏览器(**Microsoft Edge**, **Internet Explorer** 11, **Chrome **51+** **、**Firefox **47+、 **Safari** 8+)。 请参阅 [支持的客户端平台](/help/sites-deploying/technical-requirements.md#supported-client-platforms) 以了解详细信息。

### 获取软件 {#getting-the-software}

具有有效维护和支持合同的客户应已收到包含代码的邮件通知，并能够从下载AEM [**Adobe许可网站**](https://licensing.adobe.com/). 业务合作伙伴可以请求下载 [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

AEM软件包有两个形式：

* **cq-quickstart-6.5.0.jar:** 独立可执行文件 *jar* 文件，其中包含启动和运行所需的所有内容。

* **cq-quickstart-6.5.0.war:** A *战争* 文件，以在第三方应用程序服务器中进行部署。

在以下部分中，我们将介绍 **独立安装**. 有关在应用程序服务器中安装AEM的详细信息，请参阅 [应用程序服务器安装](/help/sites-deploying/application-server-install.md).

### 默认本地安装 {#default-local-install}

1. 在本地计算机上创建安装目录。 例如：

   UNIX安装位置： **/opt/aem**

   Windows安装位置： **`C:\Program Files\aem`**

   同样，在桌面上直接将示例实例安装在文件夹中也很常见。 无论如何，我们通常将此位置称为：

   `<aem-install>`

   *请注意，文件目录的路径必须只包含美国ASCII字符。*

1. 将 **jar** 和**许可**文件：

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   如果您未提供 `license.properties` 文件， AEM会将您的浏览器重定向到 **欢迎** 屏幕，您可以在其中输入许可证密钥。 如果您尚未从Adobe请求有效的许可证密钥。

1. 要在GUI环境中启动实例，只需双击 **`cq-quickstart-6.5.0.jar`** 文件。

   或者，您也可以从命令行启动AEM:

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM需要几分钟时间才能解压缩jar文件、安装自身并启动。 上述过程导致：

* an **AEM作者** 实例
* 运行 **localhost**
* 端口 **4502**

要访问实例，请将您的浏览器指向：

**`https://localhost:4502`**

创作实例中的结果将自动配置为连接到 **发布实例** on **`localhost:4503`**.

### 创作和发布安装 {#author-and-publish-installs}

默认安装( **作者** 实例 **`localhost:4502`**)，只需重命名 `jar` 文件之前，首次启动它。 命名模式为：

**`cq-<instance-type>-p<port-number>.jar`**

例如，将文件重命名为

**`cq-author-p4502.jar`**

并启动它将导致在上运行创作实例 **`localhost:4502`**.

同样，重命名并启动文件

**`cq-publish-p4503.jar`**

将导致在上运行发布实例 **`localhost:4503`**.

例如，您需要在

`<aem-install>/author`和

**`<aem-install>/publish`**

有关自定义安装的更多详细信息，请参阅以下内容：

* [自定义独立安装](/help/sites-deploying/custom-standalone-install.md)
* [运行模式](/help/sites-deploying/configure-runmodes.md)

### 未打包的安装目录 {#unpacked-install-directory}

首次启动快速入门Jar时，它会将其解压缩到名为的新子目录下的同一目录中 `crx-quickstart`. 您最终应该具备以下功能：

```xml
<aem-install>/
    license.properties
    cq-quickstart-6.5.0.jar
    crx-quickstart/
        app/
        bin/
        conf/
        launchpad/
        logs/
        metrics/
        monitoring/
        opt/
        repository/
        threaddumps/
        eula-de_DE.html
        eula-en_US.html
        eula-fr_FR.html
        eula-ja_JP.html
        readme.txt
```

如果是从UI安装实例，则将自动打开一个浏览器窗口，并且还将打开一个桌面应用程序窗口，显示实例的主机和端口以及开/关开关：

![启动屏幕](assets/screen_shot_.png)

>[!NOTE]
>
>如果您使用符号链接，请查看 [symlink问题](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html).

### 启动和停止 {#starting-and-stopping}

在AEM解压并首次启动后，双击安装目录中的jar文件只会启动实例，它不会重新安装该实例。

要从GUI中停止实例，只需单击 **打开/关闭** 在桌面应用程序窗口上切换。

您还可以从命令行停止和启动AEM。 如果您是首次安装实例，则 **命令行脚本** 位于此处：

**`<aem-install>/crx-quickstart/bin/`**

此文件夹包含以下Unix bash shell脚本：

* **`start`**:启动实例
* `stop`:停止实例
* **`status`**:报告实例的状态
* **`quickstart`**:用于配置开始信息（如有必要）。

还有相等的 **`bat`** 文件。 有关更多详细信息，请参阅：

* [命令行启动和停止](/help/sites-deploying/command-line-start-and-stop.md)

AEM启动并自动将您的web浏览器重定向到相应的页面（通常是登录页面）；例如：

`https://localhost:4502/`

![登录屏幕](assets/screen_shot_2019-04-08at83533am.png)

登录后，您即可访问AEM。 有关更多信息，请参阅以下内容，具体取决于您的角色：

* [创作](/help/sites-authoring/home.md)
* [管理](/help/sites-administering/home.md)
* [开发](/help/sites-developing/home.md)
* [管理](/help/managing/best-practices.md)

## 高级部署 {#advanced-deployment}

通过上节，您应该可以更好地了解AEM安装的基础知识。 但是，安装AEM的完整生产系统可能涉及的复杂性要高得多。 有关高级安装的完整信息，请参阅以下子页面：

* [技术要求](/help/sites-deploying/technical-requirements.md)
* [推荐的部署](/help/sites-deploying/recommended-deploys.md)
* [自定义独立安装](/help/sites-deploying/custom-standalone-install.md)
* [应用程序服务器安装](/help/sites-deploying/application-server-install.md)
* [疑难解答](/help/sites-deploying/troubleshooting.md)
* [命令行启动和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [配置](/help/sites-deploying/configuring.md)
* [升级到AEM 6.5](/help/sites-deploying/upgrade.md)
* [电子商务](/help/commerce/cif-classic/deploying/ecommerce.md)
* [配置操作方法文章](/help/sites-deploying/ht-deploy.md)
* [Web 控制台](/help/sites-deploying/web-console.md)
* [复制故障诊断](/help/sites-deploying/troubleshoot-rep.md)
* [最佳实践](/help/sites-deploying/best-practices.md)
* [部署社区](/help/communities/deploy-communities.md)
* [AEM平台简介](/help/sites-deploying/platform.md)
* [性能准则](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile 入门](/help/mobile/getting-started-aem-mobile.md)
* [什么是AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)
