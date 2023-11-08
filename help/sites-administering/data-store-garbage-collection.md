---
title: 数据存储垃圾收集
seo-title: Data Store Garbage Collection
description: 了解如何配置数据存储垃圾收藏集以释放磁盘空间。
seo-description: Learn how to configure Data Store Garbage Collection to free up disk space.
uuid: 49488a81-986a-4d1a-96c8-aeb6595fc094
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5b1e46c5-7e56-433e-b62e-2a76ea7be0fd
docset: aem65
exl-id: 0dc4a8ce-5b0e-4bc9-a6f5-df2a67149e22
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---

# 数据存储垃圾收集 {#data-store-garbage-collection}

当常规WCM资产被移除时，对基础数据存储记录的引用可以从节点层次结构中移除，但是数据存储记录本身被保留。 然后，此未引用的数据存储记录会变成不需要保留的“垃圾”。 在存在多个垃圾资产的情况下，删除它们以保留空间并优化备份和文件系统维护性能是有益的。

在大多数情况下，WCM应用程序倾向于收集信息，但几乎不经常删除信息。 尽管添加了新图像，即使取代旧版本，版本控制系统仍保留旧图像并支持根据需要恢复旧图像。 因此，我们认为添加到系统中的大多数内容实际上都被永久存储。 那么，我们可能想要清理的存储库中“垃圾”的典型来源是什么？

AEM将存储库用作多个内部活动和内部管理活动的存储空间：

* 生成和下载的软件包
* 为发布复制创建的临时文件
* 工作流负载
* 在DAM渲染期间临时创建的资产

当这些临时对象中的任意对象足够大，需要存储在数据存储中，并且当对象最终退出使用时，数据存储记录本身将保留为“垃圾”。 在典型的WCM创作/发布应用程序中，此类垃圾的最大来源通常是发布激活过程。 将数据复制到Publish时，如果首先以高效的数据格式（称为“Durbo”）收集数据，并将其存储在下的存储库中， `/var/replication/data`. 数据包通常大于数据存储的临界大小阈值，因此最终存储为数据存储记录。 复制完成后，中的节点 `/var/replication/data` 将被删除，但数据存储记录仍保留为“垃圾”。

可回收垃圾的另一个来源是包。 包数据（与其他所有内容一样）存储在存储库中，因此对于大于4KB的包，存储在数据存储中。 在开发项目过程中或随着时间的推移在维护系统的同时，可能会多次构建和重建包，每次构建都会产生新的数据存储记录，从而孤立以前的构建记录。

## 数据存储垃圾收集如何工作？ {#how-does-data-store-garbage-collection-work}

如果存储库配置了外部数据存储， [数据存储垃圾收集将自动运行](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) 作为每周维护窗口的一部分。 系统管理员还可以 [手动运行数据存储垃圾收集](#running-data-store-garbage-collection) 根据需要。 通常，建议定期执行数据存储垃圾收集，但在规划数据存储垃圾收集时请考虑以下因素：

* 数据存储垃圾收集需要时间，并且可能会影响性能，因此应该相应地规划垃圾收集。
* 删除数据存储垃圾记录不会影响正常性能，因此这不是性能优化。
* 如果不考虑存储利用率和备份时间等相关因素，则数据存储垃圾收集可能会安全地延迟。

数据存储垃圾回收器在进程开始时首先记录当前时间戳。 然后，使用多通道标记/扫描模式算法进行采集。

在第一阶段，数据存储垃圾收集器对所有存储库内容执行全面遍历。 对于引用了数据存储记录的每个内容对象，它将文件定位到文件系统中，执行元数据更新 — 修改“上次修改时间”或MTIME属性。 此时，通过此阶段访问的文件将变得比初始基线时间戳新。

在第二阶段，数据存储垃圾收集器遍历数据存储的物理目录结构，其方式与“查找”非常相似。 它检查文件的“上次修改”或MTIME属性，并作出以下确定：

* 如果MTIME比初始基线时间戳新，则可能是文件位于第一阶段，或者是一个在收集过程进行期间添加到存储库的全新文件。 在这两种情况下，记录都被认为有效，不应删除文件。
* 如果MTIME早于初始基线时间戳，则该文件不是主动引用的文件，并且被视为可移动垃圾文件。

这种方法非常适用于具有私有数据存储的单个节点。 但是，可以共享数据存储，如果共享意味着不检查来自其他存储库的对数据存储记录的潜在活动实时引用，并且可能会错误地删除活动引用的文件。 在计划任何垃圾收集之前，系统管理员必须了解数据存储的共享性质，并在知道数据存储不共享时，仅使用简单的内置数据存储垃圾收集过程。

>[!NOTE]
>
>在群集或共享数据存储设置（使用Mongo或Segment Tar）中执行垃圾收集时，日志可能会显示有关无法删除某些blob ID的警告。 发生这种情况的原因是，之前垃圾收藏集中删除的Blob ID被其他没有ID删除信息的群集或共享节点再次错误地引用。 因此，执行垃圾收集时，它会尝试删除在上次运行中已删除的ID时记录警告。 此行为不会影响性能或功能。

## 运行数据存储垃圾收集 {#running-data-store-garbage-collection}

根据运行AEM的数据存储设置，有三种方法可运行数据存储垃圾收集：

1. Via [修订版清理](/help/sites-deploying/revision-cleanup.md)  — 通常用于节点存储清理的垃圾收集机制。

1. Via [数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard)  — 特定于外部数据存储的垃圾收集机制，可在操作功能板上找到。
1. 通过 [JMX控制台](/help/sites-administering/jmx-console.md).

如果TarMK同时用作节点存储和数据存储，则修订清理可用于节点存储和数据存储的垃圾收集。 但是，如果配置了外部数据存储（如文件系统数据存储），则必须独立于修订清理显式触发数据存储垃圾收集。 数据存储垃圾收集可以通过操作仪表板或JMX控制台触发。

下表显示了AEM 6中所有受支持的数据存储部署需要使用的数据存储垃圾收集类型：

<table>
 <tbody>
  <tr>
   <td><strong>节点存储</strong><br /> </td>
   <td><strong>数据存储</strong></td>
   <td><strong>垃圾收集机构</strong><br /> </td>
  </tr>
  <tr>
   <td>tarmk</td>
   <td>tarmk</td>
   <td>修订清理（二进制文件与区段存储内联）</td>
  </tr>
  <tr>
   <td>tarmk</td>
   <td>外部文件系统</td>
   <td><p>通过操作仪表板执行数据存储垃圾收集任务</p> <p>JMX控制台</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>通过操作仪表板执行数据存储垃圾收集任务</p> <p>JMX控制台</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>外部文件系统</td>
   <td><p>通过操作仪表板执行数据存储垃圾收集任务</p> <p>JMX控制台</p> </td>
  </tr>
 </tbody>
</table>

### 通过操作仪表板运行数据存储垃圾收集 {#running-data-store-garbage-collection-via-the-operations-dashboard}

内置的“每周维护”窗口，可通过 [操作功能板](/help/sites-administering/operations-dashboard.md)，包含一个内置任务，用于在星期日凌晨1点触发数据存储垃圾收集。

如果您需要在此时间之外运行数据存储垃圾收集，则可以通过操作仪表板手动触发。

在运行数据存储垃圾收集之前，您应该检查当时是否没有运行任何备份。

1. 打开操作功能板的方法有： **导航** -> **工具** -> **操作** -> **维护**.
1. 单击或点按 **每周维护时段**.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. 选择 **数据存储垃圾收集** 任务，然后单击或点按 **运行** 图标。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 数据存储垃圾收集运行，其状态显示在仪表板中。

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>数据存储垃圾收集任务仅在您配置了外部文件数据存储的情况下可见。 请参阅 [在AEM 6中配置节点存储和数据存储](/help/sites-deploying/data-store-config.md#file-data-store) 有关如何设置文件数据存储的信息。

### 通过JMX控制台运行数据存储垃圾收集 {#running-data-store-garbage-collection-via-the-jmx-console}

本节介绍如何通过JMX控制台手动运行数据存储垃圾收集。 如果在没有外部数据存储的情况下设置安装，则这不适用于您的安装。 相反，请参阅下有关如何运行修订清理的说明 [维护存储库](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).

>[!NOTE]
>
>如果您使用外部数据存储来运行TarMK，则需要先运行修订版清理，垃圾收集才能生效。

要运行垃圾收集，请执行以下操作：

1. 在Apache Felix OSGi管理控制台中，突出显示 **主要** 选项卡并选择 **JMX** 从以下菜单中。
1. 接下来，搜索并单击 **存储库管理器** MBean(或转到 `https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`)。
1. 单击 **startDataStoreGC(boolean markOnly)**.
1. 输入&quot;`true`”用于 `markOnly` 参数（如果需要）：

   | **选项** | **描述** |
   |---|---|
   | 布尔markOnly | 设置为true以仅标记参照而不扫描标记和扫描操作。 在多个不同存储库之间共享基础BlobStore时，将使用此模式。 对于所有其他情况，将其设置为false以执行完全垃圾回收。 |

1. 单击 **调用**. CRX运行垃圾收集并指示其完成时间。

>[!NOTE]
>
>数据存储垃圾收集不会收集过去24小时内删除的文件。

>[!NOTE]
>
>仅当配置了外部文件数据存储时，数据存储垃圾收集任务才会启动。 如果尚未配置外部文件数据存储，则任务将返回消息 `Cannot perform operation: no service of type BlobGCMBean found` 调用之后。 请参阅 [在AEM 6中配置节点存储和数据存储](/help/sites-deploying/data-store-config.md#file-data-store) 有关如何设置文件数据存储的信息。

## 自动化数据存储垃圾收集 {#automating-data-store-garbage-collection}

如果可能，应在系统负荷很小时（例如，在早上）运行数据存储垃圾收集。

内置的“每周维护”窗口，可通过 [操作功能板](/help/sites-administering/operations-dashboard.md)，包含一个内置任务，用于在星期日凌晨1点触发数据存储垃圾收集。 您还应检查此时是否没有运行任何备份。 必要时，可以通过仪表板自定义维护窗口的开始。

>[!NOTE]
>
>不同时运行它的原因是，旧的（和未使用的）数据存储文件也会被备份，这样，如果需要回滚到旧的修订版本，则二进制文件仍然在备份中。

如果您不希望使用操作仪表板中的每周维护窗口运行数据存储垃圾收集，还可以使用wget或curl HTTP客户端自动执行此操作。 以下是如何使用curl自动化备份的示例：

>[!CAUTION]
>
>在以下示例中 `curl` 命令可能需要为实例配置各种参数；例如，主机名( `localhost`)，端口( `4502`)，管理员密码( `xyz`)以及实际数据存储垃圾收集的各种参数。

以下是一个示例curl命令，用于通过命令行调用数据存储垃圾收集：

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

curl命令会立即返回。

## 检查数据存储一致性 {#checking-data-store-consistency}

数据存储一致性检查将报告任何缺失但仍被引用的数据存储二进制文件。 要开始一致性检查，请执行以下步骤：

1. 转到JMX控制台。 有关如何使用JMX控制台的信息，请参见 [本文](/help/sites-administering/jmx-console.md#using-the-jmx-console).
1. 搜索 **BlobGarbageCollection** Mbean并单击它。
1. 单击 `checkConsistency()` 链接。

一致性检查完成后，将显示一条消息，显示报告的二进制文件数缺失。 如果数字大于0，请检查 `error.log` 以了解有关缺少的二进制文件的更多详细信息。

下面您将找到如何在日志中报告缺少的二进制文件的示例：

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```
