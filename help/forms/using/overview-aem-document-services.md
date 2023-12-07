---
title: AEM文档服务概述
description: AEM Document Services是用于创建、汇编和保护PDF文档的一组OSGi服务。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
exl-id: 4c8a3877-1a3c-410d-ad1f-69c73ba4fcc1
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 1%

---

# AEM文档服务概述{#overview-of-aem-document-services}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html) |
| AEM 6.5 | 本文 |


AEM Document Services是用于创建、汇编和保护PDF文档的一组OSGi服务。 Document Services包含以下服务：

## 输出服务 {#output-service}

“输出”服务允许您创建不同格式的文档，包括PDF、激光打印机格式和标签打印机格式。 激光打印机格式为PostScript和打印机控制语言(PCL)。 以下列表指定了标签打印机格式：

* 斑马(ZPL)
* Intermec (IPL)
* Datamax (DPL)
* TecToshiba (TPCL)

文档可以发送到网络打印机、本地打印机或文件系统上的文件。 Output服务将XML表单数据与表单设计合并以生成文档。 Output服务可以生成文档，而无需将XML表单数据合并到文档中。 但是，主要工作流将数据合并到文档中。

>[!NOTE]
>
>通常使用Designer创建窗体设计。 有关为Output服务创建表单设计的信息，请参阅Designer帮助。

使用Output服务将XML数据与表单设计合并时，结果为非交互式PDF文档。 非交互式PDF文档不允许用户在其字段中输入数据。 相反，您可以使用Forms服务创建一个交互式PDF表单，让用户能够在其字段中输入数据。

可以使用以下四个输出服务操作：

* **generatePDFOuput**：将表单设计和数据合并以生成PDF文档
* **generatePrintedOutput**：将表单设计与表单数据合并，生成要发送到激光打印机或标签网络打印机的文档

* **generatePDFOutputBatch**：在一次调用中合并多个模板和多个数据记录，以生成一批PDF文件。 还有一个选项，即通过合并所有PDF来生成单个PDF
* **generatePrintedOutputBatch**：在一次调用中合并多个模板和多个数据记录，以生成一批打印文档(PS、PCL、ZPL、DPL、IPL、TPCL)。 还可以选择生成单个打印文档。

## 汇编程序服务 {#assembler-service}

Assembler服务允许您组合、重新排列和增加PDF和XDP文档，并获取有关PDF文档的信息。 提交给Assembler服务的每个作业包括Document Description XML (DDX)文档、源文档和外部资源（字符串和图形）。 DDX文档提供了有关如何使用源文档生成一组结果文档的说明。

除上述功能外，汇编程序服务可以：

* 将PDF文档转换为PDF/A标准。
* 将PDF forms、XML表单（在Designer中创建）和PDF forms(在Acrobat中创建)转换为PDF/A-1b、PDF/A-2b和PDFA/A-3b。
* 转换已签名或未签名的PDF文档（需要数字签名）。
* 验证PDF/A文件的符合性，并在必要时对其进行转换。

### 关于DDX {#about-ddx}

使用Assembler服务时，请使用一种名为Document Description XML (DDX)的基于XML的语言来描述所需的输出。 DDX是一种声明性标记语言，其元素代表文档的构建块。 这些构建块包括PDF文档、XDP文档、XDP表单片段和其他元素，例如注释、书签和样式文本。

DDX文档可以指定具有以下特征的结果文档：

* 从多个PDF文档组装的PDF文档
* 从单个PDF文档分离的多个PDF文档
* PDFPortfolio，包括一个自包含的用户界面以及多个PDF和非PDF文档
* 从多个XDP文档组合的XDP文档
* 包含动态插入XDP文档中的XML片段的XDP文档
* 打包XDP文档的PDF文档
* 报告PDF文档特征的XML文件。 报告的特性包括文本、注释、表单数据、文件附件、PDFPortfolio中使用的文件、书签和PDF属性。 PDF属性包括表单属性、页面旋转和文档作者。

可以使用DDX来将PDF文档作为文档程序集或反汇编的一部分进行扩充。 您可以指定以下效果的任意组合：

* 在选定页面上添加或删除水印或背景。
* 在选定页面上添加或删除页眉和页脚。
* 删除PDF包或PDFPortfolio的结构和导航功能。 结果生成一个PDF文件。
* 为页面标签重新编号。 页面标签通常用于页码。
* 从另一源文档导入元数据。
* 添加或删除文件附件、书签、链接、注释和JavaScript。
* 设置初始视图特征并优化以在Web上查看。
* 设置加密PDF的权限。
* 旋转页面或在页面上旋转和移动内容。
* 更改所选页面的大小。
* 将数据与基于XFA的PDF合并。

您可以使用简单的输入映射来指定源文档和结果文档的位置。 您还可以使用以下外部数据URL类型：

* 文件
* FTP
* HTTP/HTTPS

## 文档保障服务 {#doc-assurance-service}

文档保障服务可帮助您加密和解密文档，通过其他使用权限扩展Adobe Reader的功能，以及向文档添加数字签名。 您的用户可以轻松地与PDF forms和文档进行交互，而您的企业可以提高安全性、归档和法规遵从性。

文档保证服务包含三个服务：签名、加密和读取器扩展。

### 签名服务 {#signature-service}

签名服务允许您在AEM服务器上处理数字签名和文档。 例如，签名服务通常用于以下情况：

* AEM服务器在将表单发送给用户以使用Acrobat或Adobe Reader打开它之前对表单进行认证。
* AEM服务器使用Acrobat或Adobe Reader验证添加到表单的签名。
* AEM服务器代表公共公证人签署表单。

签名服务访问存储在信任存储中的证书和凭据。

### 加密服务 {#encryption-service}

加密服务使您能够加密和解密文档。 文档加密后，其内容将变得不可读。 您可以加密整个PDF文档（包括其内容、元数据和附件）、除元数据以外的所有内容，或仅加密附件。 授权用户可以解密文档以获取对其内容的访问权限。 如果使用密码对PDF文档进行加密，则必须先指定打开密码，然后才能在Adobe Reader或Acrobat中查看文档。 如果PDF文档使用证书加密，用户必须使用私钥（证书）解密PDF文档。 用于解密PDF文档的私钥必须与用于加密该文档的公钥相对应。

### Reader扩展服务 {#reader-extension-service}

Reader扩展服务通过扩展具有其他使用权限的Adobe Reader的功能，使您的组织可以轻松共享交互式PDF文档。 Reader扩展服务可与Adobe Reader 7.0或更高版本一起使用。 该服务向PDF文档添加使用权限。 此操作激活在使用Adobe Reader打开PDF文档时通常不可用的功能，例如向文档添加注释、填写表单和保存文档。 第三方用户无需其他软件或插件即可使用启用了权限的文档。

当PDF文档添加了相应的使用权限后，收件人可以在Adobe Reader中执行以下操作：

* 在线或离线完成PDF文档和表单，使收件人能够在本地保存副本以保存其记录，同时仍保持添加的信息不变
* 将PDF文档保存到本地硬盘，以保留原始文档以及任何其他注释、数据或附件
* 将文件和媒体剪辑附加到PDF文档
* 使用行业标准公钥基础设施(PKI)技术应用数字签名对PDF文档进行签名、认证和身份验证
* 以电子方式提交已完成或添加注释的PDF文档
* 使用PDF文档和表单作为内部数据库和Web服务的直观开发前端
* 与其他人共享PDF文档，以便审阅人可以使用直观的标记工具添加注释。 这些工具包括电子便笺、印章、高亮和文本删除线。 Acrobat中提供了相同的函数。
* 支持条形码表单解码。

在Adobe Reader中打开启用了权限的PDF文档时，会自动激活这些特殊用户功能。 当用户使用完启用了权限的文档时，这些功能在Adobe Reader中再次被禁用。 它们保持禁用状态，直到用户收到另一个启用了权限的PDF文档。

开箱即用的DocAssurance服务不可用。 要配置DocAssurance服务，请参阅 [安装和配置配置文档服务](../../forms/using/install-configure-document-services.md).

## 发送到打印机服务 {#send-to-printer-service}

“发送到打印机”服务提供API以将文档发送到指定的打印机进行打印。
