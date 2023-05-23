---
title: 設定Android Studio專案並建置Android應用程式
seo-title: Set up the Android studio project and build the Android app
description: 設定Android Studio專案和建置AEM Forms應用程式安裝程式的步驟
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

# 設定Android Studio專案並建置Android應用程式 {#set-up-the-android-studio-project-and-build-the-android-app}

本文章適用於建置AEM Forms應用程式6.3.1.1和更新版本。 若要從AEM Forms應用程式6.3的原始程式碼建立應用程式，請參閱 [設定Eclipse專案並建置Android™應用程式](/help/forms/using/setup-eclipse-project-build-installer.md).

AEM Forms提供AEM Forms應用程式的完整原始碼。 來源包含建立自訂AEM Forms應用程式的所有元件。 原始程式碼封存， `adobe-lc-mobileworkspace-src-<version>.zip` 是 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 軟體發佈上的套件。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 區段：
   1. 選取 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 下拉式清單。
   2. 選取套件的版本和型別。 您也可以使用 **[!UICONTROL 搜尋下載]** 篩選結果的選項。
1. 點選適用於您的作業系統的套件名稱，然後選取 **[!UICONTROL 接受EULA條款]**，然後點選 **[!UICONTROL 下載]**.
1. 打开[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 選取套件並按一下 **[!UICONTROL 安裝]**.

下圖顯示擷取的 `adobe-lc-mobileworkspace-src-<version>.zip`.

![已擷取壓縮的Android™來源內容](assets/mws-content-1.png)

下列影像顯示 `android`中的資料夾 `src`資料夾。

![src中android資料夾的目錄結構](assets/android-folder.png)

## 建置標準AEM Forms應用程式 {#set-up-the-xcode-project}

1. 執行以下步驟，在Android™ Studio中設定專案並提供簽署身分：

   登入已安裝並設定Android™ Studio的電腦。

1. 複製下載的 `adobe-lc-mobileworkspace-src-<version>.zip` 封存至：

   **適用於MAC使用者**： `[User_Home]/Projects`

   **針對Windows®使用者**： `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >若為Windows®，建議將Android專案保留在系統磁碟機中。

1. 解壓縮下列目錄中的封存：

   **適用於MAC使用者**： `[User_Home]/Projects/[your-project]`

   **針對Windows®使用者**： `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >建議您將擷取的Android專案匯入Android Studio之前，先保留在系統磁碟機中。

1. 啟動Android™ Studio。

   **適用於MAC使用者**：更新 `local.properties` 檔案存在於 `[User_Home]/Projects/[your-project]/android` 資料夾並指向 `sdk.dir` 變數至 `SDK` 在案頭上的位置。

   **針對Windows®使用者**：更新 `local.properties` 檔案存在於 `%HOMEPATH%\Projects\[your-project]\android` 資料夾並指向 `sdk.dir` 變數至 `SDK` 在案頭上的位置。

1. 按一下 **[!UICONTROL 完成]** 以建置專案。

   此專案可在ADT Project Explorer中使用。

   ![建立應用程式後執行eclipse專案](assets/eclipsebuildmws.png)

1. 在Android™ Studio中，選取 **[!UICONTROL 匯入專案（Eclipse ADT、Gradle等）]**.
1. 在專案總管中，選取您想在中建立的專案根目錄 **根目錄** 文字方塊：

   **若為Mac使用者：** [User_Home]/Projects/MobileWorkspace/src/android

   **對於Windows®使用者：** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. 匯入專案後，快顯視窗中會顯示更新Android™外掛程式Gradle的選項。 視您的需求按一下適當的按鈕。

   ![dontremindmeagainforthisproject](assets/dontremindmeagainforthisproject.png)

1. 成功建置Gradle後，會出現下列畫面。 將適當的裝置或模擬器連線至系統，然後按一下 **[!UICONTROL 執行Android™]**.

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio會顯示連線的裝置和可用的模擬器。 選取您要執行應用程式的裝置，然後按一下 **確定**.

   ![connecteddevice](assets/connecteddevice.png)

建立專案後，您可以選擇使用Android™ Debug Bridge或Android™ Studio安裝應用程式。

### 使用Android™ Debug Bridge {#andriod-debug-bridge}

您可以透過，在Android™裝置上安裝應用程式 [Android™ Debug Bridge](https://developer.android.com/tools/help/adb.html) 使用下列指令：

**適用於MAC使用者**： `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**針對Windows®使用者**： `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
