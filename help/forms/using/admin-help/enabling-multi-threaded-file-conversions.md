---
title: 启用多线程文件转换
description: 了解如何启用多线程文件转换。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# 启用多线程文件转换 {#enabling-multi-threaded-file-conversions}

PDF Generator允许您为某些类型的文件启用多线程文件转换。 多线程文件转换允许同时执行多个转换，从而提高了PDF Generator的性能。

## 为OpenOffice、Word和PowerPoint文档启用多线程文件转换 {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

默认情况下，PDF Generator一次只能转换一个OpenOffice®Microsoft、Word或PowerPoint文档。 如果启用多线程转换，则PDF Generator可以同时转换多个文档。 PDF Generator会启动多个OpenOffice或PDFMaker实例（用于执行Word和PowerPoint转换）。

>[!NOTE]
>
>Microsoft® Word 2003和PowerPoint 2003不支持多线程文件转换。 要启用多线程文件转换，请升级到Microsoft® Word 2007和PowerPoint 2007或Microsoft®Word 2010和PowerPoint 2010。

>[!NOTE]
>
Microsoft® Excel、Microsoft® Visio、Microsoft® Project或Microsoft® Publisher不支持多线程文件转换。

每个OpenOffice或PDFMaker实例都使用单独的用户帐户启动。 您添加的每个用户帐户都必须是具有对Forms Server计算机的管理权限的有效用户。 在群集环境中，同一组用户必须对群集的所有节点有效。

在管理控制台的“用户帐户”页上，可以指定用于多线程文件转换的用户帐户。 您可以添加帐户、删除帐户或更改帐户密码。 如果在Windows Server 2003或Windows Server 2008上运行PDF Generator，请至少添加三个具有管理员权限的用户帐户。

在Windows Server 2003或2008上添加OpenOffice、Microsoft® Word或Microsoft®PowerPoint，或者在Linux®或Sun™ Solaris™上添加OpenOffice的用户时，为所有用户关闭初始激活对话框。

### 添加权限以替换进程级令牌 {#add-the-right-to-replace-the-process-level-token}

在Windows操作系统上，用于PDF转换的管理员用户帐户（PDFG用户）必须替换进程级别的令牌权限。 您可以使用组策略编辑器添加此权限：

1. 在Windows“开始”菜单中，单击“运行”，然后输入gpedit.msc。
1. 单击“本地计算机策略”>“计算机配置”>“Windows设置”>“安全设置”>“本地策略”>“用户权限分配”。 编辑 *替换进程级令牌* 包含Administrators组的策略。
1. 将用户添加到“替换进程级令牌”条目。

### Windows Server 2008上的OpenOffice、Microsoft®Word和Microsoft®PowerPoint所需的其他配置 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

如果您在Windows Server 2008上运行OpenOffice、Microsoft®Word或Microsoft®PowerPoint，请为添加的每个用户禁用UAC。

1. 单击“控制面板”>“用户帐户”>“打开或关闭用户帐户控制”。
1. 取消选中“Use User Account Control (UAC) to help protect your computer(使用用户帐户控制(UAC)帮助保护计算机)”框，然后单击“OK（确定）”。
1. 重新启动计算机以使设置生效。

### Linux®或Solaris™上的OpenOffice所需的其他配置 {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. 添加用户帐户。 (请参阅 [添加用户帐户](enabling-multi-threaded-file-conversions.md#add-a-user-account).)
1. 接下来，必须更改/etc/sudoers文件。 此文件的默认权限为440。 将此文件的权限更改为可写。
1. 在/etc/sudoers文件中为其他用户(除运行Forms服务器的管理员之外)添加条目。 例如，如果您以名为lcadm的用户和名为myhost的服务器的身份运行AEM表单，并且要模拟user1和user2，请将以下条目添加到/etc/sudoers中：

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   此配置使lcadm能够以“user1”或“user2”在主机“myhost”上运行任何命令而不提示输入密码。

   >[!NOTE]
   >
   确保已将系统用户和PDFG用户角色分配给“user1”和“user2” 。 要将PDFG角色分配给用户，请参阅 [添加用户帐户](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. 此外，在/etc/sudoers文件中，通过在行首添加数字符号(#)来查找并注释掉此行：

   ```shell
   Defaults requiretty
   ```

   这使您能够添加Linux®用户。

1. 将etc/sudoers文件的权限更改回440。
1. 允许您通过添加的所有用户 [添加用户帐户](enabling-multi-threaded-file-conversions.md#add-a-user-account) 以连接到Forms服务器。 例如，要授予名为user1的本地用户连接到Forms服务器的权限，请使用以下命令

   `xhost +local:user1@`

   有关更多详细信息，请参阅xhost命令文档。

1. 重新启动服务器。

>[!NOTE]
>
OpenOffice必须安装在所有PDFG用户可以访问的目录位置。 您可以通过以PDFG用户身份登录并检查是否可以正常启动OpenOffice来验证这一点。

### 添加用户帐户 {#add-a-user-account}

1. 在管理控制台中，单击服务>PDF Generator>用户帐户。
1. 单击添加，然后输入在Forms服务器上具有管理权限的用户的用户名和密码。 如果要为OpenOffice配置用户，请关闭初始OpenOffice激活对话框。

   >[!NOTE]
   >
   如果为OpenOffice配置用户，OpenOffice实例数不能大于此步骤中指定的用户帐户数。

1. 重新启动Forms服务器。

### 从用于多线程文件转换的列表中删除用户 {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. 在管理控制台中，单击服务>PDF Generator>用户帐户。
1. 单击要删除的用户旁边的复选框，然后单击删除。
1. 在确认页面上，单击删除。
1. 重新启动Forms服务器。

### 更改帐户的密码 {#change-the-password-for-an-account}

1. 在管理控制台中，单击服务>PDF Generator>用户帐户。
1. 单击用户名，然后输入并确认新密码。 此密码必须与用户的系统密码匹配。
