---
title: Adobe Experience Manager疑难解答
description: 了解AEM问题的疑难解答。
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 4%

---

# Adobe Experience Manager疑难解答 {#troubleshooting-aem}

以下部分涵盖您在使用AEM (Adobe Experience Manager)时可能遇到的一些问题，以及有关如何解决这些问题的建议。

>[!NOTE]
>
>如果您正在排查AEM中的创作问题，请参阅 [作者疑难解答。](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>如果遇到问题，也值得检查 [已知问题](/help/release-notes/release-notes.md) 适用于您的实例（发行版和服务包）。

## 针对管理员的疑难解答方案 {#troubleshooting-scenarios-for-administrators}

下表概述了管理员可以解决的问题：

<table>
 <tbody>
  <tr>
   <td><strong>角色</strong></td>
   <td><strong>问题 </strong></td>
  </tr>
  <tr>
   <td>系统管理员</td>
   <td><p>双击快速入门jar不起作用，或使用其他程序（例如，存档管理器）打开jar文件</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> </td>
   <td><p>在CRX上运行的应用程序会引发内存不足错误</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> </td>
   <td><p>双击AEM CM快速入门后，浏览器中不显示AEM欢迎屏幕</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> <p>管理员用户</p> </td>
   <td><p>创建线程转储</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> <p>管理员用户</p> </td>
   <td><p>检查未关闭的JCR会话</p> </td>
  </tr>
 </tbody>
</table>

## 安装问题 {#installation-issues}

参见 [常见安装问题](/help/sites-deploying/troubleshooting.md#common-installation-issues) 有关以下故障排除方案的信息：

* 双击“快速入门jar”不起作用，或者该JAR文件与其他程序（如存档管理器）不起作用。
* 在CRX上运行的应用程序会引发内存不足错误。
* 双击AEM快速入门后，浏览器中不显示AEM欢迎屏幕。

## 疑难解答分析方法 {#methods-for-troubleshooting-analysis}

### 创建线程转储 {#making-a-thread-dump}

线程转储是当前活动的所有Java™线程的列表。 如果AEM未正确响应，线程转储可以帮助您识别死锁或其他问题。

### 使用Sling线程转储器 {#using-sling-thread-dumper}

1. 打开 **AEM Web控制台**；例如，在 `https://localhost:4502/system/console/`.
1. 选择 **线程**&#x200B;下&#x200B;**状态** 选项卡。

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### 使用jstack（命令行） {#using-jstack-command-line}

1. 查找AEM Java™实例的PID（进程ID）。

   例如，您可以使用 `ps -ef` 或 `jps`.

1. 运行:

   `jstack <pid>`

1. 显示线程转储。

>[!NOTE]
>
>您可以使用将线程转储附加到日志文件 `>>` 输出重定向：
>
>`jstack <pid> >> /path/to/logfile.log`

请参阅 [如何从JVM进行线程转储](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=zh-Hans) 文档以了解更多信息

### 检查未关闭的JCR会话 {#checking-for-unclosed-jcr-sessions}

在为AEM WCM开发功能时，可能会打开JCR会话（相当于打开数据库连接）。 如果打开的会话从未关闭，则您的系统可能会遇到以下症状：

* 系统变慢了。
* 您可以看到许多CacheManager： resizeAll条目（在日志文件中）；以下数字(size=&lt;x>)显示缓存的数量，每个会话会打开多个缓存。
* 有时，系统内存会用尽（在数小时、数天或数周后，具体情况取决于严重程度）。

要分析未关闭的会话并找出哪个代码未关闭会话，请参阅知识库文章 [分析未关闭的会话](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html).

### 使用Adobe Experience Manager Web Console {#using-the-adobe-experience-manager-web-console}

OSGi捆绑包的状态还可以提供可能问题的早期指示。

1. 打开 **AEM Web控制台**；例如，在 `https://localhost:4502/system/console/`.
1. 选择 **包** 下 **OSGI** 选项卡。
1. 检查:

   * 捆绑包的状态。 如果有任何组件处于“不活动”或“不满意”状态，请尝试停止并重新启动该捆绑包。 如果问题仍然存在，请使用其他方法进一步调查。
   * 是否有任何捆绑包缺少依赖项。 单击单个捆绑包名称（这是一个链接），可以查看此类详细信息（以下示例没有任何问题）：

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
