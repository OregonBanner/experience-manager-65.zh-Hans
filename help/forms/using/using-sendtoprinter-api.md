---
title: 使用sendToPrinter API
seo-title: 使用sendToPrinter API
description: 使用sendToPrinter服务将文档发送到打印机。
seo-description: 使用sendToPrinter服务将文档发送到打印机。
uuid: c6a3fe8d-ec19-4350-b4a6-4c3d1971b501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: c2d564ba-fa5a-4130-b7fe-7e2c64d92170
exl-id: 5fb38afd-7517-494e-b084-1fdd4aef3ca4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 13%

---

# 使用sendToPrinter API {#using-the-sendtoprinter-api}

## 概述 {#overview}

在AEM Forms中，您可以使用SendToPrinter服务将文档发送到打印机。 SendToPrinter服务支持以下打印访问机制：

* **可直接访问的打印机** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **间接可访问的打印机** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

   将文档发送到打印机时，请指定以下打印协议之一：

   * **杯子** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * &quot;**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS**:输出服务支持通用Internet文件系统(CIFS)打印协议。

## 使用SendToPrinter服务{#using-sendtoprinter-service}

下表列出：

* 有关用于各种协议的printerName或printServer的信息。
* 打印机返回的打印机服务器URI和打印机名称的各种组合的值或例外

| 协议（访问机制） | 打印服务器URI(PrinterSpec.printServer) | 打印机的名称(PrinterSpec.printerName) | 结果 |
|--- |--- |--- |--- |
| SharedPrinter | 任意 | 空 | 例外：必需参数sPrinterName不能为空。 |
| SharedPrinter | 任意 | 无效 | 出现异常，表示找不到打印机。 |
| SharedPrinter | 任意 | 有效 | 打印作业成功。 |
| LPD | 空 | 任意 | 表示必需参数sPrintServerUri不能为空的异常。 |
| LPD | 无效 | 空 | 表示必需参数sPrinterName不能为空的异常。 |
| LPD | 无效 | 不为空 | 未找到sPrintServerUri的异常。 |
| LPD | 有效 | 无效 | 表示找不到打印机的异常。 |
| LPD | 有效 | 有效 | 成功的打印作业。 |
| CUP | 空 | 任意 | 表示必需参数sPrintServerUri不能为空的异常。 |
| CUP | 无效 | 任意 | 表示找不到打印机的异常。 |
| CUP | 有效 | 任意 | 打印作业成功。 |
| DirectIP | 空 | 任意 | 表示必需参数sPrintServerUri不能为空的异常。 |
| DirectIP | 无效 | 任意 | 表示找不到打印机的异常。 |
| DirectIP | 有效 | 任意 | 打印作业成功。 |
| CIFS | 有效 | 空 | 打印作业成功。 |
| CIFS | 无效 | 任意 | 使用CIFS打印时出现未知错误。 |
| CIFS | 空 | 任意 | 表示必需参数sPrintServerUri不能为空的异常。 |

## 身份验证支持{#authentication-support}

仅CIFS打印支持身份验证。 要进行身份验证，请在PrinterSpec中提供用户名/密码/域。 您可以通过执行以下步骤，使用AEM Granite CyprotoSupport服务加密密码：

1. 转到https://&lt;server>:&lt;port>/system/console。

1. 转到&#x200B;**[!UICONTROL Main]** > **[!UICONTROL Crypto Support]**。

1. 输入一些纯文本，然后单击&#x200B;**[!UICONTROL Protect]**。
