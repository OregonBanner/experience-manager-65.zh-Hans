---
title: 无法恢复适用于JEE群集服务器的损坏CRX存储库
description: 了解如何恢复损坏的CRX存储库的步骤。
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# 无法恢复损坏的CRX存储库 {#unable-to-restore-corrupt-crx-repository}

## 问题 {#issue}

对于使用关系数据库的JEE上的AEM Forms ，托管AEM Forms和关系数据库的计算机上的时间应始终绝对同步。 如果这些计算机上的时间不同步，则JEE服务器上的AEM Forms的CRX存储库可能会变得无法访问。 它可能已损坏，并且无法通过URL访问。 此 `AuthenticationsupportService missing` 将记录错误。

## 前提条件 {#prerequisites}

在执行上述步骤之前，请备份CRX存储库。

## 解决方案 {#solution}

1. 转到  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. 找到 `oak-core` 绑定并检查它是否正在运行。

1. 重新启动 `oak-core` 如果未运行，则为捆绑包。 如果  ![暂停按钮](/help/forms/using/assets/stop.png) 图标显示在之前 `oak-core` 捆绑，则表明捆绑处于运行状态。

1. 如果问题仍未解决，请从备份中从CRX存储库恢复，或者在备份不可用时重建CRX存储库。


## 应用于 {#applies-to}

此解决方案适用于JEE群集上的AEM Forms 。
