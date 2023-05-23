---
title: 输出服务
seo-title: Output Service
description: 說明輸出服務，它隸屬於AEM Document Services
seo-description: Describes Output Service, which is part of AEM Document Services
uuid: edddef59-b43c-486f-8734-3f97961ecf4d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 51ab91ff-c0c0-4165-ae02-f306e45eea03
docset: aem65
exl-id: 1b62e1c1-428d-4c0f-98a8-486f319fa581
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 6%

---

# 输出服务{#output-service}

## 概述 {#overview}

Output服務是OSGi服務，屬於AEM Document Services的一部分。 輸出服務支援各種輸出格式和AEM Forms Designer的輸出設計功能。 輸出服務可以轉換XFA範本和XML資料，以產生多種格式的列印檔案。

Output 服务使您能够创建应用程序，这些应用程序允许您：

* 使用 XML 数据填充模板文件来生成最终表单文档。
* 產生各種格式的輸出表單，包括非互動式PDF、PostScript、PCL和ZPL列印資料流。
* 从 XFA 表单 PDF 生成打印 PDF。
* 將多組資料與提供的範本合併，以大量產生PDF、PostScript、PCL和ZPL檔案。

>[!NOTE]
>
>輸出服務是32位元的應用程式。 在Microsoft Windows上，32位元應用程式最多可以使用2 GB的記憶體。 此限制也適用於輸出服務。

## 建立非互動式表單檔案 {#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

通常使用AEM Forms Designer建立範本。 此 `generatePDFOutput` 和 `generatePrintedOutput` Output服務的API可讓您直接將這些範本轉換為各種格式，包括PDF、PostScript、ZPL和PCL。

此 `generatePDFOutput` 作業會產生PDF，而 `generatePrintedOutput` 作業會產生PostScript、ZPL和PCL格式。 兩個操作的第一個引數都接受範本檔案的名稱(例如 `ExpenseClaim.xdp`)或包含範本的Document物件。 當您指定範本檔案的名稱時，也需指定內容根目錄作為包含範本的資料夾的路徑。 您可以使用以下任一專案指定內容根： `PDFOutputOptions` 或 `PrintedOutputOptions` 引數。 請參閱Javadoc以取得您可以使用這些引數指定之其他選項的詳細資訊。

第二個引數在產生輸出檔案時，接受與範本合併的XML檔案。

此 `generatePDFOutput` 作業也可以接受XFA型PDF表單作為輸入，並傳回PDF表單的非互動版本作為輸出。

## 產生非互動式表單檔案 {#generating-non-interactive-form-documents}

假設您有一或多個範本，且每個範本有多個XML資料記錄。

使用 `generatePDFOutputBatch` 和 `generatePrintedOutputBatch` Output服務的作業，用以產生每筆記錄的列印檔案。

您也可以將記錄合併成單一檔案。 這兩個操作都需使用四個引數。

第一個引數是Map，其中包含作為索引鍵的任意字串，以及作為值的範本檔案名稱。

第二個引數是不同的Map，其值是包含XML資料的Document物件。 該索引鍵與您為第一個引數指定的索引鍵相同。

的第三個引數 `generatePDFOutputBatch` 或 `generatePrintedOutputBatch` 屬於型別 `PDFOutputOptions` 或 `PrintedOutputOptions` （分別）。

引數型別與 `generatePDFOutput` 和 `generatePrintedOutput` 操作與具有相同的效果。

第四個引數為型別 `BatchOptions`，用來指定是否可以為每個記錄產生個別的檔案。 此引數的預設值為false。

兩者 `generatePrintedOutputBatch` 和 `generatePDFOutputBatch` 傳回型別的值 `BatchResult`. 值包含產生的檔案清單。 它也包含XML格式的中繼資料檔案，其中包含與產生的每個檔案相關的資訊。
