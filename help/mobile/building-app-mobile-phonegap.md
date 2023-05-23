---
title: 建立行動應用程式
seo-title: Building Mobile Applications
description: 本頁提供如何使用GitHub提供的程式碼來建立行動應用程式的完整逐步文章。建立您的應用程式以安裝至裝置或模擬器，以進行測試或發佈至應用程式商店。 您可以使用PhoneGap命令列介面在本機建立應用程式，或使用PhoneGap Build在雲端中建立應用程式。
seo-description: This page provides a complete step-by-step article on how to build a mobile application using code available from GitHub is available here.Build your application to install to a device or simulator for testing or for publishing to app stores. You can build applications locally using the PhoneGap Command Line Interface, or in the cloud using PhoneGap Build.
uuid: 1ff6fe1a-24cc-4973-a2cd-8d356bc649b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b2778086-8280-4306-bf3a-f6ec2a0e04df
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 1%

---

# 建立行動應用程式{#building-mobile-applications}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

建置您的應用程式以安裝至裝置或模擬器，以進行測試或發佈至應用程式商店。 您可以使用PhoneGap命令列介面在本機建立應用程式，或使用PhoneGap Build在雲端中建立應用程式。

有關如何使用GitHub提供的程式碼建立行動應用程式的完整逐步文章，已可供參考 [此處](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html).

## 將應用程式移動到發佈執行個體 {#moving-the-application-to-the-publish-instance}

將應用程式檔案移至發佈執行個體，讓您可以將內容更新提供給已安裝的行動應用程式執行個體，並使用發佈的內容建置應用程式。 應用程式包含存放庫中的兩個節點分支：

* `/content/phonegap/apps/<application name>`：作者建立和啟動的網頁。
* `/content/phonegap/content/<application name>`：應用程式設定檔案和內容同步設定。

>[!NOTE]
>
>如果您未將應用程式檔案移至發佈執行個體，內容作者將無法更新Content Sync快取。

您只需要移動以下位置的檔案： `/content/phonegap/content/<application name>` 分支至發佈執行個體。 中的檔案 `/content/phonegap/apps/<application name>` 分支會在作者啟動頁面時移動。

AEM提供將大量內容移動到發佈執行個體的兩種方法：

* [使用「啟動樹狀結構」指令](/help/sites-authoring/publishing-pages.md) 在復寫主控台上。
* [建立套件](/help/sites-administering/package-manager.md) 包含內容並復寫套件的檔案。

例如，建立名為phonegapapp的行動應用程式。 下列節點必須移至發佈執行個體： /content/phonegap/content/phonegapapp。

**秘訣：** 若要將套件從製作執行個體移動至發佈執行個體，請在套件上使用復寫命令。

![chlimage_1-16](assets/chlimage_1-16.png)

## 使用PhoneGap命令列介面建置 {#building-using-the-phonegap-command-line-interface}

使用PhoneGap命令列介面(CLI)編譯電腦上的PhoneGap應用程式。 為了將AEM內容納入您的應用程式，AEM會建立一個ZIP檔案，其中包含您行動應用程式的內容、Content Sync設定和其他必要資產。 下載ZIP檔案並將其包含在您的組建中。

### 準備您的組建環境 {#preparing-your-build-environment}

若要使用PhoneGap CLI建置，您必須安裝Node.js和PhoneGap使用者端公用程式。 您需要網際網路連線才能執行下列程式。

1. 下載並安裝 [Node.js](https://nodejs.org/).
1. 開啟終端機或命令提示字元並輸入下列節點命令以安裝PhoneGap公用程式：

   ```shell
   npm install -g phonegap
   ```

   在Unix或Linux系統上，您可能需要在命令的前置詞中加上 `sudo`.

   終端機會顯示一系列HTTPGET命令的結果。 安裝成功時，終端機會顯示程式庫的安裝位置，類似於以下範例：

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

1. （選用）取得您鎖定目標之行動平台的SDK：

   * 若要為iOS平台建置應用程式，請安裝最新版本的 [Xcode](https://developer.apple.com/xcode/).
   * 若要建置Android應用程式，請安裝 [Android SDK](https://developer.android.com/).

### 下載內容ZIP檔案 {#downloading-the-content-zip-file}

將行動應用程式的內容移至檔案系統。

1. 在行動應用程式頁面上，選取您的應用程式。
1. （可選）若要建置應用程式以進行完整安裝，請在工具列上按一下或點選「清除快取」圖示。

   ![](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >快取會儲存已安裝應用程式的內容更新。 清除快取會使所有快取的更新失效。

1. 在工具列上，按一下或點選「下載CLI資產」圖示。

   ![](do-not-localize/chlimage_1-1.png)

1. 儲存ZIP檔案後，按一下「成功」對話方塊上的「關閉」 。
1. 解壓縮ZIP檔案的內容。

### 使用PhoneGap CLI建置 {#using-the-phonegap-cli-to-build}

使用PhoneGap CLI編譯及安裝應用程式。 如需有關如何使用PhoneGap CLI的資訊，請參閱PhoneGap [命令列介面](https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html) 說明檔案。

1. 開啟終端機或命令提示字元，並將目前目錄變更為下載的應用程式ZIP檔案。 例如，下列會將目錄變更為ng-app-cli.1392137825303.zip檔案：

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. 輸入您要定位之平台的phonegap指令。 例如，以下命令會建置適用於Android的應用程式：

   ```shell
   phonegap build android
   ```

## 使用PhoneGap Build建置 {#building-using-phonegap-build}

使用PhoneGap雲端服務建置您的應用程式。 若要執行此程式，您必須先建立PhoneGap Build組態。

### 正在连接到 PhoneGap Build {#connecting-to-phonegap-build}

建立PhoneGap Build設定，以便您可以使用AEM中的PhoneGap Build服務。 提供您將用來建置行動應用程式之PhoneGap Build帳戶的使用者名稱和密碼。

1. 開啟「工具」頁面。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))。
1. 在「CQ操作」區域中，按一下「Cloud Services」。
1. 按一下PhoneGap Build的「立即設定」連結。

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 在建立設定對話方塊中，輸入Title屬性的值。 依預設，「名稱」屬性的值是從標題衍生而來，但您可以輸入名稱。 单击创建。
1. 在「PhoneGap Build組態」對話方塊中，輸入您的PhoneGap Build使用者名稱和密碼，然後按一下「確定」。

### 使用PhoneGap Build {#using-phonegap-build}

將您的應用程式資源傳送至PhoneGap Build，以便針對各種行動平台進行編譯。

1. 在行動應用程式頁面上，開啟您的行動應用程式。 ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. （選擇性）若要建立應用程式以完成安裝，請選取應用程式並按一下「清除快取」圖示。

   ![](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >快取會儲存已安裝應用程式的內容更新。 清除快取會使所有快取的更新失效。

1. 選取啟動顯示頁面，然後按一下「建置遠端」圖示。

   ![](do-not-localize/chlimage_1-3.png)

   **注意：** 建置成功完成時，Beta版的AEM Beta版不會建立收件匣通知。

1. 在「成功」對話方塊中，按一下「PhoneGap Build」以開啟Adobe PhoneGap Build頁面，網址為 [https://build.phonegap.com/apps](https://build.phonegap.com/apps). 如果您正等待應用程式出現，可以檢查 [PhoneGap Build狀態](https://status.build.phonegap.com/) 頁面。

   如需關於安裝組建的資訊，請參閱 [PhoneGap Build檔案](https://github.com/phonegap/phonegap-docs/tree/master/docs/4-phonegap-build).

   >[!NOTE]
   >
   >允許一個私密應用程式使用自由PhoneGap Build帳戶。 如果您要建置其他私人應用程式，PhoneGap建置會失敗。

### 后续步骤 {#the-next-steps}

建置程式後的下一個步驟是瞭解 [應用程式的結構](/help/mobile/phonegap-structure-an-app.md).
