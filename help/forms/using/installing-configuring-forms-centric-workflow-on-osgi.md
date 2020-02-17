---
title: 在OSGi上安装和配置以表单为中心的工作流
seo-title: 在OSGi上安装和配置以表单为中心的工作流
description: 安装和配置AEM Forms Interactive Communications，以创建业务通信、文档、声明、利益声明、营销邮件、帐单和欢迎工具包。
seo-description: 安装和配置AEM Forms Interactive Communications，以创建业务通信、文档、声明、利益声明、营销邮件、帐单和欢迎工具包。
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# 在OSGi上安装和配置以表单为中心的工作流{#installing-and-configuring-forms-centric-workflow-on-osgi}

## 简介 {#introduction}

企业从多个表单、后端系统和其他数据源收集和处理数据。 数据处理涉及审核和批准程序、重复任务和数据归档。 例如，查看表单并将其转换为PDF文档。 手动完成后，重复任务可能需要大量时间和资源。

您可以在OSGi上 [使用以表单为中心的工作流](../../forms/using/aem-forms-workflow.md) ，快速构建基于表单的自适应工作流。 这些工作流可以帮助您自动执行审阅和批准工作流、业务流程工作流和其他重复任务。 这些工作流程还有助于处理文档（创建、组合、分发和存档PDF文档，添加数字签名以限制对文档的访问，对条形码表单进行解码等），并将Adobe sign签名工作流程用于表单和文档。

设置完成后，可以手动触发这些工作流以完成定义的进程，或在用户提交表单或交互通信时以编程方式运行。 该功能包含在AEM Forms加载项包中。

AEM Forms是一个功能强大的企业级平台。 OSGi上以表单为中心的工作流程只是AEM Forms的功能之一。 有关功能的完整列表，请参 [阅AEM Forms简介](../../forms/using/introduction-aem-forms.md)。

>[!NOTE]
>
>借助OSGi上以表单为中心的工作流，您可以快速为OSGi堆栈上的各种任务构建和部署工作流，而无需在JEE堆栈上安装完整的流程管理功能。 查看OSGi上以 [表单为中心](../../forms/using/capabilities-osgi-jee-workflows.md) 的AEM工作流与JEE上的流程管理的比较，了解功能的不同之处和相似性。
>
>比较后，如果选择在JEE堆栈上安装进程管理功能，请参阅在JEE上安装或升级AEM表单 [](/help/forms/home.md) ，以了解有关安装和配置JEE堆栈以及进程管理功能的详细信息。

## 部署拓扑 {#deployment-topology}

AEM Forms加载项包是部署到AEM上的应用程序。 对于OSGi功能，您至少需要一个AEM作者或处理实例（生产作者）才能运行以表单为中心的工作流。 处理实例是加强的 [AEM作者实例](/help/forms/using/hardening-securing-aem-forms-environment.md) 。 请勿对生产作者执行任何实际创作操作，如创建工作流或自适应表单。

以下拓扑是指示性拓扑，用于针对OSGi功能运行AEM Forms Interactive Communications、Correponsement Management、AEM Forms数据捕获和以表单为中心的工作流程。 有关拓扑的详细信息，请参 [阅AEM Forms的架构和部署拓扑](/help/forms/using/aem-forms-architecture-deployment.md)。

![推荐拓扑](assets/recommended-topology.png)

OSGi上的以AEM Forms为中心的工作流在AEM Forms的作者实例上运行AEM收件箱和AEM Workflow模型创建UI。

## 系统要求 {#system-requirements}

>[!NOTE]
>
>如果您已经 [在OSGi上安装了AEM Forms](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) ，请跳到文档的“下一步”部分，如安装和配置数据 [捕获功能一文中所述](../../forms/using/installing-configuring-aem-forms-osgi.md) 。

在OSGi上开始安装和配置以表单为中心的工作流之前，请确保：

* 硬件和软件基础结构就位。 有关支持的硬件和软件的详细列表，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md)。

* AEM实例的安装路径不包含空格。
* AEM实例已启动并正在运行。 在AEM术语中，“实例”是在创作或发布模式下在服务器上运行的AEM的副本。 您至少需要一个AEM实例（作者或处理）才能在OSGi上运行以表单为中心的工作流：

   * **作者**:用于创建、上传和编辑内容以及管理网站的AEM实例。 内容准备就绪后，即会复制到发布实例。
   * **** 处理：处理实例是加强的 [AEM作者实例](/help/forms/using/hardening-securing-aem-forms-environment.md) 。 您可以设置一个作者实例，并在执行安装后对其进行强化。

   * **发布**:通过Internet或内部网络向公众提供已发布内容的AEM实例。

* 满足内存要求。 AEM Forms Add-on包需要：

   * 15 GB临时空间，用于基于Microsoft windows的安装。
   * 6 GB临时空间，用于基于UNIX的安装。

* 基于UNIX的系统的其他要求：如果您使用基于UNIX的操作系统，请从相应操作系统的安装介质安装以下包。

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

AEM Forms加载项包是部署到AEM上的应用程序。 该包包含OSGi和其他功能上以表单为中心的工作流程。 请执行以下步骤来安装加载项包：

1. 以管理员身份登录 [到AEM服务器](https://localhost:4502) ，然后打开包 [共享](https://localhost:4502/crx/packageshare)。 您需要Adobe ID才能登录到包共享。
1. 在 [AEM包共享中](https://localhost:4502/crx/packageshare/login.html)，搜索 **AEM 6.5 Forms Add-on包或最新**&#x200B;服务包&#x200B;**，单击适用于您的操作系统的包，然后单击******&#x200B;下载。 阅读并接受许可协议，然后单击“确 **定”**。 下载开始。 下载后，包旁 **会显示** “已下载”一词。

   您还可以使用版本号搜索加载项包。 有关最新包的版本号，请参阅 [AEM Forms发行文章](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 。

1. 下载完成后，单击“已下 **载”**。 您将被重定向到包管理器。 在包管理器中，搜索下载的包，然后单击“安 **装”**。

   如果您通过 [AEM Forms发行文章中列出的直接链接手动下载包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) ，请登录到包管理器，单击“上传包” ****，选择下载的包，然后单击“上传”。 上传包后，单击包名称，然后单击“安 **装”。**

1. 安装包后，系统会提示您重新启动AEM实例。 **请勿立即重新启动服务器。** 在停止AEM Forms服务器之前，请等到AEM-Installation-Directory []/crx-quickstart/logs/error.log文件中显示“ServiceEvent REGISTERED”和“ServiceEvent UNREGISTERED”消息停止，并且日志是稳定的。
1. 对所有“作者”和“发布”实例重复步骤1-4。

## 安装后配置 {#post-installation-configurations}

AEM Forms具有一些必需和可选配置。 必需配置包括配置BouncyCastle库和序列化代理。 可选配置包括配置调度程序和Adobe Target。

### 强制安装后配置 {#mandatory-post-installation-configurations}

#### 配置RSA和BouncyCastle库 {#configure-rsa-and-bouncycastle-libraries}

对所有“作者”和“发布”实例执行以下步骤以引导委派库：

1. 停止基础AEM实例。
1. 打开 [AEM安装目录\crx-quickstart\conf\sling.properties]文件进行编辑。

   如果您使 [用AEM安装目录]\crx-quickstart\bin\start.bat启动AEM，请编辑位于 [AEM_root]\crx-quickstart\的sling.properties。

1. 将以下属性添加到sling.properties文件：

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. 保存并关闭文件，然后启动AEM实例。
1. 对所有“作者”和“发布”实例重复步骤1-4。

#### 配置序列化代理 {#configure-the-serialization-agent}

对所有创作和发布实例执行以下步骤以将包列入白名单：

1. 在浏览器窗口中打开AEM配置管理器。 默认URL为https://[server]:[port]/system/console/configMgr。
1. 搜索并打开反序 **列化防火墙配置**。
1. 将 **sun.util.calendar包添加到白名单** 字段 **** 。 单击保存。
1. 对所有“作者”和“发布”实例重复步骤1-3。

### 可选的安装后配置 {#optional-post-installation-configurations}

#### 配置调度程序 {#configure-dispatcher}

Dispatcher是用于AEM的缓存和负载平衡工具。 AEM Dispatcher还有助于保护AEM服务器免受攻击。 通过将Dispatcher与企业级Web服务器结合使用，可以提高AEM实例的安全性。 如果您使用 [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)，则对AEM Forms执行以下配置：

1. 配置对AEM Forms的访问权限：

   打开dispatcher.any文件进行编辑。 导航到筛选器部分，然后将以下筛选器添加到筛选器部分：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   保存并关闭文件。 有关过滤器的详细信息，请参阅 [Dispatcher文档](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 配置引用过滤器服务：

   以管理员身份登录到Apache Felix配置管理器。 配置管理器的默认URL是https://[server]:[port_number]/system/console/configMgr。 在“配 **置** ”菜单中，选择 **Apache Sling Referrer过滤器选项** 。 在“允许主机”字段中，输入调度程序的主机名以允许它作为引用，然后单击“保 **存”**。 条目的格式为 `https://[server]:[port]`。

#### 配置缓存 {#configure-cache}

缓存是一种缩短数据访问时间、减少延迟和提高输入／输出(I/O)速度的机制。 自适应表单缓存仅存储自适应表单的HTML内容和JSON结构，而不保存任何预填数据。 它有助于缩短渲染自适应表单所需的时间。

* 在使用自适应表单缓存时，使用 [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) ，缓存自适应表单的客户端库（CSS和JavaScript）。
* 在开发自定义组件时，请在用于开发的服务器上禁用自适应表单缓存。

请执行以下步骤以配置自适应表单缓存：

1. 转到位于的AEM web控制台配置管理器 `https://[server]:[port]/system/console/configMgr`。
1. 单击 **自适应表单配置服务** ，以编辑其配置值。 在编辑配置值对话框中，在自适应表单数字字段中指定AEM Forms服务器实例可以缓存的最大表 **单或文档数** 。 默认值为 100。单击&#x200B;**保存**。

   >[!NOTE]
   >
   >要禁用缓存，请将“自适应表单数”字段中的值设置为 **0**。 当您禁用或更改缓存配置时，将重置缓存并从缓存中删除所有表单和文档。

#### 配置Adobe Sign {#configure-adobe-sign}

Adobe Sign支持自适应表单的电子签名工作流程。 电子签名改进了处理法律、销售、工资单、人力资源管理等领域文档的工作流程。

在OSGi方案上以Adobe sign和表单为中心的典型工作流程中，用户填写自适应表单以 **申请服务**。 例如，信用卡申请和公民福利表。 当用户填写、提交和签署申请表时，将启动批准／拒绝工作流。 服务提供商在AEM收件箱中审阅应用程序，并使用Adobe Sign以电子方式对应用程序进行签名。 要启用类似的电子签名工作流程，您可以将Adobe Sign与AEM Forms集成。

要将Adobe Sign与AEM Forms结合使用，请 [将Adobe Sign与AEM Forms集成](../../forms/using/adobe-sign-integration-adaptive-forms.md)。

## 后续步骤 {#next-steps}

您已将环境配置为在OSGi功能上使用以表单为中心的工作流。 现在，使用该功能的步骤是：

* [在OSGi上使用以表单为中心的工作流程](../../forms/using/aem-forms-workflow.md)
* [工作流步骤参考](/help/sites-developing/workflows-step-ref.md)
* [信件和交互通信的后期处理](../../forms/using/submit-letter-topostprocess.md)

