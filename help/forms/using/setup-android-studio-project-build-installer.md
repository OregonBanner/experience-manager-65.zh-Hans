---
title: 设置Android Studio项目并构建Android应用程序
seo-title: Set up the Android studio project and build the Android app
description: 设置Android Studio项目并构建AEM Forms应用程序安装程序的步骤
seo-description: Steps to set up the Android Studio project and build the installer for the AEM Forms app
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 7%

---

# 设置Android Studio项目并构建Android应用程序 {#set-up-the-android-studio-project-and-build-the-android-app}

本文适用于构建AEM Forms应用程序6.3.1.1及更高版本。 有关从AEM Forms应用程序6.3的源代码构建应用程序的信息，请参阅 [设置Eclipse项目并构建Android™应用程序](/help/forms/using/setup-eclipse-project-build-installer.md).

AEM Forms提供AEM Forms应用程序的完整源代码。 该源包含用于构建自定义AEM Forms应用程序的所有组件。 源代码存档， `adobe-lc-mobileworkspace-src-<version>.zip` 是 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 软件包。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 过滤器]** 部分：
   1. 选择 **[!UICONTROL Forms]** 从 **[!UICONTROL 解决方案]** 下拉列表。
   2. 选择包的版本和类型。 您还可以使用 **[!UICONTROL 搜索下载]** 选项来筛选结果。
1. 点按适用于您的操作系统的包名称，选择 **[!UICONTROL 接受EULA条款]**，然后点按 **[!UICONTROL 下载]**.
1. 打开[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 选择包并单击 **[!UICONTROL 安装]**.

下图显示了 `adobe-lc-mobileworkspace-src-<version>.zip`.

![压缩的Android™源的提取内容](assets/mws-content-1.png)

下图显示了 `android`文件夹 `src`文件夹。

![src中android文件夹的目录结构](assets/android-folder.png)

## 构建标准AEM Forms应用程序 {#set-up-the-xcode-project}

1. 执行以下步骤以在Android™ Studio中设置项目并提供签名身份：

   登录到已安装和配置Android™ Studio的计算机。

1. 复制下载的 `adobe-lc-mobileworkspace-src-<version>.zip` 存档到：

   **对于MAC用户**: `[User_Home]/Projects`

   **对于Windows®用户**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >对于Windows®，建议将android项目保留在系统驱动器中。

1. 在以下目录中提取存档：

   **对于MAC用户**: `[User_Home]/Projects/[your-project]`

   **对于Windows®用户**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >建议先将提取的android项目保留在系统驱动器中，然后再将项目导入Android Studio。

1. 启动Android™ Studio。

   **对于MAC用户**:更新 `local.properties` 文件存在于 `[User_Home]/Projects/[your-project]/android` 文件夹并指向 `sdk.dir` 变量 `SDK` 位置。

   **对于Windows®用户**:更新 `local.properties` 文件存在于 `%HOMEPATH%\Projects\[your-project]\android` 文件夹并指向 `sdk.dir` 变量 `SDK` 位置。

1. 单击 **[!UICONTROL 完成]** 来构建项目。

   项目在ADT项目资源管理器中可用。

   ![构建应用程序后的eclipse项目](assets/eclipsebuildmws.png)

1. 在Android™ Studio中，选择 **[!UICONTROL 导入项目（Eclipse ADT、Gradle等）]**.
1. 在项目资源管理器中，选择要在中构建的项目的根目录 **根目录** 文本框：

   **对于Mac用户：** [User_Home]/Projects/MobileWorkspace/src/android

   **对于Windows®用户：** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. 导入项目后，会显示一个弹出窗口，其中包含用于更新Android™插件Gradle的选项。 根据您的要求单击相应的按钮。

   ![dontremindmeagainfortproject](assets/dontremindmeagainforthisproject.png)

1. 成功生成Gradle后，将显示以下屏幕。 将相应的设备或模拟器与系统连接，然后单击 **[!UICONTROL 运行Android™]**.

   ![格拉克莱孔索莱](assets/gradleconsole.png)

1. Android™ Studio显示连接的设备和可用的模拟器。 选择要运行应用程序的设备，然后单击 **确定**.

   ![connecteddevice](assets/connecteddevice.png)

构建项目后，您可以选择使用Android™ Debug Bridge或Android™ Studio安装应用程序。

### 使用Android™ Debug Bridge {#andriod-debug-bridge}

您可以在Android™设备上通过 [Android™ Debug Bridge](https://developer.android.com/tools/help/adb.html) 使用以下命令：

**对于MAC用户**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**对于Windows®用户**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
