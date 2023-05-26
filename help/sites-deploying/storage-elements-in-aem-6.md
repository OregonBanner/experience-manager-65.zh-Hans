---
title: AEM 6.5中的存储元素
seo-title: Storage Elements in AEM 6.5
description: 了解AEM 6.5中可用的节点存储实施以及如何维护存储库。
seo-description: Learn about the node storage implementations available in AEM 6.5 and how to maintain the repository.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 1%

---

# AEM 6.5中的存储元素{#storage-elements-in-aem}

本文涵盖以下内容：

* [AEM 6中的存储概述](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [维护存储库](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6中的存储概述 {#overview-of-storage-in-aem}

AEM 6最重要的变化之一是存储库级别的创新。

目前，AEM6中有两种节点存储实施：Tar存储和MongoDB存储。

### Tar存储 {#tar-storage}

#### 使用Tar存储运行新安装的AEM实例 {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>区段节点存储的PID已从org.apache.jackrabbit.oak更改。**插件**&#x200B;在AEM 6的早期版本中为.segment.SegmentNodeStoreService，而在AEM 6.3中为org.apache.jackrabbit.oak.segment.SegmentNodeStoreService。确保进行了必要的配置调整，以便反映所做的更改。

默认情况下，AEM 6使用默认配置选项使用Tar存储来存储节点和二进制文件。 您可以通过执行以下操作来手动配置其存储设置：

1. 下载AEM 6快速入门jar并将其放入新文件夹中。
1. 通过运行以下命令解压缩AEM：

   `java -jar cq-quickstart-6.jar -unpack`

1. 创建名为的文件夹 `crx-quickstart\install` 在安装目录中。

1. 创建一个名为的文件 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` 新建的文件夹中的路径。

1. 编辑文件并设置配置选项。 以下选项可用于区段节点存储，它是AEM Tar存储实施的基础：

   * `repository.home`：存储各种与存储库相关的数据的存储库主目录的路径。 默认情况下，区段文件将存储在crx-quickstart/segmentstore目录下。
   * `tarmk.size`：区段的最大大小（以MB为单位）。 默认值为256 MB。

1. 启动AEM。

### Mongo存储 {#mongo-storage}

#### 使用Mongo Storage运行新安装的AEM实例 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

可以按照以下过程将AEM 6配置为使用MongoDB存储运行：

1. 下载AEM 6快速入门jar并将其放入新文件夹中。
1. 通过运行以下命令解压缩AEM：

   `java -jar cq-quickstart-6.jar -unpack`

1. 确保已安装MongoDB并且实例为 `mongod` 正在运行。 有关更多信息，请参阅 [安装MongoDB](https://docs.mongodb.org/manual/installation/).
1. 创建名为的文件夹 `crx-quickstart\install` 在安装目录中。
1. 通过创建一个包含您想在中使用的配置名称的配置文件来配置节点存储 `crx-quickstart\install` 目录。

   Document Node Store(AEM MongoDB存储实施的基础)使用一个名为的文件 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. 编辑文件并设置配置选项。 以下选项可供选择：

   * `mongouri`：此 [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) 需要连接到Mongo数据库。 默认为 `mongodb://localhost:27017`
   * `db`：Mongo数据库的名称。 默认情况下，新的AEM 6安装使用 **aem-author** 作为数据库名称。
   * `cache`：缓存大小（以MB为单位）。 此缓存大小分布在DocumentNodeStore中使用的各种缓存中。 默认值为256。
   * `changesSize`：Mongo中用于缓存差异输出的限定集合的大小（以MB为单位）。 默认值为256。
   * `customBlobStore`：指示使用自定义数据存储的布尔值。 默认值为false。

1. 使用要使用的数据存储的PID创建配置文件，并编辑该文件以设置配置选项。 有关详细信息，请参阅 [配置节点存储和数据存储](/help/sites-deploying/data-store-config.md).

1. 通过运行以下命令，启动具有MongoDB存储后端的AEM 6 jar：

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   其中后端运行模式为 **`-r`**，该示例从MongoDB支持开始。

#### 禁用透明超大页面 {#disabling-transparent-huge-pages}

Red Hat® Linux®使用称为Transparent Great Pages (THP)的内存管理算法。 虽然AEM执行细粒度读取和写入，但THP已针对大型操作进行了优化。 因此，建议您在Tar和Mongo存储中禁用THP。 要禁用算法，请执行以下步骤：

1. 打开 `/etc/grub.conf` 文件中的文本编辑器。
1. 将以下行添加到 **grub.conf** 文件：

   ```
   transparent_hugepage=never
   ```

1. 最后，通过运行以下命令，检查设置是否已生效：

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果禁用了THP，则上述命令的输出应为：

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>请查阅以下资源：
>
>* 有关Red Hat® Linux®上透明大型页面的更多信息，请参阅此 [文章](https://access.redhat.com/solutions/46111).
* 有关Linux®调整提示，请参阅此 [文章](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=zh-Hans).
>


## 维护存储库 {#maintaining-the-repository}

存储库的每次更新都会创建一个内容修订版本。 因此，存储库的大小会随着每次更新而增长。 为了避免不受控制的存储库增长，必须清理旧修订版以释放磁盘资源。 此维护功能称为修订版清理。 修订清理机制通过从存储库中删除过时数据来回收磁盘空间。 有关修订版清理的更多详细信息，请阅读 [“修订清理”页面](/help/sites-deploying/revision-cleanup.md).
