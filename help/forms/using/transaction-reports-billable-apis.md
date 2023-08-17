---
title: 交易报告可记帐API
seo-title: Transaction Reports Billable APIs
description: 作为交易入账的所有API的列表
seo-description: List of all the APIs that are accounted as transactions
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
exl-id: 1bc99f3b-3f28-4e74-b259-6ebddc11ffc5
source-git-commit: 4eb4a15961e7b6e83d9e8a38f34ad92d829cb9b6
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 7%

---

# 交易报告可记帐API{#transaction-reports-billable-apis}

AEM Forms提供了多个API来提交表单、处理文档和渲染文档。 某些API作为交易入账，而其他API则作为自由使用。 本文档提供了在交易报表中作为交易入账的所有API的列表。 以下是一些使用计费API的常见方案：

* 提交自适应表单、HTML5表单和表单集
* 呈现交互式通信的打印或Web版本
* 将文档从一种格式转换为另一种格式
* 拼合动态PDF文档
* 生成记录文档
* 将交互式PDF文档与另一个PDF文档合并
* 使用AEM Workflows的分配任务步骤和文档服务步骤
* 在自适应表单中使用自适应表单

计费API不考虑页数、文档或表单的长度或渲染文档的最终格式。 事务报表将事务分为两类：已渲染的文档和Forms已提交。

* **Forms已提交：** 如果从使用AEM Forms创建的任何类型的表单提交数据，并且将数据提交到任何数据存储存储库或数据库，则被视为表单提交。 例如，提交自适应表单、HTML5表单、PDF forms和表单集均被视为提交的表单。 表单集中的每个表单都被视为提交。 例如，如果一个表单集有5个表单，在提交该表单集时，transaction reporting服务将其计为5次提交。

* **呈现的文档：** 通过组合模板和数据来生成文档、对文档进行数字签名或认证、使用用于文档服务的可计费文档服务API或将文档从一种格式转换为另一种格式来生成文档，均被视为已渲染的文档。

>[!NOTE]
>
>交易报表UI显示三种类别：Forms已提交、已呈现文档和已处理的文档。 所呈现的文档和处理的文档均被视为所呈现的文档。

## 可记帐文档服务API {#billable-document-services-apis}

### 生成PDF服务 {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>从支持的文件类型创建Adobe PDF。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>从支持的文件类型创建Adobe PDF。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>将Adobe PDF转换为支持的文件类型。 </td>
   <td>已处理的文档<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>将Adobe PDF转换为支持的文件类型。 </td>
   <td>已处理的文档<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>将Adobe PDF转换为支持的文件类型。 </td>
   <td>已处理的文档<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>从HTML页创建PDF。</p> </td>
   <td>已处理的文档<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>从指向HTML页面的URL创建PDF。</td>
   <td>已处理的文档<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>从指向HTML页面的URL创建PDF。</td>
   <td>已处理的文档<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>优化PDF以通过去除不必要的元数据而减小文件大小，同时不影响质量。</td>
   <td>已处理的文档<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### DocAssurance服务 {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/docassurance/client/api/DocAssuranceService.html#secureDocument-com.adobe.aemfd.docmanager.Document-com.adobe.fd.docassurance.client.api.EncryptionOptions-com.adobe.fd.docassurance.client.api.SignatureOptions-com.adobe.fd.docassurance.client.api.ReaderExtensionOptions-com.adobe.fd.signatures.pdf.inputs.UnlockOptions-" target="_blank">secureDocument</a><br /> </td>
   <td>此API使您能够保护文档。 您可以使用该API对PDF文档进行签名、认证、阅读器扩展或加密。</td>
   <td>已处理的文档</td>
   <td>只对secureDocument的签名和认证操作收费。</td>
  </tr>
 </tbody>
</table>


### Distiller服务 {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>从支持的文件类型创建Adobe PDF。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>从支持的文件类型创建Adobe PDF。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 记录文档服务（DoR服务） {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">渲染</a></td>
   <td>调用指定的渲染方法以使用提供的参数生成记录文档。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 输出服务 {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>合并数据和模板以创建PDF文档。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>合并数据和模板以创建PDF文档。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td>
   <td>合并数据和模板以创建一组PDF文档。</td>
   <td>已处理的文档</td>
   <td> generatePDFOutputBatch API将表单模板与记录组合在一起，并生成PDF。 当您处理一批记录时，交易报告服务会将每个记录计为单独的PDF演绎版。 <br> 您可以使用 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFile</a> 用于将多个呈现组合为单个PDF文件的标记。 无论标志的状态如何，该服务都把每个记录计为单独的PDF演绎版。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>将XDP和PDF文档转换为PostScript (PS)、Printer Command Language (PCL)和ZPL文件格式。 </td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>将XDP和PDF文档转换为PostScript (PS)、Printer Command Language (PCL)和ZPL文件格式。 </td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>将一组XDP和PDF文档转换为一组PostScript (PS)、打印机命令语言(PCL)和ZPL文件格式。 </td>
   <td>已处理的文档</td>
   <td> generatePDFOutputBatch API将表单模板与记录组合在一起，并生成PDF。 当您处理一批记录时，交易报告服务会将每个记录计为单独的PDF演绎版。 <br> 您可以使用 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFile</a> 用于将多个呈现组合为单个PDF文件的标记。 无论标志的状态如何，该服务都把每个记录计为单独的PDF演绎版。 </td>
  </tr>
 </tbody>
</table>

### 表单服务 {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>渲染XDPPDF中的模板表单。 XP模板是在Forms Designer中创建的。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>从PDF表单或XDP模板提取数据</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 转换PDF服务 {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>将PDF文档转换为图像文档的列表。 支持的图像格式为JPEG、JPEG2K、PNG和TIFF。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>使用选项规范中指定的选项将FlatPDF文件转换为PostScript格式。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 条形码Forms服务 {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">解码</a></td>
   <td>解码Document对象中的所有条形码，并返回包含从条形码检索的数据的org.w3c.dom.Document对象。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 汇编程序服务 {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">调用</a></td>
   <td>执行指定的DDX文档并返回 <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">Assemblerresult</a> 包含结果文档的对象。 </td>
   <td>已处理的文档</td>
   <td>下列操作不作为交易入账：
    <ul>
     <li>创建资源包或项目组合</li>
     <li>拼接多个XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">调用</a></td>
   <td>执行指定的DDX文档并返回 <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">Assemblerresult</a> 包含结果文档的对象。 </td>
   <td>已处理的文档</td>
   <td>PDF Generator、Forms和输出服务支持的所有输入文件格式，汇编程序服务支持所有这些格式作为输出文件格式。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>使用指定的选项将指定的文档转换为PDF/A。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

调用被视为事务，取决于正在执行的操作。 当您执行以下一个或多个操作时，它将被视为事务处理：
1. 非PDF格式到PDF格式的转换。 例如，XDP格式到PDF格式的转换（对于交互和非交互通信），Word到PDF的转换。
1. PDF格式到PDF/A格式的转换。
1. PDF格式到非PDF格式的转换。 例如，PDF格式到图像格式的转换，PDF格式到文本的格式转换。


>[!NOTE]
>
>* 汇编器服务的调用API可以在内部调用另一个服务的可计费API，具体取决于输入。 因此，调用API可以计为无、单个或多个事务。 计算的事务数取决于输入和调用的内部API。
>* 使用汇编程序服务生成的单个PDF文档可计为无、单个或多个事务。 计算事务数的数量取决于提供的DDX代码。

### PDF实用程序服务  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>将PDF文档转换为XDP文件。 若要成功将PDF文档转换为XDP文件，PDF文档必须在AcroForm词典中包含XFA流。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 计费数据捕获API {#billable-data-capture-apis}

自适应表单、HTML5 Forms和表单集的所有提交事件都将计为交易。 默认情况下，提交PDF表单不会作为交易记帐。 使用提供的 [交易记录器API](record-transaction-custom-implementation.md) 将PDF forms提交记录为事务处理。

### 自适应表单 {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>用例</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td>提交自适应表单</td>
   <td>提交自适应表单以配置提交操作。 </td>
   <td>已提交的表单</td>
   <td>
    <ul>
     <li>成功提交单个或两个交易的帐户。 计算的交易记录数取决于用于提交的提交操作的类型。 例如，通过电子邮件发送PDF提交操作会记录两次交易。 一个用于表单提交的事务处理，另一个用于使用记录文件(DOR)服务生成的PDF的事务处理。 </li>
     <li>在自适应表单（自适应表单集）中使用自适应表单只能处理单个交易。 一个自适应表单中可以有任意数量的自适应表单。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### HTML5 表单 {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>用例</p> </td>
   <td>描述 </td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td>提交HTML5表单</td>
   <td>提交HTML5表单以提交在表单中配置的URL。</td>
   <td>已提交的表单</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 表单集 {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td>提交表单集</td>
   <td>将表单集提交到表单集中配置的提交URL。</td>
   <td>已提交的表单</td>
   <td>
    <ul>
     <li>在自适应表单（自适应表单集）中使用自适应表单只能处理单个交易。 一个自适应表单中可以有任意数量的自适应表单。</li>
     <li>HTML5 Forms表单中的每个表单都会将帐户设置为单独的交易。 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## OSGi API上的可计费交互式通信和以表单为中心的AEM工作流 {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

在OSGi上分配以表单为中心的AEM Workflows的任务和文档服务步骤以及交互式通信的所有演绎版，并作为事务入账。 在创作实例上预览交互式通信和使用代理UI在发布实例上预览不会计为事务。 如果工作流步骤将事务处理入帐，但工作流未能完成，则不会冲销事务处理计数。

### 交互通信 - Web 渠道 {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td>呈现Web渠道</td>
   <td>打开交互式通信的Web版本。</td>
   <td>已渲染的文档</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### 交互式通信 — 打印渠道 {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">渲染</a> (转换为PDF)</td>
   <td>生成交互式通信的PDF版本。</td>
   <td>已渲染的文档</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### OSGi上以表单为中心的AEM工作流  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>用例</p> </td>
   <td>交易报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td>提交分配任务步骤</td>
   <td>已提交的表单</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>提交工作流应用程序起点 </td>
   <td>已提交的表单</td>
   <td> </td>
  </tr>
  <tr>
   <td>从代理UI向工作流提交交互式通信（打印渠道）</td>
   <td>已渲染的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 将可记帐API记录为自定义代码的交易 {#recording-billable-apis-as-transactions-for-custom-code}

提交PDF表单、使用代理UI预览交互式通信、使用非标准表单提交和自定义实现等操作不计入事务。 AEM Forms提供了一个API，用于将此类操作记录为交易。 您可以从自定义实施中调用API以 [记录交易](/help/forms/using/record-transaction-custom-implementation.md).

## 相关文章 {#related-articles}

* [交易报表概述](../../forms/using/transaction-reports-overview.md)
* [查看和了解事务处理报表](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [记录自定义实施的交易](/help/forms/using/record-transaction-custom-implementation.md)
