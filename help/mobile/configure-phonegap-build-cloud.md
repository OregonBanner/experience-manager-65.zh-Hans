---
title: 設定您的Adobe PhoneGap BuildCloud Service
seo-title: Configure your Adobe PhoneGap Build Cloud Service
description: 請依照本頁面的說明設定雲端服務，並使用PhoneGap Build建置您的應用程式。
seo-description: Follow this page for configuring the cloud services and building your application with PhoneGap build.
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# 設定您的Adobe PhoneGap BuildCloud Service {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

此 **PhoneGap Build拼貼** 應用程式儀表板上的可讓您透過Adobe PhoneGap Build服務建置和發佈您的PhoneGap行動應用程式。

內定義的所有支援平台 **管理應用程式** 使用PhoneGap Build推播遠端組建時，將建置圖磚 **PhoneGap Build** 圖磚。

您可以將遠端組建推送至 [https://build.phonegap.com](https://build.phonegap.com) 或下載來源以使用在本機建置 [PhoneGap CLI](https://docs.phonegap.com/references/phonegap-cli/).

![PhoneGap Build拼貼](assets/chlimage_1-60.png)

## 設定Cloud Service {#configuring-the-cloud-service}

為了充分利用PhoneGap Build，您需要使用您的PhoneGap Build帳戶資訊設定AEMPhoneGap BuildCloud Service。

如果您目前沒有帳戶，請瀏覽至 [https://build.phonegap.com](https://build.phonegap.com) 並註冊！ 如果您擁有Adobe Creative Cloud會籍，最多可支援25個私人應用程式（非開放原始碼應用程式）。

在您驗證PhoneGap Build帳戶有效後，請導覽至您的AEM Cloud Management Console，尤其是 [PhoneGap BuildCloud Service](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html)。

使用 **管理Cloud Services** 圖磚來設定新的雲端服務設定。

### 使用「管理Cloud Services」圖磚 {#using-manage-cloud-services-tile}

開始使用建置應用程式之前 **PhoneGap Build** 圖磚，您必須使用設定雲端服務 **管理Cloud Services** 圖磚(從AEM Mobile控制面板)。

若要為應用程式設定雲端服務，請遵循下列步驟：

1. 按一下右上角的 **管理Cloud Services** 圖磚。

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. 選擇 **PhoneGap Build** 選項來自 **新增或編輯Cloud Service** 畫面。

   单击&#x200B;**下一步**。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 輸入您的憑證以建立新的雲端設定。

   驗證後，按一下 **提交**. 此已設定的雲端設定現在顯示在 **管理Cloud Services** 圖磚。

   ![chlimage_1-63](assets/chlimage_1-63.png)

### 使用PhoneGap Build建立您的應用程式 {#building-your-application-with-phonegap-build}

設定雲端服務後，您就可以使用建置應用程式 **PhoneGap Build** 圖磚。 按一下右上角的「 」，從「 」中選擇 **建置遠端** 或 **下載來源** 選項。

![chlimage_1-64](assets/chlimage_1-64.png)

若要使用Adobe PhoneGap Build叫用遠端組建，請按一下 **建置遠端**.

>[!NOTE]
>
>如果組建因任何原因而失敗(下方紅色iOS圖示表示平台失敗)，您可以將滑鼠移至圖示上方，取得錯誤訊息。 或者，您可以按一下圖磚底部的三點圖示「……」，直接導覽至https://build.phonegap.com （您必須驗證），並直接觀看及管理您的組建。

### 使用PhoneGap CLI建置您的應用程式 {#building-your-application-with-phonegap-cli}

PhoneGap提供命令列介面，可在本機建立您的應用程式。

使用PhoneGap命令列介面(CLI)編譯電腦上的PhoneGap應用程式。 為了將AEM內容納入您的應用程式，AEM會建立一個ZIP檔案，其中包含您行動應用程式的內容、Content Sync設定和其他必要資產。 下載ZIP檔案並將其包含在您的組建中。

若要利用PhoneGap的命令列介面，您需要設定本機環境，以包含：

1. Platform SDK (iOS、Android、WindowsPhone...)和
1. PhoneGap CLI

您可以閱讀更多資訊 [此處](https://docs.phonegap.com/references/phonegap-cli/).

安裝先決條件後，請從終端機嘗試建立簡單的應用程式，並在模擬器中或更好的裝置上執行，以進行簡單的測試：

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>add — 如果您不想在連線的裝置上執行，請在此行的結尾進行模擬。

一旦您確認上述方法有效，請使用 **PhoneGap Build** 並排至 **下載來源**. 將檔案儲存並解壓縮至本機系統。 完成此操作後：

* 導覽至該儲存的檔案（資料夾）
* 執行「phonegap run ios」（或android等）

### 其他资源 {#additional-resources}

若要瞭解作者和開發人員的角色和責任，請參閱以下資源：

* [使用AEM為Adobe PhoneGap Enterprise開發](/help/mobile/developing-in-phonegap.md)
* [在AEM中為Adobe PhoneGap Enterprise製作](/help/mobile/phonegap.md)
