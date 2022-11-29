---
title: 无法恢复适用于JEE群集服务器的损坏的CRX存储库
description: 恢复损坏的CRX存储库的步骤
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: c4f776b08cb8cc8c6eea78a3757735e063bec20c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# 无法恢复损坏的CRX存储库 {#unable-to-restore-corrupt-crx-repository}

## 带有 OS 剪贴板 {#issue}

对于使用关系数据库的JEE上的AEM Forms，托管AEM Forms的计算机上的时间与关系数据库应始终保持绝对同步。 如果这些计算机上的时间不同步，则JEE服务器上AEM Forms的CRX存储库可能会变得无法访问。 它可能显示已损坏，并且无法通过URL访问。 的 `AuthenticationsupportService missing` 错误已记录。

## 前提条件 {#prerequisites}

在执行以下步骤之前，先备份CRX存储库。

## 解决方案 {#solution}

执行以下步骤以解决问题：
1. 转到  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. 找到 `oak-core` 捆绑并检查它是否正在运行。

1. 重新启动 `oak-core` 包（如果未运行）。 如果  ![“暂停”按钮](/help/forms/using/assets/stop.png) 图标显示在 `oak-core` 包，则表示包处于运行状态。

1. 如果问题仍未解决，请从备份中从CRX存储库还原；如果备份不可用，则重新构建CRX存储库。


## 适用于 {#applies-to}

此解决方案适用于：

* AEM Forms on JEE Cluster