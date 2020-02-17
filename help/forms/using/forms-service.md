---
title: 表单服务
seo-title: 表单服务
description: 本文介绍了Forms服务以及可以使用Forms服务执行的与表单相关的任务。
seo-description: 本文介绍了Forms服务以及可以使用Forms服务执行的与表单相关的任务。
uuid: 3258d3c2-8755-4815-8c97-b2cfb9a9dfd4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: a9695d10-43ec-40eb-942f-7720abaa0973
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 表单服务 {#forms-service}

## 概述 {#overview}

Forms服务允许您创建交互式数据捕获客户端应用程序，这些应用程序验证、处理、转换和交付通常在Designer中创建的表单。 Forms服务将您开发的任何表单设计呈现为PDF文档。

Forms服务还使组织能够通过将电子表单部署为Adobe PDF来扩展其智能数据捕获流程。 您还可以使用该服务分别导入和导出现有PDF表单的数据。

使用Forms服务执行以下操作：

* 根据模板和XML数据渲染PDF表单。
* 实现表单数据集成，将数据导入PDF表单并从中提取数据。
* 基于片段渲染表单。

## 创建PDF表单 {#creating-pdf-forms-nbsp}

使用表单服务创建PDF表单以进行数据捕获。 通常，您首先使用AEM Forms Designer模板。 使用 `renderPDFForm` Forms服务的（链接到Javadoc）操作将此模板转换为PDF表单。

操作的第一个参 `renderPDFForm` 数是模板文件的名称(例如， `ExpenseClaim.xdp`)。 可以将模板文件存储在本地文件系统、CRX存储库中，或存储在HTTP或FTP位置。 可以通过在操作的参数中设置内容根来指定模板 `PDFFormRenderOptions` 文件的位 `renderPDFForm` 置。 有关可为参数指定的其他选项的详细信息，请参阅Javadoc `PDFFormRenderOptions` 。

该操 `renderPDFForm` 作还可以接受XML数据。 在创建PDF表单时，XML数据会与模板合并，以便生成的PDF表单包含指定的数据。 操作的第二个参 `renderPDFForm` 数可以接受包含XML数据的Document(Javadoc)对象。

## 从PDF表单提取数据 {#extracting-data-from-pdf-forms-nbsp}

使用 `exportData` Forms服务的(Javadoc)操作从PDF表单提取数据XML。 此操作接受文档作为其第一个参数。 可以将数据导出为XDP文档或XML文件。 如果将数据导出为XML文件，则导出的数据将删除XDP封套并返回一个纯XML文件。 可以使用第二个参数指定此排列。

## 将数据导入PDF表单 {#importing-data-into-pdf-forms}

Forms服务还允许您合并使用AEM Forms Designer创建的PDF表单，或合并使用XML `renderPDFForm` 数据的操作。 Forms服 `importData` 务的(Javadoc)操作接受PDF表单和XML数据并返回带有数据XML的PDF表单。

## 基于片段渲染表单 {#rendering-forms-based-on-fragments}

Forms服务可以根据您使用AEM Forms Designer创建的片段来渲染表单。 片段是表单的可重用部分。 它将另存为可插入多个表单设计的单独XDP文件。 例如，片段可以包括地址块或合法文本。

使用片段可简化和加速大量表单的创建和维护。 在创建表单时，插入对所需片段的引用，使片段显示在表单中。 片段引用包含指向物理XDP文件的子表单。

以下是使用片段的优势：

* **内容重用**:您可以在多个表单设计中重复使用内容。 要在多个表单中快速重复使用同一内容的部分，请创建一个片段。 复制或重新创建内容需要更长的时间。 使用片段还可确保表单设计中常用的部分在所有引用表单中具有一致的内容和外观。
* **全局更新**:在一个文件中只能对多个表单进行一次全局更改。 可以更改片段中的内容、脚本对象、数据绑定、布局或样式。 引用片段的所有XDP表单都反映这些更改。
* **共享表单创建**:您可以在多个资源之间共享表单的创建。 具备AEM Forms Designer脚本或其他高级功能的表单开发人员可以开发和共享使用脚本和动态属性的片段。 表单设计人员可以使用片段设计表单。 此外，他们还可以使用片段来确保表单的所有部分在多个表单之间具有一致的外观和功能。

