---
title: 执行就地升级
seo-title: 执行就地升级
description: 了解如何执行就地升级。
seo-description: 了解如何执行就地升级。
uuid: 478cb9db-1ea8-4bdb-b333-411dcbf2d927
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: fcb17227-ff1f-4b47-ae94-6b7f60923876
docset: aem65
feature: 升级
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 0%

---


# 执行就地升级{#performing-an-in-place-upgrade}

>[!NOTE]
>
>本页概述了AEM 6.5的升级过程。如果您有部署到应用程序服务器的安装，请参阅[应用程序服务器安装的升级步骤](/help/sites-deploying/app-server-upgrade.md)。

## 预升级步骤{#pre-upgrade-steps}

在执行升级之前，必须完成几个步骤。 有关详细信息，请参阅[升级代码和自定义](/help/sites-deploying/upgrading-code-and-customizations.md)和[预升级维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。 此外，请确保您的系统满足新版AEM的要求。 了解Pattern Detector如何帮助您评估升级的复杂性，另请参阅[规划升级](/help/sites-deploying/upgrade-planning.md)的“升级范围和要求”部分以了解更多信息。

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 迁移先决条件{#migration-prerequisites}

* **最低要求的Java版** 本：迁移工具仅适用于Java版本7及更高版本。请注意，对于AEM 6.3及更高版本，Oracle的JRE 8和IBM的JRE 7和8是唯一支持的版本。

* **升级实** 例：如果您是从5.6 **以前的版本升级**，请确保您按照升级文档6.0版中描述的过程执行了AEM 6.0的就地升级。

## 准备AEM Quickstart jar文件{#prep-quickstart-file}

1. 如果实例正在运行，则停止该实例。

1. 下载新的AEM jar文件，然后使用它替换`crx-quickstart`文件夹外的旧文件。

1. 通过运行以下命令来解压缩新快速启动程序jar:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## 内容存储库迁移{#content-repository-migration}

如果您从AEM 6.3升级，则不需要进行此迁移。对于6.3以前的版本，Adobe提供了一个工具，可用于将存储库迁移到AEM 6.3中存在的Oak Segment Tar的新版本。它作为快速启动包的一部分提供，对于将使用TarMK的任何升级都是必需的。 使用MongoMK的环境的升级不需要存储库迁移。 有关新的“区段Tar”格式的好处的更多信息，请参阅[迁移到Oak区段Tar常见问题解答](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)。

实际迁移是使用标准的AEM快速启动jar文件执行的，该文件使用新的`-x crx2oak`选项执行crx2oak工具，以简化升级并使其更加健壮。

>[!NOTE]
>
>如果您使用CRX2Oak Quickstart扩展执行TarMK存储库内容迁移，则可以通过向迁移命令行添加以下内容来删除&#x200B;**samplecontent**&#x200B;运行模式：
>
>* `--promote-runmode nosamplecontent`

>



要确定应运行的命令，请使用以下命令：

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

其中，`<<YOUR_PROFILE>>`和`<<ADDITIONAL_FLAGS>>`替换为下表中列出的用户档案和标记：

<table>
 <tbody>
  <tr>
   <td><strong>源存储库</strong></td>
   <td><strong>目标库</strong></td>
   <td><strong>个人资料</strong></td>
   <td><strong>附加标志</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2或TarMK <code>FileDataStore</code></td>
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
   <td>TarMK或crx2 <code>S3DataStore</code></td>
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

**地点：**

* `mongo-host` 是MongoDB服务器IP（例如，127.0.0.1）

* `mongo-port` 是MongoDB服务器端口(例如：27017)

* `mongo-database-name` 表示数据库的名称(例如：aem-author)

**在以下情况下，您可能还需要其他交换机：**

* 如果在Java内存映射处理不正确的Windows系统上执行升级，请向命令中添加`--disable-mmap`参数。

* 如果您使用的是Java 7，请在`-Xmx`参数后添加`-XX:MaxPermSize=2048m`参数。

有关使用crx2oak工具的其他说明，请参阅使用[CRX2Oak迁移工具](/help/sites-deploying/using-crx2oak.md)。 如果需要，可手动升级crx2oak帮助程序JAR，方法是在解压缩快速启动程序后手动将其替换为较新版本。 它在AEM安装文件夹中的位置是：`<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`。 CRX2Oak迁移工具的最新版本可从以下位置下载：[https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

如果迁移成功完成，该工具将退出，退出代码为零。 此外，在AEM安装目录的`crx-quickstart/logs`下的`upgrade.log`文件中检查WARN和ERROR消息，因为这些消息可能指示迁移期间发生的非致命错误。

检查`crx-quickstart/install`文件夹下的配置文件。 如果需要迁移，将更新这些迁移以反映目标存储库。

**关于datastores的注释：**

虽然`FileDataStore`是AEM 6.3安装的新默认设置，但不需要使用外部数据存储。 虽然建议将外部数据存储作为生产部署的最佳实践，但升级不是先决条件。 由于升级AEM中已存在复杂性，我们建议在不执行数据存储迁移的情况下执行升级。 如果需要，可以在之后作为单独的工作执行数据存储迁移。

## 迁移问题疑难解答{#troubleshooting-migration-issues}

如果您是从6.3升级，请跳过此部分。虽然提供的crx2oak用户档案应满足大多数客户的需求，但有时需要其他参数。 如果您在迁移过程中遇到错误，您的环境中可能有某些方面需要提供其他配置选项。 如果是，您可能会遇到以下错误：

**不会复制检查点，因为未指定外部数据存储。这将导致在第一个开始上重新建立完整的存储库索引。 使用 — skip-checkpoints强制迁移，或查看https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration了解更多信息。**

由于某些原因，迁移过程需要访问数据存储中的二进制文件，无法找到它。 要指定您的数据存储配置，请在迁移命令的`<<ADDITIONAL_FLAGS>>`部分中包含以下标志：

**对于S3数据存储：**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

其中，`/path/to/SharedS3DataStore.config`表示S3数据存储配置文件的路径，`/path/to/datastore`表示S3数据存储的路径。

**对于文件数据存储：**

```shell
--src-datastore=/path/to/datastore
```

其中`/path/to/datastore`表示文件数据存储的路径。

## 执行升级{#performing-the-upgrade}

**如果使用S3:**

1. 删除与S3连接器的早期版本关联的`crx-quickstart/install`下的所有jar。

1. 从[https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)下载1.10.x S3连接器的最新版本

1. 将包解压到临时文件夹，并将`jcr_root/libs/system/install`的内容复制到`crx-quickstart/install`文件夹。

### 确定正确的升级开始命令{#determining-the-correct-upgrade-start-command}

要执行升级，请务必使用jar文件开始AEM以调出实例。 要升级到6.5，另请参阅[懒惰内容迁移](/help/sites-deploying/lazy-content-migration.md)中的其他内容重组和迁移选项，您可以使用升级命令进行选择。

>[!IMPORTANT]
>
>如果您运行的是Oracle Java 11（或Java的一般版本高于8），则在启动AEM时，需要向命令行添加其他交换机。 有关详细信息，请参阅[Java 11 Considerations](/help/sites-deploying/custom-standalone-install.md#java-considerations)。

请注意，从开始脚本启动AEM不会开始升级。 大多数客户使用开始脚本开始AEM，并自定义了此开始脚本，以包括内存设置、安全证书等环境配置的交换机。 因此，我们建议按照以下步骤确定正确的升级命令：

1. 在正在运行的AEM实例上，从命令行执行以下操作：

   ```shell
   ps -ef | grep java
   ```

1. 查找AEM流程。 它看起来会像：

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 通过将现有jar的路径（本例中为`crx-quickstart/app/aem-quickstart*.jar`）替换为`crx-quickstart`文件夹同级的新jar，可修改命令。 以我们以前的命令为例，我们的命令是：

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   这将确保对升级应用所有正确的内存设置、自定义运行模式和其他环境参数。 升级完成后，将来启动时可以从开始脚本启动实例。

## 部署升级的代码库{#deploy-upgraded-codebase}

完成就地升级过程后，应部署更新的代码库。 在[升级代码和自定义页面](/help/sites-deploying/upgrading-code-and-customizations.md)中可找到更新代码库以在AEM的目标版本中工作的步骤。

## 执行升级后检查和疑难解答{#perform-post-upgrade-check-troubleshooting}

请参阅[升级后检查和疑难解答](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。
