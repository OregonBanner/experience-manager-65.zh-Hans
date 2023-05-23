---
title: 設定Visual Studio專案並建置Windows應用程式
seo-title: Set up the Visual Studio project and build the Windows app
description: 瞭解如何設定Visual Studio專案以建置AEM Forms Windows行動裝置應用程式。
seo-description: Learn how to set up a Visual Studio project to build the AEM Forms Windows mobile device app.
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
exl-id: ae7340c8-38cc-4b2b-ba17-22011471fd7d
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 5%

---

# 設定Visual Studio專案並建置Windows應用程式{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms提供AEM Forms應用程式的完整原始碼。 來源包含建立自訂工作區應用程式的所有元件。 原始程式碼封存， `adobe-lc-mobileworkspace-src-<version>.zip`是 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 軟體發佈上的套件。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 區段：
   1. 選取 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 下拉式清單。
   2. 選取套件的版本和型別。 您也可以使用 **[!UICONTROL 搜尋下載]** 篩選結果的選項。
1. 點選適用於您的作業系統的套件名稱，然後選取 **[!UICONTROL 接受EULA條款]**，然後點選 **[!UICONTROL 下載]**.
1. 打开[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 選取套件並按一下 **[!UICONTROL 安裝]**.

1. 若要下載原始程式碼封存，請開啟 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 在您的瀏覽器中。\
   來源套件會下載到您的裝置上。

下圖顯示擷取的 `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content-1](assets/mws-content-1.png)

下列影像顯示 `windows` 中的資料夾 `src` 資料夾。

![win-dir](assets/win-dir.png)

## 設定環境 {#setting-up-the-environment}

若是Windows裝置，您需要：

* Microsoft Windows 8.1或Windows 10
* Microsoft Visual Studio 2015
* Microsoft Visual Studio Tools for Apache Cordova

## 設定Visual Studio Project for AEM Forms應用程式 {#setting-up-visual-studio-project-for-aem-forms-app}

執行以下步驟，在Visual Studio中設定AEM Forms應用程式專案。

1. 複製 `adobe-lc-mobileworkspace-src-<version>.zip` 封存至 `%HOMEPATH%\Projects` 資料夾（在已安裝及設定Visual Studio 2015的Windows 8.1或Windows 10裝置上）。
1. 在中擷取封存 `%HOMEPATH%\Projects\MobileWorkspace` 目錄。
1. 導覽至 `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` 目錄。
1. 開啟 `CordovaApp.sln` 使用Visual Studio 2015建立檔案並繼續建置AEM Forms應用程式。

## 建置AEM Forms應用程式 {#build-aem-forms-app}

執行以下步驟來建置和部署AEM Forms應用程式。

>[!NOTE]
>
>AEM Forms應用程式的Windows檔案系統上儲存的資料未加密。 建議您使用Windows BitLocker磁碟機加密之類的協力廠商工具來加密磁碟資料。

1. 在Visual Studio Standard工具列中，選取 **版本** 從「建置模式」下拉式清單中選取。

1. 根據您的平台選取Windows-AnyCPU、Windows-x64或Windows-x86。 建議使用Windows-AnyCPU。
1. 在Visual Studio解決方案總管中，以滑鼠右鍵按一下專案 **CordovaApp.Windows** 並選取 **商店>建立應用程式套件**.

   ![createapppackages](assets/createapppackages.png)

   便會顯示「建立應用程式套件」精靈。

   CordovaApp.Windows_3.0.2.0_anycpu.appx安裝程式檔案是在platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test目錄中建立。

   如果您遇到錯誤 `Retarget to windows 8.1 required`，以滑鼠右鍵按一下錯誤，然後在快顯功能表中選取 **重新鎖定目標至Windows 8.1**.

   ![重新鎖定目標 — 解決方案](assets/retarget-solution.png)

1. 在「建立應用程式套件」精靈中，選取天氣或不想將應用程式上傳至Windows市集，然後按一下 **下一個**.

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. 視需要在引數中進行變更，例如應用程式組建的版本和輸出位置。

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. 專案建立後，您可以使用以下方式安裝應用程式：

   * Windows PowerShell
   * Visual Studio

   此 `.appx` 套件需要下列專案才能成功安裝：

   1. WinJS資料庫
   1. 確保套件包含自我簽署的憑證，或受信任的授權單位簽署的公開憑證，例如VeriSign。
   1. 開發人員授權

   目錄Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test包含四個主要元件：

   1. `.appx` 檔案
   1. 憑證（目前是Apache Cordova的自簽憑證）
   1. 相依性資料夾
   1. PowerShell檔案（.ps1副檔名）



## 使用Windows PowerShell部署應用程式 {#deploying-an-app-using-windows-powershell}

在Windows裝置上安裝應用程式有兩種方式。

### 透過取得開發人員授權 {#by-acquiring-the-developer-license}

1. 以滑鼠右鍵按一下PowerShell檔案( `Add-AppDevPackage.ps1)`，並選擇 **使用PowerShell執行**.

1. 安裝程式會提示您取得開發人員授權。 使用Microsoft帳戶憑證取得開發人員授權。\
   本授權的有效期為30天，您可以免費續約。
1. 當您取得開發人員授權時，安裝程式會在系統上安裝自我簽署憑證，且應用程式會成功安裝。

### 透過使用企業擁有的裝置 {#by-using-enterprise-owned-devices}

對於已加入企業網域的企業擁有裝置，不需要取得開發人員授權。

企業擁有的裝置使用Professional和Enterprise版本的Windows。

Microsoft建議您安裝受信任的授權單位，例如VeriSign。

若要部署應用程式：

* 確保裝置已加入企業的網域。
* 啟用群組原則設定。

**若要啟用群組原則設定：**

1. 在您的裝置中，執行 `gpedit.msc`.
1. 導覽至 **電腦設定>系統管理範本> Windows元件>應用程式套件部署**.
1. 按一下右鍵 **允許安裝所有信任的應用程式**.
1. 按一下 **編輯** 並選取 **已啟用**.

1. 单击&#x200B;**确定**。

編輯Visual Studio產生的PowerShell指令碼，以停止其取得開發人員授權。

在PowerShell指令碼中，設定變數： `$NeedDeveloperLicense = $false`.

對於未加入網域的裝置，需要側載產品啟用金鑰。 您可以向Windows經銷商購買。

對於Windows 8.1 Home Edition，沒有群組原則，不允許企業端載入，而且您無法將其加入企業網域。 使用開發人員授權在Windows 8.1 Home Edition裝置上部署應用程式。

如需詳細資訊，請按一下 [此處](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx).

## 使用Visual Studio部署應用程式 {#deploying-an-app-using-visual-studio}

若要使用Visual Studio在Windows上安裝應用程式：

1. 使用遠端偵錯工具連線裝置。\
   如需詳細資訊，請參閱 [在遠端電腦上執行Windows市集應用程式](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine).

1. 在Visual Studio中開啟您的應用程式後，從「解決方案平台」清單中選擇Windows-x64、Windows-x86或Windows-AnyCPU，然後選取 **遠端電腦**.
1. 您的應用程式已部署在遠端電腦上。
