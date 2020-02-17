---
title: 疑难解答
seo-title: 疑难解答
description: 本文介绍了您在AEM中可能遇到的一些安装问题。
seo-description: 本文介绍了您在AEM中可能遇到的一些安装问题。
uuid: 2ca898c3-b074-4ccd-a383-b92f226e6c14
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 5542de4e-6262-4300-9cf8-0eac79ba4f9a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 疑难解答{#troubleshooting}

此部分包含有关可帮助您进行疑难解答的日志的详细信息，还包含有关您可能在AEM中遇到的一些问题的信息。

## 创作性能疑难解答 {#troubleshoot-author-performance}

分析创作实例的慢性能可能变得相当复杂。 作为第一步，需要确定性能正在下降的技术堆栈级别。

下面的决策树提供了缩小瓶颈的指导。

![chlimage_1-75](assets/chlimage_1-75.png)

## 基本优化 {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## 配置日志文件和审核日志 {#configuring-log-files-and-audit-logs}

AEM会记录详细日志，您可能要配置这些日志以解决安装问题。 有关信息，请参阅 [使用审核记录和日志文件部分](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 。

## 使用详细选项 {#using-the-verbose-option}

启动AEM WCM时，可向命令行添加-v(verbose)选项，如下所示：java -jar cq-wcm-quickstart-&lt;version>.jar -v.

详细选项显示控制台上的一些快速启动日志输出，以便用于疑难解答。

## 常见安装问题 {#common-installation-issues}

下节介绍一些安装问题及其解决方案。

### **双击快速启动jar没有任何效果，或者使用其他程序打开jar文件（例如，存档管理器）{#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}**

这通常表示将操作系统的桌面环境配置为打开扩展名为。jar的文件时出现问题。 它还可能指示您尚未安装Java，或者您使用的是不支持的Java版本。

当jar文件使用无处不在的ZIP格式时，某些归档程序可能会自动配置桌面以将jar文件作为归档文件打开。

要进行疑难解答，请执行以下操作：

* 仔细检查是否至少安装了Java版本1.6。
* 尝试在AEM WCM快速启动中尝试上下文菜单（通常是右键单击），然后选择“打开方式……”.&quot;
* 检查是否列出了Java或Sun Java，并尝试与其一起运行AEM WCM。 如果安装了多个Java版本，请选择支持的版本。

   如果通过此步骤获得成功，并且您的操作系统提供了一个选项，以便始终使用所选程序运行。jar文件，请选择它。 从现在开始，双击应起作用。

* 有时重新安装支持的Java版本有助于恢复正确的关联。
* 您始终可以使用命令行运行CRX或启动／停止脚本，如本文档前面所述。

### **我在CRX上运行的应用程序会引发内存不足错误{#my-application-running-on-crx-throws-out-of-memory-errors}**

>[!NOTE]
>
>另请参阅 [分析内存问题](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)。


CRX本身的内存占用非常少。 如果在CRX中运行的应用程序具有较大的内存要求或请求内存密集型操作（例如，大事务），则需要使用适当的内存设置启动运行CRX的JVM实例。

使用Java命令选项定义JVM的内存设置（例如，java -Xmx512m -jar crx&amp;ast;.jar将heapsize设置为512MB）。

从命令行启动AEM WCM时，指定内存设置选项。 还可以修改AEM WCM启动／停止脚本或用于管理AEM WCM启动的自定义脚本以定义所需的内存设置。

如果已将堆大小定义为512MB，则可能希望通过创建堆转储进一步分析内存问题：

要在内存不足时自动创建堆转储，请使用以下命令：

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &amp;ast;.jar

这将生成堆转储文件(**java_...hprof**)。 在生成堆转储后，该进程可以继续运行。 通常，一个堆转储文件足以分析问题。

### **双击AEM Quickstart后，AEM欢迎屏幕不会显示在浏览器中{#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}**

在某些情况下，即使存储库本身成功运行，AEM WCM欢迎屏幕也不会自动显示。 这可能取决于操作系统设置、浏览器配置或类似因素。

通常的症状是AEM WCM快速启动窗口显示“AEM WCM正在启动，正在等待服务器启动……”.&quot; 如果该消息显示的时间较长，请使用默认的4502端口或运行实例的端口手动将AEM WCM URL输入到浏览器窗口中：http://localhost:4502/。

此外，日志可能会显示浏览器未启动的原因。

有时，AEM WCM快速启动窗口会显示消息“AEM WCM running on http://localhost:port/”，浏览器不会自动启动。 在这种情况下，请单击AEM WCM快速启动窗口中的URL（它是超链接），或在浏览器中手动输入URL。

如果其他一切都失败，请检查日志，找出发生了什么。

## 使用应用程序服务器进行安装疑难解答 {#troubleshooting-installations-with-an-application-server}

### **请求geometrixx-outdoor页面时返回“找不到页面”{#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}**

**适用于WebLogic 10.3.5和JBoss 5.1**

当对geometrixx-outdoors/en页面的请求返回404(Page Not Foun)时，您可以重新检查是否已在这些特定应用程序服务器所需的sling.properties文件中设置了其他sling属性。

有关详细信息， *请参阅部署AEM web应用程序* 。

### **响应标头大小可以大于4Kb{#response-header-size-can-be-greater-than-kb}**

502错误可能表示Web服务器无法处理AEM HTTP响应头的大小。 AEM可以生成HTTP响应头，其中包括大于4Kb的cookie。 确保您的Servlet容器已配置好，这样最大响应标头大小可以超过4kb。

例如，对于Tomcat 7.0, [HTTP Connector的maxHttpHeaderSize属性控制了标题大小的限制](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) 。

## Uninstalling Adobe Experience Manager {#uninstalling-adobe-experience-manager}

由于AEM安装在单个目录中，因此无需卸载实用程序。 卸载操作与删除整个安装目录一样简单，但卸载AEM的方式取决于要实现的内容以及使用的永久存储。

如果永久存储嵌入到安装目录中（例如，在默认的TarPM安装中），则删除文件夹也会删除数据。

>[!NOTE]
>
>Adobe强烈建议您在删除AEM之前备份存储库。 如果删除整个&lt;cq-installation-directory>，则将删除存储库。 要在删除之前保留存储库数据，请在删除其他文件夹之前，将&lt;cq-installation-directory>/crx-quickstart/repository文件夹移动或复制到其他位置。

如果您的AEM安装使用外部存储（例如，数据库服务器），则删除文件夹不会自动删除数据，但会删除存储配置，这会使恢复JCR内容变得困难。

### **JSP文件未在JBoss上编译{#jsp-files-are-not-compiled-on-jboss}**

如果在JBoss上将JSP文件安装或更新到Experience Manager，且未编译相应的Servlet，请确保正确配置了JBoss JSP编译器。 有关信息，请参阅[JBoss中的JSP编译问题](https://helpx.adobe.com/experience-manager/kb/jsps-dont-compile-jboss.html) 。
