---
title: 应用程序服务器安装的升级步骤
description: 了解如何升级通过应用程序服务器部署的AEM实例。
feature: Upgrading
exl-id: 86dd10ae-7f16-40c8-84b6-91ff2973a523
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# 应用程序服务器安装的升级步骤{#upgrade-steps-for-application-server-installations}

本节介绍更新AEM for Application Server安装所需的过程。

此过程中的所有示例都使用Tomcat作为应用程序服务器，并暗示您已部署了AEM的工作版本。 此过程旨在记录从执行的升级 **AEM版本6.4至6.5**.

1. 首先，启动TomCat。 在大多数情况下，您可以通过运行 `./catalina.sh` 启动脚本，通过从终端运行以下命令：

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. 如果已部署AEM 6.4，请访问以下内容，检查捆绑包是否正常运行：

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 接下来，取消部署AEM 6.4。可以从TomCat应用程序管理器执行此操作(`http://serveraddress:serverport/manager/html`)

1. 现在，使用crx2oak迁移工具迁移存储库。 为此，请从下载最新版本的crx2oak [此位置](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/).

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -jar crx2oak.jar --load-profile segment-fds
   ```

1. 通过执行以下操作删除sling.properties文件中的必要属性：

   1. 打开文件，位于 `crx-quickstart/launchpad/sling.properties`
   1. 步骤文本删除以下属性并保存文件：

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. 删除不再需要的文件和文件夹。 需要专门移除的项目包括：

   * 此 **启动板/启动文件夹**. 可以通过在终端中运行以下命令来删除它： `rm -rf crx-quickstart/launchpad/startup`

   * 此 **base.jar文件**： `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * 此 **BootstrapCommandFile_timestamp.txt文件**： `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * 移除 **sling.options.file** 通过运行： `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. 现在，创建用于AEM 6.5的节点存储和数据存储。为此，您可以创建两个文件，其名称如下 `crx-quickstart\install`：

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   这两个文件会将AEM配置为使用TarMK节点存储区和文件数据存储。

1. 编辑配置文件以使其随时可用。 更具体地说：

   * 将以下行添加到 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`：

     `customBlobStore=true`

   * 然后将以下行添加到 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`：

     ```
     path=./crx-quickstart/repository/datastore
     minRecordLength=4096
     ```

1. 现在，您需要更改AEM 6.5 war文件中的运行模式。 为此，请先创建一个将容纳AEM 6.5战争的临时文件夹。 本示例中的文件夹名称为 `temp`. 复制war文件后，从temp文件夹内运行以提取其内容：

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. 提取内容后，转到 **WEB-INF** 文件夹并编辑web.xml文件以更改运行模式。 要查找在XML中设置它们的位置，请查找 `sling.run.modes` 字符串。 找到后，请更改下一行代码中的运行模式，该代码默认设置为“创作”：

   ```bash
   <param-value >author</param-value>
   ```

1. 更改上述创作值并将运行模式设置为： `author,crx3,crx3tar`. 代码的最后一个块应该如下所示：

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 重新创建包含修改内容的jar：

   ```bash
   jar cvf aem65.war
   ```

1. 最后，在TomCat中部署新的战争文件。
