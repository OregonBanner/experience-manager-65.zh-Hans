---
title: 执行就地升级
description: 了解如何执行就地升级。
topic-tags: upgrading
feature: Upgrading
exl-id: aef6ef00-993c-4252-b0ad-ddc4917beaf7
source-git-commit: c0574b50f3504a4792405d6fcd8aa3a2e8e6c686
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---

# 执行就地升级{#performing-an-in-place-upgrade}

>[!NOTE]
>
>此页概述了AEM 6.5的升级过程。如果您有一个部署到应用程序服务器的安装，请参见 [应用程序服务器安装的升级步骤](/help/sites-deploying/app-server-upgrade.md).

## 升级前步骤 {#pre-upgrade-steps}

在执行升级之前，必须完成几个步骤。 参见 [升级代码和自定义项](/help/sites-deploying/upgrading-code-and-customizations.md) 和 [升级前维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 了解更多信息。 此外，请确保您的系统符合新版AEM的要求。 请参阅模式检测器如何帮助您估计升级的复杂性，并参阅的升级范围和要求部分 [规划升级](/help/sites-deploying/upgrade-planning.md) 了解更多信息。

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 迁移先决条件 {#migration-prerequisites}

* **最低必需的Java版本：** 迁移工具仅适用于Java版本7及更高版本。 请注意，对于AEM 6.3及更高版本，Oracle的JRE 8和IBM的JRE 7和8是唯一受支持的版本。

* **已升级的实例：** 如果您从某个版本升级 **早于5.6**，确保您已按照6.0版升级文档中所述的步骤执行了到AEM 6.0的就地升级。

## 准备AEM快速入门jar文件 {#prep-quickstart-file}

1. 如果实例正在运行，请停止该实例。

1. 下载新的AEM jar文件，并使用它来替换 `crx-quickstart` 文件夹。

1. 通过运行以下命令来解压缩新的快速入门jar：

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## 内容存储库迁移 {#content-repository-migration}

如果从AEM 6.3升级，则不需要此迁移。对于6.3之前的版本，Adobe提供了一个工具，可用于将存储库迁移到AEM 6.3中存在的Oak Segment Tar的新版本。它是作为快速入门程序包的一部分提供的，并且对于任何将使用TarMK的升级都是强制性的。 升级使用MongoMK的环境不需要迁移存储库。 有关新的Segment Tar格式的优势的更多信息，请参阅 [迁移到Oak区段Tar常见问题解答](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

使用标准AEM快速入门jar文件执行实际迁移，并使用新的 `-x crx2oak` 选项，用于执行crx2oak工具以简化升级并使其更加稳健。

>[!NOTE]
>
>如果您使用CRX2Oak快速入门扩展执行TarMK存储库内容迁移，则可以删除 **samplecontent** 通过将以下内容添加到迁移命令行来运行模式：
>
>* `--promote-runmode nosamplecontent`
>


要确定应运行的命令，请使用以下命令：

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

位置 `<<YOUR_PROFILE>>` 和 `<<ADDITIONAL_FLAGS>>` 将被替换为下表中列出的配置文件和标记：

<table>
 <tbody>
  <tr>
   <td><strong>源存储库</strong></td>
   <td><strong>目标存储库</strong></td>
   <td><strong>配置文件</strong></td>
   <td><strong>其他标志</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2或TarMK，带 <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>请参阅下面的疑难解答部分</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK或crx2，带 <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>请参阅下面的疑难解答部分</td>
  </tr>
  <tr>
   <td>不含数据存储的TarMK</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>无需迁移</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**其中：**

* `mongo-host` 是MongoDB服务器IP（例如，127.0.0.1）

* `mongo-port` 是MongoDB服务器端口(例如：27017)

* `mongo-database-name` 表示数据库的名称（例如：aem-author）

**对于以下情况，您可能还需要其他开关：**

* 如果您是在未正确处理Java内存映射的Windows系统上执行升级，请添加 `--disable-mmap` 参数到命令。

有关使用crx2oak工具的其他说明，请参阅使用 [CRX2Oak迁移工具](/help/sites-deploying/using-crx2oak.md). 如果需要，可以手动升级crx2oak助手JAR，方法是在解压缩快速启动后将其手动替换为较新版本。 它在AEM安装文件夹中的位置为： `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. 可以从Adobe存储库下载最新版本的CRX2Oak迁移工具，其网址为： [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

如果迁移成功完成，则该工具将退出，退出代码为零。 此外，检查以下位置中是否存在WARN和ERROR消息： `upgrade.log` 文件，位于 `crx-quickstart/logs` AEM ，因为这些错误可能表示迁移期间发生了非致命错误。

检查下方的配置文件 `crx-quickstart/install` 文件夹。 如果需要进行迁移，则将更新这些内容以反映目标存储库。

**关于数据存储的注释：**

While `FileDataStore` 是AEM 6.3安装的新默认值，不需要使用外部数据存储。 虽然建议使用外部数据存储区作为生产部署的最佳实践，但它不是升级的先决条件。 由于升级AEM时已存在的复杂性，我们建议在不执行数据存储迁移的情况下执行升级。 如果需要，可以随后单独执行数据存储迁移。

## 迁移问题疑难解答 {#troubleshooting-migration-issues}

如果您从6.3升级，请跳过此部分。虽然提供的crx2oak配置文件应满足大多数客户的需求，但有时还需要其他参数。 如果您在迁移期间遇到错误，则环境的某些方面可能需要提供其他配置选项。 如果出现这种情况，您可能会遇到以下错误：

**将不会复制检查点，因为未指定外部数据存储。 这将导致在第一次启动时重新索引整个存储库。 使用 — skip-checkpoints强制迁移，或参阅https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration以了解更多信息。**

出于某种原因，迁移过程需要访问数据存储中的二进制文件，并且无法找到它。 要指定数据存储配置，请在 `<<ADDITIONAL_FLAGS>>` 迁移命令的一部分：

**对于S3数据存储：**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

位置 `/path/to/SharedS3DataStore.config` 表示S3数据存储配置文件的路径，并且 `/path/to/datastore` 表示到S3数据存储区的路径。

**对于文件数据存储：**

```shell
--src-datastore=/path/to/datastore
```

位置 `/path/to/datastore` 表示文件数据存储的路径。

## 执行升级 {#performing-the-upgrade}

**如果使用S3：**

1. 删除下方的所有jar `crx-quickstart/install` 与S3连接器的早期版本相关联。

1. 从下载1.10.x S3连接器的最新版本 [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. 将包提取到临时文件夹并复制其内容 `jcr_root/libs/system/install` 到 `crx-quickstart/install` 文件夹。

### 确定正确的升级启动命令 {#determining-the-correct-upgrade-start-command}

要执行升级，必须使用jar文件启动AEM以调出实例。 要升级到6.5，另请参阅以下内容重构和迁移选项： [延迟内容迁移](/help/sites-deploying/lazy-content-migration.md) 使用upgrade命令进行选择。

>[!IMPORTANT]
>
>如果您运行OracleJava 11（或8个以上的Java的常规版本），则启动AEM时需要在命令行中添加其他开关。 有关更多信息，请参阅 [Java 11注意事项](/help/sites-deploying/custom-standalone-install.md#java-considerations).

请注意，从启动脚本启动AEM将不会启动升级。 大多数客户都使用启动脚本启动AEM，并自定义了此启动脚本，以包括用于环境配置（如内存设置、安全证书等）的交换机。 因此，我们建议按照以下步骤来确定正确的升级命令：

1. 在正在运行的AEM实例上，从命令行执行以下命令：

   ```shell
   ps -ef | grep java
   ```

1. 查找AEM进程。 它看上去将类似于：

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 通过替换现有jar的路径来修改命令( `crx-quickstart/app/aem-quickstart*.jar` 在本例中)与作为 `crx-quickstart` 文件夹。 以我们先前的命令为例，我们的命令是：

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   这将确保所有正确的内存设置、自定义运行模式和其他环境参数都适用于升级。 升级完成后，可从启动脚本启动实例，以便将来启动。

## 部署已升级的代码库 {#deploy-upgraded-codebase}

就地升级过程完成后，应部署更新的代码库。 有关更新代码库以使其在目标版本的AEM中正常运行的步骤，请参阅 [“升级代码和定制”页](/help/sites-deploying/upgrading-code-and-customizations.md).

## 执行升级后检查和故障排除 {#perform-post-upgrade-check-troubleshooting}

参见 [升级后检查和故障排除](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
