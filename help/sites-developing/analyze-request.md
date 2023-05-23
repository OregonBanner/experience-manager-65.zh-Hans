---
title: Request Analysis指令碼
seo-title: Request Analysis Script
description: 製作Request Analysis Script是為了方便分析access.log檔案，產生可讀報告以供日後處理
seo-description: The request analysis script is made to ease the analysis of the access.log files producing a readable report for later processing
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# Request Analysis指令碼{#request-analysis-script}

## 下载 {#download}

製作此指令碼是為了方便分析 `access.log` 產生可讀報告以供日後處理的檔案。

[获取文件](assets/analyse-access.sh)

## 描述 {#description}

製作此指令碼是為了方便分析 `access.log` 產生可讀報告以供日後處理的檔案。

它會產生整體請求數量、GET與POST、請求隨時間分佈等等。

輸出為Markdown語法，因此將更容易轉換為使用pandoc等PDF的工具，或使用Markdown檢視器等外掛程式在瀏覽器中顯示。

它可以分析命令列上提供的自訂路徑。

從檔案內告訴您如何執行的註解中獲取：

分析CQ `access.log` 推斷各種資訊並產生Markdown輸出 `stdout`.

## 用途 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

您可以在命令列上提供其他要分析的自訂路徑

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

您可以使用簡單管路儲存輸出

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
