---
title: 设置Visual studio项目并构建Windows应用程序
seo-title: 设置Visual studio项目并构建Windows应用程序
description: 了解如何设置Visual studio项目以构建AEM Forms windows移动设备应用程序。
seo-description: 了解如何设置Visual studio项目以构建AEM Forms windows移动设备应用程序。
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 设置Visual studio项目并构建Windows应用程序{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms提供AEM Forms应用程序的完整源代码。 源包含构建自定义工作区应用程序的所有组件。 源代码存档是 `adobe-lc-mobileworkspace-src-<version>.zip`包共享上包的 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 一部分。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 导航到包共享\
   URL: `https://<server>:<port>/crx/packageshare`.

1. 下载源包。 下载包时，它会添加到AEM Forms包管理器中。
1. 下载完毕后，导航到： `https://<server>:<port>/crx/packmgr/index.jsp`并安装 `adobe-aemfd-forms-app-src-pkg-<version>.zip`。

1. 要下载源代码存档，请在您的浏 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 览器中打开。\
   源包将下载到您的设备上。

下图显示提取的内容 `adobe-lc-mobileworkspace-src-<version>.zip`。

![mws-content-1](assets/mws-content-1.png)

下图显示了文件夹中的文件夹 `windows` 的目录结 `src` 构。

![win-dir](assets/win-dir.png)

## 设置环境 {#setting-up-the-environment}

对于Windows设备，您需要：

* Microsoft Windows 8.1或Windows 10
* Microsoft Visual Studio 2015
* 适用于Apache Cordova的Microsoft Visual Studio工具

## 为AEM Forms应用程序设置Visual studio项目 {#setting-up-visual-studio-project-for-aem-forms-app}

执行以下步骤以在Visual studio中设置AEM Forms应用程序项目。

1. 将存档 `adobe-lc-mobileworkspace-src-<version>.zip` 复制到安 `%HOMEPATH%\Projects` 装并配置了Visual Studio 2015的Windows 8.1或Windows 10设备中的文件夹。
1. 解压缩目录中的存 `%HOMEPATH%\Projects\MobileWorkspace` 档。
1. 导览至目 `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` 录。
1. 使用Visual `CordovaApp.sln` Studio 2015打开文件，然后继续构建AEM Forms应用程序。

## 构建AEM Forms应用程序 {#build-aem-forms-app}

执行以下步骤构建和部署AEM Forms应用程序。

>[!NOTE]
>
>存储在Windows文件系统中的AEM Forms应用程序数据未加密。 建议使用Windows bitLocker Drive Encryption等第三方工具加密磁盘数据。

1. 在Visual Studio标准工具栏中，从构 **建模式的下拉框中** ，选择“释放”。

1. 根据您的平台选择Windows-AnyCPU、Windows-x64或Windows-x86。 建议使用Windows-AnyCPU。
1. 在Visual studio解决方案资源管理器中，右键单击项目 **CordovaApp.Windows** ，然后选择“ **商店”>“创建AppPackages”**。

   ![createapppackages](assets/createapppackages.png)

   此时会显示“创建应用程序包”向导。

   将在platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test目录中创建CordovaApp.Windows_3.0.2.0_anycpu.appx安装程序文件。

   如果遇到错误， `Retarget to windows 8.1 required`请右键单击该错误，并在弹出菜单中，选择“重定 **位到Windows 8.1”**。

   ![重定向解决方案](assets/retarget-solution.png)

1. 在“创建应用程序包”向导中，选择天气条件，或者您不希望将应用程序上传到Windows应用商店，然后单击“下 **一步”**。

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. 根据需要在参数（如应用程序构建的版本和输出位置）中进行更改。

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. 构建项目后，您可以使用以下方式安装应用程序：

   * Windows powerShell
   * Visual Studio
   该包 `.appx` 需要以下项目才能成功安装：

   1. WinJS库
   1. 确保包包含自签名证书或受托机构签名的公共证书（如VeriSign）。
   1. 开发人员许可证
   目录Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test包含其中的四个主要组件：

   1. `.appx` 文件
   1. 证书（目前它是Apache Cordova自签名的证书）
   1. 依赖关系文件夹
   1. PowerShell文件（.ps1扩展名）



## 使用Windows powerShell部署应用程序 {#deploying-an-app-using-windows-powershell}

在Windows设备上安装应用程序有两种方法。

### 通过获取开发人员许可证 {#by-acquiring-the-developer-license}

1. 右键单击PowerShell文件(，然 `Add-AppDevPackage.ps1)`后选择“ **使用PowerShell运行”**。

1. 该设置会提示您获取开发人员许可证。 使用Microsoft帐户凭据获取开发人员许可证。\
   此许可证的有效期为30天，您可以免费续订。
1. 当您获得开发人员许可证时，安装程序会在系统上安装自签名证书并成功安装应用程序。

### 通过使用企业自有设备 {#by-using-enterprise-owned-devices}

对于加入到企业域的企业自有设备，无需获取开发人员许可证。

企业自有设备使用Professional和Enterprise版本的Windows。

Microsoft建议您安装由信任机构颁发的公共证书，如VeriSign。

部署应用程序：

* 确保设备已加入企业的域。
* 启用组策略设置。

**要启用组策略设置，请执行以下操作：**

1. 在您的设备中，运行 `gpedit.msc`。
1. 导航到“计 **算机配置”>“管理模板”>“Windows组件”>“应用程序包部署”**。
1. 右键单击“允许安 **装所有受信任的应用程序”**。
1. 单击“ **编辑** ”，然后选择“ **启用**”。

1. 单击&#x200B;**确定**。

编辑Visual studio生成的PowerShell脚本，以阻止它获取开发人员许可证。

在PowerShell脚本中，设置变量： `$NeedDeveloperLicense = $false`.

对于未加入域的设备，需要侧载产品激活密钥。 您可以从Windows分销商处购买。

对于Windows 8.1主页版本，没有组策略，不允许企业侧加载，您不能将其与企业域连接。 使用开发人员许可证在Windows 8.1 Home edition设备上部署应用程序。

有关详细信息，请单 [击此处](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx)。

## 使用Visual studio部署应用程序 {#deploying-an-app-using-visual-studio}

使用Visual studio在Windows上安装应用程序：

1. 使用远程调试器连接设备。\
   有关详细信息，请参 [阅在远程计算机上运行Windows应用商店应用程序](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine)。

1. 在Visual studio中打开应用程序，从“解决方案平台”列表中选择Windows-x64、Windows-x86或Windows-AnyCPU，然后选择“远程 **计算机”**。
1. 应用程序已部署到远程计算机上。

