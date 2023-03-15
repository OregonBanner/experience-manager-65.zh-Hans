---
title: 输出服务
seo-title: Output Service
description: 描述输出服务，它是AEM Document Services的一部分
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

Output服务是AEM Document Services中的OSGi服务。 输出服务支持AEM Forms Designer的各种输出格式和输出设计功能。 输出服务可以转换XFA模板和XML数据以生成各种格式的打印文档。

Output 服务使您能够创建应用程序，这些应用程序允许您：

* 使用 XML 数据填充模板文件来生成最终表单文档。
* 生成各种格式的输出表单，包括非交互式PDF、PostScript、PCL和ZPL打印流。
* 从 XFA 表单 PDF 生成打印 PDF。
* 通过将多组数据与提供的模板合并，批量生成PDF、PostScript、PCL和ZPL文档。

>[!NOTE]
>
>输出服务是32位应用程序。 在Microsoft Windows上，32位应用程序最多可以使用2 GB内存。 该限制也适用于输出服务。

## 创建非交互式表单文档 {#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

通常使用AEM Forms Designer创建模板。 此 `generatePDFOutput` 和 `generatePrintedOutput` 通过Output服务的API，您可以直接将这些模板转换为各种格式，包括PDF、PostScript、ZPL和PCL。

此 `generatePDFOutput` 操作会生成PDF，而 `generatePrintedOutput` 操作生成PostScript、ZPL和PCL格式。 两个操作的第一个参数都接受模板文件的名称(例如 `ExpenseClaim.xdp`)或包含模板的Document对象。 指定模板文件的名称时，还应指定内容根目录作为包含模板的文件夹的路径。 您可以使用以下任一方式指定内容根 `PDFOutputOptions` 或 `PrintedOutputOptions` 参数。 有关可使用这些参数指定的其他选项的详细信息，请参阅Javadoc 。

第二个参数在生成输出文档时接受与模板合并的XML文档。

此 `generatePDFOutput` 操作还可以接受基于XFA的PDF表单作为输入，并返回PDF表单的非交互版本作为输出。

## 生成非交互式表单文档 {#generating-non-interactive-form-documents}

考虑以下情况：您有一个或多个模板，并且每个模板有多个XML数据记录。

使用 `generatePDFOutputBatch` 和 `generatePrintedOutputBatch` Output服务为每个记录生成打印文档的操作。

您还可以将记录合并到单个文档中。 这两个操作都需要4个参数。

第一个参数是一个Map，它包含作为键的任意字符串和作为值的模板文件名称。

第二个参数是不同的Map，其值是包含XML数据的Document对象。 该键与为第一个参数指定的键相同。

的第三个参数 `generatePDFOutputBatch` 或 `generatePrintedOutputBatch` 属于类型 `PDFOutputOptions` 或 `PrintedOutputOptions` 的量度。

参数类型与的参数类型相同 `generatePDFOutput` 和 `generatePrintedOutput` 和的操作具有相同的效果。

第四个参数的类型为 `BatchOptions`，用于指定是否可以为每个记录生成单独的文件。 此参数的默认值为false。

两者 `generatePrintedOutputBatch` 和 `generatePDFOutputBatch` 返回类型的值 `BatchResult`. 该值包含生成的文档列表。 它还包含一个XML格式的元数据文档，该文档包含与生成的每个文档相关的信息。
