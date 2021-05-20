---
title: 输出服务
seo-title: 输出服务
description: 描述Output Service，它是AEM Document Services的一部分
seo-description: 描述Output Service，它是AEM Document Services的一部分
uuid: edddef59-b43c-486f-8734-3f97961ecf4d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 51ab91ff-c0c0-4165-ae02-f306e45eea03
docset: aem65
exl-id: 1b62e1c1-428d-4c0f-98a8-486f319fa581
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 1%

---

# 输出服务{#output-service}

## 概述 {#overview}

输出服务是AEM Document Services中的一项OSGi服务。 输出服务支持AEM Forms Designer的各种输出格式和输出设计功能。 输出服务可以转换XFA模板和XML数据，以生成各种格式的打印文档。

通过输出服务，您可以创建应用程序，以便：

* 使用XML数据填充模板文件，生成最终表单文档。
* 以各种格式生成输出表单，包括非交互式PDF、PostScript、PCL和ZPL打印流。
* 从XFA表单PDF生成打印PDF。
* 通过将多组数据与提供的模板合并，批量生成PDF、PostScript、PCL和ZPL文档。

>[!NOTE]
>
>输出服务是一个32位应用程序。 在Microsoft Windows上，32位应用程序最多可使用2 GB的内存。 该限制也适用于输出服务。

## 创建非交互式表单文档{#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

通常，您使用AEM Forms Designer创建模板。 通过输出服务的`generatePDFOutput`和`generatePrintedOutput` API，您可以直接将这些模板转换为各种格式，包括PDF、PostScript、ZPL和PCL。

`generatePDFOutput`操作会生成PDF，而`generatePrintedOutput`操作会生成PostScript、ZPL和PCL格式。 这两个操作的第一个参数接受模板文件的名称（例如`ExpenseClaim.xdp`）或包含模板的Document对象。 指定模板文件的名称时，还应将内容根指定为包含模板的文件夹的路径。 您可以使用`PDFOutputOptions`或`PrintedOutputOptions`参数指定内容根。 有关使用这些参数可指定的其他选项的详细信息，请参阅Javadoc。

第二个参数接受在生成输出文档时与模板合并的XML文档。

`generatePDFOutput`操作还可以接受基于XFA的PDF表单作为输入，并返回PDF表单的非交互式版本作为输出。

## 生成非交互式表单文档{#generating-non-interactive-form-documents}

假设您有一个或多个模板以及每个模板的多个XML数据记录。

使用输出服务的`generatePDFOutputBatch`和`generatePrintedOutputBatch`操作为每条记录生成打印文档。

您还可以将记录合并到单个文档中。 这两个操作都需要四个参数。

第一个参数是映射，其中包含任意字符串作为键，模板文件的名称作为值。

第二个参数是不同的映射，其值是包含XML数据的Document对象。 键与为第一个参数指定的键相同。

`generatePDFOutputBatch`或`generatePrintedOutputBatch`的第三个参数分别为`PDFOutputOptions`或`PrintedOutputOptions`类型。

参数类型与`generatePDFOutput`和`generatePrintedOutput`操作的参数类型相同，具有相同的效果。

第四个参数的类型为`BatchOptions`，用于指定是否可以为每个记录生成单独的文件。 此参数的默认值为false。

`generatePrintedOutputBatch`和`generatePDFOutputBatch`都返回类型为`BatchResult`的值。 值包含生成的文档列表。 它还包含XML格式的元数据文档，其中包含与所生成的每个文档相关的信息。
