---
title: 数据存储垃圾收集
seo-title: 数据存储垃圾收集
description: 了解如何配置数据存储垃圾收集以释放磁盘空间。
seo-description: 了解如何配置数据存储垃圾收集以释放磁盘空间。
uuid: 49488a81-986a-4d1a-96c8-aeb6595fc094
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5b1e46c5-7e56-433e-b62e-2a76ea7be0fd
docset: aem65
exl-id: 0dc4a8ce-5b0e-4bc9-a6f5-df2a67149e22
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---

# 数据存储垃圾收集 {#data-store-garbage-collection}

当删除常规WCM资产时，对基础数据存储记录的引用可以从节点层次结构中删除，但数据存储记录本身仍然保留。 此未引用的数据存储记录随后将变为“垃圾”，无需保留。 在存在大量垃圾资产的情况下，删除这些资产以保留空间并优化备份和文件系统维护性能是有益的。

在大多数情况下， WCM应用程序倾向于收集信息，但不会几乎频繁地删除信息。 虽然已添加新图像，甚至会取代旧版本，但版本控制系统仍保留旧图像，并且在需要时支持还原到旧图像。 因此，我们认为添加到系统中的大多数内容会被有效地永久存储。 那么，我们可能想要清理的存储库中典型的“垃圾”来源是什么？

AEM将存储库用作许多内部活动和内务活动的存储：

* 生成和下载的包
* 为发布复制创建的临时文件
* 工作流负载
* 在DAM渲染期间临时创建的资产

当这些临时对象中的任何一个足够大，需要在数据存储中存储，并且当对象最终被淘汰时，数据存储记录本身将保持为“垃圾”。 在典型的WCM创作/发布应用程序中，此类垃圾的最大来源通常是发布激活过程。 在将数据复制到发布时，如果首先以名为“Durbo”的有效数据格式收集到集合中，并存储在`/var/replication/data`下的存储库中，则数据会被复制到发布中。 数据包通常大于数据存储的临界大小阈值，因此最终存储为数据存储记录。 复制完成后，将删除`/var/replication/data`中的节点，但数据存储记录仍为“垃圾”。

可恢复垃圾的另一个来源是包。 与其他所有内容一样，包数据也存储在存储库中，因此存储在数据存储中的包大于4KB。 在开发项目过程中或在一段时间内维护系统时，可以多次构建和重建包，每个构建都会生成新的数据存储记录，同构先前构建的记录。

## 数据存储垃圾收集是如何工作的？{#how-does-data-store-garbage-collection-work}

如果已使用外部数据存储配置了存储库，则[数据存储垃圾收集将作为每周维护窗口的一部分自动运行](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection)。 系统管理员还可以根据需要手动[运行数据存储垃圾收集](#running-data-store-garbage-collection)。 通常，建议定期执行数据存储垃圾收集，但在规划数据存储垃圾收集时应考虑以下因素：

* 数据存储垃圾收集需要时间，并且可能会影响性能，因此应相应地对其进行规划。
* 删除数据存储垃圾记录不会影响正常性能，因此这不是性能优化。
* 如果存储利用率和相关因素（如备份时间）不是问题，则数据存储垃圾收集可能会安全地推迟。

数据存储垃圾收集器在进程开始时首先记录当前时间戳。 然后，使用多通标记/扫描模式算法进行收集。

在第一阶段，数据存储垃圾收集器对所有存储库内容执行全面遍历。 对于每个引用了数据存储记录的内容对象，它将文件放置在文件系统中，执行元数据更新 — 修改“上次修改时间”或MTIME属性。 此时，此阶段访问的文件将比初始基线时间戳更新。

在第二阶段，数据存储垃圾收集器以与“查找”大致相同的方式遍历数据存储的物理目录结构。 它检查了文件的“上次修改时间”或MTIME属性，并做出以下确定：

* 如果MTIME比初始基线时间戳新，则要么在第一阶段找到该文件，要么是在收集过程进行期间添加到存储库的全新文件。 其中任何一种情况均认为记录有效，档案不得删除。
* 如果MTIME在初始基线时间戳之前，则文件不是主动引用的文件，它被视为可移除垃圾。

此方法非常适用于具有专用数据存储的单个节点。 但是，数据存储可能是共享的，如果是，则表示不会检查对其他存储库中数据存储记录的潜在活动实时引用，并且活动引用的文件可能会被错误地删除。 在规划任何垃圾收集之前，系统管理员必须了解数据存储的共享性质，并且只有在知道数据存储未共享时才使用简单的内置数据存储垃圾收集过程。

>[!NOTE]
>
>在群集或共享数据存储设置（具有Mongo或Tar区段）中执行垃圾收集时，日志可能会显示有关无法删除某些Blob ID的警告。 之所以会出现这种情况，是因为之前垃圾收集中删除的Blob ID被没有ID删除信息的其他群集或共享节点再次错误地引用。 因此，在执行垃圾收集时，当垃圾收集尝试删除在上次运行中已删除的ID时，它会记录一则警告。 此行为不会影响性能或功能。

## 运行数据存储垃圾收集{#running-data-store-garbage-collection}

根据运行AEM的数据存储设置，有三种方法可运行数据存储垃圾收集：

1. 通过[修订清理](/help/sites-deploying/revision-cleanup.md) — 通常用于节点存储清理的垃圾收集机制。

1. 通过[数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard) — 操作功能板上提供的用于外部数据存储的垃圾收集机制。
1. 通过[JMX控制台](/help/sites-administering/jmx-console.md)。

如果TarMK同时用作节点存储和数据存储，则修订版清理可用于对节点存储和数据存储进行垃圾收集。 但是，如果配置了外部数据存储（如文件系统数据存储），则必须从修订版清理中单独显式触发数据存储垃圾收集。 可通过操作功能板或JMX控制台触发数据存储垃圾收集。

下表显示了数据存储垃圾收集类型，该类型需要用于AEM 6中所有受支持的数据存储部署：

<table>
 <tbody>
  <tr>
   <td><strong>节点存储</strong><br /> </td>
   <td><strong>数据存储</strong></td>
   <td><strong>垃圾收集机制</strong><br /> </td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>TarMK</td>
   <td>修订清理（二进制文件与区段存储内置）</td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>外部文件系统</td>
   <td><p>通过“操作”功能板收集数据存储垃圾任务</p> <p>JMX控制台</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>通过“操作”功能板收集数据存储垃圾任务</p> <p>JMX控制台</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>外部文件系统</td>
   <td><p>通过“操作”功能板收集数据存储垃圾任务</p> <p>JMX控制台</p> </td>
  </tr>
 </tbody>
</table>

### 通过操作功能板{#running-data-store-garbage-collection-via-the-operations-dashboard}运行数据存储垃圾收集

通过[操作功能板](/help/sites-administering/operations-dashboard.md)提供的内置每周维护窗口包含一个内置任务，可在星期日凌晨1点触发数据存储垃圾收集。

如果您需要在此时间以外运行数据存储垃圾收集，则可以通过操作功能板手动触发。

在运行数据存储垃圾收集之前，您应该检查当时是否没有运行备份。

1. 通过&#x200B;**Navigation** -> **Tools** -> **Operations** -> **Maintenance**&#x200B;打开操作功能板。
1. 单击或点按&#x200B;**每周维护窗口**。

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. 选择&#x200B;**数据存储垃圾收集**&#x200B;任务，然后单击或点按&#x200B;**运行**&#x200B;图标。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 数据存储垃圾收集运行，其状态显示在功能板中。

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>只有在您配置了外部文件数据存储后，才会显示“数据存储垃圾收集”任务。 有关如何设置文件数据存储的信息，请参阅[在AEM 6](/help/sites-deploying/data-store-config.md#file-data-store)中配置节点存储和数据存储。

### 通过JMX控制台{#running-data-store-garbage-collection-via-the-jmx-console}运行数据存储垃圾收集

本节介绍如何通过JMX控制台手动运行数据存储垃圾收集。 如果在没有外部数据存储的情况下设置了安装，则这不适用于您的安装。 请参阅[维护存储库](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)下有关如何运行修订清理的说明。

>[!NOTE]
>
>如果您使用外部数据存储运行TarMK，则需要先运行修订清理，以便垃圾收集有效。

要运行垃圾收集，请执行以下操作：

1. 在Apache Felix OSGi管理控制台中，突出显示&#x200B;**Main**&#x200B;选项卡，然后从以下菜单中选择&#x200B;**JMX**。
1. 接下来，搜索并单击&#x200B;**Repository Manager** MBean（或转到`https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`）。
1. 单击&#x200B;**startDataStoreGC(boolean markOnly)**。
1. 如果需要，为`markOnly`参数输入“`true`”：

   | **选项** | **描述** |
   |---|---|
   | 布尔标记Only | 将设置为true，以便在标记和扫描操作中仅标记参照而不扫描。 在多个不同存储库之间共享基础BlobStore时，将使用此模式。 对于所有其他情况，将其设置为false以执行完全垃圾收集。 |

1. 单击&#x200B;**调用**。 CRX运行垃圾收集并指示其完成时间。

>[!NOTE]
>
>数据存储垃圾收集将不会收集过去24小时内已删除的文件。

>[!NOTE]
>
>只有在配置了外部文件数据存储后，才会启动数据存储垃圾收集任务。 如果尚未配置外部文件数据存储，则任务将在调用后返回消息`Cannot perform operation: no service of type BlobGCMBean found`。 有关如何设置文件数据存储的信息，请参阅[在AEM 6](/help/sites-deploying/data-store-config.md#file-data-store)中配置节点存储和数据存储。

## 自动化数据存储垃圾收集{#automating-data-store-garbage-collection}

如果可能，应当在系统负载很小（例如在上午）时运行数据存储垃圾收集。

通过[操作功能板](/help/sites-administering/operations-dashboard.md)提供的内置每周维护窗口包含一个内置任务，可在星期日凌晨1点触发数据存储垃圾收集。 您还应检查当前是否没有运行备份。 维护窗口的开始时间可以根据需要通过仪表板进行自定义。

>[!NOTE]
>
>不同时运行它的原因是，这样旧（和未使用）的数据存储文件也会得到备份，因此如果需要回滚到旧修订版本，则二进制文件仍然在备份中。

如果您不想在“操作功能板”的每周维护窗口中运行数据存储垃圾收集，则还可以使用wget或curl HTTP客户端自动执行该操作。 以下是如何使用curl自动备份的示例：

>[!CAUTION]
>
>在以下示例中， `curl`命令可能需要为实例配置各种参数；例如，主机名(`localhost`)、端口(`4502`)、管理员密码(`xyz`)以及实际数据存储垃圾收集的各种参数。

以下是通过命令行调用数据存储垃圾收集的示例curl命令：

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

curl命令会立即返回。

## 检查数据存储一致性{#checking-data-store-consistency}

数据存储一致性检查将报告任何缺少但仍被引用的数据存储二进制文件。 要开始一致性检查，请执行以下步骤：

1. 转到JMX控制台。 有关如何使用JMX控制台的信息，请参阅[本文](/help/sites-administering/jmx-console.md#using-the-jmx-console)。
1. 搜索&#x200B;**BlobGarbageCollection** Mbean并单击它。
1. 单击`checkConsistency()`链接。

一致性检查完成后，将显示一条消息，其中报告为缺少的二进制文件数。 如果数字大于0，请检查`error.log`以了解有关缺少二进制文件的更多详细信息。

以下是如何在日志中报告缺少二进制文件的示例：

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```
