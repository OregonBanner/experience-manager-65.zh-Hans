---
title: 集成 [!DNL Assets] with [!DNL InDesign Server]
description: 了解如何集成 [!DNL Adobe Experience Manager Assets] with [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: 67e145e250bbe386168ab2c0f8967f91aa9d8a36
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 4%

---

# 集成 [!DNL Adobe Experience Manager Assets] with [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] 使用:

* 用于分配特定处理任务的负载的代理。 代理是 [!DNL Experience Manager] 与代理工作程序通信以执行特定任务的实例，以及 [!DNL Experience Manager] 实例来交付结果。
* 用于定义和管理特定任务的代理工作程序。
这些任务可以涵盖多种任务；例如，使用 [!DNL InDesign Server] 来处理文件。

将文件完全上传到 [!DNL Experience Manager Assets] 创建的 [!DNL Adobe InDesign] 使用代理。 它使用代理工作程序与 [!DNL Adobe InDesign Server]，其中 [脚本](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) 运行以提取元数据，并为 [!DNL Experience Manager Assets]. 代理工作程序在 [!DNL InDesign Server] 和 [!DNL Experience Manager] 云配置中的实例。

>[!NOTE]
>
>[!DNL Adobe InDesign] 将作为两个单独的产品提供。 [Adobe InDesign](https://www.adobe.com/products/indesign.html) 用于设计用于打印和数字分发的页面布局的桌面应用程序。 [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) 使您能够根据您创建的 [!DNL InDesign]. 它的运营方式是提供与其 [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) engine.脚本将写入 [!DNL ExtendScript]，与 [!DNL JavaScript]. 有关 [!DNL InDesign] 脚本请参阅 [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## 提取工作原理 {#how-the-extraction-works}

的 [!DNL Adobe InDesign Server] 可与集成 [!DNL Experience Manager Assets] 以便使用 [!DNL InDesign] 可以上传、生成演绎版、提取所有媒体（例如，视频）并存储为资产：

>[!NOTE]
>
>的早期版本 [!DNL Experience Manager] 能够提取XMP和缩略图，现在可以提取所有媒体。

1. 将INDD文件上传到 [!DNL Experience Manager Assets].
1. 框架会向 [!DNL InDesign Server] 通过SOAP（简单对象访问协议）。
此命令脚本将：

   * 检索INDD文件。
   * 执行 [!DNL InDesign Server] 命令：

      * 将提取结构、文本和任何媒体文件。
      * PDF和JPG演绎版将生成。
      * HTML和IDML呈现版本会生成。
   * 将生成的文件发布回 [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML是一种基于XML的格式，可呈现 [!DNL InDesign] 文件。 它将作为压缩包存储，使用 [ZIP](https://www.techterms.com/definition/zip) 压缩。 有关更多信息，请参阅 [InDesign交换格式INX和IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >如果 [!DNL InDesign Server] 未安装或未配置，则仍可将INDD文件上传到 [!DNL Experience Manager]. 但是，生成的演绎版将仅限为PNG和JPEG。 您将无法生成HTML、 .idml或页面演绎版。

1. 在提取和呈现生成之后：

   * 该结构被复制到 `cq:Page` （演绎版类型）。
   * 提取的文本和文件存储在 [!DNL Experience Manager Assets].
   * 所有演绎版都存储在 [!DNL Experience Manager Assets]，在资产本身中。

## 集成 [!DNL InDesign Server] Experience Manager {#integrating-the-indesign-server-with-aem}

要集成 [!DNL InDesign Server] 用于 [!DNL Experience Manager Assets] 配置代理后，您需要：

1. [安装InDesign Server](#installing-the-indesign-server).
1. 如果需要， [配置Experience Manager Assets工作流](#configuring-the-aem-assets-workflow).
仅当默认值不适合您的实例时，才需要执行此操作。
1. 配置 [代理工作程序进行InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### 安装 [!DNL InDesign Server] {#installing-the-indesign-server}

安装并启动 [!DNL InDesign Server] 用于 [!DNL Experience Manager]:

1. 下载并安装 [!DNL InDesign Server].

1. 如果需要，您可以自定义 [!DNL InDesign Server] 实例。

1. 从命令行启动服务器：

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   这将在端口8080上使用SOAP插件监听来启动服务器。 所有日志消息和输出都直接写入命令窗口。

   >[!NOTE]
   >
   >如果要将输出消息保存到文件，则使用重定向；例如，在Windows下：
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### 配置 [!DNL Experience Manager Assets] 工作流 {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] 具有预配置的工作流 **[!UICONTROL DAM更新资产]**，具有几个专门用于 [!DNL InDesign]:

* [媒体提取](#media-extraction)
* [页面提取](#page-extraction)

此工作流是使用默认值进行设置的，这些默认值可适用于您在各种创作实例上的设置(这是一个标准工作流，因此可在 [编辑工作流](/help/sites-developing/workflows-models.md#configuring-a-workflow-step))。 如果您使用的是默认值（包括SOAP端口），则不需要任何配置。

设置后，上传 [!DNL InDesign] 文件到 [!DNL Experience Manager Assets] （通过任何常用方法）会触发处理资产和准备各种演绎版的工作流。 通过将INDD文件上传到 [!DNL Experience Manager Assets] 以确认您看到下面的ID创建的不同演绎版 `<*your_asset*>.indd/Renditions`

#### 媒体提取 {#media-extraction}

此步骤控制从INDD文件提取媒体。

要进行自定义，可以编辑&#x200B;**[!UICONTROL 媒体提取]**&#x200B;步骤的&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡。

![媒体提取参数和脚本路径](assets/media_extraction_arguments_scripts.png)

媒体提取参数和脚本路径

* **ExtendScript库**:这是一个简单的http get/post方法库，其他脚本都需要此库。

* **扩展脚本**:您可以在此处指定不同的脚本组合。 如果您希望在 [!DNL InDesign Server]，请将脚本保存在 `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>请勿更改 ExtendScript 库。此库提供与Sling通信所需的HTTP功能。 此设置指定要发送到的库 [!DNL InDesign Server] 供使用。

的 `ThumbnailExport.jsx` 由媒体提取工作流步骤运行的脚本会生成JPG格式的缩略图呈现。 此演绎版供流程缩略图工作流步骤使用，以生成 [!DNL Experience Manager].

您可以配置流程缩略图工作流步骤以生成不同大小的静态演绎版。 请确保不要删除默认值，因为 [!DNL Experience Manager Assets] 界面。 最后，删除图像预览呈现版本工作流步骤会删除JPG缩略图呈现版本，因为不再需要该呈现版本。

#### 页面提取 {#page-extraction}

这会创建 [!DNL Experience Manager] 页面。 提取处理程序用于从呈现(当前HTML或IDML)中提取数据。 然后，此数据将用于使用PageBuilder创建页面。

要进行自定义，可以编辑&#x200B;**[!UICONTROL 页面提取]**&#x200B;步骤的&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡。

![chlimage_1-96](assets/chlimage_1-289.png)

* **页面提取处理程序**:从弹出列表中，选择要使用的处理程序。 提取处理程序对相关 `RenditionPicker` 选择的特定演绎版发挥作用（请参阅 `ExtractionHandler` API）。标准 [!DNL Experience Manager] 可以安装以下内容：
   * IDML导出提取句柄：在 `IDML` 在“媒体提取”步骤中生成的呈现版本。

* **页面名称**:指定要分配给结果页面的名称。 如果留空，则名称为“page”（或者如果“page”已存在，则为派生项）。

* **页面标题**:指定要分配给结果页面的标题。

* **页面根路径**:生成页面的根位置的路径。 如果留空，则将使用包含资产演绎版的节点。

* **页面模板**:在生成结果页面时使用的模板。

* **页面设计**:在生成结果页面时要使用的页面设计。

### 为配置代理工作程序 [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>工作程序驻留在代理实例上。

1. 在工具控制台中，展开 **[!UICONTROL Cloud Services配置]** 中。 然后展开 **[!UICONTROL 云代理配置]**.

1. 双击 **[!UICONTROL IDS worker]** 以打开进行配置。

1. 单击 **[!UICONTROL 编辑]** 要打开配置对话框并定义所需的设置，请执行以下操作：

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS池**
用于与通信的SOAP端点 [!DNL InDesign Server]. 您可以添加、删除和订购项目。

1. 单击确定进行保存。

### 配置Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

如果 [!DNL InDesign Server] 和 [!DNL Experience Manager] 位于不同的主机上，或者其中一个或两个应用程序在默认端口上不工作，然后进行配置 [!UICONTROL Day CQ链接外部器] 为 [!DNL InDesign Server].

1. 访问Web控制台(位于 `https://[aem_server]:[port]/system/console/configMgr`.
1. 找到配置 **[!UICONTROL Day CQ链接外部器]**. 单击 **[!UICONTROL 编辑]** 打开。
1. 链接外部器设置可帮助为 [!DNL Experience Manager] 部署和 [!DNL InDesign Server]. 使用 **[!UICONTROL 域]** 字段，以指定 [!DNL Adobe InDesign Server]. 单击“**保存**”。

   在绝对URL中，使用 `localhost` 作为本地（作者）实例的主机名，以及发布实例的主机名或IP地址，如下图所示。

   ![链接外部器设置](assets/link-externalizer-config.png)

### 为启用并行作业处理 [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

您现在可以为ID启用并行作业处理。 确定最大并行作业数(`x`) [!DNL InDesign Server] 可以处理：

* 在单台多处理器计算机上，并行作业的最大数(`x`) [!DNL InDesign Server] 可以处理的数量比运行ID的处理器数量少一个。
* 在多台计算机上运行ID时，您需要计算可用处理器总数（即所有计算机上的处理器总数），然后减去计算机总数。

要配置并行ID作业的数量，请执行以下操作：

1. 打开 **[!UICONTROL 配置]** Felix Console的选项卡；例如： `https://[aem_server]:[port]/system/console/configMgr`.

1. 在下选择IDS处理队列 `Apache Sling Job Queue Configuration`.

1. 套:

   * **类型** - `Parallel`
   * **最大并行作业数** - `<*x*>` （如上文计算）

1. 保存这些更改。
1. 要为AdobeCS6及更高版本启用多会话支持，请检查 `enable.multisession.name` 复选框，在下 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 配置。
1. 创建 [池 `x` 通过向IDS Worker配置添加SOAP端点来IDS工作器](#configuring-the-proxy-worker-for-indesign-server).

   如果有多台计算机正在运行 [!DNL InDesign Server]，为每台计算机添加SOAP端点（每台计算机的处理器数–1）。

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>使用工作程序池时，您可以启用IDS工作程序的阻止列表。
>
>为此，请启用 **[!UICONTROL enable.retry.name]** 复选框，位于 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 配置，用于启用IDS作业检索。
>
>此外，在 `com.day.cq.dam.ids.impl.IDSPoolImpl.name` 配置，为 `max.errors.to.blacklist` 参数，该参数可确定在从作业处理程序列表中禁止ID之前的作业检索次数。
>
>默认情况下，在`retry.interval.to.whitelist.name`)重新验证IDS工作程序的时间（以分钟为单位）。 如果在线找到该工作程序，则会将其从阻止列表中删除。

## 为 [!DNL InDesign Server] 10.0或更高版本 {#enabling-support-for-indesign-server-or-later}

对于 [!DNL InDesign Server] 10.0或更高版本，请执行以下步骤以启用多会话支持。

1. 从 [!DNL Experience Manager Assets] 实例 `https://[aem_server]:[port]/system/console/configMgr`.
1. 编辑配置 `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. 选择 **[!UICONTROL ids.cc.enable]** 选项，然后单击 **[!UICONTROL 保存]**.

>[!NOTE]
>
>对于 [!DNL InDesign Server] 集成 [!DNL Experience Manager Assets]，请使用多核处理器，因为单核系统不支持集成所需的会话支持功能。

## 配置 [!DNL Experience Manager] 凭据 {#configure-aem-credentials}

您可以更改访问的默认管理员凭据（用户名和密码） [!DNL InDesign Server] 从 [!DNL Experience Manager] 部署时不会中断与 [!DNL InDesign Server].

1. 转到 `/etc/cloudservices/proxy.html`.
1. 在对话框中，指定新的用户名和密码。
1. 保存凭据。

>[!MORELIKETHIS]
>
>* [关于Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

