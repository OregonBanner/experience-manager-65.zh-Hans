---
title: 故障诊断AEM
seo-title: 故障诊断AEM
description: 了解AEM的疑难解答。
seo-description: 了解AEM的疑难解答。
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 10%

---

# AEM {#troubleshooting-aem}疑难解答

以下部分涵盖您在使用AEM时可能遇到的一些问题，以及有关如何对这些问题进行故障诊断的建议。

>[!NOTE]
>
>如果您要对AEM中的创作问题进行故障诊断，请参阅[作者疑难解答。](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>遇到问题时，还可以查阅实例（发行版本或服务包）的[已知问题](/help/release-notes/known-issues.md)列表。

## {#troubleshooting-scenarios-for-administrators}管理员故障诊断方案

下表概述了管理员可能需要解决的问题：

<table>
 <tbody>
  <tr>
   <td><strong>角色</strong></td>
   <td><strong>问题 </strong></td>
  </tr>
  <tr>
   <td>系统管理员</td>
   <td><p>双击快速入门Jar不起任何作用，或者使用其他程序（例如，存档管理器）打开Jar文件</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> </td>
   <td><p>我在CRX上运行的应用程序会引发内存不足错误</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> </td>
   <td><p>双击“AEM CM快速入门”后，浏览器中不会显示“AEM欢迎”屏幕</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> <p>管理员用户</p> </td>
   <td><p>进行线程转储</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> <p>管理员用户</p> </td>
   <td><p>检查未关闭的JCR会话</p> </td>
  </tr>
 </tbody>
</table>

## 安装问题{#installation-issues}

请参阅[常见安装问题](/help/sites-deploying/troubleshooting.md#common-installation-issues) ，以了解有关以下故障诊断情景的信息：

* 双击快速启动程序 jar 不起作用，或者 JAR 文件中包含其他程序（例如归档管理器）。
* 在 CRX 上运行的应用程序出现“内存不足”错误。
* 双击 AEM 快速启动程序后，浏览器中没有显示 AEM 欢迎屏幕。

## Analysis {#methods-for-troubleshooting-analysis}疑难解答方法

### 进行线程转储{#making-a-thread-dump}

线程转储是当前活动的所有Java线程的列表。 如果AEM未做出正确响应，线程转储可以帮助您识别死锁或其他问题。

### 使用Sling线程转储程序{#using-sling-thread-dumper}

1. 打开&#x200B;**AEM Web Console**;例如，在`https://localhost:4502/system/console/`。
1. 在&#x200B;**状态**&#x200B;选项卡下选择&#x200B;**线程**。

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### 使用jstack（命令行）{#using-jstack-command-line}

1. 查找AEM Java实例的PID（进程ID）。

   例如，您可以使用`ps -ef`或`jps`。

1. 运行:

   `jstack <pid>`

1. 这将显示线程转储。

>[!NOTE]
>
>您可以使用`>>`输出重定向将线程转储附加到日志文件：
>
>`jstack <pid> >> /path/to/logfile.log`

有关更多信息，请参阅[如何从JVM](https://helpx.adobe.com/cq/kb/TakeThreadDump.html)获取线程转储文档

### 检查未关闭的JCR会话{#checking-for-unclosed-jcr-sessions}

为AEM WCM开发功能后，可能会打开JCR会话（与打开数据库连接类似）。 如果打开的会话从未关闭，则您的系统可能会出现以下症状：

* 系统变慢了。
* 您可以看到许多CacheManager:resize日志文件中的所有条目；以下数字(size=&lt;x>)显示缓存的数量，每个会话会打开多个缓存。
* 系统会不时地耗尽内存（经过几小时、几天或几周后，具体取决于严重性）。

要分析未关闭的会话并找出哪些代码未关闭会话，请参阅知识库文章[分析未关闭的会话](https://helpx.adobe.com/crx/kb/AnalyzeUnclosedSessions.html)。

### 使用Adobe Experience Manager Web控制台{#using-the-adobe-experience-manager-web-console}

OSGi包的状态还可以提前指示可能的问题。

1. 打开&#x200B;**AEM Web Console**;例如，在`https://localhost:4502/system/console/`。
1. 在&#x200B;**OSGI**&#x200B;选项卡下选择&#x200B;**Bundles**。
1. 检查:

   * 包的状态。 如果有“不活动”或“未满足”，请尝试停止并重新启动包。 如果问题仍然存在，您可能需要使用其他方法进行进一步调查。
   * 是否有任何包缺少依赖项。 单击单个包名称即可查看此类详细信息，该名称是链接（以下示例没有任何问题）：

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
