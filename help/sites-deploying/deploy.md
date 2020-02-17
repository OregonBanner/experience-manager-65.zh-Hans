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
source-git-commit: b827c8acb1db158060d209c819fc72ffbfeca65f

---


# 部署和维护{#deploying-and-maintaining}

在本页中，您将找到：

* [基本概念](#basic-concepts)

   * [什么是 AEM?](#what-is-aem)
   * [典型部署](#typical-deployment-scenarios)

      * [内部部署](#on-premise)
      * [使用Cloud manager的托管服务](#managed-services-using-cloud-manager)

* [入门](#getting-started)

   * [前提条件](#prerequisites)
   * [获取软件](#getting-the-software)
   * [默认本地安装](#default-local-install)
   * [创作和发布安装](#author-and-publish-installs)
   * [解压缩的安装目录](#unpacked-install-directory)
   * [开始和停止](#starting-and-stopping)

熟悉这些基础知识后，您将在以下子页面中找到更高级的详细信息：

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
* [AEM Platform简介](/help/sites-deploying/platform.md)
* [性能准则](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile 入门](/help/mobile/getting-started-aem-mobile.md)
* [更新版本车辆定义](/help/sites-deploying/update-release-vehicle-definitions.md)
* [什么是AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)

## 基本概念 {#basic-concepts}

### 什么是 AEM? {#what-is-aem}

Adobe Experience Manager 是基于 Web 的客户端服务器系统，可用于构建、管理和部署商业网站及相关服务。它将多个基础架构级别和应用程序级别的功能整合到一个集成包中。

在基础结构级别，AEM提供以下功能：

* **Web应用程序服务器**:AEM可以以独立模式部署（它包括集成的Jetty web服务器），也可以作为第三方应用程序服务器中的Web应用程序部署。
* **Web应用程序框架**:AEM整合了Sling web应用程序框架，可简化RESTful、面向内容的Web应用程序的编写。
* **内容存储库**:AEM包括Java内容存储库(JCR)，这是一种专门为非结构化和半结构化数据设计的分层数据库类型。 存储库不仅存储面向用户的内容，还存储应用程序使用的所有代码、模板和内部数据。

在此基础上构建，AEM还提供许多用于管理以下内容的应用程序级功能：

* **网站**
* **移动应用程序**
* **数字出版物**
* **Forms**
* **数字资产**
* **社区**
* **在线商务**

最后，客户可以使用这些基础架构和应用程序级构建块来构建自己的应用程序，从而创建自定义的解决方案。

AEM服务器基于 **Java** ，并运行在支持该平台的大多数操作系统上。 所有与AEM的客户端交互都通过Web浏 **览器完成**。

### 典型部署方案 {#typical-deployment-scenarios}

在AEM术语中，“实例”是在服务器上运行的AEM的副本。 AEM安装通常至少涉及两个实例，通常在不同的计算机上运行：

* **作者**:用于创建、上传和编辑内容以及管理网站的AEM实例。 内容准备就绪后，即会复制到发布实例。
* **发布**:向公众提供已发布内容的AEM实例。

这些实例与已安装软件相同。 它们仅通过配置来区分。 此外，大多数安装都使用调度程序：

* **调度程序**:静态Web服务器（Apache httpd、Microsoft IIS等）增强了AEM调度程序模块。 它缓存由发布实例生成的网页以提高性能。

此设置有许多高级选项和详细说明，但大多数部署的核心是创作、发布和调度程序的基本模式。 首先，我们将关注一个相对简单的机构。 随后将讨论高级部署选项。

以下各节将介绍这两种情况：

* **内部部署**:AEM在您的企业环境中部署和管理。

* **Managed Services - Cloud Manager for Adobe Experience Manager**:由Adobe Managed services部署和管理的AEM。

### On-premise {#on-premise}

您可以在企业环境中的服务器上安装AEM。 典型安装实例包括：开发、测试和发布环境。 有关如何获取AEM [软件以本地安装](/help/sites-deploying/deploy.md#getting%20started) ，请参阅入门部分。

要进一步了解典型的内部部署，请参阅建 [议的部署](/help/sites-deploying/recommended-deploys.md)。

### 使用Cloud manager的托管服务 {#managed-services-using-cloud-manager}

AEM Managed services是用于数字体验管理的完整解决方案。 它在云中提供体验交付解决方案的优势，同时保留内部部署的所有控制、安全和自定义优势。 AEM Managed services可让客户通过在云上部署以及依靠Adobe的最佳实践和支持更快地启动。 组织和业务用户可以在最短的时间内吸引客户，推动市场份额增长，并专注于创建创新的营销活动，同时减轻IT负担。

使用AEM Managed Services，客户可以实现以下优势：

**** 缩短上市时间：借助Adobe Managed services的灵活云基础架构，组织可以快速规划、启动和优化成功的数字体验。 Adobe管理云架构，无需额外的资金、硬件或软件，Adobe的客户成功工程师也可以通过AEM架构、配置、自定义来连接后端应用程序和上线最佳实践提供帮助。

**** 更高的性能：通过四个服务可用性选项（99.5%、99.9%、99.95%和99.99%）为您的企业提供可靠的数字体验。 此外，它还允许自动备份和多模式灾难恢复模型，以帮助确保可靠性和应急管理。

**** 优化的IT成本：前瞻性指导和专业知识可帮助组织始终使用最新版AEM。 Adobe白金维护和支持自动包含在AMS Enterprise/Basic的新部署中，它提供技术专业知识和操作经验以帮助组织维护其关键任务应用程序。 免费的基本Analytics或Target功能为中端市场组织提供了额外的价值，这些组织对分析和个性化的需求有限。

**** 最高安全性：通过在受限访问设施、防火墙系统后或虚拟专用云中托管客户应用程序，确保企业级物理、网络和数据安全。 它包括具有强大数据存储加密、抗病毒和数据隔离功能的单租户虚拟机。

**Cloud Manager**:Cloud manager是Adobe Experience Manager Managed services产品的一部分，它是一个自助门户，使组织能够在云中自助管理Adobe Experience Manager。 它包括最新的持续集成和持续交付(CI/CD)管道，使IT团队和实施合作伙伴能够加快定制或更新的交付，同时不会影响性能或安全性。 Cloud manager仅适用于Adobe Managed service客户。

要了解有关Cloud Manger及其资源的更多信息，请参阅《 [**Cloud Manager用户指南》**](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)。

## 入门 {#getting-started}

### 前提条件 {#prerequisites}

虽然生产实例通常在运行正式支持的操作系统的专用计算机上运行(请参阅 [Technical Requirements](/help/sites-deploying/technical-requirements.md))，但Experience Manager服务器实际将在支持 [**Java Standard Edition 8的任何系统上运行&#x200B;**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。

为了熟悉情况和在AEM上进行开发，很常使用在运行Apple OS x或Microsoft windows或Linux的桌面版本的本地计算机上安装的实例。

在客户端，AEM可与所有现代浏览器(**Microsoft Edge**、 **Internet Explorer 11、**Chrome51+** *、**Firefox **47、 ******** Safari 8+)在桌面和平板电脑操作系统上一起使用。 有关详细 [信息，请参阅支持的客户端平台](/help/sites-deploying/technical-requirements.md#supported-client-platforms) 。

### 获取软件 {#getting-the-software}

Customers with a valid maintenance and support contract should have received a mail notification with a code and be able to download AEM from the [**Adobe Licensing Website **](https://licensing.adobe.com/). Business partners can request download access from[**spphelp@adobe.com**](mailto:spphelp@adobe.com).

AEM软件包有两种形式：

* **** cq-quickstart-6.5.0.jar:独立的可执 *行文件* jar文件，包含启动和运行所需的一切。

* **** cq-quickstart-6.5.0.war:用 *于部署* 在第三方应用程序服务器中的war文件。

在下一节中，我们将介绍独 **立安装**。 有关在应用程序服务器中安装AEM的详细信息，请参 [阅应用程序服务器安装](/help/sites-deploying/application-server-install.md)。

### 默认本地安装 {#default-local-install}

1. 在本地计算机上创建一个安装目录。 例如：

   UNIX安装位置： **/opt/aem**

   Windows安装位置： **`C:\Program Files\aem`**

   同样，在桌面上的文件夹中安装示例实例也很常见。 无论如何，我们通常将此位置称为：

   `<aem-install>`

   *请注意，文件目录的路径必须只包含美国ASCII字符。*

1. 将jar **和** **license **文件放在此目录中：

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   如果您不提供文件， `license.properties` AEM将在启动时将浏览器重定向到“欢迎”屏 **幕** ，您可以在该屏幕中输入许可证密钥。 如果您还没有许可证密钥，您需要从Adobe申请有效的许可证密钥。

1. 要在GUI环境中启动实例，只需双击该文 **`cq-quickstart-6.5.0.jar`** 件。

   或者，您也可以从命令行启动AEM。 对于32位Java VM，请输入以下内容：

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

   对于64位虚拟机，输入：

   ```shell
       java -XX:MaxPermSize=256m -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM将花费几分钟时间解压缩jar文件，安装自己，然后启动。 上述过程导致：

* AEM作 **者实例**
* 在localhost上运 **行**
* 在端口 **4502上**

要访问实例点，您的浏览器可以：

**`https://localhost:4502`**

创作实例中的结果将自动配置为连接到上的 **发布实例****`localhost:4503`**。

### 创作和发布安装 {#author-and-publish-installs}

只需在首次启动文 **件之前重命名文件，即可更****`localhost:4502`**`jar` 改默认安装（上的作者实例）。 命名模式为：

**`cq-<instance-type>-p<port-number>.jar`**

例如，将文件重命名为

**`cq-author-p4502.jar`**

而启动它将导致在上运行一个作者实例 **`localhost:4502`**。

同样，重命名和启动文件

**`cq-publish-p4503.jar`**

将导致在上运行发布实例 **`localhost:4503`**。

例如，您将在

`<aem-install>/author`和

**`<aem-install>/publish`**

有关自定义安装的更多详细信息，请参阅以下内容：

* [自定义独立安装](/help/sites-deploying/custom-standalone-install.md)
* [运行模式](/help/sites-deploying/configure-runmodes.md)

### 解压缩的安装目录 {#unpacked-install-directory}

首次启动快速启动jar时，它会将自己解压缩到名为的新子目录下的同一目录中 `crx-quickstart`。 您最后应该看到以下内容：

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

如果实例是从UI安装的，则浏览器窗口将自动打开，桌面应用程序窗口也将打开，显示该实例的主机和端口以及开／关交换机：

![启动屏幕](assets/screen_shot_.png)

>[!NOTE]
>
>如果您使用的是symlink，请查看symlink [的问题](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html)。

### 开始和停止 {#starting-and-stopping}

在AEM解压并首次启动后，双击安装目录中的jar文件只会启动实例，但不会重新安装它。

要从GUI中停止实例，只需单击桌面应 **用程序窗口上的开／关** 开关。

您还可以从命令行停止和启动AEM。 假设您是第一次安装实例，命令行脚 **本位于以下位置** :

**`<aem-install>/crx-quickstart/bin/`**

此文件夹包含以下Unix bash shell脚本：

* **`start`**:启动实例
* `stop`:停止实例
* **`status`**:报告实例的状态
* **`quickstart`**:用于根据需要配置开始信息。

还有适用于Windows **`bat`** 的对等文件。 有关更多详细信息，请参阅：

* [命令行启动和停止](/help/sites-deploying/command-line-start-and-stop.md)

AEM会启动并自动将您的Web浏览器重定向到相应的页面，通常是登录页面；例如：

`https://localhost:4502/`

![登录屏幕](assets/screen_shot_2019-04-08at83533am.png)

登录后，您便可以访问AEM。 有关详细信息，请根据您的角色，参阅以下内容：

* [创作](/help/sites-authoring/home.md)
* [管理](/help/sites-administering/home.md)
* [开发](/help/sites-developing/home.md)
* [管理](/help/managing/best-practices.md)

## 高级部署 {#advanced-deployment}

以上部分应能让您充分了解AEM安装的基础知识。 但是，安装AEM的完整生产系统可能需要大得多的复杂性。 有关高级安装的完整信息，请参阅以下子页：

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
* [AEM Platform简介](/help/sites-deploying/platform.md)
* [性能准则](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile 入门](/help/mobile/getting-started-aem-mobile.md)
* [更新版本车辆定义](/help/sites-deploying/update-release-vehicle-definitions.md)
* [什么是AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)

