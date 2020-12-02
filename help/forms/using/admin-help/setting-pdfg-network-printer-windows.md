---
title: 设置PDFG网络打印机（仅限Windows）
seo-title: 设置PDFG网络打印机（仅限Windows）
description: 了解如何设置PDFG网络打印机（仅限Windows）
seo-description: 了解如何设置PDFG网络打印机（仅限Windows）
uuid: 13b8481e-5ef0-4a07-9602-7bc4d9e05dd4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7620e5e4-022e-49b2-8cfe-d5eec8ab99d7
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---


# 设置PDFG网络打印机（仅限Windows）{#setting-up-a-pdfg-network-printer-windows-only}

PDFG网络打印机允许用户从支持打印的任何应用程序生成PDF文档。 用户安装PDFG网络打印机后，Windows控制面板的“打印机”部分将显示名为&#x200B;*PDF generator*&#x200B;的新打印机。 如果具有相同名称的打印机已存在，则系统会提示用户提供其他名称。

从任何应用程序打印到此打印机会将文档（PostScript格式）发送到PDF生成器，PDF生成器会将PostScript文件转换为PDF。 根据您配置PDF Generator的方式，它以电子邮件消息附件的形式向用户发送PDF文档，将PDF文档转发到指定的AEM表单服务或进程，或同时执行这两个操作。

设置PDFG网络打印机需要以下步骤：

1. 配置电子邮件设置。 （请参阅[为PDFG网络打印机配置电子邮件设置](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer)。）
1. 在管理控制台中，配置PDFG网络打印机设置。 （请参阅[配置PDFG网络打印机设置](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings)。）
1. 确保您的用户在AEM forms数据库中配置了有效的电子邮件地址，并为每个用户分配PDFGUserPermission。<!-- Fix broken link See Setting up and organizing users -->
1. 确保用户的计算机上已安装32位JRE6。
1. 在用户的计算机上安装打印机。 （请参阅[在用户的计算机上安装PDFG网络打印机](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer)。）

## 为PDFG网络打印机{#configure-email-settings-for-pdfg-network-printer}配置电子邮件设置

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“服务管理”。
1. 在“服务管理”页上，单击provider.email_sendmail_service，指定SMTP设置，然后单击“保存”。

## 配置PDFG网络打印机设置{#configure-the-pdfg-network-printer-settings}

1. 在管理控制台中，单击“服务”>“PDF生成器”>“PDFG网络打印机”
1. 在“Adobe PDF设置”和“安全设置”列表中，选择要应用于生成的PDF的选项。 有关这些设置的详细信息，请参阅[配置Adobe PDF设置](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings)和[配置安全设置](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings)。
1. 要将转换的PDF发送回用户，请选择“通过电子邮件将转换的PDF文件发回给用户”选项并指定以下信息：

   * 用于向用户发送PDF的电子邮件地址
   * 电子邮件的主题
   * 电子邮件的页眉、正文和页脚。 在电子邮件中，&lt;receiverName>将替换为打印文档的用户的全名。

1. 要将转换的PDF发送到AEM表单服务或进程，请选择“将转换的PDF转发到指定的AEM表单服务或进程”选项并指定以下信息：

   * 要调用的服务的名称
   * 要调用的服务的操作的名称
   * 输入参数的名称，在服务或进程的component.xml文件中指定。 PDF文档将用作该输入参数的值。

1. 单击保存。

如果要还原到原始的默认电子邮件文本，请单击“恢复电子邮件内容”。

## 在用户的计算机{#install-pdfg-network-printer-on-a-user-s-computer}上安装PDFG网络打印机

具有PDFG管理员或PDFG用户角色的用户可以安装PDFG网络打印机。 计算机上必须安装32位JDK。

1. （PDFG管理员）在管理控制台中，单击“服务”>“PDF生成器”>“PDFG网络打印机”。

   （PDFG用户）转至`http(s)://[host]:'port'/pdfgui`并单击“PDFG网络打印机安装”下的链接。

1. 在“PDFG Network Printer Installation（PDFG网络打印机安装）”下，单击链接。 当提示输入用户帐户信息时，请指定您在步骤1中用于登录的用户名和密码。 出现一条消息，表示打印机已成功安装。

   ***注&#x200B;**:如果用户的密码发生更改，则用户需要在其计算机上重新安装PDFG网络打印机。无法从管理控制台更新密码。*

1. 单击确定。

