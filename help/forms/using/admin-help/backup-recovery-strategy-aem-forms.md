---
title: AEM表单的备份和恢复策略
seo-title: AEM表单的备份和恢复策略
description: 了解如何实施策略来备份数据，并确保其与AEM表单数据保持同步。
seo-description: 了解如何实施策略来备份数据，并确保其与AEM表单数据保持同步。
uuid: 98fc3115-76e5-4e58-aa30-3601866a441f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f192a8a3-1116-4d32-9b57-b53d532c0dbf
exl-id: 01ec6ebc-6d80-4417-9604-c8571aebb57e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 0%

---

# AEM表单的备份和恢复策略{#backup-and-recovery-strategy-for-aem-forms}

如果您的AEM表单实施将其他自定义数据存储在不同的数据库中，则您有责任实施策略来备份此数据，并确保其与AEM表单数据保持同步。 此外，必须设计应用程序，使其足够强大，能够处理附加数据库不同步的情况。 强烈建议在事务上下文中执行任何数据库操作以帮助保持一致状态。

在确定AEM表单的使用方式后，确定必须备份哪些文件、备份频率以及备份窗口才能使用。

>[!NOTE]
>
>与AEM表单实施的任何其他方面一样，您的备份和恢复策略必须在开发或暂存环境中开发和测试，然后才能在生产环境中使用，以确保整个解决方案能够按预期运行，而不会丢失数据。

Adobe Experience Manager(AEM)是AEM表单的一个组成部分。 因此，您需要备份AEM以及与AEM Forms备份同步，因为通信管理解决方案和服务（如表单管理器）基于AEM Forms中存储的数据。为防止任何数据丢失，必须备份AEM Forms特定数据，以确保GDS和AEM（存储库）与数据库引用相关联。数据库、GDS、AEM和内容存储根目录必须还原到与原始DNS名称相同的计算机。

## 备份类型{#types-of-backups}

AEM表单备份策略涉及两种类型的备份：

**系统映像：** 一个完整的系统备份，当您的硬盘或整个计算机停止工作时，您可以使用该备份还原计算机的内容。只有在生产部署AEM表单之前，才需要进行系统映像备份。 然后，内部公司策略规定需要系统映像备份的频率。

**AEM表单特定数据：** 应用程序数据存在于数据库、全局文档存储(GDS)和AEM存储库中，并且必须实时备份。GDS是一个目录，用于存储在进程中使用的长生命周期文件。 这些文件可能包含PDF、策略或表单模板。

>[!NOTE]
>
>如果安装了Content Services（已弃用），则还应备份Content Storage Root目录。 请参阅[内容存储根目录（仅限内容服务）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only)。

数据库用于存储对GDS文件的表单对象、服务配置、进程状态和数据库引用。 如果在数据库中启用了文档存储，则GDS中的永久数据和文档也会存储在数据库中。 可以使用以下方法备份和恢复数据库：

* **快照** 备份模式表示AEM表单系统处于备份模式时是无限期的，或处于指定的分钟数，在此之后，将不再启用备份模式。要进入或离开快照备份模式，您可以使用以下选项之一。 恢复方案之后，不应启用快照备份模式。

   * 使用管理控制台中的“备份设置”页。 要进入快照模式，请选中在安全备份模式下操作复选框。 取消选中此复选框可退出快照模式。
   * 使用LCBackupMode脚本（请参阅[备份数据库、GDS和内容存储根目录](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)）。 要退出快照备份模式，请在脚本参数中，将`continuousCoverage`参数设置为`false`或使用`leaveContinuousCoverage`选项。
   * 使用提供的备份/恢复API。 <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **滚动** 备份模式表示系统始终处于备份模式，新备份模式会话在上一个会话发布后立即启动。没有超时与滚动备份模式相关联。 当调用LCBackupMode脚本或API以退出滚动备份模式时，将开始新的滚动备份模式会话。 此模式对于支持连续备份非常有用，但仍然允许从GDS目录中清除旧的和不需要的文档。 “备份和恢复”页不支持滚动备份模式。 恢复方案后，仍启用滚动备份模式。 使用带有`leaveContinuousCoverage`选项的LCBackupMode脚本可以离开连续备份模式（滚动备份模式）。

>[!NOTE]
>
>离开滚动备份模式会立即开始新的备份模式会话。 要完全禁用滚动备份模式，请使用脚本中的`leaveContinuousCoverage`选项，该选项将覆盖现有滚动备份会话。 在快照备份模式下，您可能会像往常一样离开备份模式。

为防止数据丢失，AEM表单特定数据的备份方式必须确保GDS和内容存储根目录文档与数据库引用相关联。

>[!NOTE]
>
>当GDS存储在文件系统上而不是数据库中时，在GDS备份之前执行数据库备份。

## 备份和恢复的特殊注意事项{#special-considerations-for-backup-and-recovery}

如果由于以下更改而必须将AEM表单恢复到其他环境，请遵循以下准则：

* 更改AEM Forms服务器的IP地址、主机名或端口
* 驱动器盘符或目录路径的更改
* 更改为其他数据库主机、端口或名称

通常，此类恢复方案是由承载应用程序服务器、数据库服务器或表单服务器的服务器的硬件故障引起的。 除了本节中所述的AEM表单特定配置之外，如果AEM Forms服务器的主机名或IP地址发生更改，您还应当对AEM表单部署的其他部分（如负载平衡器和防火墙）进行必要的更改。

### 不能更改的内容{#what-cannot-be-changed}

即使可以更改数据库服务器和许多其他参数，从备份中恢复AEM表单时，仍不能更改应用程序服务器类型或数据库类型。 例如，如果您正在恢复AEM表单备份，则无法将应用程序服务器从JBoss更改为WebLogic或数据库，从Oracle更改为DB2。 此外，恢复的AEM表单必须使用相同的文件系统路径，如字体目录。

### 恢复后重新启动{#restarting-after-a-recovery}

在恢复后重新启动表单服务器之前，请执行以下操作：

1. 在维护模式下启动系统。
1. 请执行以下操作，以确保在维护模式下将表单管理器与AEM表单同步：

   1. 转到https://*server*>:*port*>/lc/fm ，然后使用管理员/密码凭据登录。
   1. 单击右上角的用户名称（在本例中为“超级管理员”）。
   1. 单击&#x200B;**管理选项**。
   1. 单击&#x200B;**开始**&#x200B;以同步存储库中的资产。

1. 在群集环境中，主节点(相对于AEM)应位于次节点之前。
1. 确保在验证系统的正常操作之前，不会从内部或外部源（如Web、SOAP或EJB进程启动器）启动任何进程。

如果移动或更改了主AEM表单数据库，请查看与您的应用程序服务器相关的安装指南，以了解有关更新AEM表单数据源IDP_DS和EDC_DS的数据库连接信息的信息。

### 更改AEM表单主机名或IP地址{#changing-the-aem-forms-hostname-or-ip-address}

在群集中，如果使用TCP缓存而不是UDP ，则必须更新缓存定位器配置。 请参阅与应用程序服务器相关的配置指南中的“配置缓存定位器（仅使用TCP进行缓存）”。

### 更改AEM表单节点文件系统路径{#changing-the-aem-forms-node-file-system-paths}

如果更改独立节点的文件系统路径，则必须更新首选项、其他系统配置、自定义应用程序和已部署的AEM表单应用程序中的相应引用。 另一方面，对于群集，所有节点必须使用相同的文件系统路径配置。 必须设置全局文档存储(GDS)根目录，并确保它指向恢复的GDS的副本，该副本与恢复的数据库同步。 设置GDS路径很重要，因为GDS可以包含打算在应用程序服务器重新启动期间保留的数据。

在群集环境中，在备份之前和恢复之后，存储库的文件系统路径配置应与所有群集节点相同。

在更改文件系统路径后，使用`[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline`文件夹中的`LCSetGDS`脚本设置GDS路径。 有关详细信息，请参阅同一文件夹中的`ReadMe.txt`文件。 如果无法使用旧的GDS目录路径，则在启动AEM表单之前，必须使用`LCSetGDS`脚本来设置GDS的新路径。

>[!NOTE]
>
>这种情况是您唯一应使用此脚本更改GDS位置的情况。 要在AEM表单运行时更改GDS位置，请使用管理控制台。 (请参阅[配置常规AEM表单设置](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*。)*

在设置GDS路径后，在维护模式下启动Forms服务器，然后使用管理控制台为新节点更新剩余的文件系统路径。 验证所有必要的配置均已更新后，请重新启动并测试AEM表单。
