---
title: 无法将Experience Manager Forms与某些版本的OracleJDK结合使用
seo-title: Unable to use Experience Manager Forms with certain versions of Oracle JDK
description: 无法将Experience Manager Forms与某些版本的OracleJDK结合使用
seo-description: Unable to use Experience Manager Forms with certain versions of Oracle JDK
exl-id: 6a8a7cb7-77d6-4bfc-82f3-82d0fddfc10a
source-git-commit: 0142b46d087d34707b09a1f172910c8b287b839d
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 4%

---

# 无法将Experience Manager Forms与某些版本的OracleJDK结合使用 {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

此问题适用于以下版本：

* Experience Manager6.3Forms
* Experience Manager6.4 Forms
* Experience Manager6.5Forms

## 带有 OS 剪贴板 {#issue}

用户遇到以下异常：
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## 原因 {#reason}

在运行Experience Manager Forms时，遇到以下版本以上或等于的OracleJDK（Java开发工具包）版本时，会出现异常：

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

上述及更高版本的Java，在JVM（Java虚拟机）中包含新的XML处理限制，这会导致某些特定于Forms的操作失败。

## 解决方法 {#workaround}

1. 停止Experience Manager Forms服务器。
1. 为应用程序服务器配置以下JVM参数：

   `-Djdk.xml.xpathExprOpLimit=2000`

   它将JVM中的系统属性设置为相当高的值，以便不会点击默认限制。

1. 启动Experience Manager Forms服务器。
