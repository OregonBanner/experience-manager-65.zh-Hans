---
title: 升級程式碼和自訂
seo-title: Upgrading Code and Customizations
description: 進一步瞭解如何在AEM中升級自訂程式碼。
seo-description: Learn more about upgrading custom code in AEM.
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: a36a310d-5943-4ff5-8ba9-50eaedda98c5
source-git-commit: a296e459461973fc2dbd0641c6fdda1d89d8d524
workflow-type: tm+mt
source-wordcount: '2115'
ht-degree: 0%

---

# 升級程式碼和自訂{#upgrading-code-and-customizations}

規劃升級時，必須調查並處理實作的下列領域。

* [升級程式碼基底](#upgrade-code-base)
* [與6.5存放庫結構一致](#align-repository-structure)
* [AEM自訂](#aem-customizations)
* [測試程式](#testing-procedure)

## 概述 {#overview}

1. **模式偵測器**  — 執行模式偵測器，如升級計畫中所述，並詳見 [此頁面](/help/sites-deploying/pattern-detector.md). 您會收到模式偵測器報告，其中除了AEM目標版本中無法使用的API/套件組合，還包含必須解決之領域的詳細資訊。 「模式偵測」報表可讓您指出程式碼中的任何不相容專案。 如果不存在任何專案，表示您的部署已經與6.5相容。 您仍然可以選擇使用6.5功能進行新開發，但並非只是為了維護相容性。 如果回報不相容，您可以選擇在相容模式中執行，並延遲開發新的6.5功能或相容性。 或者，您可以在升級後決定進行開發，然後移至步驟2。 另請參閱 [AEM 6.5的回溯相容性](/help/sites-deploying/backward-compatibility.md) 以取得更多詳細資料。

1. **開發6.5適用的程式碼基底** — 為Target版本的程式碼基底建立專用分支或存放庫。 使用升級前相容性中的資訊來規劃要更新的程式碼區域。
1. **使用6.5 Uber jar編譯** — 更新程式碼基底POM以指向6.5 Uber jar並據此編譯程式碼。
1. **更新AEM自訂*** - *AEM的任何自訂或擴充功能應更新/驗證以在6.5中運作，並新增至6.5程式碼基底。 包含UI搜尋Forms、資產自訂、使用/mnt/overlay的任何內容

1. **部署至6.5環境** - AEM 6.5 (Author + Publish)的乾淨例項應在Dev/QA環境中顯示。 應部署更新的程式碼庫和代表性內容範例（來自目前生產環境）。
1. **QA驗證和錯誤修正** - QA應在6.5的Author和Publish執行個體上驗證應用程式。發現的任何錯誤都應修正並認可至6.5程式碼基底。 視需要重複開發週期，直到修復所有錯誤為止。

在繼續升級之前，您應該要有已針對AEM目標版本進行完整測試的穩定應用程式程式碼基底。 根據測試中所做的觀察，可能有方法來最佳化自訂程式碼。 例如，其中可能包括重構程式碼以避免周遊存放庫、自訂索引以最佳化搜尋，或在JCR中使用無序節點等。

除了選擇性地升級您的程式碼基底和自訂以與新的AEM版本搭配使用外，6.5還可以利用回溯相容性功能更有效率地管理您的自訂，如中所述 [此頁面](/help/sites-deploying/backward-compatibility.md).

如上所述及下圖所示，執行 [模式偵測器](/help/sites-deploying/pattern-detector.md) 在第一個步驟中，可以幫助您評估升級的整體複雜性。 它也可以協助您決定要在相容性模式下執行，或更新自訂以使用所有新的AEM 6.5功能。 請參閱 [AEM 6.5的回溯相容性](/help/sites-deploying/backward-compatibility.md) 頁面，以取得更多詳細資料。
[ ![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## 升級程式碼基底 {#upgrade-code-base}

### 在版本控制中為6.5程式碼建立專用分支 {#create-a-dedicated-branch-for-6.5-code-in-version-control}

應使用某種形式的版本控制來管理您的AEM實作所需的所有程式碼和設定。 應建立版本控制中的專用分支，以管理目標AEM版本中程式碼庫所需的任何變更。 此分支管理針對AEM目標版本的反複程式碼庫測試和後續錯誤修正。

### 更新AEM Uber Jar版本 {#update-the-aem-uber-jar-version}

AEM Uber jar包含所有AEM API，作為您Maven專案的 `pom.xml`. 最佳實務一律會將Uber Jar納入為單一相依性，而非納入個別AEM API相依性。 升級程式碼基底時，請變更Uber Jar的版本以指向目標AEM版本。 如果您的專案是在Uber Jar存在之前的AEM版本上開發，請移除所有個別AEM API相依性。 以AEM目標版本的Uber Jar的單一包含取代它們。 針對新版Uber Jar重新編譯程式碼基底。 更新任何過時的API或方法，使其與AEM的目標版本相容。

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### 逐步停止使用管理資源解析程式 {#phase-out-use-of-administrative-resource-resolver}

透過使用管理工作階段 `SlingRepository.loginAdministrative()` 和 `ResourceResolverFactory.getAdministrativeResourceResolver()` 在AEM 6.0之前的程式碼基底中普遍存在。由於這些方法提供的存取層級過於廣泛，因此已基於安全性原因而遭到取代。 [在未來Sling版本中，將移除這些方法](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). 強烈建議您重構任何程式碼，以改用服務使用者。 有關服務使用者與的更多資訊 [如何逐步淘汰管理工作階段可在此處找到](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### 查詢和Oak索引 {#queries-and-oak-indexes}

升級程式碼庫時，必須對程式碼庫中任何查詢的使用進行徹底測試。 對於從Jackrabbit 2 (6.0以前的AEM版本)升級的客戶，這項測試尤其重要，因為Oak不會自動索引內容且應建立自訂索引。 如果從AEM 6.x版本升級，現成可用的Oak索引定義可能已變更，並且可能影響現有查詢。

下列工具可用來分析和檢查查詢效能：

* [AEM Index Tools](/help/sites-deploying/queries-and-indexing.md)

* [作業診斷工具 — 查詢效能](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

<!-- URL is 404 as of 04/24/23; commenting out * [Oak Utils](https://oakutils.appspot.com/). This is an open source tool that is not maintained by Adobe. -->

### 傳統UI編寫 {#classic-ui-authoring}

傳統UI編寫仍可在AEM 6.5中使用，但已過時。 如需詳細資訊，請參閱 [此處](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). 如果您的應用程式在傳統UI作者環境中執行，建議升級至AEM 6.5並繼續使用傳統UI。 移轉至Touch UI可規劃為獨立專案，以透過數個開發週期完成。 若要在AEM 6.5中使用傳統UI，必須將數個OSGi設定認可至程式碼基底。 如需如何進行設定的詳細資訊，請參閱 [此處](/help/sites-administering/enable-classic-ui.md).

## 與6.5存放庫結構一致 {#align-repository-structure}

為了更輕鬆升級並確保在升級期間不會覆寫設定，存放庫在6.4中進行了重組，以將內容與設定分開。

因此，必須移動數個設定，使其不再位於下 `/etc` 一如既往。 若要檢閱更新至AEM 6.4中必須檢閱和解決的整套存放庫重組問題，請參閱 [AEM 6.4中的存放庫重組](/help/sites-deploying/repository-restructuring.md).

## AEM自訂  {#aem-customizations}

必須識別AEM來源版本中AEM製作環境的所有自訂。 識別之後，建議將每個自訂內容儲存在版本控制中，或至少備份為內容套件的一部分。 所有自訂都應在生產升級之前，在執行目標AEM版本的QA或測試環境中部署及驗證。

### 一般覆蓋 {#overlays-in-general}

常見的作法是將AEM開箱即用的功能擴充，方法是使用/apps下的其他節點覆蓋/libs下的節點和/或檔案。 您應在版本控制中追蹤這些覆蓋圖，並針對AEM的目標版本進行測試。 如果檔案（例如JS、JSP、HTL）重疊，Adobe建議您留下註解，說明已增強哪些功能，以便在AEM的目標版本上更輕鬆地進行回歸測試。 一般覆蓋圖的更多資訊可以找到 [此處](/help/sites-developing/overlays.md). 特定AEM覆蓋圖的指示見下文。

### 升級自訂搜尋Forms {#upgrading-custom-search-forms}

自訂搜尋Facet在升級後需要一些手動調整才能正常運作。 如需詳細資訊，請參閱 [升級自訂搜尋Forms](/help/sites-deploying/upgrading-custom-search-forms.md).

### Assets UI自訂 {#assets-ui-customizations}

>[!NOTE]
>
>只有從AEM 6.2之前的版本升級時，才需要執行此程式。

具有自訂Assets部署的執行個體必須為升級做好準備。 此動作是必要的，可確保所有自訂內容與新的6.4節點結構相容。

您可以執行下列動作，為Assets UI準備自訂：

1. 在要升級的執行個體上，前往以下位置開啟CRXDE Lite： *https://server:port/crx/de/index.jsp*

1. 前往下列節點：

   * `/apps/dam/content`

1. 將內容節點重新命名為 **content_backup** 在視窗左側的瀏覽器窗格上按一下滑鼠右鍵，然後選擇 **重新命名**.

1. 重新命名節點後，在下方建立名為內容的節點 `/apps/dam` 已命名 **內容** 並將其節點型別設為 **sling：Folder**.

1. 移動的所有子節點 **content_backup** 在新建立的內容節點中，以滑鼠右鍵按一下瀏覽器窗格中的每個子節點，然後選取 **移動**.

1. 刪除 **content_backup** 節點。

1. 下方更新的節點 `/apps/dam` 具有正確的節點型別 `sling:Folder` 理想情況下，應儲存至版本控制中，並以程式碼庫部署，或至少備份為內容套件。

### 產生現有資產的資產ID {#generating-asset-ids-for-existing-assets}

若要產生現有資產的資產ID，請在升級AEM執行個體以執行AEM 6.5時升級資產。若要啟用「 」，必須執行此步驟 [Assets深入分析功能](/help/assets/asset-insights.md). 如需詳細資訊，請參閱 [新增內嵌程式碼](/help/assets/use-page-tracker.md#add-embed-code).

若要升級資產，請在JMX主控台中設定「關聯資產ID」套件。 根據存放庫中的資產數量， `migrateAllAssets` 可能需要很長的時間。 Adobe的內部測試估計，TarMK上的125000資產大約需要1小時。

![1487758945977](assets/1487758945977.png)

如果您需要整個資產的子集的資產ID，請使用 `migrateAssetsAtPath` API。

若為所有其他目的，請使用 `migrateAllAssets()` API。

### InDesign指令碼自訂 {#indesign-script-customizations}

Adobe建議您將自訂指令碼放在 `/apps/settings/dam/indesign/scripts` 位置。 有關InDesign指令碼自訂的更多資訊可以找到 [此處](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### 正在復原ContextHub設定 {#recovering-contexthub-configurations}

ContextHub設定會受升級影響。 有關如何復原現有ContextHub設定的說明，請參閱 [此處](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading).

### 工作流程自訂 {#workflow-customizations}

通常的做法是編輯現成的工作流程，以新增或移除不需要的功能。 自訂的常見工作流程為 [!UICONTROL DAM更新資產] 工作流程。 自訂實作所需的所有工作流程都應備份並儲存在版本控制中，因為升級期間可能會覆寫這些工作流程。

### 可编辑模板 {#editable-templates}

>[!NOTE]
>
>只有在使用AEM 6.2的可編輯範本進行Sites升級時，才需要執行此程式

可編輯範本的結構在AEM 6.2和6.3之間變更。如果您要從6.2或更舊版本升級，而且您的網站內容是使用可編輯的範本建立的，則必須使用 [回應式節點清理工具](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). 此工具旨在執行 **晚於** 清理內容的升級。 在「作者」和「發佈」層級上執行。

### CUG實作變更 {#cug-implementation-changes}

封閉式使用者群組的實作已大幅變更，以解決舊版AEM的效能和擴充性限制。 6.3已棄用舊版CUG，新實作僅支援觸控式UI。 如果您是從6.2版或更舊版本升級，請查閱移轉至新CUG實作的指示 [此處](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## 測試程式 {#testing-procedure}

應針對測試升級準備完整的測試計畫。 測試升級的程式碼基底和應用程式必須先在較低的環境中完成。 找到的任何錯誤都應透過反複的方式進行修正，直到程式碼庫穩定為止，只有在穩定後才會升級較高層級的環境。

### 測試升級程式 {#testing-the-upgrade-procedure}

這裡概述的升級程式應在開發和QA環境中進行測試，如您的自訂執行手冊中所述(請參閱 [規劃升級](/help/sites-deploying/upgrade-planning.md))。 升級程式應重複執行，直到所有步驟都記錄在升級執行手冊中且升級過程順利進行。

### 實作測試區域  {#implementation-test-areas-}

以下是任何AEM實作的重要領域，在環境升級且部署升級後的程式碼庫後，這些領域應包含在測試計畫中。

<table>
 <tbody>
  <tr>
   <td><strong>功能測試區域</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>已發佈的網站</td>
   <td>在發佈層級上測試AEM實作和相關聯的程式碼<br /> 透過Dispatcher。 應包含頁面更新的條件和<br /> 快取失效。</td>
  </tr>
  <tr>
   <td>创作</td>
   <td>在製作層級上測試AEM實作和相關聯的程式碼。 應包括頁面、元件製作和對話方塊。</td>
  </tr>
  <tr>
   <td>與Experience Cloud解決方案整合</td>
   <td>驗證與Analytics、DTM和Target等產品的整合。</td>
  </tr>
  <tr>
   <td>與協力廠商系統整合</td>
   <td>驗證「作者」和「發佈」層級上的任何協力廠商整合。</td>
  </tr>
  <tr>
   <td>驗證、安全性和許可權</td>
   <td>任何驗證機制（例如LDAP/SAML）都應經過驗證。<br /> 應在「作者」和「發佈」上測試許可權和群組<br /> 層級。</td>
  </tr>
  <tr>
   <td>查詢</td>
   <td>自訂索引和查詢應該與查詢效能一起測試。</td>
  </tr>
  <tr>
   <td>UI自訂</td>
   <td>製作環境中AEM UI的任何擴充功能或自訂專案。</td>
  </tr>
  <tr>
   <td>工作流</td>
   <td>自訂和/或現成可用的工作流程和功能。</td>
  </tr>
  <tr>
   <td>性能测试</td>
   <td>載入測試應在模擬真實世界情境的Author和Publish層上執行。</td>
  </tr>
 </tbody>
</table>

### 記錄測試計畫和結果 {#document-test-plan-and-results}

應建立涵蓋上述實作測試區域的測試計畫。 通常，依作者和發佈工作清單來區分測試計畫是可行的做法。 此測試計畫應在升級生產環境之前在開發、QA和中繼環境上執行。 測試結果和效能量度應在較低層級環境中擷取，以便在升級中繼和生產環境時提供比較。
