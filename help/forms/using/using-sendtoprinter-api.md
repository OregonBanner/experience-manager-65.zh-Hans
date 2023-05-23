---
title: 使用sendToPrint API
seo-title: Using the sendToPrinter API
description: 使用sendToPrinter服務將檔案傳送至印表機。
seo-description: Using the sendToPrinter service to send a document to printer.
uuid: c6a3fe8d-ec19-4350-b4a6-4c3d1971b501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: c2d564ba-fa5a-4130-b7fe-7e2c64d92170
exl-id: 5fb38afd-7517-494e-b084-1fdd4aef3ca4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 14%

---

# 使用sendToPrint API {#using-the-sendtoprinter-api}

## 概述 {#overview}

在AEM Forms中，您可以使用SendToPrinter服務將檔案傳送至印表機。 SendToPrinter服務支援下列列印存取機制：

* **可直接存取的印表機** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **可間接存取的印表機** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

   將檔案傳送至印表機時，請指定下列列印通訊協定之一：

   * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * &quot;**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS**：輸出服務支援通用網際網路檔案系統(CIFS)列印通訊協定。

## 使用SendToPrinter服務 {#using-sendtoprinter-service}

下表列出：

* 有關用於各種通訊協定的printerName或printServer的資訊。
* 印表機傳回印表機伺服器URI和印表機名稱的各種組合的值或例外狀況

| 通訊協定（存取機制） | 列印伺服器URI (PrinterSpec.printServer) | 印表機名稱(PrinterSpec.printerName) | 结果 |
|--- |--- |--- |--- |
| SharedPrinter | 任意 | 空 | 例外：必要的引數sPrinterName不得為空白。 |
| SharedPrinter | 任意 | 无效 | 例外狀況指出找不到印表機。 |
| SharedPrinter | 任意 | 有效 | 列印工作成功。 |
| LPD | 空 | 任意 | 例外狀況指出必要的引數sPrintServerUri不得為空白。 |
| LPD | 无效 | 空 | 例外狀況指出必要的引數sPrinterName不得為空白。 |
| LPD | 无效 | 非空白 | 例外狀況指出找不到sPrintServerUri。 |
| LPD | 有效 | 无效 | 例外狀況指出找不到印表機。 |
| LPD | 有效 | 有效 | 成功的列印工作。 |
| CUP | 空 | 任意 | 例外狀況指出必要的引數sPrintServerUri不得為空白。 |
| CUP | 无效 | 任意 | 例外狀況指出找不到印表機。 |
| CUP | 有效 | 任意 | 列印工作成功。 |
| DirectIP | 空 | 任意 | 例外狀況指出必要的引數sPrintServerUri不得為空白。 |
| DirectIP | 无效 | 任意 | 例外狀況指出找不到印表機。 |
| DirectIP | 有效 | 任意 | 列印工作成功。 |
| CIFS | 有效 | 空 | 列印工作成功。 |
| CIFS | 无效 | 任意 | 使用CIFS列印時發生未知錯誤。 |
| CIFS | 空 | 任意 | 例外狀況指出必要的引數sPrintServerUri不得為空白。 |

## 驗證支援 {#authentication-support}

只有CIFS列印支援驗證。 若要驗證，請在PrinterSpec中提供使用者名稱/密碼/網域。 您可以透過下列步驟，使用AEM Granite CyprtoSupport Service加密密碼：

1. 前往https://&lt;server>：&lt;port>/system/console。

1. 前往 **[!UICONTROL 主要]** > **[!UICONTROL 加密支援]**.

1. 輸入一些純文字，然後按一下 **[!UICONTROL Protect]**.
