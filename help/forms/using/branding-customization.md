---
title: 品牌化自定义
seo-title: Branding Customization
description: 自訂應用程式圖示、應用程式名稱、啟動影像和登入頁面，為AEM Forms應用程式提供獨特的組織專屬外觀和風格。
seo-description: Customize the application icon, application name, launch images, and login page to provide a distinct organization-specific look and feel to AEM Forms app.
uuid: fece0fa8-c417-45eb-93f1-a91b49835fa0
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f6440a36-719a-4f89-b7db-1af918a3469a
exl-id: 9333705b-9944-4a74-a30f-7d9ec85fd824
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 2%

---

# 品牌化自定义 {#branding-customization}

您可以自訂應用程式圖示、應用程式名稱、啟動影像和登入頁面，為AEM Forms應用程式提供獨特的組織特定外觀。 例如，您可以將影像變更為使用您組織的標誌。 AEM Forms應用程式支援下列自訂：

* 自訂應用程式圖示和啟動影像
* 自訂應用程式名稱
* 自訂登入頁面上的影像
* 在應用程式功能表中自訂標誌

## 自訂圖示和啟動影像 {#customizing-icon-and-launch-images}

執行以下步驟，自訂預設應用程式圖示和AEM Forms應用程式的啟動影像：

>[!NOTE]
>
>對於所有圖示和影像，請使用非交錯式PNG格式。

### 若要自訂圖示和啟動影像 {#to-customize-icon-and-launch-images}

#### 適用於iOS {#for-ios}

1. 開啟 `Capture.xcodeproj` Xcode中的專案。
1. (***用於自訂圖示***)在擷取的導覽器檢視中，導覽至 **[!UICONTROL 「擷取>擷取>支援檔案> Capture-info.plist」]**. 按一下圖示檔案旁的下拉式清單。 指定圖示檔案(.png)的名稱，並將檔案上傳至 **[!UICONTROL 擷取>擷取>資源>圖示]**. 目前支援的維度為：29x29、50x50、58x58、72x72、100x100和144x144。
1. (***用於自訂啟動影像***)確保影像的檔案名稱為：

   * 直向： `Default-Portrait~ipad.png` 和 `Default-Portrait@2x~ipad.png`
   * 橫向： `Default-Landscape~ipad.png` 和 `Default-Landscape@2x~ipad.png`

   將它們上傳到Capture專案以取代專案中的現有檔案。

   >[!NOTE]
   >
   >確保影像的名稱和解析度與您在專案中取代的影像相符。

1. 在iOS裝置或iOS模擬器上建置並執行AEM Forms應用程式。

#### 適用於Android {#for-android}

1. 將應用程式圖示檔案命名為：

   `ic_launcher.png`

1. 將對應的圖示檔案放在下列目錄中：

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`

   >[!NOTE]
   >
   >確保影像的名稱和解析度與您在專案中取代的影像相符。

1. 重建AEM Forms應用程式。

### 適用於Windows {#for-windows}

1. 取代路徑中的圖示：

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. 取代路徑中的啟動器影像：

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >確保影像的名稱和解析度與您在專案中取代的影像相符。

1. 重建AEM Forms應用程式。

## 自訂應用程式名稱 {#customize-the-app-name}

### 適用於iOS {#for-ios-1}

1. 開啟 `Capture.xcodeproj` Xcode中的專案。
1. 在「擷取」的導覽器檢視中，導覽至 **[!UICONTROL 擷取>擷取>支援檔案> InfoPlist.strings]**.

   更新值 `CFBundleDisplayName` 屬性至您要為應用程式顯示的名稱。

1. 在iOS裝置或iOS模擬器上建置並執行AEM Forms應用程式。

   如需為iOS建立應用程式的詳細資訊，請參閱 [設定Xcode專案並建置iOS應用程式](/help/forms/using/setup-xcode-project-build-installer.md).

### 適用於Android {#for-android-1}

1. 在任何文字或Xml編輯器中開啟下列Xml：

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. 更新索引鍵的值 `app_name`.
1. 重建AEM Forms應用程式。

   如需為Android建立應用程式的詳細資訊，請參閱 [設定Eclipse專案並建置Android應用程式](/help/forms/using/setup-eclipse-project-build-installer.md).

### 適用於Windows {#for-windows-1}

1. 在任何文字編輯器中開啟下列Xml：

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. 更新中的值 `<name>...</name>` 標籤之間。
1. 重建AEM Forms應用程式。

   如需為Windows建立應用程式的詳細資訊，請參閱 [設定Visual Studio專案並建置Windows應用程式](/help/forms/using/setup-visual-studio-project-build-installer.md).

## 自訂登入頁面上的影像 {#customizing-images-on-the-login-page}

AEM Forms應用程式的登入頁面具有標誌和背景影像。 標誌位於登入對話方塊的上方，背景影像位於登入對話方塊的下方。 執行以下步驟來自訂登入頁面上的預設影像：

**开始之前**

確定您有下列影像：

<table>
 <tbody>
  <tr>
   <th><p>描述</p> </th>
   <th><p>大小</p> </th>
   <th><p>文件名</p> </th>
  </tr>
  <tr>
   <td><p>徽标</p> </td>
   <td><p>72 x 72畫素</p> </td>
   <td><p>LC-logo.png</p> </td>
  </tr>
  <tr>
   <td><p>背景影像（縱向）</p> </td>
   <td><p>1280 x 989畫素</p> </td>
   <td><p>Landing_bg.jpeg</p> </td>
  </tr>
 </tbody>
</table>

**若要使用Xcode自訂登入頁面上的影像**

1. 開啟 `Capture.xcodeproj` Xcode中的專案。

1. 導覽至 `www/wsmobile/images`資料夾。
1. 若要變更標誌，請取代預設值 `LC-logo.png` 包含自訂的檔案 `LC-logo.png` 檔案。
1. 若要變更背景，請取代預設值 `Landing_bg.jpeg` 包含自訂的檔案 `Landing_bg.jpeg`檔案。
1. 在iOS裝置或iOS模擬器上建置並執行AEM Forms應用程式。

### 使用Eclipse自訂登入頁面上的影像 {#to-customize-images-on-the-login-pages-using-eclipse}

1. 在Eclipse中開啟Android專案。

1. 導覽至 `assets/www/wsmobile/images`資料夾。
1. 若要變更標誌，請取代預設值 `LC-logo.png` 包含自訂的檔案 `LC-logo.png` 檔案。
1. 若要變更背景，請取代預設值 `Landing_bg.jpeg` 包含自訂的檔案 `Landing_bg.jpeg`檔案。
1. 在Android裝置上建置並執行AEM Forms應用程式。

### 若要使用Visual Studio自訂登入頁面上的影像 {#to-customize-images-on-the-login-pages-using-visual-studio}

1. 開啟 `MWSWindows.sln` Visual Studio中的專案。

1. 導覽至 `MWSWindows\www\wsmobile\images`資料夾。
1. 若要變更標誌，請取代預設值 `LC-logo.png` 包含自訂的檔案 `LC-logo.png` 檔案。
1. 若要變更背景，請取代預設值 `Landing_bg.jpeg` 包含自訂的檔案 `Landing_bg.jpeg`檔案。
1. 在Windows裝置上建置並執行AEM Forms應用程式。

## 在應用程式功能表中自訂標誌 {#customizing_images_on_the_login_page-1}

登入AEM Forms應用程式並點選功能表按鈕後，您會看到功能表上方的標誌。 執行以下步驟來自訂預設標誌：

**开始之前**

確定您有下列影像：

<table>
 <tbody>
  <tr>
   <th><p>描述</p> </th>
   <th><p>大小</p> </th>
   <th><p>文件名</p> </th>
  </tr>
  <tr>
   <td><p>徽标</p> </td>
   <td><p>72 x 72畫素</p> </td>
   <td><p>aem_icon.png</p> </td>
  </tr>
 </tbody>
</table>

**若要使用Xcode自訂登入頁面上的影像**

1. 開啟 `Capture.xcodeproj` Xcode中的專案。

1. 導覽至 `www/wsmobile/images`資料夾。
1. 若要變更標誌，請取代預設值 `aem_icon.png` 包含自訂的檔案 `aem_icon.png` 檔案。
1. 在iOS裝置或iOS模擬器上建置並執行AEM Forms應用程式。

### 使用Eclipse自訂登入頁面上的影像 {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. 在Eclipse中開啟Android專案。

1. 導覽至 `assets/www/wsmobile/images`資料夾。
1. 若要變更標誌，請取代預設值 `aem_icon.png` 包含自訂的檔案 `aem_icon.png` 檔案。
1. 在Android裝置上建置並執行AEM Forms應用程式。

### 若要使用Visual Studio自訂登入頁面上的影像 {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. 開啟 `MWSWindows.sln` Visual Studio中的專案。

1. 導覽至 `MWSWindows\www\wsmobile\images`資料夾。
1. 若要變更標誌，請取代預設值 `aem_icon.png` 包含自訂的檔案 `aem_icon.png` 檔案。
1. 在Windows裝置上建置並執行AEM Forms應用程式。
