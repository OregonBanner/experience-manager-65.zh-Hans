---
title: 版本注意事項 [!DNL Adobe Experience Manager] 6.5
description: 尋找版本資訊、新增功能、安裝作法和詳細的變更清單 [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: fc7d3727-7cd4-47a4-8e75-840f9f9c0e62
source-git-commit: a95255594ec03c152cd96df48597ced5fce4b315
workflow-type: tm+mt
source-wordcount: '2972'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack發行說明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=WRAZ43&nav=MTVfezk2OTJDQTNFLUI4QTQtNDY2RS05NEVCLUQ5QjcyNEVENkJDNn0 -->

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.16.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | Service Pack發行 |
| 日期 | 2023年2月23日星期四 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]be/packages/cq650/servicepack/aem-service-pkg-6.5.16.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 包含在 [!DNL Experience Manager] 6.5.16.0 {#what-is-included-in-aem-6516}

[!DNL Experience Manager] 6.5.16.0包括自2019年4月6.5版首次發行以來所推出的新功能、客戶要求的重要增強功能、錯誤修正，以及效能、穩定性和安全性改善專案。 [安裝此Service Pack](#install) 於 [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Dynamic Media的一項主要改善專案如下：

新通訊協定DASH (Dynamic Adaptive Streaming over HTTP)支援已推出，適用於Dynamic Media視訊傳送（透過CMAF）中的最適化位元速率串流 [通用媒體應用程式格式] 已啟用)。

* 自适应流式处理 (DASH/HLS) 可确保最终用户获得更出色的视频观看体验.
* DASH 是自适应视频流式处理的国际标准协议，在业界得到广泛应用.
* 現在提交支援票證即可使用。

另請參閱 [在您的帳戶上啟用DASH](/help/assets/video.md#enable-dash).

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6516}

* 連線資產：當您在遠端DAM上啟用影像的智慧型裁切選項、將影像上傳至資料夾，並將資料夾同步至本機站台時，該資料夾不會在本機Sites部署上開啟。 (NPR-39912)
* 依名稱排序集合時，清單檢視無法正常運作(ASSETS-19401)
* 將大型媒體檔案(JPEG)上傳至「集合」時，Experience Manager會停止回應。 (ASSETS-19387)
* 在內容樹窗格中，顯示的資產名稱不正確，因為資產位置未正確呈現。 (ASSETS-18870)
* 使用連結共用集合時，URL中的資料在卡片檢視和清單檢視之間的隨機排列不相符。 (ASSETS-18758)
* 當您在資料夾型別上使用篩選器執行Omnisearch時，搜尋結果不一致。 (ASSETS-18227)
* 此 `dam:size` 屬性未在XMP回寫後更新，這會導致從傳回的資訊不正確 `/platform/path/to/asset.jpg;resource=metadata` API。 (ASSETS-17631)
* 所有Experience Manager執行個體上未關閉的資源解析器。 (ASSETS-16904)
* 無法為資產建立版本，即使您被指派了 `create` 和 `modify` 許可權。 (ASSETS-15956)
* 此 `move` 將資產從一個點移動到另一個點時，按鈕會隨機停用。 (ASSETS-14889)
* 熒幕助讀程式無法識別標題，因為標題標籤內的文字並未定義，而是定義為一般文字。 (ASSETS-6924)
* 影像下方的替代文字不是強制性的，但影像下顯示的文字是重複的 `Type` 屬性。 (ASSETS-6915)


## [!DNL Assets] - [!DNL Dynamic Media] {#dm-6516}

* 表單元素不包含標籤。 使用NVDA和JAWS等熒幕閱讀程式時，表單標籤資訊無法正確宣告。 (CQ-4344078)
* 下拉式清單在 `Escape` 鍵用於鍵盤。 (CQ-4344077)
* 在提供無效輸入後針對內嵌錯誤建議顯示的資訊圖示（字母「i」）無法使用鍵盤存取。 (CQ-4344076)
* `getManifestURI` 由於JCR屬性被讀取為，所以傳回null `toString` 而非 `getString`. (ASSETS-18674)
* SmartCrop視訊元件的行為不正確。 元件正在執行播放而非串流，且VTT呼叫失敗，產生404錯誤。 (ASSETS-18468)
* 選取 **[!UICONTROL 屬性]** 在資產的Viewer頁面上導致Null指標例外狀況。 (ASSETS-18420)
* [!DNL Experience Manager] DASH串流的使用者介面變更，包括下列專案：
   * 在視訊設定檔編輯器中具有可見的CMAF （通用媒體應用程式格式）欄位。
   * 讓視訊上傳程式傳送CMAF標幟。
   * 選項 **[!UICONTROL 自動]**， **[!UICONTROL hls]**、和 **[!UICONTROL 虛線]** 現在於檢視器預設集編輯器的「播放」下拉式清單中提供 **[!UICONTROL 行為]** 標籤。
(ASSETS-17428)
* 在「導覽」中，當您選取 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]** > **[!UICONTROL 建立]** > **[!UICONTROL 傳送集]**，圖片圖示會與「投影片1」文字字串重疊。 (ASSETS-18578)
* 已取消發佈的資產會再次發佈。 (ASSETS-16428)
* Experience Manager作者因載入問題而關閉，提示建立綜合警報。 (ASSETS-15937)
* 在Dynamic Media「一般設定」頁面中，出現未轉譯的錯誤訊息 `Failed to fetch data` 出現。 (ASSETS-15617)

## [!DNL Forms] {#forms-6516}

### [!DNL Forms] 主要功能 {#forms-features-6516}

* [Headless最適化Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 讓您的開發人員能夠建立、發佈和管理互動式表單，這些表單可透過API存取及互動，而不是透過傳統的圖形使用者介面。

* [最適化Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) 是一組24個開放原始碼、符合BEM規範的元件，建立在Adobe Experience Manager WCM核心元件的基礎上。 這些元件是開放原始碼，讓開發人員能夠輕鬆自訂和擴充這些元件，以符合其組織的特定需求。 任何具備自訂技能的人 [WCM核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html?lang=en) 可輕鬆自訂這些元件並設定其樣式。

* OSGi上的Reader擴充功能現在提供個別選項，可啟用PDF的匯入和匯出使用許可權，以便在Adobe Acrobat Reader中匯入或匯出資料。 (NPR-39909)

### [!DNL Forms] 修复 {#forms-fixes-6516}

* 使用 **指派任務** 步驟針對指派的任務傳送通知，會傳送兩封電子郵件給指派的個人，而非一封。 (NPR-40078)
* 當使用者隱藏表格標題時，會導致先前設定的欄寬取消設定，並且所有欄都保留相同的寬度。 (NPR-40063)
* 如果您將管理員使用者的預設密碼從 `admin`，同時執行 `Prepare Adobe Experience Manager Server For DSC deployment` 檢查AEM Forms JEE Service Pack是否失敗。 (NPR-40062)、(NPR-39387)
* OutputService和AssemblerService API無法將PDF表單轉換為PDF/A。(NPR-39990)
* AssemblerService無法將PDF轉換為PDF/A。當使用者將PDF轉換為PDF/A時，出現以下錯誤： `PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Summary" ignoreUnusedResources="true" allowCertificationSignatures="true"> <Violation count="6" key="PDFA_CS_001_NOT_DEVICE_INDEPENDENT" description="ColorSpace is not device independent`. (NPR-39956)
* 當GuideSubmitServlet API呼叫的伺服器端驗證失敗時，傳送給使用者端的回應中不會傳回錯誤。 (NPR-39925)
* 在Windows伺服器上升級至AEM 6.5.15.0 Service Pack後，使用者會遇到多個錯誤訊息，且電子郵件服務無法運作。(NPR-39919)
* 當您升級至AEM 6.5.14.0並使用importData服務將PDF與XML合併時，會發生下列錯誤： `Caused by: java.lang.NoSuchMethodError: com.adobe.xfa.form.FormModel.isXFABarcode(Lcom/adobe/xfa/Node;)Ljava/lang/Boolean`.(NPR-39807)
* 使用者安裝時 **Document Security Office** 擴充功能時，會發生下列問題：
   * Microsoft® Excel經常當機。
   * 開啟安全保護檔案時， **Document Security Office** 未偵測到擴充功能已安裝在電腦上。 指示使用者下載並安裝安全性擴充功能。 (NPR-39768)
* 使用者升級至AEM 6.5.15.0 Service Pack後，PostScript轉換為Pdf無法運作。 (NPR-39765)、(NPR-39764)
* 當使用者嘗試在開啟最適化表單後開啟導覽畫面時，它會失敗並出現NullPointer例外狀況：`[172.17.0.1[1662032923933]GET/libs/fd/af/content/editors/form/tour/content.htmlHTTP/1.1]com.day.cq.wcm.core.impl.WCMDebugFilterException:org.apache.sling.api.scripting.ScriptEvaluationException:"` (NPR-39654)
* 在Windows中，當使用者啟用高對比黑色設定時，HTML5 Forms內容在瀏覽器中呈現為HTML預覽時會變得不清楚。 (NPR-39018)
* 當使用者嘗試新增中繼資料時，「草稿」和「提交」元件的「儲存」按鈕變得無法運作。(CQ-4349601)
* 升級至AEM 6.5.15.0 Service Pack後，相對URL的重新導向無法在視覺化編輯器中運作。 (NPR-39947)
* 當使用者升級至AEM 6.5.15.0 Service Pack時，重新導向停止搭配Internet Explorer使用。 (CQ-4351745)
* 使用者升級至AEM 6.5.15.0 Service Pack後，無法辨識HTML標題標籤。 標題標籤的HTML碼會在HTML表單中顯示為文字。 (NPR-39915)
* 當使用者嘗試提交最適化表單時，會發生型別預測錯誤： `ERROR [10.207.64.167 [1668589530607] POST /app/LS4/content/forms/af/revalidate/jcr:content/guideContainer.af.submit.jsp HTTP/1.1]`( NPR-39809)
* 當使用者預覽記錄檔案使用 **傳送電子郵件** 提交動作，無法正確顯示。 郵件範本內嵌在記錄檔案的預覽中。 (CQ-4352155)
* 當使用者在具有IE相容模式的Microsoft Edge瀏覽器上預覽最適化表單作為HTML時，該表單無法正確顯示。(CQ-4352216)
* 字典必須包含具有特殊字元（例如底線或連字型大小）的新地區設定，才能啟用翻譯。 (NPR-40088)

安裝AEM 6.5.16.0 Forms附加元件Service Pack後，客戶面臨下列問題。 因此，更新版本的 [AEM 6.5.16.0 Forms附加元件service pack - 6.0.914](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 已發行。 Adobe建議使用更新的Service Pack：
* base/java.util當使用者嘗試與表單 — 使用者群組中的使用者建立調適型表單時，選擇任何範本的選項不存在，並出現類似以下內容的錯誤：內部伺服器錯誤： java.lang.NullPointerException at com.adobe.aem.formsndocuments.servlet.ThemeClientLibraryDataSourceServlet.lambda$getThemeClientLibCategoryList$3(ThemeClientLibraryDataSourceServletServlet.java.java：76) at$java.stream.referencePipeline $1.accept(ReferencePipeline.java：176) at java.base/java.util.Iterator.forEachRemaining(Iterator.java：133) (FORMS-7629)
* 未儲存程式碼編輯器規則中所做的變更。(FORMS-7532)

## 集成 {#integrations-6516}

* 從Experience Manager6.5中移除AdobeSearch&amp;Promote程式碼和相依性。AdobeSearch&amp;Promote於2022年9月終止服務。 另請參閱 [AdobeSearch&amp;Promote服務終止公告](https://experienceleague.adobe.com/docs/discontinued/using/search-promote.html?lang=en). (NPR-39706)

## [!DNL Sites] {#sites-6516}

* 目前 `cq-wcm-core` 製作版本沒有POM。 (SITES-10983)
* 轉出預覽動作不應列出要建立的頁面。 (SITES-10355， CQ-4266213)
* 在MSM分離後轉出會重新建立分離的頁面。 (SITES-9841)
* 建立啟動已逾時；使用者必須在載入畫面上等候數分鐘，要求才會逾時。 (SITES-9051)
* 「轉出頁面」使用者介面顯示不存在的父頁面路徑。 您可以轉出包含成功訊息的頁面，但子頁面不會轉出，因為父頁面從一開始就沒有轉出。 (SITES-8621)

### [!DNL Sites] - 核心组件 {#sites-core-components-6516}

* 集中處理電子郵件頁面上的連結，因此不再需要模型自訂。 (SITES-9002)

### [!DNL Sites]  — 管理員使用者介面 {#sites-adminui-6516}

* 「CSV匯出」不會匯出所選頁面下的所有頁面。 (SITES-9390)

### [!DNL Sites] - [!DNL Content Fragments] {#sites-contentfragments-6516}

* 無法列印內容片段的JSON。 原因是當您開啟內容片段的「預覽」頁面時，無法產生GraphQL查詢。 (SITES-8619)
* 重新開啟內容片段模式編輯器時，全部 **[!UICONTROL 日期與時間]** 欄位會預設為「日期與時間」型別。 (SITES-8401)

### [!DNL Sites] - [!DNL Experience Fragments] {#sites-experiencefragments-6516}

* 您無法將體驗片段移動到另一個資料夾，即使範本列在允許的範本下。 (SITES-8601)
* (SITES-7989)


### [!DNL Sites] - 页面编辑器 {#sites-pageeditor-6516}

* 更新在SITES-8464中進行的資源解析器改善的相依性，其中在製作模式中轉譯的頁面建立了大量的 `TemplatedResourceImpl` 物件。 (SITES-9350)


## Sling {#sling-6516}

* Experience Manager在啟動時鎖定。 (NPR-39832)
* 當Experience Manager的版本儲存區中存在許多虛名路徑時，Experience Manager無法啟動。 (NPR-38955)


## 翻譯專案 {#translation-6516}

* 在 `MicrosoftTranslationServiceImpl`，查詢字串引數 `Category` 不正確。 (NPR-39828)
* 建立翻譯專案會顯示錯誤 *主版頁面資源不存在*；未建立翻譯專案。 (NPR-39762)
* 無法在使用人工翻譯聯結器的翻譯專案上設定到期日。 (NPR-39593)

## 用户界面 {#ui-6516}

* 當變更為較小的解析度時，日期選擇器不會顯示，且AM/PM選取範圍不會顯示或明顯變更。 (NPR-39948)
* 使用minify js （JavaScript最小化）時，由於剖析錯誤，其不會處理最小化。 (NPR-39650)
* 標籤欄位(`/libs/cq/gui/components/coral/common/form/tagfield`)與時間軸衝突。 (CQ-4350751)


## WCM {#wcm-6516}

* 轉出預覽動作不應列出要建立的頁面。 (CQ-4266213， SITES-10355)

## 工作流 {#workflow-6516}

* 從手動刪除可編輯的工作流程模型 `/conf` 離開延遲的執行階段模型例證，而不含可編輯的模型。 (CQ-4349365)


## 安裝 [!DNL Experience Manager] 6.5.16.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.16.0需要 [!DNL Experience Manager] 6.5.請參閱 [升級檔案](/help/sites-deploying/upgrade.md) 以取得詳細指示。 <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack下載專案可在Adobe取得 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* 在具有MongoDB和多個執行個體的部署上，安裝 [!DNL Experience Manager] 使用封裝管理器的其中一個Author執行個體上的6.5.16.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建議您移除或解除安裝 [!DNL Experience Manager] 6.5.16.0套件。 因此，在安裝套件之前，您應該建立 `crx-repository` 以備您需要復原時使用。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在上安裝Service Pack [!DNL Experience Manager] 6.5 {#install-service-pack}

1. 如果執行個體處於更新模式（執行個體是從舊版更新時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。

1. 安裝之前，請先拍攝快照或進行全新備份 [!DNL Experience Manager] 執行個體。

1. 下載Service Pack，從 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟封裝管理員，然後選取 **[!UICONTROL 上傳套裝]** 以上傳套件。 若要瞭解更多，請參閱 [封裝管理員](/help/sites-administering/package-manager.md).

1. 選取套件，然後選取 **[!UICONTROL 安裝]**.

1. 若要更新S3聯結器，請在安裝Service Pack後停止執行個體，以安裝資料夾中提供的新二進位檔案取代現有的聯結器，然後重新啟動執行個體。 另請參閱 [Amazon S3資料存放區](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>安裝Service Pack期間，套件管理員UI上的對話方塊有時會結束。 Adobe建議您在存取部署之前，先等待錯誤記錄穩定下來。 等待與更新程式套件組合解除安裝相關的特定記錄，再確認安裝成功。 此問題通常發生於 [!DNL Safari] 瀏覽器，但可能間歇性地在任何瀏覽器上發生。

**自动安装**

您可以使用兩種方法自動安裝 [!DNL Experience Manager] 6.5.16.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 將套件置於 `../crx-quickstart/install` 資料夾（當伺服器線上上可用時）。 套件會自動安裝。
* 使用 [套件管理器的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安裝巢狀套件。

>[!NOTE]
>
>Experience Manager6.5.16.0不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要瞭解經過認證可搭配此版本使用的平台，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md).

1. 產品資訊頁(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (6.5.16.0)` 在 [!UICONTROL 已安裝產品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi套件組合都可以 **[!UICONTROL 作用中]** 或 **[!UICONTROL 片段]** 在OSGi主控台中(使用Web主控台： `/system/console/bundles`)。

1. OSGi套件 `org.apache.jackrabbit.oak-core` 是1.22.14版或更新版本(使用Web主控台： `/system/console/bundles`)。 <!-- NPR-39939 for 6.5.16.0 --> <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安裝Service Pack for [!DNL Experience Manager] Forms {#install-aem-forms-add-on-package}

如需在AEM Forms上安裝Service Pack的說明，請參閱 [AEM Forms Service Pack安裝指示](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### 安裝適用於Experience Manager內容片段的GraphQL索引套件 {#install-aem-graphql-index-add-on-package}

使用GraphQL的客戶應安裝 [具有GraphQL索引套件1.0.5的AEM內容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip).

這可讓您根據索引定義實際使用的功能，新增所需的索引定義。

若未安裝此套件，可能會導致GraphQL查詢緩慢或失敗。

>[!NOTE]
>
>每個執行個體只能安裝此套件一次；不需要隨每個Service Pack重新安裝此套件。

### UberJar {#uber-jar}

The UberJar for [!DNL Experience Manager] 6.5.16.0可在以下網址取得： [Maven中央存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>在Experience Manager6.5.16.0中，UberJar版本(6.5.15.0)與舊版相同。


若要在Maven專案中使用UberJar，請參閱 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 並在您的專案POM中包含下列相依性： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相關成品可在Maven中央存放庫上使用，而不是Adobe公共Maven存放庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為 `uber-jar-<version>.jar`. 因此，沒有 `classifier`，搭配 `apis` 作為值，針對 `dependency` 標籤之間。

## 已弃用功能 {#removed-deprecated-features}

底下列出標示為過時的功能 [!DNL Experience Manager] 6.5.7.0。功能最初會標示為過時，之後會在未來版本中移除。 提供替代選項。

檢閱是否在部署中使用功能或功能。 此外，計畫變更實作以使用替代選項。

| 区域 | 专题 | 替换 |
|---|---|---|
| 集成 | 此 **[!UICONTROL AEM Cloud Services選擇加入]** 熒幕已過時，因為 [!DNL Experience Manager] 和 [!DNL Adobe Target] 整合更新於 [!DNL Experience Manager] 6.5.整合支援Adobe Target Standard API。 API透過Adobe IMS和以下方式使用驗證 [!DNL Adobe I/O Runtime]. 它可支援Adobe Launch在樂器領域日益增加的作用 [!DNL Experience Manager] 頁面進行分析和個人化時，選擇加入精靈在功能上並不相關。 | 設定系統連線、Adobe IMS驗證和 [!DNL Adobe I/O Runtime] 透過個別 [!DNL Experience Manager] 雲端服務。 |
| 连接器 | Microsoft®SharePoint 2010和Microsoft®SharePoint 2013的AdobeJCR聯結器已過時 [!DNL Experience Manager] 6.5. | 不适用 |

## 已知问题 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* 請將可能已使用內容模型的自訂API名稱的GraphQL查詢更新為改用內容模型的預設名稱。

* GraphQL查詢可使用 `damAssetLucene` 索引而非 `fragments` 索引。 這可能會導致GraphQL查詢失敗或需要很長時間執行。

   若要修正問題， `damAssetLucene` 必須設定為包含下列兩個屬性：

   * `contentFragment`
   * `model`

   在索引定義變更後，需要重新索引(`reindex` = `true`)。

   執行這些步驟後，GraphQL查詢的執行速度應該會更快。

* 作為 [!DNL Microsoft®® Windows Server 2019] 不支援 [!DNL MySQL 5.7] 和 [!DNL JBoss®® EAP 7.1]， [!DNL Microsoft®® Windows Server 2019] 不支援以下專案的turnkey安裝 [!DNL AEM Forms 6.5.10.0].

* 如果您升級您的 [!DNL Experience Manager] 從6.5.0 - 6.5.4執行個體到Java™ 11上的最新Service Pack，您會看到 `RRD4JReporter` 中的例外狀況 `error.log` 檔案。 若要停止例外，請重新啟動您的執行個體 [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 使用者可以在下列位置重新命名階層中的資料夾： [!DNL Assets] 並將巢狀資料夾發佈至 [!DNL Brand Portal]. 但是，資料夾的標題不會更新於 [!DNL Brand Portal] 直到重新發佈根資料夾為止。

* 當使用者選擇在最適化表單中首次設定欄位時，儲存設定的選項未顯示在屬性瀏覽器中。 選擇在相同編輯器中設定最適化表單的其他欄位即可解決問題。

* 安裝期間可能會顯示下列錯誤和警告訊息 [!DNL Experience Manager] 6.5.x.x：
   * 「當在中設定Adobe Target整合時 [!DNL Experience Manager] 使用Target Standard API （IMS驗證），然後將體驗片段匯出至Target會導致建立錯誤的選件型別。 Target不會使用「體驗片段」/來源「Adobe Experience Manager」型別，而是會建立多個具有「HTML」/來源「Adobe Target Classic」型別的選件。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在granite/operations/maintenance找不到維護時段。
   * 使用SUM、MAX和MIN等彙總函式時，Adaptive Form伺服器端驗證會失敗(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在granite/operations/maintenance找不到維護時段。
   * 透過Shoppable Banner檢視器預覽資產時，Dynamic Media互動影像中的熱點不可見。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待登入變更完成解除登入逾時。

* 嘗試移動/刪除/發佈內容片段或網站/頁面時，發生擷取內容片段參考的問題，因為背景查詢失敗；即功能無法運作。
若要確保作業正確，您必須將下列屬性新增至索引定義節點 `/oak:index/damAssetLucene` （不需要重新索引）：

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

* 在AEM Forms中，POP3通訊協定不適用於Microsoft® Office 365的電子郵件端點。
* 在JBoss® 7.1.4平台上，當使用者安裝AEM 6.5.16.0 Service Pack時， `adobe-livecycle-jboss.ear` 部署失敗。

## 包含的OSGi套件組合和內容套件 {#osgi-bundles-and-content-packages-included}

下列文字檔案列出中包含的OSGi套件組合和內容套件 [!DNL Experience Manager] 6.5.16.0： <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager6.5.16.0中包含的OSGi套件組合清單](/help/release-notes/assets/65160_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.16.0中包含的內容套件清單](/help/release-notes/assets/65160_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站 {#restricted-sites}

這些網站僅供客戶使用。 如果您是客戶且需要存取權，請聯絡您的Adobe客戶經理。

* [產品下載網址為licensing.adobe.com](https://licensing.adobe.com/)
* [聯絡Adobe客戶支援](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)
>* [订阅 Adobe 产品更新早知道](https://www.adobe.com/cn/subscription/priority-product-update.html)

