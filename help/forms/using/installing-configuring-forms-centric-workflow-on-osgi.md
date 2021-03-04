---
title: 在OSGi上安装和配置以Forms为中心的工作流
seo-title: 在OSGi上安装和配置以Forms为中心的工作流
description: 安装和配置AEM Forms Interactive Communications，以创建业务通信、文档、声明、利益声明、营销邮件、帐单和欢迎工具包。
seo-description: 安装和配置AEM Forms Interactive Communications，以创建业务通信、文档、声明、利益声明、营销邮件、帐单和欢迎工具包。
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
translation-type: tm+mt
source-git-commit: 3690d2d76ce13064bd3946f4f6fea1a2759cdf37
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 5%

---


# 在OSGi{#installing-and-configuring-forms-centric-workflow-on-osgi}上安装和配置以Forms为中心的工作流

## 简介 {#introduction}

企业从多个表单、后端系统和其他数据源收集和处理数据。 数据处理涉及审核和批准程序、重复任务和数据归档。 例如，查看表单并将其转换为PDF文档。 手动完成时，重复任务可能需要大量时间和资源。

您可以在OSGi](../../forms/using/aem-forms-workflow.md)上使用[以Forms为中心的工作流来快速构建基于表单的自适应工作流。 这些工作流可以帮助您自动执行审阅和批准工作流、业务流程工作流和其他重复任务。 这些工作流还帮助处理文档(创建、组合、分发和存档PDF文档，添加数字签名以限制对文档的访问，对条形码表单进行解码等)，并将Adobe Sign签名工作流用于表单和文档。

设置完成后，可以手动触发这些工作流以完成定义的进程，或在用户提交表单或交互式通信时以编程方式运行。 该功能包含在AEM Forms加载项包中。

AEM Forms是一个功能强大的企业级平台。 Forms上以OSGi为中心的工作流程只是AEM Forms的功能之一。 有关功能的完整列表，请参阅[AEM Forms](introduction-aem-forms.md)简介。

>[!NOTE]
>
>借助OSGi上以Forms为中心的工作流程，您无需在JEE堆栈上安装完善的流程管理功能，即可快速构建和部署OSGi堆栈上各种任务的工作流。 请参阅OSGi上以Forms为中心的AEM工作流的[比较](capabilities-osgi-jee-workflows.md)和JEE上的流程管理，了解功能的差异和相似性。
>
>比较后，如果选择在JEE堆栈上安装进程管理功能，请参阅[在JEE](/help/forms/home.md)上安装或升级AEM Forms，了解有关安装和配置JEE堆栈和进程管理功能的详细信息。

## 部署拓扑{#deployment-topology}

AEM Forms加载项包是部署到AEM上的应用程序。 您至少需要一个AEM作者实例或处理实例（生产作者）才能在OSGi功能上运行以Forms为中心的工作流。 处理实例是[硬化的AEM作者](/help/forms/using/hardening-securing-aem-forms-environment.md)实例。 请勿对生产作者执行任何实际的创作操作，如创建工作流或自适应表单。

以下拓扑是指示性拓扑，可运行AEM Forms Interactive Communications、Corresponce Management、AEM Forms数据捕获和Forms中心式OSGi功能工作流。 有关拓扑的详细信息，请参阅[AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md)的体系结构和部署拓扑。

![推荐拓扑](assets/recommended-topology.png)

AEM Forms Forms以工作流为中心，OSGi在AEM Forms的作者实例上运行AEM Inbox和AEM Workflow Model创建UI。

## 系统要求{#system-requirements}

>[!NOTE]
>
>如[安装和配置数据捕获功能](../../forms/using/installing-configuring-aem-forms-osgi.md)文章中所述，如果您已在OSGi上安装了AEM Forms，请跳到文档的[后续步骤](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps)部分。

在OSGi上开始安装和配置以Forms为中心的工作流程之前，请确保：

* 硬件和软件基础架构已经到位。 有关所支持硬件和软件的详细列表，请参见[技术要求](/help/sites-deploying/technical-requirements.md)。

* AEM实例的安装路径不包含空格。
* AEM实例已启动且正在运行。 在AEM术语中，“实例”是在创作或发布模式下在服务器上运行的AEM的副本。 您至少需要一个AEM实例（作者或处理）才能在OSGi上运行以Forms为中心的工作流：

   * **作者**:用于创建、上传和编辑内容以及管理网站的AEM实例。内容准备就绪后，即会将其复制到发布实例。
   * **处理：** 处理实例是加强的 [AEM ](/help/forms/using/hardening-securing-aem-forms-environment.md) Authorinstance。您可以设置一个Author实例，并在执行安装后对其进行硬化。

   * **发布**:通过Internet或内部网络向公众提供已发布内容的AEM实例。

* 满足内存要求。 AEM Forms加载项包需要：

   * 15 GB临时空间，用于基于Microsoft Windows的安装。
   * 6 GB临时空间，用于基于UNIX的安装。

* 对基于UNIX的系统的额外要求：如果您使用基于UNIX的操作系统，请从相应操作系统的安装介质安装以下程序包。

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

## 安装AEM Forms加载项包{#install-aem-forms-add-on-package}

AEM Forms加载项包是部署到AEM上的应用程序。 该包包含OSGi上以Forms为中心的工作流程和其他功能。 请执行以下步骤来安装加载项包：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL 过滤器]**&#x200B;部分中：
   1. 从&#x200B;**[!UICONTROL 解决方案]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Forms]**。
   2. 为包选择版本和类型。 您还可以使用&#x200B;**[!UICONTROL 搜索下载]**&#x200B;选项来筛选结果。
1. 点按适用于您的操作系统的包名称，选择&#x200B;**[!UICONTROL 接受EULA条款]**，然后点按&#x200B;**[!UICONTROL 下载]**。
1. 打开[包管理器](https://docs.adobe.com/content/help/zh-Hans/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 选择包，然后单击&#x200B;**[!UICONTROL 安装]**。

   您还可以通过[AEM Forms发行版](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)文章中列出的直接链接下载包。

1. 安装包后，系统会提示您重新启动AEM实例。 **不要立即重新启动服务器。** 在停止AEM Forms服务器之前，请等到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止显示在 [AEM-Installation-Directory]/crx-quickstart/logs/error.log文件中，并且日志是稳定的。
1. 对所有“作者”和“发布”实例重复步骤1-7。

## 安装后配置{#post-installation-configurations}

AEM Forms有一些必选和可选配置。 必需配置包括配置BouncyCastle库和序列化代理。 可选配置包括配置调度程序和Adobe Target。

### 强制安装后配置{#mandatory-post-installation-configurations}

#### 配置RSA和BouncyCastle库{#configure-rsa-and-bouncycastle-libraries}

对所有“作者”和“发布”实例执行以下步骤以引导委派库：

1. 停止基础AEM实例。
1. 打开[AEM安装目录]\crx-quickstart\conf\sling.properties文件进行编辑。

   如果您使用[AEM安装目录]\crx-quickstart\bin\start.bat开始AEM，请编辑位于[AEM_root]\crx-quickstart\的sling.properties。

1. 将以下属性添加到sling.properties文件：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 保存并关闭文件并开始AEM实例。
1. 对所有“作者”和“发布”实例重复步骤1-4。

#### 配置序列化代理{#configure-the-serialization-agent}

对所有“作者”和“发布”实例执行以下步骤，将包添加到允许列表:

1. 在浏览器窗口中打开AEM Configuration Manager。 默认URL为https://&#39;[server]:[port]&#39;/system/console/configMgr。
1. 搜索并打开&#x200B;**反序列化防火墙配置**。
1. 将&#x200B;**sun.util.calendar**&#x200B;包添加到&#x200B;**允许列表**&#x200B;字段。 单击保存。
1. 对所有“作者”和“发布”实例重复步骤1-3。

### 可选安装后配置{#optional-post-installation-configurations}

#### 配置调度程序{#configure-dispatcher}

调度程序是AEM的缓存和负载平衡工具。 AEM Dispatcher还有助于保护AEM服务器免受攻击。 通过将Dispatcher与企业级Web服务器结合使用，可以提高AEM实例的安全性。 如果使用[Dispatcher](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html)，则对AEM Forms执行以下配置：

1. 配置对AEM Forms的访问：

   打开要编辑的dispatcher.any文件。 导航到筛选器部分，然后将以下筛选器添加到筛选器部分：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   保存并关闭文件。 有关过滤器的详细信息，请参阅[调度程序文档](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 配置推荐人筛选器服务：

   以管理员身份登录到Apache Felix配置管理器。 配置管理器的默认URL为https://&#39;server&#39;:[port_number]/system/console/configMgr。 在&#x200B;**配置**&#x200B;菜单中，选择&#x200B;**Apache Sling推荐人过滤器**&#x200B;选项。 在“允许主机”字段中，输入调度程序的主机名以允许它作为推荐人，然后单击“保存&#x200B;****”。 条目的格式为`https://'[server]:[port]'`。

#### 配置缓存{#configure-cache}

缓存是一种缩短数据访问时间、减少延迟和提高输入/输出(I/O)速度的机制。 自适应表单缓存仅存储自适应表单的HTML内容和JSON结构，而不保存任何预填数据。 它有助于缩短渲染自适应表单所需的时间。

* 使用自适应表单缓存时，使用[AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)缓存自适应表单的客户端库（CSS和JavaScript）。
* 在开发自定义组件时，请在用于开发的服务器上禁用自适应表单缓存。

请执行以下步骤以配置自适应表单缓存：

1. 转到位于`https://'[server]:[port]'/system/console/configMgr`的AEM Web控制台配置管理器。
1. 单击&#x200B;**[!UICONTROL 自适应表单和交互式通信Web渠道配置]**&#x200B;以编辑其配置值。 在编辑配置值对话框中，在&#x200B;**自适应Forms**&#x200B;数字字段中指定AEM Forms服务器实例可缓存的表单或文档的最大数量。 默认值为 100。单击&#x200B;**保存**。

   >[!NOTE]
   >
   >要禁用缓存，请将“Number of Adaptive Forms”（自适应）字段中的值设置为&#x200B;**0**。 在禁用或更改缓存配置时，将重置缓存，并从缓存中删除所有表单和文档。

#### 配置Adobe Sign {#configure-adobe-sign}

Adobe Sign支持自适应表单的电子签名工作流。 电子签名可改善处理法律、销售、工资、人力资源管理等领域文档的工作流。

在OSGi方案上以Adobe Sign和Forms为中心的典型工作流中，用户将填充自适应表单以&#x200B;**申请服务**。 例如，信用卡申请和公民福利表。 当用户填写、提交和签署申请表时，将启动批准/拒绝工作流。 服务提供商在AEM收件箱中审阅应用程序，并使用Adobe Sign以电子方式对应用程序进行签名。 要启用类似的电子签名工作流，您可以将Adobe Sign与AEM Forms集成。

要将Adobe Sign与AEM Forms一起使用，[将Adobe Sign与AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)集成。

## 后续步骤{#next-steps}

您已配置了一个环境，以在OSGi功能上使用以Forms为中心的工作流。 现在，使用该功能的步骤是：

* [在OSGi上使用以Forms为中心的工作流](../../forms/using/aem-forms-workflow.md)
* [工作流步骤参考](/help/sites-developing/workflows-step-ref.md)
* [信件和互动通信的后处理](../../forms/using/submit-letter-topostprocess.md)

