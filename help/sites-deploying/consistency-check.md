---
title: 一致性和周遊檢查
seo-title: Consistency and Traversal Checks
description: 瞭解如何執行一致性和周遊檢查。
seo-description: Learn how to perform consistency and traversal checks.
uuid: 0304e378-7c60-4bf5-9052-d01149d2a6df
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: af9a3e9d-194a-42e5-be28-b238e0c1e55e
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 一致性和周遊檢查{#consistency-and-traversal-checks}

升級時，可能會因為工作區不一致而出現問題。 您可以執行測試升級以檢視這是否會造成問題，或執行一致性檢查作為預防性動作。

如果您執行因Workspace不一致而失敗的測試升級，您會在crx-quickstart/logs/crx/error.log中看到類似下列的專案：

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## 執行一致性檢查 {#perform-a-consistency-check}

若要執行一致性檢查，請瀏覽至JMX Mbean** com.adobe.granite （儲存區域）的管理頁面** 從AEM主畫面，前往：

**「工具」>「Web主控台」>「Main（在功能表列上）」>「JMX」>「com.adobe.granite （存放庫）」**

在預設安裝中，可在此處找到：  **[|顯示給我|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

在 **作業** 在頁面的區段中，您會找到兩種方法： **`traversalCheck`** 和 **`consistencyCheck`**. 若要執行檢查，請按一下操作並輸入所需的引數。

![chlimage_1-117](assets/chlimage_1-117.png)
