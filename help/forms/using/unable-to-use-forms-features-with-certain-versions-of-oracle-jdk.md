---
title: 无法将Experience Manager Forms与OracleJDK的某些版本一起使用
description: 无法将Experience Manager Forms与OracleJDK的某些版本一起使用
exl-id: 6a8a7cb7-77d6-4bfc-82f3-82d0fddfc10a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 1%

---

# 无法将Experience Manager Forms与OracleJDK的某些版本一起使用 {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

该问题适用于以下版本：

* Experience Manager6.3 Forms
* Experience Manager6.4 Forms
* Experience Manager6.5 Forms

## 问题 {#issue}

用户遇到以下异常：
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## 原因 {#reason}

当您运行版本高于或等于以下版本的OracleJDK （Java开发工具包）的Experience Manager Forms时，会发生例外情况：

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

上述及更高版本的Java在JVM（Java虚拟机）中包含新的XML处理限制，这些限制会导致某些Forms特定操作失败。

## 解决方法 {#workaround}

1. 停止Experience Manager Forms服务器。
1. 为应用程序服务器配置以下JVM参数：

   `-Djdk.xml.xpathExprOpLimit=2000`

   它将JVM中的system属性设置为相当高的值，以便不达到默认限制。

1. 启动Experience Manager Forms服务器。
