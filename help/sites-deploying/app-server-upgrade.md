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
feature: 升级
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---


# 应用程序服务器安装的升级步骤{#upgrade-steps-for-application-server-installations}

本节介绍更新AEM Server安装所需的步骤。

此过程中的所有示例都使用Tomcat作为应用程序服务器，暗示您已部署了可工作版本的AEM。 该过程用于将从&#x200B;**AEM版本6.4到6.5**&#x200B;执行的升级文档。

1. 首先，开始汤姆·凯特。 在大多数情况下，可以通过从终端运行此命令来运行`./catalina.sh`开始启动脚本：

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. 如果AEM 6.4已部署，请访问以下链接，检查捆绑包是否正常运行：

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 接下来，取消部署AEM 6.4。这可以从TomCat App Manager(`http://serveraddress:serverport/manager/html`)中完成

1. 现在，使用crx2oak迁移工具迁移存储库。 为此，请从[此位置](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak)下载最新版crx2oak。

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -XX:MaxPermSize=2048M -jar crx2oak.jar --load-profile segment-fds
   ```

1. 通过执行以下操作，删除sling.properties文件中的必要属性：

   1. 打开位于`crx-quickstart/launchpad/sling.properties`的文件
   1. 步骤文本删除以下属性并保存文件：

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. 删除不再需要的文件和文件夹。 您需要特别删除的项目有：

   * **launchpad/startup文件夹**。 可以通过在终端中运行以下命令来删除它：`rm -rf crx-quickstart/launchpad/startup`

   * **base.jar文件**:`find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * **BootstrapCommandFile_timestamp.txt文件**:`rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * 通过运行以下命令删除&#x200B;**sling.options.file**:`find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. 现在，创建将与AEM 6.5一起使用的节点存储和数据存储。通过在`crx-quickstart\install`下创建具有以下名称的两个文件，可以执行此操作：

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   这两个文件将配置AEM以使用TarMK节点存储和文件数据存储。

1. 编辑配置文件，使其随时可用。 更具体地说：

   * 将以下行添加到`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

      ```customBlobStore=true```

   * 然后，将以下行添加到`org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

      ```
      path=./crx-quickstart/repository/datastore
      minRecordLength=4096
      ```

1. 您现在需要更改AEM 6.5 war文件中的运行模式。 为此，首先创建一个临时文件夹，用于容纳AEM 6.5战争。 此示例中文件夹的名称将为`temp`。 复制war文件后，从temp文件夹内运行以提取其内容：

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. 提取内容后，转到&#x200B;**WEB-INF**&#x200B;文件夹并编辑web.xml文件以更改运行模式。 要查找在XML中设置它们的位置，请查找`sling.run.modes`字符串。 找到后，在下一行代码中更改运行模式，默认情况下，该模式设置为作者：

   ```bash
   <param-value >author</param-value>
   ```

1. 更改上述创作值，并将运行模式设置为：`author,crx3,crx3tar`。 最终的代码块应当如下：

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 使用修改后的内容重新创建jar:

   ```bash
   jar cvf aem65.war
   ```

1. 最后，在TomCat中部署新的战争文件。
