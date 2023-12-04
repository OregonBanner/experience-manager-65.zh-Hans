---
title: 在OSGi上安装和配置以Forms为中心的工作流
description: 安装和配置AEM Forms Interactive Communications以创建业务往来函、文档、声明、福利通知、营销邮件、账单和欢迎套件。
topic-tags: installing
docset: aem65
role: Admin
exl-id: 4b24a38a-c1f0-4c81-bb3a-39ce2c4892b1
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1590'
ht-degree: 3%

---

# 在OSGi上安装和配置以Forms为中心的工作流{#installing-and-configuring-forms-centric-workflow-on-osgi}

## 简介 {#introduction}

企业从多个表单、后端系统和其他数据源收集和处理数据。 数据的处理涉及审核和批准程序、重复任务和数据存档。 例如，检查表单并将其转换为 PDF 文档。 手动完成时，重复的任务可能需要花费大量时间和大量资源。

您可以在 OSGi ](../../forms/using/aem-forms-workflow.md) 上使用 [ 以 Forms 为中心的工作流，以快速版本自适应表单的工作流。这些工作流可帮助您自动执行审核和批准工作流、业务流程工作流和其他重复性任务。 这些工作流还有助于处理文档（创建、汇编、分发和存档 PDF 文档、添加数字签名以限制对文档、解码条形码表单等），以及使用表单和 Adobe Sign 的工作流签名文档。

设置后，可以手动触发这些工作流以完成定义的进程，或在用户提交表单或交互式通信时以编程方式运行。 该功能包含在 AEM Forms 加载项包中。

AEM Forms是一个功能强大的企业级平台。 OSGi上以Forms为中心的工作流只是AEM Forms的功能之一。 有关权能的完整列表，请参见 [AEM Forms简介](introduction-aem-forms.md).

>[!NOTE]
>
>借助OSGi上以Forms为中心的工作流，您可以在OSGi栈栈上快速构建和部署用于各种任务的工作流，而无需在JEE栈栈上安装完整的流程管理功能。 查看 [比较](capabilities-osgi-jee-workflows.md) OSGi上以Forms为中心的AEM Workflow和JEE上的流程管理，以了解功能的异同。
>
>比较后，如果选择在JEE栈栈上安装进程管理功能，请参阅 [在JEE上安装或升级AEM Forms](/help/forms/home.md) ，以了解有关安装和配置JEE栈栈以及进程管理功能的详细信息。

## 部署拓扑 {#deployment-topology}

AEM Forms附加组件包是部署在AEM上的应用程序。 您只需要至少一个AEM创作或处理实例（生产创作），即可在OSGi功能上运行以Forms为中心的工作流。 处理实例是 [强化的AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) 实例。 请勿对生产作者执行任何实际创作，例如创建工作流或自适应表单。

以下拓扑是指示性拓扑，用于在OSGi功能上运行AEM Forms交互式通信、通信管理、AEM Forms数据捕获和以Forms为中心的工作流。 有关拓扑的详细信息，请参见 [AEM Forms的架构和部署拓扑](/help/forms/using/aem-forms-architecture-deployment.md).

![推荐拓扑](assets/recommended-topology.png)

OSGi上以AEM Forms Forms为中心的工作流在AEM Forms的创作实例上运行AEM收件箱和AEM工作流模型创建UI。

## 系统要求 {#system-requirements}

>[!NOTE]
>
>跳至 [后续步骤](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) 部分(如果您已在OSGi上安装AEM Forms)，请参见 [安装和配置数据捕获功能](../../forms/using/installing-configuring-aem-forms-osgi.md) 文章。

在开始在OSGi上安装和配置以Forms为中心的工作流之前，请确保：

* 硬件和软件基础架构已准备就绪。 有关支持的硬件和软件的详细列表，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

* AEM实例的安装路径不包含空格。
* AEM实例已启动并正在运行。 在AEM术语中，“实例”是在创作或发布模式下在服务器上运行的AEM的副本。 您需要至少一个AEM实例（创作或处理）才能在OSGi上运行以Forms为中心的工作流：

   * **作者**：用于创建、上载和编辑内容以及管理网站的AEM实例。 内容准备好上线后，即会复制到发布实例。
   * **正在处理：** 处理实例是 [强化的AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) 实例。 您可以设置“创作”实例，并在执行安装后进行强化。

   * **Publish**：AEM实例，通过Internet或内部网络向公众提供已发布的内容。

* 满足内存要求。 AEM Forms附加组件包需要：

   * 用于基于Microsoft Windows的安装的15 GB临时空间。
   * 用于基于UNIX的安装的6 GB临时空间。

* 基于UNIX的系统的额外要求：如果您使用的是基于UNIX的操作系统，请从相应操作系统的安装媒体安装以下软件包。

<table>
 <tbody>
  <tr>
   <td>外派人员</td>
   <td>libxcb</td>
   <td>自由类型</td>
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

## 安装AEM Forms附加组件包 {#install-aem-forms-add-on-package}

AEM Forms附加组件包是部署在AEM上的应用程序。 该包中包含有关OSGi和其他功能的以Forms为中心的工作流。 执行以下步骤以安装附加组件包：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 选择 **[!UICONTROL Adobe Experience Manager]** 在标题菜单中可用。
1. 在 **[!UICONTROL 过滤器]** 部分：
   1. 选择 **[!UICONTROL Forms]** 从 **[!UICONTROL 解决方案]** 下拉列表。
   2. 选择包的版本和类型。 您也可以使用 **[!UICONTROL 搜索下载]** 用于筛选结果的选项。
1. 选择适用于您的操作系统的包名称，然后选择 **[!UICONTROL 接受EULA条款]**，并选择 **[!UICONTROL 下载]**.
1. 打开 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  并单击 **[!UICONTROL 上传包]** 以上传包。
1. 选择包，然后单击 &quot;安装 ]**&quot;**[!UICONTROL  。

   您还可以通过 &quot; [ AEM Forms 版本 ](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) &quot; 文章中列出的直接关联下载包。

1. 安装包后，系统会提示您重新启动 AEM 实例。 **不要立即重新启动服务器。**&#x200B;在停止 AEM Forms 服务器之前，请等待 ServiceEvent 注册和 ServiceEvent 取消注册的消息在 AEM 安装目录 ] /crx-quickstart/logs/error.log 文件中 [ 停止显示，并且日志处于稳定状态。
1. 在所有作者和 Publish 实例上重复步骤1-7。

## Post 安装配置 {#post-installation-configurations}

AEM Forms具有一些强制和可选配置。 强制配置包括配置BouncyCastle库和序列化代理。 可选配置包括配置Dispatcher和Adobe Target。

### 强制性安装后配置 {#mandatory-post-installation-configurations}

#### 配置RSA和BouncyCastle库  {#configure-rsa-and-bouncycastle-libraries}

在所有Author和Publish实例上执行以下步骤以引导委派库：

1. 停止基础AEM实例。
1. 打开 [AEM安装目录]\crx-quickstart\conf\sling.properties文件进行编辑。

   如果您使用 [AEM安装目录]\crx-quickstart\bin\start.bat以启动AEM，然后编辑位于的sling.properties [AEM_root]\crx-quickstart\。

1. 将以下属性添加到sling.properties文件：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 保存并关闭文件，然后启动AEM实例。
1. 对所有创作实例和发布实例重复步骤1-4。

#### 配置序列化代理 {#configure-the-serialization-agent}

列入允许列表对所有Author和Publish实例执行以下步骤，将包添加到中：

1. 在浏览器窗口中打开AEM Configuration Manager。 默认URL为https://&#39;[服务器]：[端口]&#39;/system/console/configMgr.
1. 搜索并打开 **反序列化防火墙配置**.
1. 添加 **sun.util.calendar** 打包到 **允许列表** 字段。 单击“保存”。
1. 对所有创作实例和发布实例重复步骤1-3。

### 可选安装后配置 {#optional-post-installation-configurations}

#### 配置Dispatch {#configure-dispatcher}

Dispatcher是适用于AEM的缓存和负载平衡工具。 AEM Dispatcher还有助于保护AEM服务器免受攻击。 您可以将Dispatcher与企业级Web服务器结合使用来提高AEM实例的安全性。 如果您使用 [Dispatcher](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html)，然后为AEM Forms执行以下配置：

1. 配置AEM Forms的访问权限：

   打开dispatcher.any文件进行编辑。 导航到过滤器部分，并将以下过滤器添加到过滤器部分：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   保存并关闭文件。 有关过滤器的详细信息，请参阅 [Dispatcher文档](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. 配置反向链接筛选服务：

   以管理员身份登录Apache Felix配置管理器。 配置管理器的默认URL为https://&#39;server&#39; ：[端口号]/system/console/configMgr。 在 **配置** 菜单，选择 **Apache Sling引用过滤器** 选项。 在允许主机字段中，输入Dispatcher的主机名以允许其作为反向链接，然后单击 **保存**. 条目的格式为 `https://'[server]:[port]'`.

#### 配置缓存 {#configure-cache}

缓存是一种缩短数据访问时间、减少延迟并提高输入/输出(I/O)速度的机制。 自适应表单缓存仅存储自适应表单的HTML内容和JSON结构，而不保存任何预填数据。 它有助于减少渲染自适应表单所需的时间。

* 使用自适应表单缓存时，请使用 [AEM调度程序](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html) 缓存自适应表单的客户端库（CSS和JavaScript）。
* 开发自定义组件时，在用于开发的服务器上禁用自适应表单缓存。

执行以下步骤以配置自适应表单缓存：

1. 转到位于的AEM Web控制台配置管理器 `https://'[server]:[port]'/system/console/configMgr`.
1. 单击 **[!UICONTROL 自适应表单和交互式通信Web渠道配置]** 以编辑其配置值。 在编辑配置值对话框中，指定AEM Forms服务器实例可以缓存的最大表单或文档数 **自适应Forms的数量** 字段。 默认值为 100。单击&#x200B;**保存**。

   >[!NOTE]
   >
   >要禁用缓存，请将自适应Forms数量字段中的值设置为 **0**. 禁用或更改缓存配置时，将重置缓存并从缓存中删除所有表单和文档。

#### 配置Adobe Sign {#configure-adobe-sign}

Adobe Sign支持自适应表单的电子签名工作流程。 电子签名改进了法律、销售、工资单、人力资源管理和其他许多方面的文档的处理工作流。

在OSGi上的典型Adobe Sign和以Forms为中心的工作流场景中，用户填写自适应表单以 **申请服务**. 例如，信用卡申请表和公民权益表。当用户填写、提交和签署申请表单时，将启动批准/拒绝工作流。 服务提供商在AEM收件箱中审查应用程序，并使用Adobe Sign以电子方式签署应用程序。 要支持类似的电子签名工作流，您可以将Adobe Sign与AEM Forms集成。

要将Adobe Sign与AEM Forms一起使用， [将Adobe Sign与AEM Forms集成](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## 后续步骤 {#next-steps}

您已配置一个环境，以在OSGi功能上使用以Forms为中心的工作流。 现在，使用该功能的步骤包括：

* [在OSGi中使用以Forms为中心的工作流](../../forms/using/aem-forms-workflow.md)
* [工作流步骤参考](/help/sites-developing/workflows-step-ref.md)
* [信件和互动式通信的后处理](../../forms/using/submit-letter-topostprocess.md)
