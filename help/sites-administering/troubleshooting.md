---
title: 使用日志
seo-title: 使用日志
description: 了解如何通过使用日志对AEM进行疑难解答。
seo-description: 了解如何通过使用日志对AEM进行疑难解答。
uuid: af8b7f50-c8d4-4760-9f00-3feb0b79ee4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: da92d751-6f14-4512-9d77-7ecf098bd58e
docset: aem65
translation-type: tm+mt
source-git-commit: 8b53e79e3a88f58423e99477db930a4912a1ba09

---


# 使用日志{#working-with-logs}

本节包含有关可用日志的详细信息，以帮助您进行疑难解答。

CRX记录详细的日志。 打开包装并启动快速启动后，您可以在以下位置找到日志：

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## 激活调试日志级别 {#activating-the-debug-log-level}

默认日志级别为INFO，即DEBUG消息未记录。

要激活调试日志级别，请使用CRX资源管理器设置

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

要调试的属性。 不要将DEBUG日志级别的日志保留得比必需的时间长，因为它会生成大量日志。

调试文件中的一行通常以DEBUG开头，然后提供日志级别、安装程序操作和日志消息。 例如：

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

日志级别如下：

| 0 | 致命错误 | 操作失败，安装程序无法继续。 |
|---|---|---|
| 1 | 错误 | 操作已失败。 安装将继续进行，但CRX的某部分安装不正确，将无法正常工作。 |
| 2 | 警告 | 该操作已成功，但遇到问题。 CRX可能正常工作，也可能无法正常工作。 |
| 3 | 信息 | 该操作已成功。 |

## 用于疑难解答的详细选项 {#verbose-option-used-for-troubleshooting}

启动CRX时，可向命令行添加-v(verbose)选项，如下所示：

` java -jar crx-<*version*>-<*edition*>.jar -v`

使用详细选项进行疑难解答，因为此选项在控制台上显示一些快速启动日志输出。