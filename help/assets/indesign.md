---
title: 集成 [!DNL Assets] 替换为 [!DNL InDesign Server]
description: 了解如何集成 [!DNL Adobe Experience Manager Assets] 替换为 [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 4%

---

# 集成 [!DNL Adobe Experience Manager Assets] 替换为 [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] 使用：

* 用于分配特定处理任务负载的代理。 代理是 [!DNL Experience Manager] 与代理工作进程通信以完成特定任务及其他任务的实例 [!DNL Experience Manager] 用于交付结果的实例。
* 用于定义和管理特定任务的代理工作程序。
这些功能可以涵盖多种任务；例如，使用 [!DNL InDesign Server] 以处理文件。

要将文件完全上传到 [!DNL Experience Manager Assets] 您创建的项目 [!DNL Adobe InDesign] 使用代理。 这使用代理工作进程与 [!DNL Adobe InDesign Server]，其中 [脚本](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) 运行以提取元数据并生成各种演绎版 [!DNL Experience Manager Assets]. 代理工作程序可以实现 [!DNL InDesign Server] 和 [!DNL Experience Manager] 云配置中的实例。

>[!NOTE]
>
>[!DNL Adobe InDesign] 作为两个单独的选项提供。 [Adobe InDesign](https://www.adobe.com/products/indesign.html) 用于为打印和数字分发设计页面布局的桌面应用程序。 [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) 使您能够根据所创建的内容，以编程方式创建自动化文档 [!DNL InDesign]. 它作为一项服务提供其接口 [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) engine。脚本的编写方式 [!DNL ExtendScript]，与 [!DNL JavaScript]. 有关信息 [!DNL InDesign] 脚本请参阅 [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## 提取的工作原理 {#how-the-extraction-works}

此 [!DNL Adobe InDesign Server] 可以与集成 [!DNL Experience Manager Assets] 这样创建的INDD文件 [!DNL InDesign] 可以上传、生成演绎版、提取所有媒体（例如视频）并将其存储为资源：

>[!NOTE]
>
>早期版本的 [!DNL Experience Manager] 能够提取XMP和缩略图，现在可以提取所有媒体。

1. 将INDD文件上传到 [!DNL Experience Manager Assets].
1. 框架将命令脚本发送到 [!DNL InDesign Server] 通过SOAP（简单对象访问协议）。
此命令脚本将：

   * 检索INDD文件。
   * 执行 [!DNL InDesign Server] 命令：

      * 将提取结构、文本和任何媒体文件。
      * 将生成PDF和JPG演绎版。
      * 将生成HTML和IDML演绎版。

   * 将生成的文件发布回 [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML是一种基于XML的格式，它呈现 [!DNL InDesign] 文件。 使用以下方式将其存储为压缩包 [ZIP](https://www.techterms.com/definition/zip) 压缩。 有关更多信息，请参阅 [InDesign交换格式INX和IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >如果 [!DNL InDesign Server] 未安装或未配置，则仍可将INDD文件上传到 [!DNL Experience Manager]. 但是，生成的演绎版仅限于PNG和JPEG。 您将无法生成HTML、.idml或页面呈现版本。

1. 提取和演绎版生成后：

   * 该结构将复制到 `cq:Page` （演绎版类型）。
   * 提取的文本和文件存储在中 [!DNL Experience Manager Assets].
   * 所有演绎版都存储在 [!DNL Experience Manager Assets]，在资产本身中。

## 集成 [!DNL InDesign Server] 带有Experience Manager {#integrating-the-indesign-server-with-aem}

要集成 [!DNL InDesign Server] 用于以下对象： [!DNL Experience Manager Assets] 配置代理后，您需要：

1. [安装InDesign Server](#installing-the-indesign-server).
1. 如果需要， [配置Experience Manager Assets工作流程](#configuring-the-aem-assets-workflow).
仅当默认值不适用于您的实例时，才需要执行此操作。
1. 配置 [InDesign Server的代理工作进程](#configuring-the-proxy-worker-for-indesign-server).

### 安装 [!DNL InDesign Server] {#installing-the-indesign-server}

安装和启动 [!DNL InDesign Server] 用于以下对象： [!DNL Experience Manager]：

1. 下载并安装 [!DNL InDesign Server].

1. 如果需要，您可以自定义 [!DNL InDesign Server] 实例。

1. 从命令行启动服务器：

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   这将启动在端口8080上侦听SOAP插件的服务器。 所有日志消息和输出都直接写入命令窗口。

   >[!NOTE]
   >
   >如果要将输出消息保存到文件，则使用重定向；例如，在Windows下：
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### 配置 [!DNL Experience Manager Assets] 工作流 {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] 具有预配置的工作流 **[!UICONTROL DAM更新资产]**，其中包含多个专门用于的流程步骤 [!DNL InDesign]：

* [媒体提取](#media-extraction)
* [页面提取](#page-extraction)

此工作流设置了默认值，这些默认值可适用于您在各种创作实例上的设置(这是一个标准工作流，因此在以下位置提供了更多信息： [编辑工作流](/help/sites-developing/workflows-models.md#configuring-a-workflow-step))。 如果使用默认值（包括SOAP端口），则无需配置。

设置完成后，上传 [!DNL InDesign] 文件到 [!DNL Experience Manager Assets] （通过任何常用方法）触发工作流以处理资源并准备各种演绎版。 通过将INDD文件上传到来测试配置 [!DNL Experience Manager Assets] 用于确认您看到了IDS在 `<*your_asset*>.indd/Renditions`

#### 媒体提取 {#media-extraction}

此步骤控制从INDD文件提取介质。

要进行自定义，可以编辑&#x200B;**[!UICONTROL 媒体提取]**&#x200B;步骤的&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡。

![媒体提取参数和脚本路径](assets/media_extraction_arguments_scripts.png)

媒体提取参数和脚本路径

* **ExtendScript library**：这是一个简单的http get/post方法库，是其他脚本所必需的。

* **扩展脚本**：您可以在此处指定不同的脚本组合。 如果您希望自己的脚本在 [!DNL InDesign Server]，将脚本保存在 `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>请勿更改 ExtendScript 库。此库提供与Sling通信所需的HTTP功能。 此设置指定要发送到的库 [!DNL InDesign Server] 以便在此使用。

此 `ThumbnailExport.jsx` 通过“媒体提取”工作流步骤运行的脚本会生成JPG格式的缩略图演绎版。 此演绎版由流程缩略图工作流步骤用于生成所需的静态演绎版 [!DNL Experience Manager].

您可以配置流程缩略图工作流步骤以生成不同大小的静态呈现版本。 确保您不删除默认值，因为 [!DNL Experience Manager Assets] 界面。 最后，“删除图像预览演绎版”工作流步骤会删除JPG缩略图演绎版，因为不再需要它。

#### 页面提取 {#page-extraction}

这会创建 [!DNL Experience Manager] 页面提取元素。 提取处理程序用于从演绎版(当前为HTML或IDML)中提取数据。 然后，使用此数据通过PageBuilder创建页面。

要进行自定义，可以编辑&#x200B;**[!UICONTROL 页面提取]**&#x200B;步骤的&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡。

![chlimage_1-96](assets/chlimage_1-289.png)

* **页面提取处理程序**：从弹出列表中，选择要使用的处理程序。 提取处理程序对相关 `RenditionPicker` 选择的特定演绎版发挥作用（请参阅 `ExtractionHandler` API）。在标准中 [!DNL Experience Manager] 安装可以使用以下选项：
   * IDML导出提取句柄：对 `IDML` MediaExtract步骤中生成的演绎版。

* **页面名称**：指定要分配给结果页面的名称。 如果留空，则名称为“page”（如果“page”已存在，则为派生项）。

* **页面标题**：指定要分配给结果页面的标题。

* **页面根路径**：结果页面的根位置的路径。 如果留空，则使用保存资产的演绎版的节点。

* **页面模板**：生成生成结果页面时使用的模板。

* **页面设计**：生成生成结果页面时要使用的页面设计。

### 配置代理工作进程，用于 [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>Worker驻留在代理实例上。

1. 在工具控制台中，展开 **[!UICONTROL Cloud Service配置]** 在左窗格中。 然后展开 **[!UICONTROL 云代理配置]**.

1. 双击 **[!UICONTROL IDS worker]** 以打开进行配置。

1. 单击 **[!UICONTROL 编辑]** 打开配置对话框并定义所需的设置：

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS池**
要用于与通信的SOAP端点 [!DNL InDesign Server]. 您可以添加、删除和排序项目。

1. 单击“确定”进行保存。

### 配置Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

如果 [!DNL InDesign Server] 和 [!DNL Experience Manager] 在不同的主机上，或者其中一个或两个应用程序在默认端口上不起作用，然后配置 [!UICONTROL Day CQ链接外部化器] 设置的主机名、端口和内容路径 [!DNL InDesign Server].

1. 访问Web控制台： `https://[aem_server]:[port]/system/console/configMgr`.
1. 查找配置 **[!UICONTROL Day CQ链接外部化器]**. 单击 **[!UICONTROL 编辑]** 打开。
1. 链接外部化器设置有助于为创建绝对URL [!DNL Experience Manager] 部署和 [!DNL InDesign Server]. 使用 **[!UICONTROL 域]** 用于指定主机名的字段 [!DNL Adobe InDesign Server]. 单击&#x200B;**保存**。

   在绝对URL中，使用 `localhost` 作为本地（创作）实例的主机名，以及发布实例的主机名或IP地址，如下图所示。

   ![链接外部化器设置](assets/link-externalizer-config.png)

### 启用并行作业处理 [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

您现在可以为IDS启用并行作业处理。 确定最大并行作业数(`x`)和 [!DNL InDesign Server] 可以处理：

* 在单个多处理器计算机上，最大并行作业数(`x`)表示 [!DNL InDesign Server] 可以处理的处理器数少于运行ID的处理器数。
* 在多台计算机上运行ID时，您需要计算可用处理器的总数（即所有计算机上的处理器总数），然后减去计算机总数。

要配置并行IDS作业的数量，请执行以下操作：

1. 打开 **[!UICONTROL 配置]** 选项卡中显示的每个页面的URL长度，例如： `https://[aem_server]:[port]/system/console/configMgr`.

1. 选择IDS处理队列，位于 `Apache Sling Job Queue Configuration`.

1. 套:

   * **类型** - `Parallel`
   * **最大并行作业数** - `<*x*>` （如上计算）

1. 保存这些更改。
1. 要为AdobeCS6及更高版本启用多会话支持，请选中 `enable.multisession.name` 复选框，在 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 配置。
1. 创建 [池 `x` 通过将SOAP端点添加到IDS Worker配置中的IDS Worker](#configuring-the-proxy-worker-for-indesign-server).

   如果有多台计算机正在运行 [!DNL InDesign Server]，为每个计算机添加SOAP端点（每台计算机的处理器数–1）。

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>在使用工作进程池时，您可以启用IDS工作进程的阻止列表。
>
>为此，请启用 **[!UICONTROL enable.retry.name]** 复选框，位于 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 配置，用于启用IDS作业重试。
>
>此外，在 `com.day.cq.dam.ids.impl.IDSPoolImpl.name` 配置，为设置正值 `max.errors.to.blacklist` 参数确定从作业处理程序列表中禁止ID之前的作业重试次数。
>
>默认情况下，在可配置的(`retry.interval.to.whitelist.name`)重新验证IDS Worker所用的时间（以分钟为单位）。 如果联机找到辅助进程，则会将其从阻止列表中删除。

## 启用支持 [!DNL InDesign Server] 10.0或更高版本 {#enabling-support-for-indesign-server-or-later}

对象 [!DNL InDesign Server] 10.0或更高版本，请执行以下步骤以启用多会话支持。

1. 从打开配置管理器 [!DNL Experience Manager Assets] 实例 `https://[aem_server]:[port]/system/console/configMgr`.
1. 编辑配置 `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. 选择 **[!UICONTROL ids.cc.enable]** 选项，然后单击 **[!UICONTROL 保存]**.

>[!NOTE]
>
>对象 [!DNL InDesign Server] 与集成 [!DNL Experience Manager Assets]，请使用多核处理器，因为单核系统不支持集成所需的会话支持功能。

## 配置 [!DNL Experience Manager] 凭据 {#configure-aem-credentials}

您可以更改访问 [!DNL InDesign Server] 来自您的 [!DNL Experience Manager] 部署，无需中断与的集成 [!DNL InDesign Server].

1. 转到 `/etc/cloudservices/proxy.html`.
1. 在对话框中，指定新用户名和密码。
1. 保存凭据。

>[!MORELIKETHIS]
>
>* [关于Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)
