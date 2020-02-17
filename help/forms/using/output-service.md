---
title: 输出服务
seo-title: 输出服务
description: 描述Output Service，它是AEM Document services的一部分
seo-description: 描述Output Service，它是AEM Document services的一部分
uuid: edddef59-b43c-486f-8734-3f97961ecf4d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 51ab91ff-c0c0-4165-ae02-f306e45eea03
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 输出服务{#output-service}

## 概述 {#overview}

输出服务是AEM Document services的一个OSGi服务。 输出服务支持AEM Forms Designer的各种输出格式和输出设计功能。 输出服务可以转换XFA模板和XML数据以生成各种格式的打印文档。

输出服务允许您创建应用程序，以便：

* 使用XML数据填充模板文件，生成最终表单文档。
* 以各种格式生成输出表单，包括非交互式PDF、PostScript、PCL和ZPL打印流。
* 从XFA表单PDF生成打印PDF。
* 通过将多组数据与提供的模板合并，批量生成PDF、PostScript、PCL和ZPL文档。

>[!NOTE]
>
>输出服务是32位应用程序。 在Microsoft windows上，允许32位应用程序使用最大2 GB内存。 该限制也适用于输出服务。

## 创建非交互式表单文档 {#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

通常，您使用AEM Forms Designer创建模板。 通过 `generatePDFOutput` Output服 `generatePrintedOutput` 务的和API，您可以直接将这些模板转换为各种格式，包括PDF、PostScript、ZPL和PCL。

操 `generatePDFOutput` 作生成PDF，而操 `generatePrintedOutput` 作生成PostScript、ZPL和PCL格式。 这两个操作的第一个参数接受模板文件的名称(例如 `ExpenseClaim.xdp`)或包含模板的Document对象。 指定模板文件的名称时，还应指定内容根作为包含模板的文件夹的路径。 您可以使用或参数指定 `PDFOutputOptions` 内容根 `PrintedOutputOptions` 目录。 有关可以使用这些参数指定的其他选项的详细信息，请参阅Javadoc。

第二个参数接受在生成输出文档时与模板合并的XML文档。

操 `generatePDFOutput` 作还可以接受基于XFA的PDF表单作为输入，并将PDF表单的非交互式版本作为输出返回。

## 生成非交互式表单文档 {#generating-non-interactive-form-documents}

考虑一种情况，即您拥有一个或多个模板以及每个模板的多个XML数据记录。

使用输 `generatePDFOutputBatch` 出服 `generatePrintedOutputBatch` 务的和操作为每个记录生成打印文档。

您还可以将记录合并到一个文档中。 这两个操作都采用四个参数。

第一个参数是Map，它包含一个任意字符串作为键，模板文件的名称作为值。

第二个参数是另一个Map，其值是包含XML数据的Document对象。 该键与您为第一个参数指定的键相同。

或的第三个参 `generatePDFOutputBatch` 数分别 `generatePrintedOutputBatch` 为类型 `PDFOutputOptions` 或类 `PrintedOutputOptions` 型。

参数类型与和操作的参数类型相 `generatePDFOutput` 同， `generatePrintedOutput` 且效果相同。

第四个参数的类型 `BatchOptions`是，用于指定是否可以为每个记录生成单独的文件。 此参数的默认值为false。

同 `generatePrintedOutputBatch` 时返 `generatePDFOutputBatch` 回类型值 `BatchResult`。 该值包含生成的文档列表。 它还包含一个XML格式的元数据文档，其中包含与生成的每个文档相关的信息。
