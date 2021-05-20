---
title: 表单服务
seo-title: 表单服务
description: 本文介绍了Forms服务以及使用Forms服务可执行的与表单相关的任务。
seo-description: 本文介绍了Forms服务以及使用Forms服务可执行的与表单相关的任务。
uuid: 3258d3c2-8755-4815-8c97-b2cfb9a9dfd4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: a9695d10-43ec-40eb-942f-7720abaa0973
exl-id: bd1216e4-2248-484b-a3c1-c209da4ff94f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---

# 表单服务 {#forms-service}

## 概述 {#overview}

通过Forms服务，您可以创建交互式数据捕获客户端应用程序，以验证、处理、转换和交付通常在Designer中创建的表单。 Forms服务将您开发的任何表单设计呈现为PDF文档。

Forms服务还允许组织通过将电子表单部署为AdobePDF来扩展其智能数据捕获流程。 您还可以使用服务分别将数据导入和导出到现有PDF forms和从现有数据导出数据。

使用Forms服务执行以下操作：

* 根据模板和XML数据渲染PDF forms。
* 启用表单数据集成，以将数据导入并从PDF forms提取数据。
* 基于片段渲染表单。

## 创建PDF forms  {#creating-pdf-forms-nbsp}

使用表单服务为数据捕获创建PDF forms。 通常，您首先使用AEM Forms Designer模板。 使用Forms服务的`renderPDFForm`（链接到Javadoc）操作将此模板转换为PDF表单。

`renderPDFForm`操作的第一个参数是模板文件的名称（例如，`ExpenseClaim.xdp`）。 您可以将模板文件存储在本地文件系统、CRX存储库中，或存储在HTTP或FTP位置。 您可以通过在`renderPDFForm`操作的`PDFFormRenderOptions`参数中设置内容根来指定模板文件的位置。 有关可为`PDFFormRenderOptions`参数指定的其他选项的详细信息，请参阅Javadoc。

`renderPDFForm`操作也可以接受XML数据。 创建PDF表单时，XML数据会与模板合并，以便生成的PDF表单包含指定的数据。 `renderPDFForm`操作的第二个参数可以接受包含XML数据的文档(Javadoc)对象。

## 从PDF forms提取数据  {#extracting-data-from-pdf-forms-nbsp}

使用Forms服务的`exportData`(Javadoc)操作从PDF表单中提取数据XML。 此操作接受文档作为其第一个参数。 您可以将数据导出为XDP文档或XML文件。 如果将数据导出为XML文件，则导出的数据将删除XDP信封并返回纯XML文件。 可以使用第二个参数指定此排列。

## 将数据导入PDF forms{#importing-data-into-pdf-forms}

Forms服务还允许您将使用AEM Forms Designer或`renderPDFForm`操作创建的PDF表单与XML数据合并。 Forms服务的`importData`(Javadoc)操作接受PDF表单和XML数据，并返回带有数据XML的PDF表单。

## 基于片段的呈现表单{#rendering-forms-based-on-fragments}

Forms服务可以根据您使用AEM Forms Designer创建的片段来渲染表单。 片段是表单的可重用部分。 它将另存为单独的XDP文件，可插入到多个表单设计中。 例如，片段可以包含地址块或法律文本。

使用片段可简化和加快大量表单的创建和维护。 创建表单时，为要在表单中显示的片段插入对所需片段的引用。 片段引用包含指向物理XDP文件的子表单。

以下是使用片段的优势：

* **内容重用**:您可以在多个表单设计中重复使用内容。要在多个表单中快速重复使用同一内容的部分内容，请创建一个片段。 复制或重新创建内容需要较长时间。 使用片段还可确保表单设计中常用的部分在所有引用表单中具有一致的内容和外观。
* **全局更新**:一个文件中只能对多个表单进行一次全局更改。您可以更改片段中的内容、脚本对象、数据绑定、布局或样式。 引用片段的所有XDP表单都反映更改。
* **共享表单创建**:您可以在多个资源之间共享表单的创建。具有脚本或AEM Forms Designer其他高级功能专业知识的表单开发人员可以开发和共享使用脚本和动态属性的片段。 表单设计人员可以使用片段来设计表单。 此外，他们还可以使用片段确保表单的所有部分在多个表单中具有一致的外观和功能。
