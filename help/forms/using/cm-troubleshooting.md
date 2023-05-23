---
title: 「通訊管理：疑難排解」
seo-title: Correspondence Management Troubleshooting
description: 通訊管理疑難排解
seo-description: Correspondence Management Troubleshooting
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 6%

---

# 通訊管理：疑難排解 {#correspondence-management-troubleshooting}

## 儲存字母時發生錯誤 {#errors-when-saving-a-letter}

### 问题 {#issue}

儲存信件時會顯示下列其中一個錯誤：

* 文字模組沒有資料繫結
* 请提供以下内容所需的属性信息

### 原因 {#reason}

發生這些錯誤可能是因為下列原因之一：

* 資料字典已繫結至信件，但伺服器上不存在。
* 資料字典已繫結至字母，但名稱中有底線(_)。

### 因應措施 {#workaround}

確定您在信件中使用的資料字典位於伺服器上，且名稱中沒有底線(_)。

## 預覽信件時發生錯誤 {#error-when-previewing-a-letter}

### 问题 {#issue-1}

預覽信函時，即使信函中先前未發佈的文字資產已發佈，也會出現「載入信函時發生錯誤：無法從XML輸入匯入資產」錯誤。

### 因應措施 {#workaround-1}

使用以下步驟重設發佈執行個體上的信件快取，然後再次嘗試檢視信件：

1. 前往 **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** 並以管理員身分登入。
1. 選取 **通訊管理設定**.
1. 在 **通訊管理設定**，停用 **啟用字母快取**&#x200B;然後按一下&#x200B;**儲存。**
1. 啟用 **啟用字母快取** 然後按一下 **儲存**.
1. 重試檢視信件。
