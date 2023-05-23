---
title: 程式報表中的預先定義報表
seo-title: Pre-defined reports in Process Reporting
description: 查詢AEM Forms on JEE程式資料，以建立長時間執行的程式、程式持續時間和工作流程量的報告
seo-description: Query for AEM Forms on JEE process data to create reports on long running processes, Process duration, and Workflow volume
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# 程式報表中的預先定義報表 {#pre-defined-reports-in-process-reporting}

## 處理中報表的預先定義報表 {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reporting提供下列功能 *現成可用* 報告：

* **[長時間執行的程式](#long-running-processes)**：所有花費超過指定時間完成的AEM Forms程式報表
* **[程式持續時間圖表](#process-duration-report)**：指定AEM Forms處理序的報告（依期間）
* **[工作流程數量](#workflow-volume-report)**：指定處理序的執行中及完成的執行個體報表（依日期）

## 長時間執行的程式 {#long-running-processes}

「長時間執行的程式」報表會顯示花費超過指定時間完成的AEM Forms程式。

### 執行長時間執行處理作業報告 {#to-execute-a-long-running-process-report}

1. 若要在「程式報告」中檢視預先定義報告的清單，請前往 **程式報告** 樹狀檢視，按一下 **報表** 節點。
1. 按一下 **長時間執行的程式** 報告節點。

   ![long_running_node](assets/long_running_node.png)

   當您選取報表時， **報表引數** 面板會顯示在樹狀檢視的右側。

   ![長時間執行程式報告引數面板](assets/report_parameters_panel.png)

   参数:

   * **持續時間** (*強制*)：指定持續期間和時間單位。 顯示執行時間超過指定持續時間的所有AEM Forms程式。
   * **開始晚於** (*可選*)：選取日期。 篩選報告以顯示指定日期後開始的流程例項。
   * **開始於以下日期之前** (*可選*)：選取日期。 篩選報告以顯示指定日期之前開始的流程例項。

1. 按一下 **前往** 以執行報表。

   報告會顯示在 **報告** 右側面板 **程式報告** 視窗。

   ![long_running_processes](assets/long_running_processes.png)

   使用右上角的選項 **報告** 面板，對報告執行下列操作。

   * **重新整理**：以存放區中的最新資料重新整理報表
   * **變更圖例色彩**：選取並變更報表圖例的顏色
   * **匯出至CSV**：將報表中的資料匯出並下載至逗號分隔的檔案

## 處理期間報表  {#process-duration-report}

「程式持續時間」報表會依每個執行個體已執行的天數來顯示Forms程式的執行個體數量。

### 執行處理作業持續時間報表的方式 {#to-execute-a-process-duration-report}

1. 若要在「程式報告」中檢視預先定義的報告，請前往 **程式報告** 樹狀檢視，按一下 **報表** 節點。
1. 按一下 **處理持續時間** 報告節點。

   ![process_duration_node](assets/process_duration_node.png)

   當您選取報表時， **報表引數** 面板會顯示在樹狀檢視的右側。

   ![長時間執行程式報告引數面板](assets/process_duration_params.png)

   参数:

   * **選取程式** (*強制*)：選取AEM Forms程式。

1. 按一下 **前往** 以執行報表。

   報告會顯示在 **報告** 「程式報告」視窗右側的面板。

   ![process_duration_report](assets/process_duration_report.png)

   使用右上角的選項 **報告** 面板，對報告執行下列操作。

   * **重新整理**：以存放區中的最新資料重新整理報表
   * **變更圖例色彩**：選取並變更報表圖例的顏色
   * **匯出至CSV**：將報表中的資料匯出並下載至逗號分隔的檔案

## 工作流程數量報告 {#workflow-volume-report}

「工作流程數量」報表會依行事曆日期顯示目前執行中及已完成的AEM Forms處理序執行個體數量。

### 執行工作流程磁碟區報告 {#to-execute-a-workflow-volume-report}

1. 若要在「程式報告」中檢視預先定義的報告，請前往 **程式報告** 樹狀檢視，按一下 **報表** 節點。
1. 按一下 **工作流程數量** 報告節點。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   當您選取報表時， **報表引數** 面板會顯示在樹狀檢視的右側。

   ![長時間執行程式報告引數面板](assets/workflow_volume_params.png)

   参数:

   * **選取程式** (*強制*)：選取AEM Forms程式。

   * **開始晚於** (*可選*)：選取日期。 篩選報告以顯示指定日期後開始的流程例項。

   * **開始於以下日期之前** (*可選*)：選取日期。 篩選報告以顯示指定日期之前開始的流程例項。

1. 按一下 **前往** 以執行報表。

   報告會顯示在 **報告** 右側面板 **程式報告** 視窗。

   ![workflow_volume_report](assets/workflow_volume_report.png)

   使用右上角的選項 **報告** 面板，對報告執行下列操作。

   * **重新整理**：以存放區中的最新資料重新整理報表
   * **變更圖例色彩**：選取並變更報表圖例的顏色
   * **匯出至CSV**：將報表中的資料匯出並下載至逗號分隔的檔案
