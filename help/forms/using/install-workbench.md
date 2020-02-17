---
title: 安装工作台
seo-title: 安装工作台
description: 安装工作台。
uuid: null
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: null
translation-type: tm+mt
source-git-commit: 39ec61c3d6a49be10b50d031e8f747b66901110f

---


# 安装工作台 {#install-workbench}

本文档提供了有关安装和配置AEM Forms Workbench的说明。 安装程序还安装Forms Designer。

## 谁应阅读本文档？ {#who-should-read-this-doc}

本文档适用于负责安装、配置、管理或部署Workbench的管理员或开发人员。 还包括配置系统以支持升级的AEM Forms流程所需的信息。 提供的信息基于以下假设：阅读本文档的任何人都熟悉Microsoft® Windows®操作系统。

## 附加信息 {#additional-information}

此表中的资源可以帮助您进一步了解AEM Forms并开始使用。
<table>
 <tbody>
  <tr>
   <td><p><strong>有关</strong></p> </td>
   <td><p><strong>请参阅</strong></p> </td>
  </tr>
  <tr>
   <td><p>Workbench的过程信息</p> </td>
   <td><p><a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">工作台帮助</a><br /><br /> </p> </td>
  </tr>
  <tr>
   <td><p>有关AEM Forms及其如何与其他Adobe产品集成的一般信息</p> </td>
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65">AEM Forms概述</a><br /><br /> </p> </td>
  </tr>
  <tr>
   <td><p>AEM Forms的所有可用文档</p> </td>
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65">AEM Forms文档</a><br /><br /> </p> </td>
  </tr>
  <tr>
   <td><p>有关此产品版本的修补程序更新、技术说明和其他信息</p> </td>
   <td><p>联系Adobe企业支持</a><br /><br /> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM Forms中已弃用Flex工作空间。 它可用于AEM Forms版本。

## Before You Install {#before-you-install}

### 工作台安装概述 {#workbench-installation-overview}

Workbench是一个集成开发环境(IDE)，开发人员和表单作者使用它创建自动化的业务流程和表单。 它还用于管理流程和表单使用的资源和服务。

下图描述了Workbench安装，包括：
* 使用Workbench进行流程设计
* 使用Designer进行表单设计

>[!NOTE]
>
>AEM Forms服务器需要单独的安装程序。 有关详细信息，请参阅JEE上的AEM Forms安装文档。

![default-render-form](assets/installing-workbench.png)

## 系统先决条件 {#system-prerequisites}

本节概述了硬件和软件要求以及支持的平台。

### 最低硬件和软件要求 {#minimum-hardware-software-requirements}

**工作**&#x200B;台建议以下要求作为最低要求：安装的磁盘空间：
* 680 MB，仅限Workbench。
* 在单个驱动器上安装2.15 GB，可完整安装Workbench、Designer和样本组件。
* 400 MB用于临时安装目录——用户\temp目录为200 MB,Windows临时目录为200 MB。

>[!NOTE]
>
>如果所有这些位置都位于单个驱动器上，则安装过程中必须有1.5 GB的可用空间。 安装完成后，将删除复制到临时目录的文件。

* 硬件要求：Intel® Pentium® 4或AMD等效处理器，1 GHz处理器。
* Java™ Runtime Environment(JRE)7.0将51或更高版本更新至7.0。
* 最低1024 X 768像素或更高的显示器分辨率，16位颜色或更高。
* 与AEM Forms服务器的TCP/IPv4或TCP/IPv6网络连接。
* 安装Visual C++ 2012 32位可再分发运行时包。
* 安装Visual C++ 2013 32位可再分发运行时包。

>[!NOTE]
>
>您必须具有“管理”权限才能安装Workbench。 如果您使用非管理员帐户进行安装，安装程序将提示您输入相应帐户的凭据。

### 支持的平台 {#supported-platforms}

请参阅 [AEM Forms Supported Platforms中Workbench支持的平台的完整列表](http://adobe.com/go/learn_aemforms_supportedplatforms_65)。

## 设计人员安装注意事项 {#designer-installation-considerations}

默认情况下，Workbench安装包含相应的仅英文版Designer。 如果Workbench安装应用程序在您的计算机上检测到Designer的现有版本，则安装可能会终止，并且您必须先删除Designer的当前版本，然后才能继续。
下表列出了您在安装Workbench时可能遇到的Designer安装方案，以及您必须执行的任何操作。

<table>
 <tbody>
  <tr>
   <td><p><strong>当前安装的Designer版本</strong></p> </td>
   <td><p><strong>必需操作</strong></p> </td>
  </tr>
  <tr>
   <td><p>Acrobat pro或Acrobat Pro Extended（包括Designer）</p> </td>
   <td><p>无.<br /> 
Workbench安装会在您的计算机上检测到随Acrobat pro或Acrobat Pro Extended一起安装的Designer实例。<br />
不同版本的Designer可以共存于同一系统上，例如Designer 6.4.x(Workbench 6.4)和Designer 6.5.0.x(Workbench 6.5)。无需卸载随Acrobat 10 pro或Acrobat 10 Pro Extended或更高版本一起安装的Designer版本。
<br /></p> </td>
  </tr>
  <tr>
   <td><p>设计人员（独立）</p> </td>
   <td><p>无. <br />Workbench附带的Designer版本仅提供英文版。 <br />Workbench安装程序不会重新安装新版本的Designer。 将修补与Workbench安装程序绑定的更新版本。 这还允许您在Workbench中使用Designer的本地化版本。<br /> </p> </td>
  </tr>
 </tbody>
</table>

### 在Windows 10上卸载Designer（独立） {#uninstall-designer-standalone-windows10}

1. 转到“控 **制面板”>“程序”>“程序和功能”**
1. 在“当前安装的程序”列表中，选择“ **Adobe Designer**”。
1. 单击“ **卸载** ”，然后单 **击“是”**。

## 安装Workbench {#installing-workbench}

本章介绍如何安装Workbench。

### 安装和运行Workbench {#installing-and-running-workbench}

在安装Workbench之前，必须确保您的环境包含运行该环境所需的软件和硬件(请参阅部分： **安装前**)。

**要安装和运行Workbench，请执行以下操作：**

1. 执行下列任务之一：
   * 导览至安装介质上的\workbench目录，然后双击run_windows_installer.bat文件。
   * 将Workbench下载并解压缩到文件系统。 下载完该文件后，导航到\workbench目录并双击run_windows_installer.bat文件。
   >[!IMPORTANT]
   >
   >Workbench安装程序仅从本地驱动器运行。 它不能从远程站点运行。

   >[!NOTE]
   >
   >如果遇到错误“无法创建Java虚拟机”，请创建一个名为_JAVA_OPTIONS的环境变量（值为-Xmx512M）并运行安装程序。

1. 在“简介”屏幕上，单击“下一步”。
1. 阅读产品许可协议，选择“我接受许可协议的条款”，然后单击“下一步”。
1. （可选）如果需要此工具创建和修改表单，请选择“安装Adobe Designer”。

   >[!NOTE]
   >
   >通过取消选择此选项，您可以继续使用随Acrobat 10一起安装的Designer。

1. 接受列出的默认目录，或单击选择并导航到要安装Workbench的目录，然后单击下一步。

   >[!NOTE]
   >
   >安装目录路径不应包含#（井号）和$（美元）字符。

1. 查看预安装摘要，然后单击“安装”。 安装程序显示安装进度。
1. 查看安装摘要。 选择启动AEM Forms Workbench以启动Workbench，然后单击下一步。
1. 查看发行说明，然后单击完成。
1. 您的计算机上现在安装了以下项目：
   * **工作台**:要从“开始”菜单运行Workbench，请选择“所有程序”>“AEM表单”>“工作台”，前提是您选择将快捷方式文件夹存储在此处。 有关信息，请参阅使 <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">用Workbench文档</a> 。
   * **设计人员**:您可以从Workbench中访问Designer。 有关信息，请参阅设计人员帮助中的 <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf">入门主题</a>。
   * **AEM Forms SDK**:有关使用SDK的详细信息，请参阅 <a href="http://www.adobe.com/go/learn_aemforms_programming_65">使用AEM Forms编程</a>。

## 升级进程 {#upgrading-processes}

JEE进程上的AEM Forms可使用升级向导升级到AEM Forms应用程序。 有关详细信息，请参阅Workbench帮助中的升级旧版对象文档。

### 配置和登录服务器 {#configuring-and-logging-server}

要使用Workbench，您必须运行AEM Forms实例，通常在单独的计算机上。 您必须具有用户名和密码才能登录AEM Forms，以及有关服务器位置的详细信息。

>[!NOTE]
>
>如果您将AEM Forms配置为使用EMC Documentum或IBM FileNet存储库提供程序，并且您希望登录到除在AEM Forms管理控制台中配置为默认存储库之外的存储库，请将用户名提供为username@Repository。

### 配置超时设置 {#configuring-timeout-settings}

默认情况下，无论活动或不活动，Workbench都会在两小时后超时。 要编辑超时设置，请参阅管理控制台帮助中的“配置用户管理>配置高级系 <a href="https://docs.adobe.com/content/help/en/experience-manager-65/forms/administrator-help/configure-user-management/configure-advanced-system-attributes.html">统属性”</a>。

### 配置Workbench以通过HTTPS连接 {#configuring-workbench-to-connect-over-HTTPS}

要通过HTTPS将Workbench连接到AEM Forms服务器，您必须确保颁发公共密钥的证书颁发机构(CA)被Workbench识别为受信任。 如果未将证书识别为来自受信任的源，则必须更新位于 [Workbench_HOME]/workbench/jre/lib/security目录中的cacert文件。

>[!NOTE]
>
>[Workbench_HOME] 表示安装Workbench的目录。 默认位置为C:\Program Files (x86)\Adobe Experience Manager Forms Workbench。

确保使用证书中指定的名称连接到HTTPS。 此名称通常是完全限定的主机名。

**要更新cacert文件，请执行以下操作**:
1. 确保您有安全套接字层(SSL)证书的副本。 请与配置SSL服务器的管理员联系，或使用Web浏览器导出证书。

   >[!NOTE]
   >
   >要导出证书，请打开Web浏览器并登录到管理控制台，在浏览器中安装证书，然后将证书从浏览器导出到临时存储位置(或直接导出到 [Workbench_HOME]/workbench/jre/lib/security目录)。

1. 将证书复制到 [Workbench_HOME]/workbench/jre/lib/security目录。

1. 打开命令提示窗口，导航至 [Workbench_HOME]/workbench/jre/bin，然后键入以下命令：
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`
其中：
   * changeit是cacerts密钥库的默认密码。
   * certname是您在步骤1中选择的证书。
   * 示例是您为证书选择的别名。 可以更改此值

1. 当系统提示您信任证书时，键入“是”并点击“输入”键。 keytool继续将cacerts文件导入 [Workbench_HOME]/workbench/jre/lib/security目录。

1. 关闭并重新启动Workbench以应用更改。

### 为动态生成的模板配置缓存设置 {#configuring-cache-settings-for-dynamically-generated-templates}

如果应用程序通过自动更新XFA内容来动态生成唯一模板，则应考虑缓存操作的以下方面。 实际上，每个事务都使用一个新的唯一模板。

当表单生成器或输出在缓存中搜索或更新特定表单模板的条目时，它会使用多个键值来查找要访问的特定缓存条目。

* **模板文件名**:用作缓存表单的主要唯一标识符的模板的位置和文件名。
* **时间戳**:模板文件包含用于确定表单的上次更新时间的时间戳。
* **模板UUID**:设计人员在每个模板中为表单及其版本插入一个唯一标识符(UUID)。 每次更新表单时，都会更新嵌入的UUID。 例如，XDP模板可能显示以下内容：

   `<?xml version="1.0" encoding="UTF-8"?>`
   `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=http://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="http://www.xfa.org/schema/xfa-template/2.6/">`

* **渲染选项**:在渲染的表单高速缓存中，高速缓存内容分别存储为每组唯一的渲染选项。


Forms服务通过引用文件名或存储库位置或作为内存中的XML对象的值来接收模板。
* **通过引用传递的模板**:使用内容根目录和表单名称。 如果使用此方法在每个请求中都传递了具有不同文件名的唯一模板，则磁盘缓存将不断增长，并且永远不会重复使用。 为防止出现这种情况，应使用相同的文件名传递唯一模板，以确保所有请求都更新相同的缓存。
* **按值传递的模板**:使用使用theinDataDoc参数随数据一起传递的模板字节。 如果使用此方法传递具有不同UUID的唯一模板，则磁盘缓存将无休止地增长，并且永远不会重复使用。 为防止出现这种情况，应从所有模板中去除UUID属性，以确保不为模板创建缓存。 或者，传递相同的非空UUID允许创建缓存对象，但确保使用每个请求更新相同的缓存。

要防止缓存无休止地增长，请考虑以下因素，以使用新的AEM Forms API渲染动态生成的模板（即renderHTMLForm2和renderPDFForm2）。

使用新API时，模板将作为文档对象进行传递，文档对象在Forms服务中处理时基于是否被钝化。

对于UUID和内容根用作缓存键的钝化文档，请考虑以下方面：
* 不为没有UUID的钝化输入模板创建缓存。
* 如果传递了多个具有相同UUID和内容根目录的钝化输入模板，则覆盖相同的缓存。

对于以文件名和内容根目录作为缓存密钥的未钝化文档，请考虑以下方面：
* 对于未钝化的输入模板，缓存取决于生成文档的内容根目录和文件名。
同一缓存将仅用于内容根目录和模板文件名相同的请求。
以下最佳实践将确保在将动态生成的模板传递给Forms服务时缓存不会无限增长：
   * 删除UUID或在所有动态生成的模板中传递相同的UUID。
   * 从模板字节或磁盘上相同的文件名生成文档。

### 卸载Workbench {#uninstalling-workbench}

使用控制面板中的“添加或删除程序”功能启动卸载程序。 Workbench和Designer应用程序有单独的卸载程序。

## 配置AEM Forms XDC编辑器 {#configuring-aem-forms-xdc-editor}

使用XDC编辑器，网络打印机管理员可以创建和修改XML Forms架构设备配置(XDC)文件。 XDC文件描述了打印机的功能，如打印机语言或纸张大小与纸盒位置之间的关联。

在网络打印机管理员使用XDC编辑器之前，请重新定位示例XDC文件，并参阅使用XDC编辑器创建设备配置文件。

**要获取示例XDC文件**:
1. 在AEM Forms服务器上，找到 [AEM Forms根目录\sdk\samples\Output\IVS中的XDC文]件夹。
1. 将此文件夹的内容复制到可从Workbench或Eclipse系统访问的目录中。

**要获取XDC编辑器帮助**:
1. 转到AEM Forms文档网站。
1. 单击“开 **发** ”选项卡，然后导航到使用XDC编辑器创建设备配置文件。 下载xdc_editor_help_web.zip文件，并按照自述文件中提供的说明安装帮助文件。

