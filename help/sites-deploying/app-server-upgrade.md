---
title: 应用程序服务器安装的升级步骤
seo-title: 应用程序服务器安装的升级步骤
description: 了解如何升级通过应用程序服务器部署的AEM实例。
seo-description: 了解如何升级通过应用程序服务器部署的AEM实例。
uuid: e4020966-737c-40ea-bfaa-c63ab9a29cee
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 1876d8d6-bffa-4a1c-99c0-f6001acea825
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e

---


# 应用程序服务器安装的升级步骤{#upgrade-steps-for-application-server-installations}

本节介绍更新AEM for Application server安装时需要遵循的过程。

此过程中的所有示例都使用JBoss作为应用程序服务器，暗示您已部署了AEM的工作版本。 此过程用于记录从 **AEM版本5.6到6.3执行的升级**。

1. 首先，启动JBoss。 在大多数情况下，您可以通过从终端运 `standalone.sh` 行以下命令来运行启动脚本：

   ```shell
   jboss-install-folder/bin/standalone.sh
   ```

1. 如果已部署AEM 5.6，请通过运行以下各项来检查捆绑包是否正常运行：

   ```shell
   wget https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 接下来，取消部署AEM 5.6:

   ```shell
   rm jboss-install-folder/standalone/deployments/cq.war
   ```

1. 停止JBoss。

1. 现在，使用crx2oak迁移工具迁移存储库：

   ```shell
   java -jar crx2oak.jar crx-quickstart/repository/ crx-quickstart/oak-repository
   ```

   >[!NOTE]
   >
   >在此示例中，oak-repository是新转换的存储库将驻留的临时目录。 在执行此步骤之前，请确保您拥有最新的crx2oak.jar版本。

1. 通过执行以下操作，删除sling.properties文件中的必要属性：

   1. 打开位于 `crx-quickstart/launchpad/sling.properties`
   1. 步骤文本删除以下属性并保存文件：

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. 删除不再需要的文件和文件夹。 您需要特别删除的项目包括：

   * launchpad/ **startup文件夹**。 可以通过在终端中运行以下命令来删除它： `rm -rf crx-quickstart/launchpad/startup`

   * base. **jar文件**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * BootstrapCommandFile_timestamp.txt文件 ****: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

1. 将新迁移的区段存储复制到其正确位置：

   ```shell
   mv crx-quickstart/oak-repository/segmentstore crx-quickstart/repository/segmentstore
   ```

1. 还复制数据存储：

   ```shell
   mv crx-quickstart/repository/repository/datastore crx-quickstart/repository/datastore
   ```

1. 接下来，您需要创建包含将与新升级实例一起使用的OSGi配置的文件夹。 具体而言，需要在crx-quickstart下创建名为install的 **文件夹**。

1. 现在，创建要与AEM 6.3一起使用的节点存储和数据存储。为此，可以在crx-quickstart\install下创建两个具有以下名 **称的文件**:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`

   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`
   这两个文件将配置AEM以使用TarMK节点存储和文件数据存储。

1. 编辑配置文件，使其可供使用。 更具体地说：

   * 将以下代码行添 **加到org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**:\
      `customBlobStore=true`

   * 然后，将以下代码行添 **加到org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**:

      ```
      path=./crx-quickstart/repository/datastore
       minRecordLength=4096
      ```

1. 通过运行以下命令删除crx2运行模式：

   ```shell
   find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \
   ```

1. 您现在需要更改AEM 6.3 war文件中的运行模式。 为此，请首先创建一个临时文件夹，用于容纳AEM 6.3战争。 此示例中的文件夹名称将为临 **时**。 复制war文件后，从temp文件夹内运行以提取其内容：

   ```shell
   jar xvf aem-quickstart-6.3.0.war
   ```

1. 提取内容后，转到 **WEB-INF文件夹并编辑文**`web.xml` 件以更改运行模式。 要查找在XML中设置它们的位置，请查找字 `sling.run.modes` 符串。 找到它后，请更改下一行代码中的运行模式，默认情况下，该代码行设置为作者：

   ```shell
   <param-value >author</param-value>
   ```

1. 更改上述作者值并将运行模式设置为：author,crx3,crx3tar最终的代码块应当如下：

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 使用修改后的内容重新创建jar:

   ```shell
   jar cvf aem62.war
   ```

1. 最后，部署新的战争文件：

   ```shell
   cp temp/aem62.war jboss-install-folder/standalone/deployments/aem61.war
   ```

