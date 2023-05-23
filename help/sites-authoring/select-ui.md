---
title: 在AEM中選取您的使用者介面
description: 設定您在AEM中使用哪個介面。
uuid: ab127f2f-2f8a-4398-90dd-c5d48eed9e53
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: e418d330-f234-411d-8cad-3fd9906dcbee
docset: aem65
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 1%

---

# 選取您的UI{#selecting-your-ui}

雖然觸控式UI現在是標準UI，網站的管理和編輯幾乎已達功能對等性，但使用者有時可能想要切換至 [傳統UI](/help/sites-classic-ui-authoring/classicui.md). 有幾個選項可以執行此操作。

>[!NOTE]
>
>如需與傳統UI功能對等狀態的詳細資訊，請參閱 [Touch UI功能比較](/help/release-notes/touch-ui-features-status.md) 檔案。

您可以在多個位置定義要使用的UI：

* [為您的執行個體設定預設使用者介面](#configuring-the-default-ui-for-your-instance)
這會將預設UI設定為在使用者登入時顯示，儘管使用者可以覆寫此UI並為他們的帳戶或目前的工作階段選取不同的UI。

* [為您的帳戶設定傳統UI編寫](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
這會將UI設定為編輯頁面時使用的預設值，但使用者可以覆寫此設定，並為他們的帳戶或目前的工作階段選取不同的UI。

* [切換到目前工作階段的傳統UI](#switching-to-classic-ui-for-the-current-session)
這會切換到目前工作階段的傳統UI。

* 若為 [編寫頁面的系統會在與UI的關係中進行某些覆寫](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>用於切換至傳統UI的各種選項無法立即使用，必須針對您的執行個體專門設定。
>
>另請參閱 [啟用對傳統UI的存取](/help/sites-administering/enable-classic-ui.md) 以取得詳細資訊。

>[!NOTE]
>
>從舊版升級的執行個體將保留傳統UI以進行頁面編寫。
>
>升級後，頁面製作功能不會自動切換至觸控式UI，但您可以使用 [OSGi設定](/help/sites-deploying/configuring-osgi.md) 的 **WCM編寫UI模式服務** ( `AuthoringUIMode` 服務)。 另請參閱 [編輯器的使用者介面覆寫](#ui-overrides-for-the-editor).

## 為您的執行個體設定預設UI {#configuring-the-default-ui-for-your-instance}

系統管理員可以使用設定啟動時看到的UI和登入 [根對應](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

這可以由使用者預設值或工作階段設定來覆寫。

## 為您的帳戶設定傳統UI編寫 {#setting-classic-ui-authoring-for-your-account}

每個使用者都可以存取他/她 [使用者偏好設定](/help/sites-authoring/user-properties.md#userpreferences) 以定義他/她是否想要使用傳統UI來編寫頁面（而不是預設的UI）。

這可以由工作階段設定覆寫。

## 切換到目前工作階段的傳統UI {#switching-to-classic-ui-for-the-current-session}

使用觸控式UI時，桌上型電腦使用者可能想要恢復為傳統（僅限桌上型電腦） UI。 有幾種方法可以在目前的工作階段切換至傳統UI：

* **導覽連結**

   >[!CAUTION]
   >
   >這個用於切換至傳統UI的選項無法立即使用，必須針對您的執行個體進行專門設定。
   >
   >
   >另請參閱 [啟用對傳統UI的存取](/help/sites-administering/enable-classic-ui.md) 以取得詳細資訊。

   如果已啟用此功能，則每當您將滑鼠移至適用的主控台時，畫面都會顯示一個圖示（監視器的符號），點選/按一下此圖示即可在傳統UI中開啟適當的位置。

   例如，下列連結來自： **網站** 至 **siteadmin**：

   ![syui-01](assets/syui-01.png)

* **URL**

   傳統UI可使用歡迎畫面的URL進行存取，網址為 `welcome.html`. 例如：

   `https://localhost:4502/welcome.html`

   >[!NOTE]
   >
   >觸控式UI可透過以下方式存取： `sites.html`. 例如：
   >
   >
   >`https://localhost:4502/sites.html`

### 編輯頁面時切換到傳統UI {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>這個用於切換至傳統UI的選項無法立即使用，必須針對您的執行個體進行專門設定。
>
>另請參閱 [啟用對傳統UI的存取](/help/sites-administering/enable-classic-ui.md) 以取得詳細資訊。

如果已啟用， **開啟Classic UI** 可從以下網址取得： **頁面資訊** 對話方塊：

![syui-02](assets/syui-02.png)

### 編輯器的使用者介面覆寫 {#ui-overrides-for-the-editor}

在頁面編寫的情況下，由使用者或系統管理員定義的設定可由系統覆寫。

* 編寫頁面時：

   * 透過存取頁面時，會強制使用傳統編輯器 `cf#` 在URL中。 例如：
      `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * 使用時，會強制使用觸控式編輯器 `/editor.html` 在URL中或使用觸控裝置時。 例如：
      `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* 任何強制都是暫時的，只對瀏覽器工作階段有效

   * Cookie集的設定取決於是否啟用觸控功能( `editor.html`)或傳統( `cf#`)已使用。

* 透過開啟頁面時 `siteadmin`，將會檢查是否存在下列專案：

   * Cookie
   * 使用者偏好設定
   * 如果兩者都不存在，則預設值為中設定的定義。 [OSGi設定](/help/sites-deploying/configuring-osgi.md) 的 **WCM編寫UI模式服務** ( `AuthoringUIMode` 服務)。

>[!NOTE]
>
>若 [使用者已定義頁面編寫的偏好設定](#settingthedefaultauthoringuiforyouraccount)，不會透過變更OSGi屬性來覆寫。

>[!CAUTION]
>
>由於使用Cookie （如上所述），不建議執行以下任一操作：
>
>* 手動編輯URL — 非標準URL可能會導致未知的情況和缺乏功能。
>* 讓兩個編輯器同時開啟 — 例如，在不同的視窗中。

