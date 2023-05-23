---
title: 與Adobe Dynamic Tag Management整合
seo-title: Integrating with Adobe Dynamic Tag Management
description: 瞭解與Adobe Dynamic Tag Management的整合。
seo-description: Learn about integration with Adobe Dynamic Tag Management.
uuid: cbb9f942-44e3-4cd5-b07d-4298a7a08376
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b8c7a20a-7694-4a49-b66a-060720f17dad
exl-id: 1e0821f5-627f-4262-ba76-62303890e112
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2208'
ht-degree: 3%

---

# 與Adobe Dynamic Tag Management整合 {#integrating-with-adobe-dynamic-tag-management}

整合 [AdobeDynamic Tag Management](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) AEM，讓您能夠使用Dynamic Tag Management Web屬性來追蹤AEM網站。 Dynamic Tag Management可讓行銷人員管理用於收集資料的標籤，並在數位行銷系統之間散發資料。 例如，使用Dynamic Tag Management來收集AEM網站的使用量資料，並散發資料以在Adobe Analytics或Adobe Target中進行分析。

整合之前，您需要建立動態Tag Management [Web屬性](https://microsite.omniture.com/t2/help/en_US/dtm/#Web_Properties) 追蹤AEM網站網域的資訊。 此 [託管選項](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) 的Web屬性，以便您可以設定AEM來存取Dynamic Tag Management程式庫。

在您設定整合後，對動態Tag Management部署工具和規則的變更不需要您在AEM中變更Dynamic Tag Management設定。 這些變更可自動供AEM使用。

>[!NOTE]
>
>如果您使用具有自訂Proxy設定的DTM，您需要設定HTTP使用者端Proxy設定，因為AEM的某些功能使用3.x API，而其他功能則使用4.x API：
>
>* 3.x 通过 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) 进行配置
>* 4.x 通过 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) 进行配置
>


## 部署選項 {#deployment-options}

下列部署選項會影響與Dynamic Tag Management整合的設定。

### Dynamic Tag Management託管 {#dynamic-tag-management-hosting}

AEM支援在雲端中託管或在AEM上託管的動態Tag Management。

* 雲端託管： Dynamic Tag Management JavaScript程式庫會儲存在雲端中，您的AEM頁面會直接參照這些程式庫。
* AEM託管： Dynamic Tag Management會產生javascript程式庫。 AEM會使用工作流程模型來取得及安裝程式庫。

您的實作所使用的託管型別會決定您執行的一些設定和實作任務。 如需託管選項的相關資訊，請參閱 [託管 — 內嵌標籤](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) (在動態Tag Management說明中)。

### 中繼和生產程式庫 {#staging-and-production-library}

決定您的AEM編寫執行個體是使用動態Tag Management測試版或生產程式碼。

通常您的製作執行個體會使用動態Tag Management測試資料庫，而生產執行個體則會使用生產資料庫。 此案例可讓您使用作者例項來測試未核准的動態Tag Management設定。

如有需要，您的作者執行個體可使用生產環境程式庫。 網頁瀏覽器外掛程式可讓您在程式庫為雲端託管時，切換使用中繼程式庫進行測試。

### 使用Dynamic Tag Management部署鉤點 {#using-the-dynamic-tag-management-deployment-hook}

AEM託管Dynamic Tag Management程式庫時，您可以使用Dynamic Tag Management部署掛接服務自動將程式庫更新推送至AEM。 若對程式庫進行變更(例如編輯Dynamic Tag Management Web屬性時)，就會推送程式庫更新。

若要使用部署掛接，Dynamic Tag Management必須能夠連線至託管程式庫的AEM執行個體。 您必須 [啟用對AEM的存取權](/help/sites-administering/dtm.md#enabling-access-for-the-deployment-hook-service) 適用於Dynamic Tag Management伺服器。

在某些情況下，可能無法連線AEM，例如當AEM位於防火牆後面時。 在這些情況下，您可以使用AEM polling importer選項定期擷取程式庫。 cron工作運算式會指定程式庫下載的排程。

## 啟用Deployment Hook服務的存取權 {#enabling-access-for-the-deployment-hook-service}

啟用Dynamic Tag Management部署掛接服務以存取AEM，讓該服務可以更新AEM託管的程式庫。 指定視需要更新中繼和生產程式庫的Dynamic Tag Management伺服器的IP位址：

* 暂存: `107.21.99.31`
* 生產： `23.23.225.112` 和 `204.236.240.48`

使用下列任一專案執行設定： [網頁主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [`sling:OsgiConfig`](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) 節點：

* 在Web主控台中，使用「設定」頁面上的「DTM部署掛接設定」Adobe專案。
* 若為OSGi設定，服務PID為 `com.adobe.cq.dtm.impl.servlets.DTMDeployHookServlet`.

下表說明要設定的特性。

| Web主控台屬性 | OSGi屬性 | 描述 |
|---|---|---|
| 分段DTM IP白名單 | `dtm.staging.ip.whitelist` | 更新中繼程式庫的動態Tag Management伺服器的IP位址。 |
| 生產DTM IP白名單 | `dtm.production.ip.whitelist` | 更新生產程式庫的Dynamic Tag Management伺服器的IP位址。 |

## 建立動態Tag Management設定 {#creating-the-dynamic-tag-management-configuration}

建立雲端設定，讓AEM執行個體能夠使用Dynamic Tag Management進行驗證，並與您的Web屬性互動。

>[!NOTE]
>
>如果您的DTM Web屬性包含Adobe Analytics工具，而且您也在使用，請避免在頁面上包含兩個Adobe Analytics追蹤程式碼 [內容分析](/help/sites-authoring/content-insights.md). 在您的 [Adobe Analytics雲端設定](/help/sites-administering/adobeanalytics-connect.md#configuring-the-connection-to-adobe-analytics)，選取不包含追蹤程式碼選項。

### 常规设置 {#general-settings}

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>API權杖</td>
   <td>Dynamic Tag Management使用者帳戶的API Token屬性值。 AEM使用此屬性來驗證動態Tag Management。</td>
  </tr>
  <tr>
   <td>公司</td>
   <td>與您登入ID相關聯的公司。</td>
  </tr>
  <tr>
   <td>属性</td>
   <td>您為管理AEM網站的標籤而建立的Web屬性名稱。</td>
  </tr>
  <tr>
   <td>包含有关作者的生产代码</td>
   <td><p>選取此選項可讓AEM作者和發佈執行個體使用動態Tag Management程式庫的生產版本。 </p> <p>若未選取此選項，測試設定會套用至製作執行個體，生產設定則套用至發佈執行個體。</p> </td>
  </tr>
 </tbody>
</table>

### 自行託管屬性 — 測試和生產 {#self-hosting-properties-staging-and-production}

下列動態Tag Management設定的屬性可讓AEM託管Dynamic Tag Management程式庫。 屬性可讓AEM下載及安裝程式庫。 或者，您也可以自動更新程式庫，以確保它們能反映在Dynamic Tag Management管理應用程式中所做的變更。

有些屬性會使用您從Dynamic Tag Management Web屬性「內嵌」標籤的「程式庫下載」區段取得的值。 如需詳細資訊，請參閱 [程式庫下載](https://microsite.omniture.com/t2/help/en_US/dtm/#Library_Download) (在動態Tag Management說明中)。

>[!NOTE]
>
>當您在AEM上託管Dynamic Tag Management套件組合時，必須先在Dynamic Tag Management中啟用「程式庫下載」，才能建立設定。 此外，必須啟用Akamai，因為Akamai提供可供下載的資料庫。

在AEM上託管Dynamic Tag Management程式庫時，AEM會根據您的設定自動設定Web屬性的某些屬性。 請參閱下表的說明。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>使用自行託管</td>
   <td>選取在AEM上託管Dynamic Tag Management程式庫檔案的時間。 選取此選項會導致此表格中的其他屬性出現。</td>
  </tr>
  <tr>
   <td>DTM 包 URL</td>
   <td>用於下載Dynamic Tag Management資料庫的URL。 從Dynamic Tag Management的「資料庫下載」頁面的「下載URL」區段取得此值。 基於安全考量，此值必須手動設定。</td>
  </tr>
  <tr>
   <td>下载工作流</td>
   <td><p>用於下載和安裝Dynamic Tag Management程式庫的工作流程模型。 預設模式為預設DTM組合包下載。 除非您已建立自訂模型，否則請使用此模型。</p> <p>請注意，預設下載工作流程會在程式庫下載時自動啟動。</p> </td>
  </tr>
  <tr>
   <td>域提示</td>
   <td><p>（選用）代管Dynamic Tag Management程式庫的AEM伺服器網域。 指定值以覆寫為設定的預設網域 <a href="/help/sites-developing/externalizer.md">Day CQ Link Externalizer service</a>.</p> <p>連線至動態Tag Management時，AEM會使用此值來設定動態Tag Management Web屬性的程式庫下載屬性的測試HTTP路徑或生產HTTP路徑。</p> </td>
  </tr>
  <tr>
   <td>安全網域提示</td>
   <td><p>（選用）透過HTTPS託管Dynamic Tag Management程式庫的AEM伺服器網域。 指定值以覆寫為設定的預設網域 <a href="/help/sites-developing/externalizer.md">Day CQ Link Externalizer service</a>.</p> <p>連線至動態Tag Management時，AEM會使用此值來設定動態Tag Management Web屬性的程式庫下載屬性的測試HTTPS路徑或生產HTTPS路徑。</p> </td>
  </tr>
  <tr>
   <td>共享密钥</td>
   <td><p>（選用）用來解密下載的共用機密。 從Dynamic Tag Management之「程式庫下載」頁面的「共用機密」欄位取得此值。</p> <p><strong>注意：</strong> 您必須擁有 <a href="https://www.openssl.org/docs/apps/openssl.html">OpenSSL</a> 安裝在已安裝AEM的電腦上的程式庫，以便AEM可以解密下載的程式庫。</p> </td>
  </tr>
  <tr>
   <td>启用轮询导入程序</td>
   <td><p>（選用）選取以定期下載及安裝Dynamic Tag Management程式庫，確保您使用更新版本。 選取後，Dynamic Tag Management不會將HTTPPOST要求傳送至部署鉤點URL。</p> <p>AEM會自動為Dynamic Tag Management Web屬性設定程式庫下載屬性的「部署掛接URL」屬性。 選取後，屬性會設定為沒有值。 若未選取，屬性會以您的動態Tag Management設定的URL設定。</p> <p>當Dynamic Tag Management部署鉤點無法連線至AEM (例如AEM位於防火牆後)時，啟用輪詢匯入工具。</p> </td>
  </tr>
  <tr>
   <td>时间表表达式</td>
   <td>（當選取「啟用Polling Importer」時顯示和為必要專案。） 控制何時下載Dynamic Tag Management程式庫的cron運算式。</td>
  </tr>
 </tbody>
</table>

![chlimage_1-352](assets/chlimage_1-352.png)

### 雲端託管屬性 — 測試和生產 {#cloud-hosting-properties-staging-and-production}

當動態標籤設定是雲端託管時，您可以為動態Tag Management設定設定下列屬性。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>使用自行託管</td>
   <td>在雲端中託管Dynamic Tag Management程式庫檔案時，請清除此選項。</td>
  </tr>
  <tr>
   <td>页眉代码</td>
   <td><p>從您主機的Dynamic Tag Management取得的測試頁首代碼。 此值會在您連線至Dynamic Tag Management時自動填入。</p> <p> 若要在動態Tag Management中檢視程式碼，請按一下內嵌標籤，然後按一下主機名稱。 展開頁首程式碼區段，然後視需要按一下複製測試內嵌程式碼的內嵌程式碼或生產內嵌程式碼區域。</p> </td>
  </tr>
  <tr>
   <td>页脚代码</td>
   <td><p>從您主機的Dynamic Tag Management取得的測試頁尾代碼。 此值會在您連線至Dynamic Tag Management時自動填入。</p> <p>若要在動態Tag Management中檢視程式碼，請按一下內嵌標籤，然後按一下主機名稱。 展開「頁尾代碼」區段，然後視需要按一下「複製測試內嵌程式碼」的「內嵌程式碼」或「生產內嵌程式碼」區域。</p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-353](assets/chlimage_1-353.png)

下列程式會使用觸控最佳化UI來設定與Dynamic Tag Management的整合。

1. 在邊欄上，按一下「工具>作業>雲端>Cloud Services」 。
1. 在「動態Tag Management」區域中，會顯示下列其中一個連結來新增設定：

   * 如果這是您新增的第一個設定，請按一下立即設定。
   * 若已建立一個或多個組態，請按一下「顯示組態」，然後按一下「可用組態」旁的+連結。

   ![chlimage_1-354](assets/chlimage_1-354.png)

1. 輸入設定的標題，然後按一下「建立」。
1. 在「API權杖」欄位中，輸入動態Tag Management使用者帳戶的「API權杖」屬性值。

   若要取得API權杖的值，請聯絡DTM客戶服務。

   >[!NOTE]
   >
   >Dynamic Tag Management使用者明確要求之前，API權杖不會過期。

   ![chlimage_1-355](assets/chlimage_1-355.png)

1. 按一下「連線至DTM」。 AEM會使用Dynamic Tag Management進行驗證，並擷取您的帳戶相關聯的公司清單。
1. 選取公司，然後選取您要用來追蹤AEM網站的屬性。
1. 如果您在製作執行個體上使用中繼代碼，請取消選取「在製作上包含生產代碼」 。
1. 視需要在「測試設定」標籤和「生產設定」標籤上提供屬性的值，然後按一下「確定」。

## 手動下載Dynamic Tag Management資料庫 {#manually-downloading-the-dynamic-tag-management-library}

手動下載Dynamic Tag Management程式庫，以立即在AEM上更新。 例如，如果您想要在排程Polling Importer自動下載程式庫之前，測試更新的程式庫，請手動下載。

1. 在邊欄上，按一下「工具>作業>雲端>Cloud Services」 。
1. 在動態Tag Management區域中，按一下顯示設定，然後按一下您的設定。
1. 在「測試設定」區域或「生產設定」區域中，按一下「觸發下載工作流程」按鈕以下載和部署程式庫套件。

   ![chlimage_1-356](assets/chlimage_1-356.png)

>[!NOTE]
>
>下載的檔案儲存在 `/etc/clientlibs/dtm/my config/companyID/propertyID/servertype`.
>
>以下內容直接從您的 [DTM設定](#creating-the-dynamic-tag-management-configuration).
>
>* `myconfig`
>* `companyID`
>* `propertyID`
>* `servertype`
>


## 將動態Tag Management設定與您的網站建立關聯 {#associating-a-dynamic-tag-management-configuration-with-your-site}

將您的動態Tag Management設定與網站頁面建立關聯，以便AEM將所需的指令碼新增至頁面。 將網站的根頁面與設定建立關聯。 該頁面的所有子系都會繼承關聯。 如有需要，您可以覆寫下級頁面上的關聯。

使用以下程式，將頁面及其子系與Dynamic Tag Management設定建立關聯。

1. 在傳統UI中開啟網站的根頁面。
1. 使用Sidekick開啟頁面屬性。
1. 在「Cloud Services」標籤中，按一下「新增服務」，選取「動態Tag Management」，然後按一下「確定」。

   ![chlimage_1-357](assets/chlimage_1-357.png)

1. 使用Dynamic Tag Management下拉式選單來選取您的設定，然後按一下「確定」。

使用以下程式來覆寫頁面的繼承組態關聯。 覆寫會影響頁面及所有頁面子代。

1. 在傳統UI中開啟頁面。
1. 使用Sidekick開啟頁面屬性。
1. 在「Cloud Services」標籤上，按一下「繼承自」屬性旁的掛鎖圖示，然後在確認對話方塊中按一下「是」。

   ![chlimage_1-358](assets/chlimage_1-358.png)

1. 移除或選取其他Dynamic Tag Management設定，然後按一下「確定」。
