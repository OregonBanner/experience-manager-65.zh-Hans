---
title: 配置服务设置
seo-title: 配置服务设置
description: 了解如何配置服务设置。
seo-description: 了解如何配置服务设置。
uuid: e95425a4-62f6-473e-b21b-d081c432e02d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 2fab4b0c-e5db-47cd-b85a-4ff5ad6eb178
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# 配置服务设置 {#configure-service-settings}

您可以使用“服务管理”页为属于AEM表单的每个服务配置设置。 可用设置因所配置的服务而异。

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“服务管理”。
1. 在更改服务之前停止它。 (请参阅 [启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)。)
1. 单击要配置的服务的名称。
1. 如果服务有“配置”选项卡，则使用它更改服务的设置。 有关详细信息，请参阅以下链接的列表。

   >[!NOTE]
   >
   >“服务管理”页面上列出的并非所有服务都具有“配置”选项卡。 对于已创建的进程，仅当在Workbench中向进程添加了配置参数时，才会显示配置选项卡。 (请参阅“工作台帮助”中的“配 [置参数](https://www.adobe.com/go/learn_aemforms_workbench_63) ”。)


1. 单击“安全性”选项卡并设置服务的安全设置。 请参 [阅修改服务的安全设置](configure-service-settings.md#modifying-security-settings-for-a-service)。
1. 如果服务有“端点”选项卡，则使用它更改端点设置。 请参阅 [管理端点](/help/forms/using/admin-help/adding-enabling-modifying-or-removing.md)。
1. 单击“池”选项卡并设置池设置。 请参 [阅配置服务的池](configure-service-settings.md#configuring-pooling-for-a-service)。
1. 单击保存以保存更改，或单击取消以放弃更改。
1. 选中服务名称旁边的复选框，然后单击“开始”以重新启动服务。

## 审核工作流服务设置 {#audit-workflow-service-settings}

Workbench提供了在进程实例运行时执行时记录它们，然后回放它们以观察进程行为的功能。 (请参阅 [工作台帮助](https://www.adobe.com/go/learn_aemforms_workbench_63)。)要节省表单服务器文件系统上的空间，您可以限制存储的进程记录数据量。 您可以配置审核工作流服务( `AuditWorkflowService`)的以下属性：

**maxNumberOfRecordingInstances:** 存储的最大录制内容数。 当存储最大数量时，当创建新录制内容时，最旧的录制内容将从文件系统中删除。 如果您倾向于创建许多录制内容并且希望自动删除旧录制内容，则此属性很有用。 默认值为 50。

**MaxNumberOfRecordingEntries:** 可为每个录制内容存储的最大数据条目数。 数据条目是有关进程中操作的信息。 为操作的每次执行存储多个条目，例如操作是否开始、操作是否完成以及通向操作的路由是否完成。 当进程可以包括许多操作执行时（例如，遇到无尽循环时），此属性很有用。 默认值为 50。

## barcoded forms service settings {#barcoded-forms-service-settings}

条形码表单服务从扫 `(BarcodedFormsService)` 描的图像中提取条形码数据。 该服务接受条形码表单（TIFF或PDF）作为输入并提取由条形码编码的数据的机器表示形式。

对于条形码表单服务，可以使用以下设置。

**左阅读：** 选择后，条形码图像将从右向左水平扫描。

**阅读权：** 选择后，条形码图像将从左到右水平扫描。

**向上阅读：** 选择此选项后，条形码图像将从底部到顶部垂直扫描。

**向下阅读：** 选择后，条形码图像将从上到下垂直扫描。

>[!NOTE]
>
>默认情况下，所有选项都处于选中状态。 仅当您确定表单上没有条形码显示时，才取消选择此选项。

**基本文件路径：** 解析“运行XML文件作业”和“运行平面文件作业”操作的批量输入和输出文件参数的文件路径。 在群集配置中，基本文件路径必须是所有群集节点都具有读／写访问权限的共享文件系统位置。

**数据源名称：** 用于维护有关批处理作业的状态和历史记录信息的数据源名称。 指定的数据源必须支持全局(XA)事务。

## Central Migration Bridge服务（已弃用）设置 {#central-migration-bridge-service-settings}

Central Migration Bridge服务( `CentralMigrationBridge`)调用Adobe Central Pro Output Server(Central)功能的子集，该功能包括JFMERGE、JFTRANS和XMLIMPORT命令。 Central Migration Bridge服务操作允许您在AEM表单中重用以下Central资源：

* 模板设计(&amp;ast;.ifd)
* 输出模板(&amp;ast;.mdf)
* 数据文件（&amp;ast;.dat文件）
* 前导文件（&amp;ast;.pre文件）
* 数据定义文件(&amp;ast;.tdf)

Central Migration Bridge服务提供以下设置。

**中央安装目录：** 安装Adobe Central 5.7的目录。

## 用于EMC Documentum的Content Repository Connector服务设置 {#content-repository-connector-for-emc-documentum-service-settings}

Content Repository Connector for EMC Documentum服务( `EMCDocumentumContentRepositoryConnector`)允许您创建与Documentum存储库中存储的内容交互的流程。

以下设置可用于Content Repository Connector for EMC Documentum服务。

**资产链接对象默认路径：** Documentum存储库中用于存储Asset Link对象的路径的默认部分。 实际路径由默认路径和AEM表单存储库中表单模板的位置组成。

例如，如果默认路径设置为 `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`，并且表单模板存储在文件夹中，则资产链接对象将存储在 `/Docbase/forms/`以下位置：

`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects/Docbase/forms/`

此设置的默认值是 `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`。

## 用于IBM FileNet服务设置的Content Repository Connector {#content-repository-connector-for-ibm-filenet-service-settings}

Content Repository Connector for IBM FileNet允许您创建与IBM FileNet存储库中存储的内容交互的进程。

以下设置可用于IBM FileNet服务的Content Repository Connector。

**资产链接对象默认路径：** IBM FileNet存储库中用于存储Asset Link对象的路径的默认部分。 实际路径由默认路径和AEM表单存储库中表单模板的位置组成。

例如，如果默认路径设置为 `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`，并且表单模板存储在文件夹中，则资产链接对象将存储在 `/Docbase/forms/`以下位置：

`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects/Docbase/forms/`

此设置的默认值是 `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`。

## 转换PDF服务设置 {#convert-pdf-service-settings}

“转换PDF”服务( `ConvertPdfService`)将PDF文档转换为PostScript和多种图像格式（JPEG、JPEG 2000、PNG和TIFF）。 将PDF文档转换为PostScript对于在任何PostScript打印机上进行基于服务器的无人值守打印都很有用。 在不支持PDF文档的内容管理系统中存档文档时，将PDF文档转换为多页TIFF文件非常实用。

“转换PDF”服务提供以下设置。

**事务处理类型：** 指定如何将事务上下文传播到操作。

**必需：** 支持事务上下文（如果存在）;否则，将创建新的事务上下文。 这是默认值。

**需要新增功能：** 始终创建新事务上下文。 如果存在活动事务上下文，则会暂停该上下文。

**事务超时（秒）:** 基础事务处理提供者在回滚正在封装此操作的事务处理之前应等待的秒数。 如果传播现有事务上下文，则忽略此值。 默认值为 180。

**平滑的阈值分辨率（以dpi为单位）:** 如果您为这些元素选择了“将平滑应用于”选项，则将平滑（或消除锯齿）应用于文本、线状图和图像的图像分辨率。

**对文本应用平滑：** 控制文本的消除锯齿。 要禁用文本平滑并使用屏幕放大镜使文本更锐利、更容易阅读，请清除此复选框。

**将平滑应用于LineArt:** 应用平滑以消除线条中的突变角度。

**对图像应用平滑：** 应用平滑以最小化图像中的突变。

## Distiller服务设置 {#distiller-service-settings}

Distiller服务( `DistillerService`)通过网络将PostScript、封装的PostScript(EPS)和PRN文件转换为PDF文件。

Distiller服务有以下可用设置。

**Adobe PDF设置：** 以下预配置设置将应用于生成的PDF:

* 高质量印刷
* 超大的页面
* PDFA1b 2005 CMYK
* PDFA1b 2005 RGB
* PDFX1a 2001
* PDFX3 2002
* 印刷质量
* 最小文件大小
* 标准

可以通过PDF Generator用户界面创建新设置。

**安全设置：** 应用于生成的PDF文档的预配置安全设置。 默认值为“无安全性”。 必须使用PDF生成器创建安全设置，然后在此处输入设置。

**池大小：** 池的初始大小。 部署Distiller服务时，此编号用于确定创建并分配给空闲池的服务实现实例的数量，这些池等待调用请求。 然后，该服务容器可以立即响应调用请求而不必首先初始化服务实例。

## 文档管理服务设置 {#document-management-service-settings}

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES（已弃用）是与LiveCycle一起安装的内容管理系统。 它使用户能够设计、管理、监控和优化以人为中心的流程。 内容服务（已弃用）支持将于2014年12月31日结束。 请参 [阅Adobe产品生命周期文档](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)。 要了解有关配置Content Services（已弃用）的信息，请参阅 [管理Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf)。

文档管理服务( `DocumentManagementService`)使进程能够使用由内容服务（已弃用）提供的内容管理功能。 文档管理操作提供维护内容管理系统中的空间和内容所需的基本任务。 这些任务的示例包括复制、删除、移动、检索和存储内容、创建空间和关联以及获取和设置内容属性。

以下设置可用于文档管理服务。

**商店方案：** 内容所在的存储的方案。 默认值是工作区。

**HTTP端口：** 用于访问Content Services的端口（已弃用）。 默认值为 8080。

## 电子邮件服务设置 {#email-service-settings}

电子邮件通常用于分发内容或提供状态信息，作为自动化流程的一部分。 电子邮件服务( `EmailService`)使进程能够从POP3或IMAP服务器接收电子邮件，并向SMTP服务器发送电子邮件。

例如，进程使用电子邮件服务发送包含PDF表单附件的电子邮件。 电子邮件服务连接到SMTP服务器，以发送带有附件的电子邮件。 PDF表单设计为让收件人在完成表单后单击“提交”。 此操作会导致表单作为指定电子邮件服务器的附件返回。 电子邮件服务检索返回的电子邮件并将完成的表单存储在进程数据表单变量中。

电子邮件服务提供以下设置。

**SMTP主机：** 用于发送电子邮件的SMTP服务器的IP地址或URL。

**SMTP端口号：** 用于连接到SMTP服务器的端口。

**SMTP身份验证：** 选择是否需要用户身份验证才能连接到SMTP服务器。

**SMTP用户：** 用于登录SMTP服务器的用户帐户的用户名。

**SMTP密码：** 与SMTP用户帐户关联的口令。

**SMTP传输安全：** 用于连接到SMTP服务器的安全协议：

* 如果未使用协议，请选择“无”（数据以明文发送）
* 如果使用安全套接字层协议，请选择SSL。
* 如果使用传输层安全性，请选择TLS。

**POP3/IMAP主机：** 用于发送电子邮件的POP3或IMAP服务器的IP地址或URL。

**POP3/IMAP用户名：** 用于登录POP3或IMAP服务器的用户帐户的用户名。

**POP3/IMAP密码：** 与POP3或IMAP用户帐户关联的口令。

**POP3/IMAP端口号：** 用于连接到POP3或IMAP服务器的端口。

**POP3/IMAP:** 用于发送和接收电子邮件的协议。

**接收传输安全性：** 用于连接到SMTP服务器的安全协议：

* 如果未使用协议（数据以明文发送），请选择“无”。
* 如果使用安全套接字层协议，请选择SSL。
* 如果使用传输层安全性，请选择TLS。

## 加密服务设置 {#encryption-service-settings}

通过Encryption服务( `EncryptionService`)，您可以加密和解密文档。 文档加密后，其内容将变得不可读。 授权用户可解密文档以获得对内容的访问。 如果PDF文档使用密码进行加密，则用户必须指定打开密码，才能在Adobe Reader或Adobe Acrobat中查看文档。 同样，如果PDF文档使用证书加密，则用户必须使用与用于加密PDF文档的证书（私钥）对应的公钥对PDF文档进行解密。

加密服务提供以下设置。

**要连接到的默认LDAP服务器：** 用于检索证书以进行文档加密的LDAP服务器的主机名。

**要连接到的默认LDAP端口：** LDAP服务器的端口号。

**默认LDAP用户名：** 如果LDAP服务器需要身份验证，请指定用于连接到LDAP服务器的用户名。

**默认LDAP口令：** 如果LDAP服务器需要身份验证，请指定与用于连接到LDAP服务器的用户名对应的口令。

>[!NOTE]
>
>仅在通过SSL保护连接时（使用LDAPS），才使用简单身份验证（用户名和密码）。

**兼容性模式：**

## FTP服务设置 {#ftp-service-settings}

FTP服务( `FTP`)使进程能够与FTP服务器交互。 FTP服务操作可以从FTP服务器检索文件，将文件放在FTP服务器上，以及从FTP服务器删除文件。 例如，从进程生成的报告等文档可以存储在FTP服务器上进行分发。 或者，外部系统可以基于进程中的先前步骤生成某些文件。 在该过程的后续步骤中，文件可以被传送到远程位置。

FTP服务提供以下设置。

**默认主机：** FTP服务器的IP地址或URL。

**默认端口：** 用于连接到FTP服务器的端口。 默认值为 21。

**默认用户名：** 用于访问FTP服务器的用户帐户的名称。 用户帐户必须具有足够的权限来执行此服务需要的FTP操作。

**默认密码：** 要与指定用户名一起使用以在FTP服务器上进行身份验证的密码。

## 生成PDF服务设置 {#generate-pdf-service-settings}

“生成PDF”服务( `GeneratePDFService`)将各种本机格式的文件转换为PDF文档，并将PDF文档转换为多种文件格式。

“生成PDF”服务提供以下设置。

**Adobe PDF设置：** 如果未将这些设置指定为API调用参数的一部分，则应用于转换作业的预配置Adobe PDF设置的名称。 通过单击“服务”>“PDF生成器”>“Adobe PDF设置”，可以在管理控制台中配置Adobe PDF设置。 这些设置仅适用于基于PDFMaker的转换。

**安全设置：** 如果未将这些设置指定为API调用参数的一部分，则应用于转换作业的预配置安全设置的名称。 在管理控制台中，单击“服务”>“PDF生成器”>“安全设置”，即可配置安全设置。

**文件类型设置：** 要应用到转换作业的预配置文件类型设置的名称（如果这些设置未作为API调用参数的一部分指定）。 通过单击“服务”>“PDF生成器”>“文件类型设置”，可以在管理控制台中配置文件类型设置。

**使用Acrobat WebCapture（仅限Windows）:** 如果此设置为true，则“生成PDF”服务将使用Acrobat X Pro进行所有HTML到PDF的转换。 这可以改进由HTML生成的PDF文件的质量，但性能可能略低一些。 默认值为false。

**使用Acrobat图像转换（仅限Windows）:** 如果此设置为true，则“生成PDF”服务会使用Acrobat X Pro进行所有图像到PDF的转换。 仅当默认的纯Java转换机制无法成功转换大部分输入图像时，此设置才有用。 默认值为false。

**启用基于Acrobat的AutoCAD转换（仅限Windows）:** 如果此设置为true，则“生成PDF”服务将Acrobat X Pro用于所有DWG到PDF的转换。 仅当服务器上未安装AutoCAD或AutoCAD转换机制无法成功转换文件时，此设置才有用。

**查找用户名中禁止的特殊字符的常规表达式（仅限Windows）:** 指定在用户名中显示字符时与“导出PDF”和“优化PDF”操作相干的字符。

**ImageToPDF池大小：** “生成PDF”服务中默认（纯Java）图像到PDF转换器的池大小。 此设置控制“生成PDF”服务可以执行的最大同时图像到PDF转换。 此设置的默认值（建议用于单处理器系统）为3，在多处理器系统上可以增加此值。

**HTML到PDF池大小：** “生成PDF”服务中HTML到PDF转换器的池大小。 此设置控制“生成PDF”服务可以执行的最大同时HTML到PDF转换。 此设置的默认值（建议用于单处理器系统）为3，在多处理器系统上可增加此值。

**OCR池大小：** PDF生成器用于OCR的PaperCaptureService的池大小。 此设置的默认值（建议用于单处理器系统）为3，在多处理器系统上可增加此值。 此设置仅在Windows系统上有效。

**用于HTML到PDF转换的回退字体系列：** 当AEM表单服务器无法使用原始HTML中使用的字体时，PDF文档中使用的字体系列的名称。 如果希望转换使用不可用字体的HTML页面，请指定字体系列。 例如，以区域语言创作的页面可能使用不可用的字体。

**本机转换的重试逻辑** ：如果首次尝试转换失败，则控制PDF生成重试:

**不重试**

如果第一次转换尝试失败，请勿重试PDF转换

**重试**

无论是否达到超时阈值，请重试PDF转换。 第一次尝试的默认超时持续时间为270秒。

**如果时间允许，重试**

如果第一次转换尝试所消耗的时间小于指定的超时持续时间，则重试PDF转换。 例如，如果超时持续时间为270秒，第一次尝试消耗时间为200秒，则PDF生成器将重新尝试转换。 如果第一次尝试本身消耗了270秒，则不会重试转换。

## 指南ES4实用程序服务设置 {#guides-es4-utilities-service-settings}

创建指南时，某些资源（如指南定义）会嵌入指南中。 资源也可以作为对本地存储或AEM表单服务器上的应用程序资源的引用存在。 《指南》不包含数据，提交位置和输入的值不适用于所有外部环境。

在大多数情况下，默认的参考线渲染服务足以准备参考线，以便在Workspace或其他外部环境中使用。 (在“服务”视图中，在“工作台”中，默认服务是“参考线（系统）/进程／渲染指南- 1.0”。)Guide Utilities服务( `GuidesUtility`)允许您根据需要创建用于渲染Guide的自定义过程。

通过“指南实用程序”(Guide Utilities)操作，可向进程添加以下“指南”渲染任务:

* 确定数据是否可用于填充指南
* 嵌入指南数据或将其转换为链接
* 将引用的内容转换为可从外部访问的URL
* 替换HTML文档或其他包装器中的值，或将其转换为可从外部访问的URL
* 设置提交位置
* 指定输入值
* 创建用于表示引用内容的参数
* 如果变量可用，请设置变量

“指南实用程序”服务的默认值支持大多数用例。 但是，如有必要，您可以更改以下值。

**publicPaths:** 已弃用此选项。 请勿将此选项用于AEM表单。

**pathInfoExpiryInSeconds:** 在此时间间隔之后，来自客户端的路径信息请求将过期。 默认值为1。

**contraulExpiryInSeconds:** 从客户端请求抵押品的间隔。 默认为315576000。

**mismatchExpiryInSeconds:** 从客户端请求附属品到期的时间间隔，当eTag（实体标记）不匹配时。 （eTag是HTTP响应头。）默认值为1。

**guideContext:** “参考线”Web应用程序的上下文根目录。 与使用“参考线”Web应用程序设置的值匹配。 默认值为/Guides/。

**secureRandomAlgorithm:** 在生成密钥和标识符时使用的算法。 此值将传递给SecureRandom Java类的getInstance方法。 默认值为SHA1PRNG。

**idBytes:** 用于键标识符的随机字节数。 默认值为6。

**macAlgorithm:** 用于附属URL验证的MAC（消息验证码）算法。 此方法将传递给Mac类的getInstance方法。 默认为HmacSHA1。

**macRefreshIntervalInMinutes:** 键处于活动状态的时间。 在此间隔内某个键处于活动状态时，将生成一个新键。 新键变为活动键。 在刷新间隔的10%内保留先前处于活动状态的密钥。 此行为允许使用旧键生成的URL在键开关上继续工作。 默认为144000。

**macOverlapIntervalInMinutes:** 在生成新密钥后，前一个密钥保持有效的时间长度。 默认为1440分钟（1天）。

**macKeySeed:** 用于生成安全URL的种子值。 如果此选项为，则不刷新键。 在不同服务器上设置相同的种子将导致这些服务器生成兼容的安全URL。 如果在负载平衡器后面使用多个表单服务器，则此功能可能很有用。 输入随机的字符和数字序列作为种子。

### 在服务器群集中使用参考线 {#using-guides-in-a-server-cluster}

在不使用粘性会话的服务器群集中渲染指南失败，出现NullPointerException。 “参考线”请求利用安全URL，默认情况下，这些URL对于生成它们的服务器是唯一的。 在使用粘性会话的群集中，当请求到达群集中的某个节点后，该会话或用户的所有后续请求都将仅路由到该服务器，并且一切正常。 在不使用粘性会话的群集中，后续请求可能会点击群集中的任何服务器。 如果请求点击的服务器不是原始服务器，则无法解析安全URL。

如果在不使用粘性会话的服务器群集中使用“参考线”，请为GuidesUtility服务设置macKeySeed值，然后停止并开始群集。

macKeySeed值是用于生成安全URL的随机数生成器的种子。 设置此值将使每个群集节点以相同的方式初始化随机数生成器，并有权访问相同的安全URL。 您可以对此种子值使用任何随机字符串。

在需要刷新安全URL时更改macKeySeed值。 刷新安全URL取决于您的安全策略，它类似于更改服务器主根口令的刷新策略。 macSeedValue类似于安全URL的主密码，因为它用于生成新的唯一随机数以用于安全URL的生成和检索。

必须重新启动群集，因为macSeedValue在系统启动时是只读的。 所有节点都需要重新开始读取该值，因为它们单独使用它以种子值初始化其内部随机数。

## JDBC服务设置 {#jdbc-service-settings}

JDBC服务( `JdbcService`)使进程能够与数据库交互。

JDBC服务具有以下设置。

**datasourceName:** 一个字符串值，它表示用于连接到数据库服务器的数据源的JNDI名称。 数据源必须在承载表单服务器的应用程序服务器上定义。 默认值是AEM表单数据库的数据源的JNDI名称。

## JMS服务设置 {#jms-service-settings}

JMS服务( `JMS`)支持与Java消息传递系统(JMS)提供者的交互，这些提供者实现了点对点消息传递和发布／订阅消息传递。

使用默认属性配置JMS服务，以便服务操作可以连接JMS提供程序和关联的JNDI服务并与之交互。 服务属性的值将基于JBoss Application Server设置为默认值。 如果您使用其他应用程序服务器托管AEM表单，请更改这些值。

JMS服务可使用以下设置。

**提供者URL:** JNDI服务提供商的URL。 默认值基于JBoss Application Server。 以下URL是AEM表单支持的应用程序服务器的默认值：

**JBoss:** `<server name>:1099`

**WebLogic:** `<server name>:7001`

**WebSphere:** `<server name>:2809`

**JNDI用户名：** 用于使用JNDI服务提供商进行身份验证的帐户的用户名，该JNDI用于查找队列和主题名称。 默认值为guest。

**JNDI密码：** 与为JNDI用户名指定的用户名关联的密码。 默认值为guest。

**初始上下文工厂：** 用作初始上下文工厂的Java类。 JMS服务使用此类创建初始上下文，该上下文是解析主题和队列名称的起点。 默认值是JBoss上JMS服务的初始上下文工厂。 以下类是AEM表单支持的应用程序服务器的初始上下文工厂：

**JBoss:** org.jnp.interfaces.NamingContextFactory

**WebLogic:** weblogic.jndi.WLInitialContextFactory

**WebSphere:** com.ibm.websphere.naming.WsnInitialContextFactory

**连接用户名：** 与为连接用户名指定的用户名关联的口令。 默认值为guest。

**连接密码：** 与为连接用户名指定的用户名关联的口令。 默认值为guest。

**其他属性：** 可传递给JNDI服务提供商的属性名和值对。 这些属性取决于您所使用的提供程序的实施和配置。

属性名和值对以分号分隔 **;**。 例如，以下文本显示将为名为name1和name2的两个属性指定的值，分别具有值value1和value2:

`name1=value1;name2=value2`

## LDAP服务设置 {#ldap-service-settings}

LDAP服务( `LDAPService`)提供查询LDAP目录的操作。 LDAP目录通常用于存储有关单位中的人员、组和服务的信息。

LDAP服务提供以下设置。

**初始上下文工厂：** 用作上下文工厂的Java类。 此类用于创建到LDAP服务器的连接。 默认值为com.sun.jndi.ldap.LdapCtxFactory，它适用于大多数LDAP服务器。

**提供者URL:** 用于连接LDAP服务的URL。 值的格式为 `ldap://server name:port`

*服务器名* ，是承载LDAP服务器的计算机的名称

*port* （端口）是LDAP服务使用的通信端口。 默认值为389，这是用于LDAP连接的标准端口。

**用户名：** 用于登录LDAP服务器的用户帐户的用户名。 用户帐户需要具有连接到服务器并读取LDAP目录中的信息的权限。

根据LDAP服务器，用户名可以是简单的用户名，如 `myname` DN或DN，如 `cn=myname,cn=users,dc=myorg`。

**密码：** 与为“用户名”设置提供的用户名对应的口令。

**其他属性：** 一个字符串值，它表示其他属性及其可提供给LDAP服务器的相应值。 该值采用以下格式：

`property=value;property=value;...`

## Microsoft SharePoint配置服务设置 {#microsoft-sharepoint-configuration-service-settings}

通过Microsoft SharePoint配置服 `(MSSharePointConfigService)`务，您可以指定具有模拟权限的AEM表单用户的凭据。 有关模拟权限的信息，请参 [阅配置Connector for Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html)。

Microsoft SharePoint配置服务提供以下设置：

* 具有模拟权限的用户的用户名
* 上述用户的口令

**启用SSL(HTTPS):**

**停留时间：** 此供应用户档案在客户端上有效和缓存的时间（以秒为单位）。 默认为86400（24小时）。 当客户端应用程序与服务器同步并且指定的时间已经过时，客户端应用程序从服务器请求新的供应用户档案。

**加密：** 指定是否加密存储在移动设备上的数据。

**表单应用程序：** 在移动客户端应用程序中启用表单功能。 选择此选项后，用户可以打开表单并从移动设备启动进程。

**任务应用程序：** 在移动客户端应用程序中启用任务功能。 选择此选项后，用户可以从其移动设备访问其任务列表和完整任务。

**Content Services Application:** Enables the Content Services feature in the mobile client application. 此功能仅适用于iOS。 When this option is selected, iPhone and iPad users can access files that are stored in your organizations’s WebDAV server.

**Offline Support:** Enables users to continue using the mobile client applications even when they do not have a connection to the server (for example, when they are out of cell range or in airplane mode). Users must also enable the Offline Support setting on their mobile devices. 此功能适用于Android和iOS设备。 默认情况下，此功能处于关闭状态。

>[!NOTE]
>
>如果启用了脱机支持，然后您禁用了该支持，则用户的供应用户档案会立即更新，或在用户联机后立即更新。 如果用户处于脱机工作状态，则所有待处理任务将返回到其任务列表，并且其队列中的所有项目(包括待处理表单、任务和包含验证错误的表单)将从队列中删除。

**Android:** 允许Android设备连接到服务器。

**Apple iOS:** 允许iPhone和iPad连接到服务器。

**AIR:** 允许运行基于Adobe AIR®的应用程序的设备连接到服务器。

**黑莓：** 允许BlackBerry设备连接到服务器。

**需要Android Microsoft Exchange ActiveSync:** 指定Microsoft Exchange ActiveSync策略管理器(EAS)是否必须在Android设备上安装并处于活动状态。 选择此选项后，必须在Android设备上实施EAS。 如果未选择此选项，则不执行检查，尽管仍要执行其他要求。

**Android最小PIN长度：** Android设备必须具有全局设置，以强制PIN或密码至少为此长度。 仅仅具有指定长度的PIN是不够的。 PIN长度必须由系统强制执行，以便用户以后不能删除或缩短PIN。 默认值为 4。

**Android在擦除前的最大密码重试:** Android设备具有全局设置，该设置可在指定数量的无效密码尝试后擦除系统。 This global setting enabled and equal to or lower than the value specified here. 默认值为 5。

**删除Android擦除：** 指定在Android设备上发生策略冲突时发生的情况。 选择此选项后，帐户即被删除。 如果未选择此选项，则会删除存储的帐户密码和缓存的数据。 在用户修复策略违规之前，不会再进行同步尝试。

## 输出服务设置 {#output-service-settings}

输出服务 `(OutputService)`允许您将XML表单数据与在AEM forms Designer中创建的表单设计合并，以创建以下格式之一的文档输出流：

* PDF或PDF/A文档输出流。
* Adobe PostScript输出流。
* 打印机控制语言(PCL)输出流。
* 一种Zebra编程语言(ZPL)输出流。

输出流可被发送到网络打印机、本地打印机或磁盘文件。 在将输出服务用作进程的一部分时，您还可以将输出流作为文件附件发送到电子邮件收件人。

以下设置可用于输出服务。

**事务处理类型：** 指定如何将事务上下文传播到操作：

**必需：** 如果事务上下文已存在，则支持该上下文；否则，将创建新的事务上下文。 这是默认值。

**需要新增功能：** 始终创建新事务上下文。 如果存在活动事务上下文，则会暂停该上下文。

**事务超时（秒）:** 基础事务处理提供者在回滚正在封装此操作的事务处理之前等待的秒数。 如果传播现有事务上下文，则忽略此值。

在处理大型数据文件或在繁忙的服务器上操作时，可能需要增加输出服务超时。 要更改超时值，请确保硬件服务器具有足够的内存，并且内存可用于Java应用程序服务器堆。 默认值为 `180`.

## PDFG配置服务设置 {#pdfg-config-service-settings}

PDFG配置服务( `PDFGConfigService`)提供以下设置。

**用户作业选项目录：** 文件系统文件夹的路径，其中c服务写入Acrobat Pro Extended可以访问的作业选项文件。 The default value is [user.home]/Application Data/Adobe/Adobe PDF/Settings.

**PS Startup Directory:** The path of the file-system folder where the startup files required by Adobe Acrobat Distiller are saved. The default value is [user.home]/Application Data/Adobe/Adobe PDF/Distiller/Startup.

**PS启动文件：** Adobe Acrobat Distiller需要的启动文件的名称。 默认值为example.ps。

**Server Conversion Timeout:** The maximum job conversion timeout (in seconds) for the Generate PDF service and the Distiller service. 此设置限制了在config.xml文件和PDF Generator的管理控制台页面中可指定的最大转换超时。 默认值为 270。

**服务器全局超时：** 执行PDF转换时，表单服务器会考虑超时限制。 配置超时值以解决问题。

**作业选项前缀：** 生成PDF服务用来在作业选项文件前附加短字符串的前缀，该作业选项文件临时创建供Acrobat Distiller使用。 默认值为pdfg。

**非Unicode应用程序：** 以逗号分隔的应用程序名称列表，已知Unicode不能。 This list is pre-populated with the names of several applications, support for which is pre-configured in PDF Generator. 如果选择通过其他不能使用Unicode的第三方应用程序添加对PDF转换的支持，则必须将这些支持添加到此列表。 默认值为Autocad、Excel、PowerPoint、Project、Publisher、Visio、Word、WordPerfect。

**服务器线程池计数：** 控制“生成PDF”服务在内部用于服务涉及蜘蛛程序（转换从主页访问的链接页面）的HTML到PDF转换请求的线程池的大小。 默认值为 20。

**PDFG清除扫描秒数：** 有关详细信息，请参阅作业过期秒数部分。

**作业过期秒数：** “生成PDF”服务会在输入文件转换后立即删除这些文件。 它将输出文件临时存储一段时间，时间由“PDFG清除扫描秒数”和“作业过期秒数”设置确定。

“作业到期秒数”设置指定文件或空文件夹在有资格删除之前必须具有多大的旧版本。 “PDFG清除扫描秒数”设置指定清除线程扫描临时文件夹以查找可删除的文件的频率。

例如，如果“作业到期秒数”设置为100，而“PDFG清除扫描秒数”设置为200，则清除线程每200秒运行一次，并删除100秒或更早的文件。

“PDFG清除扫描秒数”的默认值 `43200` 为（12小时）。 “作业到期秒数”的默认值 `86400` 为（24小时）。

**默认区域设置：** 用于覆盖部署了“生成PDF”服务的服务器的默认区域设置（国家／地区+语言）。 如果未指定此参数，则从部署服务的操作系统中确定默认区域设置。 此参数控制将错误消息返回到API的语言。

## 表单工作流数据服务服务设置 {#forms-workflow-data-services-service-settings}

以下服务扩展了Data Services并公开了Workspace用来与服务器通话的组件。 除非Adobe支持部门指示您更改这些服务的配置选项，否则请勿更改。 这些服务并非用于直接访问：

* `ProcessManagementLcdsAttachmentService`
* `ProcessManagementLcdsPropertyService`
* `ProcessManagementLcdsTaskService`

## 远程处理服务设置 {#remoting-service-settings}

大多数服务都进行了配置，这样您就可以通过（AEM表单已弃用）AEM表单远程处理访问它们。 有关（AEM表单已弃用）AEM表单远程处理的信息，请参 [阅使用AEM表单编程](https://adobe.com/go/learn_aemforms_programming_63)。

Remoting服务提供以下设置。

**Flex客户端身份验证方法：** 确定当被调用的服务启用安全性、被调用的操作不支持匿名调用且客户端传入无或无效凭据时，服务器向客户端发送的响应类型。 从“自定义”或“基本”中进行选择。 默认值为“基本”。

**允许序列化非可序列化类：** 大多数AEM表单端点只允许将Serializable类用于调用。 在旧版本中，远程处理端点允许从基于Flex的客户端调用非可序列化类。 为防止APS11-15中描述的安全漏洞，此漏洞已更改。 如果要继续将非可序列化类与Flex Remoting端点一起使用，请选中此复选框。

## 存储库服务设置 {#repository-service-settings}

存储库服务( `RepositoryService`)为AEM表单提供资源存储和管理服务。 当开发人员创建应用程序时，他们可以在存储库中而不是文件系统中部署资产。 资产可以包括任何类型的附属品，包括XML表单、PDF表单（包括Acrobat表单）、表单片段、图像、用户档案、策略、SWF文件、DDX文件、XML模式、WSDL文件和测试数据。

您可以使用AEM表单中包含的默认存储库，或使用第三方存储库（EMC Documentum Content Server、IBM FileNet Content Manager或IBM Content Manager）。

存储库提供者服务是充当提供者服务的接口的服务委托。 这允许您连接到通用API，并且不必了解哪个提供者服务正在实施存储功能。 存储库提供者服务为存储库服务资源提供数据库存储。

存储库服务具有以下设置。

**提供商服务：** 用作存储提供商的服务的名称。 默认值为RepositoryProviderService。

## 签名服务设置 {#signature-service-settings}

签名服务( `SignatureService`)使您的组织能够保护其分发和接收的Adobe PDF文档的安全和隐私。 此服务使用数字签名和认证来确保文档不被更改。 更改文档会破坏其签名。 由于安全特性被应用于文档本身，文档在整个生命周期内都保持安全并受到控制；在防火墙之外，离线下载时以及提交回您的组织时。

签名服务提供以下设置。

**远程HSM SPI服务的名称：** 此选项用于在远程计算机上安装HSM时使用。 在64位Windows上安装AEM表单并且您使用HSM设备进行签名时，请指定此选项。

**远程HSM Web服务的URL:** 在64位Windows上安装AEM表单并且您使用HSM设备进行签名时，请指定此选项。

**包含表单加载更改的认证：** 选择此选项后，除XFA模板外，还将验证XFA表单状态。 请注意，启用此选项可能会对性能产生负面影响。 默认值为true。

**执行文档JavaScript脚本：** 指定在签名操作期间是否执行文档JavaScript脚本。 默认值为false。

**兼容Acrobat 9的流程文档:** 指定是否启用Acrobat 9兼容性。 例如，选择此选项后，将启用动态PDF中的“可见认证”。 默认值为false。

**签名时嵌入撤销信息：** 指定在签署PDF文档时是否嵌入吊销信息。 默认值为false。

**认证时嵌入撤销信息：** 指定在验证PDF文档时是否嵌入吊销信息。 默认值为false。

**在签名／认证过程中，强制嵌入所有证书的撤销信息：** 指定如果未嵌入所有证书的有效撤销信息，则签名操作还是认证操作失败。 请注意，如果证书不包含任何CRL或OCSP信息，则即使未检索撤销信息，该证书也被视为有效。 默认值为false。

**撤销检查顺序：** 指定通过“证书撤销列表”(CRL)和“联机证书状态协议”(OCSP)机制检查是否可能时的撤销检查顺序。 默认值为OCSPFirst。

**撤销存档信息的最大大小：** 撤销存档信息的最大大小（以千字节为单位）。 AEM表单会尝试存储尽可能多的吊销信息，但不会超出限制。 默认值是10 KB。

**支持从Adobe产品的预发行版本创建的签名：** 选择此选项后，使用Adobe产品预发行版创建的签名将正确验证。 默认值为false。

**验证时间选项：** 指定签署方证书的验证时间。 默认值为“Secure Time Else Current Time”。

**使用验证过程中在签名中存档的撤销信息：** 指定是否使用与签名一起存档的撤销信息进行撤销检查。 默认值为true。

**使用存储在文档中的验证信息验证签名：** 选择此选项后，将使用嵌入文档中的验证信息（包括撤销和时间戳信息）来验证签名。 默认值为true。

**允许的最大嵌套验证会话数：** 允许的最大嵌套验证会话数。 当OCSP或CRL证书设置不正确时，AEM表单使用此值可防止在验证OCSP或CRL签名者证书时出现无限循环。 默认值为 10。

**验证时钟最大偏差：** 签名时间在验证时间之后的最长时间（以分钟为单位）。 如果时钟偏差大于此值，则签名将无效。 默认值是65分钟。

**证书生命周期缓存：** 在缓存中联机检索或通过其他方式检索的证书的生命周期。 默认值为1天。

### 传输选项 {#transport-options}

**Proxy Host:** The URL of the proxy host. 仅在提供了一些有效值时使用。 无默认值。

**代理端口：** 代理端口。 Type any valid port number from 0 to 65535. 默认值为 80。

**Proxy Login Username:** The proxy login user name. Used only if some valid value is provided for proxy host and proxy port. 无默认值。

**Proxy Login Password:** The proxy login password. 仅当为代理主机、代理端口和代理登录用户名提供了一些有效值时才使用。 无默认值。

**最大下载限制：** 每个连接可接收的最大数据量（以MB为单位）。 最小值为1 MB，最大值为1024 MB。 默认值为16 MB。

**连接超时：** 建立新连接所需的最长等待时间（以秒为单位）。 最小值为1，最大值为300。 默认值为 5。

**套接字超时：** 在套接字超时（等待数据传输时）发生之前等待的最长时间（以秒为单位）。 最小值是1，最大值是3600。 默认值为 30。

### 路径验证选项 {#path-validation-options}

**需要明确政策：** 指定路径是否对与签署方证书的信任锚相关联的至少一个证书策略有效。 默认值为false。

**禁止任何策略：** 指定如果策略对象标识符(OID)包含在证书中，是否应该处理它。 默认值为false。

**禁止策略映射：** 指定是否允许在认证路径中进行策略映射。 默认值为false。

**检查所有路径：** 指定是应验证所有路径，还是应在找到第一个有效路径后停止验证。 选择true或false。 默认值为false。

**LDAP服务器：** 用于查找路径验证的证书的LDAP服务器。 无默认值。

**在证书AIA中遵循URI:** 指定在路径发现过程中是否处理证书AIA中的统一资源标识符(URI)。 默认值为false。

**CA证书中需要的基本约束扩展：** 指定CA证书是否必须存在证书颁发机构(CA)基本约束证书扩展。 某些早期的德国认证根证书（7及更早版本）不符合RFC 3280，并且不包含基本约束扩展。 如果用户的EE证书链接到这样的德语根，请取消选中此复选框。 默认值为true。

**在链构建过程中需要有效的证书签名：** 指定chain builder是否对用于构建链的证书要求有效签名。 选中此复选框后，chain builder将不会在证书上构建具有无效RSA签名的链。 请考虑链CA > ICA > EE，其中CA在ICA上的签名无效。 如果此设置为真，则链式构建将停止在ICA，而CA将不包含在链中。 如果此设置为false，则生成完整的3证书链。 This setting does not affect DSA signatures. 默认值为false。

### Timestamp Provider Options {#timestamp-provider-options}

**TSP Server URL:** The URL of the default timestamp provider. Used only if some valid value is provided. 无默认值。

**TSP服务器用户名：** 时间戳提供者需要的用户名。 仅在为URL提供了一些有效值时使用。 无默认值。

**TSP服务器密码：** 如果时间戳提供者需要，上述用户名的口令。 仅在为URL和用户名提供了一些有效值时使用。 无默认值。

**Request Hash Algorithm:** Specifies the hashing algorithm to be used while creating the request for the timestamp provider. 默认值为SHA1。

**Revocation Check Style:** Specifies the revocation checking style used for determining the trust status of the timestamp provider&#39;s certificate from its observed revocation status. 默认值为BestEffort。

**发送Nonce:** 指定是否随时间戳提供者请求一起发送一次。 Nonce可以是时间戳、网页上的访问计数器或旨在限制或防止文件未经授权的重放或再现的特殊标记。 默认值为true。

**在验证过程中使用过期的时间戳：** 选择此选项后，过期的时间戳可用于检索签名的验证时间。 默认值为true。

**TSP响应大小：** TSP响应的估计大小（以字节为单位）。 此值应表示配置的时间戳提供者可返回的时间戳响应的最大大小。 除非您完全确定，否则不要更改此设置。 最小值为60B，最大值为10240B。 默认值是4096B。

**忽略TimeStamp Server Extension**:选择“忽 **略时间戳服务器扩展** ”选项，以停止AEM Forms服务器联系指定的时间戳服务器。 选择此选项有助于避免因AEM Forms和时间戳服务器之间的连接超时而发生的进程故障。

### 证书撤销列表选项 {#certificate-revocation-list-options}

**请首先查阅本地URI:** 指定是否应优先于在本地URI或CRL查找中提供的CRL位置，而不是在证书中指定用于撤销检查的任何位置。 默认值为false。

**CRL查找的本地URI:** 本地CRL提供者的URL。 仅当“Consult Local URI First”（查询本地URI First）设置设置为true时，才会查询此值。 无默认值。

**撤销检查样式：** 指定用于根据CRL提供者证书观察到的吊销状态确定证书信任状态的吊销检查样式。 默认值为BestEffort。

**CRL查找的LDAP服务器：** 用于获取CRL的LDAP服务器(作为www.ldap.com)。 所有基于DN的CRL查询都将定向到此服务器。 无默认值。

**联机：** 指定是否联机获取CRL。 如果为false，则只咨询缓存的CRL（在本地磁盘或嵌入了签名的CRL）。 默认值为true。

**忽略有效日期：** 指定是否忽略响应的thisUpdate和nextUpdate时间，这可防止这些时间对响应有效性产生负面影响。 默认值为false。

**在CRL中需要AKI扩展：** 指定CRL中是否必须包含Authority Key Identifier扩展。 默认值为false。

### 联机证书状态协议选项 {#online-certificate-status-protocol-options}

**OCSP服务器URL:** 默认OCSP服务器的URL。 是否使用通过此URL指定的OCSP服务器取决于“要咨询的URL选项”设置。 无默认值。

**要咨询的URL:** 控制用于执行状态检查的OCSP服务器的列表和顺序。 默认值为UseAIAInCert。

**撤销检查样式：** 指定在验证OCSP服务器的证书时使用的撤销检查样式。 默认值为CheckIfAvailable。

**发送Nonce:** 指定是否随OCSP请求一起发送一次。 Nonce可以是时间戳、网页上的访问计数器或旨在限制或防止文件未经授权的重放或再现的特殊标记。 默认值为true。

**最大时钟偏斜时间：** 在响应时间和本地时间之间允许的最大倾斜，以分钟为单位。 最小值为0，最大值为2147483647m。 默认值为5m。

**响应新鲜度：** 预建的OCSP响应被视为有效的最长时间（以分钟为单位）。 最小值为1m，允许的最大值为2147483647。 默认值为525600（一年）。

**签署OCSP请求：** 指定是否应对OCSP请求进行签名。 默认值为false。

**请求签署方凭据别名：** 指定在启用签名时用于对OCSP请求进行签名的凭据别名。 仅在启用OCSP请求的签名时使用。 无默认值。

**联机：** 指定是否联机以执行撤销检查。 默认值为true。

**忽略响应的thisUpdate和nextUpdate时间：** 指定是否忽略响应的thisUpdate和nextUpdate时间，这可防止这些时间对响应有效性产生负面影响。 默认值为false。

**允许OCSPNoCheck扩展：** 指定是否允许在响应签名证书中使用OCSPNoCheck扩展。 默认值为true。

**需要OCSP ISIS-MTT CertHash扩展：** 指定证书公钥哈希扩展是否必须包含在OCSP响应中。 默认值为false。

### 调试的错误处理选项 {#error-handling-options-for-debugging}

**在下次API调用时清除证书缓存：** 指定在调用下一个签名服务操作时是否清除证书缓存。 调用操作后，此选项将设置回false。 默认值为false。

**在下次API调用时清除CRL缓存：** 指定在调用下一个签名服务操作时是否清除CRL缓存。 调用操作后，此选项将设置回false。 默认值为false。

**在下次API调用时清除OCSP缓存：** 指定在调用下一个签名服务操作时是否清除OCSP缓存。 调用操作后，此选项将设置回false。 默认值为false。

## 监视文件夹服务设置 {#watched-folder-service-settings}

监视文件夹服务( `WatchedFolder`)配置所有监视文件夹端点的通用属性。 它还为监视的文件夹端点提供默认值。 (请参阅 [配置监视文件夹端点](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)。)外部客户端应用程序不会调用它，也不会在Workbench中创建的进程中使用它。

“监视文件夹”服务提供以下设置。

**Cron表达式:** 石英用于计划输入目录的轮询的cron表达式。

**重复计数：** 轮询输入目录的次数。 如果端点配置中未指定此值，则使用的默认重复计数。 A value of -1 indicates indefinite scanning of the directory. 默认值是-1。

**Repeat Interval:** The default number if seconds between each poll. 除非在监视的文件夹端点配置中指定了其他值，否则此值将用作重复间隔。 默认值为 5。See the description of the Batch Size setting for additional information.

**异步：** 将调用类型标识为异步或同步。 瞬态和同步进程只能同步调用。 默认值为异步。

**等待时间：** 时间的默认值（以秒为单位），之后从输入文件夹检索文件。 如果文件或文件夹比等待时间中指定的时间早，则会选取该文件或文件夹进行处理。 默认值为 0。

**批大小：** 每次扫描处理的文件或文件夹数的默认值。 默认值为 2。

“重复间隔”和“批量大小”设置决定“监视文件夹”在每次扫描中选取的文件数。 监视文件夹使用Quartz线程池扫描输入文件夹。 线程池与其他服务共享。 如果扫描间隔较小，则线程会经常扫描输入文件夹。 If files are dropped frequently into the watched folder, keep the scan interval small. 如果文件不常被删除，请使用更大的扫描间隔，以便其他服务可以使用线程。

如果丢弃的文件量很大，请使批量变大。 例如，如果监视文件夹端点调用的服务每分钟可处理700个文件，并且用户以相同的速率将文件放入输入文件夹，则将“批量大小”设置为350，将“重复间隔”设置为30秒将帮助监视文件夹性能，而不会太频繁地扫描监视文件夹。

将文件放入监视的文件夹后，它将文件列表在输入中，这在每秒都进行扫描时会降低性能。 增加扫描间隔可以提高性能。 如果被丢弃的文件的体积较小，请相应地调整“批量大小”和“重复间隔”。 例如，如果每秒丢弃10个文件，请尝试将“重复间隔”设置为1秒，将“批量大小”设置为10。

In a cluster configuration, the batch size for a watched folder endpoint does not scale to multiple cluster nodes. 例如，如果将两个节点群集的批量大小设置为 `2` ，并且选择了“节流”选项，则节点将集体处理两个节点的文件，而不是每个节点一次处理两个文件。

**Overwrite Duplicate Filenames:** A Boolean string that specifies whether the watched folder overwrites duplicate result filenames and whether preserved documents of the same name should be overwritten.

**Preserve Folder:** The default value for the preserve folder. This folder is used to copy the source files into in case of successful processing of the input. 此值可以是空路径、相对路径或绝对路径，其文件模式如“结果文件夹”设置中所述。

**Failure Folder:** The name of the folder where the failure files are copied. 此值可以是空路径、相对路径或绝对路径，其文件模式如“结果文件夹”设置中所述。

**结果文件夹：** 结果文件夹的默认名称。 此文件夹用于将结果文件复制到中。 此值可以是具有以下文件模式的空路径、相对路径或绝对路径。

* %F =文件名前缀
* %E =文件扩展名
* %Y =年（已满）
* %y =年（最后两位）
* %M =月
* %D =月日
* %d =年
* %H =小时（24小时制）
* %h =小时（12小时制）
* %m =分钟
* %s =秒
* %l =毫秒
* %R =随机数（从0到9）
* %P =进程或作业ID

例如，如果2009年7月17日晚8点，并且您指定了， `C:/Test/WF0/failure/%Y/%M/%D/%H/`则结果文件夹为 `C:/Test/WF0/failure/2009/07/17/20`。

如果路径不是绝对的，而是相对的，则会在监视的文件夹中创建该文件夹。 有关文件模式的详细信息，请参 [阅关于文件模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。

>[!NOTE]
>
>结果文件夹的大小越小，“监视的文件夹”的性能就越好。 例如，如果监视文件夹的估计负载是每小时1000个文件，请尝试类似的模式，以 `result/%Y%M%D%H` 便每小时创建一个新的子文件夹。 如果负载较小（例如，每天1000个文件），您可以使用类似的模式 `result/%Y%M%D`。

**Stage Folder:** 监视文件夹内舞台文件夹的默认名称。

**输入文件夹：** 监视文件夹内输入文件夹的默认名称。

**失败时保留：** 如果为true，则失败时，原始文件将保留在失败文件夹中。

**节流：** 选择此选项后，将限制AEM表单在任何给定时间处理的已监视文件夹作业的数量。 “批量大小”值确定作业的最大数量（请参阅关于调节）。

## Web服务设置 {#web-service-service-settings}

Web服务( `WebService`)使进程能够调用Web服务操作。

Web服务使进程能够调用Web服务操作。 例如，组织可能希望集成一个过程，以通过调用服务提供商公开的Web服务来存储和检索联系人和帐户详细信息等信息。 Web服务调用指定的Web服务并传递其每个参数的值。 然后，它将操作的返回值保存到进程中的指定变量中。

Web服务通过发送和接收SOAP消息与Web服务交互。 该服务还支持使用WS-Attachment协议将MIME、MTOM和SwaRef附件与SOAP消息一起发送。 Web服务交互与SAP系统和。NET Web服务兼容。

Web服务服务提供以下设置。

**密钥商店：** 包含用于身份验证的私钥的keystore文件的完整路径。 表单服务器必须能够访问文件。

**密钥存储密码：** keystore文件的口令。

**密钥存储类型：** 密钥库的类型。 不提供任何值以使用为运行表单服务器的JVM配置的默认密钥库类型。 否则，请提供以下值之一：

* jks
* pkcs12
* cms
* jceks

**信任商店：** 包含Web服务服务器的公钥的信任存储文件的完整路径。

**信任存储密码：** truststore文件的口令。

**信任存储类型：** 信任存储的类型。 不提供任何值以使用为运行表单服务器的JVM配置的默认密钥库类型。 否则，请提供以下值之一：

* jks
* pkcs12
* cms
* jceks

## XSLT Transformation service settings {#xslt-transformation-service-settings}

XSLT转换服务( `XSLTService`)使进程能够在XML文档上应用可扩展样式表语言转换(XSLT)。

The following setting is available for the XSLT Transformation service.

**Factory Name:** The fully qualified name of the Java class to use for performing XSLT transformations. If no value is specified, the default factory configured in the Java Virtual Machine that runs the forms server is used.

## Modifying security settings for a service {#modifying-security-settings-for-a-service}

forms server enables you to configure security settings for each service, which allows you to configure fine-grained access control on a service-by-service level.

Default security profiles are installed, which can then be configured to meet your system needs. Each security profile has an associated domain and is created at either the user level or the group level.

### 修改服务的安全设置 {#modify-security-settings-for-a-service}

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“服务管理”。
1. 在“服务管理”页面上，单击要配置的服务。
1. Click the Security tab.
1. In the Require Callers To Authenticate list, select either Yes or No to specify whether the service can be invoked with or without credentials.

   If you select Yes, the caller of the service must be authenticated and the user principal for that caller must be authorized to invoke the service; otherwise, the invocation attempt will be refused.

   If you select No, the caller of the service may or may not be authenticated. The invocation of the service will always succeed because there is no authorization check.

1. For services that contain one or more operations flagged for anonymous access, select or deselect Anonymous Access Allowed. When anonymous access is enabled, any user within the system can invoke operations on the service. If anonymous access is disabled, users must be granted permission to call the service and invoke operations. Users are granted these permissions either directly or as being part of a group that has such permissions.
1. For some services, the user account that executes the operation affects the results. For example, in Content Services (Deprecated), the user that stores content is made the owner of the content, which affects who can later access the content. If you are using a process to store content, think about what user is used to execute the Document Management service, because that user will own the stored content.

   To specify the run-time identity used by a service to execute operations, select Specify Run As, select an option from the associated list, and then click Save. 从以下选项中进行选择：

   **Invoker:** Uses the same identity as the user who invoked the service.

   **System:** Uses the System user to run the service with full privileges.

   **Named User:** Enables you to run the service as a specific user. When you select this option, click Select User to display the Select Principal page, where you can search for and select the user.

   如果未选择“指定运行为”，则使用默认行为。

   >[!NOTE]
   >
   >始终使用系统用户帐户执行与xfaForm、文档表单和表单变量一起使用的渲染和提交服务。

1. 单击“添加主体”以指定用户和用户组对此服务具有的权限。
1. “选择主体”屏幕显示在“用户管理”中配置的用户和用户组。 如果未显示所需的用户或用户组，请使用搜索功能查找该用户或用户组。 单击用户或用户组名称。
1. On the Add Permissions screen, select the permissions to assign to the user or group for this service:

   * **INVOKE_PERM:** To invoke all operations on the service
   * **MODIFY_CONFIG_PERM:** To modify the configuration of a service
   * **SUPERVISOR_PERM:** 视图从进程创建的服务的进程实例数据
   * **START_STOP_PERM:** To start and stop a service
   * **ADD_REMOVE_ENDPOINTS_PERM:** 添加、删除和修改服务的端点
   * **CREATE_VERSION_PERM:** To create a new version of the service
   * **DELETE_VERSION_PERM:** To delete a version of the service
   * **MODIFY_VERSION_PERM:** To modify a version of the service
   * **READ_PERM:** To view the service
   * **PROCESS_OWNER_PERM:** For use in a future version of AEM forms. Do not use this permission.
   * **SERVICE_MANAGER_PERM:** For use in a future version of AEM forms. Do not use this permission.
   * **SERVICE_AGENT_PERM:** For use in a future version of AEM forms. Do not use this permission.

1. 单击添加。

### Remove the principal from a security profile {#remove-the-principal-from-a-security-profile}

1. On the Service Management page, select the service to configure.
1. Click the **Security** tab, select the security profile to remove, and click **Remove**.

## Configuring pooling for a service {#configuring-pooling-for-a-service}

每个服务都可以利用池功能来处理传入的调用请求。 使用服务池确保服务实例由单个线程一次调用，并在调用请求之间重复使用，这可能导致性能的改善。 您还可以使用池指定“最大异步服务实例”选项，此选项允许服务限制并行处理的请求数。

### 启用池 {#enable-pooling}

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“服务管理”。
1. 在“服务管理”页面上，单击要配置的服务。
1. 单击“池”选项卡。
1. 在“请求处理策略”列表中，为所有请求选择池化实例。
1. 在“初始服务实例池大小”框中，输入池的初始大小。 部署服务时，此编号用于确定在等待调用请求时创建并分配给空闲池的服务实现实例的数量。 这使得服务容器能够立即响应调用请求而不必首先初始化服务实例。
1. 在“最大服务实例池大小”框中，输入给定服务的池中的最大实例数。 此设置控制在给定时间可执行给定服务的线程数。 The default value is 0, which results in unlimited pool size.
1. 在“最大异步服务实例数”框中，输入池中可用于在任何给定时间为异步请求提供服务的最大实例数。 This setting allows the service to limit the number of requests that it can handle in parallel.
1. In the Invocation Wait Timeout box, enter the number of milliseconds to wait for a service to become available for an invocation request. 如果未指定此设置的值，则默认值为0，这将导致无等待时间。
1. 单击保存。

### Remove pooling {#remove-pooling}

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“服务管理”。
1. 在“服务管理”页面上，单击要配置的服务。
1. 单击“池”选项卡。
1. 在“请求处理策略”列表中，为每个请求选择“新实例”或为所有请求选择“单个实例”。

   **所有请求的单个实例：** 当第一个请求进入容器时，将创建并缓存服务实例。 请求后的每个请求都使用相同的服务实例来处理请求。

   **每个请求的新实例：** 为收到的每个调用创建新的服务实例。

1. 单击保存。

