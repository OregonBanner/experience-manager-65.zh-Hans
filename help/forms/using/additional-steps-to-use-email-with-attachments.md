---
title: 获取带有附件的电子邮件的其他步骤
description: 获取带有附件的电子邮件的其他步骤
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 无法在JEE平台上获取带有AEM Forms附件的电子邮件{#unable-to-get-email-with-attachments}

此问题适用于以下版本：
* Experience Manager6.5Forms

## 带有 OS 剪贴板 {#issue}

用户无法执行诸如通过电子邮件发送PDF或通过提交配置包含附件等操作。

## 解决方案 {#solution}

1. 将jar下载为 [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) 并解压缩下载的jar文件，以获取清单文件。

1. 使用的清单文件 `java.mail-1.0.jar` 从步骤1中检索以创建新的自定义jar文件，如 `java.mail-1.5.jar`.

1. 打开清单文件并替换 `1.5.0` with `1.5.6` 和 `Bundle-Version: 1.0` with `Bundle-Version:1.5`

1. 创建新的自定义Jar(`java.mail-1.5.jar`使用 `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` 文件夹：
   `jar -cfm java.mail-1.5.jar manifest.mf`

   在上述命令中， *manifest.mf* 是清单文件的名称， *java.mail-1.5.jar* 是执行上述命令后将创建的文件的名称。

1. 下载 [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. 导航到 `http://<server name>:<port>/lc/system/console/bundles`并删除名为的包 `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. 安装 `java.mail-1.5.jar` 从步骤3获得。  此步骤将重新启动JEE部署的sling属性。 在 `http://<server name>:<port>/lc/system/console/bundles` 状态显示为 **活动**.

   >注意：如果为，状态仍为 **InActive**，重新启动   **JBoss** 从 **服务控制台**.


1. 安装 `javax.mail-1.5.6.redhat-1.jar`文件。

1. 停止 **JBoss** 从 **服务控制台** 并将以下属性附加到 **Sling.properties** 文件：
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. 重新启动 **JBoss**.