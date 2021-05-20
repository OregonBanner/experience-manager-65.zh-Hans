---
title: 批量迁移资产
description: 介绍如何将资产引入 [!DNL Adobe Experience Manager]、应用元数据、生成演绎版，以及如何激活资产以发布实例。
contentOwner: AG
role: Architect, Administrator
feature: 迁移，演绎版，资产管理
exl-id: 184f1645-894a-43c1-85f5-8e0d2d77aa73
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 8%

---

# 如何批量迁移资产{#assets-migration-guide}

将资产迁移到[!DNL Adobe Experience Manager]时，需要考虑以下几个步骤。 将资产和元数据从其当前主页提取出不在本文档的范围之内，因为不同实施之间的资产和元数据差异很大，但本文档介绍了如何将这些资产引入[!DNL Experience Manager]、应用其元数据、生成演绎版，以及激活它们以发布实例。

## 前提条件 {#prerequisites}

在实际执行此方法中的任何步骤之前，请查看并实施[资产性能调整提示](performance-tuning-guidelines.md)中的指南。 许多步骤（如配置最大并发作业）都极大地提高了服务器在负载下的稳定性和性能。 在系统加载了资产后，执行其他步骤（如配置文件数据存储）的难度要大得多。

>[!NOTE]
>
>以下资产迁移工具不属于[!DNL Experience Manager]的一部分，因此不受Adobe支持：
>
>* ACS AEM Tools Tag Maker
>* ACS AEM工具CSV资产导入程序
>* ACS Commons Bulk Workflow Manager
>* ACS Commons Fast Action Manager
>* 合成工作流

>
>
本软件是开放源软件，受 [Apache v2 许可证](https://adobe-consulting-services.github.io/pages/license.html)的保护。要提出问题或报告问题，请访问[针对 ACS AEM 工具的 GitHub 问题](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues)和 [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues)。

## 迁移到[!DNL Experience Manager] {#migrating-to-aem}

将资产迁移到[!DNL Experience Manager]需要多个步骤，应将其视为一个分阶段的过程。 迁移阶段如下：

1. 禁用工作流。
1. 加载标记。
1. 摄取资产。
1. 处理演绎版。
1. 激活资产。
1. 启用工作流。

![chlimage_1-223](assets/chlimage_1-223.png)

### 禁用工作流{#disabling-workflows}

在开始迁移之前，请禁用[!UICONTROL  DAM更新资产]工作流的启动器。 最好将所有资产摄取到系统中，然后批量运行工作流。 如果迁移过程中您已经处于实时状态，则可以安排这些活动在非工作时间运行。

### 加载标记{#loading-tags}

您可能已经拥有了要应用于图像的标记分类。 虽然CSV资产导入器和[!DNL Experience Manager]支持元数据配置文件之类的工具可以自动将标记应用到资产的过程，但需要将标记加载到系统中。 [ACS AEM Tools Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html)功能允许您使用加载到系统中的Microsoft Excel电子表格来填充标记。

### 摄取资产{#ingesting-assets}

在将资产摄取到系统中时，性能和稳定性是重要的考虑因素。 由于您正在将大量数据加载到系统中，因此您需要确保系统能够正常运行，并尽可能减少所需时间，避免系统过载，这可能导致系统崩溃，特别是在已在生产中的系统中。

将资产加载到系统中的方法有两种：使用HTTP的基于推送的方法，或使用JCR API的基于拉取的方法。

#### 通过HTTP {#pushing-through-http}发送

Adobe的Managed Services团队使用名为Glutton的工具将数据加载到客户环境中。 Glutton是一个小型Java应用程序，用于将所有资产从一个目录加载到[!DNL Experience Manager]部署中的另一个目录中。 您还可以使用诸如Perl脚本之类的工具将资产发布到存储库中，而不是Glutton。

使用通过https的方法有两个主要的缺点：

1. 需要通过HTTP将资产传输到服务器。 这需要相当多的开销并且非常耗时，从而延长了执行迁移所花费的时间。
1. 如果您的标记和自定义元数据必须应用于资产，则此方法需要再运行一个自定义流程，以便在导入资产后将此元数据应用于资产。

摄取资产的另一种方法是从本地文件系统中提取资产。 但是，如果您无法将外部驱动器或网络共享装载到服务器以执行基于拉取的方法，则最好通过HTTP发布资产。

#### 从本地文件系统{#pulling-from-the-local-filesystem}获取

[ACS AEM工具CSV资产导入器](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html)从文件系统中提取资产，并从CSV文件中提取资产元数据以导入资产。 Experience Manager资产管理器API用于将资产导入系统并应用配置的元数据属性。 理想情况下，资产通过网络文件装载或通过外部驱动器装载到服务器上。

由于资产不需要通过网络传输，因此总体性能会显着提高，而且这种方法通常被视为将资产加载到存储库的最有效方法。 此外，由于该工具支持元数据摄取，因此您可以在一个步骤中导入所有资产和元数据，而无需再另外创建一个步骤来通过单独的工具应用元数据。

### 处理演绎版{#processing-renditions}

将资产加载到系统中后，您需要通过[!UICONTROL DAM更新资产]工作流处理这些资产，以提取元数据并生成演绎版。 在执行此步骤之前，您需要复制并修改[!UICONTROL DAM更新资产]工作流，以满足您的需求。 现成的工作流包含许多您可能不需要的步骤，例如Dynamic Media PTIFF生成或[!DNL InDesign Server]集成。

根据需要配置工作流后，有两个选项可用于执行该工作流：

1. 最简单的方法是[ACS Commons&#39; Bulk Workflow Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html)。 利用此工具，可执行查询并通过工作流处理查询结果。 还有一些选项可用于设置批处理大小。
1. 您可以将 [ACS Commons Fast Action Manager与Synthetic Workflows一起使](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) 用 [](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html)。 虽然此方法涉及的范围更广，但它允许您在优化服务器资源的使用时删除[!DNL Experience Manager]工作流引擎的开销。 此外，Fast Action manager还通过动态监视服务器资源和限制系统上的负载来进一步提升性能。 ACS Commons功能页上提供了示例脚本。

### 激活资产{#activating-assets}

对于具有发布层的部署，您需要将资产激活到发布场。 虽然Adobe建议运行多个发布实例，但最有效的方法是将所有资产复制到单个发布实例，然后克隆该实例。 激活大量资产时，在触发树激活后，您可能需要干预。 原因如下：触发激活时，项目会添加到Sling作业/事件队列。 此队列的大小开始超过大约40,000个项目后，处理速度会急剧减慢。 当此队列的大小超过100,000个项目后，系统稳定性开始受到影响。

要解决此问题，您可以使用[快速操作管理器](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html)管理资产复制。 这在不使用Sling队列的情况下可正常工作，从而降低开销，同时限制工作负载以防止服务器过载。 有关使用FAM管理复制的示例，请参见该功能的文档页面。

将资产转至发布场的其他选项包括使用 [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) 或 [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)，这些选项作为 Jackrabbit 中的工具提供。另一个选项是为[!DNL Experience Manager]基础结构使用一个名为[Grabbit](https://github.com/TWCable/grabbit)的开源工具，该工具声称比vlt的性能更快。

对于这些方法中的任何一种方法，我们应当注意，创作实例上的资产未显示为已激活。 要使用正确的激活状态标记这些资产，您还需要运行一个脚本来将资产标记为已激活。

>[!NOTE]
>
>Adobe不维护或支持Grabbit。

### 克隆发布{#cloning-publish}

激活资产后，您可以克隆发布实例，以创建部署所需的任意数量的副本。 克隆服务器相当简单，但需要记住一些重要步骤。 要克隆发布，请执行以下操作：

1. 备份源实例和数据存储。
1. 将实例和数据存储的备份还原到目标位置。 以下步骤均引用此新实例。
1. 在`crx-quickstart/launchpad/felix`下对`sling.id`执行文件系统搜索。 删除此文件。
1. 在数据存储的根路径下，找到并删除任何`repository-XXX`文件。
1. 编辑`crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`和`crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config`以指向新环境中数据存储的位置。
1. 启动环境。
1. 更新作者上任何复制代理的配置，以指向新实例上正确的发布实例或调度程序刷新代理，以指向新环境的正确调度程序。

### 启用工作流{#enabling-workflows}

完成迁移后，应重新启用[!UICONTROL  DAM更新资产]工作流的启动器，以支持生成演绎版并提取元数据，以便持续使用日常系统。

## 跨[!DNL Experience Manager]部署{#migrating-between-aem-instances}迁移

虽然这种情况并不常见，但有时您需要将大量数据从一个[!DNL Experience Manager]部署迁移到另一个部署；例如，执行[!DNL Experience Manager]升级、升级硬件或迁移到新数据中心时，例如通过AMS迁移。

在这种情况下，您的资产已经填充了元数据，并且已经生成了演绎版。 您只需将精力集中在将资产从一个实例移动到另一个实例即可。 在[!DNL Experience Manager]部署之间迁移时，请执行以下步骤：

1. 禁用工作流：由于您正在迁移演绎版和我们的资产，因此您希望禁用[!UICONTROL DAM更新资产]工作流的工作流启动器。

1. 迁移标记：由于源[!DNL Experience Manager]部署中已加载标记，因此可以在内容包中构建标记，并将该包安装到目标实例上。

1. 迁移资产：建议使用以下两种工具将资产从一个[!DNL Experience Manager]部署移动到另一个部署：

   * **Vault Remote** Copy或vlt rcp允许您跨网络使用vlt。您可以指定源目录和目标目录，然后vlt从一个实例下载所有存储库数据并将其加载到另一个实例。 Vlt rcp记录在[https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **** Grabbitis是由时代华纳有线公司为实施它而开发的一种开源内容同步 [!DNL Experience Manager] 工具。由于它使用连续数据流，与vlt rcp相比，它具有更低的延迟，并声称速度比vlt rcp快2到10倍。 Grabbit还仅支持增量内容的同步，这允许它在完成初始迁移过程后同步更改。

1. 激活资产：按照为初始迁移到[!DNL Experience Manager]记录的[激活资产](#activating-assets)的说明进行操作。

1. 克隆发布：与新迁移一样，加载单个发布实例并克隆该实例比在两个节点上激活内容更有效。 请参阅[克隆发布。](#cloning-publish)

1. 启用工作流：完成迁移后，请重新启用[!UICONTROL  DAM更新资产]工作流的启动器，以支持生成演绎版并提取元数据，以便持续使用日常系统。
