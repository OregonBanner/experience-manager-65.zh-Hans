---
title: 品牌化自定义
seo-title: 品牌化自定义
description: 自定义应用程序图标、应用程序名称、启动图像和登录页面，为AEM Forms应用程序提供独特的组织特定外观。
seo-description: 自定义应用程序图标、应用程序名称、启动图像和登录页面，为AEM Forms应用程序提供独特的组织特定外观。
uuid: fece0fa8-c417-45eb-93f1-a91b49835fa0
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f6440a36-719a-4f89-b7db-1af918a3469a
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 1%

---


# 品牌化自定义 {#branding-customization}

您可以自定义应用程序图标、应用程序名称、启动图像和登录页面，为AEM Forms应用程序提供特定于组织的独特外观。 例如，您可以更改图像以使用组织中的徽标。 AEM Forms应用程序支持以下自定义设置：

* 自定义应用程序图标和启动图像
* 自定义应用程序名称
* 在登录页面上自定义图像
* 自定义应用程序菜单中的徽标

## 自定义图标和启动图像{#customizing-icon-and-launch-images}

请执行以下步骤以自定义默认应用程序图标和AEM Forms应用程序的启动图像：

>[!NOTE]
>
>对于所有图标和图像，请使用非隔行PNG格式。

### 自定义图标并启动图像{#to-customize-icon-and-launch-images}

#### 对于iOS {#for-ios}

1. 在Xcode中打开`Capture.xcodeproj`项目。
1. （***对于自定义图标***）在Capture的导航器视图下，导航到&#x200B;**[!UICONTROL Capture > Capture > Supporting Files > Capture-info.plist]**。 单击“Icon files（图标文件）”旁的下拉框。 指定图标文件(.png)的名称，并上传位于&#x200B;**[!UICONTROL 捕获>捕获>资源>图标]**&#x200B;的文件。 当前支持的维度有：29x29、50x50、58x58、72x72、100x100和144x144。
1. （***用于自定义启动图像***）确保图像的文件名为：

   * 对于纵向：`Default-Portrait~ipad.png`和`Default-Portrait@2x~ipad.png`
   * 对于横向：`Default-Landscape~ipad.png`和`Default-Landscape@2x~ipad.png`

   将它们上传到Capture项目以替换项目中的现有文件。

   >[!NOTE]
   >
   >确保图像的名称和分辨率与您在项目中替换的图像匹配。

1. 在iOS设备或iOS模拟器上构建和运行AEM Forms应用程序。

#### 对于Android {#for-android}

1. 将应用程序图标文件命名为：

   `ic_launcher.png`

1. 将相应的图标文件放在以下目录中：

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`

   >[!NOTE]
   >
   >确保图像的名称和分辨率与您在项目中替换的图像匹配。

1. 重新构建AEM Forms应用程序。

### 对于Windows {#for-windows}

1. 替换路径中的图标：

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. 替换路径中的启动器图像：

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >确保图像的名称和分辨率与您在项目中替换的图像匹配。

1. 重新构建AEM Forms应用程序。

## 自定义应用程序名称{#customize-the-app-name}

### 对于iOS {#for-ios-1}

1. 在Xcode中打开`Capture.xcodeproj`项目。
1. 在Capture的导航器视图下，导航到&#x200B;**[!UICONTROL Capture > Capture > Supporting Files > InfoPlist.strings]**。

   将`CFBundleDisplayName`属性的值更新为要为应用程序显示的名称。

1. 在iOS设备或iOS模拟器上构建和运行AEM Forms应用程序。

   有关构建适用于iOS的应用程序的详细信息，请参阅[设置Xcode项目和构建iOS应用程序](/help/forms/using/setup-xcode-project-build-installer.md)。

### 对于Android {#for-android-1}

1. 在任何文本或Xml编辑器中打开以下Xml:

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. 更新键`app_name`的值。
1. 重新构建AEM Forms应用程序。

   有关构建适用于Android的应用程序的详细信息，请参阅[设置Eclipse项目和构建Android应用程序](/help/forms/using/setup-eclipse-project-build-installer.md)。

### 对于Windows {#for-windows-1}

1. 在任何文本编辑器中打开以下Xml:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. 更新`<name>...</name>`标记中的值。
1. 重新构建AEM Forms应用程序。

   有关构建适用于Windows的应用程序的详细信息，请参阅[设置Visual Studio项目和构建Windows应用程序](/help/forms/using/setup-visual-studio-project-build-installer.md)。

## 在登录页面{#customizing-images-on-the-login-page}上自定义图像

AEM Forms应用程序的登录页面有徽标和背景图像。 徽标位于登录对话框的上方，背景图像位于登录对话框的下方。 请执行以下步骤以自定义登录页面上的默认图像：

**开始之前**

确保您具有以下图像：

<table>
 <tbody>
  <tr>
   <th><p>描述</p> </th>
   <th><p>大小</p> </th>
   <th><p>文件名</p> </th>
  </tr>
  <tr>
   <td><p>徽标</p> </td>
   <td><p>72 x 72像素</p> </td>
   <td><p>LC-logo.png</p> </td>
  </tr>
  <tr>
   <td><p>背景图像（纵向）</p> </td>
   <td><p>1280 x 989像素</p> </td>
   <td><p>Landing_bg.jpeg</p> </td>
  </tr>
 </tbody>
</table>

**使用Xcode在登录页面上自定义图像**

1. 在Xcode中打开`Capture.xcodeproj`项目。

1. 导航到`www/wsmobile/images`文件夹。
1. 要更改标志，请将默认的`LC-logo.png`文件替换为自定义的`LC-logo.png`文件。
1. 要更改背景，请将默认的`Landing_bg.jpeg`文件替换为自定义的`Landing_bg.jpeg`文件。
1. 在iOS设备或iOS模拟器上构建和运行AEM Forms应用程序。

### 使用Eclipse {#to-customize-images-on-the-login-pages-using-eclipse}自定义登录页面上的图像

1. 在Eclipse中打开Android项目。

1. 导航到`assets/www/wsmobile/images`文件夹。
1. 要更改标志，请将默认的`LC-logo.png`文件替换为自定义的`LC-logo.png`文件。
1. 要更改背景，请将默认的`Landing_bg.jpeg`文件替换为自定义的`Landing_bg.jpeg`文件。
1. 在Android设备上构建和运行AEM Forms应用程序。

### 使用Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio}自定义登录页面上的图像

1. 在Visual Studio中打开`MWSWindows.sln`项目。

1. 导航到`MWSWindows\www\wsmobile\images`文件夹。
1. 要更改标志，请将默认的`LC-logo.png`文件替换为自定义的`LC-logo.png`文件。
1. 要更改背景，请将默认的`Landing_bg.jpeg`文件替换为自定义的`Landing_bg.jpeg`文件。
1. 在Windows设备上构建和运行AEM Forms应用程序。

## 自定义应用程序菜单{#customizing_images_on_the_login_page-1}中的徽标

登录AEM Forms应用程序并点击菜单按钮后，您会在菜单上方看到徽标。 请执行以下步骤以自定义默认标志：

**开始之前**

确保您具有以下图像：

<table>
 <tbody>
  <tr>
   <th><p>描述</p> </th>
   <th><p>大小</p> </th>
   <th><p>文件名</p> </th>
  </tr>
  <tr>
   <td><p>徽标</p> </td>
   <td><p>72 x 72像素</p> </td>
   <td><p>aem_icon.png</p> </td>
  </tr>
 </tbody>
</table>

**使用Xcode在登录页面上自定义图像**

1. 在Xcode中打开`Capture.xcodeproj`项目。

1. 导航到`www/wsmobile/images`文件夹。
1. 要更改标志，请将默认的`aem_icon.png`文件替换为自定义的`aem_icon.png`文件。
1. 在iOS设备或iOS模拟器上构建和运行AEM Forms应用程序。

### 使用Eclipse {#to-customize-images-on-the-login-pages-using-eclipse-1}自定义登录页面上的图像

1. 在Eclipse中打开Android项目。

1. 导航到`assets/www/wsmobile/images`文件夹。
1. 要更改标志，请将默认的`aem_icon.png`文件替换为自定义的`aem_icon.png`文件。
1. 在Android设备上构建和运行AEM Forms应用程序。

### 使用Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio-1}自定义登录页面上的图像

1. 在Visual Studio中打开`MWSWindows.sln`项目。

1. 导航到`MWSWindows\www\wsmobile\images`文件夹。
1. 要更改标志，请将默认的`aem_icon.png`文件替换为自定义的`aem_icon.png`文件。
1. 在Windows设备上构建和运行AEM Forms应用程序。
