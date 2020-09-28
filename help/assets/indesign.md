---
title: 集 [!DNL Assets] 成 [!DNL InDesign Server]
description: 了解如何 [!DNL Adobe Experience Manager Assets] 集成 [!DNL Adobe InDesign Server]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 4%

---


# 与 [!DNL Adobe Experience Manager Assets] [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] 使用:

* 用于分配特定处理任务的负载的代理。 代理是与代 [!DNL Experience Manager] 理工作者通信以实现特定任务的实例，而其 [!DNL Experience Manager] 他实例则用于传送结果。
* 用于定义和管理特定任务的代理工作器。
这些任务可以涵盖多种领域；例如，使用 [!DNL InDesign Server] 处理文件。

将文件完全上 [!DNL Experience Manager Assets] 传到您使用代理 [!DNL Adobe InDesign] 创建的文件。 它使用代理工作器与进行通信， [!DNL Adobe InDesign Server]在该 [工作器中](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) ，运行脚本以提取元数据并生成各种再现 [!DNL Experience Manager Assets]。 代理工作器在云配置中启用与实 [!DNL InDesign Server] 例之 [!DNL Experience Manager] 间的双向通信。

>[!NOTE]
>
>[!DNL Adobe InDesign] 作为两个单独的产品提供。 [Adobe InDesign](https://www.adobe.com/products/indesign.html) 桌面应用程序，用于设计用于印刷和数字分发的页面布局。 [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) 使您能够根据您所用的创作有计划地创建自动文档 [!DNL InDesign]。 它作为服务运行，提供其 [ExtendScript](https://www.adobe.com/devnet/scripting.html) 引擎的接口。脚本 [!DNL ExtendScript]在中编写，类似于 [!DNL JavaScript]。 有关脚本的 [!DNL InDesign] 信息，请 [参阅https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)。

## 提取的工作方式 {#how-the-extraction-works}

可以 [!DNL Adobe InDesign Server] 与集成，以 [!DNL Experience Manager Assets] 便上传使用创建的INDD文 [!DNL InDesign] 件、生成演绎版、提取所有媒体（例如，视频）并存储为资产：

>[!NOTE]
>
>以前的版 [!DNL Experience Manager] 本能够提取XMP和缩略图，现在可以提取所有媒体。

1. 将INDD文件上传到 [!DNL Experience Manager Assets]。
1. 框架通过SOAP(简单对象访 [!DNL InDesign Server] 问协议)将命令脚本发送到。
此命令脚本将：

   * 检索INDD文件。
   * 执行 [!DNL InDesign Server] 命令：

      * 将解压结构、文本和任何媒体文件。
      * 将生成PDF和JPG再现。
      * 将生成HTML和IDML再现。
   * 将生成的文件发布回 [!DNL Experience Manager Assets]。

   >[!NOTE]
   >
   >IDML是一种基于XML的格式，可呈现文件的所有 [!DNL InDesign] 内容。 它使用ZIP压缩存储为压 [缩包](https://www.techterms.com/definition/zip) 。 有关详细信息，请参 [阅InDesign交换格式INX和IDML](http://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8)。

   >[!CAUTION]
   >
   >如果 [!DNL InDesign Server] 未安装或未配置，则仍可将INDD文件上传到 [!DNL Experience Manager]。 但是，生成的演绎版将限制为PNG和JPEG。 您将无法生成HTML、.idml或页面再现。

1. 生成提取和再现后：

   * 此结构将被复制到 `cq:Page` （演绎版类型）。
   * 提取的文本和文件存储在中 [!DNL Experience Manager Assets]。
   * 所有演绎版都存储 [!DNL Experience Manager Assets]在资产本身中。

## 与Experience Manager [!DNL InDesign Server] 集成 {#integrating-the-indesign-server-with-aem}

要集成以 [!DNL InDesign Server] 在配置代 [!DNL Experience Manager Assets] 理后与之一起使用，您需要：

1. [安装InDesign Server](#installing-the-indesign-server)。
1. 根据需要， [配置Experience Manager资产工作流](#configuring-the-aem-assets-workflow)。
仅当默认值不适用于您的实例时，才需要这样做。
1. 为InDesign Server [配置代理工作器](#configuring-the-proxy-worker-for-indesign-server)。

### 安装 [!DNL InDesign Server] {#installing-the-indesign-server}

安装和开始 [!DNL InDesign Server] 以与 [!DNL Experience Manager]:

1. 下载并安装 [!DNL InDesign Server]。

1. 如果需要，您可以自定义实例的 [!DNL InDesign Server] 配置。

1. 从命令行开始服务器：

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   这将使服务器开始SOAP插件监听端口8080。 所有日志消息和输出都直接写入命令窗口。

   >[!NOTE]
   >
   >如果要将输出消息保存到文件，则使用重定向；例如，在Windows下：
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### 配置工作 [!DNL Experience Manager Assets] 流 {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] 具有预配置的工作流 **[!UICONTROL DAM更新资产]**，该工作流具有几个流程步骤，专门用于 [!DNL InDesign]:

* [媒体提取](#media-extraction)
* [页面提取](#page-extraction)

此工作流设置了默认值，这些默认值可以适应您在各种创作实例上的设置(这是一个标准工作流，因此在编辑工作流下可 [以获得更多信息](/help/sites-developing/workflows-models.md#configuring-a-workflow-step))。 如果您使用默认值（包括SOAP端口），则不需要任何配置。

设置后，将文 [!DNL InDesign] 件上传 [!DNL Experience Manager Assets] 到（通过任何常用方法）会触发工作流以处理资产和准备各种演绎版。 将INDD文件上传到，以确 [!DNL Experience Manager Assets] 认您看到IDS创建的不同演绎版 `<*your_asset*>.indd/Renditions`

#### Media extraction {#media-extraction}

此步骤控制INDD文件中媒体的提取。

要进行自定义，可以编辑&#x200B;**[!UICONTROL 媒体提取]**&#x200B;步骤的&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡。

![媒体提取参数和脚本路径](assets/media_extraction_arguments_scripts.png)

媒体提取参数和脚本路径

* **ExtendScript图书馆**:这是一个简单的http get/post方法库，其他脚本需要它。

* **扩展脚本**:您可以在此处指定不同的脚本组合。 如果希望在上执行您自己的脚本， [!DNL InDesign Server]请将脚本保存在 `/apps/settings/dam/indesign/scripts`。

有关脚本的信 [!DNL Adobe InDesign] 息，请参阅 [InDesign开发人员文档](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>请勿更改 ExtendScript 库。此库提供与Sling通信所需的HTTP功能。 此设置指定要发送到的库以供 [!DNL InDesign Server] 在该库使用。

由媒 `ThumbnailExport.jsx` 体提取工作流步骤运行的脚本生成JPG格式的缩略图再现。 此演绎版由“流程缩略图”工作流步骤使用，以生成所需的静态演绎版 [!DNL Experience Manager]。

您可以配置流程缩略图工作流步骤以生成不同大小的静态演绎版。 请确保不删除默认值，因为界面要求使用这些 [!DNL Experience Manager Assets] 默认值。 最后，删除图像预览再现工作流步骤将删除JPG缩略图再现，因为不再需要它。

#### Page extraction {#page-extraction}

这将从提取 [!DNL Experience Manager] 的元素创建页面。 提取处理程序用于从再现（当前为HTML或IDML）中提取数据。 此数据随后用于使用PageBuilder创建页面。

要进行自定义，可以编辑&#x200B;**[!UICONTROL 页面提取]**&#x200B;步骤的&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡。

![chlimage_1-96](assets/chlimage_1-289.png)

* **页面提取处理程序**:从弹出列表中，选择要使用的处理函数。 提取处理程序对由相关 `RenditionPicker` 选择的特定呈现进行操作（请参阅 `ExtractionHandler` API）。
In a standard [!DNL Experience Manager] installation the following is available:
   * IDML导出提取句柄：对在MediaExtract `IDML` 步骤中生成的再现进行操作。

* **页面名称**:指定要分配给结果页面的名称。 如果留空，则名称为“page”（如果“page”已存在，则为衍生项）。

* **页面标题**:指定要分配给结果页面的标题。

* **页面根路径**:生成页面的根位置的路径。 如果留空，则将使用包含资产演绎版的节点。

* **页面模板**:生成结果页面时使用的模板。

* **页面设计**:生成结果页面时要使用的页面设计。

### 为配置代理工作器 [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>该工作器驻留在代理实例上。

1. 在“工具”控制台中，展 **[!UICONTROL 开左窗格中]** 的“Cloud Services配置”。 然后展开 **[!UICONTROL 云代理配置]**。

1. 双击 **[!UICONTROL IDS worker]** 以打开进行配置。

1. 单击 **[!UICONTROL 编辑]** ，打开配置对话框并定义所需的设置：

   ![proxy_disworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS**&#x200B;池用于与通信的SOAP端点 [!DNL InDesign Server]。 您可以添加、删除和订购项目。

1. 单击确定进行保存。

### 配置Day CQ链接外部器 {#configuring-day-cq-link-externalizer}

如果在 [!DNL InDesign Server] 不同 [!DNL Experience Manager] 主机上运行，或者上述两种应用程序都未在默认端口上运行，请配置 [!UICONTROL Day CQ Link Externalizer] ，为主机设置主机名、端口和内容路径 [!DNL InDesign Server]。

1. 访问Web控制台(位 `https://[aem_server]:[port]/system/console/configMgr`于)。
1. Locate the configuration **[!UICONTROL Day CQ Link Externalizer]**, and click **[!UICONTROL Edit]** to open it.
1. 指定主机名和上下文路径，然 [!DNL Adobe InDesign Server] 后单击“ **保存**”。

   ![chlimage_1-97](assets/chlimage_1-290.png)

### 为 [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server-s}

您现在可以为IDS启用并行作业处理。 确定可处理的并行作业(`x`)的最 [!DNL InDesign Server] 大数量：

* 在单个多处理器计算机上，可处理的并`x`行作业( [!DNL InDesign Server] )的最大数目比运行IDS的处理器数少1。
* 在多台计算机上运行ID时，您需要计算可用处理器总数（即在所有计算机上），然后减去计算机总数。

要配置并行IDS作业数：

1. 打开 **[!UICONTROL Felix]** Console的“配置”选项卡；例如： `https://[aem_server]:[port]/system/console/configMgr`.

1. 在下选择IDS处理队列 `Apache Sling Job Queue Configuration`。

1. 套:

   * **类型** - `Parallel`
   * **最大并行作业** - `<*x*>` （如上所计算）

1. 保存这些更改。
1. 要启用AdobeCS6和更高版本的多会话支持，请选中配 `enable.multisession.name` 置下的复选 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 框。
1. 通过向 [IDS Worker `x` 配置添加SOAP端点，创建IDS Worker池](#configuring-the-proxy-worker-for-indesign-server)。

   如果有多台计算机正在运行， [!DNL InDesign Server]请为每台计算机添加SOAP端点（每台计算机的处理器数-1）。

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>使用工作池时，您可以启用IDS工作者的阻止列表。
>
>要执行此操作，请 **[!UICONTROL 在配置下启用]** enable.retry.name复 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 选框，该配置启用IDS作业检索。
>
>此外，在配 `com.day.cq.dam.ids.impl.IDSPoolImpl.name` 置下，为参数设置一个正值，该 `max.errors.to.blacklist` 参数在禁止IDS进入作业处理程序列表之前确定作业检索的数量。
>
>默认情况下，在IDS工作`retry.interval.to.whitelist.name`器经过可配置（分钟）时间重新验证后。 如果在线找到该工作者，则从阻止列表中删除该工作者。

## 支持10. [!DNL InDesign Server] 0或更高版本 {#enabling-support-for-indesign-server-or-later}

对 [!DNL InDesign Server] 于10.0或更高版本，请执行以下步骤以启用多会话支持。

1. 从实例中打开Configuration [!DNL Experience Manager Assets] Manager `https://[aem_server]:[port]/system/console/configMgr`。
1. 编辑配置 `com.day.cq.dam.ids.impl.IDSJobProcessor.name`。
1. Select the **[!UICONTROL ids.cc.enable]** option, and click **[!UICONTROL Save]**.

>[!NOTE]
>
>要 [!DNL InDesign Server] 与集 [!DNL Experience Manager Assets]成，请使用多核处理器，因为单核系统不支持集成所必需的会话支持功能。

## 配置凭 [!DNL Experience Manager] 据 {#configure-aem-credentials}

您可以更改从部署访问的默认管理员凭据(用户 [!DNL InDesign Server] 名和密 [!DNL Experience Manager] 码)，而不中断与的集成 [!DNL InDesign Server]。

1. 转到 `/etc/cloudservices/proxy.html`.
1. 在对话框中，指定新的用户名和密码。
1. 保存凭据。

>[!MORELIKETHIS]
>
>* [关于Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

