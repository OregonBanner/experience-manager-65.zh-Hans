---
title: 設定Xcode專案並建置iOS應用程式
seo-title: Set up the Xcode project and build the iOS app
description: 說明如何建立適用於iOS的標準AEM Forms應用程式。
seo-description: Explains how to build standard AEM Forms app for iOS.
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
exl-id: 78ce6107-8821-47d6-86ab-7ab968945e7c
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 5%

---

# 設定Xcode專案並建置iOS應用程式{#set-up-the-xcode-project-and-build-the-ios-app}

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

1. 若要下載原始程式碼封存，請開啟 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 在您的瀏覽器中。
來源套件會下載到您的裝置上。

下圖顯示擷取的 `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

下表詳細說明了 `adobe-lc-mobileworkspace-src-[version]/ios` 資料夾。

<table>
 <tbody>
  <tr>
   <th><p>目录</p> </th>
   <th><p>内容</p> </th>
  </tr>
  <tr>
   <td><p><code>CordovaLib</code></p> </td>
   <td><p>PhoneGap SDK 6.4.0</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms</code></p> </td>
   <td><p>資源、PhoneGap外掛程式和應用程式的主要模組</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>適用於AEM Forms應用程式的Xcode專案</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>AEM Forms應用程式專案的HTML、CSS、影像和JavaScript檔案</p> </td>
  </tr>
 </tbody>
</table>

如需有關程式碼簽署和將裝置新增至iOS布建入口網站的詳細資訊，請參閱 [iOS程式碼簽署設定、處理和疑難排解](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## 建置標準AEM Forms應用程式 {#set-up-the-xcode-project}

1. 執行以下步驟，在Xcode中設定專案並提供簽署身分：

   登入已安裝並設定Xcode和iOS SDK的Mac電腦。

1. 複製 `adobe-lc-mobileworkspace-src-<version>.zip` 從下載資料夾封存到 `[User_Home]/Projects/`.
1. 在中擷取封存 `[User_Home]/Projects/[your-project]`目錄。
1. 導覽至 ` [User_Home]/Projects/ `[your-project]`/adobe-lc-mobileworkspace-src-[version]/ios` 目錄。
1. 開啟 `AEM Forms.xcodeproj` Xcode中的專案。
1. 按一下 **AEM Forms**，下 **目標**，選取 **AEM Forms**. 選取 **建置設定** 索引標籤中，找到 **程式碼簽署權利** 區段，並在Debug和Release欄位中執行下列任一項作業：

   * 將欄位保留為未指定，以便建立標準的行動工作區應用程式
   * 指定要前往的欄位，如中所述 [為iOS建立安全的AEM Forms應用程式](/help/forms/using/building-secure-mobile-workspace-app.md) 以建置安全的AEM Forms應用程式。

1. 在 **建置設定** 標籤，按一下 **全部** 然後按一下 **已合併**.
1. 從 **設定** 清單，展開 **程式碼簽署**.
1. 對象 **程式碼簽署身分**，請選取適當的簽名。 如需有關建立新簽章的詳細資訊，請參閱 [建立和下載開發佈建設定檔](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. 確保為以下專案選取了相同的簽章 **偵錯**， **版本**、和 **任何iOS SDK**.
1. 在中取代下列程式碼 `AEM Forms-info.plist` 檔案：

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   替換時使用以下內容 `yourserver.com` 具有適合您伺服器的主機名稱。

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSExceptionDomains</key>
   <dict>
   <key>yourserver.com</key>
   <dict>
   <!-Include to allow subdomains->
   <key>NSIncludesSubdomains</key>
   <true/>
   <!-Include to allow HTTP requests->
   <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
   <true/>
   <!-Include to support forward secrecy->
   <key>NSExceptionRequiresForwardSecrecy</key>
   <false/>
   <!-Include to specify minimum TLS version->
   <key>NSTemporaryExceptionMinimumTLSVersion</key>
   <string>TLSv1.1</string>
   </dict>
   </dict>
   </dict>
   ```

   >[!NOTE]
   >
   >只有在AEM Forms應用程式需要連線到不遵循App Transport Security要求的伺服器時，才需要執行此步驟。

1. 下 **專案**，選取 **AEM Forms** 並確保已選取適當的簽章 **程式碼簽署身分**， **偵錯**， **版本** 和 **任何iOS SDK**.
1. 將布建的iPad連線至Mac電腦。
1. 選取已布建的裝置 **AEM Forms** 專案。

   ![ipad](assets/ipad.png)

   已選取已布建的裝置iPad Air 2。

1. 選取 **產品** > **清除**.
1. 選取 **產品** > **建置**.

## 建立AEM Forms應用程式的安裝程式 {#build-the-installer-for-the-mobile-workspace-app}

您需要封存Xcode專案以建置安裝程式（.ipa檔案）和屬性清單（.plist檔案）檔案。 屬性清單檔案包含託管內部應用程式的設定資訊，例如應用程式的名稱和託管位置。 如需屬性清單檔案的詳細資訊，請參閱 [關於資訊屬性清單檔案](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. 將布建的iPad連線至Mac電腦。 如需有關布建iPad的詳細資訊，請參閱 [建立和下載開發佈建設定檔](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. 選取已布建的裝置 **AEM Forms** 專案。

   ![ipad-1](assets/ipad-1.png)

   已選取已布建的裝置iPad Air 2。

1. 選取 **產品** > **清除**.
1. 選取 **產品** > **建置**.
1. 選取 **產品** > **封存**.
1. 在「組織器 — 封存」中，選取專案的最新封存，然後按一下 **散佈**.
1. 選取 **儲存供企業或臨時部署使用** 作為分發和點按的方法 **下一個**.
1. 選取適當的 **程式碼簽署身分** 並按一下 **下一個**. 按一下 **允許** 以套用簽名。
1. 提供應用程式的名稱並選取 **儲存供企業發佈使用**.
1. 提供 **應用程式URL** （適用於應用程式）。 例如，若要在CRX伺服器上託管應用程式，請提供URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. 在 **標題** 欄位中指定AEM Forms。
1. 按一下 **儲存** 並關閉Xcode。

   安裝程式檔案， `AEM Forms.ipa`和屬性清單檔案， `AEM Forms-info.plist`，會在指定位置建立。

1. 開啟 `AEM Forms-info.plist` 編輯器中儲存的檔案。
1. 將.ipa檔案URL中的所有空格取代為%20。
1. 儲存並關閉 `AEM Forms-info.plist` 檔案。
