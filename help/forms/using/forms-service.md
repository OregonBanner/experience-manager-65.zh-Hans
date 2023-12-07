---
title: 表单服务
description: 本文介绍Forms服务以及您可以使用Forms服务执行的表单相关任务。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
exl-id: bd1216e4-2248-484b-a3c1-c209da4ff94f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# 表单服务 {#forms-service}

## 概述 {#overview}

Forms服务允许您创建交互式数据捕获客户端应用程序，这些应用程序验证、处理、转换并交付通常在Designer中创建的表单。 Forms服务会将您开发的任何表单设计呈现为PDF文档。

Forms服务还使企业能够通过部署电子表单作为AdobePDF来扩展其智能数据捕获流程。 您还可以使用该服务分别从现有PDF forms导入和导出数据。

使用Forms服务执行以下操作：

* 基于PDF forms和XML数据渲染模板。
* 启用表单数据集成，以将数据导入PDF forms并从中提取数据。
* 根据片段渲染表单。

## 创建PDF forms  {#creating-pdf-forms-nbsp}

使用表单服务创建用于数据捕获的PDF forms。 通常，您首先使用AEM Forms Designer模板。 使用 `renderPDFForm` Forms （链接到Javadoc）操作，以将此模板转换为PDF表单。

的第一个参数 `renderPDFForm` 操作是模板文件的名称(例如， `ExpenseClaim.xdp`)。 您可以将模板文件存储在本地文件系统、CRX存储库或HTTP或FTP位置。 您可以通过在以下位置设置内容根来指定模板文件的位置： `PDFFormRenderOptions` 的参数 `renderPDFForm` 操作。 有关可以为指定的其他选项的详细信息，请参阅Javadoc `PDFFormRenderOptions` 参数。

此 `renderPDFForm` 操作也可以接受XML数据。 创建PDF表单时，XML数据将合并到模板中，以便生成的PDF表单包含指定的数据。 的第二个参数 `renderPDFForm` 操作可以接受包含XML数据的文档(Javadoc)对象。

## 从PDF forms提取数据  {#extracting-data-from-pdf-forms-nbsp}

使用 `exportData` (Javadoc)Forms服务从PDF表单中提取数据XML的操作。 此操作接受文档作为其第一个参数。 可以将数据导出为XDP文档或XML文件。 如果将数据导出为XML文件，则导出的数据将移除XDP封套并返回纯XML文件。 您可以使用第二个参数指定此排列。

## 将数据导入PDF forms {#importing-data-into-pdf-forms}

FormsPDF服务还允许您合并使用AEM Forms Designer或 `renderPDFForm` 操作。 此 `importData` (Javadoc)Forms服务的操作接受PDF表单和XML数据，并返回包含数据XML的PDF表单。

## 基于片段渲染表单 {#rendering-forms-based-on-fragments}

Forms服务可以呈现基于您使用AEM Forms Designer创建的片段的表单。 片段是表单中可重用的一部分。 它保存为单独的XDP文件，可插入到多个表单设计中。 例如，片段可以包含地址块或法律文本。

使用片段可简化并加速大量表单的创建和维护。 创建表单时，插入对片段在表单中显示的所需片段的引用。 片段引用包含一个指向物理XDP文件的子表单。

使用片段的优点如下：

* **内容重用**：您可以在多个表单设计中重用内容。 要在多个表单中快速重用相同内容的各个部分，请创建一个片段。 复制或重新创建内容需要较长时间。 使用片段还可确保表单设计中经常使用的部分在所有引用表单中都具有一致的内容和外观。
* **全局更新**：在一个文件中只能对多个表单进行一次全局更改。 您可以更改片段中的内容、脚本对象、数据绑定、布局或样式。 引用片段的所有XDP表单都会反映更改。
* **共享表单创建**：您可以在多个资源中共享表单的创建。 在AEM Forms Designer的脚本或其他高级功能方面拥有专业知识的表单开发人员可以开发和共享使用脚本和动态属性的片段。 窗体设计者可以使用片段来设计窗体。 此外，他们可以使用片段来确保表单的所有部分在多个表单中具有一致的外观和功能。
