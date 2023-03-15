---
title: 使用日志
seo-title: Working with Logs
description: 了解如何使用日志排除AEM故障。
seo-description: Learn how to troubleshoot AEM by working with logs.
uuid: af8b7f50-c8d4-4760-9f00-3feb0b79ee4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: da92d751-6f14-4512-9d77-7ecf098bd58e
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 3%

---

# 使用日志{#working-with-logs}

此部分包含有关日志的详细信息，可帮助您排除故障。

CRX记录详细的日志。 打开包装并启动“快速入门”后，您可以在以下位置找到日志：

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## 激活DEBUG日志级别 {#activating-the-debug-log-level}

默认日志级别为INFO，即不记录DEBUG消息。

要激活DEBUG日志级别，请使用CRX资源管理器设置

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

要调试的属性。 不要将日志保留在DEBUG日志级别的时间超过所需时间，因为它会生成大量日志。

调试文件中的一行通常以DEBUG开头，然后提供日志级别、安装程序操作和日志消息。 例如：

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

日志级别如下：

| 0 | 致命错误 | 操作失败，安装程序无法继续。 |
|---|---|---|
| 1 | 错误 | 操作失败。 安装会继续，但部分CRX安装不正确，无法正常工作。 |
| 2 | 警告 | 操作已成功，但遇到了问题。 CRX可能会正常工作，也可能无法正常工作。 |
| 3 | 信息 | 操作已成功。 |

## 用于故障排除的详细选项 {#verbose-option-used-for-troubleshooting}

启动CRX时，可以将 — v (verbose)选项添加到命令行中，如下所示：

` java -jar crx-<*version*>-<*edition*>.jar -v`

使用详细选项进行故障排除，因为此选项在控制台上显示一些快速入门日志输出。
