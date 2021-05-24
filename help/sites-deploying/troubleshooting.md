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
exl-id: 55576729-be9c-412e-92ac-4be90650c6fa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 0%

---

# 疑难解答{#troubleshooting}

本节包含可帮助您进行故障诊断的日志的详细信息，还包含有关您在AEM中可能遇到的一些问题的信息。

## 创作性能疑难解答{#troubleshoot-author-performance}

在创作实例上分析缓慢的性能可能会变得相当复杂。 第一步需要确定性能下降的技术堆栈级别。

以下决策树为缩小瓶颈提供了指导。

![chlimage_1-75](assets/chlimage_1-75.png)

## 基本优化{#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## 配置日志文件和审核日志{#configuring-log-files-and-audit-logs}

AEM记录您可能需要配置的详细日志，以便对安装问题进行故障诊断。 有关信息，请参阅[使用审核记录和日志文件](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)一节。

## 使用详细选项{#using-the-verbose-option}

启动AEM WCM时，可以向命令行中添加 — v(verbose)选项，如下所示：java -jar cq-wcm-quickstart-&lt;版本>.jar -v。

详细选项在控制台上显示一些快速启动日志输出，以便用于疑难解答。

## 常见安装问题{#common-installation-issues}

以下部分介绍一些安装问题及其解决方案。

### 双击快速入门Jar不起任何作用，或者使用其他程序（例如，存档管理器）{#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}打开Jar文件

这通常表示将操作系统的桌面环境配置为打开扩展名为.jar的文件时出现问题。 它还可能表示您未安装Java，或者您使用的是不受支持的Java版本。

由于jar文件使用无处不在的ZIP格式，因此某些存档程序可能会自动将桌面配置为将jar文件作为存档文件打开。

要进行故障诊断，请执行以下操作：

* 再次检查您是否至少安装了Java版本1.6。
* 在AEM WCM快速入门中尝试使用上下文菜单（通常单击鼠标右键），然后选择“打开方式……”.&quot;
* 检查是否列出了Java或Sun Java，然后尝试使用它运行AEM WCM。 如果安装了多个Java版本，请选择支持的版本。

   如果此步骤成功，并且您的操作系统提供了始终使用选定程序运行.jar文件的选项，请选择它。 此后，双击应该可以正常工作。

* 有时重新安装支持的Java版本有助于恢复正确的关联。
* 您始终可以使用命令行或启动/停止脚本来运行CRX，如本文档前面所述。

### 我在CRX上运行的应用程序会引发内存不足错误{#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>另请参阅[分析内存问题](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)。


CRX公司自身的内存占用空间非常小。 如果在CRX中运行的应用程序具有较大的内存要求或请求内存密集型操作（例如，大型事务），则需要使用适当的内存设置启动运行CRX的JVM实例。

使用Java命令选项定义JVM的内存设置（例如，java -Xmx512m -jar crx&amp;ast;.jar将heapsize设置为512MB）。

从命令行启动AEM WCM时指定内存设置选项。 还可以修改AEM WCM启动/停止脚本或用于管理AEM WCM启动的自定义脚本，以定义所需的内存设置。

如果已将堆大小定义为512MB，则可能需要通过创建堆转储进一步分析内存问题：

要在内存不足时自动创建堆转储，请使用以下命令：

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &amp;ast;.jar

这会生成堆转储文件(**java_...hprof**)。 在生成堆转储后，该进程可能会继续运行。 通常，一个堆转储文件就足以分析问题。

### 双击“AEM快速入门{#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}”后，浏览器中不会显示“AEM欢迎”屏幕

在某些情况下，即使存储库本身成功运行，AEM WCM欢迎屏幕也不会自动显示。 这可能取决于操作系统设置、浏览器配置或类似因素。

常见症状是“AEM WCM快速启动”窗口显示“AEM WCM正在启动，正在等待服务器启动…….&quot; 如果该消息显示时间较长，请使用默认的4502端口或运行实例的端口手动将AEM WCM URL输入到浏览器窗口中：http://localhost:4502/。

此外，日志可能还会显示浏览器未启动的原因。

有时，AEM WCM快速启动窗口会显示消息“AEM WCM正在http://localhost:port/上运行”，并且浏览器不会自动启动。 在这种情况下，单击AEM WCM快速入门窗口中的URL（它是超链接），或在浏览器中手动输入该URL。

如果其他所有操作都失败，请检查日志以了解发生了什么。

### 使用Java 11 {#the-website-does-not-load-or-fails-intermittently-with-java11}时，网站不会加载或间歇性失败

在Java 11上运行的AEM 6.5存在一个已知问题，即网站可能无法间歇性加载或失败。

如果发生这种情况，请按照以下解决方法操作：

1. 在`crx-quickstart/conf/`文件夹下打开`sling.properties`文件
1. 找到以下行：

   `org.osgi.framework.bootdelegation=sun.,com.sun.`

1. 将其替换为：

   `org.osgi.framework.bootdelegation=sun.,com.sun.,jdk.internal.reflect,jdk.internal.reflect.*`

1. 重新启动实例。

## 使用应用程序服务器{#troubleshooting-installations-with-an-application-server}进行安装故障排除

### 请求geometrixx-outdour页面{#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}时返回页面未找到

**适用于WebLogic 10.3.5和JBoss 5.1**

当对geometrixx-outdoors/en页面的请求返回404（页面未找到）时，您可以重新检查是否已在这些特定应用程序服务器所需的sling.properties文件中设置附加sling属性。

有关详细信息，请参阅&#x200B;*部署AEM Web应用程序*&#x200B;步骤中的。

### 响应标头大小可以大于4Kb {#response-header-size-can-be-greater-than-kb}

502错误可能表示Web服务器无法处理AEM HTTP响应标头的大小。 AEM可以生成包含大于4Kb的Cookie的HTTP响应标头。 确保配置了Servlet容器，以便最大响应标头大小可以超过4kb。

例如，对于Tomcat 7.0,[HTTP Connector](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html)的maxHttpHeaderSize属性控制标头大小的限制。

## 卸载Adobe Experience Manager {#uninstalling-adobe-experience-manager}

由于AEM安装到单个目录中，因此无需卸载实用程序。 卸载操作与删除整个安装目录一样简单，不过卸载AEM的方式取决于您要实现的内容以及您使用的永久存储。

如果永久存储嵌入在安装目录中，例如，在默认的TarPM安装中，删除文件夹也会删除数据。

>[!NOTE]
>
>Adobe强烈建议您在删除AEM之前备份存储库。 如果删除整个&lt;cq-installation-directory>，则将删除存储库。 要在删除之前保留存储库数据，请在删除其他文件夹之前，将&lt;cq-installation-directory>/crx-quickstart/repository文件夹移动或复制到其他位置。

如果您的AEM安装使用外部存储（例如，数据库服务器），则删除文件夹不会自动删除数据，但会删除存储配置，这会使恢复JCR内容变得困难。

### JP文件未在JBoss {#jsp-files-are-not-compiled-on-jboss}上编译

如果安装或更新JSP文件以在JBoss上Experience Manager，并且未编译相应的Servlet，请确保正确配置了JBoss JSP编译器。 有关信息，请参阅
JBoss](https://helpx.adobe.com/experience-manager/kb/jsps-dont-compile-jboss.html)文章中的[JSP编译问题。
