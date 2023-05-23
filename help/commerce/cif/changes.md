---
title: Commerce Integration Framework (CIF)附加元件的重大變更
description: 與舊版CIF相比，Commerce Integration Framework (CIF)附加元件發生重大變更。
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
source-git-commit: a2ababa9dd9115e963b91a7271d204d287557c40
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# Commerce Integration Framework (CIF)附加元件的重大變更{#notable-changes}

本檔案著重說明Commerce Integration Framework (CIF)附加元件與舊CIF版本之間的重要差異，主要稱為CIF Classic (Quickstart)和CIF Open-source。

## 安裝與更新

AEM CIF附加元件套件會隨AEM Package Manager安裝並更新。

**舊版CIF**

* CIF Classic：不需要安裝，CIF是Quickstart的一部分。 CIF更新是定期AEM或Service Pack更新的一部分
* CIF開放原始碼：透過GitHub安裝。 更新是手動更新/維護工作的一部分。

## 端點設定

端點會透過OSGi主控台設定。

**舊版CIF**

* CIF Classic：透過AEM中的OSGi設定
* CIF開放原始碼：透過CIF設定瀏覽器

## 部署CIF Venia專案

專案可用日期 [GitHub AEM Guides - CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) 以及透過AEM Package Manager完成的部署。

**舊版CIF**

* CIF Classic：透過AEM套件安裝

## 產品目錄資料

透過對支援必要GraphQL API的外部端點的即時呼叫，可隨選要求產品目錄資料。 這些API支援在任何指定日期存取即時或分段資料。 不需要復寫。

**舊版CIF**

* CIF Classic：透過完整或差異產品匯入，即時和分階段產品資料匯入並儲存在AEM Author上的JCR中。 即時產品資料會複製到AEM Publish。

## 具有AEM轉譯的產品目錄體驗

AEM會使用已指派給產品和類別的AEM目錄範本，即時呈現產品目錄體驗。 不需要復寫。

**舊版CIF**

* CIF Classic： AEM作者會使用目錄Blueprint工具，為每個類別/產品建立AEM頁面。 這些頁面會復寫到AEM Publish。

>[!NOTE]
>
>如需如何搭配AEM Managed Service或AEM On-Premise使用CIF的其他檔案，請參閱 [Commerce整合框架](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
