---
title: 命令行启动和停止
seo-title: 命令行启动和停止
description: 通过命令行了解如何启动和停止AEM。
seo-description: 通过命令行了解如何启动和停止AEM。
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# 命令行启动和停止{#command-line-start-and-stop}

## 从命令行启动Adobe Experience Manager {#starting-adobe-experience-manager-from-the-command-line}

该 `start` 脚本位于&lt;cq- *installation>/bin目录下* 。 提供Unix和Windows版本。 脚本启动在&lt;cq-installation>目 *录中安装的实例* 。

这两个版本支持可用于启动和调整AEM实例的环境变量列表。

<table>
 <tbody>
  <tr>
   <td><strong>环境变量 </strong></td>
   <td><strong>描述 </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>用于停止和状态脚本的TCP端口<br /> </td>
  </tr>
  <tr>
   <td>CQ_HOST</td>
   <td>主机名<br /> </td>
  </tr>
  <tr>
   <td>CQ_INTERFACE</td>
   <td>此服务器应侦听的接口<br /> </td>
  </tr>
  <tr>
   <td>CQ_RUNMODE</td>
   <td>以逗号分隔的运行模式<br /> </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>jarfile的名称<br /> </td>
  </tr>
  <tr>
   <td>CQ_USE_JAAS</td>
   <td>使用JAAS（如果为true）<br /> </td>
  </tr>
  <tr>
   <td>CQ_JAAS_CONFIG</td>
   <td>JAAS配置的路径<br /> </td>
  </tr>
  <tr>
   <td>CQ_JVM_OPTS</td>
   <td>默认JVM选项<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>请注意，某些运行模式（包括创作和发布）需要在首次启动AEM之前设置，之后无法更改。 在设置应用于生产的AEM实例之前，请参阅运行模 [式文档](/help/sites-deploying/configure-runmodes.md) 。

### Windows平台start.bat脚本示例 {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Unix平台启动脚本示例 {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>启动脚本将启动&lt;cq-installation>/app *文件夹下安装的AEM Quickstart* 。

## Stopping Adobe Experience Manager {#stopping-adobe-experience-manager}

要停止AEM，请执行下列操作之一：

* 具体取决于您所使用的平台：

   * 如果从脚本或命令行启动AEM，请按 **Ctrl+C** ，关闭服务器。
   * 如果已在UNIX上使用启动脚本，则必须使用停止脚本来停止AEM。

* 如果通过双击jar文件启动AEM，请单击启动窗口上的 **On** （开始）按钮(按钮，然后更改为 **Off**)以关闭服务器。

   ![chlimage_1-63](assets/chlimage_1-63.png)

## 从命令行停止Adobe Experience Manager {#stopping-adobe-experience-manager-from-the-command-line}

该 `stop` 脚本位于&lt;cq- *installation>/bin目录下* 。 提供Unix和Windows版本。 脚本将停止在&lt;cq-installation>目录中安 *装的正在运行的实例* 。

### Unix平台停止脚本示例 {#unix-platform-stop-script-example}

```shell
./stop
```

### Windows平台stop.bat脚本示例 {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

如果只想预配置存储库（而不重新定位），您只需：

* extract `repository.xml` to the required location

* 根据需要 `repository.xml` 进行更新

* 创建 `bootstrap.properties` 和定义 `repository.config`

同样，在开始实际安装之前。

