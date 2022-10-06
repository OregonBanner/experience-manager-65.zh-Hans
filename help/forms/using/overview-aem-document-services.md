---
title: AEM Document Services概述
seo-title: Overview of AEM Document Services
description: AEM Document Services是一组用于创建、组装和保护PDF文档的OSGi服务。
seo-description: AEM Document Services are a set of OSGi Services for creating, assembling, and securing PDF Documents.
uuid: 439144b7-f805-4819-9ed9-a6e9e374b5ed
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 10d406db-ac10-479b-b08b-d0735116a12b
docset: aem65
exl-id: 4c8a3877-1a3c-410d-ad1f-69c73ba4fcc1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 0%

---

# AEM Document Services概述{#overview-of-aem-document-services}

AEM Document Services是一组用于创建、组装和保护PDF文档的OSGi服务。 文档服务包含以下服务：

## 输出服务 {#output-service}

“输出”服务允许您创建不同格式的文档，包括PDF、激光打印机格式和标签打印机格式。 激光打印机格式为PostScript和打印机控制语言(PCL)。 以下列表指定标签打印机格式：

* 泽布拉(ZPL)
* Intermec(IPL)
* Datamax(DPL)
* TecToshiba(TPCL)

文档可以发送到网络打印机、本地打印机或文件系统上的文件。 输出服务将XML表单数据与表单设计合并以生成文档。 输出服务可以生成文档，而不将XML表单数据合并到文档中。 但是，主工作流将数据合并到文档中。

>[!NOTE]
>
>表单设计通常使用Designer创建。 有关为输出服务创建表单设计的信息，请参阅设计器帮助。

使用输出服务将XML数据与表单设计合并时，结果会生成一个非交互式PDF文档。 非交互式PDF文档不允许用户在其字段中输入数据。 相反，您可以使用Forms服务创建交互式PDF表单，以便用户在其字段中输入数据。

以下四个输出服务操作可供使用：

* **generatePDFOuput**:将表单设计与数据合并以生成PDF文档
* **generatePrintedOutput**:将表单设计与表单数据合并，以生成要发送到激光打印机或标签网络打印机的文档

* **generatePDFOutputBatch**:在一次调用中将多个模板与多个数据记录合并，以生成一批PDF文件。 还可以选择通过组合所有PDF来生成单个PDF
* **generatePrintedOutputBatch**:在一次调用中将多个模板与多个数据记录合并，以生成一批打印文档(PS、PCL、ZPL、DPL、IPL、TPCL)。 还可以选择生成单个打印文档。

## 汇编程序服务 {#assembler-service}

汇编程序服务允许您组合、重新排列和扩充PDF和XDP文档，并获取有关PDF文档的信息。 提交给汇编程序服务的每个作业都包括文档描述XML(DDX)文档、源文档和外部资源（字符串和图形）。 DDX文档提供了如何使用源文档生成一组生成文档的说明。

除上述功能外，汇编程序服务：

* 将PDF文档转换为PDF/A标准。
* 将PDF forms、XML表单（在Designer中创建）和PDF forms(在Acrobat中创建)转换为PDF/A-1b、PDF/A-2b和PDFA/A-3b。
* 转换已签名或未签名的PDF文档（需要数字签名）。
* 验证PDF/A文件的合规性，并在必要时进行转换。

### 关于DDX {#about-ddx}

使用汇编程序服务时，使用基于XML的语言(称为文档描述XML(DDX))来描述您需要的输出。 DDX是一种声明性标记语言，其元素表示文档的构建块。 这些构建基块包括PDF文档、XDP文档、XDP表单片段，以及其他元素，如注释、书签和样式化文本。

DDX文档可以指定具有以下特征的生成文档：

* PDF文档，从多个PDF文档组合
* 多个PDF文档，这些文档与单个PDF文档分开
* PDFPortfolio，包括自包含的用户界面和多个PDF文档和非PDF文档
* 从多个XDP文档组合的XDP文档
* 包含动态插入到XDP文档中的XML片段的XDP文档
* PDF包含XDP文档的文档
* 报告PDF文档特征的XML文件。 报告的特征包括文本、注释、表单数据、文件附件、用于PDFPortfolio、书签和PDF属性的文件。 PDF属性包括表单属性、页面旋转和文档作者。

可以使用DDX在文档装配或拆卸中增加PDF文档。 您可以指定以下效果的任意组合：

* 在选定页面上添加或删除水印或背景。
* 在选定页面上添加或删除页眉和页脚。
* 删除PDF包或PDFPortfolio的结构和导航功能。 结果会生成一个PDF文件。
* 重新编号页面标签。 页面标签通常用于页面编号。
* 从其他源文档导入元数据。
* 添加或删除文件附件、书签、链接、注释和JavaScript。
* 设置初始视图特征并优化以在Web上查看。
* 设置加密PDF的权限。
* 旋转页面或旋转和移动页面上的内容。
* 更改选定页面的大小。
* 将数据与基于XFA的PDF合并。

您可以使用简单的输入映射来指定源文档和生成文档的位置。 您还可以使用以下外部数据URL类型：

* 文件
* FTP
* HTTP/HTTPS

## 文档保障服务 {#doc-assurance-service}

文档保障服务可帮助您加密和解密文档，扩展具有其他使用权限的Adobe Reader功能，以及向文档添加数字签名。 您的用户可以轻松与PDF forms和文档进行交互，而您的组织可以提高安全性、归档和法规遵从性。

文档保障服务包含三项服务：签名、加密和读取器扩展。

### 签名服务 {#signature-service}

签名服务允许您在AEM服务器上处理数字签名和文档。 例如，签名服务通常用于以下情况：

* AEM服务器会在将表单发送到用户以使用Acrobat或Adobe Reader打开之前对其进行验证。
* AEM服务器将验证已使用Acrobat或Adobe Reader添加到表单的签名。
* AEM服务器代表公证员签署表格。

签名服务访问存储在信任存储中的证书和凭据。

### 加密服务 {#encryption-service}

加密服务允许您加密和解密文档。 文档加密后，其内容将变得不可读。 您可以加密整个PDF文档（包括其内容、元数据和附件）、除其元数据以外的所有内容，或仅加密附件。 授权用户可以解密文档以获得对其内容的访问。 如果PDF文档使用密码进行加密，则用户必须指定打开密码，才能在Adobe Reader或Acrobat中查看该文档。 如果PDF文档已使用证书进行加密，则用户必须使用私钥（证书）解密PDF文档。 用于解密PDF文档的私钥必须对应于用于加密文档的公钥。

### Reader扩展服务 {#reader-extension-service}

Reader扩展服务通过扩展Adobe Reader的功能以及其他使用权限，使您的组织能够轻松共享交互式PDF文档。 Reader扩展服务可与Adobe Reader 7.0或更高版本配合使用。 服务可向PDF文档添加使用权限。 此操作可激活在使用Adobe Reader打开PDF文档时通常不可用的功能，例如向文档添加注释、填写表单和保存文档。 第三方用户无需使用其他软件或插件即可处理启用了权限的文档。

当PDF文档添加了相应的使用权限时，收件人可以从Adobe Reader中执行以下活动：

* 在线或离线完成PDF文档和表单，允许收件人将副本保存在本地以供记录，同时仍保留添加的信息
* 将PDF文档保存到本地硬盘，以保留原始文档和任何其他注释、数据或附件
* 将文件和媒体剪辑附加到PDF文档
* 通过使用行业标准公钥基础结构(PKI)技术应用数字签名来签署、验证和验证PDF文档
* 以电子方式提交完整或注释的PDF文档
* 将PDF文档和表单用作内部数据库和Web服务的直观开发前端
* 与他人共享PDF文档，以便审阅人可以使用直观的标记工具添加注释。 这些工具包括电子附注、图章、高亮和文本删除线。 Acrobat中提供了相同的功能。
* 支持条形码表单解码。

当在Adobe Reader中打开启用了权限的PDF文档时，将自动激活这些特殊用户功能。 当用户使用完启用了权限的文档后，这些功能在Adobe Reader中再次被禁用。 在用户收到另一个启用权限的PDF文档之前，这些权限将保持禁用状态。

DocAssurance服务现成不可用。 要配置DocAssurance服务，请参阅 [安装和配置文档服务](../../forms/using/install-configure-document-services.md).

## 发送到打印机服务 {#send-to-printer-service}

“发送到打印机服务”提供API，用于将文档发送到指定的打印机进行打印。
