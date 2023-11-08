---
title: 配置服务设置
description: 了解如何配置服务设置。 可以使用“服务管理”页为AEM表单中的每项服务配置设置。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: a6a10ff0-6f4d-42df-9b4e-f98a53cf1806
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '10692'
ht-degree: 0%

---

# 配置服务设置 {#configure-service-settings}

您可以使用“服务管理”页为AEM表单中的每项服务配置设置。 可用设置因所配置的服务而异。

1. 在管理控制台中，单击服务>应用程序和服务>服务管理。
1. 在更改服务之前停止该服务。 (请参阅 [启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
1. 单击要配置的服务的名称。
1. 如果服务具有“配置”选项卡，请使用该选项卡更改服务的设置。 有关详细信息，请参阅下面的链接列表。

   >[!NOTE]
   >
   >并非所有列在“服务管理”页上的服务都有“配置”选项卡。 对于已创建的流程，仅当在Workbench中为流程添加了配置参数时，才会显示“配置”选项卡。 (请参阅 [Workbench帮助](https://www.adobe.com/go/learn_aemforms_workbench_63) .)


1. 单击“安全”选项卡，并设置服务的安全设置。 请参阅 [修改服务的安全设置](configure-service-settings.md#modifying-security-settings-for-a-service).
1. 如果服务具有“端点”选项卡，请使用该选项卡更改端点设置。 请参阅 [管理端点](/help/forms/using/admin-help/adding-enabling-modifying-or-removing.md).
1. 单击池选项卡，并设置池设置。 请参阅 [配置服务的池](configure-service-settings.md#configuring-pooling-for-a-service).
1. 单击“保存”以保存更改，或单击“取消”以放弃更改。
1. 选中服务名称旁边的复选框，然后单击“启动”以重新启动服务。

## 审核工作流服务设置 {#audit-workflow-service-settings}

Workbench提供了在运行时记录进程实例并播放它们以观察进程行为的功能。 (请参阅 [Workbench帮助](https://www.adobe.com/go/learn_aemforms_workbench_63).) 为了节省Forms Server文件系统的空间，您可以限制存储的进程记录数据量。 可以配置Audit Workflow Service的以下属性( `AuditWorkflowService`)：

**maxNumberOfRecordingInstances：** 存储的最大录制数。 当存储最大记录数时，最旧的记录将在创建新记录时从文件系统中删除。 如果您倾向于创建多个录制，并且希望自动删除旧录制，则此属性非常有用。 默认值为 50。

**MaxNumberOfRecordingEntries：** 每次记录可以存储的最大数据条目数。 数据条目是有关进程中的操作的信息。 对于每个操作的执行，存储多个条目，例如操作是否开始、操作是否完成以及通向操作的路由是否完成。 当进程可以包含许多操作执行时（例如，遇到无尽循环时），此属性很有用。 默认值为 50。

## 条形码表单服务设置 {#barcoded-forms-service-settings}

条形码表单服务 `(BarcodedFormsService)` 从扫描的图像中提取条形码数据。 该服务接受条形码形式(TIFF或PDF)作为输入，并提取由条形码编码的数据的机器表示形式。

条形码表单服务可使用以下设置。

**左读：** 选中后，将从右到左水平扫描条形码图像。

**读取权限：** 选中后，将从左到右水平扫描条形码图像。

**通读：** 选中后，将从下到上垂直扫描条形码图像。

**向下读取：** 选中后，将从上到下垂直扫描条形码图像。

>[!NOTE]
>
>默认情况下，将选择所有选项。 只有在您确定表单上不会出现条形码时，才应取消选择选项。

**基本文件路径：** 用于解析“运行XML文件作业”和“运行平面文件作业”操作的批处理输入和输出文件参数的相对文件路径。 在群集配置中，基本文件路径必须是所有群集节点都具有读/写访问权限的共享文件系统位置。

**数据源名称：** 用于维护有关批处理作业的状态和历史记录信息的数据源的名称。 指定的数据源必须支持全局(XA)事务。

## Central Migration Bridge服务（已弃用）设置 {#central-migration-bridge-service-settings}

Central Migration Bridge服务( `CentralMigrationBridge`)调用Adobe Central Pro Output Server (Central)功能的子集，包括JFMERGE、JFTRANS和XMLIMPORT命令。 Central Migration Bridge服务操作允许您在AEM表单中重用以下中央资源：

* 模板设计(&amp;ast；.ifd)
* 输出模板(&amp;ast；.mdf)
* 数据文件（&amp;ast；.dat文件）
* 报头文件（&amp;ast；.pre文件）
* 数据定义文件(&amp;ast；.tdf)

以下设置适用于Central Migration Bridge服务。

**中央安装目录：** 安装Adobe Central 5.7的目录。

## Content Repository Connector for EMC Documentum服务设置 {#content-repository-connector-for-emc-documentum-service-settings}

Content Repository Connector for EMC Documentum服务( `EMCDocumentumContentRepositoryConnector`)，使您能够创建与存储在Documentum存储库中的内容交互的流程。

以下设置可用于Content Repository Connector for EMC Documentum服务。

**Asset Link对象默认路径：** Documentum存储库中用于存储Asset Link对象的路径的默认部分。 实际路径由默认路径和表单模板在AEM表单存储库中的位置组成。

例如，如果将默认路径设置为 `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`，并且表单模板存储在文件夹中 `/Docbase/forms/`时，Asset Link对象存储在以下位置：

`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects/Docbase/forms/`

此设置的默认值为 `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`.

## IBM FileNet服务设置的Content Repository Connector {#content-repository-connector-for-ibm-filenet-service-settings}

IBM FileNet的Content Repository Connector允许您创建与存储在IBM FileNet存储库中的内容交互的流程。

以下设置适用于IBM FileNet服务的Content Repository Connector 。

**Asset Link对象默认路径：** IBM FileNet存储库中用于存储Asset Link对象的路径的默认部分。 实际路径由默认路径和表单模板在AEM表单存储库中的位置组成。

例如，如果将默认路径设置为 `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`，并且表单模板存储在文件夹中 `/Docbase/forms/`时，Asset Link对象存储在以下位置：

`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects/Docbase/forms/`

此设置的默认值为 `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`.

## 转换PDF服务设置 {#convert-pdf-service-settings}

转换PDF服务( `ConvertPdfService`)将PDF文档转换为PostScript和多种图像格式(JPEG、JPEG2000、PNG和TIFF)。 将PDF文档转换为PostScript对于任何PostScript打印机上基于服务器的自动打印很有用。 在不支持PDF文档的内容管理系统中归档文档时，将PDF文档转换为多页TIFF文件是切实可行的。

以下设置适用于转换PDF服务。

**事务处理类型：** 指定应将事务上下文传播到操作的方式。

**必需：** 支持事务上下文（如果存在）；否则，将创建新的事务上下文。 这是默认值。

**需要新的：** 始终创建新的事务上下文。 如果存在活动事务上下文，则将其挂起。

**事务超时（秒）：** 基础事务提供程序在回滚正在封装此操作的事务之前应等待的秒数。 如果传播了现有的事务上下文，则忽略此值。 默认值为 180。

**平滑的阈值分辨率（以dpi表示）：** 图像分辨率，如果为文本、线条图和图像选择了“将平滑化应用于”选项，则应用平滑（或消除锯齿）的图像分辨率低于该分辨率。

**对文本应用平滑：** 控制文本的消除锯齿。 要禁用文本平滑功能，并使用屏幕放大镜使文本更清晰更易于阅读，请清除此复选框。

**对线条图应用平滑：** 应用平滑以去除直线中的突变角度。

**对图像应用平滑：** 应用平滑以最小化图像中的突然变化。

## Distiller服务设置 {#distiller-service-settings}

Distiller服务( `DistillerService`)将PostScript、封装的PostScript (EPS)和PRN文件转换为通过网络进行PDF的文件。

以下设置可用于Distiller服务。

**Adobe PDF设置：** 以下预配置的设置将应用于生成的PDF：

* 高品质打印
* 超大页面
* PDFA1b 2005 CMYK
* PDFA1b 2005RGB
* PDFX1a 2001
* PDFX3 2002
* 新闻质量
* 最小文件大小
* 标准

可以通过PDF Generator用户界面创建新设置。

**安全设置：** 预配置的安全设置，应用于生成的PDF文档。 默认值为No Security。 您必须使用PDF Generator创建安全设置，然后在此处输入设置。

**池大小：** 池的初始大小。 在部署Distiller服务时，此数字用于确定已创建并分配给等待调用请求的空闲池的服务实施实例数。 然后，服务容器可以立即响应调用请求，而无需首先初始化服务实例。

## 文档管理服务设置 {#document-management-service-settings}

>[!NOTE]
>
>Adobe®LiveCycle®内容服务ES（已弃用）是随LiveCycle一起安装的内容管理系统。 它使用户能够设计、管理、监控和优化以人为中心的流程。 Content Services（已弃用）支持于2014年12月31日终止。 请参阅 [Adobe产品生命周期文档](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

文档管理服务( `DocumentManagementService`)使流程能够使用由Content Services提供的内容管理功能（已弃用）。 文档管理操作提供了在内容管理系统中维护空间和内容所需的基本任务。 此类任务的示例包括复制、删除、移动、检索和存储内容、创建空间和关联，以及获取和设置内容属性。

以下设置可用于Document Management服务。

**存储方案：** 内容所在的商店方案。 默认值为workspace。

**HTTP端口：** 用于访问内容服务的端口（已弃用）。 默认值为 8080。

## 电子邮件服务设置 {#email-service-settings}

电子邮件通常用于在自动化过程中分发内容或提供状态信息。 电子邮件服务( `EmailService`)使进程能够接收来自POP3或IMAP服务器的电子邮件，并将电子邮件发送到SMTP服务器。

例如，流程使用电子邮件服务发送带有PDF表单附件的电子邮件。 电子邮件服务连接到SMTP服务器以发送带有附件的电子邮件。 PDF表单旨在让收件人完成表单后单击“提交”。 该操作将表单作为附件返回到指定的电子邮件服务器。 电子邮件服务检索返回的电子邮件并将完成的表单存储在流程数据表单变量中。

以下设置适用于电子邮件服务。

**SMTP主机：** 用于发送电子邮件的SMTP服务器的IP地址或URL。

**SMTP端口号：** 用于连接到SMTP服务器的端口。

**SMTP身份验证：** 选择是否需要用户身份验证才能连接到SMTP服务器。

**SMTP用户：** 用于登录到SMTP服务器的用户帐户的用户名。

**SMTP密码：** 与SMTP用户帐户关联的密码。

**SMTP传输安全性：** 用于连接到SMTP服务器的安全协议：

* 如果不使用协议，则选择无（数据以明文发送）
* 如果使用Secure Sockets Layer协议，请选择SSL。
* 如果使用传输层安全性，请选择TLS。

**POP3/IMAP主机：** 用于发送电子邮件的POP3或IMAP服务器的IP地址或URL。

**pop3/IMAP用户名：** 用于登录到POP3或IMAP服务器的用户帐户的用户名。

**POP3/IMAP密码：** 与POP3或IMAP用户帐户关联的密码。

**POP3/IMAP端口号：** 用于连接到POP3或IMAP服务器的端口。

**POP3/IMAP：** 用于发送和接收电子邮件的协议。

**接收传输安全性：** 用于连接到SMTP服务器的安全协议：

* 如果不使用协议，则选择无（数据以明文发送）。
* 如果使用Secure Sockets Layer协议，请选择SSL。
* 如果使用传输层安全性，请选择TLS。

## 加密服务设置 {#encryption-service-settings}

加密服务( `EncryptionService`)，您可以对文档进行加密和解密。 文档加密后，其内容将变得不可读。 授权用户可以解密文档以获得对内容的访问权限。 如果使用密码对PDF文档进行加密，则必须先指定打开密码，然后才能在Adobe Reader或Adobe Acrobat中查看文档。 同样，如果PDF文档使用证书加密，则用户必须使用与用于加密PDF文档的证书（私钥）对应的公钥对PDF文档进行解密。

加密服务可使用以下设置。

**要连接的默认LDAP服务器：** 用于检索文档加密证书的LDAP服务器的主机名。

**要连接的默认LDAP端口：** LDAP服务器的端口号。

**默认LDAP用户名：** 如果LDAP服务器需要身份验证，请指定用于连接到LDAP服务器的用户名。

**默认LDAP密码：** 如果LDAP服务器需要身份验证，请指定与用于连接到LDAP服务器的用户名对应的密码。

>[!NOTE]
>
仅在通过SSL（使用LDAPS）保护连接时使用简单身份验证（用户名和密码）。

**兼容模式：**

## FTP服务设置 {#ftp-service-settings}

FTP服务( `FTP`)使进程能够与FTP服务器交互。 FTP服务操作可以从FTP服务器上检索文件、将文件放在FTP服务器上，以及从FTP服务器上删除文件。 例如，从进程生成的报告等文档可以存储在FTP服务器上进行分发。 或者，外部系统可能会根据流程中先前的步骤生成某些文件。 在该过程的后续步骤中，可以将文件传输到远程位置。

以下设置可用于FTP服务。

**默认主机：** FTP服务器的IP地址或URL。

**默认端口：** 用于连接到FTP服务器的端口。 默认值为 21。

**默认用户名：** 可用于访问FTP服务器的用户帐户的名称。 用户帐户必须具有足够的特权来执行此服务所需的FTP操作。

**默认密码：** 与指定的用户名一起使用以向FTP服务器进行身份验证的密码。

## 生成PDF服务设置 {#generate-pdf-service-settings}

生成PDF服务( `GeneratePDFService`)将各种本机格式的文件转换为PDF文档，并将PDF文档转换为多种文件格式。

以下设置可用于生成PDF服务。

**Adobe PDF设置：** 要应用于转化作业的预配置Adobe PDF设置的名称，前提是这些设置未作为API调用参数的一部分指定。 可通过单击服务>PDF Generator> Adobe PDF设置，在管理控制台中配置Adobe PDF设置。 这些设置仅适用于基于PDFMaker的转换。

**安全设置：** 要应用于转化作业的预配置安全设置的名称（如果这些设置未作为API调用参数的一部分指定）。 可通过单击“服务”>“PDF Generator”>“安全设置”，在管理控制台中配置安全设置。

**文件类型设置：** 要应用于转换作业的预配置文件类型设置的名称（如果这些设置未作为API调用参数的一部分指定）。 通过单击“服务”>“PDF Generator”>“文件类型设置”，可在管理控制台中配置文件类型设置。

**使用Acrobat WebCapture（仅限Windows）：** 当此设置为true时，生成PDF服务会将Acrobat X Pro用于所有HTMLPDF转化。 虽然性能可能会稍有降低，但这可以提高HTML生成的PDF文件的质量。 默认值为false。

**使用Acrobat映像转换（仅限Windows）：** 当此设置为true时，生成PDF服务会使用Acrobat X Pro执行所有图像到PDF的转换。 仅当默认的纯Java转换机制无法成功转换大部分输入图像时，此设置才有用。 默认值为false。

**启用基于Acrobat的AutoCAD转换（仅限Windows）：** 当此设置为true时，“生成PDF”服务会将Acrobat X Pro用于所有DWG以PDF转化。 仅当服务器上未安装AutoCAD或AutoCAD转换机制无法成功转换文件时，此设置才有用。

**用于查找用户名中禁止使用的特殊字符的正则表达式（仅限Windows）：** 指定当字符出现在用户名中时干扰Export PDF和Optimize PDF操作的字符。

**ImageToPDF池大小：** 生成PDF服务中默认（纯Java）图像到PDF转换器的池大小。 此设置控制生成PDF服务可以执行的最大同时图像到PDF转换。 此设置的默认值（建议用于单处理器系统）为3，您可以在多处理器系统上增加此值。

**PDF池的HTML大小：** 生成PDF服务中HTML到PDF转换器的池大小。 此设置控制生成PDF服务可以执行的最大并发HTML到PDF转化。 此设置的默认值（建议用于单处理器系统）为3，您可以在多处理器系统上增加此值。

**OCR池大小：** PDF Generator用于OCR的PaperCaptureService的池大小。 此设置的默认值（建议用于单处理器系统）为3，您可以在多处理器系统上增加此值。 此设置仅在Windows系统中有效。

**HTML到PDF转换的回退字体系列：** 当原始HTML中使用的字体对AEM Forms Server不可用时，在PDF文档中使用的字体系列的名称。 如果要转换使用不可用字体的HTML页，请指定字体系列。 例如，以区域语言编写的页面可能会使用不可用的字体。

**重试本机转换逻辑** 管理在首次尝试转换失败时重试的PDF生成：

**不重试**

如果首次转换尝试失败，请勿重试PDF转换

**重试**

无论是否已达到超时阈值，都重试PDF转换。 第一次尝试的默认超时持续时间为270秒。

**如果时间允许，重试**

如果首次转换尝试所用的时间小于指定的超时持续时间，请重试PDF转换。 例如，如果超时持续时间为270秒，而第一次尝试耗时200秒，则PDF Generator将重新尝试转换。 如果第一次尝试本身用了270秒，则不会重试转换。

## 指南ES4 Utilities服务设置 {#guides-es4-utilities-service-settings}

创建指南时，指南中会嵌入一些资源，例如指南定义。 资源还可以作为本地或AEM Forms Server上存储的应用程序资源的引用存在。 该指南不包含数据，并且提交位置和输入的值并非适用于所有外部环境。

在大多数情况下，默认的指南渲染服务足以准备指南，以供在工作区或其他外部环境中使用。 (在“服务”视图的Workbench中，默认服务是“指南（系统）/进程/渲染指南 — 1.0”。) Guide Utilities服务( `GuidesUtility`)允许您创建用于呈现指南的自定义流程（如有必要）。

通过“指南实用工具”操作，可以将以下“指南”渲染任务添加到进程中：

* 确定数据是否可用于填充指南
* 嵌入指南数据或将其转换为链接
* 将引用的内容转换为外部可访问的URL
* 替换HTML文档或其他包装中的值，或将它们转换为外部可访问的URL
* 设置提交位置
* 指定输入值
* 创建参数以表示引用的内容
* 如果变体可用，请设置变体

Guide Utilities服务的默认值支持大多数用例。 但是，如有必要，可以更改以下值。

**publicPaths：** 此选项已弃用。 请勿在AEM表单中使用此选项。

**pathInfoExpiryInSeconds：** 客户端的路径信息请求到期后的时间间隔。 默认值为1。

**collateralExpiryInSeconds：** 客户抵押资产请求的过期时间间隔。 默认值为315576000。

**mismatchExpiryInSeconds：** 当eTag（实体标记）不匹配时，客户端的宣传品请求过期的间隔。 （eTag是HTTP响应标头。） 默认值为1。

**guideContext：** Guides Web应用程序的上下文根目录。 与使用Guides Web应用程序设置的值匹配。 默认值为/Guides/。

**secureRandomAlgorithm：** 生成密钥和标识符时使用的算法。 此值将传递给SecureRandom Java类的getInstance方法。 默认值为SHA1PRNG。

**idBytes：** 用作密钥标识符的随机字节数。 默认值为6。

**macAlgorithm：** 用于抵押品URL验证的MAC（报文身份验证代码）算法。 此方法将传递给Mac类的getInstance方法。 默认值为HmacSHA1。

**macRefreshIntervalInMinutes：** 键处于活动状态的时长。 当密钥在此间隔内处于活动状态时，将生成新密钥。 新键将成为活动键。 以前的活动密钥会保留10%的刷新间隔。 此行为允许使用旧键生成的URL在键开关中继续工作。 默认值为144000。

**macOverlapIntervalInMinutes：** 生成新密钥后，上一个密钥保持有效的时间长度。 默认值为1440分钟（1天）。

**macKeySeed：** 用于生成安全URL的种子值。 如果选择此选项，则不会刷新键。 在不同服务器上设置相同的种子将导致这些服务器生成兼容的安全URL。 如果在负载平衡器后使用多个Forms服务器，则此功能可能很有用。 输入字符和数字的随机序列作为种子。

### 在服务器群集中使用Guides {#using-guides-in-a-server-cluster}

在不使用粘性会话的服务器群集中呈现指南失败，并出现NullPointerException。 Guides请求使用安全URL，默认情况下，这些URL对于生成它们的服务器是唯一的。 在使用粘性会话的集群中，当请求命中集群中的节点后，该会话或用户的所有后续请求都将专门路由到该服务器，一切正常。 在不使用粘性会话的集群中，后续请求可以点击集群中的任何服务器。 如果请求点击的服务器不是原始服务器，则无法解析安全URL。

如果您在不使用粘性会话的服务器群集中使用Guides，请为GuidesUtility服务设置macKeySeed值，然后停止并启动群集。

macKeySeed值是用于生成安全URL的随机数生成器的种子。 设置此值会导致每个群集节点以相同的方式初始化随机数生成器，并访问相同的安全URL。 您可以对此种子值使用任意随机字符串。

需要刷新安全URL时更改macKeySeed值。 刷新安全URL取决于您的安全策略，类似于更改服务器的主根密码的刷新策略。 macSeedValue类似于安全URL的主口令，因为它用于生成新的唯一随机数，以用于安全URL的生成和检索。

必须重新启动群集，因为macSeedValue在系统启动时是只读的。 所有节点都需要重新启动才能读取该值，因为它们单独使用该值以种子值初始化其内部随机数。

## JDBC服务设置 {#jdbc-service-settings}

JDBC服务( `JdbcService`)使进程能够与数据库交互。

以下设置可用于JDBC服务。

**数据源名称：** 一个字符串值，表示用于连接到数据库服务器的数据源的JNDI名称。 必须在托管Forms Server的应用程序服务器上定义数据源。 默认值是AEM forms数据库的数据源的JNDI名称。

## JMS服务设置 {#jms-service-settings}

JMS服务( `JMS`)支持与同时实现点对点消息传递和发布/订阅消息传递的Java Messaging System (JMS)提供商的交互。

使用默认属性配置JMS服务，以便服务操作可以与JMS提供程序和关联的JNDI服务连接和交互。 服务属性的值根据JBoss应用程序服务器设置为默认值。 如果您使用其他应用程序服务器来承载AEM表单，请更改这些值。

以下设置可用于JMS服务。

**提供程序URL：** JNDI服务提供程序的URL。 默认值基于JBoss应用程序服务器。 以下URL是AEM Forms支持的应用程序服务器的默认值：

**JBoss：** `<server name>:1099`

**WebLogic：** `<server name>:7001`

**WebSphere：** `<server name>:2809`

**JNDI用户名：** 用于向用于查找队列和主题名称的JNDI服务提供程序进行身份验证的帐户的用户名。 默认值为guest。

**JNDI口令：** 与为JNDI用户名指定的用户名关联的口令。 默认值为guest。

**初始上下文工厂：** 用作初始上下文工厂的Java类。 JMS服务使用此类创建初始上下文，这是解析主题和队列名称的起点。 默认值是JBoss上JMS服务的初始上下文工厂。 以下类是AEM Forms支持的应用程序服务器的初始上下文工厂：

**JBoss：** org.jnp.interfaces.NamingContextFactory

**WebLogic：** weblogic.jndi.WLInitialContextFactory

**WebSphere：** com.ibm.websphere.naming.WsnInitialContextFactory

**连接用户名：** 与为连接用户名指定的用户名关联的密码。 默认值为guest。

**连接密码：** 与为连接用户名指定的用户名关联的密码。 默认值为guest。

**其他属性：** 可传递给JNDI服务提供程序的属性名称和值对。 这些属性取决于您所使用的提供程序的实施和配置。

属性名称和值对使用分号分隔 **；**. 例如，以下文本显示将为名为name1和name2的两个属性指定的值，分别为value1和value2：

`name1=value1;name2=value2`

## LDAP服务设置 {#ldap-service-settings}

LDAP服务( `LDAPService`)提供查询LDAP目录的操作。 LDAP目录通常用于存储组织中人员、组和服务的相关信息。

以下设置可用于LDAP服务。

**初始上下文工厂：** 用作上下文工厂的Java类。 此类用于创建与LDAP服务器的连接。 默认值为com.sun.jndi.ldap.LdapCtxFactory，该值适用于大多数LDAP服务器。

**提供程序URL：** 用于连接到LDAP服务的URL。 值的格式为 `ldap://server name:port`

*服务器名称* 是承载LDAP服务器的计算机的名称

*端口* 是LDAP服务使用的通信端口。 默认值为389，这是用于LDAP连接的标准端口。

**用户名：** 用于登录到LDAP服务器的用户帐户的用户名。 用户帐户需要具有连接到服务器的权限并读取LDAP目录中的信息。

根据LDAP服务器的不同，用户名可能是一个简单的用户名，例如 `myname` 或DN，例如 `cn=myname,cn=users,dc=myorg`.

**密码：** 与为Username设置提供的用户名对应的密码。

**其他属性：** 一个字符串值，它表示可以提供给LDAP服务器的其他属性及其相应的值。 该值采用以下格式：

`property=value;property=value;...`

## Microsoft SharePoint配置服务设置 {#microsoft-sharepoint-configuration-service-settings}

Microsoft SharePoint配置服务 `(MSSharePointConfigService)`允许您为具有模拟权限的AEM表单用户指定凭据。 有关模拟权限的信息，请参阅 [为Microsoft SharePoint配置连接器](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html).

Microsoft SharePoint配置服务有以下设置可用：

* 具有模拟权限的用户用户名
* 上述用户的密码

**启用SSL (HTTPS)：**

**存留时间：** 此预配配置文件在客户端上有效并缓存的时间长度（以秒为单位）。 默认值为86400（24小时）。 当客户端应用程序与服务器同步且经过了指定的时间量时，客户端应用程序会向服务器请求新的设置配置文件。

**加密：** 指定是否加密存储在移动设备上的数据。

**Forms应用程序：** 在移动客户端应用程序中启用Forms功能。 选择此选项后，用户可以从其移动设备打开表单并启动流程。

**任务应用程序：** 在移动客户端应用程序中启用Tasks功能。 选择此选项后，用户可以从其移动设备访问其任务列表并完成任务。

**Content Services应用程序：** 在移动客户端应用程序中启用Content Services功能。 此功能仅适用于iOS。 选择此选项后，iPhone和iPad用户可以访问存储在贵组织的WebDAV服务器中的文件。

**脱机支持：** 使用户能够继续使用移动客户端应用程序，即使他们未连接到服务器也是如此（例如，当他们超出单元格范围或处于飞行模式时）。 用户还必须在其移动设备上启用离线支持设置。 此功能适用于Android和iOS设备。 默认情况下，此功能处于关闭状态。

>[!NOTE]
>
如果已启用离线支持，然后又禁用它，则会立即更新用户的设置配置文件，或者在用户在线时立即更新配置文件。 如果用户一直在脱机工作，则所有待处理任务都将返回到其“任务”列表，并且其队列中的所有项目（包括待处理表单、任务以及包含验证错误的表单）都将从队列中删除。

**Android：** 允许Android设备连接到服务器。

**Apple iOS：** 允许iPhone和iPad连接到服务器。

**AIR：** 允许运行基于Adobe AIR®的应用程序的设备连接到服务器。

**BlackBerry：** 允许BlackBerry设备连接到服务器。

**需要Android Microsoft Exchange ActiveSync：** 指定是否必须在Android设备上安装并激活Microsoft Exchange ActiveSync策略管理器(EA)。 如果选择该选项，必须在Android设备上实施EA。 如果未选择此选项，则不会执行检查，但会强制实施其他要求。

**Android最小PIN长度：** Android设备必须具有全局设置，以强制使PIN或密码至少具有此长度。 仅具有指定长度的PIN是不够的。 系统必须强制执行PIN长度，以便用户以后不能删除或缩短PIN。 默认值为 4。

**擦除前Android最大密码重试次数：** Android设备具有全局设置，可在尝试使用指定次数的无效密码后清除系统。 此全局设置已启用，并且等于或小于此处指定的值。 默认值为 5。

**Android删除时擦除：** 指定当Android设备上发生策略冲突时会发生的情况。 选择此选项后，将删除该帐户。 未选择此选项时，将删除存储的帐户密码和缓存的数据。 在用户修复策略违规之前，不再尝试同步。

## 输出服务设置 {#output-service-settings}

输出服务 `(OutputService)`允许您将XML表单数据与在AEM Forms Designer中创建的表单设计合并，以创建以下格式之一的文档输出流：

* PDF或PDF/文档输出流。
* Adobe PostScript输出流。
* 打印机控制语言(PCL)输出流。
* 一种斑马编程语言(ZPL)输出流。

输出流可以发送到网络打印机、本地打印机或盘文件。 在流程中使用Output服务时，您还可以将输出流作为文件附件发送给电子邮件收件人。

以下设置可用于Output服务。

**事务处理类型：** 指定应将事务上下文传播到操作的方式：

**必需：** 如果事务上下文已存在，则支持该上下文；否则，将创建新的事务上下文。 这是默认值。

**需要新的：** 始终创建新的事务上下文。 如果存在活动事务上下文，则将其挂起。

**事务超时（秒）：** 基础事务提供程序在回滚正在封装此操作的事务之前等待的秒数。 如果传播了现有的事务上下文，则忽略此值。

在处理大型数据文件或运行繁忙的服务器时，可能需要增加Output服务超时时间。 要更改超时值，请确保硬件服务器具有足够的内存并且内存对Java应用程序服务器栈可用。 默认值为 `180`。

## PDFG配置服务设置 {#pdfg-config-service-settings}

以下设置可用于PDFG配置服务( `PDFGConfigService`)。

**用户作业选项目录：** C服务写入Acrobat Pro Extended可访问的作业选项文件的文件系统文件夹的路径。 默认值为 [用户主页]/Application Data/Adobe/Adobe PDF/Settings.

**PS启动目录：** 保存了Adobe Acrobat Distiller所需的启动文件的文件系统文件夹的路径。 默认值为 [用户主页]/Application Data/Adobe/Adobe PDF/Distiller/Startup.

**PS启动文件：** Adobe Acrobat Distiller所需的启动文件的名称。 默认值为example.ps。

**服务器转换超时：** 生成PDF服务和Distiller服务的最大作业转换超时（秒）。 该设置限制了config.xml文件和管理控制台页面中为PDF Generator指定的最大转换超时。 默认值为 270。

**服务器全局超时：** 在执行PDF转换时，Forms Server会考虑超时限制。 配置超时值以解决问题。

**作业选项前缀：** 生成PDF服务用来在作业选项文件前添加短字符串的前缀，该文件是它临时创建的，可供Acrobat Distiller使用。 默认值为pdfg。

**非Unicode应用程序：** 已知不适用于Unicode的应用程序名称列表（以逗号分隔）。 此列表中预先填充了多个应用程序的名称，这些应用程序支持在PDF Generator中预先配置。 如果选择添加对通过其他不具有Unicode功能的第三方应用程序进行的PDF转换的支持，则必须将应用程序添加到此列表中。 默认值为Autocad、Excel、PowerPoint、Project、Publisher、Visio、Word、WordPerfect。

**服务器线程池计数：** 控制生成PDF服务在内部使用的线程池的大小，用于为涉及爬网的HTML到PDF转换请求提供服务（转换可从主页访问的链接页面）。 默认值为 20。

**PDFG清理扫描秒数：** 有关详细信息，请参阅作业过期秒数。

**作业过期秒数：** 生成PDF服务会在转换输入文件后立即删除这些文件。 它临时存储输出文件，存储时间长度由“PDFG清理扫描秒数”和“作业过期秒数”设置决定。

作业过期秒数设置指定文件或空文件夹在符合删除条件之前必须达到的旧时间。 PDFG Cleanup Scan Seconds设置指定清理线程扫描临时文件夹以查找可删除文件的频率。

例如，如果作业过期秒数设置为100，而PDFG清理扫描秒数设置为200，则清理线程每200秒运行一次，并删除100秒或更早的文件。

PDFG清理扫描秒的默认值为 `43200` （12小时）。 作业过期秒数的默认值为 `86400` （24小时）。

**默认区域设置：** 用于覆盖部署生成PDF服务的服务器的默认区域设置（国家/地区+语言）。 如果未指定此参数，则默认区域设置由部署服务的操作系统决定。 此参数控制将错误消息返回到API所用的语言。

## 表单工作流数据服务服务设置 {#forms-workflow-data-services-service-settings}

以下服务扩展数据服务并公开Workspace用于与服务器通信的汇编程序。 请勿更改这些服务的配置选项，除非Adobe支持部门指示您这样做。 这些服务不适用于直接访问：

* `ProcessManagementLcdsAttachmentService`
* `ProcessManagementLcdsPropertyService`
* `ProcessManagementLcdsTaskService`

## 远程服务设置 {#remoting-service-settings}

大多数服务都已配置，因此您可以通过(AEM表单已弃用) AEM Forms远程访问它们。 有关(不用于AEM表单)AEM表单远程处理的信息，请参阅 [使用AEM表单编程](https://adobe.com/go/learn_aemforms_programming_63).

以下设置适用于远程服务。

**Flex客户端身份验证方法：** 确定当所调用的服务启用了安全性、所调用的操作不支持匿名调用，并且客户端传入了无凭据或无效的凭据时，服务器发送回客户端的响应类型。 从“自定义”或“基本”中选择。 默认值为Basic。

**允许序列化不可序列化的类：** 大多数AEM表单端点只允许使用可序列化类进行调用。 在旧版本中，远程端点允许使用不可序列化的类从基于Flex的客户端进行调用。 为了防止APS11-15中描述的安全漏洞，已更改此设置。 如果要继续将不可序列化的类与Flex远程端点一起使用，请选中此复选框。

## 存储库服务设置 {#repository-service-settings}

存储库服务( `RepositoryService`)为AEM forms提供资源存储和管理服务。 当开发人员创建应用程序时，他们可以在存储库中部署资产，而不是在文件系统上部署资产。 资产可以包括任何类型的附属资料，包括XML表单、PDF forms(包括Acrobat表单)、表单片段、图像、配置文件、策略、SWF文件、DDX文件、XML架构、WSDL文件和测试数据。

您可以使用AEM表单附带的默认存储库，或使用第三方存储库( EMC Documentum Content Server 、 IBM FileNet Content Manager或IBM Content Manager )。

存储库提供方服务是一个服务委托，充当提供方服务的接口。 这样，您就可以连接到公共API，而不必知道哪个提供商服务正在实施存储功能。 存储库提供程序服务提供存储库服务资源的数据库存储。

以下设置适用于存储库服务。

**提供程序服务：** 用作存储提供程序的服务的名称。 默认值为RepositoryProviderService。

## 签名服务设置 {#signature-service-settings}

签名服务( `SignatureService`)允许贵组织保护其分发和接收的Adobe PDF文档的安全性和隐私。 此服务使用数字签名和认证，确保文档不被更改。 更改文档会破坏其签名。 由于安全功能应用于文档本身，所以文档在其整个生命周期内都保持安全和受控制；在防火墙之外，当文档离线下载时，以及当它提交回您的组织时。

以下设置可用于签名服务。

**远程HSM SPI服务的名称：** 在远程计算机上安装HSM时，可使用此选项。 在64位Windows上安装AEM表单且使用HSM设备进行签名时指定此选项。

**远程HSM Web服务的URL：** 在64位Windows上安装AEM表单且使用HSM设备进行签名时指定此选项。

**认证以包括表单加载更改：** 选择此选项时，除了XFA模板之外，还会验证XFA表单状态。 请注意，启用此选项可能会对性能产生负面影响。 默认值为true。

**执行文档JavaScript脚本：** 指定在签名操作期间是否执行Document JavaScript脚本。 默认值为false。

**处理与Acrobat 9兼容的文档：** 指定是否启用Acrobat 9兼容性。 例如，选择此选项时，将启用动态PDF中的可见认证。 默认值为false。

**签名时嵌入吊销信息：** 指定签名PDF文档时是否嵌入吊销信息。 默认值为false。

**在认证时嵌入吊销信息：** 指定验证PDF文档时是否嵌入吊销信息。 默认值为false。

**在签名/认证期间强制嵌入所有证书的吊销信息：** 指定如果未嵌入所有证书的有效吊销信息，签名或证书操作是否失败。 请注意，如果证书不包含任何CRL或OCSP信息，则即使未检索到任何吊销信息，该证书也被视为有效。 默认值为false。

**吊销检查顺序：** 指定在通过证书吊销列表(CRL)和联机证书状态协议(OCSP)机制进行检查时吊销检查的顺序。 默认值为OCSPFirst。

**吊销存档信息的最大大小：** 吊销存档信息的最大大小（以KB为单位）。 AEM forms会尝试在不超出限制的情况下存储尽可能多的吊销信息。 默认值为10 KB。

**支持从Adobe产品的预发行版本创建的签名：** 选择此选项后，使用Adobe产品的预发行版本创建的签名将正确验证。 默认值为false。

**验证时间选项：** 指定签名者证书的验证时间。 默认值为Secure Time Else Current Time。

**验证期间在签名中存档的使用吊销信息：** 指定使用签名归档的吊销信息是否用于吊销检查。 默认值为true。

**使用文档中存储的验证信息来验证签名：** 选择此选项时，文档中嵌入的验证信息（包括吊销和时间戳信息）将用于验证签名。 默认值为true。

**允许的最大嵌套验证会话：** 允许的最大嵌套验证会话数。 如果未正确设置OCSP或CRL证书，AEM Forms在验证OCSP或CRL签名者证书时使用此值防止无限循环。 默认值为 10。

**验证的最大时钟偏差：** 签名时间在验证时间之后的最长时间（以分钟为单位）。 如果时钟偏差大于此值，则签名将无效。 默认值为65分钟。

**证书生命周期缓存：** 缓存中通过在线或其他方式检索的证书的生命周期。 默认值为1天。

### 传输选项 {#transport-options}

**代理主机：** 代理主机的URL。 仅在提供有效值时使用。 无默认值。

**代理端口：** 代理端口。 键入从0到65535的任何有效端口号。 默认值为 80。

**代理登录用户名：** 代理登录用户名。 仅当为代理主机和代理端口提供了有效值时才使用。 无默认值。

**代理登录密码：** 代理登录密码。 仅当为代理主机、代理端口和代理登录用户名提供了有效值时才使用。 无默认值。

**最大下载限制：** 每个连接可以接收的最大数据量（以MB为单位）。 最小值为1 MB，最大值为1024 MB。 默认值为16 MB。

**连接超时：** 建立新连接的最长等待时间（秒）。 最小值为1，最大值为300。 默认值为 5。

**套接字超时：** 发生套接字超时（等待数据传输时）之前的最长等待时间（以秒为单位）。 最小值为1，最大值为3600。 默认值为 30。

### 路径验证选项 {#path-validation-options}

**需要明确的策略：** 指定路径是否必须对至少一个与签名者证书的信任锚点关联的证书策略有效。 默认值为false。

**禁止任何策略：** 指定如果策略对象标识符(OID)包含在证书中，是否应对其进行处理。 默认值为false。

**禁止策略映射：** 指定证书路径中是否允许策略映射。 默认值为false。

**检查所有路径：** 指定是应验证所有路径，还是应在找到第一个有效路径后停止验证。 选择true或false。 默认值为false。

**LDAP服务器：** 用于查找证书以进行路径验证的LDAP服务器。 无默认值。

**遵循证书AIA中的URI：** 指定在路径发现期间是否处理证书AIA中的统一资源标识符(URI)。 默认值为false。

**CA证书中所需的基本约束扩展：** 指定CA证书是否必须存在证书颁发机构(CA)基本约束证书扩展。 一些早期的德国认证根证书（7及更早版本）不符合RFC 3280，并且不包含基本约束扩展。 如果已知用户的EE证书链到这样一个德语根，请取消选中此复选框。 默认值为true。

**链构建过程中需要有效的证书签名：** 指定链生成器是否要求对用于生成链的证书进行有效的签名。 选中此复选框后，链生成器将不会生成证书上具有无效RSA签名的链。 考虑链CA > ICA > EE ，其中CA在ICA上的签名无效。 如果此设置为true，则链构建将在ICA处停止，并且CA将不会包含在链中。 如果此设置为false，则会生成完整的3证书链。 此设置不会影响DSA签名。 默认值为false。

### 时间戳提供程序选项 {#timestamp-provider-options}

**TSP服务器URL：** 默认时间戳提供程序的URL。 仅在提供有效值时使用。 无默认值。

**TSP服务器用户名：** 时间戳提供方要求的用户名。 仅当为URL提供了有效值时才使用。 无默认值。

**TSP服务器密码：** 上述用户名的密码（如果时间戳提供程序要求）。 仅当为URL和用户名提供了有效值时才使用。 无默认值。

**请求哈希算法：** 指定在创建时间戳提供程序的请求时要使用的哈希算法。 默认值为SHA1。

**吊销选择样式：** 指定吊销检查样式，用于从观察到的吊销状态确定时间戳提供方证书的信任状态。 默认值为BestEffort。

**发送随机数：** 指定是否使用时间戳提供程序请求发送nonce。 nonce可以是时间戳、网页上的访问计数器，或者用于限制或防止文件未经授权重放或复制的特殊标记。 默认值为true。

**在验证期间使用过期的时间戳：** 选择此选项时，过期的时间戳可用于检索签名的验证时间。 默认值为true。

**TSP响应大小：** TSP响应的估计大小（字节）。 此值应表示配置的时间戳提供程序可以返回的时间戳响应的最大大小。 除非您非常确定，否则请勿更改此设置。 最小值为60B，最大值为10240B。 默认值为4096B。

**忽略时间戳服务器扩展**：选择 **忽略时间戳服务器扩展** 用于停止AEM Forms服务器联系指定的时间戳服务器的选项。 选择选项有助于避免由于AEM Forms与时间戳服务器之间的连接超时而发生的进程失败。

### 证书吊销列表选项 {#certificate-revocation-list-options}

**首先查阅本地URI：** 指定对于吊销检查而言，在本地URI或CRL查找中提供的CRL位置是否应该优先于证书中指定的任何位置。 默认值为false。

**用于CRL查找的本地URI：** 本地CRL提供程序的URL。 仅当Consult Local URI First设置设置为true时才查阅此值。 无默认值。

**吊销选择样式：** 指定吊销检查样式，用于根据CRL提供程序的证书的观察到的吊销状态来确定其信任状态。 默认值为BestEffort。

**用于CRL查找的LDAP服务器：** 用于获取CRL的LDAP服务器(如www.ldap.com)。 所有基于DN的CRL查询都将定向到此服务器。 无默认值。

**联机：** 指定是否联机以获取CRL。 如果为false，则仅查看缓存的CRL（在本地磁盘上或嵌入签名的CRL）。 默认值为true。

**忽略有效日期：** 指定是否忽略响应的thisUpdate和nextUpdate时间，以防止这些时间对响应有效性产生负面影响。 默认值为false。

**需要CRL中的AKI扩展：** 指定授权密钥标识符扩展是否必须包含在CRL中。 默认值为false。

### 联机证书状态协议选项 {#online-certificate-status-protocol-options}

**OCSP服务器URL：** 默认OCSP服务器的URL。 是否使用通过此URL指定的OCSP服务器取决于URL咨询选项设置。 无默认值。

**咨询选项的URL：** 控制用于执行状态检查的OCSP服务器的列表和顺序。 默认值为UseAIAInCert。

**吊销选择样式：** 指定验证OCSP服务器的证书时使用的吊销检查样式。 默认值为CheckIfAvailable。

**发送随机数：** 指定是否随OCSP请求发送随机数。 nonce可以是时间戳、网页上的访问计数器，或者用于限制或防止文件未经授权重放或复制的特殊标记。 默认值为true。

**最大时钟偏差时间：** 响应时间和本地时间之间允许的最大偏差（分钟）。 最小值为0，最大值为2147483647m。 默认值为5m。

**响应刷新时间：** 预构建OCSP响应被视为有效的最长时间（以分钟为单位）。 最小值为1m，允许的最大值为2147483647。 默认值为525600（一年）。

**签署OCSP请求：** 指定是否应对OCSP请求进行签名。 默认值为false。

**请求签名者凭据别名：** 指定启用签名时用于对OCSP请求进行签名的凭据别名。 仅在启用OCSP请求签名时使用。 无默认值。

**联机：** 指定是否联机以进行吊销检查。 默认值为true。

**忽略响应的thisUpdate和nextUpdate时间：** 指定是否忽略响应的thisUpdate和nextUpdate时间，以防止这些时间对响应有效性产生负面影响。 默认值为false。

**允许OCSPNoCheck扩展：** 指定响应签名证书中是否允许OCSPNoCheck扩展。 默认值为true。

**需要OCSP ISIS-MTT CertHash扩展：** 指定是否必须将证书公钥哈希扩展包含在OCSP响应中。 默认值为false。

### 用于调试的错误处理选项 {#error-handling-options-for-debugging}

**下次API调用时清除证书缓存：** 指定在调用下一个签名服务操作时是否清除证书缓存。 调用该操作后，此选项将设置为false。 默认值为false。

**下次API调用时清除CRL缓存：** 指定在调用下一个签名服务操作时是否清除CRL缓存。 调用该操作后，此选项将设置为false。 默认值为false。

**下次API调用时清除OCSP缓存：** 指定在调用下一个签名服务操作时是否清除OCSP缓存。 调用该操作后，此选项将设置为false。 默认值为false。

## 观察文件夹服务设置 {#watched-folder-service-settings}

观察文件夹服务( `WatchedFolder`)配置所有观察文件夹端点的通用属性。 它还提供监视文件夹端点的默认值。 (请参阅 [配置观察文件夹端点](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).) 它不会被外部客户端应用程序调用，也不会在Workbench中创建的进程中使用。

以下设置可用于Watched Folder服务。

**Cron表达式：** Quartz用来安排轮询输入目录的cron表达式。

**重复计数：** 轮询输入目录的次数。 如果未在终结点配置中指定此值，则使用默认重复计数。 值为–1表示无限扫描目录。 默认值为–1。

**重复间隔：** 每个轮询之间的默认秒数。 除非在观察文件夹终结点配置中指定了不同的值，否则此值将用作重复间隔。 默认值为 5。有关其他信息，请参阅批量大小设置的说明。

**异步：** 将调用类型标识为异步或同步。 瞬态和同步进程只能同步调用。 默认值为asynchronous。

**等待时间：** 时间的默认值，以秒为单位，在此之后将从输入文件夹中检索文件。 如果文件或文件夹的时间早于等待时间中指定的时间，则会拾取它进行处理。 默认值为 0。

**批次大小：** 每次扫描处理的文件或文件夹数的默认值。 默认值为 2。

“重复间隔”和“批次大小”设置确定每次扫描中观察文件夹选取的文件数。 观察文件夹使用Quartz线程池扫描输入文件夹。 线程池与其他服务共享。 如果扫描间隔很小，则线程会经常扫描输入文件夹。 如果文件经常被放入观察文件夹，则扫描间隔应尽量小。 如果文件不经常被丢弃，请使用较大的扫描间隔，以便其他服务可以使用线程。

如果正在删除大量文件，请使批次大小变大。 例如，如果监视文件夹端点调用的服务每分钟可以处理700个文件，并且用户以相同的速率将文件放入输入文件夹，则将“批处理大小”设置为350，将“重复间隔”设置为30秒将有助于提高监视文件夹的性能，而不会产生过于频繁地扫描监视文件夹的成本。

当文件被拖放到watched文件夹中时，它会列出输入中的文件，如果每秒都进行扫描，则可能会降低性能。 增加扫描间隔可以提高性能。 如果正在删除的文件量很小，请相应地调整“批次大小”和“重复间隔”。 例如，如果每秒删除10个文件，请尝试将“重复间隔”设置为1秒，并将“批次大小”设置为10。

在群集配置中，观察文件夹端点的批处理大小不会扩展到多个群集节点。 例如，如果将批次大小设置为 `2` 对于双节点群集且选择了Throttle选项时，这些节点会以两个批次共同处理文件，而不是每个节点一次处理两个文件。

**覆盖重复的文件名：** 一个布尔字符串，它指定监视文件夹是否覆盖重复的结果文件名以及是否应覆盖保留的同名文档。

**保留文件夹：** 保留文件夹的默认值。 如果成功处理输入，则使用此文件夹将源文件复制到中。 此值可以是具有文件模式的空路径、相对路径或绝对路径，如结果文件夹设置中所述。

**失败文件夹：** 复制失败文件的文件夹的名称。 此值可以是具有文件模式的空路径、相对路径或绝对路径，如结果文件夹设置中所述。

**结果文件夹：** 结果文件夹的缺省名称。 此文件夹用于将结果文件复制到中。 此值可以是具有以下文件模式的空、相对或绝对路径。

* %F =文件名前缀
* %E =文件扩展名
* %Y =年（完整）
* %y =年（最后两位数）
* %M =月
* %D =日期
* %d =年中的日
* %H =小时（24小时制）
* %h =小时（12小时制）
* %m =分钟
* %s =秒
* %l =毫秒
* %R =随机数（从0到9）
* %P =进程或作业标识

例如，如果是2009年7月17日晚上8点，并且您指定 `C:/Test/WF0/failure/%Y/%M/%D/%H/`，结果文件夹为 `C:/Test/WF0/failure/2009/07/17/20`.

如果路径不是绝对路径而是相对路径，则会在观察文件夹内创建文件夹。 有关文件模式的详细信息，请参见 [关于文件模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
结果文件夹的大小越小， Watched文件夹的性能就越好。 例如，如果观察文件夹的预计负载为每小时1000个文件，请尝试以下模式 `result/%Y%M%D%H` 以便每小时创建一个新的子文件夹。 如果负载较小（例如，每天1000个文件），则可以使用以下模式 `result/%Y%M%D`.

**暂存文件夹：** 观察文件夹中舞台文件夹的默认名称。

**输入文件夹：** 观察文件夹内输入文件夹的缺省名称。

**失败时保留：** 如果为true，则失败时原始文件将保留在失败文件夹中。

**限制：** 如果选择该选项，它会限制AEM在任何给定时间处理受监视文件夹作业的数量。 “批次大小”值确定最大作业数（请参阅关于限制）。

## Web服务服务设置 {#web-service-service-settings}

Web服务( `WebService`)允许进程调用Web服务操作。

Web服务使进程能够调用Web服务操作。 例如，组织可能希望通过调用服务提供商公开的Web服务来集成存储和检索信息（如联系人和帐户详细信息）的流程。 Web服务调用指定的Web服务并传递其每个参数的值。 然后，它将操作返回的值保存到进程中的指定变量中。

Web服务通过发送和接收SOAP消息与Web服务进行交互。 该服务还支持使用WS-Attachment协议通过SOAP消息发送MIME、MTOM和SwaRef附件。 Web服务交互与SAP系统和.NET Web服务兼容。

以下设置可用于Web服务服务。

**密钥存储：** 包含用于身份验证的私钥的密钥库文件的完整路径。 Forms服务器必须能够访问该文件。

**密钥存储密码：** 密钥库文件的密码。

**密钥存储类型：** 密钥库的类型。 不提供值以使用为运行Forms服务器的JVM配置的默认密钥库类型。 否则，请提供以下值之一：

* jks
* pkcs12
* cms
* jceks

**信任存储区：** 包含Web服务服务器公钥的信任存储文件的完整路径。

**信任存储区密码：** truststore文件的密码。

**信任存储类型：** 信任库的类型。 不提供值以使用为运行Forms服务器的JVM配置的默认密钥库类型。 否则，请提供以下值之一：

* jks
* pkcs12
* cms
* jceks

## XSLT转换服务设置 {#xslt-transformation-service-settings}

XSLT转换服务( `XSLTService`)使进程能够对XML文档应用可扩展样式表语言转换(XSLT)。

以下设置适用于XSLT转换服务。

**工厂名称：** 用于执行XSLT转换的Java类的完全限定名称。 如果未指定值，则使用在运行Forms服务器的Java虚拟机中配置的默认工厂。

## 修改服务的安全设置 {#modifying-security-settings-for-a-service}

通过Forms Server，您可以为每个服务配置安全设置，从而逐个服务级别配置细粒度访问控制。

安装默认安全配置文件，然后可以根据您的系统需求对其进行配置。 每个安全配置文件都有一个关联的域，并在用户级别或组级别创建。

### 修改服务的安全设置 {#modify-security-settings-for-a-service}

1. 在管理控制台中，单击服务>应用程序和服务>服务管理。
1. 在“服务管理”页上，单击要配置的服务。
1. 单击“Security（安全）”选项卡。
1. 在需要呼叫者进行身份验证列表中，选择是或否，以指定是否可以使用凭据调用服务。

   如果选择“是”，必须对该服务的调用者进行身份验证，并且必须授权该调用者的用户主体调用该服务；否则，将拒绝调用尝试。

   如果选择“否”，则服务的调用者可能接受验证，也可能不接受验证。 由于没有授权检查，因此服务的调用将始终成功。

1. 对于包含标记为匿名访问的一个或多个操作的服务，请选择或取消选择“允许匿名访问”。 启用匿名访问后，系统内的任何用户都可以调用对服务的操作。 如果禁用匿名访问，则必须授予用户调用服务和调用操作的权限。 用户可以直接获得这些权限，也可以作为拥有这些权限的组的一部分获得这些权限。
1. 对于某些服务，执行操作的用户帐户会影响结果。 例如，在Content Services（已弃用）中，存储内容的用户成为内容的所有者，这会影响谁以后可以访问内容。 如果您使用进程来存储内容，请考虑使用哪个用户来执行Document Management服务，因为该用户将拥有存储的内容。

   要指定服务用于执行操作的运行时标识，请选择指定运行方式，从关联的列表中选择一个选项，然后单击保存。 从以下选项中进行选择：

   **调用程序：** 使用与调用服务的用户相同的标识。

   **系统：** 使用系统用户以完全权限运行服务。

   **指定用户：** 允许您以特定用户身份运行服务。 选择此选项时，单击选择用户以显示“选择承担者”页，在该页中可以搜索和选择用户。

   如果未选择“指定运行方式”，则使用缺省行为。

   >[!NOTE]
   >
   与xfaForm、文档表单和表单变量一起使用的渲染和提交服务始终使用系统用户帐户执行。

1. 单击“添加主体”指定用户和组对此服务具有的权限。
1. “选择承担者”屏幕显示在“用户管理”中配置的用户和组。 如果未显示所需的用户或组，请使用搜索功能查找该用户或组。 单击用户或组名。
1. 在“添加权限”屏幕上，选择要分配给此服务的用户或组的权限：

   * **INVOKE_PERM：** 调用服务上的所有操作
   * **MODIFY_CONFIG_PERM：** 修改服务的配置
   * **SUPERVISOR_PERM：** 查看从进程创建的服务的进程实例数据
   * **START_STOP_PERM：** 启动和停止服务
   * **ADD_REMOVE_ENDPOINTS_PERM：** 添加、删除和修改服务的端点
   * **CREATE_VERSION_PERM：** 创建服务的版本
   * **DELETE版本PERM：** 删除服务的版本
   * **MODIFY_VERSION_PERM：** 修改服务的版本
   * **READ_PERM：** 查看服务
   * **PROCESS_OWNER_PERM：** 用于AEM Forms的未来版本。 请勿使用此权限。
   * **SERVICE_MANAGER_PERM：** 用于AEM Forms的未来版本。 请勿使用此权限。
   * **SERVICE_AGENT_PERM：** 用于AEM Forms的未来版本。 请勿使用此权限。

1. 单击添加。

### 从安全配置文件中删除主体 {#remove-the-principal-from-a-security-profile}

1. 在“服务管理”页上，选择要配置的服务。
1. 单击 **安全性** 选项卡，选择要删除的安全配置文件，然后单击 **移除**.

## 配置服务的池 {#configuring-pooling-for-a-service}

每个服务可以利用池功能来处理传入的调用请求。 使用服务池可以确保服务实例由单个线程一次调用，并在调用请求间重复使用，这可以提高性能。 您还可以使用池指定“最大异步服务实例数”选项，该选项允许服务限制并行处理的请求数。

### 启用池 {#enable-pooling}

1. 在管理控制台中，单击服务>应用程序和服务>服务管理。
1. 在“服务管理”页上，单击要配置的服务。
1. 单击“池”选项卡。
1. 在“请求处理策略”列表中，为所有请求选择“池化实例”。
1. 在“初始服务实例池大小”框中，输入池的初始大小。 在部署服务时，此数字用于确定在等待调用请求时创建并分配给空闲池的服务实施实例数。 这使服务容器能够立即响应调用请求，而无需首先初始化服务实例。
1. 在“最大服务实例池大小”框中，输入指定服务的池中的最大实例数。 该设置控制能够在给定时间执行给定服务的线程数。 默认值为0，这将导致池大小不受限制。
1. 在最大异步服务实例数框中，输入池中可用于在任意给定时间为异步请求提供服务的最大实例数。 该设置允许服务限制可并行处理的请求数。
1. 在调用等待超时框中，输入等待服务可用于调用请求的毫秒数。 如果不为此设置指定值，则缺省值为0，这不会产生等待时间。
1. 单击保存。

### 删除池 {#remove-pooling}

1. 在管理控制台中，单击服务>应用程序和服务>服务管理。
1. 在“服务管理”页上，单击要配置的服务。
1. 单击“池”选项卡。
1. 在“请求处理策略”列表中，为每个请求选择“新建实例”，或为所有请求选择“单个实例”。

   **所有请求的单个实例：** 当第一个请求进入容器时，将创建并缓存服务实例。 请求之后的每个请求都使用相同的服务实例来处理请求。

   **每个请求的新实例：** 每次收到调用时，都会创建一个新的服务实例。

1. 单击保存。
