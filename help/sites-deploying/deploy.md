---
title: 部署和维护
seo-title: 部署和维护
description: 了解如何开始安装AEM。
seo-description: 了解如何开始安装AEM。
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
translation-type: tm+mt
source-git-commit: cb07e24b01084f57ad46615cb463ad5a0329c181
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 7%

---


# 部署和维护{#deploying-and-maintaining}

在此页中，您将找到：

* [基本概念](#basic-concepts)

   * [什么是 AEM?](#what-is-aem)
   * [典型部署](#typical-deployment-scenarios)

      * [内部部署](#on-premise)
      * [Managed Services使用Cloud Manager](#managed-services-using-cloud-manager)

* [入门](#getting-started)

   * [前提条件](#prerequisites)
   * [获取软件](#getting-the-software)
   * [默认本地安装](#default-local-install)
   * [创作和发布安装](#author-and-publish-installs)
   * [解压缩的安装目录](#unpacked-install-directory)
   * [启动和停止](#starting-and-stopping)

熟悉这些基础知识后，您将在以下子页面中找到更高级和详细信息：

* [技术要求](/help/sites-deploying/technical-requirements.md)
* [建议的部署](/help/sites-deploying/recommended-deploys.md)
* [自定义独立安装](/help/sites-deploying/custom-standalone-install.md)
* [应用程序服务器安装](/help/sites-deploying/application-server-install.md)
* [疑难解答](/help/sites-deploying/troubleshooting.md)
* [命令行启动和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [配置](/help/sites-deploying/configuring.md)
* [升级到AEM 6.5](/help/sites-deploying/upgrade.md)
* [电子商务](/help/sites-deploying/ecommerce.md)
* [配置操作方法文章](/help/sites-deploying/ht-deploy.md)
* [Web 控制台](/help/sites-deploying/web-console.md)
* [复制疑难解答](/help/sites-deploying/troubleshoot-rep.md)
* [最佳实践](/help/sites-deploying/best-practices.md)
* [部署社区](/help/communities/deploy-communities.md)
* [AEM平台简介](/help/sites-deploying/platform.md)
* [性能指南](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile 入门](/help/mobile/getting-started-aem-mobile.md)
* [什么是AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)

## 基本概念 {#basic-concepts}

### 什么是 AEM? {#what-is-aem}

Adobe Experience Manager 是基于 Web 的客户端服务器系统，可用于构建、管理和部署商业网站及相关服务。它将多个基础架构级别和应用程序级别的功能整合到一个集成包中。

在基础架构级别AEM提供以下内容：

* **Web 应用程序服务器**:AEM可以以独立模式部署（它包括集成的Jetty Web服务器），也可以作为第三方应用程序服务器中的Web应用程序部署。
* **Web 应用程序框架**:AEM整合了SlingWeb 应用程序框架，可简化REST风格的、面向内容的Web应用程序的编写。
* **内容存储库**:AEM包含一个Java内容存储库(JCR)，它是一种专门为非结构化和半结构化数据设计的分层数据库。 存储库不仅存储面向用户的内容，还存储应用程序使用的所有代码、模板和内部数据。

在此基础上，AEM还优惠了许多应用程序级功能，用于管理：

* **网站**
* **移动应用程序**
* **数字出版物**
* **表单**
* **数字资产**
* **社区**
* **在线商务**

最后，客户可以使用这些基础架构和应用程序级构建块创建自定义的解决方案，方法是构建自己的应用程序。

AEM服务器基 **于Java** ，并运行于支持该平台的大多数操作系统上。 与AEM的所有客户端交互都通过Web **浏览器完成**。

### 典型部署方案 {#typical-deployment-scenarios}

在AEM术语中，“实例”是在服务器上运行的AEM的副本。 AEM安装通常至少涉及两个实例，通常运行在不同的计算机上：

* **作者**:用于创建、上传和编辑内容以及管理网站的AEM实例。 内容准备就绪后，即会复制到发布实例。
* **发布**:为公众提供已发布内容的AEM实例。

这些实例与已安装的软件完全相同。 它们仅通过配置区分。 此外，大多数安装都使用调度程序：

* **调度程序**:静态Web服务器（Apache httpd、Microsoft IIS等） 增强了AEM调度程序模块。 它缓存由发布实例生成的网页以提高性能。

此设置有许多高级选项和详细说明，但大多数部署的核心是作者、发布和调度程序的基本模式。 首先，我们将关注一个相对简单的机构。 随后将讨论高级部署选项。

以下各节介绍了这两种情况：

* **内部部署**:AEM在您的公司环境中部署和管理。

* **Managed Services-Adobe Experience Manager云经理**:AEM由Adobe Managed Services部署和管理。

### On-premise {#on-premise}

您可以在公司环境的服务器上安装AEM。 典型安装实例包括：开发、测试和发布环境。 有关如何让AEM软 [件在本地安装](/help/sites-deploying/deploy.md#getting%20started) ，请参阅入门部分。

要进一步了解典型的内部部署，请参阅推荐 [部署](/help/sites-deploying/recommended-deploys.md)。

### Managed Services使用Cloud Manager {#managed-services-using-cloud-manager}

AEMManaged Services是数字体验管理的完整解决方案。 它在云中提供体验投放解决方案的优势，同时保留预置部署的所有控制、安全和自定义优势。 AEMManaged Services通过在云上进行部署以及依靠Adobe的最佳实践和支持，使客户能够更快地启动产品。 组织和业务用户只需极少的时间即可吸引客户，推动市场份额增长，并专注于创建创新的营销活动，同时减轻IT负担。

借助AEMManaged Services，客户可以实现以下优势：

**缩短上市时间：** 借助Adobe Managed Services的灵活云基础架构，组织可以快速规划、启动和优化成功的数字体验。 Adobe无需额外资金、硬件或软件即可管理云架构，Adobe的客户成功工程师也可以帮助管理AEM架构、资源调配、自定义以连接到后端应用程序和上线最佳实践。

**更高的性能：** 通过四个服务可用性选项（99.5%、99.9%、99.95%和99.99%）为您的企业提供可靠的数字体验。 此外，它还允许自动备份和多模式灾难恢复模型，以帮助确保可靠性和应急管理。

**优化的IT成本：** 前瞻性指导和专业知识可帮助组织始终掌握AEM的最新版本。 Adobe白金维护和支持自动包括在AMS企业／基础的新部署中，提供技术专业知识和操作经验，帮助组织维护其任务关键型应用程序。 免费的基本分析或目标功能优惠额外价值，尤其是对分析和个性化需求有限的中端市场组织。

**最高安全性：** 通过在受限访问设施、防火墙系统后或虚拟专用云中托管客户应用程序，确保企业级物理、网络和数据安全。 它包括具有强大数据存储加密、抗病毒和数据隔离功能的单租户虚拟机。

**云管理器**:Cloud Manager是Adobe Experience ManagerManaged Services服务的一部分，它是一个自助门户，使组织能够在云中自行管理Adobe Experience Manager。 它包括一流的连续集成和连续投放(CI/CD)管道，使IT团队和实施合作伙伴能够在不影响性能或安全性的情况下加快自定义或更新的投放。 Cloud Manager仅适用于Adobe托管服务客户。

要进一步了解Cloud Manager及其资源，请参阅《Cloud Manager [**用户指南》**](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)。

## 入门 {#getting-started}

### 前提条件 {#prerequisites}

虽然生产实例通常在运行正式支持的操作系统的专用计算机上运行(请 [参阅技术要求](/help/sites-deploying/technical-requirements.md))，但Experience Manager服务器实际上将在支持Java Standard Edition [**8的任何系统上运行**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。

为了熟悉和在AEM上进行开发，使用运行Apple OS X或Microsoft Windows或Linux的桌面版本的本地计算机上安装的实例非常常见。

在客户端，AEM可与所有现代化的浏览器(**Microsoft Edge**、Internet Explorer **11、**Chrome** 51+ ****、**Firefox **47+、****** Safari 8+)在桌面和平板电脑操作系统上工作。 有关详 [细信息，请参阅](/help/sites-deploying/technical-requirements.md#supported-client-platforms) “支持的客户端平台”。

### 获取软件 {#getting-the-software}

Customers with a valid maintenance and support contract should have received a mail notification with a code and be able to download AEM from the [**Adobe Licensing Website**](https://licensing.adobe.com/). Business partners can request download access from [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

AEM软件包有两种形式：

* **cq-quickstart-6.5.0.jar:** 独立的可执 *行程序* jar文件，包含启动和运行所需的一切。

* **cq-quickstart-6.5.0.war:** 用于 *部署* 在第三方应用程序服务器中的war文件。

在下一节中，我们将介绍独 **立安装**。 有关在应用程序服务器中安装AEM的详细信息，请参 [阅应用程序服务器安装](/help/sites-deploying/application-server-install.md)。

### 默认本地安装 {#default-local-install}

1. 在本地计算机上创建安装目录。 例如：

   UNIX安装位置： **/opt/aem**

   Windows安装位置： **`C:\Program Files\aem`**

   同样，在桌面上直接将示例实例安装在文件夹中也很常见。 无论如何，我们通常将此位置称为：

   `<aem-install>`

   *请注意，文件目录的路径必须只包含美国ASCII字符。*

1. 将jar **和** **license **文件放在此目录中：

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   如果您不提供文件， `license.properties` AEM将在启动时将浏览器重定 **向到** “欢迎”屏幕，您可以在该屏幕中输入许可证密钥。 如果您还没有许可证密钥，您需要从Adobe申请有效的许可证密钥。

1. 要在GUI环境中开始实例，只需多次单击文 **`cq-quickstart-6.5.0.jar`** 件。

   或者，您也可以从命令行启动AEM。 对于32位Java VM，请输入以下内容：

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

   对于64位虚拟机，输入：

   ```shell
       java -XX:MaxPermSize=256m -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM需要几分钟时间才能解压缩jar文件、安装自己并开始。 上述过程导致：

* aem **author实例**
* 在localhost上运 **行**
* 在端口4502 **上**

要访问实例，请将浏览器指向：

**`https://localhost:4502`**

创作实例中的结果将自动配置为连接到上 **的发布实例****`localhost:4503`**。

### 创作和发布安装 {#author-and-publish-installs}

只需在首次启动文 **件之前重** 命名文件，即可更改默认安装( **`localhost:4502`**`jar` 上的作者实例)。 命名模式为：

**`cq-<instance-type>-p<port-number>.jar`**

例如，将文件重命名为

**`cq-author-p4502.jar`**

并启动它将导致在上运行一个作者实例 **`localhost:4502`**。

同样，重命名和启动文件

**`cq-publish-p4503.jar`**

将导致在上运行发布实例 **`localhost:4503`**。

例如，您将在

`<aem-install>/author`和

**`<aem-install>/publish`**

有关自定义安装的更多详细信息，请参阅：

* [自定义独立安装](/help/sites-deploying/custom-standalone-install.md)
* [运行模式](/help/sites-deploying/configure-runmodes.md)

### 解压缩的安装目录 {#unpacked-install-directory}

首次启动快速启动jar时，它将将其解压缩到名为的新子目录下的同一目录中 `crx-quickstart`。 您最后应该有以下内容：

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

如果实例是从UI安装的，则浏览器窗口将自动打开，桌面应用程序窗口也将打开，显示该实例的主机和端口以及开／关开关：

![开始屏幕](assets/screen_shot_.png)

>[!NOTE]
>
>如果您使用的是symlinks，请查看symlink [的问题](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html)。

### 启动和停止 {#starting-and-stopping}

在AEM解压并首次启动后，多次单击安装目录中的jar文件只会开始实例，但不会重新安装它。

要从GUI中停止实例，只需单击桌 **面应用程序窗口** 上的开／关开关。

您还可以从命令行停止和开始AEM。 假定您已首次安装该实例，则命 **令行脚本** 位于此处：

**`<aem-install>/crx-quickstart/bin/`**

此文件夹包含以下Unix bash外壳程序脚本：

* **`start`**:开始实例
* `stop`:停止实例
* **`status`**:报告实例的状态
* **`quickstart`**:用于配置开始信息（如果需要）。

还有适用于Windows **`bat`** 的对等文件。 有关详细信息，请参阅：

* [命令行启动和停止](/help/sites-deploying/command-line-start-and-stop.md)

AEM开始并自动将您的Web浏览器重定向到相应的页面，通常是登录页面；例如：

`https://localhost:4502/`

![登录屏幕](assets/screen_shot_2019-04-08at83533am.png)

登录后，您即可访问AEM。 有关详细信息，请根据您的角色，参阅以下内容：

* [创作](/help/sites-authoring/home.md)
* [管理](/help/sites-administering/home.md)
* [开发](/help/sites-developing/home.md)
* [管理](/help/managing/best-practices.md)

## 高级部署 {#advanced-deployment}

以上部分应能让您充分理解AEM安装的基础知识。 但是，安装AEM的完整生产系统可能涉及的复杂性要大得多。 有关高级安装的完整信息，请参阅以下子页：

* [技术要求](/help/sites-deploying/technical-requirements.md)
* [建议的部署](/help/sites-deploying/recommended-deploys.md)
* [自定义独立安装](/help/sites-deploying/custom-standalone-install.md)
* [应用程序服务器安装](/help/sites-deploying/application-server-install.md)
* [疑难解答](/help/sites-deploying/troubleshooting.md)
* [命令行启动和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [配置](/help/sites-deploying/configuring.md)
* [升级到AEM 6.5](/help/sites-deploying/upgrade.md)
* [电子商务](/help/sites-deploying/ecommerce.md)
* [配置操作方法文章](/help/sites-deploying/ht-deploy.md)
* [Web 控制台](/help/sites-deploying/web-console.md)
* [复制疑难解答](/help/sites-deploying/troubleshoot-rep.md)
* [最佳实践](/help/sites-deploying/best-practices.md)
* [部署社区](/help/communities/deploy-communities.md)
* [AEM平台简介](/help/sites-deploying/platform.md)
* [性能指南](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile 入门](/help/mobile/getting-started-aem-mobile.md)
* [什么是AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)
