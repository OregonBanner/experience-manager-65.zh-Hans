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
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---


# 数据存储垃圾收集 {#data-store-garbage-collection}

当删除常规WCM资产时，对基础数据存储记录的引用可从节点层次中删除，但数据存储记录本身仍然保持。 此未引用的数据存储记录随后变为“垃圾”，无需保留。 在存在大量垃圾资源的情况下，消除垃圾资源可以节省空间并优化备份和文件系统维护性能，这是很有益的。

在大多数情况下，WCM应用程序往往收集信息，但删除信息的频率几乎不同。 虽然新图像被添加，甚至取代旧版本，但版本控制系统仍保留旧图像，并支持在必要时还原到旧图像。 因此，我们认为添加到系统的大多数内容都被有效地永久存储。 那么，我们可能想要清理的存储库中“垃圾”的典型来源是什么？

AEM将存储库用作许多内部和家政活动的存储:

* 构建和下载的包
* 为发布复制创建的临时文件
* 工作流负载
* 在DAM渲染过程中临时创建的资产

当这些临时对象中的任何一个都足够大，需要存储在数据存储中，并且当该对象最终失效时，数据存储记录本身将保持为“垃圾”。 在典型的WCM作者／发布应用程序中，此类垃圾的最大来源通常是发布激活的过程。 当数据被复制到发布时，如果首先以名为“Durbo”的有效数据格式收集到集合中并存储在`/var/replication/data`下的存储库中，则数据会被复制到发布中。 数据包通常大于数据存储的临界大小阈值，因此最终存储为数据存储记录。 复制完成后，`/var/replication/data`中的节点将被删除，但数据存储记录仍为“垃圾”。

可恢复垃圾的另一个来源是包。 与其他所有数据一样，包数据存储在存储库中，因此存储在数据存储中的包大于4KB。 在开发项目过程中或在一段时间内维护系统时，可以多次构建和重建包，每个构建都生成新的数据存储记录，同构前一个构建的记录。

## 数据存储垃圾收集是如何工作的？{#how-does-data-store-garbage-collection-work}

如果存储库已配置外部数据存储，[数据存储垃圾收集将作为每周维护窗口的一部分自动运行](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection)。 系统管理员还可以根据需要手动[运行数据存储垃圾收集。 ](#running-data-store-garbage-collection)通常，建议定期执行数据存储垃圾收集，但在规划数据存储垃圾收集时应考虑以下因素：

* 数据存储垃圾收集需要时间，并可能影响性能，因此应相应地进行规划。
* 删除数据存储垃圾记录不会影响正常性能，因此这不是性能优化。
* 如果不考虑存储利用率和备份时间等相关因素，则可能会安全地延迟数据存储垃圾收集。

数据存储垃圾收集器在进程开始时首先记录当前时间戳。 然后，使用多通标记／扫描模式算法进行该收集。

在第一阶段，数据存储垃圾收集器对所有存储库内容执行全面遍历。 对于每个引用了数据存储记录的内容对象，它将文件放在文件系统中，执行元数据更新——修改“上次修改时间”或MTIME属性。 此时，此阶段访问的文件将比初始基线时间戳更新。

在第二阶段，数据存储垃圾收集器以与“查找”基本相同的方式遍历数据存储的物理目录结构。 它检查了文件的“上次修改时间”或MTIME属性，并作出以下确定：

* 如果MTIME比初始基线时间戳新，则要么在第一阶段找到该文件，要么是在集合过程进行中添加到存储库的全新文件。 其中一种情况，记录被认为有效，不得删除。
* 如果MTIME在初始基线时间戳之前，则该文件不是主动引用的文件，它被视为可移除垃圾。

此方法适用于具有私有数据存储的单个节点。 但是，数据存储可能是共享的，如果这意味着不检查其他存储库中对数据存储记录的潜在活动实时引用，并且可能错误地删除了活动引用的文件。 在规划任何垃圾收集之前，系统管理员必须了解数据存储的共享性质，并且仅当知道数据存储未共享时才使用简单的内置数据存储垃圾收集过程。

>[!NOTE]
>
>当在群集或共享数据存储设置中执行垃圾收集时（使用Mongo或Segment Tar），日志可能显示有关无法删除某些Blob ID的警告。 发生这种情况的原因是以前垃圾收集中删除的blob ID被其他没有ID删除信息的群集或共享节点再次错误引用。 因此，当执行垃圾收集时，当它尝试删除在上次运行中已删除的ID时，它会记录一条警告消息。 此行为不影响性能或功能。

## 运行数据存储垃圾收集{#running-data-store-garbage-collection}

根据AEM所运行的数据存储设置，有三种运行数据存储垃圾收集的方法：

1. 通过[修订清除](/help/sites-deploying/revision-cleanup.md) —— 通常用于节点存储清理的垃圾收集机制。

1. 通过[数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard) —— 特定于外部数据存储的垃圾收集机制，该机制在“操作”仪表板中可用。
1. 通过[JMX控制台](/help/sites-administering/jmx-console.md)。

如果TarMK同时用作节点存储和数据存储，则“修订清理”可用于节点存储和数据存储的垃圾收集。 但是，如果配置了外部数据存储（如文件系统数据存储），则必须显式触发数据存储垃圾收集，而不是修订清除。 数据存储垃圾收集可通过“操作”仪表板或JMX控制台触发。

下表显示了需要用于AEM 6中所有受支持数据存储部署的数据存储垃圾收集类型：

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
   <td>修订清理（二进制文件与段存储内置）</td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>外部文件系统</td>
   <td><p>通过“操作”任务存储垃圾收集仪表板</p> <p>JMX控制台</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>通过“操作”任务存储垃圾收集仪表板</p> <p>JMX控制台</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>外部文件系统</td>
   <td><p>通过“操作”任务存储垃圾收集仪表板</p> <p>JMX控制台</p> </td>
  </tr>
 </tbody>
</table>

### 通过操作仪表板{#running-data-store-garbage-collection-via-the-operations-dashboard}运行数据存储垃圾收集

内置的每周维护窗口(可通过[操作仪表板](/help/sites-administering/operations-dashboard.md)访问)包含一个内置任务，用于在周日的凌晨1点触发数据存储垃圾收集。

如果您需要在此时间之外运行数据存储垃圾收集，则可以通过“操作”仪表板手动触发。

在运行数据存储垃圾收集之前，您应检查当时没有运行备份。

1. 通过&#x200B;**Navigation** -> **Tools** -> **Operations** -> **Maintenance**&#x200B;打开“操作”仪表板。
1. 单击或点按&#x200B;**每周维护窗口**。

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. 选择&#x200B;**数据存储垃圾收集**&#x200B;任务，然后单击或点按&#x200B;**运行**&#x200B;图标。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 数据存储垃圾收集运行，其状态显示在仪表板中。

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>只有在配置了外部文件数据存储时，数据存储垃圾收集任务才可见。 有关如何设置文件数据存储的信息，请参见[在AEM 6](/help/sites-deploying/data-store-config.md#file-data-store)中配置节点存储和数据存储。

### 通过JMX控制台{#running-data-store-garbage-collection-via-the-jmx-console}运行数据存储垃圾收集

本节介绍如何通过JMX控制台手动运行数据存储垃圾收集。 如果安装是在没有外部数据存储的情况下设置的，则这不适用于您的安装。 相反，请参见[维护存储库](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)下有关如何运行修订清理的说明。

>[!NOTE]
>
>如果您正在与外部数据存储一起运行TarMK，则需要先运行修订清理，以便垃圾收集有效。

要运行垃圾收集，请执行以下操作：

1. 在Apache Felix OSGi管理控制台中，突出显示&#x200B;**Main**&#x200B;选项卡，并从以下菜单中选择&#x200B;**JMX**。
1. 然后，搜索并单击&#x200B;**存储库管理器** MBean（或转至`https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`）。
1. 单击&#x200B;**startDataStoreGC(boolean markOnly)**。
1. 如果需要，输入“`true`”作为&lt;a1/>参数：`markOnly`

   | **选项** | **描述** |
   |---|---|
   | 布尔型markOnly | 在标记和扫描操作中，设置为true可仅标记参照而不扫描。 当基础BlobStore在多个不同的存储库之间共享时，将使用此模式。 对于所有其他情况，将其设置为false即可执行完全垃圾收集。 |

1. 单击&#x200B;**调用**。 CRX运行垃圾收集并指示它何时完成。

>[!NOTE]
>
>数据存储垃圾收集不会收集在过去24小时内已删除的文件。

>[!NOTE]
>
>仅当您配置了外部文件数据存储时，数据存储垃圾收集任务才会开始。 如果尚未配置外部文件数据存储，任务将在调用后返回消息`Cannot perform operation: no service of type BlobGCMBean found`。 有关如何设置文件数据存储的信息，请参见[在AEM 6](/help/sites-deploying/data-store-config.md#file-data-store)中配置节点存储和数据存储。

## 自动化数据存储垃圾收集{#automating-data-store-garbage-collection}

如果可能，应在系统上负载很小时（例如在上午）运行数据存储垃圾收集。

内置的每周维护窗口(可通过[操作仪表板](/help/sites-administering/operations-dashboard.md)访问)包含一个内置任务，用于在周日的凌晨1点触发数据存储垃圾收集。 您还应检查此时是否未运行备份。 可以根据需要通过开始来自定义维护窗口的仪表板。

>[!NOTE]
>
>不同时运行它的原因是，旧（和未使用）数据存储文件也得到备份，因此，如果需要回滚到旧修订，二进制文件仍在备份中。

如果您不想在“操作”仪表板中使用“每周维护窗口”运行数据存储垃圾收集，也可以使用wget或curl HTTP客户端自动进行。 以下是如何使用curl自动备份的示例：

>[!CAUTION]
>
>在以下示例中，`curl`命令可能需要为实例配置各种参数；例如，主机名(`localhost`)、端口(`4502`)、管理员密码(`xyz`)和实际数据存储垃圾收集的各种参数。

下面是一个通过命令行调用数据存储垃圾收集的curl命令示例：

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

curl命令会立即返回。

## 检查数据存储一致性{#checking-data-store-consistency}

数据存储一致性检查将报告所有缺少但仍被引用的数据存储二进制文件。 要开始一致性检查，请执行以下步骤：

1. 转到JMX控制台。 有关如何使用JMX控制台的信息，请参阅[本文](/help/sites-administering/jmx-console.md#using-the-jmx-console)。
1. 搜索&#x200B;**BlobGarbageCollection** Mbean并单击它。
1. 单击`checkConsistency()`链接。

一致性检查完成后，将显示报告为缺失的二进制文件数。 如果该数字大于0，请检查`error.log`以了解有关缺失二进制文件的详细信息。

在下面，您将在日志中找到如何报告缺少的二进制文件的示例：

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```

