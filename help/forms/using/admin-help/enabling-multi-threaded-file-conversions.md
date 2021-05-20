---
title: 启用多线程文件转换
seo-title: 启用多线程文件转换
description: 了解如何启用多线程文件转换。
seo-description: 了解如何启用多线程文件转换。
uuid: 830c78aa-4f68-4e01-8b24-69a0275689c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 85d655bb-1b6b-4b4d-ae39-eca3ef9b7fd7
feature: PDF 生成器
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---

# 启用多线程文件转换{#enabling-multi-threaded-file-conversions}

PDF生成器为某些类型的文件提供了启用多线程文件转换的功能。 多线程文件转换允许PDF生成器同时执行多次转换，从而提高了其性能。

## 为OpenOffice、Word和PowerPoint文档{#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}启用多线程文件转换

默认情况下，PDF生成器一次只能转换一个OpenOffice、Microsoft Word或PowerPoint文档。 如果启用多线程转换，则PDF生成器可以同时转换多个文档。 PDF生成器将启动OpenOffice或PDFMaker的多个实例（用于执行Word和PowerPoint转换）。

>[!NOTE]
>
>Microsoft Word 2003和PowerPoint 2003不支持多线程文件转换。 要启用多线程文件转换，请升级到Microsoft Word 2007和PowerPoint 2007或Microsoft Word 2010和PowerPoint 2010。

>[!NOTE]
>
>Microsoft Excel、Microsoft Visio、Microsoft Project或Microsoft Publisher不支持多线程文件转换。

OpenOffice或PDFMaker的每个实例都使用单独的用户帐户启动。 您添加的每个用户帐户都必须是在Forms服务器计算机上具有管理权限的有效用户。 在群集环境中，同一组用户必须对群集的所有节点都有效。

在管理控制台的“用户帐户”页面上，您可以指定用于多线程文件转换的用户帐户。 您可以添加帐户、删除帐户或更改帐户密码。 如果您在Windows Server 2003或Windows Server 2008上运行PDF生成器，请至少添加三个具有管理员权限的用户帐户。

在Windows Server 2003或2008上为OpenOffice、Microsoft Word或Microsoft PowerPoint添加用户，或在Linux或Sun™ Solaris™上为OpenOffice添加用户时，请取消所有用户的初始激活对话框。

### 添加替换进程级令牌{#add-the-right-to-replace-the-process-level-token}的权限

在Windows操作系统上，用于PDF转换（PDFG用户）的管理员用户帐户将需要替换进程级别的令牌权限。 您可以使用组策略编辑器添加此权限：

1. 在“Windows开始”菜单中，单击“运行”，然后输入gpedit.msc。
1. 单击“本地计算机策略”>“计算机配置”>“Windows设置”>“安全设置”>“本地策略”>“用户权限分配”。 编辑&#x200B;*替换进程级别令牌*&#x200B;策略以包含Administrators组。
1. 将用户添加到替换进程级别令牌条目。

### Windows Server 2008 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}上的OpenOffice、Microsoft Word和Microsoft PowerPoint所需的其他配置

如果您在Windows Server 2008上运行OpenOffice、Microsoft Word或Microsoft PowerPoint，请为添加的每个用户禁用UAC。

1. 单击控制面板>用户帐户>打开或关闭用户帐户控制。
1. 取消选中“使用用户帐户控制(UAC)帮助保护计算机”框，然后单击“确定”。
1. 重新启动计算机以使设置生效。

### Linux或Solaris {#additional-configuration-required-for-openoffice-on-linux-or-solaris}上的OpenOffice所需的其他配置

1. 添加用户帐户。 （请参阅[添加用户帐户](enabling-multi-threaded-file-conversions.md#add-a-user-account)。）
1. 接下来，您将对/etc/sudoers文件进行更改。 此文件的默认权限为440。 将此文件的权限更改为可写。
1. 在/etc/sudoers文件中为其他用户（运行表单服务器的管理员除外）添加条目。 例如，如果您以名为lcadm的用户和名为myhost的服务器的身份运行AEM表单，并且要模拟user1和user2，请将以下条目添加到/etc/sudoers:

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   此配置使lcadm能够在主机“myhost”上以“user1”或“user2”的形式运行任何命令，而无需提示输入密码。

   >[!NOTE]
   >
   >确保已将系统用户和PDFG用户角色分配给“user1”和“user2”。 要向用户分配PDFG角色，请参阅[添加用户帐户](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. 此外，在/etc/sudoers文件中，通过在行的开头添加数字符号(#)来找到此行并注释掉：

   ```shell
   Defaults requiretty
   ```

   这样您就可以添加Linux用户。

1. 将etc/sudoers文件的权限更改回440。
1. 允许您通过[添加用户帐户](enabling-multi-threaded-file-conversions.md#add-a-user-account)添加的所有用户与表单服务器建立连接。 例如，要允许名为user1的本地用户具有与表单服务器建立连接的权限，请使用以下命令

   `xhost +local:user1@`

   有关更多详细信息，请参阅xhost命令文档。

1. 重新启动服务器。

>[!NOTE]
>
>必须将OpenOffice安装在所有PDFG用户都可以访问的目录位置中。 您可以以PDFG用户身份登录并检查是否可以在无问题的情况下启动OpenOffice来验证这一点。

### 添加用户帐户{#add-a-user-account}

1. 在管理控制台中，单击“服务”>“PDF生成器”>“用户帐户”。
1. 单击添加，然后输入对表单服务器具有管理权限的用户的用户名和密码。 如果要为OpenOffice配置用户，请关闭初始的OpenOffice激活对话框。

   >[!NOTE]
   >
   >如果为OpenOffice配置用户，则OpenOffice的实例数不能大于此步骤中指定的用户帐户数。

1. 重新启动表单服务器。

### 从用于多线程文件转换的列表{#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}中删除用户

1. 在管理控制台中，单击“服务”>“PDF生成器”>“用户帐户”。
1. 单击要删除的用户旁边的复选框，然后单击删除。
1. 在确认页面上，单击删除。
1. 重新启动表单服务器。

### 更改帐户{#change-the-password-for-an-account}的密码

1. 在管理控制台中，单击“服务”>“PDF生成器”>“用户帐户”。
1. 单击用户名，然后输入并确认新密码。 此密码必须与用户的系统密码匹配。
