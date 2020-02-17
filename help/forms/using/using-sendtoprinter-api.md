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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用sendToPrinter API {#using-the-sendtoprinter-api}

## 概述 {#overview}

在AEM Forms中，可以使用SendToPrinter服务将文档发送到打印机。 SendToPrinter服务支持以下打印访问机制：

* **可直接访问的打印机**`: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **间接可访问的打印机**`: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

   将文档发送到打印机时，请指定以下打印协议之一：

   * **CUPS**`: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * ``**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * ``**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter**`: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS**:输出服务支持通用Internet文件系统(CIFS)打印协议。

## 使用SendToPrinter Service {#using-sendtoprinter-service}

下表列出：

* 有关printerName或printServer以用于各种协议的信息。
* 打印机为打印机服务器URI和打印机名称的各种组合返回的值或例外

| 协议（访问机制） | 打印服务器URI(PrinterSpec.printServer) | 打印机的名称(PrinterSpec.printerName) | 结果 |
|--- |--- |--- |--- |
| SharedPrinter | 任意 | 空 | 例外：必需参数sPrinterName不能为空。 |
| SharedPrinter | 任意 | 无效 | 出现异常情况，表示找不到打印机。 |
| SharedPrinter | 任意 | 有效 | 成功的打印作业。 |
| LPD | 空 | 任意 | 表示必需参数sPrintServerUri不能为空的例外。 |
| LPD | 无效 | 空 | 表示必需参数sPrinterName不能为空的例外。 |
| LPD | 无效 | 不为空 | 一个异常，表示未找到sPrintServerUri。 |
| LPD | 有效 | 无效 | 表示找不到打印机的例外。 |
| LPD | 有效 | 有效 | 成功的打印作业。 |
| CUP | 空 | 任意 | 表示必需参数sPrintServerUri不能为空的例外。 |
| CUP | 无效 | 任意 | 表示找不到打印机的例外。 |
| CUP | 有效 | 任意 | 成功的打印作业。 |
| DirectIP | 空 | 任意 | 表示必需参数sPrintServerUri不能为空的例外。 |
| DirectIP | 无效 | 任意 | 表示找不到打印机的例外。 |
| DirectIP | 有效 | 任意 | 成功的打印作业。 |
| CIFS | 有效 | 空 | 成功的打印作业。 |
| CIFS | 无效 | 任意 | 使用CIFS进行打印时出现未知错误。 |
| CIFS | 空 | 任意 | 表示必需参数sPrintServerUri不能为空的例外。 |

## 身份验证支持 {#authentication-support}

身份验证仅支持CIFS打印。 要进行身份验证，请在PrinterSpec中提供用户名／密码／域。 您可以通过执行以下步骤，使用AEM Granite CyprotoSupport服务加密口令：

1. 转到https://&lt;server>:&lt;port>/system/console。

1. 转到“主 **[!UICONTROL 要]** ”>“ **[!UICONTROL 加密支持”]**。

1. 输入一些纯文本，然后单击“保 **[!UICONTROL 护”]**。

