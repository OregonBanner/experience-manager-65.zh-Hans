---
title: AEM 6.5中的存储元素
seo-title: AEM 6.5中的存储元素
description: 了解AEM 6.5中可用的节点存储实施以及如何维护存储库。
seo-description: 了解AEM 6.5中可用的节点存储实施以及如何维护存储库。
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---

# AEM 6.5{#storage-elements-in-aem}中的存储元素

在本文中，我们将介绍：

* [AEM 6中的存储概述](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [维护存储库](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6 {#overview-of-storage-in-aem}中的存储概述

AEM 6中最重要的更改之一是存储库级别的创新。

目前，AEM6中提供了两个节点存储实施：Tar存储和MongoDB存储。

### 焦油存储{#tar-storage}

#### 运行新安装的AEM实例和Tar存储{#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>区段节点存储的PID已从org.apache.jackrabbit.oak发生更改。**plugins**.segment.SegmentNodeStoreService(在AEM 6的先前版本中)到AEM 6.3中的org.apache.jackrabbit.oak.segment.SegmentNodeStoreService。请确保进行必要的配置调整以反映此更改。

默认情况下，AEM 6使用Tar存储，使用默认配置选项来存储节点和二进制文件。 要手动配置其存储设置，请按照以下步骤操作：

1. 下载AEM 6快速入门Jar并将其置于新文件夹中。
1. 运行以解包AEM:

   `java -jar cq-quickstart-6.jar -unpack`

1. 在安装目录中创建名为`crx-quickstart\install`的文件夹。

1. 在新创建的文件夹中创建名为`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`的文件。

1. 编辑文件并设置配置选项。 区段节点存储提供了以下选项，这是AEM Tar存储实施的基础：

   * `repository.home`:存储各种存储库相关数据的存储库主页的路径。默认情况下，区段文件将存储在crx-quickstart/segmentstore目录下。
   * `tarmk.size`:区段的最大大小(MB)。默认为256MB。

1. 启动AEM。

### Mongo存储{#mongo-storage}

#### 使用Mongo Storage {#running-a-freshly-installed-aem-instance-with-mongo-storage}运行新安装的AEM实例

AEM 6可配置为通过MongoDB存储运行，具体过程如下：

1. 下载AEM 6快速入门Jar并将其放入新文件夹中。
1. 运行以下命令解包AEM:

   `java -jar cq-quickstart-6.jar -unpack`

1. 确保已安装MongoDB，并且`mongod`的实例正在运行。 有关更多信息，请参阅[安装MongoDB](https://docs.mongodb.org/manual/installation/)。
1. 在安装目录中创建名为`crx-quickstart\install`的文件夹。
1. 通过创建一个配置文件来配置节点存储，该配置文件的名称是您要在`crx-quickstart\install`目录中使用的配置。

   文档节点存储(是AEM MongoDB存储实施的基础)使用名为`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`的文件

1. 编辑文件并设置配置选项。 以下选项可供选择：

   * `mongouri`:连 [](https://docs.mongodb.org/manual/reference/connection-string/) 接到Mongo数据库所需的MongoURI。默认为 `mongodb://localhost:27017`
   * `db`:Mongo数据库的名称。默认情况下，新的AEM 6安装使用&#x200B;**aem-author**&#x200B;作为数据库名称。
   * `cache`:高速缓存大小(MB)。它分布在DocumentNodeStore中使用的各种缓存中。 默认为 256。
   * `changesSize`:Mongo中用于缓存差异输出的封闭集合的大小(MB)。默认为 256。
   * `customBlobStore`:布尔值，指示将使用自定义数据存储。默认值为false。

1. 使用您要使用的数据存储的PID创建配置文件，然后编辑该文件以设置配置选项。 有关更多信息，请参阅[配置节点存储和数据存储](/help/sites-deploying/data-store-config.md)。

1. 通过运行以下操作，使用MongoDB存储后端启动AEM 6 jar :

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   其中&#x200B;**`-r`**&#x200B;是后端运行模式。 在本例中，将从MongoDB支持开始。

#### 禁用透明大页面{#disabling-transparent-huge-pages}

Red Hat Linux使用一种名为“透明大页”(THP)的内存管理算法。 在AEM执行细粒度读取和写入时，THP已针对大型操作进行优化。 因此，建议您在Tar和Mongo存储上禁用THP。 要禁用算法，请执行以下步骤：

1. 在您选择的文本编辑器中打开`/etc/grub.conf`文件。
1. 将以下行添加到&#x200B;**grub.conf**&#x200B;文件：

   ```
   transparent_hugepage=never
   ```

1. 最后，通过运行以检查该设置是否生效：

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果禁用了THP，则上述命令的输出应为：

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>此外，您还可以查阅以下资源：
>
>* 有关Red Hat Linux上透明大页的详细信息，请参阅此[文章](https://access.redhat.com/solutions/46111)。
>* 有关Linux调整提示，请参阅此[文章](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)。

>



## 维护存储库{#maintaining-the-repository}

对存储库的每次更新都会创建新的内容修订版本。 因此，每次更新时，存储库的大小都会增大。 为避免存储库增长失控，需要清理旧的修订版本以释放磁盘资源。 此维护功能称为修订清理。 修订清理机制将通过从存储库中删除过时的数据来回收磁盘空间。 有关修订清理的更多详细信息，请阅读[修订清理页面](/help/sites-deploying/revision-cleanup.md)。
