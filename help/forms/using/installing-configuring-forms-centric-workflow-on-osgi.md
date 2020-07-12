---
title: 在OSGi上安装和配置以表单为中心的工作流程
seo-title: 在OSGi上安装和配置以表单为中心的工作流程
description: 安装和配置AEM Forms互动通信，以创建业务通信、文档、声明、利益声明、营销邮件、帐单和欢迎套件。
seo-description: 安装和配置AEM Forms互动通信，以创建业务通信、文档、声明、利益声明、营销邮件、帐单和欢迎套件。
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
translation-type: tm+mt
source-git-commit: a18a018181a779b9f48ef3e39c26410a1bc4919b
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 2%

---


# 在OSGi上安装和配置以表单为中心的工作流程{#installing-and-configuring-forms-centric-workflow-on-osgi}

## 简介 {#introduction}

企业从多个表单、后端系统和其他数据源收集和处理数据。 数据处理涉及审核和批准程序、重复任务和数据归档。 例如，查看表单并将其转换为PDF文档。 手动完成操作后，重复性任务可能需要大量时间和资源。

您可以在OSGi [上使用以表单为中心的工作流](../../forms/using/aem-forms-workflow.md) ，快速构建基于表单的自适应工作流。 这些工作流可以帮助您自动执行审阅和批准工作流、业务流程工作流和其他重复任务。 这些工作流还帮助处理文档(创建、组合、分发和存档PDF文档，添加数字签名以限制对文档的访问，对条形码表单进行解码等)，并将Adobe Sign签名工作流与表单和文档结合使用。

设置完成后，可以手动触发这些工作流以完成定义的进程，或在用户提交表单或交互通信时以编程方式运行。 该功能包含在AEM Forms附加包中。

AEM Forms是一个功能强大的企业级平台。 OSGi上以表单为中心的工作流程只是AEM Forms的一项功能。 有关功能的完整列表，请参 [阅AEM Forms简介](introduction-aem-forms.md)。

>[!NOTE]
>
>借助OSGi上以表单为中心的工作流程，您可以快速为OSGi堆栈上的各种任务构建和部署工作流，而无需在JEE堆栈上安装成熟的流程管理功能。 查看OSGi [上以表](capabilities-osgi-jee-workflows.md) 单为中心的AEM工作流与JEE上的流程管理的对比，了解功能的不同之处和相似性。
>
>比较后，如果选择在JEE堆栈上安装流程管理功能，请参 [阅在JEE上安装或升级AEM Forms](/help/forms/home.md) ，了解有关安装和配置JEE堆栈和流程管理功能的详细信息。

## 部署拓扑 {#deployment-topology}

AEM Forms加载项包是部署到AEM上的应用程序。 只需至少一个AEM Author或处理实例（生产作者），即可在OSGi功能上运行以表单为中心的工作流程。 处理实例是硬化 [的AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) 实例。 请勿对生产作者执行任何实际创作，如创建工作流或自适应表单。

以下拓扑是指示性拓扑，用于在OSGi功能上运行AEM Forms交互通信、通信管理、AEM Forms数据捕获和以表单为中心的工作流。 有关拓扑的详细信息，请参 [阅AEM Forms的架构和部署拓扑](/help/forms/using/aem-forms-architecture-deployment.md)。

![推荐拓扑](assets/recommended-topology.png)

AEM Forms在OSGi上以表单为中心的工作流在AEM Forms的作者实例上运行AEM收件箱和AEM工作流模型创建UI。

## 系统要求 {#system-requirements}

>[!NOTE]
>
>如果您已 [在OSGi上安装文档](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) ，请跳到AEM Forms的“下一步”部分，如安装和配置数 [据捕获功能文章中所述](../../forms/using/installing-configuring-aem-forms-osgi.md) 。

在OSGi上开始安装和配置以表单为中心的工作流程之前，请确保：

* 硬件和软件基础架构已到位。 有关受支持硬件和软件的详细列表，请参 [阅技术要求](/help/sites-deploying/technical-requirements.md)。

* AEM实例的安装路径不包含空格。
* AEM实例已启动并正在运行。 在AEM术语中，“实例”是在创作或发布模式下在服务器上运行的AEM的副本。 您至少需要一个AEM实例（作者或处理）才能在OSGi上运行以表单为中心的工作流：

   * **作者**: 用于创建、上传和编辑内容以及管理网站的AEM实例。 内容准备就绪后，即会复制到发布实例。
   * **处理：** 处理实例是硬化 [的AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) 实例。 您可以设置一个作者实例，并在执行安装后对其进行强化。

   * **发布**: 通过Internet或内部网络向公众提供已发布内容的AEM实例。

* 满足内存要求。 AEM Forms加载项包需要：

   * 15 GB临时空间，用于基于Microsoft Windows的安装。
   * 6 GB临时空间用于基于UNIX的安装。

* 基于UNIX的系统的额外要求： 如果您使用基于UNIX的操作系统，请从相应操作系统的安装介质安装以下软件包。

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

AEM Forms加载项包是部署到AEM上的应用程序。 该软件包包含OSGi上的以表单为中心的工作流程和其他功能。 请执行以下步骤来安装加载项包：

1. 开放 [软件分发](https://experience.adobe.com/downloads)。 您需要Adobe ID登录软件分发。
1. 点按 **[!UICONTROL 标题]** 菜单中可用的Adobe Experience Manager。
1. 在过滤器 **[!UICONTROL 部分]** :
   1. 从“ **[!UICONTROL 解决方]** 案 **[!UICONTROL ”下]** 拉列表中选择“表单”。
   2. 选择包的版本和类型。 您还可以使用“搜 **[!UICONTROL 索下载]** ”选项筛选结果。
1. 点按适用于您的操作系统的包名称，选择“ **[!UICONTROL 接受EULA条款]**”，然后点 **[!UICONTROL 按下载]**。
1. 打开 [包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) ，然后单 **[!UICONTROL 击“上传包]** ”以上传包。
1. Select the package and click **[!UICONTROL Install]**.

   您还可以通过AEM Forms版本文章中列出的直接链接下载 [该包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) 。

1. 安装包后，系统会提示您重新启动AEM实例。 **请勿立即重新启动服务器。** 在停止AEM Forms服务器之前，请等到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止显示在 [AEM-Installation-Directory]/crx-quickstart/logs/error.log文件中，并且日志是稳定的。
1. 对所有“作者”和“发布”实例重复步骤1-7。

## 安装后配置 {#post-installation-configurations}

AEM Forms有一些必选和可选配置。 必需配置包括配置BouncyCastle库和序列化代理。 可选配置包括配置调度程序和Adobe Target。

### 强制安装后配置 {#mandatory-post-installation-configurations}

#### 配置RSA和BouncyCastle库  {#configure-rsa-and-bouncycastle-libraries}

对所有“作者”和“发布”实例执行以下步骤以引导委派库：

1. 停止基础AEM实例。
1. 打开AEM [安装目录\crx-quickstart\conf\sling.properties]文件进行编辑。

   如果您使 [用AEM安]装目录\crx-quickstart\bin\start.bat开始AEM，请编辑位于AEM_root \crx-quickstart\ [的sling.properties]。

1. 将以下属性添加到sling.properties文件：

   ```
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

#### 配置Dispatcher {#configure-dispatcher}

Dispatcher是AEM的缓存和负载平衡工具。 AEMDispatcher还有助于保护AEM服务器免受攻击。 您可以结合使用Dispatcher与企业级Web服务器，提高AEM实例的安全性。 如果您使 [用Dispatcher](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html)，则对AEM Forms执行以下配置：

1. 为AEM Forms配置访问权限：

   打开调度程序。any文件进行编辑。 导航到筛选器部分，然后将以下筛选器添加到筛选器部分：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   保存并关闭文件。 有关过滤器的详细信息，请参阅 [Dispatcher文档](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 配置推荐人筛选器服务：

   以管理员身份登录到Apache Felix配置管理器。 配置管理器的默认URL为https://&#39;server&#39;:[port_number]/system/console/configMgr。 在“配 **置** ”菜单中，选 **择“Apache Sling推荐人过滤器** ”选项。 在“允许主机”字段中，输入调度程序的主机名以允许它作为推荐人，然后单击“保 **存”**。 条目的格式为 `https://'[server]:[port]'`。

#### 配置缓存 {#configure-cache}

缓存是一种缩短数据访问时间、减少延迟和提高输入／输出(I/O)速度的机制。 自适应表单缓存仅存储自适应表单的HTML内容和JSON结构，而不保存任何预填数据。 它有助于缩短渲染自适应表单所需的时间。

* 在使用自适应表单缓存时，请 [使用AEMDispatcher](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html) 来缓存自适应表单的客户端库（CSS和JavaScript）。
* 在开发自定义组件时，在用于开发的服务器上禁用自适应表单缓存。

请执行以下步骤以配置自适应表单缓存：

1. 请转至AEM Web控制台配置管理器 `https://'[server]:[port]'/system/console/configMgr`。
1. 单击 **自适应表单配置服务** ，以编辑其配置值。 在“编辑配置值”对话框中，在“自适应表单数”字段中指定AEM Forms服务器实例可以缓存的最 **大表单数或文档** 。 默认值为 100。单击&#x200B;**保存**。

   >[!NOTE]
   >
   >要禁用缓存，请将“自适应表单数”字段中的值设置 **为0**。 在禁用或更改缓存配置时，将重置缓存并从缓存中删除所有表单和文档。

#### 配置Adobe Sign {#configure-adobe-sign}

Adobe Sign支持自适应表单的电子签名工作流。 电子签名可改善处理法律、销售、工资、人力资源管理等文档的工作流。

在OSGi上以Adobe Sign和表单为中心的典型工作流程中，用户填写自适应表单 **以申请服务**。 例如，信用卡申请和公民福利表。 当用户填写、提交和签署申请表时，将启动批准／拒绝工作流。 服务提供商在AEM收件箱中审阅应用程序，并使用Adobe Sign对应用程序进行电子签名。 要启用类似的电子签名工作流，您可以将Adobe Sign与AEM Forms集成。

要将Adobe Sign与AEM Forms结合使 [用，请将Adobe Sign与AEM Forms结合使用](../../forms/using/adobe-sign-integration-adaptive-forms.md)。

## 后续步骤 {#next-steps}

您已配置环境，以在OSGi功能上使用以表单为中心的工作流程。 现在，使用该功能的步骤是：

* [在OSGi上使用以表单为中心的工作流程](../../forms/using/aem-forms-workflow.md)
* [工作流步骤参考](/help/sites-developing/workflows-step-ref.md)
* [信件和互动通信的后处理](../../forms/using/submit-letter-topostprocess.md)

