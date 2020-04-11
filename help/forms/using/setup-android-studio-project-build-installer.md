---
title: 设置Android Studio项目并构建Android应用程序
seo-title: 设置Android Studio项目并构建Android应用程序
description: 设置Android Studio项目和构建AEM Forms应用程序安装程序的步骤
seo-description: 设置Android Studio项目和构建AEM Forms应用程序安装程序的步骤
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 设置Android Studio项目并构建Android应用程序 {#set-up-the-android-studio-project-and-build-the-android-app}

本文用于构建AEM Forms应用程序6.3.1.1及更高版本。 有关从AEM Forms App 6.3的源代码构建应用程序的信息，请参阅 [设置Eclipse项目和构建Android™应用程序](/help/forms/using/setup-eclipse-project-build-installer.md)。

AEM Forms提供AEM Forms应用程序的完整源代码。 源包含用于构建自定义AEM Forms应用程序的所有组件。 源代码存档是 `adobe-lc-mobileworkspace-src-<version>.zip` 包共享上包的 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 一部分。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 导航到包共享

   URL: `https://<server>:<port>/crx/packageshare`.

1. 下载源包。 下载包时，它会添加到AEM Forms包管理器中。
1. 下载完毕后，导航到： `https://<server>:<port>/crx/packmgr/index.jsp`并安装 `adobe-aemfd-forms-app-src-pkg-<version>.zip`。

1. 要下载源代码存档，请在您的浏 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 览器中打开。

   源包将下载到您的设备上。

下图显示提取的内容 `adobe-lc-mobileworkspace-src-<version>.zip`。

![解压缩的Android™源的解压缩内容](assets/mws-content-1.png)

下图显示了文件夹中文件夹 `android`的目录结 `src`构。

![src中android文件夹的目录结构](assets/android-folder.png)

## 构建标准AEM Forms应用程序 {#set-up-the-xcode-project}

1. 执行以下步骤以在Android™ Studio中设置项目并提供签名标识：

   登录到已安装和配置Android™ Studio的计算机。

1. 将下载的存 `adobe-lc-mobileworkspace-src-<version>.zip` 档复制到：

   **对于MAC用户**: `[User_Home]/Projects`

   **对于Windows®用户**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >对于Windows®，建议将android项目保留在系统驱动器中。

1. 解压缩以下目录中的存档：

   **对于MAC用户**: `[User_Home]/Projects/[your-project]`

   **对于Windows®用户**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >建议在将项目导入Android Studio之前，先将解压的Android项目保留在系统驱动器中。

1. 启动Android™ Studio。

   **对于MAC用户**:更新文 `local.properties` 件夹中的文件， `[User_Home]/Projects/[your-project]/android` 并将变量指 `sdk.dir` 向桌面 `SDK` 上的位置。

   **对于Windows®用户**:更新文 `local.properties` 件夹中的文件， `%HOMEPATH%\Projects\[your-project]\android` 并将变量指 `sdk.dir` 向桌面 `SDK` 上的位置。

1. 单击 **[!UICONTROL 完成]** ，以构建项目。

   项目在ADT项目浏览器中可用。

   ![构建应用程序后的Eclipse项目](assets/eclipsebuildmws.png)

1. 在Android™ Studio中，选 **[!UICONTROL 择“导入项目”（Eclipse ADT、Gradle等）]**。
1. 在项目资源管理器中，在“根目录”文本框中选择要构建的项目的 **根目录** :

   **对于Mac用户：**[User_Home]/Projects/MobileWorkspace/src/android

   **对于Windows®用户：** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. 导入项目后，将显示一个弹出窗口，其中包含更新Android™插件Gradle的选项。 根据您的要求，单击相应的按钮。

   ![dontremindmeaganafulterproject](assets/dontremindmeagainforthisproject.png)

1. 成功构建Gradle后，将显示以下屏幕。 将相应的设备或模拟器与系统连接，然后单击“ **[!UICONTROL 运行Android™”]**。

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio显示连接的设备和可用的模拟器。 选择要运行应用程序的设备，然后单击“确 **定”**。

   ![已连接设备](assets/connecteddevice.png)

在构建项目后，您可以选择使用Android™ Debug Bridge或Android™ Studio安装应用程序。

### 使用Android™ Debug Bridge {#andriod-debug-bridge}

可以通过 [Android™ Debug Bridge使用以下命令在Android™设备上安装应用程序](https://developer.android.com/tools/help/adb.html) :

**对于MAC用户**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**对于Windows®用户**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
