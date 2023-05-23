---
title: 啟動和停止服務
seo-title: Starting and stopping services
description: 瞭解如何啟動和停止與AEM Forms模組、應用程式伺服器和資料庫關聯的服務。
seo-description: Learn how to start and stop services associated with AEM Forms modules and the application server and database.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 啟動和停止服務 {#starting-and-stopping-services}

AEM表單中有兩種型別的服務：

* 控制AEM表單應用程式伺服器和資料庫的服務。
* 控制AEM表單模組的服務

## 啟動或停止與AEM表單模組關聯的服務 {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM表單模組(例如Forms、Rights Management、輸出)可作為服務運作。 有時您可能需要停止或啟動這些AEM表單模組的服務。 例如，在變更服務的設定後，您必須停止然後重新啟動AEM表單服務。

1. 在管理主控台中按一下 **服務** > **應用程式和服務** > **服務管理**.
1. 在「服務管理」頁面上，選取要停止或啟動之服務旁的核取方塊，然後按一下停止或啟動。

## 啟動或停止應用程式伺服器和資料庫的服務 {#start-or-stop-services-for-the-application-server-and-database}

AEM表單的完整實作包括應用程式伺服器和資料庫服務：

* *`[application server]`* 適用於AEM表單
* *`[database]`* 適用於AEM表單

在Windows上，這些服務可透過 **管理工具** > **服務面板**. 例如，如果您使用turnkey方法在JBoss上安裝AEM表單，則您的系統上可使用下列服務：

* 適用於Adobe Experience Manager表單的JBoss
* 適用於Adobe Experience Manager的MySQL表單

從「服務」面板的清單中選取這些服務，然後按一下面板上的適當動作按鈕，即可啟動或停止這些服務。

在UNIX®或Linux上，從命令列輸入下列文字，其中 *`[service name]`* 是您正在驗證的服務名稱：

```java
     ps -A | grep [service name]
```
