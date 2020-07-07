---
title: 使用PDF生成器转换文件
seo-title: 使用PDF生成器转换文件
description: 了解如何使用PDF生成器转换文件。
seo-description: 了解如何使用PDF生成器转换文件。
uuid: 295afb8f-130a-44f5-b0ab-e4c93c0c9e52
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 999ae2be-56ba-48c1-861b-8d4c991a0206
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 0%

---


# 使用PDF生成器转换文件{#converting-files-using-pdf-generator}

您可以使用PDF Generator网页转换文件。

## 创建PDF文件 {#create-a-pdf-file}

1. 在管理控制台中，单击“服务”>“PDF生成器”>“创建PDF”。
1. 单击“浏览”以查找并选择文件。

   >[!NOTE]
   >
   >PDF Generator能够自动检测。doc、.xls、.ppt和。rtf文件的文件类型，即使文件名缺少文件扩展名也是如此。 此功能不适用于。docx、.xlsx和。pptx文件。

1. 在“配置设置”下，选择“使用自定义设置”或“上传设置文件”。

   * 如果您使用的是自定义设置，请选择Adobe PDF设置、安全设置和文件类型设置并指定超时。

      Adobe PDF设置仅适用于PS至PDF、EPS至PDF、PRN至PDF、启用OCR的图像至PDF以及本机至PDF转换。 超时设置指定完成转换所用的最长时间。 默认为270秒。 在图像到PDF和OpenOffice到PDF的转换过程中，不使用这些设置。

   * 如果要上传设置文件，请在框中键入其路径和名称，或单击“浏览”查找并选择文件。

1. （可选）在“XMP元数据文件”下，键入XMP文件的路径和名称，或单击“浏览”查找并选择文件。 XMP文件可用于包含标准元数据信息。 (请参 [阅关于XMP文件](converting-files-using-pdf-generator.md#about-xmp-files)。)
1. 单击创建。创建文件时，将显示指向该文件的链接。 如果转换过程中出错，则会显示警告。 如果创建的是Postscript文件，则警告还包含指向日志文件的链接。
1. 单击PDF文件的链接。 文件将在Acrobat中打开。

### 关于XMP文件 {#about-xmp-files}

PDF Generator在Acrobat 5.0或更高版本中创建的PDF文档包含XML格式的文档元数据。 *元数据* 包括有关文档及其内容的信息，如作者姓名、关键字以及搜索实用程序可以使用的版权信息。

文档元数据包含（但不限于）也显示在Acrobat的“文档属性”对话框的“描述”选项卡上的信息。 “描述”选项卡上所做的更改会反映在文档元数据中。 文档元数据可以通过使用第三方产品进行扩展和修改。

Adobe Extensible Metadata Platform(XMP)为Adobe应用程序提供了一个通用的XML框架，该框架实现了文档元数据在出版工作流的创建、处理和交换的标准化。 您可以以XMP格式保存和导入文档元数据XML源代码，从而在各种文档之间轻松共享元数据。 有关XMP文件的详细信息，请参 [阅可扩展元数据平台(XMP)](https://www.adobe.com/products/xmp/)[和Adobe XMP开发人员中心](https://www.adobe.com/devnet/xmp.html)。

您可以在Acrobat中创建XMP文件。

## 将HTML文件或ZIP文件转换为PDF {#convert-an-html-file-or-zip-file-to-pdf}

您可以使用PDF生成器将以下类型的文件转换为Adobe PDF:

* HTML文件，可以通过上传HTML文件或指定网页或网站的URL进行转换。
* 归档文件(ZIP)，可包含HTML文件、图像文件或两者。

如果ZIP文件在其文件夹层次结构的最低级别包含多个HTML文件，则ZIP文件还必须包含index.htm或index.html文件。

>[!NOTE]
>
>* HTML到PDF功能需要系统字体目录中的某些字体。 在Linux、Solaris和AIX系统上，系统字体目录必须包含Courier字体。 在Windows系统上，系统字体目录必须包含Times New Roman。
   >
   >
* （仅限基于UNIX的系统）AEM Forms服务器上应提供以下日文字体之一，以将带有日文字体的网页转换为PDF文档。
   >
   >  
* 《萨扎纳米哥特》
>  * &quot;Kozuka Gothic Pro-VI&quot;
>  * &quot;Kozuka Mincho Pro-VI&quot;
>  * 《萨扎纳米哥特》
>  * 《Kozuka Mincho Pr6N》
>  * 《萨萨纳米明草》
>  * “Adobe Heiti Std”
>  * “Adobe Song Std”

   >
   >
* 要从本地文件系统上传文件，请使用HTML至PDF页面上的“上传文件”选项。


1. 在管理控制台中，单击“服务”>“PDF生成器”>“HTML到PDF”。
1. 通过执行下列操作之一指定要转换的文件：

   * 在“上传文件”中，键入HTML文件或ZIP文件的路径和文件名，或单击“浏览”找到并选择它。
   * 在“指定URL”框中，键入要转换的页面或网站的URL。

   >[!NOTE]
   >
   >要转换的文件的文件扩展名必须为。html、.htm或。zip。

1. 指定配置设置：

   * 要使用自定义设置，请选择“使用自定义设置”，指定安全性和文件类型设置，然后指定超时值。 默认值为270秒。
   >[!NOTE]
   >
   >如果您将“生成PDF”服务配置为使用Acrobat WebCapture，则您在此页上选择的“文件类型设置”不会影响生成的PDF。 而是对服务器上安装的Acrobat版本进行适当的更改。

   * 要使用现有设置文件，请选择“上传设置文件”，然后单击“浏览”以转到文件位置。


1. 要上传XMP文件，请单击“浏览”并转到文件位置。 XMP文件可用于包含标准元数据信息。 (请参 [阅关于XMP文件](converting-files-using-pdf-generator.md#about-xmp-files)。)
1. 单击创建。创建文件时，将显示指向PDF文件的链接。
1. 单击链接以在Acrobat中视图PDF文档。

## 将PDF文件导出为其他文件格式（仅限Windows） {#export-a-pdf-file-to-another-file-format-windows-only}

您可以将PDF文件导出为各种文件格式，如《服务参考》的“生成PDF服务”一 [章所述](https://www.adobe.com/go/learn_aemforms_services_63)。

1. 在管理控制台中，单击“服务”>“PDF生成器”>“导出PDF”。
1. 单击“浏览”以找到要导出的PDF文件。
1. 在“将PDF文件导出为列表”中，选择要将PDF文件导出到的格式。
1. 在指定超时框中，输入在应用程序超时之前等待的时间。 默认值为270秒。

   转换文件时显示的转换时间可能大于此处指定的值。 转换时间包括等待线程或进程所花费的时间、转换文件所花费的时间以及回退转换器所花费的时间（如果适用）。 次. 指定超时值只是转换文件所花费的时间。

1. （可选）在“指定自 **定义预检用户档案** ”选项中，单击“浏览”，然后选择 [自定义预检用户档案](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html)。 预检用户档案仅在将文档转换为PDF归档(PDF/A)格式时使用。
1. 单击“导出”。 转换完成后，将显示指向导出文件的链接。
1. 单击链接以视图转换的文件。

## 优化PDF（仅限Windows） {#optimize-a-pdf}

PDF Generator支持减小PDF文件的大小。

>[!NOTE]
>
>优化数字签名文档会删除数字签名并使其失效。

1. 在管理控制台中，单击“服务”>“PDF生成器”>“优化PDF”。
1. 单击“浏览”以找到要优化的PDF文件。
1. 指定配置设置：

   * 要使用自定义设置，请选择“使用自定义设置”，指定文件类型设置，然后指定超时值。 默认值为270秒。
   * 要使用现有设置文件，请选择“上传设置文件”，然后单击“浏览”以转到文件位置。

1. 单击创建。

