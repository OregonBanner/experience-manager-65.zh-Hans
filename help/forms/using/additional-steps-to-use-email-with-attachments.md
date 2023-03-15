---
title: 获取带有附件的电子邮件的其他步骤
description: 获取带有附件的电子邮件的其他步骤
exl-id: 0d0713fb-d95a-4a95-91ef-9cdaea30e343
source-git-commit: 2e9b9c40f54aa54a946e4320341ed4a760c56fd1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 无法获取JEE平台上AEM Forms的带附件的电子邮件{#unable-to-get-email-with-attachments}

该问题适用于以下版本：
* Experience Manager6.5 Forms

## 带有 OS 剪贴板 {#issue}

用户无法执行操作，例如通过电子邮件发送PDF或使用提交配置包含附件。

## 解决方案 {#solution}

1. 将jar下载为 [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) 并解压缩下载的jar文件以获取清单文件。

1. 使用的清单文件 `java.mail-1.0.jar` 从步骤1检索以创建新的自定义jar文件，例如 `java.mail-1.5.jar`.

1. 打开清单文件并替换所有出现的 `1.5.0` 替换为 `1.5.6` 和 `Bundle-Version: 1.0` 替换为 `Bundle-Version:1.5`

1. 创建新的自定义jar (`java.mail-1.5.jar`)文件，方法是 `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` 文件夹为：
   `jar -cfm java.mail-1.5.jar manifest.mf`

   在上述命令中， *manifest.mf* 是清单文件的名称，并且 *java.mail-1.5.jar* 是在执行上述命令后创建的文件的名称。

1. 下载 [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. 导航到 `http://<server name>:<port>/lc/system/console/bundles`并删除名为 `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. 安装 `java.mail-1.5.jar` 步骤3得到的。  此步骤重新启动JEE部署的sling属性。 等待已安装的捆绑包位于 `http://<server name>:<port>/lc/system/console/bundles` 将状态显示为 **活动**.

   >注意：在这种情况下，状态仍为 **处于活动状态**，重新启动   **Jboss** 从 **服务控制台**.


1. 安装 `javax.mail-1.5.6.redhat-1.jar`使用步骤5下载的文件。

1. 停止 **Jboss** 从 **服务控制台** 并将以下属性附加到 **Sling.properties** 文件：
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. 重新启动 **Jboss**.
