---
title: 在AEM 6中配置节点存储和数据存储
description: 了解如何配置节点存储和数据存储，以及如何执行数据存储垃圾收集。
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
exl-id: c1c90d6a-ee5a-487d-9a8a-741b407c8c06
source-git-commit: 4e68a8a8d84d0ffa1d28ab13c196731e58b4cf9a
workflow-type: tm+mt
source-wordcount: '3447'
ht-degree: 1%

---

# 在AEM 6中配置节点存储和数据存储{#configuring-node-stores-and-data-stores-in-aem}

## 简介 {#introduction}

在Adobe Experience Manager(AEM)中，二进制数据可以独立于内容节点进行存储。 二进制数据存储在数据存储中，而内容节点存储在节点存储中。

可使用OSGi配置配置数据存储区和节点存储区。 每个OSGi配置都使用永久标识符(PID)进行引用。

## 配置步骤 {#configuration-steps}

要同时配置节点存储和数据存储，请执行以下步骤：

1. 将AEM快速入门JAR文件复制到其安装目录。
1. 创建文件夹 `crx-quickstart/install` 在安装目录中。
1. 首先，通过创建一个配置文件来配置节点存储，该配置文件的名称是您要在 `crx-quickstart/install` 目录访问Advertising Cloud的帮助。

   例如，文档节点存储(是AEM MongoMK实施的基础)使用文件 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. 编辑文件，并设置配置选项。
1. 使用您要使用的数据存储的PID创建配置文件。 编辑文件以设置配置选项。

   >[!NOTE]
   >
   >请参阅 [节点存储配置](#node-store-configurations) 和 [数据存储配置](#data-store-configurations) ，以了解配置选项。

1. 启动AEM。

## 节点存储配置 {#node-store-configurations}

>[!CAUTION]
>
>较新版本的Oak为OSGi配置文件采用了新的命名方案和格式。 新命名方案要求将配置文件命名为 **.config** 且新格式要求键入值，并且 [此处](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>如果您从旧版Oak升级，请确保备份 `crx-quickstart/install`文件夹。 升级后，将文件夹的内容还原到升级后的安装，并修改 **.cfg** to **.config**.
>
>如果您正在阅读本文以准备从 **AEM 5.x** 安装时，请确保您查阅 [升级](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html) 文档。

### 区段节点存储 {#segment-node-store}

区段节点存储是Adobe在AEM6中实施TarMK的基础。 它使用 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` 用于配置的PID。

>[!CAUTION]
>
>区段节点存储的PID已从 `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` AEM 6到 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` 在AEM 6.3中。确保进行必要的配置调整以反映此更改。

您可以配置以下选项：

* `repository.home`:存储与存储库相关数据的存储库主页的路径。 默认情况下，区段文件存储在 `crx-quickstart/segmentstore` 目录访问Advertising Cloud的帮助。

* `tarmk.size`:区段的最大大小(MB)。 默认最大为256MB。
* `customBlobStore`:布尔值，指示使用自定义数据存储。 对于AEM 6.3及更高版本，默认值为true。 在AEM 6.3之前，默认值为false。

以下示例 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` 文件：

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### 文档节点存储 {#document-node-store}

文档节点存储是AEM MongoMK实施的基础。 它使用 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID。 以下配置选项可用：

* `mongouri`:的 [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) 连接到Mongo数据库时需要。 默认为 `mongodb://localhost:27017`

* `db`:Mongo数据库的名称。 默认值为 **Oak** ``. However, new AEM 6 installations use **aem-author** ``作为默认数据库名称。

* `cache`:高速缓存大小(MB)。 它分布在DocumentNodeStore中使用的各种缓存中。 默认为 `256`

* `changesSize`:Mongo中用于缓存差异输出的封闭集合的大小(MB)。 默认为 `256`

* `customBlobStore`:布尔值，指示将使用自定义数据存储。 默认为 `false`。

以下示例 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` 文件：

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## 数据存储配置 {#data-store-configurations}

在处理大量二进制文件时，建议使用外部数据存储而不是默认的节点存储，以便最大化性能。

例如，如果您的项目需要大量的媒体资产，则在文件或S3数据存储下存储这些资产将比直接在MongoDB中存储更快地访问它们。

与MongoDB相比，文件数据存储提供了更好的性能，而且Mongo备份和还原操作在大量资产的情况下也更慢。

有关不同数据存储和配置的详细信息如下所述。

>[!NOTE]
>
>要启用自定义数据存储，您需要确保 `customBlobStore` 设置为 `true` 在相应的节点存储配置文件([区段节点存储](/help/sites-deploying/data-store-config.md#segment-node-store) 或 [文档节点存储](/help/sites-deploying/data-store-config.md#document-node-store))。

### 文件数据存储 {#file-data-store}

这是 [FileDataStore](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html) 在杰克拉布特2号。 它提供了一种将二进制数据作为普通文件存储在文件系统上的方法。 它使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID。

以下配置选项可用：

* `repository.home`:存储各种存储库相关数据的存储库主页的路径。 默认情况下，二进制文件将存储在 `crx-quickstart/repository/datastore` 目录

* `path`:存储文件的目录的路径。 如果指定，则优先于 `repository.home` 值

* `minRecordLength`:数据存储中存储的文件的最小大小（以字节为单位）。 小于此值的二进制内容将内嵌。

>[!NOTE]
>
>使用NAS存储共享文件数据存储时，请确保仅使用高性能设备以避免性能问题。

## Amazon S3数据存储 {#amazon-s-data-store}

可以将AEM配置为在Amazon的简单存储服务(S3)中存储数据。 它使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 用于配置的PID。

要启用S3数据存储功能，需要下载和安装包含S3数据存储连接器的功能包。 转到 [Adobe存储库](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) 并从1.10.x版本的功能包下载最新版本(例如，com.adobe.granite.oak.s3connector-1.10.0.zip)。 此外，您还需要下载并安装上列出的最新AEM Service Pack [AEM 6.5发行说明](/help/release-notes/release-notes.md) 页面。

>[!NOTE]
>
>将AEM与TarMK结合使用时，默认情况下，二进制文件将存储在 `FileDataStore`. 要将TarMK与S3数据存储结合使用，您需要使用 `crx3tar-nofds` 运行模式，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下载后，您可以按如下方式安装和配置S3连接器：

1. 将功能包zip文件的内容解压缩到临时文件夹中。

1. 转到临时文件夹，然后导航到以下位置：

   ```xml
   jcr_root/libs/system/install
   ```

   将上述位置的所有内容复制到 `<aem-install>/crx-quickstart/install.`

1. 如果AEM已配置为与Tar或MongoDB存储一起使用，请从***&lt;aem-install>***/*crx-quickstart*/*安装* 文件夹。 需要删除的文件包括：

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回到已提取功能包的临时位置，并复制以下文件夹的内容：

   * `jcr_root/libs/system/config`

   到

   * `<aem-install>/crx-quickstart/install`

   确保仅复制当前配置所需的配置文件。 对于专用数据存储和共享数据存储设置，请复制 `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 文件。

   >[!NOTE]
   >
   >在群集设置中，逐个对群集的所有节点执行上述步骤。 此外，请确保对所有节点使用相同的S3设置。

1. 编辑文件并添加设置所需的配置选项。
1. 启动AEM。

### 升级到1.10.x S3 Connector的新版本 {#upgrading-to-a-new-version-of-the-s-connector}

如果您需要升级到新版本的1.10.x S3连接器(例如，从1.10.0到1.10.4)，请执行以下步骤：

1. 停止AEM实例。

1. 导航到 `<aem-install>/crx-quickstart/install/15` ，并备份其内容。
1. 备份后，通过删除 `<aem-install>/crx-quickstart/install/15` 文件夹，例如：

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >上述文件名仅用于说明目的。

1. 从 [Adobe存储库](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. 将内容解压缩到单独的文件夹，然后导航到 `jcr_root/libs/system/install/15`.
1. 将jar文件复制到 **&lt;aem-install>**/crx-quickstart/install/15(位于AEM安装文件夹中)。
1. 启动AEM并检查连接器功能。

您可以使用以下选项来使用配置文件：

* accessKey:AWS访问密钥。
* secretKey:AWS密钥访问密钥。 **注意：** 当 `accessKey` 或 `secretKey` 未指定，则 [IAM角色](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) 用于身份验证。
* s3存储段：存储段名称。
* s3地区：桶区域。
* 路径：数据存储的路径。 默认值为 **&lt;aem install=&quot;&quot; folder=&quot;&quot;>/repository/datastore**
* minRecordLength:应存储在数据存储中的对象的最小大小。 最小值/默认值为 **16KB。**
* maxCachedBinarySize:大小小于或等于此大小的二进制文件将存储在内存缓存中。 大小以字节为单位。 默认为**17408 **(17 KB)。

* cacheSize:缓存的大小。 值以字节为单位指定。 默认值为 **64GB**.
* 密码：仅在对共享数据存储设置使用无二进制复制时使用。
* stagingSplitPercentage:配置为用于暂存异步上传的缓存大小的百分比。 默认值为 **10**.
* uploadThreads:用于异步上传的上传线程数。 默认值为 **10**.
* stagingPurgeInterval:从暂存缓存中清除已完成上载的间隔，以秒为单位。 默认值为 **300** 秒（5分钟）。
* stagingRetryInterval:上传失败的重试间隔，以秒为单位。 默认值为 **600** 秒（10分钟）。

### 存储段区域选项 {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>美国标准</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>美国西部</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>美国西部（北加利福尼亚）</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>欧盟（爱尔兰）<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>亚太（新加坡）<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>亚太地区（悉尼）<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>亚太（东京）</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>南美洲（圣保罗）<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>

**数据存储缓存**

>[!NOTE]
>
>的DataStore实施 `S3DataStore`, `CachingFileDataStore` 和 `AzureDataStore` 支持本地文件系统缓存。 的 `CachingFileDataStore` 当数据存储在NFS（网络文件系统）上时，实施非常有用。

从旧版缓存实施（Oak 1.6之前）升级时，本地文件系统缓存目录的结构存在差异。 在旧缓存结构中，已下载和已上传的文件都直接放在缓存路径下。 新结构将下载和上传分开，并将它们存储在两个名为 `upload` 和 `download` 在缓存路径下。 升级过程应该是无缝的，任何挂起的上传都应计划上传，而任何以前下载的缓存文件都将在初始化时放入缓存中。

您还可以使用 `datastorecacheupgrade` oak-run命令。 有关如何执行命令的详细信息，请检查 [readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) 用于oak-run模块。

缓存具有大小限制，可使用cacheSize参数对其进行配置。

**下载**

在从DataStore访问本地缓存之前，将检查所请求文件/blob的记录。 当缓存超出配置的限制时(请参阅 `cacheSize` 参数)时，会逐出某些文件以回收空间。

**异步上传**

缓存支持异步上传到DataStore。 文件将在本地缓存中（在文件系统上）存放，异步作业开始上传文件。 异步上传的数量受暂存缓存大小的限制。 暂存缓存的大小通过使用 `stagingSplitPercentage` 参数。 此参数定义用于暂存缓存的缓存大小百分比。 此外，可下载的缓存百分比计算为 **(100 - `stagingSplitPercentage`) &#42;`cacheSize`**.

异步上传是多线程的，且线程数量是使用 `uploadThreads` 参数。

上传完成后，文件将移至主下载缓存。 当暂存缓存大小超过其限制时，将同步将文件上传到DataStore，直到上一个异步上传完成，并且暂存缓存中的空间再次可用。 已上传的文件将由周期性作业从暂存区域中删除，该作业的间隔由 `stagingPurgeInterval` 参数。

失败的上传（例如，由于网络中断）将被置于重试队列中并定期重试。 重试间隔通过使用 `stagingRetryInterval parameter`.

#### 使用Amazon S3配置无二进制复制 {#configuring-binaryless-replication-with-amazon-s}

要使用S3配置无二进制复制，需要执行以下步骤：

1. 安装创作实例和发布实例，并确保正确启动它们。
1. 通过打开 *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. 按 **编辑** 按钮 **设置** 中。
1. 更改 **序列化** 将选项类型设为 **二进制减**.

1. 添加参数“ `binaryless`= `true`&quot; 更改后，URI应类似于以下内容：

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. 重新启动所有创作和发布实例，以使更改生效。

#### 使用S3和MongoDB创建群集 {#creating-a-cluster-using-s-and-mongodb}

1. 使用以下命令解包CQ快速启动：

   `java -jar cq-quickstart.jar -unpack`

1. 解压缩AEM后，在安装目录内创建一个文件夹 *crx-quickstart*/*安装*.

1. 在 `crx-quickstart` 文件夹：

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*.*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*配置*

   创建文件后，根据需要添加配置选项。

1. 按照上面所述，安装S3数据存储所需的两个包。
1. 确保已安装MongoDB，且实例为 `mongod` 正在运行。
1. 使用以下命令启动AEM:

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. 对第二个AEM实例重复步骤1至4。
1. 启动第二个AEM实例。

#### 配置共享数据存储 {#configuring-a-shared-data-store}

1. 首先，在共享数据存储所需的每个实例上创建数据存储配置文件：

   * 如果您使用 `FileDataStore`，创建名为的文件 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 然后放进去 `<aem-install>/crx-quickstart/install` 文件夹。

   * 如果使用S3作为数据存储，请创建名为 `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 在 `<aem-install>/crx-quickstart/install` 文件夹。

1. 修改每个实例上的数据存储配置文件以指向同一数据存储。 有关更多信息，请参阅 [本文](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. 如果实例已从现有服务器克隆，则需要删除 `clusterId` 在存储库脱机时，使用最新的oak-run工具对新实例进行删除。 您需要运行的命令是：

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >如果配置了区段节点存储，则需要指定存储库路径。 默认情况下，路径为 `<aem-install-folder>/crx-quickstart/repository/segmentstore.` 如果配置了文档节点存储，则可以使用 [Mongo连接字符串URI](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >可以从以下位置下载Oak-run工具：
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >请注意，需要根据您在AEM安装中使用的Oak版本来使用该工具的不同版本。 在使用该工具之前，请查看下面的版本要求列表：
   >
   >
   >
   >    * 对于Oak版本 **1.2.x** 使用Oak-run **1.2.12或更高版本**
   >    * 对于Oak版本 **比上面更新**，请使用与AEM安装的Oak核心相匹配的Oak-run版本。


1. 最后，验证配置。 为此，您需要查找每个共享该文件的存储库添加到数据存储的唯一文件。 文件的格式为 `repository-[UUID]`，其中UUID是每个单独存储库的唯一标识符。

   因此，正确的配置应具有与共享数据存储的存储库相同数量的唯一文件。

   文件的存储方式各不相同，具体取决于数据存储：

   * 对于 `FileDataStore` 文件在数据存储文件夹的根路径下创建。
   * 对于 `S3DataStore` 文件在配置的S3存储段下创建 `META` 文件夹。

## Azure 数据存储 {#azure-data-store}

可以将AEM配置为在Microsoft的Azure存储服务中存储数据。 它使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` 用于配置的PID。

要启用Azure数据存储功能，需要下载并安装包含Azure连接器的功能包。 转到 [Adobe存储库](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) 并从1.6.x版本的功能包下载最新版本（例如，com.adobe.granite.oak.azureblobconnector-1.6.3.zip）。

>[!NOTE]
>
>将AEM与TarMK结合使用时，默认情况下，二进制文件将存储在FileDataStore中。 要将TarMK与Azure DataStore结合使用，您需要使用 `crx3tar-nofds` 运行模式，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下载后，您可以按如下方式安装和配置Azure连接器：

1. 将功能包zip文件的内容解压缩到临时文件夹中。

1. 转到临时文件夹，并复制 `jcr_root/libs/system/install` 到 `<aem-install>crx-quickstart/install` 文件夹。
1. 如果AEM已配置为与Tar或MongoDB存储一起使用，请从 `/crx-quickstart/install` 文件夹。 需要删除的文件包括：

   ForMongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   对于TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回到已提取功能包的临时位置，并复制 `jcr_root/libs/system/config` 到 `<aem-install>/crx-quickstart/install` 文件夹。
1. 编辑配置文件并添加安装程序所需的配置选项。
1. 启动AEM。

您可以使用以下选项来使用配置文件：

* azureSas=&quot;&quot;:在连接器的1.6.3版中，添加了Azure共享访问签名(SAS)支持。 **如果配置文件中同时存在SAS和存储凭据，则SAS具有优先级。** 有关SAS的详细信息，请参阅 [官方文档](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1). 确保对“=”字符进行转义，如“\=”。

* azureBlobEndpoint=&quot;&quot;:Azure Blob端点。 例如， https://&lt;storage-account>.blob.core.windows.net 。
* accessKey=&quot;&quot;:存储帐户名称。 有关Microsoft Azure身份验证凭据的更多详细信息，请参阅 [官方文档](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account).

* secretKey=&quot;&quot;:存储访问密钥。 确保对“=”字符进行转义，如“\=”。
* container=&quot;&quot;:Microsoft Azureblob存储容器名称。 容器是一组Blob的组。 有关更多详细信息，请阅读 [官方文档](https://msdn.microsoft.com/en-us/library/dd135715.aspx).
* maxConnections=&quot;&quot;:每个操作并发请求数。 默认值为 1。
* maxErrorRetry=&quot;&quot;:每个请求的重试次数。 默认值为 3。
* socketTimeout=&quot;&quot;:请求使用的超时间隔（以毫秒为单位）。 默认值为5分钟。

除了上述设置外，还可以配置以下设置：

* 路径：数据存储的路径。 默认为 `<aem-install>/repository/datastore.`
* RecordLength:应存储在数据存储中的对象的最小大小。 默认为16KB。
* maxCachedBinarySize:大小小于或等于此大小的二进制文件将存储在内存缓存中。 大小以字节为单位。 默认为17408(17 KB)。
* cacheSize:缓存的大小。 值以字节为单位指定。 默认为64 GB。
* 密码：仅在对共享数据存储设置使用无二进制复制时使用。
* stagingSplitPercentage:配置为用于暂存异步上传的缓存大小的百分比。 默认值为 10。
* uploadThreads:用于异步上传的上传线程数。 默认值为 10。
* stagingPurgeInterval:从暂存缓存中清除已完成上载的间隔，以秒为单位。 默认值为300秒（5分钟）。
* stagingRetryInterval:上传失败的重试间隔，以秒为单位。 默认值为600秒（10分钟）。

>[!NOTE]
>
>所有设置都应带引号，例如：

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## 数据存储垃圾收集 {#data-store-garbage-collection}

数据存储垃圾收集过程用于删除数据存储中任何未使用的文件，从而释放该过程中有价值的磁盘空间。

您可以通过以下方式运行数据存储垃圾收集：

1. 转到位于 *https://&lt;serveraddress:port>/system/console/jmx*
1. 搜索 **存储库管理。** 找到存储库管理器MBean后，单击它可显示可用选项。
1. 滚动到页面的结尾，然后单击 **startDataStoreGC(boolean markOnly)** 链接。
1. 在以下对话框中，输入 `false` 对于 `markOnly` 参数，然后单击 **调用**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >的 `markOnly` paramater表示垃圾收集的扫描阶段是否将运行。

## 共享数据存储的数据存储垃圾收集 {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>在群集或共享数据存储设置（具有Mongo或Tar区段）中执行垃圾收集时，日志可能会显示有关无法删除某些Blob ID的警告。 之所以会出现这种情况，是因为之前垃圾收集中删除的Blob ID被没有ID删除信息的其他群集或共享节点再次错误地引用。 因此，在执行垃圾收集时，当垃圾收集尝试删除在上次运行中已删除的ID时，它会记录一则警告。 此行为不会影响性能或功能。

>[!NOTE]
> 如果您使用共享数据存储设置，并且数据存储垃圾收集被禁用，则运行Lucene Binary清理任务可能会突然增加所使用的磁盘空间。 要避免这种情况，您需要在所有创作实例和发布实例上禁用BlobTracker，如下所示：
>
> 1. 停止AEM实例。
> 2. 添加 `blobTrackSnapshotIntervalInSecs=L"0"` 参数 `crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` 文件。 此参数需要Oak 1.12.0、1.10.2或更高版本。
> 3. 重新启动AEM实例。


使用较新版本的AEM，还可以在由多个存储库共享的数据存储上运行数据存储垃圾收集。 为了能够在共享数据存储上运行数据存储垃圾收集，请执行以下步骤：

1. 确保在共享数据存储的所有存储库实例上禁用为数据存储垃圾收集配置的任何维护任务。
1. 运行 [二进制垃圾收集](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) 逐个 **全部** 共享数据存储的存储库实例。 但是，请确保输入 `true` 对于 `markOnly` 参数：

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. 在所有实例上完成上述过程后，再次从 **any** 实例数：

   1. 转到JMX控制台并选择“存储库管理器”Mbean。
   1. 单击 **单击startDataStoreGC(boolean markOnly)** 链接。
   1. 在以下对话框中，输入 `false` 对于 `markOnly` 参数。
   这将整理使用之前使用的标记阶段找到的所有文件，并从数据存储中删除未使用的其余文件。
