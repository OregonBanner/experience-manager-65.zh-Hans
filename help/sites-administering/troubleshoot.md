---
title: AEM疑难解答
seo-title: AEM疑难解答
description: 了解AEM疑难解答问题。
seo-description: 了解AEM疑难解答问题。
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# AEM疑难解答 {#troubleshooting-aem}

以下部分介绍了在使用AEM时可能遇到的一些问题，以及有关如何解决这些问题的建议。

>[!NOTE]
>
>如果您正在对AEM中的创作问题进行疑难解答，请参阅作 [者疑难解答。](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>遇到问题时，还可以查阅实例（发行版本或服务包）的[已知问题](/help/release-notes/known-issues.md)列表。

## 管理员方案疑难解答 {#troubleshooting-scenarios-for-administrators}

下表概述了管理员可能需要解决的问题：

<table>
 <tbody>
  <tr>
   <td><strong>角色</strong></td>
   <td><strong>问题 </strong></td>
  </tr>
  <tr>
   <td>系统管理员</td>
   <td><p>双击快速启动jar没有任何效果，或者使用其他程序打开jar文件（例如，存档管理器）</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> </td>
   <td><p>我在CRX上运行的应用程序会引发内存不足错误</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> </td>
   <td><p>双击AEM CM快速启动后，AEM欢迎屏幕不会显示在浏览器中</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> <p>管理员用户</p> </td>
   <td><p>制作线程转储</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> <p>管理员用户</p> </td>
   <td><p>检查未关闭的JCR会话</p> </td>
  </tr>
 </tbody>
</table>

## 安装问题 {#installation-issues}

有关以 [下疑难解答场景的信息](/help/sites-deploying/troubleshooting.md#common-installation-issues) ，请参阅常见安装问题：

* 双击快速启动程序 jar 不起作用，或者 JAR 文件中包含其他程序（例如归档管理器）。
* 在 CRX 上运行的应用程序出现“内存不足”错误。
* 双击 AEM 快速启动程序后，浏览器中没有显示 AEM 欢迎屏幕。

## 疑难解答分析的方法 {#methods-for-troubleshooting-analysis}

### 制作线程转储 {#making-a-thread-dump}

线程转储是当前处于活动状态的所有Java线程的列表。 如果AEM没有正确响应，线程转储可以帮助您识别死锁或其他问题。

### 使用吊线翻车器 {#using-sling-thread-dumper}

1. 打开 **AEM Web Console**;例如， `https://localhost:4502/system/console/`。
1. 在“状态 **”**&#x200B;选项卡下&#x200B;**，选择“线程** ”。

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### 使用jstack（命令行） {#using-jstack-command-line}

1. 查找AEM java实例的PID（进程ID）。

   例如，您可以使用 `ps -ef` 或 `jps`。

1. 运行:

   `jstack <pid>`

1. 这将显示线程转储。

>[!NOTE]
>
>您可以使用输出重定向将线程转储追加到日志 `>>` 文件：
>
>`jstack <pid> >> /path/to/logfile.log`

有关更 [多信息，请参阅如何从JVM获取线程转储](https://helpx.adobe.com/cq/kb/TakeThreadDump.html) 文档

### 检查未关闭的JCR会话 {#checking-for-unclosed-jcr-sessions}

为AEM WCM开发功能后，可能会打开JCR会话（类似于打开数据库连接）。 如果打开的会话从未关闭，则系统可能会出现以下症状：

* 系统变慢。
* 您可以看到许多CacheManager:resize日志文件中的所有条目；以下数字(size=&lt;x>)显示缓存的数量，每个会话打开多个缓存。
* 系统不时内存不足（几小时、几天或几周后——具体取决于严重性）。

要分析未关闭的会话并找出哪些代码不关闭会话，请参阅知识库文章分析未关 [闭的会话](https://helpx.adobe.com/crx/kb/AnalyzeUnclosedSessions.html)。

### 使用Adobe Experience Manager Web Console {#using-the-adobe-experience-manager-web-console}

OSGi捆绑包的状态还可以提前指示可能的问题。

1. 打开 **AEM Web Console**;例如， `https://localhost:4502/system/console/`。
1. 在“ **OSGI** ”选项 **卡下选择** “捆绑”。
1. 检查:

   * 包的状态。 如果有“非活动”或“未满足”，请尝试停止并重新启动捆绑。 如果问题仍然存在，则可能需要使用其他方法进行进一步调查。
   * 是否有任何包缺少依赖关系。 单击单个捆绑名称即可查看此类详细信息，该名称是链接（以下示例没有任何问题）:

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)

