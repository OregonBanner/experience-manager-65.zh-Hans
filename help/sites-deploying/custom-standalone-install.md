---
title: 自定义独立安装
seo-title: 自定义独立安装
description: 了解安装独立AEM实例时可用的选项。
seo-description: 了解安装独立AEM实例时可用的选项。
uuid: 83fc49d8-2c44-4bb2-988a-f29475066efc
contentOwner: Tyler Rushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: deae8ecb-a2ee-4442-97ca-98bfd1b85738
docset: aem65
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# 自定义独立安装{#custom-standalone-install}

本节介绍在安装独立AEM实例时可用的选项。 您还可以阅读存 [储元素](/help/sites-deploying/storage-elements-in-aem-6.md) ，以了解有关在新安装AEM 6后选择后端存储类型的更多信息。

## 通过重命名文件来更改端口号 {#changing-the-port-number-by-renaming-the-file}

AEM的默认端口为4502。 如果该端口不可用或已在使用中，快速启动会自动将其配置为使用第一个可用的端口号，如下所示：4502、8080、8081、8082、8083、8084、8085、8888、9362 `<*random*>`。

还可以通过重命名快速启动jar文件来设置端口号，以便文件名包括端口号；例如， `cq5-publish-p4503.jar` 或 `cq5-author-p6754.jar`。

重命名快速入门jar文件时，应遵循各种规则：

* 重命名文件时，它必须以 `cq;` 中开头 `cq5-publish-p4503.jar`。

* 建议您始终 *在端口号* 前加-p;如cq5-publish-p4503.jar或cq5-author-p6754.jar中所示。

>[!NOTE]
>
>这是为了确保您不必担心要满足提取端口号所使用的规则：
>
>* 端口号必须为4或5位数
>* 这些数字必须在短划线之后
>* 如果文件名中有任何其他数字，则端口号必须前缀 `-p`
>* 忽略文件名开头的“cq5”前缀
>



>[!NOTE]
>
>您还可以使用start命令中的选项 `-port` 更改端口号。

### Java 11注意事项 {#java-considerations}

如果运行的是Oracle Java 11（或Java的一般版本高于8），则在启动AEM时，需要向命令行添加其他交换机。

* 以下——需 `-add-opens` 要添加交换机，以防止在 `stdout.log`

```shell
--add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

* 此外，您需要使用交换机来 `-XX:+UseParallelGC` 减轻任何潜在的性能问题。

以下是在Java 11上启动AEM时其他JVM参数的外观示例：

```shell
-XX:+UseParallelGC --add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

最后，如果运行的是从AEM 6.3升级的实例，请确保在下面将以下属性设 **置为** true `sling.properties`:

* `felix.bootdelegation.implicit`

## 运行模式 {#run-modes}

**运行模式** ，允许您针对特定用途调整AEM实例；例如，创作或发布、测试、开发、内部网等。 这些模式还允许您控制示例内容的使用。 此示例内容在构建快速入门之前定义，可以包括包、配置等。 当您希望保持安装精简且无需示例内容时，这对于生产就绪型安装尤为有用。 有关详细信息，请参阅：

* [运行模式](/help/sites-deploying/configure-runmodes.md)

## 添加文件安装提供程序 {#adding-a-file-install-provider}

默认情况下，文件 `crx-quickstart/install` 夹会被监视文件。
此文件夹不存在，但只能在运行时创建。

如果将包、配置或内容包放入此目录中，则会自动选取并安装它。 如果删除了它，它将被卸载。
这是将捆绑包、内容包或配置放入存储库的另一种方式。

这对于几个使用案例特别有趣：

* 在开发过程中，将某些内容放入文件系统可能会更容易。
* 如果出现问题，则无法访问Web控制台和存储库。 通过此组件，您可以将其他捆绑包放入此目录中，并且应安装这些捆绑包。
* 可 `crx-quickstart/install` 以在快速启动之前创建文件夹，并可以将其他包放在那里。

>[!NOTE]
>
>另请参阅 [如何在服务器启动时自动安装CRX包](https://helpx.adobe.com/experience-manager/kb/HowToInstallPackagesUsingRepositoryInstall.html) （有关示例）。

## 将Adobe Experience manager作为Windows服务进行安装和启动 {#installing-and-starting-adobe-experience-manager-as-a-windows-service}

>[!NOTE]
>
>请务必在以管理员身份登录时执行以下过程，或使用以管理员身份运行上下文菜 **单选择启动／运行这些步骤** 。
>
>以具有管理员权限的用户身份登录 **不足**。 如果您在完成这些步骤时未以管理员身份登录，则会收到“已拒 **绝访问** ”错误。

要将AEM作为Windows服务安装和启动，请执行以下操作：

1. 在文本编辑器中打开crx-quickstart\opt\helpers\instsrv.bat文件。
1. 如果要配置64位Windows服务器，请根据您的操作系统，将prunsrv的所有实例替换为以下命令之一：

   * prunsrv_amd64
   * prunsrv_ia64
   此命令调用相应的脚本，该脚本以64位Java而非32位Java启动Windows服务守护程序。

1. 要防止进程进入多个进程，请增加最大堆大小和PermGen JVM参数。 找到该 `set jvm_options` 命令并按如下方式设置值：

   `set jvm_options=-XX:MaxPermSize=256M;-Xmx1792m`

1. 打开命令提示符，将当前目录更改为AEM安装的crx-quickstart/opt/helpers文件夹，然后输入以下命令以创建服务：

   `instsrv.bat cq5`

   要验证是否已创建服务，请在“管理工具”控制面板中打开服务，或在“命令提 `start services.msc` 示”中键入。 cq5服务将显示在列表中。

1. 通过执行下列操作之一启动服务：

   * 在“服务”控制面板中，单击cq5，然后单击“开始”。
   ![chlimage_1-11](assets/chlimage_1-11.png)

   * 在命令行中，键入net start cq5。
   ![chlimage_1-12](assets/chlimage_1-12.png)

1. Windows指示服务正在运行。 AEM启动，并且任务管理器中显示prunsrv可执行文件。 在Web浏览器中，导航到AEM，例如， `https://localhost:4502` 开始使用AEM。

   ![chlimage_1-13](assets/chlimage_1-13.png)

>[!NOTE]
>
>创建Windows服务时，将使用instsrv.bat文件中的属性值。 如果在instsrv.bat中编辑属性值，则必须卸载，然后重新安装服务。

>[!NOTE]
>
>在将AEM作为服务进行安装时，必须从配置管理器中为中的日志目录提供 `com.adobe.xmp.worker.files.ncomm.XMPFilesNComm` 绝对路径。

要卸载服务，请在“服 **务”控制面板中或在命** 令行中单击“停止 **”，导航到该文件夹并键入**`instsrv.bat -uninstall cq5`。 当您键入时，服务会从“ **服务** ”控制面板的列表或命令行的列表中删除 `net start`。

## 重新定义临时工作目录的位置 {#redefining-the-location-of-the-temporary-work-directory}

Java计算机临时文件夹的默认位置为 `/tmp`。 AEM也使用此文件夹，例如，在构建包时。

如果要更改临时文件夹的位置（例如，如果需要具有更多可用空间的目录），请通过添加JVM参数来定义* `<new-tmp-path>`*:

`-Djava.io.tmpdir="/<*new-tmp-path*>"`

至：

* 服务器启动命令行
* serverctl或启动脚本中的CQ_JVM_OPTS环境参数

## 快速启动文件中提供的其他选项 {#further-options-available-from-the-quickstart-file}

快速启动帮助文件中介绍了更多选项和重命名约定，该文件可通过-help选项获得。 要访问帮助，请键入：

* `java -jar cq5-<*version*>.jar -help`

```shell
Loading quickstart properties: default
Loading quickstart properties: instance
Setting properties from filename '/Users/Desktop/AEM/cq-quickstart-5.6.0.jar'
--------------------------------------------------------------------------------
Adobe Experience Manager Quickstart (build 20130129)
--------------------------------------------------------------------------------
Usage:
 Use these options on the Quickstart command line.
--------------------------------------------------------------------------------

-help (--help,-h)
         Show this help message
-quickstart.server.port (-p,-port) <port>
         Set server port number
-contextpath (-c,-org.apache.felix.http.context_path) <contextpath>
         Set context path
-debug <port>
         Enable Java Debugging on port number; forces forking
-gui
         Show GUI if running on a terminal
-nobrowser (-quickstart.nobrowser)
         Do not open browser at startup
-unpack
         Unpack installation files only, do not start the server (implies
         -verbose)
-v (-verbose)
         Do not redirect stdout/stderr to files and do not close stdin
-nofork
         Do not fork the JVM, even if not running on a console
-fork
         Force forking the JVM if running on a console, using recommended
         default memory settings for the forked JVM.
-forkargs <args> [<args> ...]
         Additional arguments for the forked JVM, defaults to '-Xmx1024m
         -XX:MaxPermSize=256m '.  Use -- to specify values starting with -,
         example: '-forkargs -- -server'
-a (--interface) <interface>
         Optional IP address (interface) to bind to
-pt <string>
         Process type (main/fork) - do not use directly, used when forking a
         process
-r <string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string>]]]]]]]]]
         Runmode(s) - Use this to define the run mode(s)
-b <string>
         Base folder - defines the path under which the quickstart work folder
         is created
-low-mem-action <string>
         Low memory action - what to do if memory is insufficient at startup
-use-control-port
         Start a control port
-ll <level>
         Define launchpad log level (1 = error...4 = debug)
--------------------------------------------------------------------------------
Quickstart filename options
--------------------------------------------------------------------------------
Usage:
 Rename the jar file, including one of the patterns shown below, to set the
corresponding option. Command-line options have priority on these filename
patterns.
--------------------------------------------------------------------------------

-NNNN
         Include -NNNN.jar or -pNNNN in the renamed jar filename to run on port
         NNNN, for example: quickstart-8085.jar
-nobrowser
         Include -nobrowser in the renamed jar filename to avoid opening the
         browser at startup, example: quickstart-nobrowser-8085.jar
-publish
         Include -publish in the renamed jar filename to run cq5 in "publish"
         mode, example: cq5-publish-7502.jar
--------------------------------------------------------------------------------
The license.properties file
--------------------------------------------------------------------------------
  The license.properties file stores licensing information, created from the
  licensing form displayed on first startup and stored in the folder from where
  Quickstart is run.
--------------------------------------------------------------------------------
Log files
--------------------------------------------------------------------------------
  Once Quickstart has been unpacked and started, log files can be found under
  ./crx-quickstart/logs.
--------------------------------------------------------------------------------
```

## 在Amazon EC2环境中安装AEM {#installing-aem-in-the-amazon-ec-environment}

在Amazon Elastic Compute Cloud(EC2)实例上安装AEM时，如果在EC2实例上安装作者实例和发布，则按照安装AEM manager实例的过程正确安装 [作者实例](#installinginstancesofaemmanager);但是，Publish实例将变为作者。

在EC2环境中安装Publish实例之前，请执行以下操作：

1. 首次启动Publish实例之前，解压缩该实例的jar文件。 要解压缩文件，请使用以下命令：

   ```xml
   java -jar quickstart.jar -unpack
   ```

   >[!NOTE]
   >
   >如果在首次启动实 **例后** ，更改了模式，则无法更改运行模式。

1. 通过运行以启动实例：

   ```xml
   java -jar quickstart.jar -r publish
   ```

   >[!CAUTION]
   >
   >请务必首先运行上述命令，在解包实例后运行该实例。 否则，将不生成quickstart.properties填充。 如果没有此文件，任何未来的AEM升级都将失败。

1. 在bin文 **件夹中** ，打开 **开始脚本** ，并检查以下部分：

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='author'
   fi
   ```

1. 更改运行模式以 **发布** ，并保存文件。

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='publish'
   fi
   ```

1. 停止实例，并通过运行启动脚本重 **新启** 动它。

## 验证安装 {#verifying-the-installation}

以下链接可用于验证您的安装是否可操作（所有示例的基础是该实例在localhost的端口8080上运行，CRX安装在/crx下，而Launchpad安装在／下）:

* `https://localhost:8080/crx/de`
CRXDE lite控制台。

* `https://localhost:8080/system/console`
Web控制台。

## 安装后的操作 {#actions-after-installation}

虽然配置AEM WCM有许多可能，但应执行某些操作，或至少在安装后立即查看：

* 请查阅安 [全核对清单](/help/sites-administering/security-checklist.md) ，了解确保系统安全所需的任务。
* 查看随AEM WCM一起安装的默认用户和用户组列表。 检查您是否要对任何其他帐户执行操作——有关更多详细 [信息，请参阅安全和用户管理](/help/sites-administering/security.md) 。

## 访问CRXDE Lite和Web控制台 {#accessing-crxde-lite-and-the-web-console}

启动AEM WCM后，您还可以访问：

* [CRXDE Lite](#accessing-crxde-lite) —— 用于访问和管理存储库
* [Web控制台](#accessing-the-web-console) -用于管理或配置OSGi包（也称为OSGi控制台）

### 访问CRXDE Lite {#accessing-crxde-lite}

要打开CRXDE Lite，您可以从欢 **迎屏幕中选择CRXDE Lite** ，或使用浏览器导航到

```
 https://<<i>host</i>>:<<i>port</i>>/crx/de/index.jsp
```

例如：`https://localhost:4502/crx/de/index.jsp`

![installcq_crxdelite](assets/installcq_crxdelite.png)

#### 访问Web控制台 {#accessing-the-web-console}

要访问Adobe CQ web控制台，您可以从欢迎屏幕中选择 **OSGi Console** ，或使用浏览器导航到

```
 https://<host>:<port>/system/console
```

例如：或`https://localhost:4502/system/console`用于“包”页面`https://localhost:4502/system/console/bundles`

![chlimage_1-14](assets/chlimage_1-14.png)

有关 [更多详细信息，请参阅Web控制台的OSGi配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 。

## 疑难解答 {#troubleshooting}

有关处理安装过程中可能出现的问题的信息，请参阅：

* [疑难解答](/help/sites-deploying/troubleshooting.md)

## Uninstalling Adobe Experience Manager {#uninstalling-adobe-experience-manager}

由于AEM安装在单个目录中，因此无需卸载实用程序。 卸载操作与删除整个安装目录一样简单，但卸载AEM的方式取决于要实现的内容以及使用的永久存储。

如果永久存储嵌入到安装目录中（例如，在默认的TarPM安装中），则删除文件夹也会删除数据。

>[!NOTE]
>
>Adobe强烈建议您在删除AEM之前备份存储库。 如果删除整个&lt;cq-installation-directory>，则将删除存储库。 要在删除之前保留存储库数据，请在删除其他文件夹之前，将&lt;cq-installation-directory>/crx-quickstart/repository文件夹移动或复制到其他位置。

如果您的AEM安装使用外部存储（例如，数据库服务器），则删除文件夹不会自动删除数据，但会删除存储配置，这会使恢复JCR内容变得困难。
