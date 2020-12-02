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
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 1%

---


# 自定义独立安装{#custom-standalone-install}

本节介绍安装独立AEM实例时可用的选项。 您还可以阅读[存储元素](/help/sites-deploying/storage-elements-in-aem-6.md)，以了解有关在新安装AEM 6之后选择后端存储类型的更多信息。

## 通过重命名文件{#changing-the-port-number-by-renaming-the-file}更改端口号

AEM的默认端口为4502。 如果该端口不可用或已在使用，快速启动将自动配置为使用第一个可用端口号，如下所示：4502、8080、8081、8082、8083、8084、8085、8888、9362、`<*random*>`。

也可以通过重命名快速启动jar文件来设置端口号，以便文件名包括端口号；例如，`cq5-publish-p4503.jar`或`cq5-author-p6754.jar`。

重命名快速启动jar文件时，要遵循各种规则：

* 重命名文件时，它必须与`cq;`开始，如`cq5-publish-p4503.jar`中所示。

* 建议您&#x200B;*始终*&#x200B;在端口号前加-p;如cq5-publish-p4503.jar或cq5-author-p6754.jar中所示。

>[!NOTE]
>
>这是为了确保您不必担心填写用于提取端口号的规则：
>
>* 端口号必须为4或5位数
>* 这些数字必须在短划线后
>* 如果文件名中有任何其他数字，则端口号必须前缀为`-p`
>* 忽略文件名开头的“cq5”前缀

>



>[!NOTE]
>
>您还可以使用开始命令中的`-port`选项更改端口号。

### Java 11注意事项{#java-considerations}

如果您运行的是OracleJava 11（或Java的一般版本高于8），则在启动AEM时，需要向命令行添加其他交换机。

* 需要添加以下- `-add-opens`交换机，以防止在`stdout.log`中出现相关的反射访问WARNING消息

```shell
--add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

* 此外，您还需要使用`-XX:+UseParallelGC`交换机来减轻任何潜在的性能问题。

以下是在Java 11上启动AEM时其他JVM参数的外观示例：

```shell
-XX:+UseParallelGC --add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

最后，如果运行的实例是从AEM 6.3升级的，请确保在`sling.properties`下将以下属性设置为&#x200B;**true**:

* `felix.bootdelegation.implicit`

## 运行模式 {#run-modes}

**运** 行modellow以调整AEM实例以实现特定目的；例如，创作或发布、测试、开发、内部网等。这些模式还允许您控制示例内容的使用。 此示例内容是在构建快速启动之前定义的，可以包括包、配置等。 当您希望保持安装精简且无需示例内容时，此功能对于生产就绪型安装尤为有用。 有关详细信息，请参阅：

* [运行模式](/help/sites-deploying/configure-runmodes.md)

## 添加文件安装提供程序{#adding-a-file-install-provider}

默认情况下，文件夹`crx-quickstart/install`为文件进行监视。
此文件夹不存在，但只能在运行时创建。

如果将包、配置或内容包放入此目录中，将自动拾取并安装它。 如果删除，则卸载它。
这是将捆绑包、内容包或配置放入存储库的另一种方式。

这对于几个使用案例特别有趣：

* 在开发过程中，将某些内容放入文件系统可能会更容易。
* 如果出现问题，则无法访问Web控制台和存储库。 通过此程序，您可以将其他捆绑包放入此目录中，并且应安装这些捆绑包。
* 在快速启动之前，可以创建`crx-quickstart/install`文件夹，并可以将其他包放在那里。

>[!NOTE]
>
>另请参阅[如何在服务器启动时自动安装CRX包](https://helpx.adobe.com/experience-manager/kb/HowToInstallPackagesUsingRepositoryInstall.html)，以获取示例。

## 将Adobe Experience Manager安装并启动为Windows服务{#installing-and-starting-adobe-experience-manager-as-a-windows-service}

>[!NOTE]
>
>请确保在以管理员身份登录或使用&#x200B;**以管理员身份运行**&#x200B;上下文菜单选项开始/运行这些步骤时执行以下过程。
>
>以具有管理员权限的用户身份登录是&#x200B;**不够**。 如果完成这些步骤时您没有以管理员身份登录，您将收到&#x200B;**拒绝访问**&#x200B;错误。

要将AEM作为Windows服务进行安装和开始:

1. 在文本编辑器中打开crx-quickstart\opt\helpers\instsrv.bat文件。
1. 如果要配置64位Windows服务器，请根据您的操作系统，将prunsrv的所有实例替换为以下命令之一：

   * prunsrv_amd64
   * prunsrv_ia64

   此命令调用相应的脚本，该脚本以64位Java而不是32位Java开始Windows服务守护程序。

1. 要防止该进程进入多个进程，请增加最大堆大小和PermGen JVM参数。 找到`set jvm_options`命令并按如下方式设置值：

   `set jvm_options=-XX:MaxPermSize=256M;-Xmx1792m`

1. 打开命令提示符，将当前目录更改为AEM安装的crx-quickstart/opt/helpers文件夹，然后输入以下命令以创建服务：

   `instsrv.bat cq5`

   要验证是否已创建服务，请在“管理工具”控制面板中打开服务，或在命令提示符下键入`start services.msc`。 cq5服务显示在列表中。

1. 开始服务，方法如下：

   * 在“服务”控制面板中，单击cq5，然后单击“开始”。

   ![chlimage_1-11](assets/chlimage_1-11.png)

   * 在命令行中，键入net开始cq5。

   ![chlimage_1-12](assets/chlimage_1-12.png)

1. Windows指示服务正在运行。 AEM开始和prunsrv可执行文件显示在任务管理器中。 在Web浏览器中，导航到AEM，例如，`https://localhost:4502`使用AEM开始。

   ![chlimage_1-13](assets/chlimage_1-13.png)

>[!NOTE]
>
>创建Windows服务时，将使用instsrv.bat文件中的属性值。 如果在instsrv.bat中编辑属性值，则必须先卸载，然后重新安装服务。

>[!NOTE]
>
>安装AEM作为服务时，必须从Configuration Manager为`com.adobe.xmp.worker.files.ncomm.XMPFilesNComm`中的日志目录提供绝对路径。

要卸载服务，请单击&#x200B;**服务**&#x200B;控制面板中的&#x200B;**停止**，或者在命令行中，导航到文件夹并键入`instsrv.bat -uninstall cq5`。 从&#x200B;**Services**&#x200B;控制面板中的列表或在键入`net start`时从命令行中的列表删除服务。

## 重新定义临时工作目录{#redefining-the-location-of-the-temporary-work-directory}的位置

java计算机的临时文件夹的默认位置为`/tmp`。 AEM也使用此文件夹，例如在构建包时。

如果要更改临时文件夹的位置（例如，如果您需要具有更多可用空间的目录），请通过添加JVM参数来定义* `<new-tmp-path>`*:

`-Djava.io.tmpdir="/<*new-tmp-path*>"`

到以下任一位置：

* 服务器启动命令行
* serverctl或环境脚本中的CQ_JVM_OPTS开始参数

## 快速启动文件{#further-options-available-from-the-quickstart-file}中提供的其他选项

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

## 在AmazonEC2环境{#installing-aem-in-the-amazon-ec-environment}中安装AEM

在AmazonElastic Compute Cloud(EC2)实例上安装AEM时，如果在EC2实例上同时安装作者和发布，则按照[安装AEM Manager](#installinginstancesofaemmanager)实例中的步骤正确安装作者实例；但是，Publish实例将变为作者。

在EC2环境上安装Publish实例之前，请执行以下操作：

1. 首次启动Publish实例之前，解压缩该实例的jar文件。 要解压缩文件，请使用以下命令：

   ```xml
   java -jar quickstart.jar -unpack
   ```

   >[!NOTE]
   >
   >如果在首次启动实例后更改模式&#x200B;**，则无法更改运行模式。**

1. 通过运行开始实例：

   ```xml
   java -jar quickstart.jar -r publish
   ```

   >[!CAUTION]
   >
   >请确保在解压实例后，首先运行上面的命令来运行它。 否则，将不生成quickstart.properties填充。 如果没有此文件，任何未来的AEM升级都将失败。

1. 在&#x200B;**bin**&#x200B;文件夹中，打开&#x200B;**开始**&#x200B;脚本并检查以下部分：

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='author'
   fi
   ```

1. 将运行模式更改为&#x200B;**publish**&#x200B;并保存文件。

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='publish'
   fi
   ```

1. 通过运行&#x200B;**开始**&#x200B;脚本停止实例并重新启动它。

## 验证安装{#verifying-the-installation}

以下链接可用于验证您的安装是否可操作（所有示例均基于实例在localhost的端口8080上运行，CRX安装在/crx和／下的Launchpad下）:

* `https://localhost:8080/crx/de`
CRXDE Lite控制台。

* `https://localhost:8080/system/console`
Web控制台。

## 安装后的操作{#actions-after-installation}

尽管配置AEM WCM有许多可能，但应执行某些操作，或至少在安装后立即查看：

* 请查阅[安全清单](/help/sites-administering/security-checklist.md)以了解确保系统安全所需的任务。
* 查看随AEM WCM一起安装的默认用户和用户组的列表。 检查您是否要对任何其他帐户执行操作——有关更多详细信息，请参阅[安全和用户管理](/help/sites-administering/security.md)。

## 访问CRXDE Lite和Web控制台{#accessing-crxde-lite-and-the-web-console}

启动AEM WCM后，您还可以访问：

* [CRXDE Lite](#accessing-crxde-lite) -用于访问和管理存储库
* [Web控制台](#accessing-the-web-console) -用于管理或配置OSGi捆绑包（也称为OSGi控制台）

### 访问CRXDE Lite{#accessing-crxde-lite}

要打开CRXDE Lite，您可以从欢迎屏幕中选择&#x200B;**CRXDE Lite**，或使用浏览器导航到

```
 https://<<i>host</i>>:<<i>port</i>>/crx/de/index.jsp
```

例如：`https://localhost:4502/crx/de/index.jsp`

![installcq_crxdelite](assets/installcq_crxdelite.png)

#### 访问Web控制台{#accessing-the-web-console}

要访问Adobe CQWeb控制台，您可以从欢迎屏幕中选择&#x200B;**OSGi控制台**&#x200B;或使用浏览器导航到

```
 https://<host>:<port>/system/console
```

例如：
`https://localhost:4502/system/console`
或“捆绑包”页
`https://localhost:4502/system/console/bundles`

![chlimage_1-14](assets/chlimage_1-14.png)

有关更多详细信息，请参阅Web控制台的[OSGi配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)。

## 疑难解答 {#troubleshooting}

有关处理安装过程中可能出现的问题的信息，请参阅：

* [疑难解答](/help/sites-deploying/troubleshooting.md)

## 卸载Adobe Experience Manager{#uninstalling-adobe-experience-manager}

由于AEM安装在单个目录中，因此无需卸载实用程序。 卸载操作与删除整个安装目录一样简单，但卸载AEM的方式取决于您要实现的目标以及使用的永久存储。

如果永久存储嵌入到安装目录中，例如，在默认的TarPM安装中，删除文件夹也会删除数据。

>[!NOTE]
>
>Adobe强烈建议您在删除AEM之前备份存储库。 如果删除整个&lt;cq-installation-directory>，则将删除存储库。 要在删除之前保留存储库数据，请在删除其他文件夹之前，移动或复制&lt;cq-installation-directory>/crx-quickstart/repository文件夹。

如果安装AEM时使用外部存储（例如，数据库服务器），删除文件夹不会自动删除数据，但会删除存储配置，这会使恢复JCR内容变得困难。
