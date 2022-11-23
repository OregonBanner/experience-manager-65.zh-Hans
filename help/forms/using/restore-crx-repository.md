---
title: 无法恢复适用于JEE群集服务器的损坏的CRX存储库
description: 恢复损坏的CRX存储库的步骤
source-git-commit: a7d125503b0bd3c52cb3a959e2f0dde1a69cbe2b
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---

# 无法恢复损坏的CRX存储库 {#unable-to-restore-corrupt-crx-repository}

## 带有 OS 剪贴板 {#issue}

对于在JEE上部署的具有RDB持久性的AEM Forms,AEM Forms主机和数据库计算机必须处于绝对时间同步状态。 但是，如果时钟因某些原因不同步，则CRX存储库会损坏，并且其URL变得不可访问。 错误为 `AuthenticationsupportService missing` 在日志文件中发生。

## 解决方案 {#solution}

执行以下步骤以解决问题：
1. 转到  [https://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).

1. 找到 `oak-core` 捆绑并检查它是否正在运行。

1. 重新启动 `oak-core` 包（如果未运行）。 如果在 `oak-core` 包，则表示包处于运行状态。

1. 如果问题仍未解决，请从备份中从CRX存储库还原；如果备份不可用，则重新构建CRX存储库。

   >[!NOTE]
   >
   >在执行上述步骤之前，先备份CRX存储库。

## 适用于 {#applies-to}

此解决方案适用于：

* AEM Forms on JEE Cluster Server


