---
title: 匯入和匯出PDF產生器組態檔
seo-title: Importing and exporting PDF Generator configuration files
description: 瞭解如何匯入和匯出PDF產生器組態檔。
seo-description: Learn how to import and export PDF Generator configuration files.
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
feature: PDF Generator
exl-id: b363b23a-29bb-4ea4-a8f2-5ba9fe3c7b27
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# 匯入和匯出PDF產生器組態檔 {#importing-and-exporting-pdf-generator-configuration-files}

組態檔包含PDF產生器轉換資訊，包括PDF、檔案型別和安全性設定。

>[!NOTE]
>
>無法透過匯入自訂native2pdfconfig.xml檔案來變更PDF產生器的逾時設定。 該檔案中的逾時設定僅供參考，並在PDF產生器中顯示目前的設定。 若要變更逾時設定，請參閱以下的「設定PDF產生器效能引數」： [安裝和部署AEM表單](https://www.adobe.com/go/learn_aemforms_installJBoss_63).

## 匯出您目前的組態檔 {#export-your-current-configuration-file}

1. 在Administration Console中，按一下「服務>PDF產生器>組態檔>匯出組態」。
1. 若要匯出設定，請選取適當的選項：

   * 若要匯出所有已命名的設定，請選取「下載整個設定」。
   * 若只要匯出一個Adobe PDF設定、安全性設定或檔案型別設定，請選取「下載最低設定」。

      如果您要匯出最小組態，請選取要匯出的Adobe PDF、安全性及檔案型別設定。

1. 按一下「下載」 ，並將XML檔案儲存在適當的位置。

## 匯入組態檔 {#import-a-configuration-file}

>[!NOTE]
>
>您的系統將根據匯入檔案中的資訊重新設定。

1. 在Administration Console中，按一下「服務>PDF產生器>組態檔>匯入組態」。
1. 選取「匯入現有的組態檔」。
1. 若要在「組態檔案」方塊中指定檔案位置，請按一下「瀏覽」來尋找並選取檔案，然後按一下 **匯入**.

## 轉換AutoCAD檔案中的所有圖層 {#convert-all-layers-within-autocad-files}

根據預設，「PDF產生器」只會將AutoCAD檔案的預設圖層轉換為PDF，而不是檔案中的所有圖層。 若要轉換所有圖層，請遵循此程式。

1. 在Administration Console中，按一下「服務>PDF產生器>組態檔>匯出組態」。
1. 選取「下載整個設定」，然後按一下「下載」。
1. 在文字編輯器中，開啟下載的檔案，並在 `AutoCAD` 標籤內 `PDFMaker` 標籤，新增文字 `convertAllPages="true"`.
1. 在Administration Console中，按一下「服務>PDF產生器>組態檔>匯入組態」。
1. 選取「匯入現有的組態檔」，指定更新的檔案，然後按一下「匯入」。

   使用修改過的組態檔案轉換的任何AutoCAD檔案都會轉換所有圖層。

## 將您的設定重設為隨PDF產生器安裝的原始設定 {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. 在Administration Console中，按一下「服務>PDF產生器>組態檔>匯入組態」。
1. 選取「重設組態至預設設定」，然後按一下「匯入」。
