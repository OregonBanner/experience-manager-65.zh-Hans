---
title: 批量迁 [!DNL Adobe Experience Manager Assets] 移资产。
description: 介绍如何将资产引入 [!DNL Adobe Experience Manager]、应用元数据、生成演绎版并将其激活以发布实例。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '1800'
ht-degree: 8%

---


# 如何批量迁移资产 {#assets-migration-guide}

将资产迁移到 [!DNL Adobe Experience Manager]中时，需要考虑几个步骤。 从当前主页提取资产和元数据不在此文档的范围内，因为实施之间的差异很大，但此文档介绍如何将这些资产引入、应用其元数据、生成演绎版并激活它们以发布实例。 [!DNL Experience Manager]

## 前提条件 {#prerequisites}

在实际执行此方法中的任何步骤之前，请查看并实施资产性能调整 [提示中的指导](performance-tuning-guidelines.md)。 许多步骤（如配置最大并发作业）都极大地提高了服务器在负载下的稳定性和性能。 其他步骤（如配置文件数据存储）在系统加载资产后更难执行。

>[!NOTE]
>
>以下资产迁移工具不是Adobe的 [!DNL Experience Manager] 一部分，也不受Adobe支持：
>
>* ACS AEM Tools Tag Maker
>* ACS AEM工具CSV资产导入程序
>* ACS Commons Bulk Workflow Manager
>* ACS Commons Fast Action Manager
>* 合成工作流
>
>
本软件是开放源软件，受 [Apache v2 许可证](https://adobe-consulting-services.github.io/pages/license.html)的保护。要提出问题或报告问题，请访问[针对 ACS AEM 工具的 GitHub 问题](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues)和 [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues)。

## 迁移到 [!DNL Experience Manager] {#migrating-to-aem}

将资产迁 [!DNL Experience Manager] 移到需要多个步骤，应将其视为分阶段过程。 迁移的阶段如下：

1. 禁用工作流。
1. 加载标记。
1. 摄取资源。
1. 处理再现。
1. 激活资产。
1. 启用工作流。

![chlimage_1-223](assets/chlimage_1-223.png)

### 禁用工作流 {#disabling-workflows}

在开始迁移之前，请禁用DAM更新资产工 [!UICONTROL 作流的启动] 器。 最好将所有资产引入系统，然后批量运行工作流。 如果迁移时您已经处于活动状态，则可以计划这些活动在非工作时运行。

### 加载标记 {#loading-tags}

您可能已经拥有要应用于图像的标记分类。 虽然CSV资产导入程序和元数据用户档案 [!DNL Experience Manager] 支持等工具可以自动将标记应用到资产的流程，但需要将标记加载到系统中。 利用 [ACS AEM Tools Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) （ACS AEM工具标记生成器）功能，您可以通过使用加载到系统中的Microsoft Excel电子表格填充标记。

### 收录资源 {#ingesting-assets}

在将资产引入系统时，性能和稳定性是重要考虑事项。 由于要将大量数据加载到系统中，因此您需要确保系统能够正常运行，并尽可能减少所需的时间，避免系统过载，这会导致系统崩溃，特别是在已在生产中的系统中。

将资产加载到系统中有两种方法： 使用HTTP的基于推送的方法，或使用JCR API的基于拖曳的方法。

#### 通过HTTP发送 {#pushing-through-http}

Adobe的Managed Services团队使用一种名为Glutton的工具将数据加载到客户环境中。 Glutton是一个小型Java应用程序，它将所有资源从一个目录加载到实例上的另一个 [!DNL Experience Manager] 目录。 您还可以使用Perl脚本等工具将资源发布到存储库中，而不是使用Glutton。

使用通过https的方式有两个主要的缺点：

1. 需要通过HTTP将资源传输到服务器。 这需要相当多的开销，并且非常耗时，从而延长了执行迁移所需的时间。
1. 如果您具有必须应用于资产的标记和自定义元数据，则此方法需要另外一个自定义流程，您需要运行该流程才能在导入资产后将此元数据应用到资产。

获取资源的另一种方法是从本地文件系统中提取资源。 但是，如果无法将外部驱动器或网络共享装入服务器以执行基于拉式的方法，则通过HTTP发布资产是最佳选择。

#### 从本地文件系统读取 {#pulling-from-the-local-filesystem}

ACS [AEM工具CSV资产导入程序](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) ，会从文件系统中提取资产，从CSV文件中提取资产元数据，以便进行资产导入。 Experience Manager Asset Manager API用于将资产导入系统并应用配置的元数据属性。 理想情况下，资产通过网络文件装载或通过外部驱动器装载到服务器上。

由于资产无需通过网络传输，因此总体性能得到显着改善，而且通常认为此方法是将资产加载到存储库中的最有效方法。 此外，由于该工具支持元数据摄取，因此您可以通过一个步骤导入所有资产和元数据，而不是通过另一个工具创建第二个步骤来应用元数据。

### 处理演绎版 {#processing-renditions}

在将资产加载到系统后，您需要通过DAM更新资产工作流 [!UICONTROL 处理资产] ，以提取元数据并生成演绎版。 在执行此步骤之前，您需要重复和修改 [!UICONTROL DAM更新资产工作流] ，以满足您的需求。 现成工作流包含许多您可能不需要的步骤，如Scene7 PTIFF生成或集 [!DNL InDesign Server] 成。

根据需要配置工作流后，您有两个选项可用于执行该工作流：

1. 最简单的方法是 [ACS Commons的Bulk Workflow Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html)。 此工具允许您执行查询并通过工作流处理查询结果。 还有设置批大小的选项。
1. 您可以将 [ACS Commons Fast Action Manager与Synthetic Workflows一起使](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) 用 [](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html)。 While this approach is much more involved, it lets you remove the overhead of the [!DNL Experience Manager] workflow engine while optimizing the use of server resources. 此外，Fast Action manager还通过动态监视服务器资源和限制系统上的负载来进一步提升性能。 ACS Commons功能页上提供了示例脚本。

### 激活资产 {#activating-assets}

对于具有发布层的部署，您需要将资产激活到发布场。 虽然Adobe建议运行多个发布实例，但最有效的方法是将所有资源复制到单个发布实例，然后克隆该实例。 在激活大量资产时，在触发树状激活后，您可能需要进行干预。 原因如下： 触发激活时，项目会添加到Sling作业/事件序列。 当此队列的大小开始超过约40,000个项目时，处理速度会显着降低。 当此队列的大小超过100,000项后，系统稳定性开始会受到影响。

要解决此问题，您可以使用快速操 [作管理器](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) 来管理资产复制。 这样，无需使用Sling队列，即可降低开销，同时还可以限制工作负载以防止服务器过载。 该功能的文档页面上显示了使用FAM管理复制的示例。

将资产转至发布场的其他选项包括使用 [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) 或 [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)，这些选项作为 Jackrabbit 中的工具提供。Another option is to use an open-sourced tool for your [!DNL Experience Manager] infrastructure called [Grabbit](https://github.com/TWCable/grabbit), which claims to have faster performance than vlt.

对于任何这些方法，需要注意的是，作者实例上的资产未显示为已激活。 要使用正确的激活状态标记这些资产，您还需要运行一个脚本来将资产标记为已激活。

>[!NOTE]
>
>Adobe不维护或支持Grabbit。

### 克隆发布 {#cloning-publish}

激活资产后，您可以克隆发布实例以创建部署所需的任意数量的副本。 克隆服务器相当简单，但需要记住一些重要步骤。 要克隆发布：

1. 备份源实例和数据存储。
1. 将实例和数据存储的备份还原到目标位置。 以下步骤均涉及此新实例。
1. Perform a filesystem search under `crx-quickstart/launchpad/felix` for `sling.id`. 删除此文件。
1. 在数据存储的根路径下，找到并删除任何 `repository-XXX` 文件。
1. 编 `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 辑 `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` 并指向新环境上数据存储的位置。
1. 开始环境。
1. 更新作者上任何复制代理的配置以指向新实例上的正确发布实例或调度程序刷新代理，以指向新环境的正确调度程序。

### 启用工作流 {#enabling-workflows}

完成迁移后，应重新启用 [!UICONTROL DAM更新资产工作流的启动器] ，以支持再现生成和元数据提取，以便持续使用日常系统。

## 跨部署 [!DNL Experience Manager] 迁移 {#migrating-between-aem-instances}

虽然不是那么常见，但有时您需要将大量数据从一个实例迁移到另 [!DNL Experience Manager] 一个实例； 例如，当您执行升级 [!DNL Experience Manager] 、升级硬件或迁移到新数据中心时，例如AMS迁移。

在这种情况下，您的资产已填充元数据，并且已生成演绎版。 您只需将精力集中在将资产从一个实例移动到另一个实例上。 在实例之间 [!DNL Experience Manager] 迁移时，您需要执行以下步骤：

1. 禁用工作流: 由于您正在将演绎版与我们的资产一起迁移，因此您希望禁用DAM更新资产工作流 [!UICONTROL 的工作流启动] 器。

1. 迁移标记： 由于已在源实例中加载了标 [!DNL Experience Manager] 记，因此可以在内容包中构建它们并将该包安装在目标实例上。

1. 迁移资产： 建议使用两种工具将资产从一个实例移 [!DNL Experience Manager] 动到另一个：

   * **Vault Remote** Copy或vlt rcp允许您通过网络使用vlt。 您可以指定源目录和目标目录，vlt从一个实例下载所有存储库数据并将其加载到另一个实例。 Vlt rcp在https://jackrabbit.apache.org/filevault/rcp.html上有 [文档](https://jackrabbit.apache.org/filevault/rcp.html)
   * **Grabbit** 是Time Warner Cable为实施而开发的一个开源内容同步 [!DNL Experience Manager] 工具。 由于它使用连续的数据流，与vlt rcp相比，它具有更低的延迟，并声称速度比vlt rcp快2到10倍。 Grabbit还支持仅同步增量内容，这允许它在完成初始迁移通过后同步更改。

1. 激活资产： 按照说明激活 [为初始迁移](#activating-assets) 而记录的资产 [!DNL Experience Manager]。

1. 克隆发布： 与新迁移一样，加载单个发布实例并克隆它比激活两个节点上的内容更有效。 请参 [阅克隆发布。](#cloning-publish)

1. 启用工作流: 完成迁移后，请重新启用DAM更新资产工 [!UICONTROL 作流的启动程序] ，以支持再现生成和元数据提取，以便进行日常系统使用。
