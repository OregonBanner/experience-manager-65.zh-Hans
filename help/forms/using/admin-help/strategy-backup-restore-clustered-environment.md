---
title: 群集环境中备份和恢复的策略
seo-title: 群集环境中备份和恢复的策略
description: 如果您的AEM表单实施将其他自定义数据存储在其他数据库中，则必须实施备份此数据的策略，以确保其与AEM表单数据保持同步。
seo-description: 如果您的AEM表单实施将其他自定义数据存储在其他数据库中，则必须实施备份此数据的策略，以确保其与AEM表单数据保持同步。
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 0%

---


# 群集环境中备份和恢复的策略 {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>如果您的AEM表单实施将其他自定义数据存储在其他数据库中，则必须实施备份此数据的策略，以确保其与AEM表单数据保持同步。 此外，应用程序必须设计得足够健壮，才能处理额外数据库不同步的情况。 强烈建议在事务的上下文中执行任何数据库操作，以帮助保持一致的状态。

您需要备份AEM表单系统的以下部分，才能从任何错误中恢复：

* AEM表单使用的数据库
* 长期存在数据和其他永久文档的GDS
* AEM数据库(crx-repository)

>[!NOTE]
>
>您需要备份AEM表单安装程序正在使用的任何其他数据，如客户字体、连接器数据等。

## 备份群集环境 {#back-up-a-clustered-environment}

本主题讨论备份任何AEM表单群集环境的以下策略：

* 离线备份（停机）
* 无停机的脱机备份（备用节点已关闭）
* 在线备份，不停机但响应延迟
* 备份Bootstrap属性文件

### 离线备份（停机） {#offline-backup-with-downtime}

1. 关闭整个群集和相关服务。 (请参 [阅启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何节点上备份数据库、GDS和连接器。 (请参 [阅要备份和恢复的文件](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 执行以下步骤以脱机备份AEM存储库：

   1. 对于每个群集节点，备份包含群集节点id的文件。
   1. 备份任何辅助群集节点（包括子目录）的所有文件。
   1. 单独备份每个群集节点的存储库／系统ID。
   有关详细步骤，请参 [阅备份和还原](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)。

1. 备份任何其他数据，如客户字体。
1. 再次开始群集。

### 无停机的脱机备份 {#offline-backup-with-no-downtime}

1. 进入滚动备份模式。 (请参 [阅进入备份模式](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   请注意，在恢复后，我们需要离开滚动备份模式。

1. 关闭群集中与AEM相关的任何辅助节点。 (请参 [阅启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何节点上备份数据库、GDS和连接器。 (请参 [阅要备份和恢复的文件](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 执行以下步骤以脱机备份AEM存储库：

   1. 对于每个群集节点，备份包含群集节点id的文件。
   1. 备份任何辅助群集节点（包括子目录）的所有文件。
   1. 单独备份每个群集节点的repository/system.id。
   有关详细步骤，请参 [阅备份和还原](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)。

1. 备份任何其他数据，如客户字体。
1. 再次开始群集。

### 在线备份，不停机但响应延迟 {#online-backup-with-no-downtime-but-delay-in-response}

1. 进入滚动备份模式。 (请参 [阅进入备份模式](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   请注意，在恢复后，您需要离开滚动备份模式。

1. 关闭群集中与AEM相关的任何辅助节点。 (请参 [阅启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何节点上备份数据库、GDS和连接器。 (请参 [阅要备份和恢复的文件](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 执行以下步骤联机备份AEM存储库：

   1. 对于每个群集节点，备份包含cluster_node.id的文件。
   1. 单独备份每个群集节点的repository/system.id。
   1. 在任何辅助节点上对存储库执行联机备份，以了解详细步骤，请参阅联机备份。

1. 备份任何其他数据，如客户字体。
1. 再次开始群集。

### 备份Bootstrap属性文件 {#back-up-the-bootstrap-properties-file}

创建AEM群集时，将在应用程序服务器中为所有辅助节点创建一个属性文件。 建议备份Bootstrap属性文件。 您可以在应用程序服务器上的以下位置找到该文件：

* JBoss: 在BIN目录中
* WebLogic: 在域目录中
* WebSphere: 用户档案目录

您需要备份AEM辅助节点的灾难恢复方案的文件，并在应用程序服务器上的指定位置将其替换（如果已恢复）。

## 群集环境中的恢复 {#recovery-in-a-clustered-environment}

如果整个群集或单个节点出现任何故障，您需要使用备份恢复它。

对于单节点恢复，您只需关闭单个节点并运行单节点恢复过程。

如果整个群集因数据库崩溃等故障而失败，您需要执行以下步骤。 恢复取决于使用的备份方法。

### 恢复单个节点 {#restoring-a-single-node}

1. 停止损坏的节点。

   >[!NOTE]
   >
   >如果损坏的节点是AEM主节点，请关闭整个群集节点。

1. 从系统映像重新创建物理系统。
1. 将修补程序或更新应用于自创建图像后应用的AEM表单。 在备份过程中记录了此信息。 必须将AEM表单恢复到与备份系统时相同的修补程序级别。
1. (*可选*)如果所有其他节点都正常工作，则AEM存储库也可能已损坏。 在这种情况下，AEM存储库的error.log文件中将显示一个存储库不同步消息。

   要恢复存储库，请执行以下步骤。

   >[!NOTE]
   >
   >如果压缩的crx-repository备份联机，请将其解压缩到任意位置，然后执行脱机还原过程。

   1. 删除节点的clusterNode目录中的存储库、共享的、版本和工作区目录。
   1. 将群集节点（包括子目录）的备份还原到该节点。
   1. 在节点上删除文件clusterNode/revision.log。
   1. 删除节点上的。lock（如果存在）。
   1. 删除节点上的repository/system.id（如果存在）。
   1. 删除节点上的文件&amp;ast;&amp;ast;/listener.properties（如果存在）。
   1. 恢复单个群集节点的repository/cluster_node.id。

>[!NOTE]
>
>请考虑以下几点：

* 如果失败的节点是AEM主节点，则将辅助存储库文件夹（crx-repository\crx.0000，其中0000可以是任何数字）中的所有内容复制到crx-repository\存储库文件夹，并删除辅助存储库文件夹。
* 在重新启动任何群集节点之前，请确保从主节点删除存储库/clustered.txt。
* 确保主节点是先启动的，一旦它完全启动，就开始其他节点。

### 恢复整个群集 {#restoring-the-entire-cluster}

1. 停止所有群集节点。
1. 从系统映像重新创建物理系统。
1. 将修补程序或更新应用到自创建图像起应用的AEM表单AEM表单。 此信息记录在备份过程的步骤1中。 必须将AEM表单恢复到与备份系统时相同的修补程序级别。
1. 恢复数据库、GDS和连接器。
1. 执行以下操作以脱机恢复AEM存储库：

   >[!NOTE]
   >
   >如果压缩的crx-repository备份联机，请将其解压缩到任意位置，然后执行脱机还原过程。

   1. 在所有群集节点上，删除clusterNode目录中的存储库、共享的、版本和工作区目录。
   1. 删除共享目录中的所有文件和目录。
   1. 将群集节点（包括子目录）的备份还原到一个群集节点。
   1. 将还原的群集节点的所有文件复制到所有其他群集节点。 完成后，每个群集节点都包含相同的数据。
   1. 在所有群集节点上删除文件clusterNode/revision.log。
   1. 删除所有群集节点上的。lock（如果存在）。
   1. 删除repository/system.id所有群集节点（如果存在）。
   1. 删除所有群集节点上的文件&amp;ast;&amp;ast;/listener.properties（如果存在）。
   1. 恢复单个群集节点的repository/cluster_node.id。

>[!NOTE]
>
>请考虑以下几点：

* 如果失败的节点是AEM主节点，则将从辅助存储库文件夹（它类似于crx-repository\crx.0000，其中000可以是任何数字）中的所有内容复制到crx-repository\存储库文件夹。
* 在重新启动任何群集节点之前，请确保从主节点删除存储库/clustered.txt。
* 确保主节点是先启动的，一旦它完全启动，就开始其他节点。

## 备份和恢复通信管理解决方案发布节点 {#back-up-and-restore-correspondence-management-solution-publish-node}

发布者节点在群集环境中没有任何主次关系。 您可以通过执行备份和还原来备份任 [何发布者节点](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)。

### 恢复单个发布者节点 {#recover-a-single-publisher-node}

1. 关闭需要恢复的节点，直到该节点再次启动，才执行任何发布活动。
1. 使用恢复备份 [(https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring恢复备]份)恢复发布节点。

### 恢复群集 {#recover-a-cluster}

1. 关闭群集。
1. 使用恢复备份 [(https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring恢复备]份)恢复发布节点。
1. 开始主节点，后跟作者群集的辅助节点。

