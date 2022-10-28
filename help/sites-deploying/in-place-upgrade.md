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
>本页概述了AEM 6.5的升级过程。如果您的安装已部署到应用程序服务器，请参阅 [应用程序服务器安装的升级步骤](/help/sites-deploying/app-server-upgrade.md).

## 升级前步骤 {#pre-upgrade-steps}

在执行升级之前，必须完成几个步骤。 请参阅 [升级代码和自定义](/help/sites-deploying/upgrading-code-and-customizations.md) 和 [升级前维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 以了解更多信息。 此外，请确保您的系统满足新版AEM的要求。 请参阅模式检测器如何帮助您评估升级的复杂性，另请参阅 [规划升级](/help/sites-deploying/upgrade-planning.md) 以了解更多信息。

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 迁移先决条件 {#migration-prerequisites}

* **所需的最低Java版本：** 迁移工具仅适用于Java版本7及更高版本。 请注意，对于AEM 6.3及更高版本，Oracle的JRE 8和IBM的JRE 7和8是唯一受支持的版本。

* **已升级实例：** 如果您从版本升级 **大于5.6**，请确保按照升级文档6.0版中所述的过程，就地升级到AEM 6.0。

## 准备AEM快速入门Jar文件 {#prep-quickstart-file}

1. 如果实例正在运行，请停止该实例。

1. 下载新的AEM jar文件，然后使用它替换 `crx-quickstart` 文件夹。

1. 通过运行以下命令来解包新的快速入门Jar:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## 内容存储库迁移 {#content-repository-migration}

如果您从AEM 6.3升级，则无需进行此迁移。对于低于6.3的版本，Adobe提供了一个工具，可用于将存储库迁移到AEM 6.3中存在的Oak Segment Tar的新版本。该工具作为快速启动包的一部分提供，对于将使用TarMK的任何升级而言，是强制性的。 使用MongoMK的环境的升级不需要存储库迁移。 有关新区段焦油格式的好处的更多信息，请参阅 [迁移到Oak区段Tar常见问题解答](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

实际迁移使用标准AEM快速入门Jar文件执行，该文件使用新 `-x crx2oak` 选项，可执行crx2oak工具以简化升级并使其更加稳健。

>[!NOTE]
>
>如果您使用CRX2Oak快速入门扩展执行TarMK存储库内容迁移，则可以删除 **samplecontent** 运行模式，方法是将以下内容添加到迁移命令行：
>
>* `--promote-runmode nosamplecontent`
>


要确定应运行的命令，请使用以下命令：

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

其中 `<<YOUR_PROFILE>>` 和 `<<ADDITIONAL_FLAGS>>` 将替换为下表中列出的配置文件和标记：

<table>
 <tbody>
  <tr>
   <td><strong>源存储库</strong></td>
   <td><strong>目标存储库</strong></td>
   <td><strong>配置文件</strong></td>
   <td><strong>其他标记</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2或TarMK与 <code>FileDataStore</code></td>
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
   <td>没有数据存储的TarMK</td>
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

* `mongo-database-name` 表示数据库的名称(例如：aem-author)

**在以下情况下，您可能还需要其他交换机：**

* 如果您在未正确处理Java内存映射的Windows系统上执行升级，请添加 `--disable-mmap` 参数。

有关使用crx2oak工具的其他说明，请参阅使用 [CRX2Oak迁移工具](/help/sites-deploying/using-crx2oak.md). 如果需要，可以手动升级crx2oak帮助程序JAR，方法是在解压缩快速启动程序后将其手动替换为较新版本。 它在AEM安装文件夹中的位置是： `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. 可以从Adobe存储库下载最新版本的CRX2Oak迁移工具，网址为： [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

如果迁移成功完成，则该工具将退出，退出代码为0。 此外，在 `upgrade.log` 文件，位于 `crx-quickstart/logs` 在AEM安装目录中，因为这些错误可能指示迁移期间发生的非致命错误。

检查下方的配置文件 `crx-quickstart/install` 文件夹。 如果需要迁移，将更新这些库以反映目标存储库。

**关于数据存储的说明：**

While `FileDataStore` 是AEM 6.3安装的新默认设置，无需使用外部数据存储。 虽然建议将外部数据存储用作生产部署的最佳实践，但升级并非先决条件。 由于升级AEM中已存在复杂性，我们建议在不执行数据存储迁移的情况下执行升级。 如果需要，可以在之后作为单独的工作执行数据存储迁移。

## 迁移问题疑难解答 {#troubleshooting-migration-issues}

如果您从6.3升级，请跳过此部分。尽管提供的crx2oak配置文件应满足大多数客户的需求，但有时需要其他参数。 如果您在迁移期间遇到错误，则环境的某些方面可能需要提供其他配置选项。 如果是，您可能会遇到以下错误：

**检查点将不会复制，因为未指定外部数据存储。 这将导致在首次启动时重新编制完整存储库索引。 使用 — skip-checkpoints强制迁移，或访问https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration以了解更多信息。**

由于某些原因，迁移过程需要访问数据存储中的二进制文件，但无法找到它。 要指定数据存储配置，请在 `<<ADDITIONAL_FLAGS>>` 迁移命令的一部分：

**对于S3数据存储：**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

其中 `/path/to/SharedS3DataStore.config` 表示S3数据存储配置文件的路径，并 `/path/to/datastore` 表示S3数据存储的路径。

**对于文件数据存储：**

```shell
--src-datastore=/path/to/datastore
```

其中 `/path/to/datastore` 表示文件数据存储的路径。

## 执行升级 {#performing-the-upgrade}

**如果使用S3:**

1. 删除下方的任何jar `crx-quickstart/install` 与S3连接器的早期版本关联。

1. 从下载最新版本的1.10.x S3连接器 [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. 将包解压缩到临时文件夹，并复制 `jcr_root/libs/system/install` 到 `crx-quickstart/install` 文件夹。

### 确定正确的升级开始命令 {#determining-the-correct-upgrade-start-command}

要执行升级，请务必使用jar文件启动AEM以调出实例。 要升级到6.5，另请参阅 [延迟内容迁移](/help/sites-deploying/lazy-content-migration.md) 使用升级命令可进行选择。

>[!IMPORTANT]
>
>如果您运行的是OracleJava 11（或Java的通常版本高于8），则启动AEM时，需要向命令行中添加其他开关。 有关更多信息，请参阅 [Java 11注意事项](/help/sites-deploying/custom-standalone-install.md#java-considerations).

请注意，从开始脚本启动AEM将不会开始升级。 大多数客户都使用开始脚本来启动AEM，并且已自定义此开始脚本，以包含用于环境配置（如内存设置、安全证书等）的交换机。 因此，我们建议遵循以下过程来确定正确的升级命令：

1. 在运行的AEM实例上，从命令行执行以下操作：

   ```shell
   ps -ef | grep java
   ```

1. 查找AEM流程。 它看起来像：

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 通过替换现有jar的路径( `crx-quickstart/app/aem-quickstart*.jar` 在本例中)，新jar是 `crx-quickstart` 文件夹。 以我们以前的命令为例，我们的命令将为：

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   这将确保为升级应用所有正确的内存设置、自定义运行模式和其他环境参数。 升级完成后，可以从将来启动的启动脚本中启动实例。

## 部署升级的代码库 {#deploy-upgraded-codebase}

完成就地升级过程后，应部署更新的代码库。 有关更新代码库以在AEM的目标版本中工作的步骤，请参阅 [“升级代码和自定义”页面](/help/sites-deploying/upgrading-code-and-customizations.md).

## 执行升级后检查和疑难解答 {#perform-post-upgrade-check-troubleshooting}

请参阅 [升级后检查和疑难解答](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
