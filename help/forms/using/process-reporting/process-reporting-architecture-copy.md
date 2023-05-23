---
title: 程式報告的運作方式
seo-title: How Process Reporting Works
description: 構成AEM Forms on JEE Process Reporting的服務說明和Process Reporting UI的簡介
seo-description: Description of the services that make up the AEM Forms on JEE Process Reporting and an introduction to the Process Reporting UI
uuid: 4631b734-a679-495c-a708-2348bf22c1f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a1af9920-5d2a-462f-bdee-ccec4c047c5b
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# 程式報告的運作方式 {#how-process-reporting-works}

程式報告是AEM Forms on JEE的報告模組。

程式報告可讓您執行AEM Forms程式和工作的報告。

Process Reporting使用內嵌的Process Reporting存放庫來發佈Forms資料。 然後使用該資料執行報表。

「程式報告」包含下列模組：

* [ProcessDataPublisher服務](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [ProcessDataStorage服務](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [OSGi服務](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [查詢資料servlet](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [程式報告使用者介面](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## 程式報告架構 {#process-reporting-architecture-br}

![processreportingarchitecture](assets/processreportingarchitecture.png)

## 程式報告模組 {#process-reporting-modules}

### ProcessDataPublisher服務 {#processdatapublisher-service-br}

ProcessDataPublisher伺服器會定期在AEM Forms資料庫上執行，並擷取自上次執行服務後變更的資料。 然後會將資料發佈至Process Data Storage服務。

如需設定服務的詳細資訊，請參閱 [設定ProcessDataPublisher服務](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### ProcessDataStorageProvider服務 {#processdatastorageprovider-service-br}

ProcessDataStorageProvider服務會從ProcessDataPublisher服務接收程式資料，並將資料儲存到Process Reporting儲存庫。

如需設定服務的詳細資訊，請參閱 [設定ProcessDataStorageProvider服務](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### OSGi服務 {#osgi-service-br}

QueryDataServlet使用此服務從Process Reporting存放庫取得報表資料。

### QueryDataServlet服務 {#querydataservlet-service-br}

QueryDataServlet服務接受來自程式報告使用者介面的查詢。

然後，服務會使用OSGi服務來取得相關報表資料、處理資料，然後將資料傳回至使用者介面。

### 程式報告使用者介面 {#process-reporting-user-interface-br}

「程式報表」使用者介面是網頁瀏覽器介面。 您可以使用此介面來檢視從AEM Forms資料庫發佈的程式與工作資訊。

### QueryDataServlet服務 {#querydataservlet-service-br-1}

QueryDataServlet服務接受來自程式報告使用者介面的查詢。

然後，服務會使用OSGi服務來取得相關報表資料、處理資料，然後將資料傳回至使用者介面。

### 自訂報表 {#custom-reports-br}

您可以建立自己的自訂報表，並在「程式報表」使用者介面的「自訂報表」標籤中顯示這些報表。

如需建立自訂報表的步驟，請參閱文章中的若要建立自訂報表 [自訂報告進行中報告](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
