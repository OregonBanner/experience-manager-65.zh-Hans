---
title: 构建移动应用程序
seo-title: 构建移动应用程序
description: 本页提供有关如何使用GitHub提供的代码构建移动应用程序的完整分步文章，请参阅此处。构建您的应用程序以安装到设备或模拟器上进行测试或发布到应用商店。 您可以使用PhoneGap命令行界面在本地构建应用程序，或使用PhoneGap Build在云中构建应用程序。
seo-description: 本页提供有关如何使用GitHub提供的代码构建移动应用程序的完整分步文章，请参阅此处。构建您的应用程序以安装到设备或模拟器上进行测试或发布到应用商店。 您可以使用PhoneGap命令行界面在本地构建应用程序，或使用PhoneGap Build在云中构建应用程序。
uuid: 1ff6fe1a-24cc-4973-a2cd-8d356bc649b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b2778086-8280-4306-bf3a-f6ec2a0e04df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 1%

---


# 构建移动应用程序{#building-mobile-applications}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

构建应用程序以安装到设备或模拟器以进行测试或发布到应用程序商店。 您可以使用PhoneGap命令行界面在本地构建应用程序，或使用PhoneGap Build在云中构建应用程序。

[此处](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html)提供了有关如何使用GitHub提供的代码构建移动应用程序的完整分步文章。

## 将应用程序移到Publish实例{#moving-the-application-to-the-publish-instance}

将应用程序文件移动到发布实例，以便您能够为已安装的移动应用程序实例提供内容更新，以及使用已发布的内容构建应用程序。 应用程序由存储库中的两个节点分支组成：

* `/content/phonegap/apps/<application name>`:作者创建和激活的网页。
* `/content/phonegap/content/<application name>`:应用程序配置文件和内容同步配置。

>[!NOTE]
>
>如果不将应用程序文件移动到发布实例，内容作者将无法更新内容同步缓存。

您只需将`/content/phonegap/content/<application name>`分支中的文件移动到发布实例。 作者激活页面时，将移动`/content/phonegap/apps/<application name>`分支中的文件。

AEM提供两种将批量内容移动到发布实例的方法：

* [使用复制控制台](/help/sites-authoring/publishing-pages.md) 上的激活树命令。
* [创建包](/help/sites-administering/package-manager.md) 含内容的包并复制该包。

例如，将创建名为phonegapapp的移动应用程序。 必须将以下节点移动到发布实例：/content/phonegap/content/phonegapapp.

**提示：** 要将包从作者实例移动到发布实例，请对包使用“复制”命令。

![chlimage_1-16](assets/chlimage_1-16.png)

## 使用PhoneGap命令行接口{#building-using-the-phonegap-command-line-interface}构建

使用PhoneGap命令行界面(CLI)在您的计算机上编译PhoneGap应用程序。 要将AEM内容包含到您的应用程序中，AEM将创建一个ZIP文件，其中包含您的移动应用程序内容、内容同步配置和其他必需资源。 下载ZIP文件并将其包含在您的内部版本中。

### 准备构建环境{#preparing-your-build-environment}

要使用PhoneGap CLI进行构建，您需要安装Node.js和PhoneGap客户端实用程序。 您需要Internet连接才能执行以下过程。

1. 下载并安装[Node.js](https://nodejs.org/)。
1. 打开终端或命令提示符并输入以下节点命令以安装PhoneGap实用程序：

   ```shell
   npm install -g phonegap
   ```

   在Unix或Linux系统上，可能需要在命令前加上`sudo`前缀。

   终端显示一系列HTTPGET命令的结果。 安装成功后，终端将显示库的安装位置，与以下示例类似：

   ```xml
   /usr/local/bin/phonegap -> /usr/local/lib/node_modules/phonegap/bin/phonegap.js
   phonegap@3.3.0-0.19.6 /usr/local/lib/node_modules/phonegap
   ├── pluralize@0.0.4
   ├── colors@0.6.0-1
   ├── semver@1.1.0
   ├── qrcode-terminal@0.9.4
   ├── shelljs@0.1.4
   ├── optimist@0.6.0 (...)
   ├── prompt@0.2.11 (...)
   ├── phonegap-build@0.8.4 (...)
   ├── connect-phonegap@0.8.1 (...)
   └── cordova@3.3.0-0.1.1 (...)
   ```

1. （可选）获取您所针对的移动平台的SDK:

   * 要构建适用于iOS平台的应用程序，请安装最新版本的[Xcode](https://developer.apple.com/xcode/)。
   * 要构建Android应用程序，请安装[Android SDK](https://developer.android.com/)。

### 下载内容ZIP文件{#downloading-the-content-zip-file}

将移动应用程序的内容移到文件系统。

1. 在“移动应用程序”页面上，选择您的应用程序。
1. （可选）要构建应用程序以完成安装，请在工具栏中单击或点按清除缓存图标。

   ![](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >缓存保存已安装应用程序的内容更新。 清除缓存会撤消所有缓存的更新。

1. 在工具栏中，单击或点按下载CLI资产图标。

   ![](do-not-localize/chlimage_1-1.png)

1. 保存ZIP文件后，单击“成功”对话框上的“关闭”。
1. 解压ZIP文件的内容。

### 使用PhoneGap CLI构建{#using-the-phonegap-cli-to-build}

使用PhoneGap CLI编译和安装应用程序。 有关如何使用PhoneGap CLI的信息，请参阅PhoneGap [命令行界面](https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html)文档。

1. 打开终端或命令提示符，将当前目录更改为下载的应用程序ZIP文件。 例如，以下内容将目录更改为ng-app-cli.1392137825303.zip文件：

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. 输入您所定位平台的phonegap命令。 例如，以下命令构建适用于Android的应用程序：

   ```shell
   phonegap build android
   ```

## 使用PhoneGap Build{#building-using-phonegap-build}构建

使用PhoneGap云服务构建您的应用程序。 要执行此过程，必须先创建PhoneGap Build配置。

### 正在连接到 PhoneGap Build {#connecting-to-phonegap-build}

创建PhoneGap Build配置，以便从AEM内使用PhoneGap Build服务。 提供用于构建移动应用程序的PhoneGap Build帐户的用户名和密码。

1. 打开“工具”页面。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))。
1. 在“CQ操作”区域，单击Cloud Services。
1. 单击“立即配置”链接以获取PhoneGap Build。

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 在创建配置对话框中，键入标题属性的值。 默认情况下，“名称”属性的值是从标题派生的，但您可以输入名称。 单击创建。
1. 在“PhoneGap Build配置”对话框中，键入PhoneGap Build用户名和密码，然后单击“确定”。

### 使用PhoneGap Build{#using-phonegap-build}

将您的应用程序资源发送到PhoneGap Build，以便针对各种移动平台进行编译。

1. 在“移动应用程序”页面上，打开移动应用程序。 ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. （可选）要构建应用程序以完成安装，请选择该应用程序并单击“清除缓存”图标。

   ![](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >缓存保存已安装应用程序的内容更新。 清除缓存会撤消所有缓存的更新。

1. 选择初始页面，然后单击“构建远程”图标。

   ![](do-not-localize/chlimage_1-3.png)

   **注意：** 构建成功完成时，AEM Beta的测试版不会创建收件箱通知。

1. 在“成功”对话框中，单击“PhoneGap Build”以打开位于[https://build.phonegap.com/apps](https://build.phonegap.com/apps)的Adobe PhoneGap Build页面。 如果您正在等待应用程序出现，则可以检查[PhoneGap Build状态](https://status.build.phonegap.com/)页。

   有关安装内部版本的信息，请参阅[PhoneGap Build文档](https://docs.build.phonegap.com/en_US/3.1.0/#googtrans%28en%29)。

   >[!NOTE]
   >
   >免费PhoneGap Build帐户允许使用一个专用应用程序。 如果要构建其他专用应用程序，PhoneGap构建将失败。

### 后续步骤 {#the-next-steps}

构建过程后的下一步是了解应用程序](/help/mobile/phonegap-structure-an-app.md)的[结构。
