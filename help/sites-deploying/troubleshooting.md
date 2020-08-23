---
title: 疑难解答
seo-title: 疑难解答
description: 本文介绍您在AEM上可能遇到的一些安装问题。
seo-description: 本文介绍您在AEM上可能遇到的一些安装问题。
uuid: 2ca898c3-b074-4ccd-a383-b92f226e6c14
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 5542de4e-6262-4300-9cf8-0eac79ba4f9a
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---


# 疑难解答{#troubleshooting}

本节包括有关日志的详细信息，可帮助您进行故障排除，还包括有关您可能遇到的AEM问题的一些信息。

## 创作性能疑难解答 {#troubleshoot-author-performance}

分析创作实例的慢性能可能变得相当复杂。 作为第一步，它需要确定性能正在下降的技术堆栈级别。

下面的决策树提供了缩小瓶颈的指导。

![chlimage_1-75](assets/chlimage_1-75.png)

## 基本优化 {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## 配置日志文件和审核日志 {#configuring-log-files-and-audit-logs}

AEM会记录详细日志，您可能要配置这些日志，以排除安装问题。 有关信息，请参 [阅使用审核记录和日志文件](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 。

## 使用详细选项 {#using-the-verbose-option}

在开始AEM WCM时，可以向命令行添加-v(verbose)选项，如：java -jar cq-wcm-quickstart-&lt;version>.jar -v.

详细选项显示控制台上的一些快速启动日志输出，以便用于故障排除。

## 常见安装问题 {#common-installation-issues}

下节介绍一些安装问题及其解决方案。

### 多次-单击快速启动jar没有任何效果，或者使用其他项目（例如，归档管理器）打开jar文件 {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

这通常表示操作系统的桌面环境配置为打开扩展名为。jar的文件时出现问题。 它还可能指示您未安装Java，或者您使用的是不支持的Java版本。

当jar文件使用无处不在的ZIP格式时，某些归档项目可能会自动配置桌面以将jar文件作为归档文件打开。

要进行疑难解答，请执行以下操作：

* 多次检查是否至少安装了Java版本1.6。
* 尝试AEM WCM快速启动上的上下文菜单（通常单击鼠标右键），然后选择“打开方式……”&quot;
* 检查是否列出了Java或Sun Java，并尝试与它一起运行AEM WCM。 如果安装了多个Java版本，请选择支持的版本。

   如果您通过此步骤获得成功，并且您的操作系统优惠了一个选项，以便始终使用选定的项目运行。jar文件，请选择它。 多次单击应从现在开始生效。

* 有时重新安装支持的Java版本有助于恢复正确的关联。
* 您始终可以如上所述使用命令行或开始/停止脚本运行CRX。

### 我在CRX上运行的应用程序会引发内存不足错误 {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>另请参阅 [分析内存问题](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)。


CRX本身内存占用很少。 如果在CRX中运行的应用程序具有较大的内存要求或请求占用大量内存的操作（例如，大事务），则需要使用适当的内存设置启动运行CRX的JVM实例。

使用Java命令选项定义JVM的内存设置（例如，java -Xmx512m -jar crx&amp;ast;.jar将heapsize设置为512MB）。

从命令行启动AEM WCM时指定内存设置选项。 还可以修改用于管理AEM WCM启动的AEM WCM开始/停止脚本或自定义脚本以定义所需的内存设置。

如果已将堆大小定义为512MB，您可能希望通过创建堆转储进一步分析内存问题：

要在内存不足时自动创建堆转储，请使用以下命令：

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &amp;ast;.jar

这将生成堆转储文&#x200B;**件(java_...hprof**)。 生成堆转储后，该进程可能继续运行。 通常，一个堆转储文件足以分析问题。

### The AEM Welcome screen does not display in the browser after double-clicking AEM Quickstart {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

在某些情况下，即使存储库本身成功运行，AEM WCM欢迎屏幕也不会自动显示。 这可能取决于操作系统设置、浏览器配置或类似因素。

通常的症状是AEM WCM快速启动窗口显示“AEM WCM正在启动，正在等待服务器启动……&quot; 如果此消息显示时间较长，请使用默认的4502端口或运行实例的端口，手动将AEM WCM URL输入浏览器窗口：http://localhost:4502/。

此外，日志可能会显示浏览器未启动的原因。

有时，AEM WCM快速启动窗口会显示消息“AEM WCM running on http://localhost:port/”，浏览器不会自动开始。 在这种情况下，单击AEM WCM快速启动窗口中的URL（它是超链接）或在浏览器中手动输入URL。

如果其他方法都失败，请查看日志，找出发生了什么。

## 使用应用程序服务器进行安装疑难解答 {#troubleshooting-installations-with-an-application-server}

### 请求geometrixx-outdoor页面时返回“找不到页面” {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}

**适用于WebLogic 10.3.5和JBoss 5.1**

当对geometrixx-outdoors/en页面的请求返回404（找不到页面）时，您可以重新检查是否已在这些特定应用程序服务器所需的sling.properties文件中设置了附加sling属性。

有关详细信息， *请参阅部署AEM* web应用程序步骤。

### 响应标头大小可以大于4Kb {#response-header-size-can-be-greater-than-kb}

502个错误可能表示Web服务器无法处理AEM HTTP响应头的大小。 AEM可以生成包含大于4Kb的cookie的HTTP响应头。 确保您的servlet容器已配置，这样最大响应标头大小可以超过4kb。

例如，对于Tomcat 7.0,HTTP连接器的maxHttpHeaderSize属性 [控制了头大小](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) （限制）。

## Uninstalling Adobe Experience Manager {#uninstalling-adobe-experience-manager}

由于AEM安装在单个目录中，因此无需卸载实用程序。 卸载操作与删除整个安装目录一样简单，但卸载AEM的方式取决于您要实现的目标以及使用的永久存储。

如果永久存储嵌入到安装目录中，例如，在默认的TarPM安装中，删除文件夹也会删除数据。

>[!NOTE]
>
>Adobe强烈建议您在删除AEM之前备份存储库。 如果删除整个&lt;cq-installation-directory>，则将删除存储库。 要在删除之前保留存储库数据，请在删除其他文件夹之前，移动或复制&lt;cq-installation-directory>/crx-quickstart/repository文件夹。

如果安装AEM时使用外部存储（例如，数据库服务器），删除文件夹不会自动删除数据，但会删除存储配置，这会使恢复JCR内容变得困难。

### JSP文件未在JBoss上编译 {#jsp-files-are-not-compiled-on-jboss}

如果安装或更新JSP文件以Experience ManagerJBoss，并且未编译相应的Servlet，请确保正确配置了JBoss JSP编译器。 有关信息，请参阅[JBoss中的JSP编译问题](https://helpx.adobe.com/experience-manager/kb/jsps-dont-compile-jboss.html) 。
