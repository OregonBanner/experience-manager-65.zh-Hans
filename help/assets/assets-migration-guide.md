---
title: 批量迁移资产
description: 介绍如何将资产引入 [!DNL Adobe Experience Manager]，应用元数据，生成演绎版，并将其激活到发布实例。
contentOwner: AG
role: Architect, Admin
feature: Migration,Renditions,Asset Management
exl-id: 184f1645-894a-43c1-85f5-8e0d2d77aa73
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 8%

---

# 如何批量迁移资产 {#assets-migration-guide}

将资产迁移到时 [!DNL Adobe Experience Manager]，则需要考虑以下几个步骤。 从当前主目录中提取资源和元数据超出了此文档的范围，因为不同实施之间的资产和元数据差别很大，但本文档介绍了如何将这些资产提取到 [!DNL Experience Manager]，应用其元数据，生成演绎版，并将其激活到发布实例。

## 前提条件 {#prerequisites}

在实际执行此方法中的任何步骤之前，请查看并实施 [资产性能调整提示](performance-tuning-guidelines.md). 通过配置最大并发作业等许多步骤，可以大大提高服务器在负载下的稳定性和性能。 加载系统资产后，其他步骤（如配置文件数据存储）的执行难度会大得多。

>[!NOTE]
>
>以下资源迁移工具不包含在内 [!DNL Experience Manager] Adobe不支持和：
>
>* ACS AEM工具标记生成器
>* ACS AEM工具CSV资产导入程序
>* ACS Commons批量工作流管理器
>* ACS Commons快速操作管理器
>* 合成工作流
>
>本软件是开放源软件，受 [Apache v2 许可证](https://adobe-consulting-services.github.io/pages/license.html)的保护。要提出问题或报告问题，请访问[针对 ACS AEM 工具的 GitHub 问题](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues)和 [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues)。

## 迁移至 [!DNL Experience Manager] {#migrating-to-aem}

将资产迁移到 [!DNL Experience Manager] 需要执行多个步骤，应视为分阶段执行的过程。 迁移的阶段如下：

1. 禁用工作流。
1. 加载标记。
1. 引入资产。
1. 处理演绎版。
1. 激活资产。
1. 启用工作流。

![chlimage_1-223](assets/chlimage_1-223.png)

### 禁用工作流 {#disabling-workflows}

在开始迁移之前，请为禁用启动器 [!UICONTROL DAM更新资产] 工作流。 最好将所有资产摄取到系统中，然后批量运行工作流。 如果您已在迁移过程中处于活动状态，则可以安排这些活动在休息时间运行。

### 加载标记 {#loading-tags}

您可能已经有一个要应用于图像的标记分类。 而工具(如CSV资产导入程序和 [!DNL Experience Manager] 对元数据配置文件的支持可以自动将标记应用到资产的过程，标记需要加载到系统中。 此 [ACS AEM工具标记生成器](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) 功能允许您使用加载到系统中的某个Microsoft Excel电子表格来填充标记。

### 引入资产 {#ingesting-assets}

在将资产引入系统时，性能和稳定性是重要考虑事项。 由于您要将大量数据加载到系统中，因此希望确保系统能够正常执行，并且能够将所需的时间减至最少，同时避免系统过载，因为这样做可能会导致系统崩溃，尤其是在已经处于生产状态的系统中。

有两种将资产加载到系统中的方法：使用HTTP的基于推送的方法或使用JCR API的基于拉取的方法。

#### 通过HTTP发送 {#pushing-through-http}

Adobe的Managed Services团队使用名为Glutton的工具将数据加载到客户环境中。 Glutton是一个小型Java应用程序，它将所有资产从一个目录加载到上的另一个目录中。 [!DNL Experience Manager] 部署。 您还可以使用Perl脚本等工具将资产发布到存储库中，而不是Glutton。

使用https推送方法有两个主要缺点：

1. 资产需要通过HTTP传输到服务器。 这需要相当多的开销并非常耗时，因此会延长执行迁移所需的时间。
1. 如果您必须将标记和自定义元数据应用于资源，则此方法需要运行另一个自定义流程，在导入资源后，您需要运行该流程才能将此元数据应用于资源。

摄取资产的另一种方法是从本地文件系统提取资产。 但是，如果不能将外部驱动器或网络共享装载到服务器以执行基于拉取的方法，则通过HTTP发布资源是最佳选择。

#### 从本地文件系统获取 {#pulling-from-the-local-filesystem}

此 [ACS AEM工具CSV资产导入程序](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) 从文件系统中提取资源，从CSV文件提取资源元数据以用于资源导入。 Experience Manager资源管理器API用于将资源导入系统，并应用配置的元数据属性。 理想情况下，资产可通过网络文件装载或外部驱动器装载到服务器上。

由于资产不需要通过网络传输，因此整体性能会显着提升，通常认为此方法是将资产加载到存储库的最有效方法。 此外，由于该工具支持元数据摄取，因此您可以在单个步骤中导入所有资源和元数据，而不是同时创建第二个步骤来通过单独的工具应用元数据。

### 流程演绎版 {#processing-renditions}

将资产加载到系统后，您需要通过 [!UICONTROL DAM更新资产] 此工作流用于提取元数据和生成演绎版。 在执行此步骤之前，您需要复制并修改 [!UICONTROL DAM更新资产] 工作流以满足您的需求。 这个现成的工作流包含许多您可能不需要执行的步骤，例如Dynamic Media PTIFF生成或 [!DNL InDesign Server] 集成。

根据需要配置工作流后，有两个选项可用于执行工作流：

1. 最简单的方法是 [ACS Commons的批量工作流管理器](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). 使用此工具，您可以执行查询，并通过工作流处理查询的结果。 也可以选择设置批次大小。
1. 您可以将 [ACS Commons Fast Action Manager与Synthetic Workflows一起使](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) 用 [](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html)。 虽然此方法涉及的范围更广，但它允许您删除 [!DNL Experience Manager] 工作流引擎，同时优化服务器资源的使用。 此外，Fast Action manager还通过动态监视服务器资源和限制系统上的负载来进一步提升性能。 ACS Commons功能页上提供了示例脚本。

### 激活资产 {#activating-assets}

对于具有发布层的部署，您需要将资产激活到发布场。 虽然Adobe建议运行多个发布实例，但最有效的方法是将所有资源复制到单个发布实例，然后克隆该实例。 在激活大量资产时，触发树激活后，您可能需要介入。 原因如下：触发激活时，项目将添加到Sling作业/事件队列。 在此队列的大小开始超过约40,000个项目后，处理速度会显着减慢。 当此队列的大小超过100,000个项目后，系统稳定性开始受到影响。

要解决此问题，您可以使用 [快速操作管理器](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) 以管理资产复制。 此操作无需使用Sling队列，从而降低了开销，同时抑制了工作负载以防止服务器过载。 该功能的文档页面上显示了使用FAM管理复制的示例。

将资产转至发布场的其他选项包括使用 [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) 或 [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)，这些选项作为 Jackrabbit 中的工具提供。另一种选择是为 [!DNL Experience Manager] 已调用基础结构 [抓取位](https://github.com/TWCable/grabbit)，它声称比vlt的性能更快。

对于这些方法中的任一方法，需要注意的是，创作实例上的资产不会显示为已激活。 若要以正确的激活状态处理标记这些资产的问题，您还需要运行脚本以将资产标记为已激活。

>[!NOTE]
>
>Adobe不维护或支持Grabbit。

### 克隆发布 {#cloning-publish}

激活资产后，您可以克隆发布实例以创建部署所需的任意数量的副本。 克隆服务器相当简单，但需要记住一些重要步骤。 要克隆发布，请执行以下操作：

1. 备份源实例和数据存储。
1. 将实例和数据存储的备份还原到目标位置。 以下步骤均引用此新实例。
1. 在下执行文件系统搜索 `crx-quickstart/launchpad/felix` 对象 `sling.id`. 删除此文件。
1. 在数据存储的根路径下，找到并删除任意 `repository-XXX` 文件。
1. 编辑 `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 和 `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` 指向数据存储在新环境中的位置。
1. 启动环境。
1. 更新作者上任何复制代理的配置以指向正确的发布实例，或更新新实例上的Dispatcher刷新代理以指向新环境的正确Dispatcher。

### 启用工作流 {#enabling-workflows}

完成迁移后， [!UICONTROL DAM更新资产] 应重新启用工作流以支持演绎版生成和元数据提取，以供日常系统使用。

## 迁移范围 [!DNL Experience Manager] 部署 {#migrating-between-aem-instances}

虽然并非如此常见，但有时您需要从其中迁移大量数据 [!DNL Experience Manager] 部署到另一个环境；例如，当您执行 [!DNL Experience Manager] 升级、升级硬件或迁移到新数据中心，例如使用AMS迁移。

在这种情况下，您的资源已填充元数据，并且已生成演绎版。 您只需关注将资产从一个实例移动到另一个实例即可。 在之间迁移时 [!DNL Experience Manager] 部署，请执行以下步骤：

1. 禁用工作流：由于您正在随我们的资产迁移演绎版，因此要为禁用工作流启动器 [!UICONTROL DAM更新资产] 工作流。

1. 迁移标记：因为源中已加载标记 [!DNL Experience Manager] 部署后，您可以在内容包中构建它们，并在目标实例上安装该包。

1. 迁移资产：建议使用两种工具从一个工具移动资产 [!DNL Experience Manager] 部署到另一个：

   * **保险库远程复制** 或vlt rcp ，允许您通过网络使用vlt。 您可以指定源目录和目标目录，vlt将从一个实例下载所有资料档案库数据，然后将其加载到另一个实例中。 Vlt rcp记录在 [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **抓取位** 是一款开源内容同步工具，由时代华纳有线为其用户开发， [!DNL Experience Manager] 实现。 由于它使用连续的数据流，与vlt rcp相比，它的延迟更小，速度比vlt rcp快2到10倍。 Grabbit还仅支持增量内容的同步，这允许它在完成初始迁移阶段后同步更改。

1. 激活资源：按照的说明操作 [激活资产](#activating-assets) 已记录初始迁移到 [!DNL Experience Manager].

1. 克隆发布：与新迁移一样，加载单个发布实例并进行克隆比在两个节点上激活内容更有效。 请参阅 [正在克隆发布。](#cloning-publish)

1. 启用工作流：完成迁移后，为以下对象重新启用启动器： [!UICONTROL DAM更新资产] 此工作流用于支持演绎版生成和元数据提取，以供日常系统使用。
