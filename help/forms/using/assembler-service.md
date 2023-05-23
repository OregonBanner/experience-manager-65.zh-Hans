---
title: 使用組合器服務
seo-title: Using Assembler Service
description: 組合器服務可讓您組合、重新排列和增加PDF和XDP檔案，並取得有關PDF檔案的資訊。
seo-description: The Assembler service lets you combine, rearrange, and augment PDF and XDP documents and obtain information about PDF documents.
uuid: 1efce50b-2d98-408e-aa43-ac4999de41a8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 6a99042f-79c7-494b-bca0-73f2b5725b58
docset: aem65
exl-id: 2acd6b19-0fe8-4994-b0f4-c9d5b9f3fdf1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 6%

---

# 使用組合器服務{#using-assembler-service}

組合器服務可讓您組合、重新排列和增加PDF和XDP檔案，並取得有關PDF檔案的資訊。 提交至Assembler服務的每個工作都包含檔案描述XML (DDX)檔案、來原始檔以及外部資源（字串和圖形）。 如需關於組合器服務的詳細資訊，請參閱 [組合器服務概要](../../forms/using/overview-aem-document-services.md#p-assembler-service-p).

您可將組裝服務用於下列操作：

## 汇编 PDF 文档 {#assemble-pdf-documents}

您可以使用「組合器」服務，將兩個或多個PDF檔案組合成單一PDF檔案或PDFPortfolio。 您也可以將輔助導覽或增強安全性的功能套用至PDF檔案。 以下是可用于汇编 PDF 文档的一些方法：

### 汇编一个简单的 PDF 文档 {#assemble-a-simple-pdf-document}

下圖顯示三個來原始檔合併為單一結果檔案。

![從多個PDF檔案組合簡單PDF檔案](assets/as_document_assembly.png)

從多個PDF檔案組合簡單PDF檔案

以下範例是用於組裝檔案的簡單DDX檔案。 它指定用來產生產生結果檔案的來原始檔的名稱，以及結果檔案的名稱：

```xml
<PDF result="Doc4">
<PDF source="Doc1"/>
<PDF source="Doc2"/>
<PDF source="Doc3"/>
</PDF>
```

檔案元件會產生一份包含下列內容和\
特性：

* 每個來原始檔的全部或部分
* 來自每個來原始檔的全部或部分書籤，針對組合結果檔案標準化
* 從基礎檔案(Doc1)採用的其他特性，包括中繼資料、頁面標籤和頁面大小
* 或者，產生的檔案會包括由來原始檔中的書籤建構的目錄

### 创建 PDF 文档组合 {#create-a-pdf-portfolio}

Assembler服務可建立包含檔案集合和自含式使用者介面的PDFPortfolio。 此介面稱為「PDFPortfolio配置」或「PDFPortfolio導覽器（導覽器）」。 PDFPortfolio透過新增導覽器、資料夾和歡迎頁面來擴展PDF套件的功能。 此介面可運用當地語系化的文字字串、自訂色彩配置和圖形資源，提升使用者體驗。 PDFPortfolio也可以包含用來組織投資組合中檔案的資料夾。

組合器服務解譯下列DDX檔案時，會組合一個PDFPortfolio，其中包括PDFPortfolio導覽器和兩個檔案的套件。 服務會從myNavigator來源指定的位置取得瀏覽器。 它會將瀏覽器的預設色彩配置變更為粉紅Scheme色彩配置。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1">
<Portfolio>
<Navigator source="myNavigator"/>
<ColorScheme scheme="pinkScheme"/>
</Portfolio>
<PackageFiles>
<PDF source="sourcePDF1"/>
<PDF source="sourcePDF2"/>
</PackageFiles>
</PDF>
</DDX>
```

### 汇编加密的文档 {#assemble-encrypted-documents}

當您組合檔案時，也可以使用密碼對PDF檔案進行加密。 使用密碼加密PDF檔案後，使用者必須指定密碼，才能在Adobe Reader或Acrobat中檢視PDF檔案。 若要使用密碼加密PDF檔案，DDX檔案必須包含加密PDF檔案所需的加密元素值。

加密服務不一定要成為LiveCycle安裝的一部分，才能使用密碼加密PDF檔案。

如果一個或多個輸入檔案已加密，請提供密碼以開啟檔案作為DDX的一部分。

### 使用 Bates 编号汇编文档 {#assemble-documents-using-bates-numbering}

當您組合檔案時，可以使用Bates編號來將唯一的頁面識別碼套用到每個頁面。 當您使用Bates編號時，檔案（或檔案集）中的每一頁都會被指定唯一識別該頁面的編號。 例如，包含用料表資訊且與組裝料號生產相關聯的製造檔案可以包含識別碼。 Bates數字包含循序遞增的數值，以及選用的首碼和尾碼。 前置詞+數值+後置詞稱為Bates模式。

下圖顯示的PDF檔案包含位於檔案標題中的唯一識別碼。

![包含位於檔案標題中唯一識別碼的PDF檔案](do-not-localize/as_batesnumber.png)

包含位於檔案標題中唯一識別碼的PDF檔案

### 合并和汇编文档 {#flatten-and-assemble-documents}

您可以使用Assembler服務將互動式PDF檔案（例如表單）轉換為非互動式PDF檔案。 互動式PDF檔案可讓使用者輸入或修改位於PDF檔案欄位中的資料。 將互動式PDF檔案轉換為非互動式PDF檔案的程式稱為平面化。 當PDF檔案平面化時，表單欄位會保留其圖形外觀，但不再具有互動性。 平面化PDF檔案的一個原因是為了確保無法修改資料。 此外，與欄位關聯的指令碼不再運作。

當您建立由互動式PDF檔案組裝的PDF檔案時，組裝程式服務會先將表單平面化，然後再將它們組裝到結果檔案中。

>[!NOTE]
>
>Assembler服務會使用Output服務來平面化動態XFA表單。 如果Assembler服務處理需要其平面化XFA動態表單的DDX，且輸出服務無法使用，則會擲回例外狀況。 組合器服務可平面化Acrobat表單或靜態XFA表單，而不使用輸出服務。

## 組合XDP檔案 {#assemble-xdp-documents}

您可以使用Assembler服務，將多個XDP檔案組合成單一XDP檔案或PDF檔案。 對於包含插入點的來源XDP檔案，您可以指定要插入的片段。

以下是組裝XDP檔案的一些方法：

### 組合簡單XDP檔案 {#assemble-a-simple-xdp-document}

下圖顯示三個來源XDP檔案正在組裝成單一結果XDP檔案。 產生的XDP檔案包含三個來源XDP檔案，包括其關聯資料。 產生的檔案會從基礎檔案（第一個來源XDP檔案）取得基本屬性。

![從多個XDP檔案組合一個簡單的XDP檔案](assets/as_assembler_xdpassembly.png)

從多個XDP檔案組合一個簡單的XDP檔案

以下是產生上述結果的DDX檔案。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="MyXDPResult">
<XDP source="sourceXDP1"/>
<XDP source="sourceXDP2"/>
<XDP source="sourceXDP3"/>
</XDP>
</DDX>
```

### 在組裝期間解析參照 {#resolving-references-during-assembly}

通常，XDP檔案可以包含透過絕對或相對參照參照的影像。 依預設，組合器服務會保留對產生XDP檔案中影像的參照。

您可以指定Assembler服務在組裝時如何透過XDP檔案中的絕對或相對參照來處理來源XDP檔案中參照的影像。 您可以選擇將所有影像內嵌在結果中，使其不包含相對或絕對參照。 您可透過設定resolveAssets標籤的值來定義此屬性，此值可使用下列任一選項。 依預設，結果檔案中不會解析任何參照。

<table>
 <tbody> 
  <tr> 
   <th>价值</th> 
   <th>描述</th> 
  </tr> 
  <tr> 
   <td>无</td> 
   <td>不會解析任何參照。</td> 
  </tr> 
  <tr> 
   <td>全部</td> 
   <td>將所有參照的影像內嵌在來源XDP檔案中。</td> 
  </tr> 
  <tr> 
   <td>相对</td> 
   <td>在來源XDP中嵌入透過相對參照參照參照的所有影像<br /> 檔案。</td> 
  </tr> 
  <tr> 
   <td>绝对</td> 
   <td>在來源XDP中嵌入透過絕對參照參照的所有影像<br /> 檔案。</td> 
  </tr> 
 </tbody> 
</table>

您可以在XDP來源標籤或父XDP結果標籤中指定resolveAssets屬性的值。 如果將屬性指定給XDP結果標籤，則它將被作為XDP結果子項的所有XDP來源元素繼承。 但是，明確指定來源元素的屬性會覆寫該來原始檔的結果元素設定。

#### 解析XDP檔案中的所有來源參照 {#resolve-all-source-references-in-an-xdp-document}

若要解析來源XDP檔案中的所有參照，請為下列專案指定resolveAssets屬性：\
結果檔案變更為全部，如下列範例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
<XDP source="input3.xdp" />
</XDP>
</DDX
```

您也可以單獨指定所有來源XDP檔案的屬性，以獲得相同的屬性\
个结果.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp">
<XDP source="input1.xdp" resolveAssets="all"/>
<XDP source="input2.xdp" resolveAssets="all"/>
<XDP source="input3.xdp" resolveAssets="all"/>
</XDP>
</DDX>
```

#### 解析XDP檔案中選取的來源參照 {#resolve-selected-source-references-in-an-xdp-document}

您可以透過指定來源參照的resolveAssets屬性，選擇性地指定要解析的來源參照。 個別來原始檔的屬性會覆寫結果XDP檔案的設定。 在此範例中，也會解析包含的片段。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" >
<XDPContent source="fragment.xdp" insertionPoint="MyInsertionPoint"
fragment="myFragment"/>
</XDP>
<XDP source="input2.xdp" />
</XDP>
</DDX>
```

#### 選擇性解析絕對或相對參照 {#selectively-resolve-absolute-or-relative-references}

您可以選擇性地解析所有或部分來原始檔中的絕對或相對參照，如下列範例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="absolute">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
</XDP>
</DDX
```

### 動態地將表單片段插入XFA表單 {#dynamically-insert-form-fragments-into-an-xfa-form}

您可以使用Assembler服務來建立XFA表單，該表單是從片段插入到的其他XFA表單建立的。 使用此功能，您可以使用片段來建立多個表單。

支援動態插入表單片段，支援單一原始碼控制。 您可維護常用元件的單一來源。 例如，您可以為公司橫幅建立片段。 如果橫幅變更，您只需修改片段。 包含片段的其他表單則維持不變。

表單設計人員使用LiveCycle設計人員來建立表單片段。 這些片段在XFA表單中具有唯一名稱的子表單。 表單設計人員也使用Designer來建立具有唯一名稱插入點的XFA表單。 您（程式設計人員）會撰寫DDX檔案，指定如何將片段插入XFA表單。

下圖顯示兩個XML表單（XFA範本）。 左邊的表單包含一個名為myInsertionPoint的插入點。 右邊的表單包含一個名為myFragment的片段。

![將表單片段插入XFA表單](assets/as_assembler_fragment_assy_assembled.png)

將表單片段插入XFA表單

組合器服務解譯下列DDX檔案時，會建立包含其他XML表單的XML表單。 來自myFragmentSource檔案的myFragment子表單插入myFormSource檔案的myInsertionPoint。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="myFormResult">
<XDP source="myFormSource">
<XDPContent fragment="myFragment" insertionPoint="myInsertionPoint"
source="myFragmentSource"/>
</XDP>
</XDP>
</DDX
```

### 將XDP檔案封裝為PDF {#package-an-xdp-document-as-pdf}

您可以使用Assembler服務將XDP檔案封裝為PDF檔案，如此DDX檔案所示。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1" encryption="passEncProfile1">
<XDP>
<XDP source="sourceXDP3"/>
<XDP source="sourceXDP4"/>
</XDP>
</PDF>
</DDX>
```

## 拆分 PDF 文档 {#disassemble-pdf-documents}

您可以使用「組合器」服務來分解PDF檔案。 此服務可以從來原始檔中擷取頁面，或依據書籤分割來原始檔。 通常，如果 PDF 文档最初是从多个单独文档（例如对帐单集合）创建的，则此任务很有用。

### 从源文档中提取页面 {#extract-pages-from-a-source-document}

在下圖中，頁面1-3會從來原始檔中擷取，並放置在新的結果檔案中。

![從來原始檔擷取特定頁面](assets/as_intro_page_extraction.png)

從來原始檔擷取特定頁面

以下範例是用來拆解檔案的DDX檔案。

```xml
<PDF result="Doc4">
<PDF source="Doc2" pages="1-3"/>
</PDF>
```

### 根据书签拆分源文档 {#divide-a-source-document-based-on-bookmarks}

在下圖中，DocA會分成多個結果檔案。 頁面上的第一個1級書籤會識別新結果檔案的開頭。

![根據書籤將來原始檔分割為多個檔案](assets/as_intro_pdfsfrombookmarks.png)

根據書籤將來原始檔分割為多個檔案

以下範例是DDX檔案，它使用書籤來拆解來原始檔。

```xml
<PDFsFromBookmarks prefix="A">
<PDF source="DocA"/>
</PDFsFromBookmarks>
```

## 判斷檔案是否符合PDF/A標準 {#determine-whether-documents-are-pdf-a-compliant}

您可以使用Assembler服務來判斷PDF檔案是否符合PDF/A標準。 PDF/A 是一种用于长期保存文档内容的存档格式。字体将嵌入到文档中，并且文件是未压缩的。因此，PDF/A 文档通常比标准 PDF 文档大。此外，PDF/A 文档不包含音频和视频内容。

## 取得PDF檔案的相關資訊 {#obtain-information-about-a-pdf-document}

您可以使用Assembler服務來取得有關PDF檔案的下列資訊：

* 文字資訊。

   * 檔案每一頁上的文字
   * 檔案每一頁上的每個字的位置
   * 檔案每一頁各段落中的句子

* 書籤，包括頁碼、標題、目的地和外觀。 您可以匯出此\
   PDF檔案中的資料，並將其匯入PDF檔案中。

* 檔案附件，包括檔案資訊。 對於頁面層級附件，它也包含\
   檔案附件附註的位置。 您可以從PDF檔案匯出此資料，並且\
   將其匯入至PDF檔案。

* 封裝檔案，包括檔案資訊、資料夾、封裝、結構描述和欄位資料。 您可以從PDF檔案匯出此資料，並將其匯入PDF檔案。

## 驗證DDX檔案 {#validate-ddx-documents}

您可以使用組合器服務來判斷DDX檔案是否有效。 例如，如果您從先前的LiveCycle版本升級，則驗證會確保您的DDX檔案有效。

## 呼叫其他服務 {#call-other-services}

您可以使用DDX檔案，讓Assembler服務呼叫下列LiveC週期服務。 Assembler服務只能呼叫那些與LiveCycle一起安裝的服務。

**Reader擴充功能服務**：可讓Adobe Reader使用者以數位方式簽署產生的PDF檔案。

**Forms服務**：合併XDP檔案和XML資料檔案，以產生包含已填互動式表單的PDF檔案。

**輸出服務**：將動態XML表單轉換為包含非互動式表單的PDF檔案（將表單平面化）。 Assembler服務會平面化靜態XML表單和Acrobat表單，而不需呼叫Output服務。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="outDoc">
<PDF source="doc1"/>
<PDF source="doc2"/>
<ReaderRights
credentialAlias="LCESCred"
digitalSignatures="true"/>
</PDF>
</DDX>
```

使用DDX和Assembler服務呼叫其他LiveC週期服務可簡化您的程式圖。 這甚至可以減少您自訂工作流程所花費的精力。 (另请参阅
