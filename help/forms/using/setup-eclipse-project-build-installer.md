---
title: 构建AEM FormsAndroid应用程序
seo-title: 构建AEM FormsAndroid应用程序
description: 设置Android Studio项目和为AndroidAEM Forms应用程序构建。apk文件的步骤
seo-description: 设置Android Studio项目和为AndroidAEM Forms应用程序构建。apk文件的步骤
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---


# 构建AEM FormsAndroid应用程序 {#build-the-aem-forms-android-app}

按照建议的序列执行以下步骤，为AEM Forms构建Android应用程序。

1. [下载AEM Forms应用程序源代码包](#download-android-zip)
1. [设置环境变量](#set-environment-variable-android)
1. [构建标准AEM Forms应用程序](#set-up-the-xcode-project)

## 下载AEM Forms应用程序源代码包 {#download-android-zip}

AEM Forms应用程序源代码包是指存 `adobe-lc-mobileworkspace-src-<version>.zip` 档。 此存档包含构建自定义AEM Forms应用程序所需的源代码。 存档包含在软件分 `adobe-aemfd-forms-app-src-pkg-<version>.zip`发上提供的包中。

请执行以下步骤下载文 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 件：

1. 开放 [软件分发](https://experience.adobe.com/downloads)。 您需要Adobe ID登录软件分发。
1. 点按 **[!UICONTROL 标题]** 菜单中可用的Adobe Experience Manager。
1. 在过滤器 **[!UICONTROL 部分]** :
   1. 从“ **[!UICONTROL 解决方]** 案 **[!UICONTROL ”下]** 拉列表中选择“表单”。
   2. 选择包的版本和类型。 您还可以使用“搜 **[!UICONTROL 索下载]** ”选项筛选结果。
1. 点按适用于您的操作系统的包名称，选择“ **[!UICONTROL 接受EULA条款]**”，然后点 **[!UICONTROL 按下载]**。
1. 打开 [包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) ，然后单 **[!UICONTROL 击“上传包]** ”以上传包。
1. Select the package and click **[!UICONTROL Install]**.
1. 要下载源代码存档，请在 **您的浏览器中打开https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>** .zip。 Android应用程序。zip文件将下载到您的设备上。
1. 将。zip文件的内容解压缩到本地文件系统上的文件夹中。 例如， *C:\&lt;文件夹结构>\adobe-lc-mobileworkspace-src-2.4.20*

下图显示文件夹的 `adobe-lc-mobileworkspace-src-<version>.zip\android`结构。

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 设置环境变量 {#set-environment-variable-android}

在开始环境应用程序的构建过程之前，请设置以下AEM Forms变量：

* 将JAVA_HOME环境变量设置为本地文件系统中JDK软件的位置。 例如，C:\Program Files\Java\jdk1.8.0_181
* 为Android `ANDROID_SDK_ROOT` 将系统环境变量设置为SDK位置。 例如，C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* 设置系 `Path` 统环境变量，以包括Android的平台工具和工具文件夹位置。 例如，C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools。

## 构建标准AEM Forms应用程序 {#set-up-the-xcode-project}

在本地文件系统上保存adobe-lc-mobileworkspace-src-&lt;version>.zip文件并设置环境变量后，使用以下任意选项构建标准AEM FormsAndroid应用程序：

* [使用Android Studio构建AEM Forms应用程序](#using-android-studio)
* [使用Android Studio生成。apk文件](#generate-apk-android-studio)

### 使用Android Studio构建AEM Forms应用程序 {#using-android-studio}

请执行以下步骤以使用Android Studio构建AEM Forms应用程序：

1. 在您的计算机上启动Android Studio应用程序。
1. 单击 **打开现有Android Studio项目**。 如果打开现有项目的对话框不自动显示，请选择“文 **件** ”>“ **打开”**。
1. 导航 *到本地文件系统上的adobe-lc-mobileworkspace-src-&lt;version>.zip/android* ，然后单击“确 **定”**。

   Android **选项** 显示在左窗格中。

   ![android_folder_studio](assets/android_folder_studio.png)

1. 从左 **窗格中** ，选择android，然后单 **击“运行** ” **>“**&#x200B;运行‘android’”。
1. 从“选择部署目标”对话框的“已连接设备”部分选择Android设备，然后单击“确定”。

   成功构建开发环境后，您现在可以对应用程序应用自定义。 使用以下文章自定义应用程序：

   * [品牌化自定义](/help/forms/using/branding-customization.md)
   * [主题自定义](/help/forms/using/theme-customization.md)
   * [手势自定义](/help/forms/using/gesture-customization.md)

   在将适当的自定义应用程序后，您可以生成要分发的。apk文件。

### 使用Android Studio生成。apk文件 {#generate-apk-android-studio}

执行以下步骤以使用Android Studio生成。apk文件：

1. 在您的计算机上启动Android Studio应用程序。
1. 选择 **打开现有Android Studio项目**。 如果打开现有项目的对话框不自动显示，请选择“文 **件** ”>“ **打开”**。
1. 导航 *到本地文件系统上的adobe-lc-mobileworkspace-src-&lt;version>.zip/android* ，然后单击“确 **定”**。

   android选项显示在左窗格中。

1. 选择 **“构建** ”> **“构建APK** ”以生成。apk文件。

   （可选）选 **择** “构建” **>“生成已签名的APK** ”以生 [成。apk文](https://developer.android.com/studio/publish/app-signing) 件的已签名版本。

## 使用Android Debug Bridge {#build-android-debug-bridge}

生成。apk文件后，请执行以下命令，使用Android Debug Bridge在Android设备上安 [装应用程序](https://developer.android.com/tools/help/adb.html)。

**Windows用户：** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**MAC用户：** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
