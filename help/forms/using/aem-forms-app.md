---
title: AEM Forms應用程式
seo-title: AEM Forms app
description: AEM Forms應用程式可讓您的欄位工作者在其行動裝置上使用最適化表單。
seo-description: AEM Forms app enables your field workers to use adaptive forms on their mobile devices.
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
exl-id: 171754a2-1ba5-42dc-b6d2-3d730807cc31
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '2450'
ht-degree: 2%

---

# AEM Forms應用程式簡介 {#aem-forms-app}

## 概述 {#overview}

AEM Forms應用程式可讓您根據伺服器，在行動裝置上同步最適化表單、行動表單和表單集。 您可以定義的工作流程為 [OSGi上的Forms中心工作流程](/help/forms/using/aem-forms-workflow.md) 或JEE上的Forms工作流程。 例如，您經營一間銀行公司，並使用AEM Forms來管理客戶應用程式和通訊。 您的客戶填寫表單並提交以進行驗證。 如果您在行動裝置上啟用表單，您的客戶可以在AEM Forms應用程式中填寫表單。 您也可以在行動裝置上啟用驗證表單，以管理驗證工作流程。 您的欄位工作者可以將行動裝置傳送給客戶、驗證詳細資料並提交表單。 AEM Forms應用程式會與AEM Forms伺服器同步，並擷取為行動裝置啟用的表單。 如果應用程式離線，則會將資料儲存在本機。

客戶可透過Software Distribution取得AEM Forms應用程式的原始程式碼。 Software Distribution中的原始程式碼套件如下： `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

iOS、Android、Windows裝置支援AEM Forms應用程式。 您可以從Google Play安裝適用於Android的AEM Forms應用程式，從App Store安裝iOS，以及從Windows市集安裝Windows。

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ！[app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ！[microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

若要在iOS、Android或Windows裝置上安裝、自訂和發佈應用程式，請參閱 [自訂、建置和分發AEM Forms應用程式](#customize-build-distribute).

## 前提条件 {#prerequisites}

AEM Forms應用程式需要AEM Forms伺服器。 使用者可以轉譯您在AEM Forms伺服器中所建立的表單、填寫表單、儲存為草稿並提交表單。 應用程式會連線至伺服器，並從伺服器擷取已啟用的表單。 AEM Forms應用程式會與伺服器同步，一旦在應用程式中載入表單，使用者就可以離線工作。 如果應用程式離線，資料會儲存在裝置上，並在應用程式上線時與伺服器同步。

### 搭配使用AEM Forms工作流程的伺服器的AEM Forms應用程式 {#aem-forms-app-with-servers-using-aem-forms-workflow}

如果您有AEM Forms Workflow伺服器，則可在AEM Forms應用程式中將表單轉譯為任務。 例如，您經營一家銀行公司，而客戶填寫應用程式來使用您的服務。 應用程式是調適型表單，可接受客戶的資訊，並將其儲存為提交以供稽核。 管理員會檢閱應用程式，並將驗證請求轉寄給現場工作人員。 轉送的應用程式會在您的現場工作人員的應用程式中啟用驗證表單作為任務。 您的現場工作人員會將行動裝置帶給您的客戶，並驗證詳細資訊。

### 在OSGi上使用以Forms為中心的工作流程的伺服器的AEM Forms應用程式 {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

如果您有AEM Forms伺服器，可以將最適化表單轉譯為AEM收件匣應用程式，以及轉譯AEM Forms應用程式中的工作。 例如，您經營一家銀行公司，而客戶填寫應用程式來使用您的服務。 應用程式與最適化表單相關聯，該表單接受來自客戶的資訊，並將其儲存為提交以供稽核。 管理員複查任務並核准現場工作人員的驗證請求。 您的現場工作人員會將行動裝置帶給您的客戶，並驗證詳細資訊。

### 獨立表單或AEM Forms應用程式(含無AEM Forms工作流程的伺服器) {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

未使用AEM Forms Workflow的AEM Forms伺服器是OSGi上的AEM Forms，或是獨立行動表單或最適化表單。 AEM Forms應用程式可搭配您的AEM Forms實作用於 [osgi](/help/sites-deploying/configuring-osgi.md). 您為AEM Forms應用程式啟用和發佈的Forms可在您的應用程式中使用。

這些表單會從您的應用程式下載，並可離線使用。 例如，您正在執行銀行公司，而客戶在您的網站上填寫應用程式。 應用程式是調適型表單，可接受客戶的資訊，並將其儲存以供稽核。 管理員會稽核表單，並在AEM編寫執行個體中建立驗證表單。 管理員可讓表單與AEM Forms應用程式同步，並予以發佈。 如果AEM Forms應用程式中有驗證表單，您的欄位代理程式可使用行動裝置來驗證客戶的詳細資料。 行動裝置與伺服器同步，且驗證表單已載入應用程式中。 您的欄位代理可以造訪您的客戶、驗證詳細資訊、將資料儲存為草稿，或提交驗證表單。 只要應用程式上線，表單就會與伺服器同步。

若要在AEM Forms應用程式中同步處理您的表單：

1. 在製作執行個體中，選取表單，然後按一下 **[!UICONTROL 檢視屬性]**.

1. 在屬性頁面中，按一下 **[!UICONTROL 進階]**.
1. 在進階下，啟用選項： **[!UICONTROL 與AEM Forms應用程式同步]** 並點選 **[!UICONTROL 儲存]**.

發佈表單時，應用程式會與伺服器同步並擷取表單。 若要同步處理多個表單，請在作者執行個體中，選取表單管理員中的多個表單，然後點選 **[!UICONTROL 與AEM Forms應用程式同步]**.

## 行動裝置支援 {#mobile-device-support}

另請參閱 [AEM Forms應用程式（先前稱為行動工作區）](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## AEM Forms應用程式的主要功能 {#key-features-of-aem-forms-app}

### 具有AEM Forms伺服器的AEM Forms應用程式 {#aem-forms-app-with-aem-forms-servers}

您可以將應用程式與AEM Forms伺服器同步，並可在行動裝置上使用表單。

使用AEM Forms Workflow伺服器時，表單可以與Workbench程式和AEM收件匣應用程式中的起點相關聯。 AEM收件匣應用程式可以有與其關聯的最適化表單。 起點可以有一個最適化表單、HTML5表單或與之關聯的表單集。 起點可作為任務提交，或任務可儲存為草稿。 如需AEM收件匣應用程式與起點之間差異的詳細資訊，請參閱 [表單中心AEM工作流程在OSGi和AEM Forms JEE工作流程上的動作和功能](capabilities-osgi-jee-workflows.md).

在沒有AEM Forms工作流程的AEM Forms伺服器上，啟用於應用程式中同步的表單會在AEM Forms應用程式中轉譯。 Forms可在應用程式的Forms標籤中使用，可提交或儲存為草稿。 應用程式支援最適化表單和行動表單。

1. **將任務或表單儲存為草稿**

   另存為草稿選項可儲存任務或表單的快照，以及相關表單中填寫的資料和附加的檔案。 草稿會儲存至行動裝置並與AEM Forms伺服器同步，以供稍後擷取。

   另請參閱 [將任務或表單儲存為草稿](/help/forms/using/save-as-draft.md).

1. **將表單另存為範本**

   有時，使用者填寫表單時，對幾個欄位的輸入會維持不變。 對於這類例項，您可以填寫每個例項中需要相同值的欄位，並將表單或草稿另存為範本。 現在，每次您建立範本的執行個體時，指定的欄位已填入範本中指定的值。 它有助於您節省填寫表單所需的時間和精力。

   另請參閱 [將表單另存為範本](/help/forms/using/save-forms-and-start-points-as-templates.md).

### 使用任務和表單 {#working-with-tasks-and-forms}

您可以將應用程式與AEM Forms Workflow伺服器同步，並可在行動裝置上處理任務和表單。

行動裝置上的任務包含最適化表單、HTML5表單或表單集，也可以包含附件和 [摘要URL](/help/forms/using/getting-task-variables-summary-url.md). 依預設，指派給您的任務會放在 **[!UICONTROL 任務]** 資料夾。 處理任務時，您可以變更任務並在AEM Forms伺服器上儲存任務的草稿副本。

行動裝置上的表單可以是最適化表單或行動表單。 Forms資料夾中提供已在表單應用程式中啟用同步的Forms。 您可以同步在AEM Forms伺服器中啟用的表單，而無需AEM Forms工作流程(OSGi上的AEM Forms)。

请参阅：

* [開啟任務](/help/forms/using/open-task.md)
* [使用表單](/help/forms/using/working-with-form.md)

### 離線工作 {#working-offline}

您可以在離線模式下使用行動裝置。 即使沒有網路連線，您也可以登入應用程式，並可處理上次連線時與裝置同步處理的所有表單。 如需如何同步化表單的詳細資訊，請參閱 [同步應用程式](/help/forms/using/sync-app.md). 如果您選擇同步化與表單相關聯的附件，您也可以在離線模式下開啟附件。 您可以在離線模式中編輯表單、新增註解，以及提交或儲存表單。 下次您上線時，表單會與AEM Forms伺服器同步。

如需詳細資訊，請參閱 [在離線模式下工作](/help/forms/using/work-offline-mode.md).

### 新增註解 {#adding-annotations}

您可以將下列附件新增至行動裝置上的表單

* **附註** — 您可以使用「附註」功能，在表單中新增手繪塗鴉或文字附註。 如需詳細資訊，請參閱 [新增附註](/help/forms/using/add-attachments.md#adding-a-note).

* **圖片**- AEM Forms應用程式包含的一項功能會使用相機功能或行動裝置的收藏館。 使用像片附件，您可以新增像片及相關的表單。 如需詳細資訊，請參閱 [新增像片](/help/forms/using/add-attachments.md#adding-a-photograph).

### 自動儲存 {#autosave}

當使用者在AEM Forms應用程式中輸入資料時，自動儲存功能會定期儲存。 AEM Forms應用程式中的自動儲存功能可協助您避免因電池電量不足等狀況而關閉應用程式時造成資料遺失。

另請參閱 [在AEM Forms應用程式中使用自動儲存](/help/forms/using/autosave-data-app.md).

## AEM收件匣和AEM Forms應用程式功能之間的差異 {#differences-between-aem-inbox-and-aem-forms-app-features}

啟動以Forms為中心的工作流程有兩個顯著的方法，就是 [AEM收件匣](/help/forms/using/manage-applications-inbox.md) 和AEM Forms應用程式。 但AEM收件匣和AEM Forms應用程式的功能有所不同。 AEM收件匣僅適用於 [以Forms為中心的工作流程](/help/forms/using/aem-forms-workflow.md) 而AEM Forms應用程式可搭配以Forms為中心的工作流程及程式管理運作。 如需AEM收件匣與AEM Forms應用程式功能之間差異的詳細資訊，請參閱 [表單中心AEM工作流程在OSGi和AEM Forms JEE工作流程上的動作和功能](capabilities-osgi-jee-workflows.md).

## 支援的表單 {#supported-forms}

AEM Forms應用程式支援的表單型別：

### 自适应表单 {#adaptive-form}

AEM Forms應用程式支援動態調整以符合使用者輸入的最適化表單。 也支援延遲載入的最適化表單。

### 行動表單 {#mobile-form}

您可以在AEM Forms中建立行動裝置的表單。 行動表單會在行動裝置中呈現為HTML表單，且會根據顯示裝置進行調整。

### 表单集 {#formset}

使用表單集，可以分組與服務或流程相關的多個表單，以自動化業務流程並向終端使用者呈現。 在這種情況下，使用者可以完整填寫整個集合，而且不需要檔案、提交和追蹤個別表單或流程。

>[!NOTE]
>
>需要AEM Forms工作流程(JEE上的AEM Forms)。

## AEM Forms應用程式的運作方式 {#how-aem-forms-app-works}

AEM Forms應用程式為現場工作人員提供行動解決方案，以處理指派給他們的表單。 應用程式會從伺服器快取完整資料，並將所有工作儲存在本機，以提供有效率的使用者體驗。 磁碟中的資料會透過即時同步更新傳送至伺服器。

AEM Forms應用程式是以PhoneGap 5.0為基礎的應用程式，其中骨幹模式可透過檢視有效用於呈現儲存在模式中的資料。 所有原生作業都是透過PhoneGap外掛程式執行。

## 自訂、建置和分發AEM Forms應用程式 {#customize-build-distribute}

>[!NOTE]
>
>僅適用於使用AEM Forms應用程式原始碼來建立應用程式時。

AEM Forms應用程式可輕鬆根據組織特定需求自訂。 應用程式的原始碼會與AEM Forms一併提供。 您可以變更原始程式碼，並建立自己的行動工作者解決方案。 您也可以使用自己的企業金鑰簽署應用程式。

### 自定义 {#customize}

您可以針對下列專案自訂您的應用程式：

**品牌化**：變更應用程式圖示、應用程式名稱、啟動影像和AEM Forms應用程式中的頁面。 您也可以變更文字，將特定地區的應用程式當地語系化。 如需品牌化AEM Forms應用程式的詳細資訊，請參閱 [品牌自訂](/help/forms/using/branding-customization.md).

**主題**：在AEM Forms應用程式使用者介面中變更樣式，例如顏色、字型和間距。 如需詳細資訊，請參閱 [佈景主題自訂](/help/forms/using/theme-customization.md).

**手勢**：變更手勢，例如在AEM Forms應用程式使用者介面中向右撥和向左撥動。 如需詳細資訊，請參閱 [手勢自訂](/help/forms/using/gesture-customization.md).

如需設定AEM Forms應用程式專案以進行自訂的詳細資訊，請參閱：

* [設定AEM Forms應用程式的環境](/help/forms/using/setup-environment-mobile-workspace.md)
* [設定Visual Studio專案並建置Windows應用程式](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [設定Xcode專案並建置iOS應用程式](/help/forms/using/setup-xcode-project-build-installer.md)
* [設定Eclipse專案並建置Android應用程式](/help/forms/using/setup-eclipse-project-build-installer.md)

### 建置和散佈 {#build-and-distribute}

AEM Forms應用程式的原始程式碼可從 `adobe-lc-mobileworkspace-src.zip` 這可作為Software Distribution上AEM Forms應用程式來源套件的一部分。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 區段：
   1. 選取 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 下拉式清單。
   2. 選取套件的版本和型別。 您也可以使用 **[!UICONTROL 搜尋下載]** 篩選結果的選項。
1. 點選適用於您的作業系統的套件名稱，然後選取 **[!UICONTROL 接受EULA條款]**，然後點選 **[!UICONTROL 下載]**.
1. 打开[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 選取套件並按一下 **[!UICONTROL 安裝]**.

**適用於iOS**：

如需如何建立iOS應用程式(.ipa)的詳細資訊，請參閱 [設定Xcode專案並建置iOS應用程式](/help/forms/using/setup-xcode-project-build-installer.md).

如需如何使用布建設定檔簽署AEM Forms應用程式的詳細資訊，請參閱 [iOS程式碼簽署設定、處理和疑難排解](https://developer.apple.com/support/code-signing/).

**適用於Android**：

如需如何建立Android應用程式(.apk)的詳細資訊，請參閱 [設定Eclipse專案並建置Android應用程式](/help/forms/using/setup-eclipse-project-build-installer.md).

如需如何簽署AEM Forms應用程式的詳細資訊，請參閱 [簽署您的應用程式](https://developer.android.com/tools/publishing/app-signing.html).

**適用於Windows**：

如需有關如何建立Windows應用程式(.appx)的詳細資訊，請參閱 [設定Visual Studio專案並建置Windows應用程式](/help/forms/using/setup-visual-studio-project-build-installer.md).

如需如何透過MDM發佈應用程式的詳細資訊，請參閱 [發佈AEM Forms應用程式](/help/forms/using/distribute-mobile-workspace-app.md). 透過MDM發佈的應用程式僅適用於iOS和Android。

## Recommendations可將Mobile Workspace升級至AEM Forms應用程式 {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

如果您要升級至最新版AEM Forms應用程式，請務必詳閱下列要點：

* **如果您從Android上的Play Store安裝舊版應用程式**
您可以直接從Play Store升級應用程式。

* **如果使用原始程式碼建置和安裝應用程式的舊版(適用於iOS和Android)**：

   安裝新應用程式之前，請先將所有資料與AEM Forms伺服器同步。 資料同步後，請解除安裝舊版應用程式，然後安裝新應用程式。
