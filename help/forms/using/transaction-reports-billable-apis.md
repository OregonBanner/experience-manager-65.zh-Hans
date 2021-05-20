---
title: 交易报表计费API
seo-title: 交易报表计费API
description: 作为交易入账的所有API的列表
seo-description: 作为交易入账的所有API的列表
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
exl-id: 1bc99f3b-3f28-4e74-b259-6ebddc11ffc5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1963'
ht-degree: 7%

---

# 交易报表计费API{#transaction-reports-billable-apis}

AEM Forms提供了多个API来提交表单、处理文档和渲染文档。 某些API作为交易入账，而其他API则可免费使用。 本文档提供了作为交易报表中的交易入账的所有API的列表。 以下是使用可计费API的一些常见情况：

* 提交自适应表单、HTML5表单和表单集
* 呈现交互式通信的打印版或Web版
* 将文档从一种格式转换为另一种格式
* 拼合动态PDF文档
* 生成记录文档
* 将交互式PDF文档与其他PDF文档合并
* 使用AEM Workflow的分配任务步骤和文档服务步骤
* 在自适应表单中使用自适应表单

帐单API不考虑页数、文档或表单的长度或渲染文档的最终格式。 事务报表将事务分为两类：已提交和Forms已提交的文档。

* **Forms已提交：** 从通过AEM Forms创建的任何类型的表单提交数据，并将数据提交到任何数据存储存储库或数据库时，都会被视为表单提交。例如，提交自适应表单、HTML5表单、PDF forms和表单集将作为提交的表单进行处理。 表单集中的每个表单都被视为提交。 例如，如果表单集有5个表单，则提交表单集后，交易报告服务会将其计为5次提交。

* **已呈现的文档：** 通过组合模板和数据、对文档进行数字签名或认证、使用可计费文档服务API进行文档服务，或将文档从一种格式转换为另一种格式来生成文档，均被视为已呈现的文档。

>[!NOTE]
>
>交易报表UI显示三个类别：Forms已提交、已提交的文档和已处理的文档。 所呈现的文档和已处理的文档均作为已呈现的文档入账。

## 计费文档服务API {#billable-document-services-apis}

### 生成PDF服务{#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易记录报表类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>从支持的文件类型创建Adobe PDF 。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>从支持的文件类型创建Adobe PDF 。</td>
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
   <td><p>从HTML页面创建PDF。</p> </td>
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
   <td>优化PDF以减小文件大小，方法是在不影响质量的情况下删除不必要的元数据。</td>
   <td>已处理的文档<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Distiller服务{#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易记录报表类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>从支持的文件类型创建Adobe PDF 。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>从支持的文件类型创建Adobe PDF 。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 记录服务文档（DoR服务）{#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易记录报表类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">render</a></td>
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
   <td>交易记录报表类别</td>
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
   <td> generatePDFOutputBatch API将表单模板与记录组合在一起，并生成PDF。 当您处理一批记录时，事务报表服务会将每个记录计为单独的PDF格式副本。 <br> 您可以使用getGenerateManyFiles <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--"></a> 标记将多个演绎版合并到单个PDF文件。无论标记状态如何，服务都会将每个记录计为单独的PDF呈现版本。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>将XDP和PDF文档转换为PostScript(PS)、打印机命令语言(PCL)和ZPL文件格式。 </td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>将XDP和PDF文档转换为PostScript(PS)、打印机命令语言(PCL)和ZPL文件格式。 </td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>将一组XDP和PDF文档转换为一组PostScript(PS)、打印机命令语言(PCL)和ZPL文件格式。 </td>
   <td>已处理的文档</td>
   <td> generatePDFOutputBatch API将表单模板与记录组合在一起，并生成PDF。 当您处理一批记录时，事务报表服务会将每个记录计为单独的PDF格式副本。 <br> 您可以使用getGenerateManyFiles <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--"></a> 标记将多个演绎版合并到单个PDF文件。无论标记状态如何，服务都会将每个记录计为单独的PDF呈现版本。 </td>
  </tr>
 </tbody>
</table>

### 表单服务 {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易记录报表类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>从XDP模板渲染PDF表单。 XP模板在Forms Designer中创建。</td>
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

### 转换PDF服务{#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易记录报表类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>将PDF文档转换为图像文档列表。 支持的图像格式为JPEG、JPEG2K、PNG和TIFF。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>使用选项规范中指定的选项将平面PDF文件转换为PostScript格式。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 条形码Forms服务{#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易记录报表类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">解码</a></td>
   <td>解码Document对象中的所有条形码，并返回一个org.w3c.dom.Document对象，该对象包含从条形码中检索的数据。</td>
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
   <td>交易记录报表类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">调用</a></td>
   <td>执行指定的DDX文档并返回包含生成文档的<a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a>对象。 </td>
   <td>已处理的文档</td>
   <td>下列业务不会入账为交易：
    <ul>
     <li>创建资源包或项目组合</li>
     <li>拼合多个XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">调用</a></td>
   <td>执行指定的DDX文档并返回包含生成文档的<a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a>对象。 </td>
   <td>已处理的文档</td>
   <td>汇编程序服务支持PDF生成器、Forms和输出服务支持的所有输入文件格式都支持这些格式作为输出文件格式。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>使用指定的选项将指定的文档转换为PDF/A。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 汇编程序服务的调用API可以根据输入在内部调用另一个服务的计费API。 因此，调用API可以计为无、单个或多个事务。 计数的事务数取决于输入和调用的内部API。
>* 使用汇编程序服务生成的单个PDF文档可以计为无、单个或多个事务。 计数的交易数取决于提供的DDX代码。

>



### PDF实用程序服务{#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易记录报表类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>将PDF文档转换为XDP文件。 要成功将PDF文档转换为XDP文件，PDF文档必须在AcroForm词典中包含XFA流。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 计费数据捕获API {#billable-data-capture-apis}

自适应表单、HTML5 Forms和表单集的所有提交事件都将作为交易记录入账。 默认情况下，提交PDF表单不会作为交易记录。 使用提供的[事务记录器API](record-transaction-custom-implementation.md)将PDF forms提交记录为事务。

### 自适应表单 {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>用例</p> </td>
   <td>描述</td>
   <td>交易记录报表类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td>提交自适应表单</td>
   <td>提交自适应表单以配置提交操作。 </td>
   <td>已提交的表单</td>
   <td>
    <ul>
     <li>成功提交仅考虑一两项交易。 计数的事务处理数取决于用于提交的提交操作类型。 例如，通过电子邮件提交操作帐户发送PDF，用于两个交易计数。 一个交易用于表单提交，另一个交易用于使用记录文档(DOR)服务生成的PDF。 </li>
     <li>在自适应表单（自适应表单集）中使用自适应表单只会计入单笔交易。 自适应表单中可以包含任意数量的自适应表单。</li>
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
   <td>交易记录报表类别</td>
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
   <td>交易记录报表类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td>提交表单集</td>
   <td>将表单集提交到在表单集中配置的提交URL。</td>
   <td>已提交的表单</td>
   <td>
    <ul>
     <li>在自适应表单（自适应表单集）中使用自适应表单只会计入单笔交易。 自适应表单中可以包含任意数量的自适应表单。</li>
     <li>HTML5 Forms表单中的每个表单都会将帐户设置为单独的事务。 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## OSGi API上的计费交互式通信和以表单为中心的AEM工作流{#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

在OSGi和交互式通信的所有演绎版上分配以表单为中心的AEM工作流的任务和文档服务步骤，并作为事务处理入账。 在创作实例上预览交互式通信和使用代理UI在发布实例上预览不会计为事务。 如果工作流步骤将事务处理入帐，且工作流无法完成，则事务处理计数不会冲销。

### 交互通信 - Web 渠道 {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易记录报表类别</td>
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

### 交互式通信 — 打印渠道{#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易记录报表类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> （转换为PDF）</td>
   <td>生成交互式通信的PDF版本。</td>
   <td>已渲染的文档</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### OSGi {#form-centric-aem-workflows-on-osgi}上以表单为中心的AEM工作流

<table>
 <tbody>
  <tr>
   <td><p>用例</p> </td>
   <td>交易记录报表类别</td>
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

## 将计费API记录为自定义代码{#recording-billable-apis-as-transactions-for-custom-code}的交易记录

诸如提交PDF表单、使用代理UI预览交互式通信、使用非标准表单提交和自定义实施等操作不会计为交易。 AEM Forms提供了一个API来记录此类操作（如交易）。 您可以从自定义实施中调用API以[记录事务](/help/forms/using/record-transaction-custom-implementation.md)。

## 相关文章{#related-articles}

* [交易报表概述](../../forms/using/transaction-reports-overview.md)
* [查看和了解交易报表](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [记录自定义实施的交易](/help/forms/using/record-transaction-custom-implementation.md)
