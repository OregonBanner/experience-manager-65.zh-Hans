---
title: 设置Android studio项目并构建Android应用程序
seo-title: 设置Android studio项目并构建Android应用程序
description: 设置Android Studio项目和构建AEM Forms应用程序安装程序的步骤
seo-description: 设置Android Studio项目和构建AEM Forms应用程序安装程序的步骤
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---


# 设置Android studio项目并构建Android应用程序{#set-up-the-android-studio-project-and-build-the-android-app}

本文适用于构建AEM Forms应用程序6.3.1.1及更高版本。 有关从AEM FormsApp 6.3的源代码构建应用程序，请参阅[设置Eclipse项目并构建Android™应用程序](/help/forms/using/setup-eclipse-project-build-installer.md)。

AEM Forms提供AEM Forms应用的完整源代码。 该源包含构建自定义AEM Forms应用程序的所有组件。 源代码存档`adobe-lc-mobileworkspace-src-<version>.zip`是软件分发`adobe-aemfd-forms-app-src-pkg-<version>.zip`包的一部分。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 打开[软件分发](https://experience.adobe.com/downloads)。 您需要Adobe ID才能登录软件分发。
1. 点按标题菜单中的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL 过滤器]**&#x200B;部分中：
   1. 从&#x200B;**[!UICONTROL 解决方案]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Forms]**。
   2. 选择包的版本和类型。 您还可以使用&#x200B;**[!UICONTROL 搜索下载]**&#x200B;选项筛选结果。
1. 点按适用于您的操作系统的程序包名称，选择&#x200B;**[!UICONTROL 接受EULA条款]**，然后点按&#x200B;**[!UICONTROL 下载]**。
1. 打开[包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html)并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 选择软件包，然后单击&#x200B;**[!UICONTROL 安装]**。

下图显示了`adobe-lc-mobileworkspace-src-<version>.zip`的提取内容。

![解压缩的Android™源的提取内容](assets/mws-content-1.png)

下图显示了`src`文件夹中`android`文件夹的目录结构。

![src中android文件夹的目录结构](assets/android-folder.png)

## 构建标准AEM Forms应用程序{#set-up-the-xcode-project}

1. 执行以下步骤在Android™ Studio中设置项目并提供签名标识：

   登录到已安装和配置Android™ Studio的计算机。

1. 将下载的`adobe-lc-mobileworkspace-src-<version>.zip`存档复制到：

   **对于MAC用户**:  `[User_Home]/Projects`

   **对于Windows®用户**:  `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >对于Windows®，建议将android项目保留在系统驱动器中。

1. 在以下目录中解压存档：

   **对于MAC用户**:  `[User_Home]/Projects/[your-project]`

   **对于Windows®用户**:  `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >建议先将解压缩的android项目保留在系统驱动器中，然后再将项目导入Android Studio。

1. 启动Android™ Studio。

   **对于MAC用户**:更新文 `local.properties` 件夹中的 `[User_Home]/Projects/[your-project]/android` 文件，并将变 `sdk.dir` 量指 `SDK` 向桌面上的位置。

   **对于Windows®用户**:更新文 `local.properties` 件夹中的 `%HOMEPATH%\Projects\[your-project]\android` 文件，并将变 `sdk.dir` 量指 `SDK` 向桌面上的位置。

1. 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以构建项目。

   项目在ADT项目资源管理器中可用。

   ![构建应用程序后的eclipse项目](assets/eclipsebuildmws.png)

1. 在Android™ Studio中，选择&#x200B;**[!UICONTROL “导入项目”（Eclipse ADT、Gradle等）]**。
1. 在项目资源管理器中，在&#x200B;**根目录**&#x200B;文本框中选择要构建的项目的根目录：

   **对于Mac用户** [:User]_Home/Projects/MobileWorkspace/src/android

   **对于Windows®用户：** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. 导入项目后，将显示一个弹出窗口，其中包含更新Android™插件Gradle的选项。 根据您的要求，单击相应的按钮。

   ![dontremindmeagainfolterproject](assets/dontremindmeagainforthisproject.png)

1. 成功构建Gradle后，将显示以下屏幕。 将相应的设备或模拟器与系统连接，然后单击“运行Android™**[!UICONTROL ”。]**

   ![格拉克莱孔索尔](assets/gradleconsole.png)

1. Android™ Studio显示连接的设备和可用的模拟器。 选择要运行应用程序的设备，然后单击&#x200B;**确定**。

   ![连接设备](assets/connecteddevice.png)

构建项目后，您可以选择使用Android™ Debug Bridge或Android™ Studio安装应用程序。

### 使用Android™调试桥{#andriod-debug-bridge}

可通过[Android™调试桥](https://developer.android.com/tools/help/adb.html)在Android™设备上安装应用程序，并使用以下命令：

**对于MAC用户**:  `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**对于Windows®用户**:  `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
