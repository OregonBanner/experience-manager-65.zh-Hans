---
title: AEM Document services概述
seo-title: AEM Document services概述
description: AEM文档服务是一组用于创建、组合和保护PDF文档的OSGi服务。
seo-description: AEM文档服务是一组用于创建、组合和保护PDF文档的OSGi服务。
uuid: 439144b7-f805-4819-9ed9-a6e9e374b5ed
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 10d406db-ac10-479b-b08b-d0735116a12b
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# AEM Document services概述{#overview-of-aem-document-services}

AEM文档服务是一组用于创建、组合和保护PDF文档的OSGi服务。 文档服务包含以下服务：

## 输出服务 {#output-service}

通过“输出”服务，您可以创建不同格式的文档，包括PDF、激光打印机格式和标签打印机格式。 激光打印机格式为PostScript和打印机控制语言(PCL)。 以下列表指定标签打印机格式：

* 泽布拉(ZPL)
* Intermec(IPL)
* Datamax(DPL)
* TecToshiba(TPCL)

可将文档发送到网络打印机、本地打印机或文件系统上的文件。 输出服务将XML表单数据与表单设计合并，以生成文档。 输出服务可以生成文档，而无需将XML表单数据合并到文档中。 但是，主工作流将数据合并到文档中。

>[!NOTE]
>
>表单设计通常使用设计器创建。 有关为输出服务创建表单设计的信息，请参阅设计人员帮助。

使用“输出”服务将XML数据与表单设计合并时，结果是一个非交互式PDF文档。 非交互式PDF文档不允许用户在其字段中输入数据。 相反，您可以使用Forms服务创建交互式PDF表单，该表单允许用户在其字段中输入数据。

以下四个输出服务操作可供使用：

* **generatePDFOuput**:将表单设计与数据合并以生成PDF文档
* **generatePrintedOutput**:将表单设计与表单数据合并，以生成要发送到激光打印机或标签网络打印机的文档

* **generatePDFOutputBatch**:在一个调用中将多个模板与多个数据记录合并，以生成一批PDF文件。 还可以选择通过组合所有PDF来生成单个PDF
* **generatePrintedOutputBatch**:在一次调用中将多个模板与多个数据记录合并，以生成一批打印文档(PS、PCL、ZPL、DPL、IPL、TPCL)。 还可以选择生成单个打印文档。

## 汇编器服务 {#assembler-service}

通过Assembler服务，您可以合并、重新排列和增强PDF和XDP文档，并获取有关PDF文档的信息。 提交到Assembler服务的每个作业都包括文档描述XML(DDX)文档、源文档和外部资源（字符串和图形）。 DDX文档提供了有关如何使用源文档生成一组生成文档的说明。

除了上述功能，Assembler服务还：

* 将PDF文档转换为PDF/A标准。
* 将PDF表单、XML表单（在Designer中创建）和PDF表单（在Acrobat中创建）转换为PDF/A-1b、PDF/A-2b和PDFA/A-3b。
* 转换已签名或未签名的PDF文档（需要数字签名）。
* 验证PDF/A文件的规范性，并在必要时转换它。

### 关于DDX {#about-ddx}

使用Assembler服务时，使用基于XML的语言(称为“文档描述XML”(DDX))来描述所需的输出。 DDX是一种声明性标记语言，其元素表示文档的构件块。 这些构建块包括PDF文档、XDP文档、XDP表单片段和其他元素，如注释、书签和样式文本。

DDX文档可以指定生成的文档，这些文档具有以下特点：

* 由多个PDF文档组合的PDF文档
* 将多个PDF文档与一个PDF文档分开
* 包含自包含的用户界面以及多个PDF和非PDF文档的PDF包
* 由多个XDP文档组合的XDP文档
* 包含动态插入到XDP文档中的XML片段的XDP文档
* 打包XDP文档的PDF文档
* 报告PDF文档特性的XML文件。 报告的特性包括文本、注释、表单数据、文件附件、PDF包中使用的文件、书签和PDF属性。 PDF属性包括表单属性、页面旋转和文档作者。

可以使用DDX作为文档组合或拆卸的一部分来增强PDF文档。 您可以指定以下效果的任意组合：

* 在选定页面上添加或删除水印或背景。
* 在选定的页面上添加或删除页眉和页脚。
* 删除PDF包或PDF包的结构和导航功能。 结果是一个PDF文件。
* 重新编号页面标签。 页面标签通常用于页码。
* 从其他源文档导入元数据。
* 添加或删除文件附件、书签、链接、注释和JavaScript。
* 设置初始视图特征并优化以在Web上查看。
* 设置加密PDF的权限。
* 旋转页面或旋转并移动页面上的内容。
* 更改选定页面的大小。
* 将数据与基于XFA的PDF合并。

您可以使用简单的输入映射指定源文档和生成文档的位置。 您还可以使用以下外部数据URL类型：

* 文件
* FTP
* HTTP/HTTPS

## 文档保障服务 {#doc-assurance-service}

文档保障服务可帮助您加密和解密文档，使用其他使用权限扩展Adobe reader的功能，并为文档添加数字签名。 您的用户可以与PDF表单和文档轻松交互，而您的组织可以提高安全性、存档和合规性。

文档保障服务包含三项服务：签名、加密和Reader扩展。

### 签名服务 {#signature-service}

签名服务允许您在AEM服务器上处理数字签名和文档。 例如，签名服务通常在以下情况下使用：

* AEM服务器会在使用Acrobat或Adobe reader将表单发送给用户以打开前对其进行认证。
* AEM服务器会验证已使用Acrobat或Adobe Reader添加到表单的签名。
* AEM服务器代表公证员签署表单。

签名服务访问存储在信任存储区中的证书和凭据。

### 加密服务 {#encryption-service}

加密服务允许您对文档进行加密和解密。 文档加密后，其内容将变得不可读。 您可以加密整个PDF文档（包括其内容、元数据和附件）、除其元数据之外的所有内容，或仅加密附件。 授权用户可以解密文档以获得对其内容的访问。 如果PDF文档使用密码进行加密，则用户必须指定打开密码，才能在Adobe Reader或Acrobat中查看该文档。 如果PDF文档使用证书加密，则用户必须使用私钥（证书）解密该PDF文档。 用于解密PDF文档的私钥必须与用于加密文档的公钥相对应。

### Reader扩展服务 {#reader-extension-service}

Reader Extensions服务通过扩展Adobe Reader的功能以及额外的使用权限，使您的组织能够轻松共享交互式PDF文档。 Reader Extensions服务可与Adobe Reader 7.0或更高版本一起使用。 该服务向PDF文档添加使用权限。 此操作可激活在使用Adobe reader打开PDF文档时通常不可用的功能，如向文档添加注释、填写表单和保存文档。 第三方用户不需要额外的软件或插件即可处理支持权限的文档。

当PDF文档添加了相应的使用权限时，收件人可以从Adobe Reader中执行以下活动：

* 联机或脱机完成PDF文档和表单，允许收件人将副本保存在本地以备记录，同时仍可保持添加的信息完好无损
* 将PDF文档保存到本地硬盘中以保留原始文档和任何其他注释、数据或附件
* 将文件和媒体剪辑附加到PDF文档
* 通过使用行业标准公钥基础结构(PKI)技术应用数字签名，对PDF文档进行签名、验证和验证
* 以电子方式提交已填写完毕或加批注的PDF文档
* 将PDF文档和表单用作内部数据库和Web服务的直观开发前端
* 与他人共享PDF文档，使审阅者可以使用直观的标记工具添加注释。 这些工具包括电子附注、图章、高亮和文本删除线。 Acrobat中提供的功能相同。
* 支持条形码表单解码。

当在Adobe reader中打开启用了权限的PDF文档时，这些特殊用户功能会自动激活。 当用户完成对启用权限的文档的处理后，Adobe reader中将再次禁用这些功能。 在用户收到另一个已启用权限的PDF文档之前，这些文档将一直处于禁用状态。

开箱即用，DocAssurance服务不可用。 要配置DocAssurance服务，请参阅安装和配置 [配置文档服务](../../forms/using/install-configure-document-services.md)。

## 发送到打印机服务 {#send-to-printer-service}

“发送到打印机服务”提供API，用于将文档发送到指定的打印机进行打印。
