---
title: 使用日志
seo-title: 使用日志
description: 了解如何通过使用日志对AEM进行故障诊断。
seo-description: 了解如何通过使用日志对AEM进行故障诊断。
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
source-wordcount: '246'
ht-degree: 3%

---

# 使用日志{#working-with-logs}

此部分包含有关可帮助您进行故障诊断的日志的详细信息。

CRX记录详细日志。 解包并启动快速入门后，您可以在以下位置找到日志：

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## 激活DEBUG日志级别{#activating-the-debug-log-level}

默认日志级别为“信息”，即不记录DEBUG消息。

要激活“调试”日志级别，请使用CRX资源管理器设置

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

要调试的属性。 请勿将日志保留在DEBUG日志级别，因为该日志会生成大量日志，所以不要将其保留在必要的时间以内。

调试文件中的一行通常以DEBUG开头，然后提供日志级别、安装程序操作和日志消息。 例如：

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

日志级别如下：

| 0 | 致命错误 | 操作失败，安装程序无法继续。 |
|---|---|---|
| 1 | 错误 | 操作失败。 安装将继续进行，但CRX的一部分安装不正确，无法正常工作。 |
| 2 | 警告 | 操作已成功，但遇到问题。 CRX可能正常工作，也可能无法正常工作。 |
| 3 | 信息 | 操作成功。 |

## 用于{#verbose-option-used-for-troubleshooting}故障排除的详细选项

启动CRX时，可以向命令行中添加 — v(verbose)选项，如下所示：

` java -jar crx-<*version*>-<*edition*>.jar -v`

使用详细选项进行故障诊断，因为此选项在控制台上显示一些快速启动日志输出。
