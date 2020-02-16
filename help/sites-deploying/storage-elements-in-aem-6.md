---
title: AEM 6.5中的存储元素
seo-title: AEM 6.5中的存储元素
description: 了解AEM 6.5中提供的节点存储实现以及如何维护存储库。
seo-description: 了解AEM 6.5中提供的节点存储实现以及如何维护存储库。
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# AEM 6.5中的存储元素{#storage-elements-in-aem}

在本文中，我们将介绍：

* [AEM 6中的存储概述](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [维护存储库](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6中的存储概述 {#overview-of-storage-in-aem}

AEM 6中最重要的更改之一是存储库级别的创新。

目前，AEM6中提供两个节点存储实现：Tar存储和MongoDB存储。

### Tar存储 {#tar-storage}

#### 运行包含Tar Storage的新安装的AEM实例 {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>区段节点存储的PID已从org.apache.jackrabbit.oak更改。**plugins**.segment.SegmentNodeStoreService在AEM 6.3中的先前版本转换为org.apache.jackrabbit.oak.segment.SegmentNodeStoreService。确保进行必要的配置调整以反映此更改。

默认情况下，AEM 6使用Tar存储来存储节点和二进制文件，使用默认配置选项。 要手动配置其存储设置，请按照以下步骤操作：

1. 下载AEM 6快速入门jar并将其放入新文件夹。
1. 通过运行以下项来解压缩AEM:

   `java -jar cq-quickstart-6.jar -unpack`

1. 在安装目录中创 `crx-quickstart\install` 建名为的文件夹。

1. 在新创建的文 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` 件夹中创建名为的文件。

1. 编辑文件并设置配置选项。 以下选项可用于区段节点存储，这是AEM的Tar存储实施的基础：

   * `repository.home`:存储各种存储库相关数据的存储库主目录路径。 默认情况下，段文件将存储在crx-quickstart/segmentstore目录下。
   * `tarmk.size`:段的最大大小(MB)。 默认为256MB。

1. 启动AEM。

### Mongo Storage {#mongo-storage}

#### 使用Mongo Storage运行新安装的AEM实例 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

可以按照以下过程将AEM 6配置为与MongoDB存储一起运行：

1. 下载AEM 6快速入门jar并将其放入新文件夹。
1. 通过运行以下命令解压缩AEM:

   `java -jar cq-quickstart-6.jar -unpack`

1. 确保已安装MongoDB，且某个实例正在 `mongod` 运行。 有关详细信息，请参 [阅安装MongoDB](https://docs.mongodb.org/manual/installation/)。
1. 在安装目录中创 `crx-quickstart\install` 建名为的文件夹。
1. 通过创建一个配置文件来配置节点存储，该配置文件的名称是您要在目录中使用的配 `crx-quickstart\install` 置。

   文档节点存储（AEM的MongoDB存储实施的基础）使用名为 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. 编辑文件并设置配置选项。 以下选项可供选择：

   * `mongouri`:连 [接到Mongo数据库](https://docs.mongodb.org/manual/reference/connection-string/) 所需的MongoURI。 默认为 `mongodb://localhost:27017`
   * `db`:Mongo数据库的名称。 默认情况下，新的AEM 6安装 **使用aem-author** 作为数据库名称。
   * `cache`:缓存大小（以MB为单位）。 它分布在DocumentNodeStore中使用的各种高速缓存中。 默认为 256。
   * `changesSize`:Mongo中用于缓存差异输出的已封闭集合的大小(MB)。 默认为 256。
   * `customBlobStore`:指示将使用自定义数据存储的布尔值。 默认值为false。

1. 使用您要使用的数据存储库的PID创建配置文件并编辑该文件，以设置配置选项。 有关详细信息，请参 [阅配置节点存储和数据存储](/help/sites-deploying/data-store-config.md)。

1. 通过运行以下项，使用MongoDB存储后端启动AEM 6jar:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   其中 **`-r`** 是后端运行模式。 在此示例中，它将从MongoDB支持开始。

#### 禁用透明大页面 {#disabling-transparent-huge-pages}

Red Hat linux使用一种称为“透明大页”(THP)的内存管理算法。 当AEM执行细粒度的读和写时，THP针对大操作进行了优化。 因此，建议您在Tar和Mongo存储上禁用THP。 要禁用算法，请执行以下步骤：

1. 在您选择的 `/etc/grub.conf` 文本编辑器中打开文件。
1. 将以下代码行添 **加到grub.conf** 文件：

   ```
   transparent_hugepage=never
   ```

1. 最后，通过运行以下设置检查该设置是否生效：

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果禁用了THP，则上述命令的输出应为：

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>此外，您还可以参考以下资源：
>
>* 有关Red Hat linux上透明大页的详细信息，请参阅此 [文章](https://access.redhat.com/solutions/46111)。
>* 有关Linux调整提示，请参阅此 [文章](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)。
>



## 维护存储库 {#maintaining-the-repository}

对存储库的每次更新都会创建新内容修订。 因此，每次更新都会增大存储库的大小。 为避免存储库增长失控，需要清理旧版本以释放磁盘资源。 此维护功能称为修订清除。 修订清除机制将通过从存储库中删除过时的数据来回收磁盘空间。 有关“修订清除”的更多详细信息，请阅读“修订 [清除”页面](/help/sites-deploying/revision-cleanup.md)。
