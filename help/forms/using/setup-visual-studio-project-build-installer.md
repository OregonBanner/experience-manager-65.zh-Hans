---
title: 设置Visual Studio项目并构建Windows应用程序
seo-title: 设置Visual Studio项目并构建Windows应用程序
description: 了解如何设置Visual Studio项目以构建AEM Forms Windows移动设备应用程序。
seo-description: 了解如何设置Visual Studio项目以构建AEM Forms Windows移动设备应用程序。
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
exl-id: ae7340c8-38cc-4b2b-ba17-22011471fd7d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 5%

---

# 设置Visual Studio项目并构建Windows应用程序{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms提供AEM Forms应用程序的完整源代码。 该源包含用于构建自定义工作区应用程序的所有组件。 源代码存档`adobe-lc-mobileworkspace-src-<version>.zip`是Software Distribution上`adobe-aemfd-forms-app-src-pkg-<version>.zip`包的一部分。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;部分中：
   1. 从&#x200B;**[!UICONTROL Solution]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Forms]**。
   2. 选择包的版本和类型。 您还可以使用&#x200B;**[!UICONTROL 搜索下载]**&#x200B;选项来筛选结果。
1. 点按适用于您的操作系统的包名称，选择&#x200B;**[!UICONTROL 接受EULA条款]**，然后点按&#x200B;**[!UICONTROL 下载]**。
1. 打开[包管理器](https://docs.adobe.com/content/help/zh-Hans/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 选择包并单击&#x200B;**[!UICONTROL Install]**。

1. 要下载源代码存档，请在浏览器中打开`https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip`。\
   将在您的设备上下载源包。

下图显示了`adobe-lc-mobileworkspace-src-<version>.zip`的提取内容。

![mws-content-1](assets/mws-content-1.png)

下图显示了`src`文件夹中`windows`文件夹的目录结构。

![win-dir](assets/win-dir.png)

## 设置环境{#setting-up-the-environment}

对于Windows设备，您需要：

* Microsoft Windows 8.1或Windows 10
* Microsoft Visual Studio 2015
* 适用于Apache Cordova的Microsoft Visual Studio Tools

## 为AEM Forms应用程序{#setting-up-visual-studio-project-for-aem-forms-app}设置Visual Studio项目

执行以下步骤，在Visual Studio中设置AEM Forms应用程序项目。

1. 将`adobe-lc-mobileworkspace-src-<version>.zip`存档文件复制到安装并配置了Visual Studio 2015的Windows 8.1或Windows 10设备的`%HOMEPATH%\Projects`文件夹中。
1. 提取`%HOMEPATH%\Projects\MobileWorkspace`目录中的存档。
1. 导航到`%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows`目录。
1. 使用Visual Studio 2015打开`CordovaApp.sln`文件，然后继续构建AEM Forms应用程序。

## 构建AEM Forms应用程序{#build-aem-forms-app}

执行以下步骤来构建和部署AEM Forms应用程序。

>[!NOTE]
>
>存储在AEM Forms应用程序的Windows文件系统上的数据未加密。 建议您使用诸如Windows BitLocker驱动器加密之类的第三方工具来加密磁盘数据。

1. 在Visual Studio标准工具栏中，从构建模式的下拉列表中选择&#x200B;**Release**。

1. 根据您的平台选择Windows-AnyCPU、Windows-x64或Windows-x86。 建议使用Windows-AnyCPU。
1. 在Visual Studio解决方案资源管理器中，右键单击项目&#x200B;**CordovaApp.Windows**，然后选择&#x200B;**商店>创建AppPackages**。

   ![createapppackages](assets/createapppackages.png)

   此时会显示创建应用程序包向导。

   CordovaApp.Windows_3.0.2.0_anycpu.appx安装程序文件创建在platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test目录中。

   如果遇到错误`Retarget to windows 8.1 required`，请右键单击该错误，然后在弹出菜单中，选择&#x200B;**重定位到Windows 8.1**。

   ![重定位解决方案](assets/retarget-solution.png)

1. 在“创建应用程序包”向导中，选择天气或您不希望将应用程序上传到windows应用商店，然后单击&#x200B;**下一步**。

   ![createapppackage向导1](assets/createapppackageswizard1.png)

1. 根据需要，在参数中进行更改，例如应用程序内部版本的版本和输出位置。

   ![createapppackage向导2](assets/createapppackageswizard2.png)

1. 构建项目后，您可以使用以下方法安装应用程序：

   * Windows PowerShell
   * Visual Studio

   `.appx`包需要以下项目才能成功安装：

   1. WinJS库
   1. 确保包附带自签名证书，或受信任机构签名的公共证书（如VeriSign）。
   1. 开发人员许可证

   Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test目录包含其中的四个主要组件：

   1. `.appx` 文件
   1. 证书（目前是Apache Cordova自签名的证书）
   1. 依赖关系文件夹
   1. PowerShell文件（.ps1扩展名）



## 使用Windows PowerShell {#deploying-an-app-using-windows-powershell}部署应用程序

在Windows设备上安装应用程序有两种方法。

### 通过获取开发人员许可证{#by-acquiring-the-developer-license}

1. 右键单击PowerShell文件(`Add-AppDevPackage.ps1)`)，然后选择&#x200B;**使用PowerShell**&#x200B;运行。

1. 安装程序会提示您获取开发人员许可证。 使用Microsoft帐户凭据获取开发人员许可证。\
   此许可证的有效期为30天，您可以免费续订此许可证。
1. 当您获得开发人员许可证时，安装程序会在系统上安装自签名证书，并且应用程序安装成功。

### 使用企业自有设备{#by-using-enterprise-owned-devices}

对于加入企业域的企业自有设备，无需获取开发人员许可证。

企业自有设备使用Windows的专业版和企业版。

Microsoft建议您安装颁发公共证书（如VeriSign）的受信任机构。

要部署应用程序，请执行以下操作：

* 确保设备已加入到企业的域中。
* 启用组策略设置。

**要启用组策略设置，请执行以下操作：**

1. 在设备中，运行`gpedit.msc`。
1. 导航到&#x200B;**计算机配置>管理模板> Windows组件>应用程序包部署**。
1. 右键单击&#x200B;**允许所有受信任的应用程序安装**。
1. 单击&#x200B;**编辑**&#x200B;并选择&#x200B;**已启用**。

1. 单击&#x200B;**确定**。

编辑Visual Studio生成的PowerShell脚本，以阻止其获取开发人员许可证。

在PowerShell脚本中，设置变量：`$NeedDeveloperLicense = $false`。

对于未加入域的设备，需要边加载产品激活密钥。 您可以从Windows经销商处购买。

对于Windows 8.1主版，没有组策略，不允许企业侧加载，您不能将其加入到企业域中。 使用开发人员许可证在Windows 8.1 Home Edition设备上部署应用程序。

有关更多信息，请单击[此处](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx)。

## 使用Visual Studio {#deploying-an-app-using-visual-studio}部署应用程序

要使用Visual Studio在Windows上安装应用程序，请执行以下操作：

1. 使用远程调试器连接设备。\
   有关详细信息，请参阅[在远程计算机上运行Windows应用商店应用程序](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine)。

1. 在Visual Studio中打开应用程序后，从“解决方案平台”列表中选择Windows-x64、Windows-x86或Windows-AnyCPU，然后选择&#x200B;**远程计算机**。
1. 您的应用程序已部署在远程计算机上。
