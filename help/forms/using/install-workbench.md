---
title: 安装工作台
seo-title: Install workbench
description: 安装工作台。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
role: Admin
exl-id: d530dbb9-f95e-4329-9665-37faf8f7931b
source-git-commit: 18cfefb794382b5314b18a62645f1fba28d314a2
workflow-type: tm+mt
source-wordcount: '2232'
ht-degree: 0%

---

# 安装Workbench {#install-workbench}

本文档提供有关安装和配置AEM Forms Workbench的说明。 安装程序还会安装Forms Designer。

## 谁应该阅读本文档？ {#who-should-read-this-doc}

本文档面向负责安装、配置、管理或部署Workbench的管理员或开发人员。 此外，还包含配置系统以支持升级后的AEM Forms流程的信息。 所提供的信息基于以下假设：阅读本文档的任何人都熟悉Microsoft® Windows®操作系统。

## 附加信息 {#additional-information}

此表中的资源可以帮助您详细了解AEM Forms并开始使用。
<table>
 <tbody>
  <tr>
   <td><p><strong>有关信息</strong></p> </td>
   <td><p><strong>请参阅</strong></p> </td>
  </tr>
  <tr>
   <td><p>Workbench的程序信息</p> </td>
   <td><p><a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Workbench帮助</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>有关AEM Forms及其如何与其他Adobe产品集成的一般信息</p> </td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/getting-started/introduction-aem-forms.html?lang=en">AEM Forms概述</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>AEM Forms的所有可用文档</p> </td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/getting-started/introduction-aem-forms.html?lang=en">AEM Forms文档</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>有关此产品版本的修补程序更新、技术说明和其他信息</p> </td>
   <td><p>联系Adobe企业支持</a><br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Flex工作区已被AEM Forms弃用。 它适用于AEM Forms版本。

## 安装之前 {#before-you-install}

### Workbench安装概述 {#workbench-installation-overview}

Workbench是一个集成开发环境(IDE)，开发人员和表单作者可使用它来创建自动化的业务流程和表单。 它还用于管理流程和表单使用的资源和服务。

下图描述了Workbench的安装，其中包括：
* 使用Workbench进行流程设计
* 使用Designer进行表单设计

>[!NOTE]
>
>AEM Forms Server需要单独的安装程序。 有关更多信息，请参阅AEM Forms on JEE安装文档。

![default-render-form](assets/installing-workbench.png)

## 系统先决条件 {#system-prerequisites}

本节概述了硬件和软件要求以及支持的平台。

### 最低硬件和软件要求 {#minimum-hardware-software-requirements}

**Workbench**
建议满足以下最低要求：安装所需的磁盘空间：
* 仅680 MB用于Workbench。
* 2.15 GB的容量，用于完整安装Workbench、设计人员和示例组件。
* 临时安装目录为400 MB — 用户\temp目录为200 MB，Windows临时目录为200 MB。

>[!NOTE]
>
>如果所有这些位置都驻留在单个驱动器上，则安装期间必须有1.5 GB的可用空间。 安装完成后，将删除复制到临时目录的文件。

* 硬件要求：英特尔®奔腾® 4或等效的AMD® 1 GHz处理器。
* Java™ Runtime Environment (JRE) 7.0将51或更高版本更新为7.0。
* 最低为1024 X 768像素或更高的显示器分辨率（使用16位颜色或更高）。
* 到AEM Forms服务器的TCP/IPv4或TCP/IPv6网络连接。
* 安装Visual C++可再发行运行时包2012 32位。
* 安装Visual C++可再发行运行时包2013 32位。

>[!NOTE]
>
>您必须具有管理权限才能安装Workbench。 如果您使用非管理员帐户进行安装，安装程序会提示您输入相应帐户的凭据。

### 支持的平台 {#supported-platforms}

请参阅Workbench支持的平台的完整列表，网址为 [AEM Forms支持的平台](https://www.adobe.com/go/learn_aemforms_supportedplatforms_65).

## Designer安装注意事项 {#designer-installation-considerations}

默认情况下，Workbench安装包含相应的纯英语版设计器。 如果Workbench安装应用程序检测到计算机上存在设计器版本，安装可能会终止，并且您需要先删除当前版本的设计器，然后才能继续。
下表包含您在安装Workbench时可能遇到的设计器安装场景以及必须执行的任何操作的完整列表。

<table>
 <tbody>
  <tr>
   <td><p><strong>当前已安装的设计器版本</strong></p> </td>
   <td><p><strong>必需操作</strong></p> </td>
  </tr>
  <tr>
   <td><p>Acrobat Pro或Acrobat Pro Extended（包括设计器）</p> </td>
   <td><p>无。<br /> 
Workbench安装会检测计算机上随Acrobat Pro或Acrobat Pro Extended一起安装的Designer实例。<br />
不同版本的Designer可以共存于同一系统中，例如，适用于Workbench 6.4的Designer 6.4.x和适用于Workbench 6.5的Designer 6.5.0.x。无需卸载与Acrobat 10 Pro或Acrobat 10 Pro Extended或更高版本一起安装的Designer版本。
<br /></p> </td>
  </tr>
  <tr>
   <td><p>Designer（独立）</p> </td>
   <td><p>无。<br />Workbench中包含的Designer版本仅限英语。 <br />Workbench安装程序不会重新安装新版本的Designer。 而是将修补与Workbench安装程序捆绑在一起的更新版本。 这还允许您在Workbench中使用本地化版本的Designer。<br /> </p> </td>
  </tr>
 </tbody>
</table>

### 在Windows 10上卸载Designer （独立） {#uninstall-designer-standalone-windows10}

1. 转到 **控制面板>程序>程序和功能**
1. 在当前安装的程序列表中，选择 **Adobe设计器**.
1. 单击 **卸载** 然后单击 **是**.

## 安装Workbench {#installing-workbench}

本章介绍如何安装Workbench。

### 安装和运行Workbench {#installing-and-running-workbench}

在安装Workbench之前，必须确保您的环境包含运行它所需的软件和硬件(请参阅以下部分： **安装之前**)。

**要安装和运行Workbench，请执行以下操作：**

1. 执行以下任务之一：
   * 导航到安装介质上的\workbench目录，并双击run_windows_installer.bat文件。
   * 将Workbench下载并解压缩到您的文件系统。 下载后，导航到\workbench目录并双击run_windows_installer.bat文件。

   >[!IMPORTANT]
   >
   >Workbench安装程序只能从本地驱动器运行。 无法从远程站点运行它。

   >[!NOTE]
   >
   >如果遇到错误“无法创建Java™虚拟机”，请创建一个名为_JAVA_investigations的环境OPTIONS（值为 — Xmx512M），然后运行安装程序。

1. 在“Introduction（简介）”屏幕上，单击“Next（下一步）”。
1. 阅读产品许可协议，选择“I accept the terms of the License Agreement（我接受许可协议的条款）” ，然后单击“Next（下一步）”。
1. （可选）如果需要此工具创建和修改表单，请选择安装Adobe设计器。

   >[!NOTE]
   通过取消选中此选项，您可以继续使用随Acrobat 10一起安装的Designer。

1. 接受列出的默认目录，或单击“选择”并导航到要安装Workbench的目录，然后单击“下一步”。

   >[!NOTE]
   安装目录路径不应包含# （井号）和$ （美元）字符。

1. 查看预安装摘要，然后单击安装。 安装程序显示安装进度。
1. 查看安装摘要。 选择“启动AEM Forms Workbench”以启动Workbench，然后单击“下一步”。
1. 查看发行说明，然后单击完成。
1. 您的计算机上现在安装了以下项目：
   * **Workbench**：要从“开始”菜单中运行Workbench，请选择所有程序> AEM Forms > Workbench（如果您选择将快捷文件夹存储在该处）。 欲了解相关信息，请参见 <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">使用Workbench</a> 文档。
   * **设计器**：您可以从Workbench内部访问设计器。 有关信息，请参阅中的快速入门主题 <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf">Designer帮助</a>.
   * **AEM FORMS SDK**：有关使用SDK的更多信息，请参阅 <a href="https://helpx.adobe.com/pdf/aem-forms/6-3/programming-with-aem-forms.pdf">使用AEM Forms编程</a>.

## 升级流程 {#upgrading-processes}

可以使用升级向导将AEM Forms on JEE进程升级到AEM Forms应用程序。 有关详细信息，请参阅Workbench帮助中的升级旧版工件文档。

### 配置和登录到服务器 {#configuring-and-logging-server}

要使用Workbench，您必须运行一个AEM Forms实例，通常是在单独的计算机上。 您必须具有用户名和密码才能登录到AEM Forms，并且了解有关服务器位置的详细信息。

>[!NOTE]
如果您已将AEM Forms配置为使用EMC Documentum®或IBM® FileNet存储库提供程序，并且希望登录到其他存储库(而不是在AEM Forms管理控制台中配置为默认的存储库)，请以username@Repository的形式提供用户名。

### 配置超时设置 {#configuring-timeout-settings}

默认情况下，Workbench会在两小时后超时，无论活动还是非活动。 要编辑超时设置，请参阅 <a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/configure-user-management/configure-advanced-system-attributes.html">管理控制台帮助</a>.

### 配置Workbench以通过HTTPS连接 {#configuring-workbench-to-connect-over-HTTPS}

要通过HTTPS将Workbench连接到AEM Forms服务器，您必须确保将颁发公钥的证书颁发机构(CA)识别为Workbench受信任。 如果无法识别证书来自受信任的来源，则必须更新 [Workbench_HOME]/workbench/jre/lib/security目录。

>[!NOTE]
[Workbench_HOME] 表示安装Workbench的目录。 默认位置为C:\Program Files (x86)\Adobe Experience Manager Forms Workbench。

确保使用证书中指定的名称连接到HTTPS。 此名称通常是完全限定的主机名。

**更新cacert文件**：
1. 确保您有安全套接字层(SSL)证书的副本。 请与配置SSL服务器的管理员联系，或使用Web浏览器导出证书。

   >[!NOTE]
   要导出证书，请打开Web浏览器并登录到管理控制台，在浏览器中安装证书，然后将证书从浏览器导出到临时存储位置(或直接导出到 [Workbench_HOME]/workbench/jre/lib/security directory)。

1. 将证书复制到 [Workbench_HOME]/workbench/jre/lib/security目录。

1. 打开命令提示符窗口，导航至 [Workbench_HOME]/workbench/jre/bin，然后键入以下命令：
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`其中：
   * `changeit` 是cacerts密钥库的默认密码。
   * certname是您在步骤1中选择的证书。
   * 示例是您为证书选择的别名。 此值可以更改。

1. 当提示信任证书时，键入Yes并按Enter键。 keytool继续将cacerts文件导入 [Workbench_HOME]/workbench/jre/lib/security目录。

1. 关闭并重新启动Workbench以应用更改。

### 为动态生成的模板配置缓存设置 {#configuring-cache-settings-for-dynamically-generated-templates}

如果您的应用程序通过自动更新XFA内容来动态生成唯一模板，则应考虑缓存操作的以下方面。 实际上，每个交易都使用新的唯一模板。

当表单生成器或输出在缓存中搜索或更新特定表单模板的项目时，它会使用多个键值来查找将访问的特定缓存项目。

* **模板文件名**：用作缓存表单的主要唯一标识符的模板的位置和文件名。
* **时间戳**：模板文件包含一个时间戳，用于确定表单的上次更新时间。
* **模板UUID**：Designer会在每个模板中为表单及其版本插入一个唯一标识符(UUID)。 每次更新表单时，都会更新嵌入的UUID。 例如，XDP模板可能显示以下内容：

   `<?xml version="1.0" encoding="UTF-8"?>`
   `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=https://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="https://www.xfa.org/schema/xfa-template/2.6/">`

* **渲染选项**：在渲染的表单缓存中，缓存内容将针对每组唯一渲染选项单独存储。


Forms服务通过引用文件名或存储库位置，或者通过值接收模板，该值作为内存中的XML对象。
* **通过引用传递的模板**：使用内容根和表单名称。 如果使用此方法在每个请求中传递了具有不同文件名的唯一模板，则磁盘缓存会无限增长，永远不会被重复使用。 为防止出现这种情况，应使用相同的文件名传递唯一的模板，以确保为所有请求更新相同的缓存。
* **按值传递的模板**：使用通过inDataDoc参数与数据一起传递的模板字节。 如果使用此方法传递具有不同UUID的唯一模板，则磁盘缓存会无限增长，并且永远不会被重复使用。 要防止出现这种情况，应从所有模板中剥除UUID属性，以确保不为该模板创建缓存。 或者，传递相同的非null UUID可以创建缓存对象，但可以确保使用每个请求更新相同缓存。

为了防止缓存无限增长，请考虑以下因素，以便使用新的AEM Forms API渲染动态生成的模板，即renderHTMLForm2和renderPDFForm2。

使用新API时，模板作为文档对象传递，在Forms服务中根据其是否被钝化进行处理。

对于将UUID和内容根用作缓存键的钝化文档，请考虑以下方面：
* 缓存不是为没有UUID的钝化输入模板创建的。
* 如果传递了多个具有相同UUID和内容根的钝化输入模板，则会覆盖相同的缓存。

对于文件名和内容根目录用作缓存键的非钝化文档，请考虑以下方面：
* 对于非钝化输入模板，缓存取决于生成文档的内容根目录和文件名。
只有内容根和模板文件名相同的请求才会使用相同的缓存。
以下最佳实践可确保将动态生成的模板传递到Forms服务时，缓存不会无限增加：
   * 在所有动态生成的模板中剥离UUID或传递相同的UUID。
   * 通过模板字节或磁盘上的相同文件名生成文档。

### 卸载Workbench {#uninstalling-workbench}

使用控制面板中的“Add or Remove Programs（添加或删除程序）”功能启动卸载程序。 Workbench和Designer应用程序具有单独的卸载程序。

## 配置AEM Forms XDC编辑器 {#configuring-aem-forms-xdc-editor}

使用XDC编辑器，网络打印机管理员可以创建并修改XML Forms体系结构设备配置(XDC)文件。 XDC文件描述打印机的功能，如打印机语言或纸张大小与纸盒位置之间的相关性。

在网络打印机管理员使用XDC编辑器之前，请重新定位示例XDC文件，并参阅使用XDC编辑器创建设备配置文件。

**获取示例XDC文件**：
1. 在AEM Forms服务器上，找到XDC文件夹，位于 [AEM Forms根目录]\sdk\samples\Output\IVS.
1. 将此文件夹的内容复制到可从Workbench或Eclipse系统访问的目录中。

**获取XDC编辑器帮助**：
1. 转到AEM Forms文档网站。
1. 单击 **开发** 选项卡并导航到使用XDC编辑器创建设备配置文件。 按照自述文件中提供的说明下载xdc_editor_help_web.zip文件并安装帮助文件。
