---
title: 事务处理报告可开单API
seo-title: 事务处理报告可开单API
description: 作为事务处理的所有API的列表
seo-description: 作为事务处理的所有API的列表
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# 事务处理报告可开单API{#transaction-reports-billable-apis}

AEM Forms提供了多个API，用于提交表单、处理文档和渲染文档。 某些API作为事务处理入账，而其他API则免费使用。 本文档提供了在事务报告中作为事务处理入账的所有API的列表。 以下是使用收费API的几个常见情况：

* 提交自适应表单、HTML5表单和表单集
* 渲染交互式通信的打印版或Web版
* 将文档从一种格式转换为另一种格式
* 拼合动态PDF文档
* 生成记录文档
* 将交互式PDF文档与另一PDF文档合并
* 使用AEM工作流的分配任务步骤和文档服务步骤
* 在自适应表单中使用自适应表单

付费API不考虑页数、文档或表单的长度或渲染文档的最终格式。 事务处理报表将事务处理分为两个类别：已渲染的文档和已提交的表单。

* **** 提交的表单：当从使用AEM Forms创建的任何类型的表单提交数据并且数据提交到任何数据存储存储库或数据库被视为表单提交。 例如，提交自适应表单、HTML5表单、PDF表单和表单集将作为提交的表单入账。 表单集中的每个表单都被视为提交。 例如，如果表单集有5个表单，则提交表单集时，事务报告服务会将其计为5个提交。

* **** 渲染的文档：通过组合模板和数据、对文档进行数字签名或认证、使用文档服务的可计费文档服务API或将文档从一种格式转换为另一种格式来生成文档，作为所呈现的文档入账。

>[!NOTE]
>
>事务处理报表UI显示三个类别：已提交的表单、已呈现的文档和已处理的文档。 渲染的文档和处理的文档均视为渲染的文档。

## 收费文档服务API {#billable-document-services-apis}

### 生成PDF服务 {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>事务处理报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>根据支持的文件类型创建Adobe PDF。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>根据支持的文件类型创建Adobe PDF。</td>
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">优化PDF</a></td>
   <td>优化PDF，通过删除不必要的元数据来减小文件大小，而不会影响质量。</td>
   <td>已处理的文档<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Distiller Service {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>事务处理报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>根据支持的文件类型创建Adobe PDF。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>根据支持的文件类型创建Adobe PDF。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 记录服务文档（DoR服务） {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>事务处理报告类别</td>
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
   <td>事务处理报告类别</td>
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
   <td> generatePDFOutputBatch API将表单模板与记录组合，并生成PDF。 在您处理一批记录时，事务处理报告服务会将每条记录计为单独的PDF再现。 <br> 您可以使用 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--"></a> getGenerateManyFiles标志将多个再现合并为单个PDF文件。 无论标记状态如何，服务都将每个记录计为单独的PDF再现。 </td>
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
   <td> generatePDFOutputBatch API将表单模板与记录组合，并生成PDF。 在您处理一批记录时，事务处理报告服务会将每条记录计为单独的PDF再现。 <br> 您可以使用 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--"></a> getGenerateManyFiles标志将多个再现合并为单个PDF文件。 无论标记状态如何，服务都将每个记录计为单独的PDF再现。 </td>
  </tr>
 </tbody>
</table>

### 表单服务 {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>事务处理报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>从XDP模板渲染PDF表单。 XP模板是在Forms Designer中创建的。</td>
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
   <td>事务处理报告类别</td>
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

### Barcoded Forms Service {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>事务处理报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">解码</a></td>
   <td>解码Document对象中的所有条码，并返回一个org.w3c.dom.Document对象，该对象包含从条形码检索到的数据。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 汇编器服务 {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>事务处理报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">调用</a></td>
   <td>执行指定的DDX文档并返回一个 <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> 对象，其中包含生成的文档。 </td>
   <td>已处理的文档</td>
   <td>下列业务不会作为交易入账：
    <ul>
     <li>创建包或包</li>
     <li>拼接多个XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">调用</a></td>
   <td>执行指定的DDX文档并返回一个 <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> 对象，其中包含生成的文档。 </td>
   <td>已处理的文档</td>
   <td>PDF Generator、Forms和Output服务支持的所有输入文件格式，Assembler服务都支持这些格式作为输出文件格式。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>使用指定的选项将指定文档转换为PDF/A。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 汇编程序服务的调用API可以根据输入在内部调用另一服务的可计费API。 因此，调用API可以作为无、单个或多个事务处理进行处理。 计数的事务数取决于输入和调用的内部API。
>* 使用汇编程序服务生成的单个PDF文档可以作为无、单个或多个事务处理进行处理。 计数的事务数取决于提供的DDX代码。
>



### PDF实用程序服务 {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>事务处理报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>将PDF文档转换为XDP文件。 要使PDF文档成功转换为XDP文件，PDF文档必须在AcroForm词典中包含XFA流。</td>
   <td>已处理的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 收费数据捕获API {#billable-data-capture-apis}

自适应表单、HTML5表单和表单集的所有提交事件都作为事务处理入账。 默认情况下，提交PDF表单不作为事务处理入账。 使用提供的 [事务记录器API](transaction-reports-billable-apis.md#recordingbillableapisastransactionsforcustomcode) ，将PDF表单提交记录为事务。

### 自适应表单 {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>用例</p> </td>
   <td>描述</td>
   <td>事务处理报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td>提交自适应表单</td>
   <td>提交自适应表单以配置提交操作。 </td>
   <td>已提交的表单</td>
   <td>
    <ul>
     <li>成功提交可完成一两个事务。 计数的事务处理数取决于用于提交的提交操作的类型。 例如，通过电子邮件提交操作帐户发送PDF可处理两个事务。 一个用于提交表单的事务，另一个用于使用记录文档(DOR)服务生成的PDF。 </li>
     <li>在自适应表单（自适应表单表单集）中使用自适应表单只会计入单个事务。 您可以在自适应表单中拥有任意数量的自适应表单。</li>
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
   <td>事务处理报告类别</td>
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
   <td>事务处理报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td>提交表单集</td>
   <td>将表单集提交到在表单集中配置的提交URL。</td>
   <td>已提交的表单</td>
   <td>
    <ul>
     <li>在自适应表单（自适应表单表单集）中使用自适应表单只会计入单个事务。 您可以在自适应表单中拥有任意数量的自适应表单。</li>
     <li>HTML5表单中的每个表单都将帐户设置为单独的事务。 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## OSGi API上的收费交互式通信和以表单为中心的AEM工作流 {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

在OSGi和交互式通信的所有演绎版上分配以表单为中心的AEM工作流的任务和文档服务步骤，并作为事务处理入账。 在创作实例上预览交互式通信和使用代理UI在发布实例上预览不会作为事务处理入账。 如果工作流步骤将事务处理计算在内，而工作流无法完成，则事务处理计数不会冲销。

### 交互通信 - Web 渠道 {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>事务处理报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td>渲染Web渠道</td>
   <td>打开交互式通信的Web版本。</td>
   <td>已渲染的文档</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>事务处理报告类别</td>
   <td>附加信息</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">渲染</a> （转换为PDF）</td>
   <td>生成交互式通信的PDF版本。</td>
   <td>已渲染的文档</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### OSGi上以表单为中心的AEM工作流 {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>用例</p> </td>
   <td>事务处理报告类别</td>
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
   <td>将交互式通信（打印渠道）从代理UI提交到工作流</td>
   <td>已渲染的文档</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 将收费API记录为自定义代码的事务处理 {#recording-billable-apis-as-transactions-for-custom-code}

诸如提交PDF表单、使用代理UI预览交互式通信、使用非标准表单提交和自定义实现等操作不会作为事务处理入账。 AEM Forms提供了一个API来记录事务等操作。 您可以从自定义实现调用API以记 [录事务](/help/forms/using/record-transaction-custom-implementation.md)。

## 相关文章 {#related-articles}

* [事务处理报告概述](../../forms/using/transaction-reports-overview.md)
* [查看和了解事务处理报表](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [记录自定义实现的事务](/help/forms/using/record-transaction-custom-implementation.md)

