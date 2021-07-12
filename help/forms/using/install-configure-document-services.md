---
title: 安装和配置文档服务
seo-title: 安装和配置文档服务
description: 安装AEM Forms文档服务以创建、组合、分发、存档PDF文档、添加数字签名以限制对文档的访问，以及对条形码表单进行解码。
seo-description: 安装AEM Forms文档服务以创建、组合、分发、存档PDF文档、添加数字签名以限制对文档的访问，以及对条形码表单进行解码。
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
role: Admin
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '4295'
ht-degree: 2%

---

# 安装和配置文档服务 {#installing-and-configuring-document-services}

AEM Forms提供一组OSGi服务来完成不同的文档级操作，例如，创建、组合、分发和存档PDF文档、添加数字签名以限制对文档的访问以及对条形码表单进行解码的服务。 这些服务包含在AEM Forms附加组件包中。 这些服务统称为文档服务。 可用文档服务及其主要功能列表如下：

* **汇编程序服务：** 允许您组合、重新排列和扩充PDF和XDP文档，并获取有关PDF文档的信息。它还有助于将PDF文档转换为PDF/A标准，将PDF forms、XML表单和PDF forms转换为PDF/A-1b、PDF/A-2b和PDFA/A-3b。 有关更多信息，请参阅[汇编程序服务](/help/forms/using/assembler-service.md)。

* **ConvertPDF服务：** 允许您将PDF文档转换为PostScript或图像文件（JPEG、JPEG 2000、PNG和TIFF）。有关更多信息，请参阅[ConvertPDF Service](/help/forms/using/using-convertpdf-service.md)。

* **条形码Forms服务：** 允许您从条形码的电子图像中提取数据。该服务接受包含一个或多个条形码的TIFF和PDF文件作为输入，并提取条形码数据。 有关更多信息，请参阅[条形码Forms服务](/help/forms/using/using-barcoded-forms-service.md)。

* **DocAssurance服务：** 允许您加密和解密文档，扩展具有其他使用权限的Adobe Reader功能，以及向文档添加数字签名。文档保障服务包含三项服务：签名、加密和读取器扩展。 有关详细信息，请参阅[DocAssurance Service](/help/forms/using/overview-aem-document-services.md)。

* **加密服务：** 允许您加密和解密文档。文档加密后，其内容将变得不可读。 授权用户可以解密文档以获得对其内容的访问。 有关更多信息，请参阅[Encryption Service](/help/forms/using/overview-aem-document-services.md#encryption-service)。

* **Forms服务：** 允许您创建交互式数据捕获客户端应用程序，以验证、处理、转换和交付通常在Forms Designer中创建的表单。Forms服务可呈现您开发为PDF文档的任何表单设计。 有关更多信息，请参阅[Forms服务](/help/forms/using/forms-service.md)。

* **输出服务：** 允许您创建不同格式的文档，包括PDF、激光打印机格式和标签打印机格式。激光打印机格式为PostScript和打印机控制语言(PCL)。 有关更多信息，请参阅[输出服务](/help/forms/using/output-service.md)。

* **PDF生成器服务：** PDF生成器服务提供了API，可将本机文件格式转换为PDF。它还可将PDF转换为其他文件格式，并优化PDF文档的大小。 有关更多信息，请参阅[PDF生成器服务](aem-document-services-programmatically.md#pdfgeneratorservice)。

* **Reader扩展服务：** 通过扩展Adobe Reader的功能（具有其他使用权限），您的组织可以轻松共享交互式PDF文档。该服务可激活在使用Adobe Reader打开PDF文档时不可用的功能，例如向文档添加注释、填写表单和保存文档。 有关更多信息，请参阅[Reader扩展服务](/help/forms/using/overview-aem-document-services.md#reader-extension-service)。

* **签名服务：** 允许您在AEM服务器上处理数字签名和文档。例如，签名服务通常用于以下情况：

   * AEM服务器会在将表单发送到用户以使用Acrobat或Adobe Reader打开之前对其进行验证。
   * AEM服务器将验证已使用Acrobat或Adobe Reader添加到表单的签名。
   * AEM服务器代表公证员签署表格。

   签名服务访问存储在信任存储中的证书和凭据。 有关更多信息，请参阅[签名服务](/help/forms/using/aem-document-services-programmatically.md)。

AEM Forms是一个功能强大的企业级平台，而文档服务只是AEM Forms的一项功能。 有关功能的完整列表，请参阅[AEM Forms简介](/help/forms/using/introduction-aem-forms.md)。

## 部署拓扑 {#deployment-topology}

AEM Forms附加组件包是部署在AEM上的应用程序。 通常，运行AEM Forms文档服务只需要一个AEM实例（创作或发布）。 建议使用以下拓扑来运行AEM Forms文档服务。 有关拓扑的详细信息，请参阅[AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md)的架构和部署拓扑。

![AEM Forms的架构和部署拓扑](do-not-localize/document-services.png)

>[!NOTE]
>
>尽管AEM Forms允许您从单个服务器设置并运行所有功能，但您应该执行容量规划、负载平衡，并为生产环境中的特定功能设置专用服务器。 例如，对于使用PDF生成器服务来转换每天数千页的环境和用于捕获数据的多个自适应表单，为PDF生成器服务和自适应表单功能分别设置单独的AEM Forms服务器。 它有助于提供最佳性能，并可以相互独立地扩展服务器。

## 系统要求 {#system-requirements}

在开始安装和配置AEM Forms文档服务之前，请确保：

* 硬件和软件基础架构已到位。 有关支持的硬件和软件的详细列表，请参见[技术要求](/help/sites-deploying/technical-requirements.md)。

* AEM实例的安装路径不包含空格。
* AEM实例已启动且正在运行。 在AEM术语中，“实例”是在创作或发布模式下的服务器上运行的AEM的副本。 通常，运行AEM Forms文档服务只需要一个AEM实例（创作或发布）：

   * **作者**:用于创建、上传和编辑内容以及管理网站的AEM实例。内容准备就绪后，即会复制到发布实例。
   * **发布**:通过Internet或内部网络向公众提供已发布内容的AEM实例。

* 满足内存要求。 AEM Forms附加组件包需要：

   * 15 GB的临时空间，用于基于Microsoft Windows的安装。
   * 6 GB的临时空间，用于基于UNIX的安装。

* 安装了PDF生成器在Microsoft Windows和Linux上执行转换所需的客户端软件：

   * **Microsoft Windows**:安 [装](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)Microsoft  [Office或Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux**:安 [装Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* 在Microsoft Windows上，PDF生成器支持WebKit、Acrobat WebCapture和PhantomJS转换路由，以将HTML文件转换为PDF文档。
>* 在基于UNIX的操作系统上，PDF生成器支持WebKit和PhantomJS转换路由，以将HTML文件转换为PDF文档。

>



### 基于UNIX的操作系统的额外要求 {#extrarequirements}

如果您使用基于UNIX的操作系统，请从相应操作系统的安装介质安装以下软件包：

<table> 
 <tbody> 
  <tr> 
   <td> 
    <ul> 
     <li>expat</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libxcb</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>自由类型</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXau</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 
    <ul> 
     <li>libSM</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>zlib</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libICE</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libuuid</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 
    <ul> 
     <li>glibc</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXext</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>nss-softokn-freebl</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>fontconfig</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 
    <ul> 
     <li>libX11</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXrender</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXrandr</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXinerama</li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

* **(仅限PDF生成器**)安装32位版本的libcurl、libcrypto和libssl库，并创建以下符号链接。符号链接指向相应库的最新版本：

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **（仅限PDF生成器）** PDF生成器服务支持通过WebKit和PhantomJS路由将HTML文件转换为PDF文档。要启用PhantomJS路由的转换，请安装下面列出的64位库。 通常，这些库已安装。 如果缺少任何库，请手动安装：

   * linux-gate.so.1
   * libz.so.1
   * libfontconfig.so.1
   * libfreetype.so.6
   * libdl.so.2
   * librt.so.1
   * libpthread.so.0
   * libstdc++.so.6
   * libm.so.6
   * libgcc_s.so.1
   * libc.so.6
   * ld-linux.so.2
   * libexpat.so.1

## 预安装配置 {#preinstallationconfigurations}

安装前配置部分中列出的配置仅适用于PDF生成器服务。 如果未配置PDF生成器服务，则可以跳过安装前配置部分。

### 安装Adobe Acrobat和第三方应用程序 {#install-adobe-acrobat-and-third-party-applications}

如果您要使用PDF生成器服务将本机文件格式(如Microsoft Word、Microsoft Excel、Microsoft PowerPoint、OpenOffice、WordPerfect X7和Adobe Acrobat)转换为PDF文档，请确保这些应用程序已安装在AEM Forms服务器上。

>[!NOTE]
>
>* Adobe Acrobat、Microsoft Word、Excel和Powerpoint仅适用于Microsoft Windows。 如果您使用基于UNIX的操作系统，请安装OpenOffice以将富文本文件和支持的Microsoft Office文件转换为PDF文档。
>* 为配置为使用PDF生成器服务的所有用户安装Adobe Acrobat和第三方软件后显示的所有对话框，请关闭。
>* 至少启动一次所有已安装的软件。 关闭配置为使用PDF生成器服务的所有用户的所有对话框。

>



安装Acrobat后，打开Microsoft Word。 在&#x200B;**Acrobat**&#x200B;选项卡上，单击&#x200B;**创建PDF**，然后将计算机上可用的.doc或.docx文件转换为PDF文档。 如果转换成功，AEM Forms便可将Acrobat与PDF生成器服务结合使用。

### 设置环境变量 {#setup-environment-variables}

为32位和64位Java开发工具包、第三方应用程序和Adobe Acrobat设置环境变量。 环境变量应包含用于启动相应应用程序的可执行文件的绝对路径，例如，下表列出了一些应用程序的环境变量：

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>应用程序</strong></p> </td> 
   <td><p><strong>环境变量</strong></p> </td> 
   <td><p><strong>示例</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>JDK（64位）</strong></p> </td> 
   <td><p>JAVA_HOME</p> </td> 
   <td><p>C:\Program Files\Java\jdk1.8.0_74</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>JDK（32位）</strong></p> </td> 
   <td><p>JAVA_HOME_32</p> </td> 
   <td><p>C:\Program Files (x86)\Java\jdk1.8.0_74</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>Adobe Acrobat</strong></p> </td> 
   <td><p>Acrobat_PATH</p> </td> 
   <td><p>C:\Program Files (x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>记事本</strong></p> </td> 
   <td><p>Notepad_PATH</p> </td> 
   <td><p>C:\WINDOWS\notepad.exe<br /> <strong></strong></p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>OpenOffice</strong></p> </td> 
   <td><p>OpenOffice_PATH</p> </td> 
   <td><p>C:\Program Files (x86)\OpenOffice.org4</p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>* 所有环境变量和相应的路径都区分大小写。
>* JAVA_HOME、JAVA_HOME_32和Acrobat_PATH（仅限Windows）是必需的环境变量。
>* 环境变量OpenOffice_PATH设置为安装文件夹，而不是可执行文件的路径。
>* 请勿为Microsoft Office应用程序（如Word、PowerPoint、Excel和Project）或AutoCAD设置环境变量。 如果这些应用程序安装在服务器上，则“生成PDF”服务会自动启动这些应用程序。
>* 在基于UNIX的平台上，将OpenOffice安装为/root。 如果OpenOffice未作为根安装，则PDF生成器服务无法将OpenOffice文档转换为PDF文档。 如果您需要以非根用户身份安装和运行OpenOffice，请为非根用户提供sudo权限。
>* 如果您在基于UNIX的平台上使用OpenOffice，请运行以下命令以设置路径变量：

>
>  
`export OpenOffice_PATH=/opt/openoffice.org4`

### （仅适用于IBM WebSphere）配置IBM SSL套接字提供程序 {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

执行以下步骤以配置IBM SSL套接字提供程序：

1. 创建java.security文件的副本。 文件的默认位置为`[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`。
1. 打开复制的java.security文件进行编辑。
1. 更改默认的SSL套接字工厂以使用JSSE2工厂，而不是默认的IBM WebSphere工厂：

   **默认内容：**

   ```shell
   #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   #WebSphere socket factories (in cryptosf.jar)
   ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

   **修改的内容：**

   ```shell
   ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   
   #WebSphere socket factories (in cryptosf.jar)
   #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

1. 要启用AEM Forms服务器以使用更新的java.security文件，请在启动AEM Forms服务器时，添加以下java参数：

   `-Djava.security.properties= [path of newly created Java.security file].`

### （仅限Windows）配置Install Ink and Shittring服务 {#configure-install-ink-and-handwriting-service}

如果运行的是Microsoft Windows Server，请配置Ink and Sharting服务。 使用Microsoft Office的链接功能打开Microsoft PowerPoint文件时需要该服务：

1. 打开服务器管理器。 单击快速启动托盘上的&#x200B;**[!UICONTROL 服务器管理器]**&#x200B;图标。
1. 单击&#x200B;**[!UICONTROL 功能]**&#x200B;菜单中的&#x200B;**[!UICONTROL 添加功能]** 。 选中&#x200B;**[!UICONTROL Ink and Sharting Services]**&#x200B;复选框。
1. **[!UICONTROL 选择]** “特征”对话框，并 **[!UICONTROL 选择“墨迹和笔]** 迹服务”。单击&#x200B;**[!UICONTROL Install]**&#x200B;并安装服务。

### （仅限Windows）为Microsoft Office配置文件块设置 {#configure-the-file-block-settings-for-microsoft-office}

更改Microsoft Office信任中心设置，以启用PDF生成器服务来转换使用旧版Microsoft Office创建的文件。

1. 打开Microsoft Office应用程序。 例如，Microsoft Word。 导航到&#x200B;**[!UICONTROL File]**> **[!UICONTROL Options]**。 将出现“选项”对话框。

1. 单击&#x200B;**[!UICONTROL 信任中心]**，然后单击&#x200B;**[!UICONTROL 信任中心设置]**。
1. 在&#x200B;**[!UICONTROL 信任中心设置]**&#x200B;中，单击&#x200B;**[!UICONTROL 文件块设置]**。
1. 在&#x200B;**[!UICONTROL 文件类型]**&#x200B;列表中，取消选择&#x200B;**[!UICONTROL 打开]**&#x200B;以获取应允许PDF生成器服务转换为PDF文档的文件类型。

### （仅限Windows）授予“替换进程级别令牌”权限 {#grant-the-replace-a-process-level-token-privilege}

用于启动应用程序服务器的用户帐户需要&#x200B;**替换进程级别令牌**&#x200B;权限。 默认情况下，本地系统帐户具有&#x200B;**替换进程级别令牌**&#x200B;权限。 对于使用本地管理员组的用户运行的服务器，必须明确授予该权限。 执行以下步骤以授予权限：

1. 打开Microsoft Windows的组策略编辑器。 要打开组策略编辑器，请单击&#x200B;**[!UICONTROL 开始]**，在“开始搜索”框中键入&#x200B;**gpedit.msc**，然后单击&#x200B;**[!UICONTROL 组策略编辑器]**。
1. 导航到&#x200B;**[!UICONTROL 本地计算机策略]** > **[!UICONTROL 计算机配置]** > **[!UICONTROL Windows设置]** > **[!UICONTROL 安全设置]** > **[!UICONTROL 本地策略]** > **[!UICONTROL 用户权限分配]**&#x200B;并编辑&#x200B;**[!UICONTROL 替换进程级别令牌]**，并包括管理员组。
1. 将用户添加到替换进程级别令牌条目。

### （仅限Windows）为非管理员启用PDF生成器服务 {#enable-the-pdf-generator-service-for-non-administrators}

您可以允许非管理员用户使用PDF生成器服务。 通常，只有具有管理权限的用户才能使用该服务：

1. 创建环境变量PDFG_NON_ADMIN_ENABLED。
1. 将环境变量的值设置为TRUE。
1. 重新启动AEM Forms实例。

### （仅限Windows）禁用用户帐户控制(UAC) {#disable-user-account-control-uac}

1. 要访问系统配置实用程序，请转到&#x200B;**[!UICONTROL 开始>运行]**，然后输入&#x200B;**[!UICONTROL MSCONFIG]**。
1. 单击&#x200B;**[!UICONTROL 工具]**&#x200B;选项卡并向下滚动并选择&#x200B;**[!UICONTROL 更改UAC设置]**。 单击&#x200B;**[!UICONTROL Launch]**&#x200B;在新窗口中运行命令。
1. 将滑块调整到“从不通知”级别。 完成后，关闭命令窗口并关闭系统配置窗口。
1. 验证UAC的注册表设置是否设置为0（零）。 执行以下步骤以验证：

   1. Microsoft建议在修改注册表之前先备份该注册表。 有关详细步骤，请参阅[如何在Windows](https://support.microsoft.com/en-us/help/322756)中备份和恢复注册表。
   1. 打开Microsoft Windows Registry编辑器。 要打开注册表编辑器，请转到“开始”>“运行”，键入regedit，然后单击“确定”。
   1. 导航至 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. 确保将EnableLUA的值设置为0（零）。
   1. 确保将&#x200B;**EnableLUA**&#x200B;的值设置为0（零）。 如果值不为0，请将值更改为0。 关闭注册表编辑器。

1. 重新启动计算机。

### （仅限Windows）禁用错误报告服务 {#disable-error-reporting-service}

在Windows Server上使用PDF生成器服务将文档转换为PDF时，Windows Server有时会报告可执行文件遇到问题，需要关闭。 但是，它不会影响PDF转换，因为它会在后台继续显示。

为避免收到错误，您可以禁用Windows错误报告。 有关禁用错误报告的更多信息，请参阅[https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx)。

### （仅限Windows）配置HTML到PDF的转换 {#configure-html-to-pdf-conversion}

PDF生成器服务提供WebKit、WebCapture和PhantomJS路由或方法，以将HTML文件转换为PDF文档。 在Windows上，要为WebKit和Acrobat WebCapture路由启用转换，请将Unicode字体复制到%windir%\fonts目录。

>[!NOTE]
>
>每当将新字体安装到字体文件夹时，请重新启动AEM Forms实例。

### （仅限基于UNIX的平台）用于HTML到PDF转换的额外配置  {#extra-configurations-for-html-to-pdf-conversion}

在基于UNIX的平台上，PDF生成器服务支持WebKit和PhantomJS路由，以将HTML文件转换为PDF文档。 要启用HTML到PDF的转换，请执行适用于您首选的转换路由的以下配置：

### （仅限基于UNIX的平台）启用对Unicode字体的支持（仅限WebKit） {#enable-support-for-unicode-fonts-webkit-only}

根据您的系统，将Unicode字体复制到以下任意目录：

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType(Solaris)

>[!NOTE]
>
>* 在RedHat Enterprise Linux 6.x及更高版本上，信使字体不可用。 要安装Courier字体，请下载font-ibm-type1-1.0.3.zip存档。 在/usr/share/fonts中解压存档。 创建从/usr/share/X11/fonts到/usr/share/fonts的符号链接。
>* 从Html2PdfSvc/bin和/usr/share/fonts目录中删除所有.lst字体缓存文件。
>* 确保目录/usr/lib/X11/fonts和/usr/share/fonts存在。 如果目录不存在，则使用ln命令创建从/usr/share/X11/fonts到/usr/lib/X11/fonts的符号链接，以及从/usr/share/fonts到/usr/share/X11/fonts的其他符号链接。 另外，请确保在/usr/lib/X11/fonts上提供Courier字体。
>* 确保所有字体（Unicode和非Unicode）在/usr/share/fonts或/usr/share/X11/fonts目录中均可用。
>* 当您以非根用户身份运行PDF生成器服务时，请提供对所有字体目录的非根用户读写权限。
>* 每当将新字体安装到字体文件夹时，请重新启动AEM Forms实例。

>



## 安装AEM Forms附加组件包 {#install-aem-forms-add-on-package}

AEM Forms附加组件包是部署在AEM上的应用程序。 该包包含AEM Forms文档服务和其他AEM Forms功能。 请执行以下步骤以安装包：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;部分中：
   1. 从&#x200B;**[!UICONTROL Solution]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Forms]**。
   2. 选择包的版本和类型。 您还可以使用&#x200B;**[!UICONTROL 搜索下载]**&#x200B;选项来筛选结果。
1. 点按适用于您的操作系统的包名称，选择&#x200B;**[!UICONTROL 接受EULA条款]**，然后点按&#x200B;**[!UICONTROL 下载]**。
1. 打开[包管理器](https://docs.adobe.com/content/help/zh-Hans/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 选择包并单击&#x200B;**[!UICONTROL Install]**。

   您还可以通过[AEM Forms版本](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)文章中列出的直接链接下载包。

1. 安装包后，系统会提示您重新启动AEM实例。 **不要立即停止服务器。** 在停止AEM Forms服务器之前，请等待ServiceEvent REGISTERED和ServiceEvent UNEXIGNED消息停止出现在.log `[AEM-Installation-Directory]/crx-quickstart/logs/error`文件中，并且日志稳定。

## 安装后配置 {#post-installation-configurations}

### 为RSA/BouncyCastle库配置引导委派  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. 停止AEM实例。 导航到[AEM安装目录]\crx-quickstart\conf\ folder。 打开sling.properties文件进行编辑。

   如果您使用`[AEM installation directory]\crx-quickstart\bin\start.bat`启动AEM实例，请编辑位于`[AEM_root]\crx-quickstart\`的sling.properties。

1. 将以下属性添加到sling.properties文件：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. （仅限AIX）将以下属性添加到sling.properties文件：

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. 保存并关闭文件。

### 配置字体管理器服务  {#configuring-the-font-manager-service}

1. 以管理员身份登录到[AEM Configuration Manager](http://localhost:4502/system/console/configMgr)。
1. 找到并打开&#x200B;**[!UICONTROL CQ-DAM-Handler-Gibson字体管理器]**&#x200B;服务。 指定System Fonts 、 Customer Server Fonts和Customer Fonts目录的路径。 单击&#x200B;**[!UICONTROL 保存]**。

   >[!NOTE]
   >
   >您使用Adobe以外各方提供的字体的权利受此类各方向您提供的这些字体的许可协议约束，而且您使用Adobe软件的许可不涵盖这些权利。 Adobe建议您在将非Adobe字体与Adobe软件结合使用之前，先查看并确保遵守所有适用的非Adobe许可协议，特别是在服务器环境中使用字体时。
   > 将新字体安装到字体文件夹后，请重新启动AEM Forms实例。

### 配置本地用户帐户以运行PDF生成器服务  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

运行PDF生成器服务需要本地用户帐户。 有关创建本地用户的步骤，请参阅[在Windows中创建用户帐户](https://support.microsoft.com/en-us/help/13951/windows-create-user-account)或[在基于UNIX的平台中创建用户帐户](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/4/html/Step_by_Step_Guide/s1-starting-create-account.html)。

1. 打开[AEM Forms PDF生成器配置](http://localhost:4502/libs/fd/pdfg/config/ui.html)页面。

1. 在&#x200B;**[!UICONTROL 用户帐户]**&#x200B;选项卡中，提供本地用户帐户的凭据，然后单击&#x200B;**[!UICONTROL 提交]**。 如果Microsoft Windows出现提示，则允许访问用户。 成功添加后，配置的用户将显示在&#x200B;**[!UICONTROL 用户帐户]**&#x200B;选项卡的&#x200B;**[!UICONTROL 您的用户帐户]**&#x200B;部分下。

### 配置超时设置 {#configure-the-time-out-settings}

1. 在[AEM配置管理器](http://localhost:4502/system/console/configMgr)中，找到并打开&#x200B;**[!UICONTROL Jacorb ORB提供程序]**&#x200B;服务。

   在&#x200B;**[!UICONTROL Custom Properties.name]**&#x200B;字段中添加以下内容，然后单击&#x200B;**[!UICONTROL Save]**。 它将挂起的回复超时（也称为CORBA客户端超时）设置为600秒。

   `jacorb.connection.client.pending_reply_timeout=600000`

1. 登录到AEM创作实例，然后导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 配置PDF生成器]**。 默认URL为http://localhost:4502/libs/fd/pdfg/config/ui.html。

   打开&#x200B;**[!UICONTROL General Configuration]**&#x200B;选项卡，并修改环境的以下字段值：

<table> 
 <tbody> 
  <tr> 
   <td>字段</td> 
   <td>描述</td> 
   <td>默认值</td> 
  </tr> 
  <tr> 
   <td>服务器转换超时</td> 
   <td>PDFG转换在“服务器转换超时”中定义的秒数内保持活动状态</td> 
   <td>270秒<br /> </td> 
  </tr> 
  <tr> 
   <td>PDFG 清理扫描秒数</td> 
   <td>执行转换后操作所需的秒数。<br /> </td> 
   <td>3600秒</td> 
  </tr> 
  <tr> 
   <td>作业盗取秒数</td> 
   <td>允许PDF生成器服务运行转换的持续时间。 确保作业过期秒数的值大于PDFG清理扫描秒数值。</td> 
   <td>7200秒</td> 
  </tr> 
 </tbody> 
</table>

### （仅限Windows）为PDF生成器服务配置Acrobat {#configure-acrobat-for-the-pdf-generator-service}

在Microsoft Windows上，PDF生成器服务使用Adobe Acrobat将支持的文件格式转换为PDF文档。 执行以下步骤来为PDF生成器服务配置Adobe Acrobat:

1. 打开Acrobat，然后选择&#x200B;**[!UICONTROL 编辑]**> **[!UICONTROL 首选项]**> **[!UICONTROL 更新程序]**。 在检查更新中，取消选择&#x200B;**[!UICONTROL 自动安装更新]**，然后单击&#x200B;**[!UICONTROL 确定]**。 关闭Acrobat。
1. 双击系统上的PDF文档。 当Acrobat首次启动时，将显示登录、欢迎屏幕和EULA对话框。 为配置为使用PDF生成器的所有用户关闭这些对话框。
1. 运行PDF生成器实用程序批处理文件，为PDF生成器服务配置Acrobat:

   1. 打开[AEM包管理器](http://localhost:4502/crx/packmgr/index.jsp)并从包管理器下载`adobe-aemfd-pdfg-common-pkg-[version].zip`文件。
   1. 解压缩下载的.zip文件。 使用管理权限打开命令提示符。
   1. 导航到`[extracted-zip-file]\jcr_root\etc\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\scripts`目录。 运行以下批处理文件：

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat配置为随PDF生成器服务一起运行。

1. 运行系统就绪工具(SRT)以验证Acrobat安装。 该工具检查计算机是否配置正确以运行PDF生成器转换，并在指定路径下生成报告：

   1. 打开命令提示符。 导航到`[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\etc\fd\ pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\srt`文件夹。 在命令提示符下运行以下命令：

      `cscript SystemReadinessTool.vbs [Path_of_reports_folder] en`

      >[!NOTE]
      >
      >如果系统就绪工具报告pdfgen.api文件在acrobat插件文件夹中不可用，请将pdfgen.api文件从`[extracted-adobe-aemfd-pdfg-common-pkg]\plugins\x86_win32`目录复制到`[Acrobat_root]\Acrobat\plug_ins`目录。

   1. 导航至 `[Path_of_reports_folder]`. 打开SystemReadinessTool.html文件。 验证报告并修复上述问题。

### （仅限Windows）配置HTML到PDF转换的主路由 {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

PDF生成器服务提供了多条路由，可将HTML文件转换为PDF文档：Webkit、Acrobat WebCapture（仅限Windows）和PhantomJS。 Adobe建议使用PhantomJS路由，因为它能够处理动态内容，并且不依赖于32位库、32位JDK，或者不需要额外的字体。 此外，PhantomJS路由不需要sudo或root访问权限即可运行转化。

HTML到PDF转换的默认主要路由是Webkit。 要更改转化路线，请执行以下操作：

1. 在AEM创作实例上，导航到&#x200B;**[!UICONTROL 工具]**> **[!UICONTROL Forms]**> **[!UICONTROL 配置PDF生成器]**。

1. 在&#x200B;**[!UICONTROL 常规配置]**&#x200B;选项卡中，从&#x200B;**[!UICONTROL 用于HTML到PDF转换的主路由]**&#x200B;下拉菜单中选择首选转换路由。

### 初始化全局信任存储 {#intialize-global-trust-store}

使用信任存储管理，您可以导入、编辑和删除您信任的服务器上用于验证数字签名和证书身份验证的证书。 您可以导入和导出任意数量的证书。 导入证书后，您可以编辑信任设置和信任存储类型。 执行以下步骤以初始化信任存储：

1. 以管理员身份登录AEM Forms实例。
1. 转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 信任存储]**。
1. 单击&#x200B;**[!UICONTROL 创建TrustStore]**。 设置密码，然后点按&#x200B;**[!UICONTROL Save]**。

### 为Reader扩展和加密服务设置证书 {#set-up-certificates-for-reader-extension-and-encryption-service}

DocAssurance服务可以对PDF文档应用使用权限。 要对PDF文档应用使用权限，请配置证书。

在设置证书之前，请确保您具有：

* 证书文件(.pfx)。

* 随证书提供的私钥密码。

* 私钥别名. 您可以执行Java keytool命令来查看私钥别名：
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* 密钥库文件密码。 如果您使用的是Adobe的Reader扩展证书，则Keystore文件密码始终与私钥密码相同。

请执行以下步骤来配置证书：

1. 以管理员身份登录到AEM创作实例。 转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用户]**。
1. 单击用户帐户的&#x200B;**[!UICONTROL name]**&#x200B;字段。 此时将打开“编辑用户设置”]**页。**[!UICONTROL &#x200B;在AEM创作实例中，证书位于KeyStore中。 如果您之前尚未创建KeyStore，请单击&#x200B;**[!UICONTROL 创建KeyStore]**&#x200B;并为KeyStore设置新密码。 如果服务器已包含KeyStore，请跳过此步骤。  如果您使用的是Adobe的Reader扩展证书，则Keystore文件密码始终与私钥密码相同。
1. 在&#x200B;**[!UICONTROL 编辑用户设置]**&#x200B;页面上，选择&#x200B;**[!UICONTROL KeyStore]**&#x200B;选项卡。 展开&#x200B;**[!UICONTROL 从密钥存储文件添加私钥]**&#x200B;选项并提供别名。 别名用于执行Reader扩展操作。
1. 要上传证书文件，请单击&#x200B;**[!UICONTROL 选择密钥存储文件]**&#x200B;并上传&lt;filename>.pfx文件。

   将与证书关联的&#x200B;**[!UICONTROL 密钥存储密码]**、**[!UICONTROL 私钥密码]**&#x200B;和&#x200B;**[!UICONTROL 私钥别名]**&#x200B;添加到相应的字段。 单击&#x200B;**[!UICONTROL Submit]**。

   >[!NOTE]
   >
   >在生产环境中，将您的评估凭据替换为生产凭据。 在更新过期或评估凭据之前，请确保删除旧的Reader扩展凭据。

1. 单击&#x200B;**[!UICONTROL 编辑用户设置]**&#x200B;页面上的&#x200B;**[!UICONTROL 保存并关闭]**。

### 启用AES-256 {#enable-aes}

要对PDF文件使用AES 256加密，请获取并安装Java加密扩展(JCE)无限强度管辖策略文件。 替换jre/lib/security文件夹中的local_policy.jar和US_export_policy.jar文件。 例如，如果您使用Sun JDK，请将下载的文件复制到`[JAVA_HOME]/jre/lib/security`文件夹中。

汇编程序服务依赖于Reader扩展服务、签名服务、Forms服务和输出服务。 执行以下步骤以验证所需的服务是否已启动且正在运行：

1. 以管理员身份登录到URL `https://'[server]:[port]'/system/console/bundles`。
1. 搜索以下服务并确保服务已启动且正在运行：

<table> 
 <tbody> 
  <tr> 
   <th>服务名称</th> 
   <th>包名称</th> 
  </tr> 
  <tr> 
   <td>签名服务</td> 
   <td>adobe-aemfd-signatures</td> 
  </tr> 
  <tr> 
   <td>Reader 扩展服务</td> 
   <td>com.adobe.aemfd.adobe-aemfd-readerextensions<br /> </td> 
  </tr> 
  <tr> 
   <td>表单服务</td> 
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector<br /> </td> 
  </tr> 
  <tr> 
   <td>输出服务</td> 
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector</td> 
  </tr> 
 </tbody> 
</table>

## 已知问题和疑难解答 {#known-issues-and-troubleshooting}

* 如果压缩的输入文件在文件名中包含双字节字符的HTML文件，则HTML到PDF的转换会失败。 要避免出现此问题，请在命名HTML文件时不要使用双字节字符。

* 在基于UNIX的操作系统上，执行以下操作以查找任何缺少的库：

1. 导航至 `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. 运行以下命令以列出PhantomJS在从HTML转换到PDF时需要的所有库。

   `ldd phantomjs`

   运行以下命令以列出缺少的库。

   `ldd phantomjs | grep not`

1. 手动安装缺少的库。

## 下面的步骤 {#next-steps}

您有一个可用的AEM Forms文档服务环境。 您可以通过以下方式使用文档服务：

* [在OSGi上以表单为中心的工作流](/help/forms/using/aem-forms-workflow.md)
* [观察文件夹](/help/forms/using/watched-folder-in-aem-forms.md)
* [文档服务API](/help/forms/using/aem-document-services-programmatically.md)
