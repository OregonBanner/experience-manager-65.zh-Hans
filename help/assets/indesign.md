---
title: 将 [!DNL Assets] 与 [!DNL InDesign Server]集成
description: 了解如何将 [!DNL Adobe Experience Manager Assets] 与 [!DNL Adobe InDesign Server]集成。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 117208c634613559bb13556e12f094add70006e2
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 4%

---


# 将[!DNL Adobe Experience Manager Assets]与[!DNL Adobe InDesign Server]{#integrating-aem-assets-with-indesign-server}集成

[!DNL Adobe Experience Manager Assets] 使用:

* 用于分配特定处理任务的负载的代理。 代理是与代理工作器通信以实现特定任务的[!DNL Experience Manager]实例，其他[!DNL Experience Manager]实例则用于传送结果。
* 用于定义和管理特定任务的代理工作器。
这些任务可以涵盖多种领域；例如，使用[!DNL InDesign Server]处理文件。

要将文件完全上传到您使用[!DNL Adobe InDesign]创建的[!DNL Experience Manager Assets]代理。 它使用代理工作器与[!DNL Adobe InDesign Server]进行通信，其中运行[脚本](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)以提取元数据并为[!DNL Experience Manager Assets]生成各种再现。 代理工作器在云配置中启用[!DNL InDesign Server]和[!DNL Experience Manager]实例之间的双向通信。

>[!NOTE]
>
>[!DNL Adobe InDesign] 作为两个单独的产品提供。[Adobe](https://www.adobe.com/products/indesign.html) 用于设计印刷和数字分发的页面布局的InDesigndesktop应用程序。[Adobe InDesign](https://www.adobe.com/products/indesignserver.html) ·Serverenals使您能够根据您所用的文档有计划地创建自动化客户 [!DNL InDesign]。它作为服务运行，为其[ExtendScript](https://www.adobe.com/devnet/scripting.html)引擎提供接口。脚本以[!DNL ExtendScript]编写，与[!DNL JavaScript]类似。 有关[!DNL InDesign]脚本的信息，请参阅[https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)。

## 提取的工作方式{#how-the-extraction-works}

[!DNL Adobe InDesign Server]可以与[!DNL Experience Manager Assets]集成，以便上传使用[!DNL InDesign]创建的INDD文件、生成演绎版、提取所有媒体（例如，视频）并存储为资产：

>[!NOTE]
>
>以前版本的[!DNL Experience Manager]能够提取XMP和缩略图，现在可以提取所有媒体。

1. 将INDD文件上传到[!DNL Experience Manager Assets]。
1. 框架通过SOAP（简单对象访问协议）将命令脚本发送到[!DNL InDesign Server]。
此命令脚本将：

   * 检索INDD文件。
   * 执行[!DNL InDesign Server]命令：

      * 将解压结构、文本和任何媒体文件。
      * 将生成PDF和JPG再现。
      * 将生成HTML和IDML再现。
   * 将生成的文件发回[!DNL Experience Manager Assets]。

   >[!NOTE]
   >
   >IDML是一种基于XML的格式，可呈现[!DNL InDesign]文件的所有内容。 它使用[ZIP](https://www.techterms.com/definition/zip)压缩作为压缩包存储。 有关详细信息，请参阅[InDesign交换格式INX和IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8)。

   >[!CAUTION]
   >
   >如果未安装或未配置[!DNL InDesign Server]，则仍可将INDD文件上传到[!DNL Experience Manager]。 但是，生成的演绎版将限制为PNG和JPEG。 您将无法生成HTML、.idml或页面再现。

1. 生成提取和再现后：

   * 此结构将复制到`cq:Page`（再现类型）。
   * 提取的文本和文件存储在[!DNL Experience Manager Assets]中。
   * 所有演绎版都存储在资产本身的[!DNL Experience Manager Assets]中。

## 将[!DNL InDesign Server]与Experience Manager{#integrating-the-indesign-server-with-aem}集成

要集成[!DNL InDesign Server]以与[!DNL Experience Manager Assets]一起使用，并在配置代理后，您需要：

1. [安装InDesign Server](#installing-the-indesign-server)。
1. 如果需要，[配置Experience Manager资产工作流](#configuring-the-aem-assets-workflow)。
仅当默认值不适用于您的实例时，才需要这样做。
1. 为InDesign Server](#configuring-the-proxy-worker-for-indesign-server)配置[代理工作器。

### 安装[!DNL InDesign Server] {#installing-the-indesign-server}

安装并开始[!DNL InDesign Server]以与[!DNL Experience Manager]一起使用：

1. 下载并安装[!DNL InDesign Server]。

1. 如果需要，您可以自定义[!DNL InDesign Server]实例的配置。

1. 从命令行开始服务器：

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   这将使服务器开始SOAP插件监听端口8080。 所有日志消息和输出都直接写入命令窗口。

   >[!NOTE]
   >
   >如果要将输出消息保存到文件，则使用重定向；例如，在Windows下：
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### 配置[!DNL Experience Manager Assets]工作流{#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] 具有预配置的工作流 **[!UICONTROL DAM更新资产]**，该工作流具有几个流程步骤，专门用于 [!DNL InDesign]:

* [媒体提取](#media-extraction)
* [页面提取](#page-extraction)

此工作流设置了默认值，这些默认值可以适应您在各种创作实例上的设置（这是一个标准工作流，因此在[编辑工作流](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)下有进一步的信息）。 如果您使用默认值（包括SOAP端口），则不需要任何配置。

设置完成后，将[!DNL InDesign]文件上传到[!DNL Experience Manager Assets]（通过任何常用方法）会触发处理资产和准备各种演绎版的工作流。 将INDD文件上传到[!DNL Experience Manager Assets]，以确认您看到IDS在`<*your_asset*>.indd/Renditions`下创建的不同再现，从而测试您的配置

#### 媒体提取{#media-extraction}

此步骤控制INDD文件中媒体的提取。

要进行自定义，可以编辑&#x200B;**[!UICONTROL 媒体提取]**&#x200B;步骤的&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡。

![媒体提取参数和脚本路径](assets/media_extraction_arguments_scripts.png)

媒体提取参数和脚本路径

* **ExtendScript图书馆**:这是一个简单的http get/post方法库，其他脚本需要它。

* **扩展脚本**:您可以在此处指定不同的脚本组合。如果希望在[!DNL InDesign Server]上执行您自己的脚本，请在`/apps/settings/dam/indesign/scripts`保存脚本。

有关[!DNL Adobe InDesign]脚本的信息，请参阅[InDesign开发人员文档](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>请勿更改 ExtendScript 库。此库提供与Sling通信所需的HTTP功能。 此设置指定要发送到[!DNL InDesign Server]以供在此使用的库。

由媒体提取工作流步骤运行的`ThumbnailExport.jsx`脚本生成JPG格式的缩略图再现。 此演绎版由“流程缩略图”工作流步骤用于生成[!DNL Experience Manager]所需的静态演绎版。

您可以配置流程缩略图工作流步骤以生成不同大小的静态演绎版。 请确保不删除默认值，因为[!DNL Experience Manager Assets]接口需要这些默认值。 最后，删除图像预览再现工作流步骤将删除JPG缩略图再现，因为不再需要它。

#### 页面提取{#page-extraction}

这将从提取的元素创建[!DNL Experience Manager]页。 提取处理程序用于从再现（当前为HTML或IDML）中提取数据。 此数据随后用于使用PageBuilder创建页面。

要进行自定义，可以编辑&#x200B;**[!UICONTROL 页面提取]**&#x200B;步骤的&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡。

![chlimage_1-96](assets/chlimage_1-289.png)

* **页面提取处理程序**:从弹出列表中，选择要使用的处理函数。提取处理程序对由相关 `RenditionPicker` 选择的特定呈现进行操作（请参阅 `ExtractionHandler` API）。
在标准[!DNL Experience Manager]安装中，可以使用以下内容：
   * IDML导出提取句柄：对在MediaExtract步骤中生成的`IDML`再现进行操作。

* **页面名称**:指定要分配给结果页面的名称。如果留空，则名称为“page”（如果“page”已存在，则为衍生项）。

* **页面标题**:指定要分配给结果页面的标题。

* **页面根路径**:生成页面的根位置的路径。如果留空，则将使用包含资产演绎版的节点。

* **页面模板**:生成结果页面时使用的模板。

* **页面设计**:生成结果页面时要使用的页面设计。

### 为[!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}配置代理工作器

>[!NOTE]
>
>该工作器驻留在代理实例上。

1. 在“工具”控制台中，展开左窗格中的&#x200B;**[!UICONTROL Cloud Services配置]**。 然后展开&#x200B;**[!UICONTROL 云代理配置]**。

1. 双击 **[!UICONTROL IDS worker]** 以打开进行配置。

1. 单击&#x200B;**[!UICONTROL 编辑]**&#x200B;以打开配置对话框并定义所需的设置：

   ![proxy_disworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS**
池用于与通信的SOAP端点 [!DNL InDesign Server]。您可以添加、删除和订购项目。

1. 单击确定进行保存。

### 配置Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

如果[!DNL InDesign Server]和[!DNL Experience Manager]在不同的主机上运行，或者这两个应用程序都不在默认端口上运行，请配置[!UICONTROL  Day CQ Link Externalizer]以设置[!DNL InDesign Server]的主机名、端口和内容路径。

1. 访问位于`https://[aem_server]:[port]/system/console/configMgr`的Web控制台。
1. 找到配置&#x200B;**[!UICONTROL Day CQ Link Externalizer]**，然后单击&#x200B;**[!UICONTROL 编辑]**&#x200B;将其打开。
1. 指定[!DNL Adobe InDesign Server]的主机名和上下文路径，然后单击&#x200B;**保存**。

   ![chlimage_1-97](assets/chlimage_1-290.png)

### 为[!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server-s}启用并行作业处理

您现在可以为IDS启用并行作业处理。 确定[!DNL InDesign Server]可处理的并行作业的最大数量(`x`):

* 在单个多处理器计算机上，[!DNL InDesign Server]可处理的并行作业(`x`)的最大数量比运行IDS的处理器数量少1。
* 在多台计算机上运行ID时，您需要计算可用处理器总数（即在所有计算机上），然后减去计算机总数。

要配置并行IDS作业数：

1. 打开Felix控制台的&#x200B;**[!UICONTROL Configurations]**&#x200B;选项卡；例如：`https://[aem_server]:[port]/system/console/configMgr`。

1. 选择`Apache Sling Job Queue Configuration`下的IDS处理队列。

1. 套:

   * **类型** - `Parallel`
   * **最大并行作业** - `<*x*>` （如上所计算）

1. 保存这些更改。
1. 要启用AdobeCS6和更高版本的多会话支持，请选中`com.day.cq.dam.ids.impl.IDSJobProcessor.name`配置下的`enable.multisession.name`复选框。
1. 通过向IDS Worker配置](#configuring-the-proxy-worker-for-indesign-server)添加SOAP端点，创建`x` IDS Worker的[池。

   如果有多台计算机运行[!DNL InDesign Server]，请为每台计算机添加SOAP端点（每台计算机的处理器数-1）。

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>使用工作池时，您可以启用IDS工作者的阻止列表。
>
>为此，请启用`com.day.cq.dam.ids.impl.IDSJobProcessor.name`配置下的&#x200B;**[!UICONTROL enable.retry.name]**&#x200B;复选框，该配置启用IDS作业检索。
>
>此外，在`com.day.cq.dam.ids.impl.IDSPoolImpl.name`配置下，为`max.errors.to.blacklist`参数设置一个正值，该值在禁止作业处理程序列表的IDS之前确定作业检索的数量。
>
>默认情况下，在以分钟为单位的可配置(`retry.interval.to.whitelist.name`)时间后，IDS工作器将重新验证。 如果在线找到该工作者，则从阻止列表中删除该工作者。

## 支持[!DNL InDesign Server] 10.0或更高版本{#enabling-support-for-indesign-server-or-later}

对于[!DNL InDesign Server] 10.0或更高版本，请执行以下步骤以启用多会话支持。

1. 从您的[!DNL Experience Manager Assets]实例`https://[aem_server]:[port]/system/console/configMgr`打开Configuration Manager。
1. 编辑配置`com.day.cq.dam.ids.impl.IDSJobProcessor.name`。
1. 选择&#x200B;**[!UICONTROL ids.cc.enable]**&#x200B;选项，然后单击&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
>对于与[!DNL Experience Manager Assets]的[!DNL InDesign Server]集成，请使用多核处理器，因为单核系统不支持集成所必需的会话支持功能。

## 配置[!DNL Experience Manager]凭据{#configure-aem-credentials}

您可以更改从[!DNL Experience Manager]部署访问[!DNL InDesign Server]的默认管理员凭据（用户名和密码），而不中断与[!DNL InDesign Server]的集成。

1. 转到 `/etc/cloudservices/proxy.html`.
1. 在对话框中，指定新的用户名和密码。
1. 保存凭据。

>[!MORELIKETHIS]
>
>* [关于Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

