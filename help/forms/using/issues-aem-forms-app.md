---
title: 疑難排解AEM Forms應用程式
seo-title: Troubleshoot AEM Forms app
description: 瞭解AEM Forms應用程式的常見問題以及如何疑難排解。
seo-description: Learn about common issues with AEM Forms app and how to troubleshoot them.
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
exl-id: caec5fc3-db52-4bf5-8eb2-17e5189ab819
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 1%

---

# 疑難排解AEM Forms應用程式 {#troubleshoot-aem-forms-app}

本文介紹建置AEM Forms應用程式時可能顯示的錯誤訊息，以及解決這些訊息的步驟。

本文章節包括：

* [iOS使用者的附件遺失](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [HTML5工作區使用者提交的表單草稿在入口網站上不可見](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [HTML5表單（未快取）無法載入AEM Forms應用程式](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms無法在Windows上同步](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [不支援的Gradle版本](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Gradle和Android Gradle外掛程式相容性問題](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## iOS使用者的附件遺失 {#attachment-loss-for-ios-users}

iOS適用的AEM Forms應用程式設定為在OSGi上與AEM Forms同步，僅支援欄位層級附件。 所有附件都必須有唯一的名稱。 如果多個附件具有相同的名稱，則只會保留一個附件，而其他具有相同名稱的所有附件都會遺失。 執行以下步驟，防止iOS裝置上的使用者發生資料遺失：

1. 在連線的伺服器上，導覽至 **Adobe Experience Manager >工具>作業> Web Console**.
1. 尋找並按一下 **[!UICONTROL 最適化表單和互動式通訊Web頻道設定]**.
1. 在 [!UICONTROL 最適化表單和互動式通訊Web頻道設定] 對話方塊，啟用 **將檔案名稱設為唯一**.

   若 **將檔案名稱設為唯一** 設定已停用，如果使用者嘗試提交具有多個附件的調適型表單，將會遇到資料遺失。

1. 单击“**保存**”。

## HTML5工作區使用者提交的表單草稿在入口網站上不可見 {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

適用於AEM Forms應用程式中啟用的HTML5表單，具有 **另存為草稿** HTML呈現設定檔，工作區使用者看不到已儲存的草稿。 若要檢視工作區使用者在入口網站上提交的HTML5表單已儲存草稿，請執行下列步驟：

1. 開啟CRXDE並使用管理員憑證登入。

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. 在CRXDE的根路徑中，按一下「存取控制」下的「存取控制清單」 **+**.
1. 在 **新增專案** 對話方塊中，按一下「主參與者」欄位中的群組搜尋按鈕。
1. 在「選取主參與者」對話方塊的「名稱」欄位中，輸入 `PERM_WORKSPACE_USER` 並按一下 **搜尋**.
1. 選取 `PERM_WORKSPACE_USER` 群組，並按一下 **確定**.
1. 在新增專案對話方塊中， `PERM_WORKSPACE_USER` 在「主體」欄位中選取了群組。

   啟用 `jcr:read` 使用者群組的許可權。

1. 单击&#x200B;**确定**。

## HTML5表單（未快取）無法載入AEM Forms應用程式 {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

當AEM Forms應用程式連線至舊版AEM Forms伺服器時，非快取的HTML5表單無法在AEM Forms應用程式中載入。

執行以下步驟以解決問題：

1. 在作者執行個體中，導覽至 **「Adobe Experience Manager >工具>設定Workspace App離線服務>立即設定」**.
1. 在 **Workspace App離線服務** 頁面，按一下 **手動資源快取**.

   URL： https://&lt;server>：&lt;port>/libs/fd/workspace-offline/content/config.html

1. 在 **手動資源快取** 索引標籤，按一下 **+** 按鈕以新增CRX路徑。
1. 在 **新增資源** 欄位，型別： /etc.clientlibs/fd/xfaforms/I18N/en_US.js ，然後按一下 **新增**.
1. 单击“**保存**”。

## AEM Forms無法在Windows上同步 {#aem-forms-do-not-sync-on-windows}

在Windows上的AEM Forms應用程式中，如果表單路徑或其任何資源包含大於或等於256個字元，則表單不會與連線的伺服器同步。

修改表單及其資源的路徑，將字元數減少到256個字元以下。

## 不支援的Gradle版本 {#unsupported-version-of-gradle}

**錯誤訊息：** 專案使用不支援的Gradle版本。

當您在Android Studio中建置AEM Forms應用程式時，會顯示錯誤訊息。 發生此問題是因為系統支援不支援的Gradle版本。

**解析度：** 按一下 **修正Gradle包裝並重新匯入專案** 以解決問題。

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle和Android Gradle外掛程式相容性問題 {#gradle-and-android-gradle-plug-in-compatibility-issues}

**錯誤訊息：** Android Gradle外掛程式和Gradle的版本不相容。

當您選取時，會顯示錯誤訊息 **建置APK** 選項來自 **建置** Android Studio使用者介面上的功能表。

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**解析度：** 開啟 **Gradle指令碼** > **gradle-wrapper.properties** 檔案並編輯 **distributionUrl** 屬性。

例如，Android Studio主控台建議將Gradle版本降級為3.5版。在中編輯版本 **distributionUrl**&#x200B;之&#x200B;**gradle-wrapper.properties** 檔案。

選取 **建置** > **建置APK** 再次解決錯誤並產生.apk檔案。

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
