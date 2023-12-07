---
title: 使用sendToPrinter API
description: 使用sendToPrinter服务将文档发送到打印机。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
exl-id: 5fb38afd-7517-494e-b084-1fdd4aef3ca4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 14%

---

# 使用sendToPrinter API {#using-the-sendtoprinter-api}

## 概述 {#overview}

在AEM Forms中，您可以使用SendToPrinter服务将文档发送到打印机。 SendToPrinter服务支持以下打印访问机制：

* **直接访问的打印机** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **可间接访问的打印机** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

  在将文档发送到打印机时，请指定以下打印协议之一：

   * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * &quot;**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **共享打印机** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIF**：输出服务支持通用Internet文件系统(CIF)打印协议。

## 使用SendToPrinter服务 {#using-sendtoprinter-service}

下表列出了：

* 有关用于各种协议的printerName或printServer的信息。
* 打印机为打印机服务器URI和打印机名称的各种组合返回的值或异常

| 协议（访问机制） | 打印服务器URI (PrinterSpec.printServer) | 打印机的名称(PrinterSpec.printerName) | 结果 |
|--- |--- |--- |--- |
| SharedPrinter | 任意 | 空 | 异常：必需的参数sPrinterName不能为空。 |
| SharedPrinter | 任意 | 无效 | 出现异常，指出找不到打印机。 |
| SharedPrinter | 任意 | 有效 | 打印作业成功。 |
| LPD | 空 | 任意 | 出现异常，指示所需的参数sPrintServerUri不能为空。 |
| LPD | 无效 | 空 | 出现异常，指示所需的参数sPrinterName不能为空。 |
| LPD | 无效 | 不为空 | 表示未找到sPrintServerUri的异常。 |
| LPD | 有效 | 无效 | 出现异常，说明找不到打印机。 |
| LPD | 有效 | 有效 | 成功的打印作业。 |
| CUP | 空 | 任意 | 出现异常，指示所需的参数sPrintServerUri不能为空。 |
| CUP | 无效 | 任意 | 出现异常，说明找不到打印机。 |
| CUP | 有效 | 任意 | 打印作业成功。 |
| DirectIP | 空 | 任意 | 出现异常，指示所需的参数sPrintServerUri不能为空。 |
| DirectIP | 无效 | 任意 | 出现异常，说明找不到打印机。 |
| DirectIP | 有效 | 任意 | 打印作业成功。 |
| CIFS | 有效 | 空 | 打印作业成功。 |
| CIFS | 无效 | 任意 | 使用CIF打印时出现未知错误。 |
| CIFS | 空 | 任意 | 出现异常，指示所需的参数sPrintServerUri不能为空。 |

## 身份验证支持 {#authentication-support}

只有CIF打印支持身份验证。 要进行身份验证，请在PrinterSpec中提供用户名/密码/域。 可以通过执行以下步骤使用AEM Granite CyprtoSupport服务加密口令：

1. 转到https://&lt;server>：&lt;port>/system/console。

1. 转到 **[!UICONTROL 主要]** > **[!UICONTROL 加密支持]**.

1. 输入一些纯文本，然后单击 **[!UICONTROL Protect]**.
