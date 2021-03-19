---
title: 在AEM 6中配置节点存储和数据存储
seo-title: 在AEM 6中配置节点存储和数据存储
description: 了解如何配置节点存储和数据存储以及如何执行数据存储垃圾收集。
seo-description: 了解如何配置节点存储和数据存储以及如何执行数据存储垃圾收集。
uuid: 1a58c0ba-1c32-4539-ad0d-0a27c8c4ff5e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: b97482f2-2791-4d14-ae82-388302d9eab3
docset: aem65
legacypath: /deploy/platform/data-store-config
feature: 配置
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3424'
ht-degree: 1%

---


# 在AEM 6{#configuring-node-stores-and-data-stores-in-aem}中配置节点存储和数据存储

## 简介 {#introduction}

在Adobe Experience Manager(AEM)中，二进制数据可以独立于内容节点存储。 二进制数据被存储在数据存储中，而内容节点被存储在节点存储中。

可以使用OSGi配置配置数据存储和节点存储。 每个OSGi配置都使用永久标识符(PID)进行引用。

## 配置步骤{#configuration-steps}

要配置节点存储和数据存储，请执行以下步骤：

1. 将AEM快速启动JAR文件复制到其安装目录。
1. 在安装目录中创建文件夹`crx-quickstart/install`。
1. 首先，通过创建一个配置文件来配置节点存储区，该配置文件的名称是您要在`crx-quickstart/install`目录中使用的节点存储区选项。

   例如，文档节点存储(它是AEM MongoMK实现的基础)使用文件`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`。

1. 编辑文件，并设置配置选项。
1. 使用要使用的数据存储的PID创建配置文件。 编辑文件以设置配置选项。

   >[!NOTE]
   >
   >有关配置选项，请参阅[节点存储配置](#node-store-configurations)和[数据存储配置](#data-store-configurations)。

1. 开始 AEM。

## 节点存储配置{#node-store-configurations}

>[!CAUTION]
>
>Oak的较新版本对OSGi配置文件采用了新的命名方案和格式。 新命名方案要求将配置文件命名为&#x200B;**.config**，并且新格式要求键入值，并且此处记录有[。](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format)
>
>如果您从旧版Oak升级，请确保首先备份`crx-quickstart/install`文件夹。 升级后，将文件夹的内容恢复到升级后的安装，并将配置文件的扩展从&#x200B;**.cfg**&#x200B;修改为&#x200B;**.config**。
>
>如果您正在阅读本文以准备从&#x200B;**AEM 5.x**&#x200B;安装升级，请确保首先查阅[升级](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html)文档。

### 区段节点存储{#segment-node-store}

细分节点存储是Adobe在AEM6中实现TarMK的基础。 它使用`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` PID进行配置。

>[!CAUTION]
>
>段节点存储的PID已从AEM 6的`org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions`更改为AEM 6.3中的`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService`。请确保进行必要的配置调整以反映此更改。

您可以配置以下选项：

* `repository.home`:存储与存储库相关数据的存储库主目录的路径。默认情况下，段文件存储在`crx-quickstart/segmentstore`目录下。

* `tarmk.size`:段的最大大小(MB)。默认最大为256MB。
* `customBlobStore`:指示使用自定义数据存储的布尔值。对于AEM 6.3及更高版本，默认值为true。 在AEM 6.3之前，默认值为false。

以下是示例`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`文件：

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### 文档节点存储{#document-node-store}

文档节点存储是AEM MongoMK实现的基础。 它使用`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID。 以下配置选项可用：

* `mongouri`:连接 [](https://docs.mongodb.org/manual/reference/connection-string/) 到Mongo数据库所需的MongoURI。默认为 `mongodb://localhost:27017`

* `db`:Mongo数据库的名称。默认值为&#x200B;**Oak** ``. However, new AEM 6 installations use **aem-author** ``作为默认数据库名称。

* `cache`:缓存大小(MB)。它分布在DocumentNodeStore中使用的各种缓存中。 默认为 `256`

* `changesSize`:Mongo中用于缓存差异输出的已限制集合的大小(MB)。默认为 `256`

* `customBlobStore`:指示将使用自定义数据存储的布尔值。默认为 `false`.

以下是示例`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`文件：

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## 数据存储配置{#data-store-configurations}

在处理大量二进制文件时，建议使用外部数据存储而不是默认节点存储，以便最大化性能。

例如，如果您的项目需要大量媒体资源，则将这些资源存储在File或S3 Data Store下比直接存储在MongoDB中更快地访问它们。

与MongoDB相比，文件数据存储提供了更好的性能，而且Mongo备份和恢复操作对于大量资源也较慢。

有关不同数据存储和配置的详细信息如下所述。

>[!NOTE]
>
>要启用自定义文档存储，您需要确保在相应的节点存储配置文件（[区段节点存储](/help/sites-deploying/data-store-config.md#segment-node-store)或[节点存储](/help/sites-deploying/data-store-config.md#document-node-store)）中将`customBlobStore`设置为`true`。

### 文件数据存储 {#file-data-store}

这是Jackrabbit 2中存在的[FileDataStore](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html)的实现。 它提供了一种将二进制数据作为普通文件存储在文件系统中的方法。 它使用`org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID。

以下配置选项可用：

* `repository.home`:存储各种存储库相关数据的存储库主目录的路径。默认情况下，二进制文件将存储在`crx-quickstart/repository/datastore`目录下

* `path`:存储文件的目录的路径。如果指定，则它优先于`repository.home`值

* `minRecordLength`:数据存储中存储的文件的最小大小（以字节为单位）。小于此值的二进制内容将内嵌。

>[!NOTE]
>
>使用NAS存储共享文件数据存储时，请确保仅使用高性能设备以避免性能问题。

## Amazon S3数据存储{#amazon-s-data-store}

可以将AEM配置为在Amazon的简单存储服务(S3)中存储数据。 它使用`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` PID进行配置。

要启用S3数据存储功能，需要下载并安装包含S3 Datastore Connector的功能包。 转至[Adobe库](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)，从1.10.x版本的功能包下载最新版本（例如，com.adobe.granite.oak.s3connector-1.10.0.zip）。 此外，您还需要下载并安装[AEM 6.5发行说明](/help/release-notes/sp-release-notes.md)页面中列出的最新AEM Service Pack。

>[!NOTE]
>
>将AEM与TarMK一起使用时，默认情况下，二进制文件将存储在`FileDataStore`中。 要将TarMK与S3数据存储区一起使用，您需要使用`crx3tar-nofds`运行模式开始AEM，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下载后，您可以按如下方式安装和配置S3连接器：

1. 将功能包zip文件的内容解压缩到临时文件夹。

1. 转到临时文件夹并导航到以下位置：

   ```xml
   jcr_root/libs/system/install
   ```

   将上述位置的所有内容复制到`<aem-install>/crx-quickstart/install.`

1. 如果AEM已配置为与Tar或MongoDB存储一起使用，请在继续操作之前从****&lt;aem-install>***/*crx-quickstart*/*install*&#x200B;文件夹中删除任何现有配置文件。 需要删除的文件有：

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回到提取了功能包的临时位置，并复制以下文件夹的内容：

   * `jcr_root/libs/system/config`

   到

   * `<aem-install>/crx-quickstart/install`

   确保仅复制当前配置所需的配置文件。 对于专用数据存储区和共享数据存储区设置，都复制`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`文件。

   >[!NOTE]
   >
   >在群集设置中，逐个对群集的所有节点执行上述步骤。 另外，请确保对所有节点使用相同的S3设置。

1. 编辑文件并添加安装程序所需的配置选项。
1. 开始 AEM。

### 升级到1.10.x S3 Connector {#upgrading-to-a-new-version-of-the-s-connector}的新版本

如果您需要升级到1.10.x S3连接器的新版本（例如，从1.10.0升级到1.10.4），请遵循以下步骤：

1. 停止AEM实例。

1. 导览至AEM安装文件夹中的`<aem-install>/crx-quickstart/install/15`并备份其内容。
1. 备份后，删除`<aem-install>/crx-quickstart/install/15`文件夹中的所有jar文件，以删除旧版S3 Connector及其依赖项，例如：

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >上述文件名仅用于说明。

1. 从[Adobe库](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)下载1.8.x功能包的最新版本。
1. 将内容解压缩到单独的文件夹，然后导航到`jcr_root/libs/system/install/15`。
1. 将jar文件复制到AEM安装文件夹中的&#x200B;**&lt;aem-install>**/crx-quickstart/install/15。
1. 开始AEM并检查连接器功能。

可以使用以下选项来使用配置文件：

* accessKey:AWS访问密钥。
* secretKey:AWS秘密访问密钥。 **注意：** 或者， [IAM](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) 角色可用于身份验证。如果您使用的是IAM角色，则不再需要指定`accessKey`和`secretKey`。

* s3Bucket:存储段名称。
* s3地区：桶区。
* 路径：数据存储的路径。 默认值为&#x200B;**&lt;AEM install folder>/repository/datastore**
* minRecordLength:应存储在数据存储中的对象的最小大小。 最小/默认值为&#x200B;**16KB。**
* maxCachedBinarySize:大小小于或等于此大小的二进制文件将存储在内存缓存中。 大小以字节为单位。 默认值为**17408 **(17 KB)。

* cacheSize:缓存的大小。 该值以字节为单位指定。 默认值为&#x200B;**64GB**。
* 秘密：仅在对共享数据存储设置使用无二进制复制时使用。
* stagingSplitPercentage:配置为用于暂存异步上传的缓存大小的百分比。 默认值为&#x200B;**10**。
* uploadThreads:用于异步上传的上传线程数。 默认值为&#x200B;**10**。
* stagingPurgeInterval:从暂存缓存中清除已完成上载的时间间隔（以秒为单位）。 默认值为&#x200B;**300**&#x200B;秒（5分钟）。
* stagingRetryInterval:失败上载的重试间隔（秒）。 默认值为&#x200B;**600**&#x200B;秒（10分钟）。

### 存储段区域选项{#bucket-region-options}

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
   <td>亚太（悉尼）<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>亚太地区（东京）</td>
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
>`S3DataStore`、`CachingFileDataStore`和`AzureDataStore`的DataStore实现支持本地文件系统缓存。 `CachingFileDataStore`实现在DataStore位于NFS（网络文件系统）上时很有用。


从旧缓存实现（Oak 1.6之前）升级时，本地文件系统缓存目录的结构有所不同。 在旧缓存结构中，下载的文件和上传的文件都直接放在缓存路径下。 新结构将下载和上载分离，并将它们存储在缓存路径下名为`upload`和`download`的两个目录中。 升级过程应是无缝的，任何挂起的上载应计划上载，并且在初始化时，缓存中之前下载的任何文件都将放入缓存中。

您还可以使用oak-run的`datastorecacheupgrade`命令脱机升级缓存。 有关如何执行该命令的详细信息，请查阅[readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md)以获取oak-run模块。

缓存具有大小限制，可使用cacheSize参数进行配置。

**下载**

在从DataStore访问本地缓存之前，将检查本地缓存中所请求文件/blob的记录。 当缓存在缓存中添加文件时超出配置的限制（请参见`cacheSize`参数）时，将逐出某些文件以回收空间。

**异步上传**

缓存支持异步上载到DataStore。 文件将在本地存放在缓存中（在文件系统上），并执行异步作业开始以上传文件。 异步上载的数量受暂存缓存大小的限制。 使用`stagingSplitPercentage`参数配置暂存缓存的大小。 此参数定义用于暂存缓存的缓存大小百分比。 此外，可下载的缓存百分比计算为&#x200B;**(100 - `stagingSplitPercentage`)*`cacheSize`**。

异步上传是多线程的，线程数是使用`uploadThreads`参数配置的。

上载完成后，文件将移至主下载缓存。 当暂存缓存大小超过其限制时，文件将同步上传到DataStore，直到以前的异步上传完成，并且暂存缓存中的空间再次可用。 已上载文件将通过一个周期性作业从暂存区域中删除，该作业的间隔由`stagingPurgeInterval`参数配置。

失败的上载（例如，由于网络中断）被置于重试队列中并定期重试。 使用`stagingRetryInterval parameter`配置重试间隔。

#### 使用Amazon S3 {#configuring-binaryless-replication-with-amazon-s}配置无二进制复制

为了使用S3配置无二进制复制，需要执行以下步骤：

1. 安装作者实例和发布实例，并确保它们正确启动。
1. 打开到&#x200B;*https://localhost:4502/etc/replication/agents.author/publish.html*&#x200B;的页面，转到复制代理设置。
1. 按&#x200B;**设置**&#x200B;部分中的&#x200B;**编辑**&#x200B;按钮。
1. 将&#x200B;**Serialization**&#x200B;类型选项更改为&#x200B;**Binary less**。

1. 在传输URI中添加参数“ `binaryless`= `true`”。 更改后，uri应类似于：

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. 重新启动所有作者和发布实例，使更改生效。

#### 使用S3和MongoDB {#creating-a-cluster-using-s-and-mongodb}创建群集

1. 使用以下命令解压缩CQ快速启动：

   `java -jar cq-quickstart.jar -unpack`

1. 解压缩AEM后，在安装目录&#x200B;*crx-quickstart*/*install*&#x200B;内创建一个文件夹。

1. 在`crx-quickstart`文件夹中创建以下两个文件：

   * *org.apache.jackrabbit.oak.plugins.文档.DocumentNodeStoreService*。*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*。*config*

   创建文件后，根据需要添加配置选项。

1. 按照上面的说明安装S3数据存储所需的两个包。
1. 确保已安装MongoDB，且`mongod`的实例正在运行。
1. 开始 AEM使用以下命令：

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. 对第二个AEM实例重复步骤1至4。
1. 开始第二个AEM实例。

#### 配置共享数据存储{#configuring-a-shared-data-store}

1. 首先，在共享数据存储所需的每个实例上创建数据存储配置文件：

   * 如果您使用`FileDataStore`，请创建名为`org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`的文件，并将其放在`<aem-install>/crx-quickstart/install`文件夹中。

   * 如果使用S3作为数据存储，请在`<aem-install>/crx-quickstart/install`文件夹中创建一个名为`rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`的文件，如上所示。

1. 修改每个实例上的数据存储配置文件以指向同一数据存储。 有关详细信息，请参阅[本文](/help/sites-deploying/data-store-config.md#data-store-configurations)。
1. 如果已从现有服务器克隆了该实例，则需要在存储库脱机时使用最新的oak-run工具删除新实例的`clusterId`。 您需要运行的命令是：

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >如果配置了区段节点存储区，则需要指定存储库路径。 默认情况下，路径为`<aem-install-folder>/crx-quickstart/repository/segmentstore.`。如果配置了文档节点存储，则可以使用[ Mongo连接字符串URI](https://docs.mongodb.org/manual/reference/connection-string/)。

   >[!NOTE]
   >
   >Oak-run工具可从以下位置下载：
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >请注意，需要根据您在AEM安装中使用的Oak版本使用不同版本的工具。 在使用该工具之前，请检查以下版本要求列表:
   >
   >
   >
   >    * 对于Oak版本&#x200B;**1.2.x**，请使用Oak-run **1.2.12或更高版本**
   >    * 对于比上述&#x200B;**版本更新的Oak版本**，请使用与AEM安装的Oak核心相匹配的Oak-run版本。


1. 最后，验证配置。 为此，您需要查找每个共享数据存储库添加到数据存储的唯一文件。 文件的格式为`repository-[UUID]`，其中UUID是每个独立存储库的唯一标识符。

   因此，正确的配置应该具有与共享数据存储的存储库相同的唯一文件。

   根据数据存储区的不同，文件存储方式也有所不同：

   * 对于`FileDataStore`，在数据存储文件夹的根路径下创建文件。
   * 对于`S3DataStore`，文件将在配置的S3存储桶中创建在`META`文件夹下。

## Azure 数据存储 {#azure-data-store}

可以将AEM配置为在Microsoft的Azure存储服务中存储数据。 它使用`org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` PID进行配置。

要启用Azure数据存储功能，需要下载并安装包含Azure连接器的功能包。 转至[Adobe库](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/)，从1.6.x版的功能包下载最新版本（例如，com.adobe.granite.oak.azureblobconnector-1.6.3.zip）。

>[!NOTE]
>
>将AEM与TarMK一起使用时，默认情况下，二进制文件将存储在FileDataStore中。 要将TarMK与Azure DataStore一起使用，您需要使用`crx3tar-nofds`运行模式开始AEM，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下载后，您可以按如下方式安装和配置Azure连接器：

1. 将功能包zip文件的内容解压缩到临时文件夹。

1. 转到临时文件夹，将`jcr_root/libs/system/install`的内容复制到`<aem-install>crx-quickstart/install`文件夹。
1. 如果AEM已配置为使用Tar或MongoDB存储，请在继续操作之前，从`/crx-quickstart/install`文件夹中删除任何现有配置文件。 需要删除的文件有：

   ForMongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   对于TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回到已提取功能包的临时位置，并将`jcr_root/libs/system/config`的内容复制到`<aem-install>/crx-quickstart/install`文件夹。
1. 编辑配置文件并添加安装程序所需的配置选项。
1. 开始 AEM。

可以使用以下选项来使用配置文件：

* azureSas=&quot;&quot;:在连接器的版本1.6.3中，增加了Azure共享访问签名(SAS)支持。 **如果配置文件中同时存在SAS和存储凭据，则SAS具有优先级。** 有关SAS的更多信息，请参阅 [官方文档](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1)。确保“=”字符以“\=”的方式转义。

* azureBlobEndpoint=&quot;&quot;:Azure Blob端点。 例如，https://&lt;存储-account>.blob.core.windows.net。
* accessKey=&quot;&quot;:存储帐户名。 有关Microsoft Azure身份验证凭据的详细信息，请参阅[官方文档](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account)。

* secretKey=&quot;&quot;:存储访问键。 确保“=”字符以“\=”的方式转义。
* 容器=&quot;&quot;:Microsoft Azure Blob存储容器名称。 容器是一组块的组。 有关更多详细信息，请阅读[官方文档](https://msdn.microsoft.com/en-us/library/dd135715.aspx)。
* maxConnections=&quot;&quot;:每个操作并发请求数。 默认值为 1。
* maxErrorRetry=&quot;&quot;:每个请求的重试数。 默认值为 3。
* socketTimeout=&quot;&quot;:用于请求的超时间隔（以毫秒为单位）。 默认值为5分钟。

除上述设置外，还可以配置以下设置：

* 路径：数据存储的路径。 默认为 `<aem-install>/repository/datastore.`
* RecordLength:应存储在数据存储中的对象的最小大小。 默认为16KB。
* maxCachedBinarySize:大小小于或等于此大小的二进制文件将存储在内存缓存中。 大小以字节为单位。 默认为17408(17 KB)。
* cacheSize:缓存的大小。 该值以字节为单位指定。 默认为64GB。
* 秘密：仅在对共享数据存储设置使用无二进制复制时使用。
* stagingSplitPercentage:配置为用于暂存异步上传的缓存大小的百分比。 默认值为 10。
* uploadThreads:用于异步上传的上传线程数。 默认值为 10。
* stagingPurgeInterval:从暂存缓存中清除已完成上载的时间间隔（以秒为单位）。 默认值为300秒（5分钟）。
* stagingRetryInterval:失败上载的重试间隔（秒）。 默认值为600秒（10分钟）。

>[!NOTE]
>
>所有设置都应置于引号之间，例如：

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## 数据存储垃圾收集{#data-store-garbage-collection}

数据存储垃圾收集过程用于删除数据存储中任何未使用的文件，从而释放该过程中有价值的磁盘空间。

可以通过以下方式运行数据存储垃圾收集：

1. 转到位于&#x200B;*https://&lt;serveraddress:port>/system/console/jmx*&#x200B;的JMX控制台
1. 正在搜索&#x200B;**RepositoryManagement。** 找到存储库管理器MBean后，单击它可调出可用选项。
1. 滚动到页面末尾，然后单击&#x200B;**startDataStoreGC(boolean markOnly)**&#x200B;链接。
1. 在以下对话框中，输入`markOnly`参数的`false`，然后单击&#x200B;**调用**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >`markOnly`参数表示垃圾收集的扫描阶段是否将运行。

## 共享数据存储{#data-store-garbage-collection-for-a-shared-data-store}的数据存储垃圾收集

>[!NOTE]
>
>当在群集或共享数据存储设置（使用Mongo或区段Tar）中执行垃圾收集时，日志可能显示有关无法删除某些Blob ID的警告。 发生这种情况的原因是，在以前的垃圾收集中删除的blob ID被其他没有ID删除信息的群集或共享节点再次错误引用。 因此，在执行垃圾收集时，当它尝试删除在上次运行中已删除的ID时，它会记录警告。 此行为不影响性能或功能。

对于较新版本的AEM，还可以在多个存储库共享的数据存储上运行数据存储垃圾收集。 要能够在共享数据存储上运行数据存储垃圾收集，请执行以下步骤：

1. 确保为数据存储垃圾收集配置的所有维护任务在共享数据存储的所有存储库实例上都处于禁用状态。
1. 在共享数据存储的&#x200B;**所有**&#x200B;存储库实例上分别运行[二进制垃圾收集](/help/sites-deploying/data-store-config.md#data-store-garbage-collection)中所述的步骤。 但是，在单击“调用”按钮之前，请务必为`markOnly`参数输入`true`:

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. 在所有实例上完成上述过程后，从实例的&#x200B;**任何**&#x200B;再次运行数据存储垃圾收集：

   1. 转到JMX控制台，并选择“存储库管理器Mbean”。
   1. 单击&#x200B;**单击startDataStoreGC(boolean markOnly)**&#x200B;链接。
   1. 在以下对话框中，再次输入`markOnly`参数的`false`。

   这将整理使用之前使用的标记阶段找到的所有文件，并从数据存储中删除其余未使用的文件。

