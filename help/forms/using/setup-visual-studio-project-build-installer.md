---
title: 设置Visual Studio项目并构建Windows应用程序
seo-title: 设置Visual Studio项目并构建Windows应用程序
description: 了解如何设置Visual Studio项目以构建AEM FormsWindows移动设备应用程序。
seo-description: 了解如何设置Visual Studio项目以构建AEM FormsWindows移动设备应用程序。
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---


# 设置Visual Studio项目并构建Windows应用程序{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms提供AEM Forms应用程序的完整源代码。 该源包含构建自定义工作区应用程序的所有组件。 源代码存档是 `adobe-lc-mobileworkspace-src-<version>.zip`软件分发软件包 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 的一部分。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 开放 [软件分发](https://experience.adobe.com/downloads)。 您需要Adobe ID登录软件分发。
1. 点按 **[!UICONTROL 标题]** 菜单中可用的Adobe Experience Manager。
1. 在过滤器 **[!UICONTROL 部分]** :
   1. 从“ **[!UICONTROL 解决方]** 案 **[!UICONTROL ”下]** 拉列表中选择“表单”。
   2. 选择包的版本和类型。 您还可以使用“搜 **[!UICONTROL 索下载]** ”选项筛选结果。
1. 点按适用于您的操作系统的包名称，选择“ **[!UICONTROL 接受EULA条款]**”，然后点 **[!UICONTROL 按下载]**。
1. 打开 [包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) ，然后单 **[!UICONTROL 击“上传包]** ”以上传包。
1. Select the package and click **[!UICONTROL Install]**.

1. 要下载源代码存档，请在浏 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 览器中打开。\
   源包将下载到您的设备上。

下图显示提取的内容 `adobe-lc-mobileworkspace-src-<version>.zip`。

![mws-content-1](assets/mws-content-1.png)

下图显示了文件夹中文件 `windows` 夹的目录 `src` 结构。

![win-dir](assets/win-dir.png)

## 设置环境 {#setting-up-the-environment}

对于Windows设备，您需要：

* Microsoft Windows 8.1或Windows 10
* Microsoft Visual Studio 2015
* 适用于Apache Cordova的Microsoft Visual Studio工具

## 为AEM Forms应用程序设置Visual Studio项目 {#setting-up-visual-studio-project-for-aem-forms-app}

执行以下步骤以在Visual Studio中设置AEM Forms应用程序项目。

1. 将存 `adobe-lc-mobileworkspace-src-<version>.zip` 档复制 `%HOMEPATH%\Projects` 到安装并配置了Visual Studio 2015的Windows 8.1或Windows 10设备中的文件夹。
1. 解压目录中的存 `%HOMEPATH%\Projects\MobileWorkspace` 档。
1. 导航到目 `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` 录。
1. 使用Visual `CordovaApp.sln` Studio 2015打开文件，然后继续构建AEM Forms应用程序。

## 构建AEM Forms应用程序 {#build-aem-forms-app}

请执行以下步骤以构建和部署AEM Forms应用程序。

>[!NOTE]
>
>存储在Windows文件系统中的AEM Forms应用程序数据未加密。 建议使用Windows BitLocker驱动器加密等第三方工具加密磁盘数据。

1. 在Visual Studio标准工具栏中，从 **构建模** 式的下拉菜单中选择“释放”。

1. 根据您的平台选择Windows-AnyCPU、Windows-x64或Windows-x86。 建议使用Windows-AnyCPU。
1. 在Visual Studio解决方案资源管理器中，右键单击项目CordovaApp. **Windows** ，然后选择 **“商店”>“创建AppPackages**”。

   ![createapppackages](assets/createapppackages.png)

   此时会显示“创建应用程序包”向导。

   将在platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test目录中创建CordovaApp.Windows_3.0.2.0_anycpu.appx安装程序文件。

   如果遇到错 `Retarget to windows 8.1 required`误，请右键单击该错误，并在弹出菜单中选择“重 **新定位到Windows 8.1”**。

   ![重定位解决方案](assets/retarget-solution.png)

1. 在“创建应用程序包”向导中，选择天气或您不希望将应用程序上传到windows应用商店，然后单击“下 **一步”**。

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. 根据需要更改参数，如应用程序构建的版本和输出位置。

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. 构建项目后，您可以使用以下方式安装应用程序：

   * Windows PowerShell
   * Visual Studio

   该包 `.appx` 需要以下项目才能成功安装：

   1. WinJS库
   1. 确保软件包随附自签名证书或受信任颁发机构签名的公共证书（如VeriSign）。
   1. 开发人员许可证

   目录Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test包含其中的四个主要组件：

   1. `.appx` 文件
   1. 证书（目前它是Apache Cordova自签名的证书）
   1. 依赖关系文件夹
   1. PowerShell文件（.ps1扩展名）



## 使用Windows PowerShell部署应用程序 {#deploying-an-app-using-windows-powershell}

在Windows设备上安装应用程序有两种方法。

### 通过获取开发人员许可证 {#by-acquiring-the-developer-license}

1. 右键单击PowerShell文件(，然 `Add-AppDevPackage.ps1)`后选择“ **使用PowerShell运行”**。

1. 安装程序会提示您获取开发人员许可证。 使用Microsoft帐户凭据获取开发人员许可证。\
   此许可证的有效期为30天，您可以免费续订。
1. 当您获得开发人员许可证时，安装程序会在系统上安装自签名证书，并且应用程序会成功安装。

### 通过使用企业自有设备 {#by-using-enterprise-owned-devices}

对于加入企业域的企业自有设备，无需获得开发人员许可证。

企业自有设备使用Professional和Enterprise版本的Windows。

Microsoft建议您安装一个颁发公共证书（如VeriSign）的受信任颁发机构。

部署应用程序：

* 确保设备已加入企业的域。
* 启用组策略设置。

**要启用组策略设置，请执行以下操作：**

1. 在您的设备中，运行 `gpedit.msc`。
1. 导航到“计 **算机配置”>“管理模板”>“Windows组件”>“应用程序包部署**”。
1. 右键单击“允许安 **装所有受信任的应用程序”**。
1. 单击 **编辑** ，然后选 **择启用**。

1. 单击&#x200B;**确定**。

编辑Visual Studio生成的PowerShell脚本，以阻止它获取开发人员许可证。

在PowerShell脚本中，设置变量： `$NeedDeveloperLicense = $false`.

对于未加入域的设备，需要侧载产品激活密钥。 您可以从Windows分销商处购买。

对于Windows 8.1主页版本，没有组策略，不允许进行企业侧加载，您不能将其与企业域相加。 使用开发人员许可证在Windows 8.1 Home Edition设备上部署应用程序。

有关详细信息，请单 [击此处](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx)。

## 使用Visual Studio部署应用程序 {#deploying-an-app-using-visual-studio}

在Windows上使用Visual Studio安装应用程序：

1. 使用远程调试器连接设备。\
   有关详细信息，请参 [阅在远程计算机上运行Windows应用商店应用程序](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine)。

1. 在Visual Studio中打开应用程序，从“解决方案平台”列表中选择Windows-x64、Windows-x86或Windows-AnyCPU，然后选择“远程 **计算机**”。
1. 您的应用程序已部署在远程计算机上。

