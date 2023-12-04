---
title: 设置Visual Studio项目并构建Windows应用程序
seo-title: Set up the Visual Studio project and build the Windows app
description: 了解如何设置Visual Studio项目以构建AEM Forms Windows移动设备应用程序。
seo-description: Learn how to set up a Visual Studio project to build the AEM Forms Windows mobile device app.
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
exl-id: ae7340c8-38cc-4b2b-ba17-22011471fd7d
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 2%

---

# 设置Visual Studio项目并构建Windows应用程序{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms提供了AEM Forms应用程序的完整源代码。 源包含用于构建自定义工作区应用程序的所有组件。 源代码存档， `adobe-lc-mobileworkspace-src-<version>.zip`是 `adobe-aemfd-forms-app-src-pkg-<version>.zip` Software Distribution上的包。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 选择 **[!UICONTROL Adobe Experience Manager]** 在标题菜单中可用。
1. 在 **[!UICONTROL 过滤器]** 部分：
   1. 选择 **[!UICONTROL Forms]** 从 **[!UICONTROL 解决方案]** 下拉列表。
   2. 选择包的版本和类型。 您也可以使用 **[!UICONTROL 搜索下载]** 用于筛选结果的选项。
1. 选择适用于您的操作系统的包名称，然后选择 **[!UICONTROL 接受EULA条款]**，并选择 **[!UICONTROL 下载]**.
1. 打开 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  并单击 **[!UICONTROL 上传包]** 以上传包。
1. 选择包并单击 **[!UICONTROL 安装]**.

1. 要下载源代码存档，请打开 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 在浏览器中。\
   源包将在您的设备上下载。

下图显示了提取的 `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content-1](assets/mws-content-1.png)

下图显示了 `windows` 中的文件夹 `src` 文件夹。

![win-dir](assets/win-dir.png)

## 设置环境 {#setting-up-the-environment}

对于Windows设备，您需要：

* Microsoft Windows 8.1或Windows 10
* Microsoft Visual Studio 2015
* Microsoft Visual Studio Tools for Apache Cordova

## 为AEM Forms应用程序设置Visual Studio项目 {#setting-up-visual-studio-project-for-aem-forms-app}

执行以下步骤，在Visual Studio中设置AEM Forms应用程序项目。

1. 复制 `adobe-lc-mobileworkspace-src-<version>.zip` 存档到 `%HOMEPATH%\Projects` 安装并配置了Visual Studio 2015的Windows 8.1或Windows 10设备中的文件夹。
1. 在中提取存档 `%HOMEPATH%\Projects\MobileWorkspace` 目录。
1. 导航至 `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` 目录。
1. 打开 `CordovaApp.sln` 使用Visual Studio 2015生成文件并继续构建AEM Forms应用程序。

## 构建AEM Forms应用程序 {#build-aem-forms-app}

执行以下步骤来构建和部署AEM Forms应用程序。

>[!NOTE]
>
>存储在AEM Forms应用程序的Windows文件系统中的数据未加密。 建议您使用Windows BitLocker驱动器加密等第三方工具来加密磁盘数据。

1. 在Visual Studio Standard工具栏中，选择 **版本** 构建模式的下拉菜单中。

1. 基于您的平台选择Windows-AnyCPU、Windows-x64或Windows-x86。 建议使用Windows-AnyCPU。
1. 在Visual Studio解决方案资源管理器中，右键单击项目 **CordovaApp.Windows** 并选择 **商店>创建应用程序包**.

   ![createapppackages](assets/createapppackages.png)

   此时会显示“创建应用程序包”向导。

   CordovaApp.Windows_3.0.2.0_anycpu.appx安装程序文件在platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test目录中创建。

   如果您遇到错误 `Retarget to windows 8.1 required`，右键单击错误，然后在弹出菜单中，选择 **重新定位到Windows 8.1**.

   ![重定目标解](assets/retarget-solution.png)

1. 在“创建应用程序包”向导中，选择您是否要将应用程序上传到Windows应用商店，然后单击 **下一个**.

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. 根据需要更改参数，如应用程序内部版本的版本和输出位置。

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. 生成项目后，您可以使用以下代码安装应用程序：

   * Windows PowerShell
   * Visual Studio

   此 `.appx` 包需要以下项目才能成功安装：

   1. WinJS库
   1. 确保该软件包附带自签名证书，或受信任机构签名的公共证书，如VeriSign。
   1. 开发人员许可证

   目录Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test包含四个主要组件：

   1. `.appx` 文件
   1. 证书（当前是Apache Cordova的自签名证书）
   1. 依赖关系文件夹
   1. PowerShell文件（.ps1扩展名）

## 使用Windows PowerShell部署应用程序 {#deploying-an-app-using-windows-powershell}

在Windows设备上安装应用程序有两种方法。

### 通过获取开发人员许可证 {#by-acquiring-the-developer-license}

1. 右键单击PowerShell文件( `Add-AppDevPackage.ps1)`，并选择 **使用PowerShell运行**.

1. 安装程序会提示您获取开发人员许可证。 使用Microsoft帐户凭据获取开发人员许可证。\
   此许可证的有效期为30天，您可以免费续订。
1. 获取开发人员许可证后，安装程序会在系统上安装自签名证书，并且应用程序安装成功。

### 使用企业拥有的设备 {#by-using-enterprise-owned-devices}

对于已加入企业域的企业自有设备，不需要获取开发人员许可证。

企业拥有的设备使用Windows的Professional和Enterprise版本。

Microsoft建议您安装受信任颁发机构颁发的公共证书，如VeriSign。

要部署应用程序，请执行以下操作：

* 确保设备已加入企业的域。
* 启用组策略设置。

**启用组策略设置：**

1. 在您的设备中，运行 `gpedit.msc`.
1. 导航到 **计算机配置>管理模板> Windows组件>应用程序包部署**.
1. 右键单击 **允许安装所有受信任的应用程序**.
1. 单击 **编辑** 并选择 **已启用**.

1. 单击&#x200B;**确定**。

编辑Visual Studio生成的PowerShell脚本以阻止其获取开发人员许可证。

在PowerShell脚本中，设置变量： `$NeedDeveloperLicense = $false`.

对于未加入域的设备，需要侧加载产品激活密钥。 您可以从Windows经销商处购买。

对于Windows 8.1 Home Edition，没有组策略，不允许企业端加载，您无法将其与企业域联接。 使用开发人员许可证在Windows 8.1 Home Edition设备上部署应用程序。

有关详细信息，请单击 [此处](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx).

## 使用Visual Studio部署应用程序 {#deploying-an-app-using-visual-studio}

要使用Visual Studio在Windows上安装应用程序，请执行以下操作：

1. 使用远程调试器连接设备。\
   有关更多信息，请参阅 [在远程计算机上运行Windows应用商店应用](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine).

1. 在Visual Studio中打开应用程序后，从“解决方案平台”列表中选择Windows-x64、Windows-x86或Windows-AnyCPU，然后选择 **远程计算机**.
1. 您的应用程序已部署到远程计算机上。
