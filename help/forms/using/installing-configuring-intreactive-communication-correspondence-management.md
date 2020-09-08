---
title: 安装和配置交互通信
seo-title: 安装和配置交互通信
description: 安装和配置AEM Forms互动通信，以创建业务通信、文档、声明、利益声明、营销邮件、帐单和欢迎套件。
seo-description: 安装和配置AEM Forms互动通信，以创建业务通信、文档、声明、利益声明、营销邮件、帐单和欢迎套件。
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
translation-type: tm+mt
source-git-commit: cbc43991143397c8bc0080b7402bfdc664522ab8
workflow-type: tm+mt
source-wordcount: '1411'
ht-degree: 1%

---


# 安装和配置交互通信{#install-and-configure-interactive-communications}

## 简介 {#introduction}

AEM Form能够集中创建、汇编、管理和投放安全的交互式文档，如业务通信、文档、声明、利益声明、营销邮件、帐单和欢迎套件。 此功能称为交互式通信。 该功能包含在AEM Forms附加包中。 加载项包部署在AEM的作者或发布实例上。

您可以使用交互式通信功能以多种格式生成通信。 例如，Web和PDF。 您可以将交互式通信与AEM Workflow集成，根据客户选择的渠道处理和交付组合的通信。 例如，通过电子邮件向最终用户发送通信。

如果您从先前版本升级并已投资于通信管理，则可以安装兼容 [性包](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) ，以继续使用通信管理。 有关交互式通信和通信管理之间差异的信息，请参 [阅交互式通信概述](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management)。

AEM Forms是一个强大的企业级平台。 交互通信只是AEM Forms的一项能力。 有关功能的完整列表，请参 [阅AEM Forms简介](../../forms/using/introduction-aem-forms.md)。

## 部署拓扑 {#deployment-topology}

AEM Forms加载项包是部署到AEM上的应用程序。 运行交互通信功能至少需要一个AEM作者和处理实例。 以下拓扑是指示性拓扑，用于运行AEM Forms交互通信、通信管理、AEM Forms数据捕获和以Forms为中心的OSGi功能工作流。 有关拓扑的详细信息，请参 [阅AEM Forms的架构和部署拓扑](/help/forms/using/aem-forms-architecture-deployment.md)。

![推荐拓扑](assets/recommended-topology.png)

AEM Forms交互通信在AEM Forms的作者实例上运行管理、创作和代理用户界面。 Publish实例托管最终版本的交互式通信，可供最终用户使用。

## 系统要求 {#system-requirements}

在开始安装和配置AEM Forms的交互式通信和通信管理功能之前，请确保：

* 硬件和软件基础架构已到位。 有关受支持硬件和软件的详细列表，请参 [阅技术要求](/help/sites-deploying/technical-requirements.md)。

* AEM实例的安装路径不包含空格。
* AEM实例已启动且正在运行。 在AEM术语中，“实例”是在创作或发布模式下在服务器上运行的AEM的副本。 您至少需要一个AEM实例（作者或处理）来运行AEM Forms的交互式通信和通信管理功能：

   * **作者**:用于创建、上传和编辑内容以及管理网站的AEM实例。 内容准备就绪后，即会复制到发布实例。
   * **处理：** 处理实例是加强的 [AEM作者实例](/help/forms/using/hardening-securing-aem-forms-environment.md) 。 您可以设置一个作者实例，并在执行安装后对其进行强化。

   * **发布**:通过Internet或内部网络向公众提供已发布内容的AEM实例。

* 满足内存要求。 AEM Forms附加包要求：

   * 15 GB临时空间，用于基于Microsoft Windows的安装。
   * 6 GB临时空间用于基于UNIX的安装。

* 基于UNIX的系统的额外要求：如果您使用基于UNIX的操作系统，请从相应操作系统的安装介质安装以下软件包。

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>libxcb</td>
   <td>freetype</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuuid</td>
  </tr>
  <tr>
   <td>glibc</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## Install AEM Forms add-on package {#install-aem-forms-add-on-package}

AEM Forms加载项包是部署到AEM上的应用程序。 该软件包包含AEM Forms的交互通信、通信管理和其他功能。 请执行以下步骤来安装加载项包：

1. 开放 [软件分发](https://experience.adobe.com/downloads)。 您需要Adobe ID才能登录软件分发。
1. 点按 **[!UICONTROL 标题]** 菜单中提供的Adobe Experience Manager。
1. 在过滤器 **[!UICONTROL 部分]** :
   1. 从“ **[!UICONTROL 解决方]** 案 **[!UICONTROL ”下拉]** 列表中选择Forms。
   2. 选择包的版本和类型。 您还可以使用“搜 **[!UICONTROL 索下载]** ”选项筛选结果。
1. 点按适用于您的操作系统的包名称，选择“ **[!UICONTROL 接受EULA条款]**”，然后点 **[!UICONTROL 按下载]**。
1. 打开 [包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) ，然后单 **[!UICONTROL 击“上传包]** ”以上传包。
1. Select the package and click **[!UICONTROL Install]**.

   您还可以通过AEM Forms版本文章中列出的直接链接下载 [该包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) 。

1. 安装包后，系统会提示您重新启动AEM实例。 **请勿立即重新启动服务器。** 在停止AEM Forms服务器之前，请等到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止显示在 [AEM Installation-Directory]/crx-quickstart/logs/error.log文件中，并且日志是稳定的。
1. 对所有“作者”和“发布”实例重复步骤1-7。

## 安装后配置 {#post-installation-configurations}

AEM Forms有一些强制性和可选配置。 必需配置包括配置BouncyCastle库和序列化代理。 可选配置包括配置调度程序和Adobe Target。

### 强制安装后配置 {#mandatory-post-installation-configurations}

#### 配置RSA和BouncyCastle库  {#configure-rsa-and-bouncycastle-libraries}

对所有“作者”和“发布”实例执行以下步骤以引导委派库：

1. 停止基础AEM实例。
1. 打开AEM [安装目]录\crx-quickstart\conf\sling.properties文件进行编辑。

   如果您使 [用AEM安]装目录\crx-quickstart\bin\start.bat将AEM [开始，则请编辑位于AEM_root_\crx-quickstart\的]sling.properties。

1. 将以下属性添加到sling.properties文件：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. 保存并关闭文件，并开始AEM实例。
1. 对所有“作者”和“发布”实例重复步骤1-4。

#### 配置序列化代理 {#configure-the-serialization-agent}

对所有“作者”和“发布”实例执行以下步骤，将包添加到该允许列表:

1. 在浏览器窗口中打开AEM Configuration Manager。 默认URL为[https://&#39;]server[]:port&#39;/system/console/configMgr。
1. 搜索并打开反序 **列化防火墙配置**。
1. 将sun. **util.calendar包添加** 到“ **** ”字段。 单击保存。
1. 对所有“作者”和“发布”实例重复步骤1-3。

### 可选安装后配置 {#optional-post-installation-configurations}

#### 安装兼容性包 {#install-compatibility-package}

在AEM 6.5Forms，交互通信是创建客户通信的默认和推荐的方法。 如果您已从先前版本升级或迁移，并计划继续使用字母（通信管理），请安装 [AEMFD兼容性包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT)。

AEMFD兼容性软件包允许您在AEM 6.4Forms、AEM 6.3Forms和AEM 6.2FormsAEM 6.5Forms上使用以下资源：

* 文档片段
* 书信
* 数据字典
* 自适应表单已弃用的模板和页面

#### 配置调度程序 {#configure-dispatcher}

调度程序是Adobe Experience Manager的缓存和／或负载平衡工具，可与企业级Web服务器结合使用。 如果您使 [用Dispatcher](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html)，请为AEM Forms执行以下配置：

1. 为AEM Forms配置访问：

   打开调度程序。any文件进行编辑。 导航到筛选器部分，然后将以下筛选器添加到筛选器部分：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   保存并关闭文件。 有关过滤器的详细信息，请参 [阅Dispatcher文档](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 配置推荐人筛选器服务：

   以管理员身份登录到Apache Felix配置管理器。 配置管理器的默认URL为https://&#39;server&#39;:[port_number]/system/console/configMgr。 在“配 **置** ”菜单中，选 **择“Apache Sling推荐人过滤器** ”选项。 在“允许主机”字段中，输入调度程序的主机名以允许它作为推荐人，然后单击“保 **存”**。 条目的格式为https://&#39;[server]:[port]。

#### 整合Adobe Target {#integrate-adobe-target}

如果您的客户提供的体验不吸引人，他们可能会放弃交互式通信。 虽然这令客户感到沮丧，但也可以增加组织的支持量和成本。 确定并提供正确的客户体验是至关重要的，也具有挑战性，这将增加转化率。 AEM表单是解决此问题的关键。

AEM forms与Adobe Marketing Cloud解决方案Adobe Target集成，跨多个数字渠道提供个性化、引人入胜的客户体验。 要使用Adobe Target进行个性化的交互式交流， [请将Adobe Target与AEM Forms整合](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)。

#### 为表单数据模型配置SSL通信  {#configure-ssl-communcation-for-form-data-model}

可以为表单数据模型启用SSL通信。 要为表单数据模型启用SSL通信，请在启动任何AEM Forms实例之前，向所有实例的Java信任存储添加证书。 您可以运行以下命令来添加证书：

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## 后续步骤 {#next-steps}

您已配置环境以使用交互通信和通信管理功能。 现在，使用该功能的步骤是：

* [通信管理概述](/help/forms/using/interactive-communications-overview.md)

* [创建交互式通信](../../forms/using/create-interactive-communication.md)

* [创建信函管理信函](../../forms/using/create-letter.md)

