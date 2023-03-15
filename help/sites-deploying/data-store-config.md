---
title: 在AEM 6中配置节点存储和数据存储
description: 了解如何配置节点存储和数据存储以及如何执行数据存储垃圾收集。
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
exl-id: c1c90d6a-ee5a-487d-9a8a-741b407c8c06
source-git-commit: 461424de9158e14e251037004ea3590ed35bb4a0
workflow-type: tm+mt
source-wordcount: '3584'
ht-degree: 2%

---

# 在AEM 6中配置节点存储和数据存储{#configuring-node-stores-and-data-stores-in-aem}

## 简介 {#introduction}

在Adobe Experience Manager (AEM)中，可以独立于内容节点存储二进制数据。 二进制数据存储在数据存储中，而内容节点存储在节点存储中。

可以使用OSGi配置配置数据存储和节点存储。 每个OSGi配置都使用永久性标识符(PID)引用。

## 配置步骤 {#configuration-steps}

要配置节点存储和数据存储，请执行以下步骤：

1. 将AEM快速入门JAR文件复制到其安装目录。
1. 创建文件夹 `crx-quickstart/install` 在安装目录中。
1. 首先，通过创建包含要在中使用的节点存储选项名称的配置文件来配置节点存储 `crx-quickstart/install` 目录。

   例如，Document节点存储(AEM MongoMK实施的基础)使用文件 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. 编辑文件，并设置配置选项。
1. 使用要使用的数据存储的PID创建配置文件。 编辑文件以设置配置选项。

   >[!NOTE]
   >
   >参见 [节点存储配置](#node-store-configurations) 和 [数据存储配置](#data-store-configurations) 配置选项。

1. 启动AEM。

## 节点存储配置 {#node-store-configurations}

>[!CAUTION]
>
>较新版本的Oak对OSGi配置文件采用新的命名方案和格式。 新的命名方案要求配置文件命名为 **.config** 并且新格式要求键入值，并且 [在此处记录](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>如果您从旧版Oak升级，请确保您对 `crx-quickstart/install`文件夹优先。 升级后，将文件夹的内容恢复到升级后的安装，并从修改配置文件的扩展名 **.cfg** 到 **.config**.
>
>如果您正在阅读本文，以便为从 **AEM 5.x** 安装，请务必查阅 [升级](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html) 文档优先。

### 区段节点存储 {#segment-node-store}

区段节点存储是Adobe在AEM6中实施TarMK的基础。 它使用 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` 用于配置的PID。

>[!CAUTION]
>
>区段节点存储的PID已从 `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` / AEM 6至 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` 在AEM 6.3中。确保进行必要的配置调整以反映此更改。

您可以配置以下选项：

* `repository.home`：存储与存储库相关的数据的存储库主目录的路径。 默认情况下，区段文件存储在 `crx-quickstart/segmentstore` 目录。

* `tarmk.size`：区段的最大大小（以MB为单位）。 默认最大为256MB。
* `customBlobStore`：指示使用自定义数据存储的布尔值。 对于AEM 6.3及更高版本，默认值为true。 在AEM 6.3之前，默认为false。

以下是示例 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` 文件：

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### 文档节点存储 {#document-node-store}

文档节点存储是AEM MongoMK实现的基础。 它使用 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID。 以下配置选项可用：

* `mongouri`：此 [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) 需要连接到Mongo数据库。 默认为 `mongodb://localhost:27017`

* `db`：Mongo数据库的名称。 默认为 **Oak** ``. However, new AEM 6 installations use **aem-author** ``作为默认数据库名称。

* `cache`：缓存大小（以MB为单位）。 这分布在DocumentNodeStore中使用的各种缓存中。 默认为 `256`

* `changesSize`：Mongo中用于缓存差异输出的限定集合的大小（以MB为单位）。 默认为 `256`

* `customBlobStore`：布尔值，指示将使用自定义数据存储。 默认为 `false`。

以下是示例 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` 文件：

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## 数据存储配置 {#data-store-configurations}

在处理大量二进制文件时，建议使用外部数据存储而不是默认节点存储，以便最大化性能。

例如，如果您的项目需要大量媒体资产，将它们存储在File或S3 Data Store下将使访问它们的速度比直接存储在MongoDB中更快。

文件数据存储提供了比MongoDB更好的性能，而且对于大量资产， Mongo备份和恢复操作也较慢。

有关不同数据存储和配置的详细信息如下所述。

>[!NOTE]
>
>要启用自定义数据存储，您需要确保 `customBlobStore` 设置为 `true` 在相应的Node Store配置文件([区段节点存储](/help/sites-deploying/data-store-config.md#segment-node-store) 或 [文档节点存储](/help/sites-deploying/data-store-config.md#document-node-store))。

### 文件数据存储 {#file-data-store}

这是的实施 [FileDataStore](https://jackrabbit.apache.org/api/trunk/org/apache/jackrabbit/core/data/FileDataStore.html) 在Jackrabbit 2中提供。 它提供了一种将二进制数据作为普通文件存储在文件系统中的方法。 它使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` pid。

这些配置选项可用：

* `repository.home`：存储各种存储库相关数据的存储库主目录的路径。 默认情况下，二进制文件将存储在 `crx-quickstart/repository/datastore` 目录

* `path`：存储文件时所在的目录的路径。 如果指定，则优先于 `repository.home` 值

* `minRecordLength`：数据存储中存储的文件的最小大小（以字节为单位）。 将内联小于此值的二进制内容。

>[!NOTE]
>
>使用NAS存储共享文件数据存储时，请确保仅使用高性能设备以避免性能问题。

## Amazon S3数据存储 {#amazon-s-data-store}

可以将AEM配置为将数据存储在Amazon的简单存储服务(S3)中。 它使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 用于配置的PID。

为了启用S3数据存储功能，需要下载并安装包含S3数据存储连接器的功能包。 转到 [Adobe存储库](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) 并从1.10.x版的功能包（例如，com.adobe.granite.oak.s3connector-1.10.0.zip）下载最新版本。 此外，您还需要下载并安装列于以下地址的最新AEM Service Pack： [AEM 6.5发行说明](/help/release-notes/release-notes.md) 页面。

>[!NOTE]
>
>在将AEM与TarMK结合使用时，默认情况下，二进制文件将存储在 `FileDataStore`. 要将TarMK与S3数据存储区结合使用，您需要使用启动AEM `crx3tar-nofds` 运行模式，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下载后，您可以按如下方式安装和配置S3 Connector：

1. 将功能包zip文件的内容提取到临时文件夹。

1. 转到临时文件夹并导航到以下位置：

   ```xml
   jcr_root/libs/system/install
   ```

   将以上位置的所有内容复制到 `<aem-install>/crx-quickstart/install.`

1. 如果已将AEM配置为使用Tar或MongoDB存储，请从***中删除任何现有的配置文件&lt;aem-install>***/*crx-quickstart*/*安装* 文件夹，然后再继续。 需要删除的文件包括：

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回到提取功能包的临时位置，并复制以下文件夹的内容：

   * `jcr_root/libs/system/config`

   到

   * `<aem-install>/crx-quickstart/install`

   确保仅复制当前配置所需的配置文件。 对于专用数据存储和共享数据存储设置，请复制 `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 文件。

   >[!NOTE]
   >
   >在群集设置中，对群集的所有节点逐个执行上述步骤。 此外，请确保对所有节点使用相同的S3设置。

1. 编辑文件并添加设置所需的配置选项。
1. 启动AEM。

## 升级到1.10.x S3连接器的新版本 {#upgrading-to-a-new-version-of-the-s-connector}

如果您需要升级到新版本的1.10.x S3连接器（例如，从1.10.0到1.10.4），请执行以下步骤：

1. 停止AEM实例。

1. 导航到 `<aem-install>/crx-quickstart/install/15` AEM ，并备份其内容。
1. 备份后，删除S3连接器的旧版本及其依赖项，方法是删除 `<aem-install>/crx-quickstart/install/15` 文件夹，例如：

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >上述文件名仅用于说明目的。

1. 从以下位置下载最新版本的1.10.x功能包： [Adobe存储库](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. 将内容解压缩到单独的文件夹，然后导航到 `jcr_root/libs/system/install/15`.
1. 将jar文件复制到 **&lt;aem-install>**/crx-quickstart/install/15位于AEM安装文件夹中。
1. 启动AEM并检查连接器功能。

您可以使用配置文件以及下面详述的选项。

<!--
* accessKey: The AWS access key.
* secretKey: The AWS secret access key. **Note:** When the `accessKey` or `secretKey` is not specified then the [IAM role](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) is used for authentication.
* s3Bucket: The bucket name.
* s3Region: The bucket region.
* path: The path of the data store. The default is **&lt;AEM install folder&gt;/repository/datastore**
* minRecordLength: The minimum size of an object that should be stored in the data store. The minimum/default is **16KB.**
* maxCachedBinarySize: Binaries with size less than or equal to this size will be stored in memory cache. The size is in bytes. The default is **17408 **(17 KB).
* cacheSize: The size of the cache. The value is specified in bytes. The default is **64GB**.
* secret: Only to be used if using binaryless replication for shared datastore setup.
* stagingSplitPercentage: The percentage of cache size configured to be used for staging asynchronous uploads. The default value is **10**.
* uploadThreads: The number of uploads threads that are used for asynchronous uploads. The default value is **10**.
* stagingPurgeInterval: The interval in seconds for purging finished uploads from the staging cache. The default value is **300** seconds (5 minutes).
* stagingRetryInterval: The retry interval in seconds for failed uploads. The default value is **600** seconds (10 minutes).
-->

### S3连接器配置文件选项 {#s3-connector-configuration-file-options}

>[!NOTE]
>
>S3连接器同时支持IAM用户身份验证和IAM角色身份验证。 要使用IAM角色身份验证，请忽略 `accessKey` 和 `secretKey` 配置文件中的值。 然后，S3连接器将默认为 [IAM角色](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) 已分配给实例。

| 键 | 描述 | 默认 | 必填 |
| --- | --- | --- | --- |
| accessKey | 有权访问存储桶的IAM用户的访问密钥ID。 |  | 是，当不使用IAM角色时。 |
| 密钥 | 有权访问存储桶的IAM用户的访问密钥。 |  | 是，当不使用IAM角色时。 |
| cachesize | 本地缓存的大小（以字节为单位）。 | 64GB | 否. |
| connectimeout | 设置初始建立连接时超时前等待的时间（以毫秒为单位）。 | 10000 | 否. |
| maxCachedBinarySize | 大小小于或等于此值（以字节为单位）的二进制文件将存储在内存缓存中。 | 17408 (17 KB) | 否. |
| maxConnections | 设置允许的最大打开HTTP连接数。 | 50 | 否. |
| maxErrorRetry | 设置失败的（可重试的）请求的最大重试次数。 | 3 | 否. |
| minRecordLength | 应存储在数据存储中的对象的最小大小（以字节为单位）。 | 16384 | 否. |
| 路径 | AEM数据存储的本地路径。 | `crx-quickstart/repository/datastore` | 否. |
| proxyHost | 设置客户端将连接的可选代理主机。 |  | 否. |
| 代理端口 | 设置客户端将连接的可选代理端口。 |  | 否. |
| s3Bucket | S3存储段的名称。 |  | 是 |
| s3EndPoint | S3 REST API端点。 |  | 否. |
| s3Region | 存储段所在的区域。 查看此 [页面](https://docs.aws.amazon.com/general/latest/gr/s3.html) 了解更多详细信息。 | 运行AWS实例的区域。 | 否. |
| sockettimeout | 设置在连接超时并关闭之前等待通过已建立的打开连接传输数据的时间（毫秒）。 | 50000 | 否. |
| stagingPurgeInterval | 从暂存缓存中清除已完成上载的时间间隔（以秒为单位）。 | 300 | 否. |
| stagingRetryInterval | 重试失败上载的时间间隔（以秒为单位）。 | 600 | 否. |
| stagingSplitPercentage | 百分比 `cacheSize` 用于暂存异步上传。 | 10 | 否. |
| uploadthreads | 用于异步上传的上传线程数。 | 10 | 否. |
| writeThreads | 通过S3传输管理器写入时使用的并发线程数。 | 10 | 否. |

<!---
### Bucket region options {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>US Standard</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>US West</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>US West (Northern California)</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>EU (Ireland)<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Singapore)<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Sydney)<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Tokyo)</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>South America (Sao Paolo)<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>
-->

### 数据存储缓存 {#data-store-caching}

>[!NOTE]
>
>的DataStore实施 `S3DataStore`， `CachingFileDataStore` 和 `AzureDataStore` 支持本地文件系统缓存。 此 `CachingFileDataStore` 当DataStore位于NFS （网络文件系统）上时，实施非常有用。

从旧版缓存实施（Oak 1.6以前的版本）升级时，本地文件系统缓存目录的结构存在差异。 在旧的缓存结构中，下载的文件和上传的文件都直接放在缓存路径下。 新结构将下载和上传分开，并将其存储在两个名为的目录中 `upload` 和 `download` 在缓存路径下。 升级过程应该是无缝的，所有挂起的上传都应安排在上传，之前下载到缓存中的任何文件都将在初始化时放入缓存中。

您还可以使用以下工具离线升级缓存： `datastorecacheupgrade` oak-run的命令。 有关如何执行命令的详细信息，请检查 [自述文件](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) 用于oak-run模块。

缓存具有大小限制，可以使用cacheSize参数进行配置。

#### 下载 {#downloads}

在从DataStore访问请求的文件/blob之前，将检查本地缓存中的记录。 当缓存超过配置的限制时(请参阅 `cacheSize` 参数)，则在向缓存中添加文件时，将会收回某些文件以回收空间。

#### 异步上传 {#async-upload}

缓存支持异步上传到DataStore。 文件将存放在本地、缓存中（在文件系统中），并且开始执行异步作业以上传文件。 异步上传的数量受临时缓存大小的限制。 使用配置暂存缓存的大小 `stagingSplitPercentage` 参数。 此参数定义用于暂存缓存的缓存大小百分比。 此外，还可计算可用于下载的缓存的百分比 **(100 - `stagingSplitPercentage`) &#42;`cacheSize`**.

异步上传是多线程的，线程数通过使用 `uploadThreads` 参数。

上传完成后，文件将移至主下载缓存。 当暂存缓存大小超过其限制时，会将文件同步上传到DataStore，直到上一次异步上传完成并且暂存缓存中再次有可用空间为止。 通过定期作业（其间隔由配置）将上传的文件从暂存区中删除 `stagingPurgeInterval` 参数。

失败的上传（例如，由于网络中断）将被置于重试队列中，并定期重试。 重试间隔通过使用 `stagingRetryInterval parameter`.

#### 使用Amazon S3配置无二进制复制 {#configuring-binaryless-replication-with-amazon-s}

要使用S3配置无二进制复制，需要执行以下步骤：

1. 安装创作实例和发布实例，并确保它们已正确启动。
1. 通过打开页面转到复制代理设置 *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. 按 **编辑** 中的按钮 **设置** 部分。
1. 更改 **序列化** 键入选项至 **无二进制**.

1. 添加参数&quot; `binaryless`= `true`”在传输URI中。 更改后，URI应类似于以下内容：

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. 重新启动所有创作和发布实例，以使更改生效。

#### 使用S3和MongoDB创建群集 {#creating-a-cluster-using-s-and-mongodb}

1. 使用以下命令解压缩CQ快速启动：

   `java -jar cq-quickstart.jar -unpack`

1. 解压缩AEM后，在安装目录中创建一个文件夹 *crx-quickstart*/*安装*.

1. 在中创建这两个文件 `crx-quickstart` 文件夹：

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*.*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*config*

   创建文件后，根据需要添加配置选项。

1. 按照上面的说明，安装S3数据存储所需的两个捆绑包。
1. 确保已安装MongoDB并且实例为 `mongod` 正在运行。
1. 使用以下命令启动AEM：

   `java -Xmx1024m -jar cq-quickstart.jar -r crx3,crx3mongo`

1. 对第二个AEM实例重复步骤1至4。
1. 启动第二个AEM实例。

#### 配置共享数据存储 {#configuring-a-shared-data-store}

1. 首先，在共享数据存储所需的每个实例上创建数据存储配置文件：

   * 如果您使用 `FileDataStore`，创建一个名为的文件 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 然后将其放入 `<aem-install>/crx-quickstart/install` 文件夹。

   * 如果使用S3作为数据存储，请创建一个名为的文件o `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 在 `<aem-install>/crx-quickstart/install` 文件夹（如上所示）。

1. 修改每个实例上的数据存储配置文件，以指向同一数据存储。 有关更多信息，请参阅 [本文](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. 如果实例是从现有服务器克隆的，则需要删除 `clusterId` 在存储库脱机时使用最新的oak-run工具执行的新实例。 您需要运行的命令是：

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >如果配置了区段节点存储，则需要指定存储库路径。 默认情况下，路径为 `<aem-install-folder>/crx-quickstart/repository/segmentstore.` 如果配置了文档节点存储，您可以使用 [Mongo连接字符串URI](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >可以从以下位置下载Oak-run工具：
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >请注意，根据您在AEM安装中使用的Oak版本，需要使用该工具的不同版本。 在使用工具之前，请查看下面的版本要求列表：
   >
   >
   >
   >    * 对于Oak版本 **1.2.x** 使用Oak运行 **1.2.12或更高版本**
   >    * 对于Oak版本 **比上面更新**，使用与AEM安装的Oak核心匹配的Oak-run版本。


1. 最后，验证配置。 为此，您需要查找由共享它的每个存储库添加到数据存储中的唯一文件。 文件的格式为 `repository-[UUID]`，其中UUID是每个存储库的唯一标识符。

   因此，正确的配置应具有与共享数据存储区的存储库相同数量的唯一文件。

   文件存储方式有所不同，具体取决于数据存储：

   * 对于 `FileDataStore` 这些文件在数据存储文件夹的根路径下创建。
   * 对于 `S3DataStore` 这些文件是在配置的S3存储桶中创建的，位于 `META` 文件夹。

## Azure 数据存储 {#azure-data-store}

可以将AEM配置为将数据存储在Microsoft的Azure存储服务中。 它使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` 用于配置的PID。

为了启用Azure数据存储功能，需要下载并安装包含Azure连接器的功能包。 转到 [Adobe存储库](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) 并从1.6.x版的功能包（例如，com.adobe.granite.oak.azureblobconnector-1.6.3.zip）下载最新版本。

>[!NOTE]
>
>在将AEM与TarMK结合使用时，二进制文件将默认存储在FileDataStore中。 要将TarMK与Azure DataStore结合使用，您需要使用启动AEM `crx3tar-nofds` 运行模式，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下载后，您可以按如下方式安装和配置Azure连接器：

1. 将功能包zip文件的内容提取到临时文件夹。

1. 转到临时文件夹并复制内容 `jcr_root/libs/system/install` 到 `<aem-install>crx-quickstart/install` 文件夹。
1. 如果已将AEM配置为使用Tar或MongoDB存储，请从 `/crx-quickstart/install` 文件夹，然后再继续。 需要删除的文件包括：

   对于MongoMK：

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   对于TarMK：

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回到已提取功能包的临时位置，并复制其内容 `jcr_root/libs/system/config` 到 `<aem-install>/crx-quickstart/install` 文件夹。
1. 编辑配置文件并添加安装程序所需的配置选项。
1. 启动AEM。

配置文件具有以下选项：

* AzureSas=”：在连接器的1.6.3版本中，添加了Azure共享访问签名(SAS)支持。 **如果配置文件中同时存在SAS和存储凭据，则SAS具有优先级。** 有关SAS的更多信息，请参见 [官方文档](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1). 确保“=”字符像“\=”一样转义。

* azureBlobEndpoint=&quot;&quot;： Azure Blob端点。 例如， https://&lt;storage-account>.blob.core.windows.net.
* accessKey=&quot;&quot;：存储帐户名称。 有关Microsoft Azure身份验证凭据的更多详细信息，请参阅 [官方文档](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account).

* secretKey=&quot;&quot;：存储访问密钥。 确保“=”字符像“\=”一样转义。
* container=&quot;&quot;： Microsoft Azure Blob存储容器名称。 容器是一组Blob。 欲知更多详情，请阅读 [官方文档](https://msdn.microsoft.com/en-us/library/dd135715.aspx).
* maxConnections=&quot;：每个操作的并发请求数。 默认值为 1。
* maxErrorRetry=&quot;&quot;：每个请求的重试次数。 默认值为 3。
* socketTimeout=&quot;&quot;：请求所使用的超时间隔（以毫秒为单位）。 默认值为5分钟。

除了上述设置外，还可以配置以下设置：

* path：数据存储的路径。 默认为 `<aem-install>/repository/datastore.`
* RecordLength：应存储在数据存储中的对象的最小大小。 默认值为16KB。
* maxCachedBinarySize：大小小于或等于此大小的二进制文件将存储在内存缓存中。 大小以字节为单位。 默认值为17408 (17 KB)。
* cacheSize：缓存的大小。 该值以字节为单位。 默认值为64GB。
* 密钥：仅在使用无二进制复制进行共享数据存储设置时使用。
* stagingSplitPercentage：配置为用于暂存异步上载的缓存大小的百分比。 默认值为 10。
* uploadThreads：用于异步上载的上载线程数。 默认值为 10。
* stagingPurgeInterval：从暂存缓存中清除已完成上载的时间间隔（以秒为单位）。 默认值为300秒（5分钟）。
* stagingRetryInterval：失败上载的重试间隔（以秒为单位）。 默认值为600秒（10分钟）。

>[!NOTE]
>
>所有设置都应置于引号之间，例如：

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## 数据存储垃圾收集 {#data-store-garbage-collection}

数据存储垃圾收集过程用于删除数据存储中的任何未使用的文件，从而在该过程中释放宝贵的磁盘空间。

您可以通过以下方式运行数据存储垃圾收集：

1. 转到JMX控制台，位于 *https://&lt;serveraddress:port>/system/console/jmx*
1. 正在搜索 **存储库管理。** 找到存储库管理器MBean后，单击它可显示可用选项。
1. 滚动到页面末尾，然后单击 **startDataStoreGC(boolean markOnly)** 链接。
1. 在下面的对话框中，输入 `false` 对于 `markOnly` 参数，然后单击 **调用**：

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >此 `markOnly` 参数表示垃圾回收的清理阶段是否运行。

## 共享数据存储的数据存储垃圾收集 {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>在群集或共享数据存储设置（使用Mongo或Segment Tar）中执行垃圾收集时，日志可能会显示有关无法删除某些blob ID的警告。 发生此情况的原因是，之前垃圾收藏集中删除的blob ID被其他群集或共享节点再次错误地引用，而这些节点没有删除这些ID的相关信息。 因此，执行垃圾收集时，如果尝试删除在上次运行中已删除的ID，它将记录警告。 此行为不会影响性能或功能。

>[!NOTE]
>
>如果您使用共享数据存储设置并且数据存储垃圾收集被禁用，则运行Lucene二进制清理任务可能会突然增加使用的磁盘空间。 要避免出现这种情况，您需要按如下方式在所有创作和发布实例上禁用BlobTracker：
>
>1. 停止AEM实例。
>2. 添加 `blobTrackSnapshotIntervalInSecs=L"0"` 中的参数 `crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` 文件。 此参数需要Oak 1.12.0、1.10.2或更高版本。
>3. 重新启动AEM实例。


使用较新版本的AEM，数据存储垃圾收集也可以在由多个存储库共享的数据存储上运行。 为了能够在共享数据存储上运行数据存储垃圾收集，请执行以下步骤：

1. 确保在共享数据存储的所有存储库实例上禁用为数据存储垃圾收集配置的任何维护任务。
1. 运行中所述的步骤 [二进制垃圾收集](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) 单独打开 **所有** 共享数据存储区的存储库实例。 但是，请确保输入 `true` 对于 `markOnly` 单击调用按钮之前的参数：

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. 在所有实例上完成上述过程后，再次从运行数据存储垃圾收集 **任意** 实例：

   1. 转到JMX控制台，然后选择存储库管理器Mbean。
   1. 单击 **单击startDataStoreGC(boolean markOnly)** 链接。
   1. 在下面的对话框中，输入 `false` 对于 `markOnly` 参数。
   这将整理使用之前使用的标记阶段找到的所有文件，并从数据存储中删除其余未使用的文件。
