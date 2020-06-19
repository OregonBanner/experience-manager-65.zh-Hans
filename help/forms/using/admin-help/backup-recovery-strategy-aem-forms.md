---
title: AEM表单的备份和恢复策略
seo-title: AEM表单的备份和恢复策略
description: 了解如何实施备份数据的战略并确保其与AEM表单数据保持同步。
seo-description: 了解如何实施备份数据的战略并确保其与AEM表单数据保持同步。
uuid: 98fc3115-76e5-4e58-aa30-3601866a441f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f192a8a3-1116-4d32-9b57-b53d532c0dbf
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 0%

---


# AEM表单的备份和恢复策略{#backup-and-recovery-strategy-for-aem-forms}

如果您的AEM表单实施将其他自定义数据存储在其他数据库中，则您负责实施备份此数据的策略，并确保其与AEM表单数据保持同步。 此外，应用程序必须设计得足够健壮，才能处理额外数据库不同步的情况。 强烈建议在事务的上下文中执行任何数据库操作，以帮助保持一致的状态。

在确定AEM表单的使用方式后，确定必须备份哪些文件、备份频率以及备份窗口。

>[!NOTE]
>
>与AEM表单实施的任何其他方面一样，您的备份和恢复策略必须在开发或分阶段环境中进行开发和测试，然后才能用于生产，以确保整个解决方案能按预期工作，而不会丢失数据。

Adobe Experience Manager(AEM)是AEM表单的一个组成部分。 因此，您需要备份AEM，并与AEM表单备份同步，因为Corresponce Management Solution和服务（如表单管理器）基于AEM表单的AEM部分中存储的数据。要防止数据丢失，必须以某种方式备份AEM表单特定数据，以确保GDS和AEM（存储库）与数据库引用关联。、GDS、AEM和内容存储根目录必须还原到与原始DNS名称相同的计算机。

## 备份类型 {#types-of-backups}

AEM表单备份策略涉及两种类型的备份：

**系统映像：** 一个完整的系统备份，当硬盘或整个计算机停止工作时，您可以使用它恢复计算机内容。 系统映像备份仅在AEM表单的生产部署之前是必需的。 然后，内部公司策略规定系统映像备份的需要频率。

**AEM表单特定数据：** 应用程序存储存在于数据库、全局文档(GDS)和AEM存储库中，必须实时备份。 GDS是一个目录，用于存储在进程中使用的长寿命文件。 这些文件可能包括PDF、策略或表单模板。

>[!NOTE]
>
>如果安装了Content Services(Deprecated)，则还要备份“内容存储”根目录。 请参 [阅内容存储根目录（仅限Content Services）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only)。

数据库用于存储表单对象、服务配置、进程状态和对GDS文件的数据库引用。 如果在文档库中启用存储，则GDS中的永久数据和文档也会存储在数据库中。 可以使用以下方法备份和恢复数据库：

* **快照备份** 模式表示AEM表单系统处于无限期备份模式或指定的分钟数内处于备份模式，此后备份模式不再启用。 要进入或离开快照备份模式，可使用以下选项之一。 恢复方案后，不应启用快照备份模式。

   * 使用管理控制台中的“备份设置”页。 要进入快照模式，请选中“在安全备份模式下操作”复选框。 取消选中此复选框可退出快照模式。
   * 使用LCBackupMode脚本(请 [参阅备份存储库、GDS和内容根目录](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories))。 要退出快照备份模式，请在脚本参数中，将参 `continuousCoverage` 数设置为 `false` 或使用 `leaveContinuousCoverage` 选项。
   * 使用提供的备份／恢复API。 <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **滚动备份** 模式表示系统始终处于备份模式，新备份模式会话在上一个会话发布后立即启动。 没有超时与滚动备份模式相关。 当调用LCBackupMode脚本或API以退出滚动备份模式时，将开始新的滚动备份模式会话。 此模式对于支持连续备份很有用，但仍允许从GDS目录中清除旧的和不需要的文档。 “备份和恢复”页不支持滚动备份模式。 恢复方案后，仍启用滚动备份模式。 您可以使用带有选项的LCBackupMode脚本离开连续备份模式(滚动备 `leaveContinuousCoverage` 份模式)。

>[!NOTE]
>
>离开滚动备份模式会立即开始新的备份模式会话。 要完全禁用滚动备份模式，请使 `leaveContinuousCoverage` 用脚本中的选项，该选项覆盖现有滚动备份会话。 在快照备份模式下，您可以像通常那样离开备份模式。

要防止数据丢失，AEM表单特定数据的备份方式必须确保GDS和内容存储根目录文档与数据库引用相关。

>[!NOTE]
>
>当GDS存储在文件系统而非数据库中时，请在GDS备份之前执行数据库备份。

## 备份和恢复的特殊注意事项 {#special-considerations-for-backup-and-recovery}

如果您由于以下更改而必须将AEM表单恢复到其他环境，请遵循以下准则：

* 更改AEM Forms服务器的IP地址、主机名或端口
* 驱动器号或目录路径的更改
* 更改为其他数据库主机、端口或名称

通常，此类恢复方案是由承载应用程序服务器、数据库服务器或表单服务器的服务器的硬件故障引起的。 除本节所述的AEM表单特定配置外，如果AEM表单服务器的主机名或IP地址发生更改，您还应对AEM表单部署的其他部分（如负载平衡和防火墙）进行必要的更改。

### 无法更改的内容 {#what-cannot-be-changed}

即使可以更改数据库服务器和许多其他参数，在从备份恢复AEM表单时，也无法更改应用程序服务器类型或数据库类型。 例如，如果要恢复AEM表单备份，则无法将应用程序服务器从JBoss更改为WebLogic，或将数据库从Oracle更改为DB2。 此外，恢复的AEM表单必须使用相同的文件系统路径，如字体目录。

### 恢复后重新启动 {#restarting-after-a-recovery}

在恢复后重新启动表单服务器之前，请执行以下操作：

1. 开始系统处于维护模式。
1. 执行以下操作，确保在维护模式下Form Manager与AEM Forms同步：

   1. 转到https://&lt;*server*>:&lt;*port*>/lc/fm，然后使用管理员／密码凭据登录。
   1. 单击右上角的用户名称（本例中为“超级管理员”）。
   1. 单击“ **管理选项**”。
   1. 单击 **开始** ，以同步存储库中的资产。

1. 在群集环境中，主节点（与AEM相关）应在辅助节点之前启动。
1. 确保在验证系统的正常操作之前，不会从内部或外部源（如Web、SOAP或EJB进程启动器）启动任何进程。

如果主AEM表单数据库被移动或更改，请查看与应用程序服务器相关的安装指南，以了解有关更新AEM表单数据源IDP_DS和EDC_DS的数据库连接信息。

### 更改AEM表单主机名或IP地址 {#changing-the-aem-forms-hostname-or-ip-address}

在群集中，如果使用TCP缓存而不是UDP，则必须更新缓存定位器配置。 请参阅与应用程序服务器相关的配置指南中的“配置缓存定位器（仅使用TCP进行缓存）”。

### 更改AEM表单节点文件系统路径 {#changing-the-aem-forms-node-file-system-paths}

如果更改独立节点的文件系统路径，则必须更新首选项、其他系统配置、自定义应用程序和已部署的AEM表单应用程序中的相应引用。 另一方面，对于群集，所有节点必须使用相同的文件系统路径配置。 必须设置全局文档存储(GDS)根目录，并确保它指向与恢复的数据库同步的已恢复GDS的副本。 设置GDS路径很重要，因为GDS可包含要在应用程序服务器重启期间保留的数据。

在群集环境中，备份前和恢复后，存储库的文件系统路径配置应与所有群集节点的配置相同。

在更 `LCSetGDS`改文件系 `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` 统路径后，使用文件夹中的脚本设置GDS路径。 有关详细 `ReadMe.txt` 信息，请参阅同一文件夹中的文件。 如果无法使用旧的GDS目录路 `LCSetGDS` 径，则在开始AEM表单之前，必须使用脚本将新路径设置为GDS。

>[!NOTE]
>
>这种情况是您唯一应使用此脚本更改GDS位置的情况。 要在AEM表单运行时更改GDS位置，请使用管理控制台。 (请参 [阅配置常规AEM表单](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)设置*。)*

设置GDS路径后，在维护模式下开始表单服务器，并使用管理控制台更新新节点的其余文件系统路径。 验证所有必要的配置都已更新后，请重新启动并测试AEM表单。
