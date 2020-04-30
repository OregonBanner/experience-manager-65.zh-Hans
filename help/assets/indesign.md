---
title: 将[!DNL Adobe Experience Manager Assets]与[!DNL Adobe InDesign Server]集成
description: 了解如何将[!DNL Adobe Experience Manager Assets]与[!DNL Adobe InDesign Server]集成。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 集成 [!DNL Adobe Experience Manager Assets] 于 [!DNL Adobe InDesign Server]{#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] 使用:

* 用于分配特定处理任务的负载的代理。 代理是与代理 [!DNL Experience Manager] 工作器通信以实现特定任务的实例，而其他实例 [!DNL Experience Manager] 则用于传送结果。
* 用于定义和管理特定任务的代理Worker。
这可以涵盖各种任务;例如，使用 [!DNL InDesign Server] 处理文件。

将文件完全上传 [!DNL Experience Manager Assets] 到您使用代理创建 [!DNL Adobe InDesign] 的文件。 它使用代理Worker与进行通信 [!DNL Adobe InDesign Server]，运行脚 [本](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) ，以提取元数据并为其生成各种再现 [!DNL Experience Manager Assets]。 代理Worker支持云配置中的实例 [!DNL InDesign Server] 与实 [!DNL Experience Manager] 例之间的双向通信。

>[!NOTE]
>
>[!DNL Adobe InDesign] 作为两个单独的产品提供。 [Adobe InDesign桌面应用程序](https://www.adobe.com/products/indesign.html) ，用于设计用于印刷和数字分发的页面布局。 [Adobe InDesign Server使您能够](https://www.adobe.com/products/indesignserver.html) 根据您使用创建的内容有计划地创建自动文档 [!DNL InDesign]。 它作为服务运行，为其 [ExtendScript引擎提供接口。脚本编写](https://www.adobe.com/devnet/scripting.html) ，类似于 [!DNL ExtendScript][!DNL JavaScript]。 有关脚本的 [!DNL InDesign] 信息，请参 [阅https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)。

## 提取的工作原理 {#how-the-extraction-works}

可以 [!DNL Adobe InDesign Server] 与集成，以便 [!DNL Experience Manager Assets][!DNL InDesign] 上传使用创建的INDD文件、生成再现、提取所有媒体（例如，视频）并存储为资产：

>[!NOTE]
>
>旧版本 [!DNL Experience Manager] 能够提取XMP和缩略图，现在可以提取所有媒体。

1. 将INDD文件上传到 [!DNL Experience Manager Assets]。
1. 框架通过SOAP(简单对象访问协 [!DNL InDesign Server] 议)将命令脚本发送到。
此命令脚本将：

   * 检索INDD文件。
   * 执行 [!DNL InDesign Server] 命令：

      * 将提取结构、文本和任何媒体文件。
      * 将生成PDF和JPG再现。
      * 将生成HTML和IDML再现。
   * 将生成的文件发布回 [!DNL Experience Manager Assets]。
   >[!NOTE]
   >
   >IDML是一种基于XML的格式，可呈现文件的所有 [!DNL InDesign] 内容。 它使用 [ZIP压缩作为压缩包存](https://www.techterms.com/definition/zip) 储。 有关详细信息，请参 [阅InDesign Interchange Formats INX和IDML](http://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8)。

   >[!CAUTION]
   >
   >如果尚 [!DNL InDesign Server] 未安装或未配置，则仍可将INDD文件上传到 [!DNL Experience Manager]。 但是，生成的演绎版将限于PNG和JPEG。 您将无法生成HTML、.idml或页面再现。

1. 生成提取和再现后：

   * 此结构将复制到一 `cq:Page` 个（演绎版类型）。
   * 提取的文本和文件存储在中 [!DNL Experience Manager Assets]。
   * 所有演绎版都存储 [!DNL Experience Manager Assets]在资产本身中。

## 与AEM [!DNL InDesign Server] 集成 {#integrating-the-indesign-server-with-aem}

要集成以 [!DNL InDesign Server] 便与配置代 [!DNL Experience Manager Assets] 理一起使用，您需要：

1. [安装InDesign Server](#installing-the-indesign-server)。
1. 如果需要， [请配置Experience Manager资产工作流](#configuring-the-aem-assets-workflow)。
仅当默认值不适用于您的实例时，才需要这样做。
1. 为InDesign [Server配置代理Worker](#configuring-the-proxy-worker-for-indesign-server)。

### 安装 [!DNL InDesign Server]{#installing-the-indesign-server}

要安装并开始以 [!DNL InDesign Server] 便与以下对象一起使用 [!DNL Experience Manager]:

1. 下载并安装 [!DNL InDesign Server]。

1. 如果需要，您可以自定义实例的 [!DNL InDesign Server] 配置。

1. 从命令行开始服务器：

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   这将使服务器开始SOAP插件在端口8080上监听。 所有日志消息和输出都直接写入命令窗口。

   >[!NOTE]
   >
   >如果要将输出消息保存到文件，则使用重定向；例如，在Windows下：
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### 配置工作 [!DNL Experience Manager Assets] 流 {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] 具有预配置的工作流 **[!UICONTROL DAM更新资产]**，该工作流具有几个流程步骤，专门用于 [!DNL InDesign]:

* [媒体提取](#media-extraction)
* [页面提取](#page-extraction)

此工作流设置了默认值，这些默认值可以适应您在各种创作实例上的设置(这是一个标准工作流，因此在“编辑工作流”下可 [以获得更多信息](/help/sites-developing/workflows-models.md#configuring-a-workflow-step))。 如果您使用默认值（包括SOAP端口），则不需要任何配置。

设置完成后，将文 [!DNL InDesign] 件上传到 [!DNL Experience Manager Assets] （通过任何常用方法）会触发处理资产和准备各种演绎版的工作流。 将INDD文件上传到中以测试您的配 [!DNL Experience Manager Assets] 置，以确认您看到IDS创建的不同再现 `<*your_asset*>.indd/Renditions`

#### Media extraction {#media-extraction}

此步骤控制媒体从INDD文件的提取。

要进行自定义，可以编辑&#x200B;**[!UICONTROL 媒体提取]**&#x200B;步骤的&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡。

![媒体提取参数和脚本路径](assets/media_extraction_arguments_scripts.png)

媒体提取参数和脚本路径

* **ExtendScript库**:这是一个简单的http get/post方法库，其他脚本需要它。

* **扩展脚本**:您可以在此处指定不同的脚本组合。 如果希望在上执行您自己的脚本，请 [!DNL InDesign Server]将脚本保存在 `/apps/settings/dam/indesign/scripts`。

有关InDesign脚本的信息，请参阅 [InDesign开发人员文档](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>请勿更改 ExtendScript 库。此库提供与Sling通信所需的HTTP功能。 此设置指定要发送到的库以 [!DNL InDesign Server] 便在那里使用。

由媒 `ThumbnailExport.jsx` 体提取工作流步骤运行的脚本生成JPG格式的缩略图再现。 此演绎版由“流程缩略图”工作流步骤用于生成所需的静态演绎版 [!DNL Experience Manager]。

您可以配置“流程缩略图”工作流步骤以生成大小不同的静态演绎版。 确保不删除默认值，因为界面要求使用这些默认值 [!DNL Experience Manager Assets] 。 最后，删除图像预览再现工作流步骤将删除。jpg缩略图再现，因为不再需要它。

#### Page extraction {#page-extraction}

这会从提取 [!DNL Experience Manager] 的元素创建一个页面。 提取处理程序用于从再现（当前为HTML或IDML）中提取数据。 此数据随后用于使用PageBuilder创建页面。

要进行自定义，可以编辑&#x200B;**[!UICONTROL 页面提取]**&#x200B;步骤的&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡。

![chlimage_1-96](assets/chlimage_1-289.png)

* **页面提取处理程序**:从弹出式列表中，选择要使用的处理函数。 提取处理程序对由相关 `RenditionPicker` 选择的特定呈现进行操作（请参阅 `ExtractionHandler` API）。
In a standard [!DNL Experience Manager] installation the following is available:
   * IDML导出提取句柄：对在MediaExtract步 `IDML` 骤中生成的再现进行操作。

* **页面名称**:指定要分配给结果页面的名称。 如果留空，则名称为“page”（如果“page”已存在，则为派生名称）。

* **页面标题**:指定要分配给结果页面的标题。

* **页面根路径**:生成页面的根位置的路径。 如果保留为空，则将使用包含资产演绎版的节点。

* **页面模板**:生成结果页面时要使用的模板。

* **页面设计**:生成生成页面时要使用的页面设计。

### 为配置代理Worker [!DNL InDesign Server]{#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>该worker驻留在代理实例上。

1. 在工具控制台中，展开 **[!UICONTROL 左侧窗格中的云服务配置]** 。 然后展开 **[!UICONTROL 云代理配置]**。

1. 双击 **[!UICONTROL IDS worker]** 以打开进行配置。

1. 单击 **[!UICONTROL 编辑]** ，打开配置对话框并定义所需的设置：

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS池**&#x200B;用于与通信的SOAP端点 [!DNL InDesign Server]。 您可以添加、删除和订购项目。

1. 单击确定进行保存。

### 配置Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

如果在不 [!DNL InDesign Server] 同的主机上运行 [!DNL Experience Manager] ，或者上述两种应用程序都未在默认端口上运行，请配置 [!UICONTROL Day CQ Link Externalizer] ，以设置主机名、端口和内容路径 [!DNL InDesign Server]。

1. 访问Web控制台(位于 `https://[aem_server]:[port]/system/console/configMgr`)。
1. Locate the configuration **[!UICONTROL Day CQ Link Externalizer]**, and tap **[!UICONTROL Edit]** to open it.
1. 指定主机名和上下文路径，然后 [!DNL Indesign Server] 单击“保 **存”**。

   ![chlimage_1-97](assets/chlimage_1-290.png)

### 支持并行作业处理 [!DNL InDesign Server]{#enabling-parallel-job-processing-for-indesign-server-s}

您现在可以为IDS启用并行作业处理。 确定可处理的并行作业(`x`)的最 [!DNL InDesign Server] 大数量：

* 在单个多处理器机器上，可处理的并行作业(`x`)的最 [!DNL InDesign Server] 大数目比运行IDS的处理器数少一个。
* 在多台计算机上运行ID时，您需要计算可用处理器的总数（即在所有计算机上），然后减去计算机的总数。

要配置并行IDS作业的数量，请执行以下操作：

1. 打开Felix **[!UICONTROL Console的]** “配置”选项卡；例如： `https://[aem_server]:[port]/system/console/configMgr`.

1. 在下选择IDS处理队列 `Apache Sling Job Queue Configuration`。

1. 套:

   * **类型** - `Parallel`
   * **最大并行作业** - `<*x*>` （如上所计算）

1. 保存这些更改。
1. 要启用对Adobe CS6和更高版本的多会话支持，请选中配置下 `enable.multisession.name` 的复选框 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 复选框。
1. 通过向 [IDS Worker配 `x` 置添加SOAP端点，创建IDS Worker池](#configuring-the-proxy-worker-for-indesign-server)。

   如果有多台计算机正在运 [!DNL InDesign Server]行，请为每台计算机添加SOAP端点（每台计算机的处理器数-1）。

   >[!NOTE]
   >
   >您可以选择在处理大量员工时启用IDS工作人员的黑名单。
   >
   >
   >为此，请在配置下启 **[!UICONTROL 用enable.retry.name]** 复选框 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` ，该复选框将启用IDS作业检索。
   >
   >
   >此外，在该配 `com.day.cq.dam.ids.impl.IDSPoolImpl.name` 置下，为参数设置一个正值，该参数在禁止IDS从作业处理程序列表之 `max.errors.to.blacklist` 前确定作业检索的数量。
   >
   >
   >默认情况下，在IDS Worker经过可配置(retry.interval.to.whitelist.name)时间（以分钟为单位）后，将重新验证IDS Worker。 如果在线找到该员工，则该员工会从黑名单中删除。

## 支持 [!DNL InDesign Server] 10.0或更高版本 {#enabling-support-for-indesign-server-or-later}

对于 [!DNL InDesign Server] 10.0或更高版本，请执行以下步骤以启用多会话支持。

1. 从实例中打开配置 [!DNL Experience Manager Assets] 管理器 `https://[aem_server]:[port]/system/console/configMgr`。
1. 编辑配置 `com.day.cq.dam.ids.impl.IDSJobProcessor.name`。
1. Select the **[!UICONTROL ids.cc.enable]** option, and click **[!UICONTROL Save]**.

>[!NOTE]
>
>要 [!DNL InDesign Server] 与集 [!DNL Experience Manager Assets]成，请使用多核处理器，因为单核系统不支持集成所需的会话支持功能。

## 配置凭 [!DNL Experience Manager] 据 {#configure-aem-credentials}

您可以更改从实例访问的默认管理员凭据(用户名和 [!DNL InDesign Server] 口令), [!DNL Experience Manager] 而不中断与的集成 [!DNL InDesign Server]。

1. 转到 `/etc/cloudservices/proxy.html`.
1. 在对话框中，指定新的用户名和密码。
1. 保存凭据。

>[!MORELIKETHIS]
>
>* [关于Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

