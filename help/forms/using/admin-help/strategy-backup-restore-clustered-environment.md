---
title: 群集环境中的备份和恢复策略
description: 如果AEM表单实施将其他自定义数据存储在其他数据库中，则必须实施策略来备份此数据，确保它与AEM表单数据保持同步。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 98c96349-f253-475f-b646-352269814a38
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1396'
ht-degree: 0%

---

# 群集环境中的备份和恢复策略 {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>如果AEM表单实施将其他自定义数据存储在其他数据库中，则必须实施策略来备份此数据，确保它与AEM表单数据保持同步。 此外，应用程序必须设计得足够强健，能够处理其他数据库不同步的情况。 强烈建议在事务上下文中执行任何数据库操作，以帮助保持一致状态。

您需要备份AEM表单系统的以下部分，以便从任何错误中恢复：

* AEM表单使用的数据库
* 具有长期数据和其他持久性文档的GDS
* AEM数据库(crx-repository)

>[!NOTE]
>
>您需要备份AEM表单设置正在使用的任何其他数据，例如客户字体、连接器数据等。

## 备份群集环境 {#back-up-a-clustered-environment}

本主题讨论备份任何AEM表单群集环境的以下策略：

* 离线备份与停机时间
* 不停机进行脱机备份（备份已关闭的辅助节点）
* 在线备份，无停机时间但响应延迟
* 备份Bootstrap属性文件

### 离线备份与停机时间 {#offline-backup-with-downtime}

1. 关闭整个群集和相关服务。 (请参阅 [启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何节点上，备份数据库、 GDS和连接器。 (请参阅 [要备份和恢复的文件](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 要脱机备份AEM存储库，请执行以下步骤：

   1. 对于每个群集节点，备份包含群集节点ID的文件。
   1. 备份任何辅助群集节点的所有文件，包括子目录。
   1. 分别备份每个群集节点的存储库/系统ID。

   有关详细步骤，请参阅 [备份和恢复](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. 备份任何其他数据，如客户字体。
1. 再次启动群集。

### 离线备份，无需停机 {#offline-backup-with-no-downtime}

1. 进入滚动备份模式。 (请参阅 [进入备份模式](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   恢复后退出滚动备份模式。

1. 关闭与AEM有关的群集的任何辅助节点。 (请参阅 [启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何节点上，备份数据库、 GDS和连接器。 (请参阅 [要备份和恢复的文件](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 要脱机备份AEM存储库，请执行以下步骤：

   1. 对于每个群集节点，备份包含群集节点ID的文件。
   1. 备份任何辅助群集节点的所有文件，包括子目录。
   1. 分别备份每个群集节点的repository/system.id。

   有关详细步骤，请参阅 [备份和恢复](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. 备份任何其他数据，如客户字体。
1. 再次启动群集。

### 在线备份，无停机时间但响应延迟 {#online-backup-with-no-downtime-but-delay-in-response}

1. 进入滚动备份模式。 (请参阅 [进入备份模式](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   恢复后退出滚动备份模式。

1. 关闭与AEM有关的群集的任何辅助节点。 (请参阅 [启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何节点上，备份数据库、 GDS和连接器。 (请参阅 [要备份和恢复的文件](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 要联机备份AEM存储库，请执行以下步骤：

   1. 对于每个群集节点，备份包含cluster_node.id的文件。
   1. 分别备份每个群集节点的repository/system.id。
   1. 在任何辅助节点上，对存储库进行联机备份，以了解详细步骤，请参阅联机备份。

1. 备份任何其他数据，如客户字体。
1. 再次启动群集。

### 备份Bootstrap属性文件 {#back-up-the-bootstrap-properties-file}

创建AEM群集时，会在应用程序服务器中为所有辅助节点创建一个属性文件。 建议备份Bootstrap属性文件。 您可以在应用程序服务器上的以下位置找到文件：

* JBoss®：在BIN目录中
* WebLogic：在域目录中
* WebSphere®：在配置文件目录中

备份AEM辅助节点灾难恢复方案的文件，并在应用程序服务器上的指定位置替换该文件（如果恢复）。

## 在群集环境中恢复 {#recovery-in-a-clustered-environment}

如果整个群集或单个节点出现任何故障，请使用备份恢复它。

对于单节点恢复，请关闭单节点并运行单节点恢复过程。

如果整个群集由于数据库崩溃等故障而失败，请执行以下步骤。 恢复取决于使用的备份方法。

### 恢复单个节点 {#restoring-a-single-node}

1. 停止损坏的节点。

   >[!NOTE]
   >
   >如果损坏的节点是AEM主节点，请关闭整个群集节点。

1. 从系统映像重新创建物理系统。
1. 将自映像生成以来应用的修补程序或更新应用到AEM表单。 此信息是在备份过程中记录的。 必须将AEM表单恢复到与备份系统时相同的修补程序级别。
1. (*可选*)如果所有其他节点均可正常运行，则AEM存储库也可能会损坏。 在这种情况下，您将在AEM存储库的error.log文件中看到一条存储库取消同步消息。

   要恢复存储库，请执行以下步骤。

   >[!NOTE]
   >
   >如果压缩的crx-repository备份已联机，请在任何位置解压缩该备份，然后执行脱机还原过程。

   1. 删除节点的clusterNode目录中的存储库、共享、版本和工作区目录。
   1. 将群集节点（包括子目录）的备份还原到该节点。
   1. 删除节点上的文件clusterNode/revision.log 。
   1. 删除节点上的.lock （如果存在）。
   1. 删除节点上的repository/system.id （如果存在）。
   1. 删除节点上的文件&amp;ast；&amp;ast；/listener.properties （如果存在）。
   1. 恢复单个群集节点的repository/cluster_node.id 。

>[!NOTE]
>
>请考虑以下几点：

* 如果失败的节点是AEM主节点，请将辅助存储库文件夹（crx-repository\crx.0000，其中0000可以是任意数字）中的所有内容复制到crx-repository\存储库文件夹，并删除辅助存储库文件夹。
* 在重新启动任何群集节点之前，请确保从主节点中删除存储库/clustered.txt 。
* 确保先启动主节点，然后在启动后启动其他节点。

### 恢复整个群集 {#restoring-the-entire-cluster}

1. 停止所有群集节点。
1. 从系统映像重新创建物理系统。
1. 对自映像生成以来应用的AEM formsAEM表单应用补丁或更新。 此信息记录在备份过程的步骤1中。 必须将AEM表单恢复到与备份系统时相同的修补程序级别。
1. 恢复数据库、GDS和连接器。
1. 执行以下操作以离线恢复AEM存储库：

   >[!NOTE]
   >
   >如果压缩的crx-repository备份已联机，请在任何位置解压缩该备份，然后执行脱机还原过程。

   1. 在所有群集节点上，删除clusterNode目录中的存储库、共享、版本和工作区目录。
   1. 删除共享目录中的所有文件和目录。
   1. 将群集节点（包括子目录）的备份还原到一个群集节点。
   1. 将已还原群集节点的所有文件复制到所有其他群集节点。 完成后，每个群集节点包含相同的数据。
   1. 删除所有群集节点上的文件clusterNode/revision.log 。
   1. 删除所有群集节点上的.lock （如果存在）。
   1. 删除repository/system.id所有群集节点（如果存在）。
   1. 删除所有群集节点上的文件&amp;ast；&amp;ast；/listener.properties （如果存在）。
   1. 恢复单个群集节点的repository/cluster_node.id 。

>[!NOTE]
>
>请考虑以下几点：

* 如果失败的节点是AEM主节点，请将辅助存储库文件夹中的所有内容（类似于crx-repository\crx.0000，其中0000可以是任意数字）复制到crx-repository\存储库文件夹。
* 在重新启动任何群集节点之前，请确保从主节点中删除存储库/clustered.txt 。
* 确保先启动主节点，然后在启动后启动其他节点。

## 备份和恢复Correspondence Management Solution发布节点 {#back-up-and-restore-correspondence-management-solution-publish-node}

发布服务器节点在群集环境中没有任何主 — 辅关系。 您可以通过以下方式备份任何发布者节点 [备份和恢复](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### 恢复单个发布者节点 {#recover-a-single-publisher-node}

1. 关闭必须恢复的节点，并在节点再次启动之前不执行任何发布活动。
1. 使用以下方式还原发布节点 [恢复备份](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### 恢复群集 {#recover-a-cluster}

1. 关闭群集。
1. 使用以下方式还原发布节点 [恢复备份](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).
1. 启动主节点，然后启动创作群集的辅助节点。
