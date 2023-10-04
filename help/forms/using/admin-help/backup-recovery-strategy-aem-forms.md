---
title: AEM表单的备份和恢复策略
description: 了解如何实施策略以备份数据并确保数据与AEM表单数据保持同步。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01ec6ebc-6d80-4417-9604-c8571aebb57e
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '1491'
ht-degree: 0%

---

# AEM表单的备份和恢复策略{#backup-and-recovery-strategy-for-aem-forms}

如果您的AEM表单实施将其他自定义数据存储在其他数据库中，则您负责实施策略以备份此数据并确保其与AEM表单数据保持同步。 此外，应用程序必须设计得足够强健，能够处理其他数据库不同步的情况。 强烈建议在事务上下文中执行任何数据库操作，以帮助保持一致状态。

确定使用AEM表单的方式后，请确定必须备份哪些文件、备份频率以及备份窗口是否可用。

>[!NOTE]
>
>与AEM forms实施的任何其他方面一样，您的备份和恢复策略必须在开发或暂存环境中开发和测试，然后才能用于生产，以确保整个解决方案按预期工作，且不会丢失数据。

Adobe Experience Manager (AEM)是AEM表单的一个组成部分。 因此，您需要备份AEM以及与AEM表单备份同步，因为通信管理解决方案和服务（如表单管理器）都基于AEM表单的AEM部分中所存储的数据。为了防止任何数据丢失，必须备份AEM表单的特定数据，以确保GDS和AEM（存储库）与数据库引用关联。数据库、GDS、AEM和内容存储根目录必须还原到与原始数据库具有相同DNS名称的计算机。

## 备份类型 {#types-of-backups}

AEM Forms备份策略包含两种类型的备份：

**系统映像：** 一种完整的系统备份，可在硬盘或整个计算机停止工作时用于还原计算机的内容。 只有在部署AEM表单之前，才需要执行系统映像备份。 然后，内部公司策略会规定系统映像备份的频率。

**AEM表单特定数据：** 应用程序数据存在于数据库、全局文档存储(GDS)和AEM存储库中，并且必须实时备份。 GDS是用于存储进程中使用的长期文件的目录。 这些文件可能包括PDF、策略或表单模板。

>[!NOTE]
>
>如果已安装Content Services（已弃用），则还要备份内容存储根目录。 请参阅 [内容存储根目录（仅限Content Services）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

数据库用于存储表单对象、服务配置、进程状态以及对GDS文件的数据库引用。 如果启用了数据库中的文档存储，则GDS中的持久数据和文档也存储在数据库中。 可以使用以下方法备份和恢复数据库：

* **快照备份** 模式表示AEM forms系统处于无限期备份模式或在指定的分钟数内处于备份模式，在此之后将不再启用备份模式。 要进入或退出快照备份模式，可以使用以下选项之一。 在恢复方案后，不应启用快照备份模式。

   * 使用管理控制台中的“备份设置”页。 要进入快照模式，请选中“在安全备份模式下操作”复选框。 取消选中该复选框可退出快照模式。
   * 使用LCBackupMode脚本(请参见 [备份数据库、 GDS和内容存储根目录](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories))。 要退出快照备份模式，请在脚本参数中设置 `continuousCoverage` 参数至 `false` 或使用 `leaveContinuousCoverage` 选项。
   * 使用提供的备份/恢复API。 <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **正在滚动备份** 模式表示系统始终处于备份模式，一旦释放上一个会话，就会启动新的备份模式会话。 没有超时与滚动备份模式相关联。 当调用LCBackupMode脚本或API离开滚动备份模式时，将开始新的滚动备份模式会话。 此模式在支持连续备份时非常有用，但仍允许从GDS目录中清除旧文档和不需要的文档。 不支持通过“备份和恢复”页滚动备份模式。 恢复方案后，仍启用滚动备份模式。 您可以将LCBackupMode脚本与 `leaveContinuousCoverage` 选项。

>[!NOTE]
>
>退出滚动备份模式会立即启动新的备份模式会话。 要完全禁用滚动备份模式，请使用 `leaveContinuousCoverage` 脚本中的选项，用于覆盖现有的滚动备份会话。 当处于快照备份模式时，您可以像往常一样退出备份模式。

为防止数据丢失，AEM表单特定数据的备份方式必须确保GDS和内容存储根目录文档与数据库引用关联。

>[!NOTE]
>
>当GDS存储在文件系统上而不是数据库中时，在GDS备份之前执行数据库备份。

## 备份和恢复的特殊注意事项 {#special-considerations-for-backup-and-recovery}

如果由于以下更改而必须将AEM表单恢复到其他环境，请使用以下准则：

* 更改AEM Forms服务器的IP地址、主机名或端口
* 更改驱动器号或目录路径
* 更改为其他数据库主机、端口或名称

通常，此类恢复方案是由承载应用程序服务器、数据库服务器或表单服务器的服务器的硬件故障引起的。 除了本节所述的AEM表单特定配置外，如果AEM表单服务器的主机名或IP地址发生更改，您还应该对AEM表单部署的其他部分（如负载平衡器和防火墙）进行必要的更改。

### 无法更改的内容 {#what-cannot-be-changed}

即使可以更改数据库服务器和许多其他参数，在从备份中恢复AEM表单时，也不能更改应用程序服务器类型或数据库类型。 例如，如果要恢复AEM表单备份，则无法将应用程序服务器从JBoss更改为WebLogic，或将数据库从Oracle更改为DB2。 此外，恢复的AEM表单必须使用相同的文件系统路径，如fonts目录。

### 恢复后重新启动 {#restarting-after-a-recovery}

在恢复后重新启动表单服务器之前，请执行以下操作：

1. 在维护模式下启动系统。
1. 执行以下操作以确保在维护模式下将表单管理器与AEM表单同步：

   1. 转到https://&lt;*服务器*>：&lt;*端口*>/lc/fm并使用administrator/password凭据登录。
   1. 单击右上角的用户（在此例中为“超级管理员”）名称。
   1. 单击 **管理员选项**.
   1. 单击 **开始** 从存储库同步资产。

1. 在群集环境中，主节点(对于AEM)应在辅助节点之前启动。
1. 确保在验证系统的正常操作之前，不会从内部或外部源（如Web、SOAP或EJB进程启动器）启动任何进程。

如果移动或更改了主AEM表单数据库，请查看与您的应用程序服务器相关的安装指南，以了解有关更新AEM表单数据源IDP_DS和EDC_DS的数据库连接信息的信息。

### 更改AEM表单主机名或IP地址 {#changing-the-aem-forms-hostname-or-ip-address}

在群集中，如果使用TCP缓存而不是UDP，则必须更新缓存定位器配置。 请参阅与应用程序服务器相关的配置指南中的“配置缓存定位器（仅使用TCP进行缓存）”。

### 更改AEM forms节点文件系统路径 {#changing-the-aem-forms-node-file-system-paths}

如果更改独立节点的文件系统路径，则必须更新首选项、其他系统配置、自定义应用程序和已部署的AEM表单应用程序中的相应引用。 另一方面，对于群集，所有节点必须使用相同的文件系统路径配置。 您必须设置全局文档存储(GDS)根目录，并确保它指向已恢复的GDS的副本，该副本与已恢复的数据库同步。 设置GDS路径很重要，因为GDS可以包含要在应用程序服务器重新启动后持续保留的数据。

在群集环境中，对于备份之前和恢复之后的所有群集节点，存储库的文件系统路径配置应该相同。

使用 `LCSetGDS`中的脚本 `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` 文件夹设置GDS路径。 请参阅 `ReadMe.txt` 文件来了解详细信息。 如果无法使用旧的GDS目录路径， `LCSetGDS` 在启动AEM表单之前，必须使用脚本来设置GDS的新路径。

>[!NOTE]
>
>只有在这种情况下，您才应使用此脚本来更改GDS位置。 要在AEM表单运行时更改GDS位置，请使用Administration Console。 (请参阅 [配置常规AEM表单设置](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.) *

设置GDS路径后，以维护模式启动Forms服务器，然后使用管理控制台更新新节点的剩余文件系统路径。 验证所有必需的配置均已更新后，请重新启动并测试AEM表单。
