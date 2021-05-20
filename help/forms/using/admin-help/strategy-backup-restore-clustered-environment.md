---
title: 在群集环境中备份和恢复的策略
seo-title: 在群集环境中备份和恢复的策略
description: 如果您的AEM表单实施将其他自定义数据存储在不同的数据库中，则必须实施策略来备份此数据，以确保其与AEM表单数据保持同步。
seo-description: 如果您的AEM表单实施将其他自定义数据存储在不同的数据库中，则必须实施策略来备份此数据，以确保其与AEM表单数据保持同步。
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
exl-id: 98c96349-f253-475f-b646-352269814a38
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 0%

---

# 群集环境{#strategy-for-backup-and-restore-in-a-clustered-environment}中的备份和恢复策略

>[!NOTE]
>
>如果您的AEM表单实施将其他自定义数据存储在不同的数据库中，则必须实施策略来备份此数据，以确保其与AEM表单数据保持同步。 此外，必须设计应用程序，使其足够强大，能够处理附加数据库不同步的情况。 强烈建议在事务上下文中执行任何数据库操作以帮助保持一致状态。

您需要备份AEM表单系统的以下部分，以便从任何错误中恢复：

* AEM表单使用的数据库
* 具有长期数据和其他永久文档的GDS
* AEM数据库(crx-repository)

>[!NOTE]
>
>您需要备份您的AEM表单设置所使用的任何其他数据，例如客户字体、连接器数据等。

## 备份群集环境{#back-up-a-clustered-environment}

本主题讨论了备份任何AEM表单群集环境的以下策略：

* 离线备份（停机时间）
* 无停机的脱机备份（关闭的辅助节点备份）
* 在线备份，无停机但响应延迟
* 备份Bootstrap属性文件

### 离线备份，停机时间{#offline-backup-with-downtime}

1. 关闭整个群集和相关服务。 （请参阅[启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)）
1. 在任何节点上备份数据库、 GDS和连接器。 （请参阅[要备份和恢复的文件](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)）
1. 执行以下步骤以脱机备份AEM存储库：

   1. 对于每个群集节点，备份包含群集节点ID的文件。
   1. 备份任何辅助群集节点（包括子目录）的所有文件。
   1. 分别备份每个群集节点的存储库/系统ID。

   有关详细步骤，请参阅[备份和还原](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)。

1. 备份任何其他数据，例如客户字体。
1. 再次启动群集。

### 无停机的离线备份{#offline-backup-with-no-downtime}

1. 进入滚动备份模式。 （请参阅[进入备份模式](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes)）

   请注意，在恢复后，我们需要离开滚动备份模式。

1. 关闭群集中与AEM相关的任何辅助节点。 （请参阅[启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)）
1. 在任何节点上备份数据库、 GDS和连接器。 （请参阅[要备份和恢复的文件](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)）
1. 执行以下步骤以脱机备份AEM存储库：

   1. 对于每个群集节点，备份包含群集节点ID的文件。
   1. 备份任何辅助群集节点（包括子目录）的所有文件。
   1. 分别备份每个群集节点的repository/system.id 。

   有关详细步骤，请参阅[备份和还原](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)。

1. 备份任何其他数据，例如客户字体。
1. 再次启动群集。

### 联机备份，无停机但响应延迟{#online-backup-with-no-downtime-but-delay-in-response}

1. 进入滚动备份模式。 （请参阅[进入备份模式](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes)）

   请注意，恢复后，您需要离开滚动备份模式。

1. 关闭群集中与AEM相关的任何辅助节点。 （请参阅[启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)）
1. 在任何节点上备份数据库、 GDS和连接器。 （请参阅[要备份和恢复的文件](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)）
1. 执行以下步骤以联机备份AEM存储库：

   1. 对于每个群集节点，备份包含cluster_node.id的文件。
   1. 分别备份每个群集节点的repository/system.id 。
   1. 在任何辅助节点上，对存储库进行联机备份以了解详细步骤，请参阅联机备份。

1. 备份任何其他数据，例如客户字体。
1. 再次启动群集。

### 备份Bootstrap属性文件{#back-up-the-bootstrap-properties-file}

创建AEM群集时，将在应用程序服务器中为所有辅助节点创建一个属性文件。 建议备份Bootstrap属性文件。 您可以在应用程序服务器上的以下位置找到该文件：

* JBoss:在BIN目录中
* WebLogic:在域目录中
* WebSphere:在配置文件目录中

您需要备份文件以备AEM次节点的灾难恢复方案，并在应用程序服务器上的指定位置（如果已恢复）替换该文件。

## 在群集环境{#recovery-in-a-clustered-environment}中恢复

如果整个群集或单个节点出现任何故障，您需要使用备份还原它。

对于单节点恢复，只需关闭单节点并运行单节点恢复过程。

如果整个群集因数据库崩溃等故障而失败，您需要执行以下步骤。 恢复取决于使用的备份方法。

### 恢复单个节点{#restoring-a-single-node}

1. 停止损坏的节点。

   >[!NOTE]
   >
   >如果损坏的节点是AEM主节点，请关闭整个群集节点。

1. 从系统映像重新创建物理系统。
1. 将补丁或更新应用于自创建图像以来应用的AEM表单。 在备份过程中记录了此信息。 AEM表单必须恢复到与备份系统时相同的修补程序级别。
1. （*可选*）如果所有其他节点都运行正常，则AEM存储库也可能已损坏。 在这种情况下，您会在AEM存储库的error.log文件中看到一条存储库不同步消息。

   要恢复存储库，请执行以下步骤。

   >[!NOTE]
   >
   >如果压缩的crx-repository备份已联机，请在任意位置解压缩该备份，然后按照脱机还原过程进行操作。

   1. 删除节点clusterNode目录中的存储库、共享、版本和工作区目录。
   1. 将群集节点（包括子目录）的备份还原到该节点。
   1. 删除节点上的文件clusterNode/revision.log 。
   1. 删除节点上的.lock（如果存在）。
   1. 删除节点上的repository/system.id（如果存在）。
   1. 删除节点上的文件&amp;ast;&amp;ast;/listener.properties（如果存在）。
   1. 恢复单个群集节点的repository/cluster_node.id 。

>[!NOTE]
>
>请考虑以下几点：

* 如果失败的节点是AEM主节点，请将辅助存储库文件夹（crx-repository\crx.0000，其中000可以是任何位数）中的所有内容复制到crx-repository\存储库文件夹，并删除辅助存储库文件夹。
* 在重新启动任何群集节点之前，请确保从主节点删除存储库/clustered.txt 。
* 确保主节点首先启动，一旦完全启动，就启动其他节点。

### 恢复整个群集{#restoring-the-entire-cluster}

1. 停止所有群集节点。
1. 从系统映像重新创建物理系统。
1. 将补丁或更新应用到自创建图像以来应用的AEM表单AEM表单。 此信息记录在备份过程的第1步中。 AEM表单必须恢复到与备份系统时相同的修补程序级别。
1. 恢复数据库、GDS和连接器。
1. 执行以下操作以脱机恢复AEM存储库：

   >[!NOTE]
   >
   >如果压缩的crx-repository备份已联机，请在任意位置解压缩该备份，然后按照脱机还原过程进行操作。

   1. 在所有群集节点上，删除clusterNode目录中的存储库、共享、版本和工作区目录。
   1. 删除共享目录中的所有文件和目录。
   1. 将群集节点（包括子目录）的备份还原到一个群集节点。
   1. 将还原的群集节点的所有文件复制到所有其他群集节点。 完成后，每个群集节点都包含相同的数据。
   1. 删除所有群集节点上的文件clusterNode/revision.log 。
   1. 删除所有群集节点上的.lock（如果存在）。
   1. 删除repository/system.id所有群集节点（如果存在）。
   1. 删除所有群集节点上的文件&amp;ast;&amp;ast;/listener.properties（如果存在）。
   1. 恢复单个群集节点的repository/cluster_node.id 。

>[!NOTE]
>
>请考虑以下几点：

* 如果失败的节点是AEM主节点，请将辅助存储库文件夹（类似于crx-repository\crx.0000，其中000可以是任意位数）中的所有内容复制到crx-repository\存储库文件夹。
* 在重新启动任何群集节点之前，请确保从主节点删除存储库/clustered.txt 。
* 确保主节点首先启动，一旦完全启动，就启动其他节点。

## 备份和恢复通信管理解决方案发布节点{#back-up-and-restore-correspondence-management-solution-publish-node}

发布者节点在群集环境中没有任何主次关系。 您可以按照[Backup and Restore](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)执行任何Publisher节点的备份。

### 恢复单个发布者节点{#recover-a-single-publisher-node}

1. 关闭需要恢复的节点，在该节点再次启动之前，不执行任何发布活动。
1. 使用[恢复备份](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring)恢复发布节点。

### 恢复群集{#recover-a-cluster}

1. 关闭群集。
1. 使用[恢复备份](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring)恢复发布节点。
1. 启动主节点，然后启动创作群集的次节点。
