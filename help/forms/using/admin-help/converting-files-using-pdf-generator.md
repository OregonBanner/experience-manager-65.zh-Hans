---
title: 使用PDF生成器转换文件
seo-title: Converting files using PDF Generator
description: 了解如何使用PDF生成器转换文件。
seo-description: Learn how to convert files using PDF Generator.
uuid: 295afb8f-130a-44f5-b0ab-e4c93c0c9e52
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 999ae2be-56ba-48c1-861b-8d4c991a0206
feature: PDF Generator
exl-id: 0e2c12b5-24c8-4aca-8826-cb661051ce4f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# 使用PDF生成器转换文件{#converting-files-using-pdf-generator}

您可以使用PDF生成器网页来转换文件。

## 创建PDF文件 {#create-a-pdf-file}

1. 在管理控制台中，单击服务>PDF生成器>创建PDF。
1. 单击“浏览”查找并选择文件。

   >[!NOTE]
   >
   >PDF生成器能够自动检测.doc、.xls、.ppt和.rtf文件的文件类型，即使文件名缺少文件扩展名也是如此。 此功能不适用于.docx、.xlsx和.pptx文件。

1. 在配置设置下，选择使用自定义设置或上传设置文件。

   * 如果您使用的是自定义设置，请选择Adobe PDF设置、安全设置和文件类型设置，并指定超时。

      Adobe PDF设置仅适用于PS到PDF、EPS到PDF、PRN到PDF、打开OCR的图像到PDF以及本机到PDF的转换。 超时设置指定完成转换所需的最长时间。 默认值为270秒。 在图像到PDF和OpenOffice到PDF转换期间不使用这些设置。

   * 如果要上载设置文件，请在框中键入其路径和名称，或单击“浏览”查找并选择该文件。

1. （可选）在XMP元数据文件下，键入XMP文件的路径和名称，或单击浏览查找并选择该文件。 XMP文件可用于包含标准元数据信息。 (请参阅 [关于XMP文件](converting-files-using-pdf-generator.md#about-xmp-files).)
1. 单击创建。创建文件后，将显示指向该文件的链接。 如果在转换过程中出现错误，则会显示警告。 如果您正在创建Postscript文件，警告中还会包含指向日志文件的链接。
1. 单击PDF文件的链接。 文件将在Acrobat中打开。

### 关于XMP文件 {#about-xmp-files}

PDF生成器在Acrobat 5.0或更高版本中创建的PDF文档包含XML格式的文档元数据。 *元数据* 包括有关文档及其内容的信息，如作者姓名、关键字和搜索实用程序可以使用的版权信息。

文档元数据包含（但不限于）也显示在Acrobat中“文档属性”对话框的“描述”选项卡上的信息。 在“描述”选项卡中所做的更改将反映在文档元数据中。 可以使用第三方产品扩展和修改文档元数据。

Adobe可扩展元数据平台(XMP)为Adobe应用程序提供了一个通用的XML框架，该框架标准化了跨发布工作流的文档元数据的创建、处理和交换。 您可以以XMP格式保存和导入文档元数据XML源代码，以便在不同文档之间共享元数据。 有关XMP文件的更多信息，请参阅 [可扩展元数据平台(XMP)](https://www.adobe.com/products/xmp/) 和 [AdobeXMP开发人员中心](https://www.adobe.com/devnet/xmp.html).

您可以在Acrobat中创建XMP文件。

## 将HTML文件或ZIP文件转换为PDF {#convert-an-html-file-or-zip-file-to-pdf}

您可以使用PDF生成器将以下类型的文件转换为Adobe PDF：

* HTML文件，您可以通过上传HTML文件或指定网页或网站的URL来转换这些文件。
* 存档文件(ZIP)，可以包含HTML文件或图像文件，或同时包含两者。

如果ZIP文件在其文件夹层次结构的最低级别包含多个HTML文件，则ZIP文件还必须包含index.htm或index.html文件。

>[!NOTE]
>
>* “HTMLPDF”功能要求在system font目录中使用某些字体。 在Linux、Solaris和AIX系统上，系统字体目录必须包含Courier字体。 在Windows系统上，系统字体目录必须包含Times New Roman。
>
>* （仅限基于UNIX的系统）在AEM Forms服务器上应使用以下日语字体之一，以将使用日语字体的网页转换为PDF文档。
>
>  * “萨扎纳米哥特语”
>  * “Kozuka Gothic专业版VI”
>  * “Kozuka Mincho专业版VI”
>  * “萨扎纳米哥特语”
>  * &quot;Kozuka Mincho Pr6N&quot;
>  * “萨扎纳米米米乔”
>  * “Adobe黑地标准时间”
>  * “Adobe Song标准”
>
>* 要从本地文件系统上传文件，请使用“HTMLPDF”页上的“上传文件”选项。


1. 在管理控制台中，单击服务>PDF生成器>要PDF的HTML。
1. 通过执行以下任务之一指定要转换的文件：

   * 在上传文件中，键入HTML文件或ZIP文件的路径和文件名，或单击“浏览”找到并选择该文件。
   * 在指定URL框中，键入要转换的页面或网站的URL。

   >[!NOTE]
   >
   >要转换的文件必须具有.html、.htm或.zip文件扩展名。

1. 指定配置设置：

   * 要使用自定义设置，请选择使用自定义设置，指定安全和文件类型设置，并指定超时值。 默认值为270秒。
   >[!NOTE]
   >
   >如果将“生成PDF”服务配置为使用Acrobat WebCapture，则在此页上选择的“文件类型设置”不会影响生成的PDF。 而是应该对服务器上安装的Acrobat版本进行适当的更改。

   * 要使用现有设置文件，请选择“上载设置文件”，然后单击“浏览”转到文件位置。


1. 要上传XMP文件，请单击“浏览”并转到文件位置。 XMP文件可用于包含标准元数据信息。 (请参阅 [关于XMP文件](converting-files-using-pdf-generator.md#about-xmp-files).)
1. 单击创建。创建文件后，将显示指向PDF文件的链接。
1. 单击该链接可在Acrobat中查看PDF文档。

## 将PDF文件导出为其他文件格式（仅限Windows） {#export-a-pdf-file-to-another-file-format-windows-only}

您可以将PDF文件导出为各种文件格式，如的生成PDF服务一章中所述 [服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

1. 在管理控制台中，单击服务>PDF生成器>Export PDF。
1. 单击“浏览”找到要导出的PDF文件。
1. 在要列出的Export PDF文件中，选择要导出PDF文件的格式。
1. 在指定超时框中，输入应用程序超时前等待的时间。 默认值为270秒。

   转换文件时显示的转换时间可能大于您在此处指定的值。 转换时间包括等待线程或进程所花费的时间、转换文件所花费的时间，以及回退转换器所花费的时间（如果适用）。 次. Specify a Timeout值只是转换文件所用的时间。

1. （可选）在 **指定自定义印前检查配置文件** 选项，单击浏览，然后选择 [自定义印前检查配置文件](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html). 仅在将文档转换为PDF存档(PDF/A)格式时使用印前检查配置文件。
1. 单击“导出”。 转换完成后，将显示指向导出文件的链接。
1. 单击链接可查看转换后的文件。

## 优化PDF（仅限Windows） {#optimize-a-pdf}

PDF生成器支持减小PDF文件的大小。

>[!NOTE]
>
>优化数字签名文档可删除数字签名并使其无效。

1. 在管理控制台中，单击服务>PDF生成器>Optimize PDF。
1. 单击“浏览”找到要优化的PDF文件。
1. 指定配置设置：

   * 要使用自定义设置，请选择使用自定义设置，指定文件类型设置，然后指定超时值。 默认值为270秒。
   * 要使用现有设置文件，请选择“上载设置文件”，然后单击“浏览”转到文件位置。

1. 单击创建。
