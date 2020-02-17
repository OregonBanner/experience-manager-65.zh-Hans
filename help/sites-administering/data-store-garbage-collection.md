---
title: 数据存储垃圾收集
seo-title: 数据存储垃圾收集
description: 了解如何配置Data Store垃圾收集以释放磁盘空间。
seo-description: 了解如何配置Data Store垃圾收集以释放磁盘空间。
uuid: 49488a81-986a-4d1a-96c8-aeb6595fc094
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5b1e46c5-7e56-433e-b62e-2a76ea7be0fd
docset: aem65
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2

---


# 数据存储垃圾收集 {#data-store-garbage-collection}

当删除常规WCM资产时，对基础数据存储记录的引用可以从节点层次中删除，但数据存储记录本身保持。 这个未引用的数据存储记录随后变为“垃圾”，无需保留。 在存在大量垃圾资产的情况下，删除这些资产以保留空间并优化备份和文件系统维护性能是有益的。

在大多数情况下，WCM应用程序往往收集信息，但删除信息的频率几乎不同。 虽然添加了新图像，甚至取代了旧版本，但版本控制系统仍保留旧版本，并在需要时支持还原到旧版本。 因此，我们认为添加到系统的大多数内容都被有效地永久存储。 那么，我们可能想要清理的存储库中“垃圾”的典型来源是什么？

AEM将存储库用作许多内部和家务活动的存储：

* 构建和下载的包
* 为发布复制创建的临时文件
* 工作流负载
* 在DAM渲染期间临时创建的资产

当任何这些临时对象都足够大以需要数据存储在数据存储中时，并且当该对象最终失效时，数据存储记录本身将保持为“垃圾”。 在典型的WCM作者／发布应用程序中，此类垃圾的最大来源通常是发布激活过程。 当数据被复制到发布时，如果首先以名为“Durbo”的高效数据格式收集到集合中并存储在位于下的存储库中，则数据将被复制到发布中 `/var/replication/data`。 数据包通常大于数据存储的临界大小阈值，因此最终存储为数据存储记录。 复制完成后，将删除中的节 `/var/replication/data` 点，但数据存储记录仍保留为“垃圾”。

另一个可恢复垃圾源是包。 与其他所有内容一样，包数据存储在存储库中，因此存储在数据存储中的包大于4KB。 在开发项目过程中或在一段时间内维护系统时，可以多次构建和重建包，每个构建产生新的数据存储记录，同构前一个构建的记录。

## 数据存储垃圾收集是如何工作的？ {#how-does-data-store-garbage-collection-work}

如果存储库已配置外部数据存储，则数 [据存储垃圾收集将作为每周维护窗口的一部分自动运行](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) 。 系统管理员还可 [以根据需要手动运行数据存储垃圾收集](#running-data-store-garbage-collection) 。 通常，建议定期执行数据存储垃圾收集，但在规划数据存储垃圾收集时应考虑以下因素：

* 数据存储垃圾收集需要时间并且可能会影响性能，因此应相应地进行规划。
* 删除数据存储垃圾记录不会影响正常性能，因此这不是性能优化。
* 如果不考虑存储利用率和备份时间等相关因素，那么数据存储垃圾收集可能会被安全地推迟。

数据存储垃圾收集器在进程开始时首先记录当前时间戳。 然后，使用多通标记／扫描图案算法执行该集合。

在第一阶段，数据存储垃圾收集器对所有存储库内容执行全面遍历。 对于引用数据存储记录的每个内容对象，它都将文件放在文件系统中，执行元数据更新——修改“上次修改时间”或MTIME属性。 此时，此阶段访问的文件将比初始基线时间戳更新。

在第二阶段，数据存储垃圾收集器以与“查找”基本相同的方式遍历数据存储的物理目录结构。 它检查了文件的“上次修改时间”或MTIME属性，并作出以下决定：

* 如果MTIME比初始基准时间戳新，则文件在第一阶段找到，或者它是在集合进程进行期间添加到存储库的全新文件。 其中任何一种情况均认为记录有效，不得删除。
* 如果MTIME在初始基准时间戳之前，则该文件不是主动引用的文件，它被视为可删除垃圾。

此方法适用于具有专用数据存储的单个节点。 但是，数据存储可能是共享的，如果这意味着不检查对来自其他存储库的数据存储记录的潜在活动实时引用，并且可能错误地删除了活动引用的文件。 在规划任何垃圾收集之前，系统管理员必须了解数据存储的共享性质，并且只在知道数据存储没有共享时使用简单的内置数据存储垃圾收集过程。

>[!NOTE]
>
>在群集或共享数据存储设置中执行垃圾收集时（使用Mongo或区段Tar），日志可能显示有关无法删除某些blob ID的警告。 这是因为在以前的垃圾收集中删除的blob ID被其他没有ID删除信息的群集或共享节点再次错误地引用。 因此，当执行垃圾收集时，它会在尝试删除在上次运行中已删除的ID时记录一条警告消息。 此行为不影响性能或功能。

## Running Data Store Garbage Collection {#running-data-store-garbage-collection}

根据AEM所运行的数据存储设置，有三种运行数据存储垃圾收集的方法：

1. 通过 [修订清除](/help/sites-deploying/revision-cleanup.md) -通常用于节点存储清理的垃圾收集机制。

1. 通过 [数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard) -一种特定于外部数据存储的垃圾收集机制，可在操作控制板上使用。
1. 通过 [JMX控制台](/help/sites-administering/jmx-console.md)。

如果TarMK同时用作节点存储和数据存储，则“修订清除”可用于节点存储和数据存储的垃圾收集。 但是，如果配置了外部数据存储（如文件系统数据存储），则必须显式触发数据存储垃圾收集与修订清除。 数据存储垃圾收集可以通过操作控制板或JMX控制台触发。

下表显示了AEM 6中需要用于所有受支持数据存储部署的数据存储垃圾收集类型：

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
   <td>修订清除（二进制文件与区段存储内嵌）</td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>外部文件系统</td>
   <td><p>通过操作控制板执行数据存储垃圾收集任务</p> <p>JMX控制台</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>通过操作控制板执行数据存储垃圾收集任务</p> <p>JMX控制台</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>外部文件系统</td>
   <td><p>通过操作控制板执行数据存储垃圾收集任务</p> <p>JMX控制台</p> </td>
  </tr>
 </tbody>
</table>

### 通过“操作控制板”运行数据存储垃圾收集 {#running-data-store-garbage-collection-via-the-operations-dashboard}

内置的每周维护窗口(通过 [Operations Dashboard提供](/help/sites-administering/operations-dashboard.md))包含一个内置任务，用于在周日的凌晨1点触发Data Store垃圾收集。

如果您需要在此时间之外运行数据存储垃圾收集，则可以通过“操作控制板”手动触发该垃圾收集。

在运行数据存储垃圾收集之前，您应检查当时是否没有运行备份。

1. 通过导航打开“操作 **控制板** ” -> **Tools** -> **Operations** - **Maintenance Internation**”。
1. 单击或点按每周 **维护窗口**。

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. 选择“数 **据存储垃圾收集** ”任务，然后单击或点按“运 **行** ”图标。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 数据存储垃圾收集会运行，其状态会显示在功能板中。

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>只有在您配置了外部文件数据存储时，“数据存储垃圾收集”任务才可见。 有关 [如何设置文件数据存储的信息，请参阅配置AEM 6中的节点存储和数据存储](/help/sites-deploying/data-store-config.md#file-data-store) 。

### 通过JMX控制台运行数据存储垃圾收集 {#running-data-store-garbage-collection-via-the-jmx-console}

本节介绍如何通过JMX控制台手动运行数据存储垃圾收集。 如果安装是在没有外部数据存储的情况下进行的，则这不适用于您的安装。 相反，请参阅维护存储库下有关如何运行修订清 [除的说明](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)。

>[!NOTE]
>
>如果您使用外部数据存储运行TarMK，则需要先运行“修订清除”，以使垃圾收集有效。

运行垃圾收集：

1. 在Apache Felix OSGi管理控制台中，突出显示 **Main** （主）选项卡，并从以下菜单 **中选择** JMX。
1. 然后，搜索并单击 **Repository Manager** MBean(或转至 `https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`)。
1. 单击 **startDataStoreGC(boolean markOnly)**。
1. 如果需要，`true`请输入“ `markOnly` ”作为参数：

   | **Option** | **描述** |
   |---|---|
   | boolean markOnly | 在标记和扫描操作中，设置为true可仅标记参照而不扫描。 当在多个不同存储库之间共享基础BlobStore时，将使用此模式。 对于所有其他情况，将其设置为false即可执行完全垃圾收集。 |

1. 单击“ **调用**”。 CRX运行垃圾收集并指示其何时完成。

>[!NOTE]
>
>数据存储垃圾收集不会收集在过去24小时内已删除的文件。

>[!NOTE]
>
>只有在您配置了外部文件数据存储时，数据存储垃圾收集任务才会启动。 如果尚未配置外部文件数据存储，则任务将在调用后返回 `Cannot perform operation: no service of type BlobGCMBean found` 消息。 有关 [如何设置文件数据存储的信息，请参阅配置AEM 6中的节点存储和数据存储](/help/sites-deploying/data-store-config.md#file-data-store) 。

## Automating Data Store Garbage Collection {#automating-data-store-garbage-collection}

如果可能，应在系统上负载很少时运行数据存储垃圾收集，例如在上午。

内置的每周维护窗口(通过 [Operations Dashboard提供](/help/sites-administering/operations-dashboard.md))包含一个内置任务，用于在周日的凌晨1点触发Data Store垃圾收集。 您还应检查此时是否未运行备份。 维护窗口的开始可以根据需要通过仪表板进行自定义。

>[!NOTE]
>
>不同时运行它的原因是，旧（和未使用）数据存储文件也会备份，因此，如果需要回滚到旧版本，则二进制文件仍位于备份中。

如果您不想在“操作控制板”的“每周维护窗口”中运行数据存储垃圾收集，也可以使用wget或curl HTTP客户端自动执行垃圾收集。 以下是如何使用curl自动备份的示例：

>[!CAUTION]
>
>在以下示例 `curl` 中，可能需要为实例配置各种参数；例如，实际数据存储垃圾 `localhost`收集的主机名()、端口( `4502`)、管理员密码( `xyz`)和各种参数。

下面是一个通过命令行调用数据存储垃圾收集的curl命令示例：

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

curl命令会立即返回。

## 检查数据存储一致性 {#checking-data-store-consistency}

数据存储一致性检查将报告所有缺少但仍被引用的数据存储二进制文件。 要开始一致性检查，请执行以下步骤：

1. 转到JMX控制台。 有关如何使用JMX控制台的信息，请参 [阅本文](/help/sites-administering/jmx-console.md#using-the-jmx-console)。
1. 搜索 **BlobGarbageCollection** Mbean并单击它。
1. 单击链 `checkConsistency()` 接。

一致性检查完成后，将显示一条消息，显示报告为缺失的二进制文件数。 如果该数字大于0，请查看，以了 `error.log` 解有关缺失二进制文件的更多详细信息。

以下是如何在日志中报告缺少的二进制文件的示例：

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```

