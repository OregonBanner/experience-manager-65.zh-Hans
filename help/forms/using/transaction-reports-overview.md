---
title: 交易報表概觀
seo-title: Transaction Reports Overview
description: 保持提交的所有表單、演算的互動式通訊、轉換為另一種格式的檔案等內容的計數
seo-description: Keep a count of all the forms submitted, interactive communication rendered, Documents converted to one format to another, and more
uuid: 2c3dc1f3-5bbf-4aab-aa84-7aef5aabadf6
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b2c09e6b-a1d8-4b30-af2c-988442a3a986
docset: aem65
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# 交易報表概觀{#transaction-reports-overview}

## 简介 {#introduction}

AEM Forms中的交易報告可讓您保留自AEM Forms部署上的指定日期以來發生的所有交易的計數。 目的是提供有關產品使用的資訊，並幫助業務利害關係人瞭解其數位處理量。 交易的範例包括：

* 提交最適化表單、HTML5表單或表單集
* 互動式通訊的列印或網頁版本轉譯
* 將檔案從一種檔案格式轉換為另一種檔案格式

如需被視為交易的專案的詳細資訊，請參閱 [可記帳API](../../forms/using/transaction-reports-billable-apis.md).

交易記錄預設為停用。 您可以 [啟用交易記錄](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) 從AEM Web主控台。 您可以檢視關於作者、處理或發佈執行個體的交易報告。 檢視所有交易彙總的作者或處理執行個體的交易報告。 檢視發佈執行個體的交易報告，瞭解僅在該發佈執行個體上發生的所有交易的計數，該報告執行於此處。

請勿在同一AEM例項上製作內容（建立最適化表單、互動式通訊、主題和其他製作活動）和程式檔案（使用工作流程、檔案服務和其他處理活動）。 讓用來製作內容的AEM Forms伺服器停用交易記錄。 讓用來處理檔案的AEM Forms伺服器保持啟用交易記錄。

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

交易會在緩衝區中保留指定的期間（排清緩衝區時間+反向復寫時間）。 依預設，交易計數大約需要90秒才會反映在交易報告中。

提交PDF表單、使用代理程式UI預覽互動式通訊或使用非標準表單提交方法等動作不會計為交易。 AEM Forms提供API來記錄這類交易。 從您的自訂實作呼叫API以記錄交易。

## 支援的拓撲 {#supported-topology}

交易報告僅可在OSGi環境的AEM Forms上取得。 它支援author-publish、author-processing-publish，且僅支援處理拓撲。 如需拓撲範例，請參閱 [AEM Forms的架構和部署拓撲](../../forms/using/transaction-reports-overview.md).

交易計數會從發佈執行個體反向復寫到製作或處理執行個體。 指示性的作者 — 發佈拓撲顯示如下：

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms交易報表不支援僅包含發佈例項的拓撲。

### 使用交易報告的准則 {#guidelines-for-using-transaction-reports}

* 停用所有編寫執行個體的交易報告，因為編寫執行個體的報告包含在編寫活動期間註冊的交易。
* 啟用 **僅顯示來自發佈的交易** 作者執行個體上的選項，用來檢視來自所有發佈執行個體的累計交易。 您也可以只檢視特定發佈執行個體上實際交易的每個發佈執行個體的交易報告。
* 請勿使用作者執行個體來執行工作流程和處理檔案。
* 在使用交易報告之前，如果您擁有發佈伺服器的拓撲，請確定所有發佈執行個體都啟用了反向復寫。
* 交易資料會從發佈執行個體反向復寫至僅對應的製作或處理執行個體。 作者或處理執行個體無法進一步將資料復寫至其他執行個體。 例如，如果您有author-processing-publish拓撲，則彙總的交易資料只會復寫到處理執行個體。

## 相关文章 {#related-articles}

* [檢視與瞭解交易報表](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [交易報表可記帳API](../../forms/using/transaction-reports-billable-apis.md)
* [記錄自訂實作的交易](/help/forms/using/record-transaction-custom-implementation.md)
