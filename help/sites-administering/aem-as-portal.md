---
title: AEM入口網站和Portlet
seo-title: AEM Portals and Portlets
description: 瞭解AEM中的入口網站和入口網站。
seo-description: Learn about Portals and Portles in AEM.
uuid: 7f9e316d-277e-4a1e-b6f3-cd89addc897b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 99528fda-5c8c-4034-bcbe-a4cea42f694b
docset: aem65
exl-id: b5f3d3a6-39c0-4aa5-8562-3cc6fa2b9e46
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '6086'
ht-degree: 0%

---

# AEM入口網站和Portlet{#aem-portals-and-portlets}

本檔案說明下列各項：

* AEM入口網站架構
* 管理和設定AEM as a portal
* 使用AEM作為入口網站
* 在Portlet （例如網頁伺服器）中安裝、設定和顯示AEM內容

## AEM入口網站架構 {#aem-portal-architecture}

AEM入口網站架構包含入口網站和portlet的定義。

### 什麼是入口網站？ {#what-is-a-portal}

入口網站是一種網站應用程式，可提供個人化、單一登入、不同來源的內容整合，並託管資訊系統的展示層。

您可以在AEM中執行符合JSR 286規範的Portlet。 Portlet元件可讓您在頁面上內嵌Portlet。 另請參閱 [管理AEM內容Portlet](#administeringthecqcontentportlet).

### 什麼是Portlet？ {#what-is-a-portlet}

Portlet是部署在產生動態內容之容器內的Web元件。 Portlet介面會封裝並部署為Portlet容器內的.war檔案。 如果您執行AEM作為入口網站，則需要Portlet的.war檔案才能執行Portlet。

若要設定AEM內容顯示在入口網站中，請參閱 [在Portlet中安裝、設定和使用AEM](#installingconfiguringandusingcqinaportlet).

### AEM入口網站Director {#aem-portal-director}

>[!CAUTION]
>
>AEM Portal Director自AEM 6.4起即已過時。另請參閱 [過時和移除的功能](https://helpx.adobe.com/experience-manager/6-4/release-notes/deprecated-removed-features.html).

## 管理AEM內容Portlet {#administering-the-aem-content-portlet}

AEM內容Portlet可讓您在入口網站中顯示AEM內容。 此Portlet位於 `/crx-quickstart/opt/portal`、和能以各種方式自訂。 例如，您可以部署自己的驗證服務，產生AEM所需的驗證資訊，以覆寫預設行為，藉此自訂SSO/驗證處理。 外掛程式會使用已定義的API，讓您藉由建立外掛程式來針對API新增自己的功能。 外掛程式可部署至執行中的Portlet。 若要正常運作，它需要AEM製作和發佈執行個體的設定，以及要在啟動時顯示的內容路徑。

部分設定可透過Portlet偏好設定進行變更，其他設定則可透過OSGi服務設定進行變更。 您透過以下方式變更這些設定： **設定** 檔案或OSGi Web主控台。

### Portlet喜好設定 {#portlet-preferences}

Portal偏好設定可在部署時於入口網站伺服器設定，或透過編輯 **WEB-INF/portlet.xml** 部署portlet web應用程式之前的檔案。 portlet.xml檔案預設會顯示如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<portlet-app xmlns="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd /opt/SUNWps/dtd/portlet.xsd"
             version="1.0">
   <portlet>
      <portlet-name>RSSWeatherPortlet</portlet-name>
      <portlet-class>org.jboss.portlet.weather.WeatherPortlet</portlet-class>
      <init-param>
         <name>default_zipcode</name>
         <value>05673</value>
      </init-param>
      <init-param>
         <name>RSS_XSL</name>
         <value>/WEB-INF/Rss.xsl</value>
      </init-param>
      <init-param>
         <name>base_url</name>
         <value>https://xml.weather.yahoo.com/forecastrss?p=</value>
      </init-param>
      <expiration-cache>180</expiration-cache>
      <supports>
         <mime-type>text/html</mime-type>
         <portlet-mode>VIEW</portlet-mode>
         <portlet-mode>EDIT</portlet-mode>
      </supports>
      <portlet-info>
         <title>Weather Portlet</title>
      </portlet-info>
      <portlet-preferences>
         <preference>
            <name>expires</name>
            <value>180</value>
         </preference>
         <preference>
            <name>RssXml</name>
            <value>https://xml.weather.yahoo.com/forecastrss?p=33145</value>
            <read-only>false</read-only>
         </preference>
      </portlet-preferences>
   </portlet>
</portlet-app>
```

Portlet可使用下列偏好設定進行設定：

<table>
 <tbody>
  <tr>
   <td>start路徑</td>
   <td><p>這是Portlet的開始路徑：它定義最初顯示的內容。</p> <p><strong>重要</strong>AEM ：如果將Portlet設定為連線至在不同於<strong> /</strong>，您必須啟用此力 <strong>CQUrlInfo</strong> 在這些AEM例項的Html資料庫管理員設定中（例如透過Felix Webconsole），或編輯將無法運作，且不會顯示偏好設定對話方塊。</p> </td>
  </tr>
  <tr>
   <td>htmlSelector</td>
   <td>附加至每個url的選擇器。 依預設，這是 <strong>Portlet</strong>，因此對html頁面的所有請求都使用結尾為 <strong>.portlet.html.</strong> 這允許在AEM中使用自訂指令碼來轉譯Portlet。</td>
  </tr>
  <tr>
   <td>addCssToPortalHeader</td>
   <td><p>根據預設，AEMHTML頁面中包含的css檔案會包含在Portlet中。 停用此選項會排除預設的css檔案。</p> <p>如果啟用此選項，會根據入口網站的行為，將CSS檔案新增至html頁面的標頭或內嵌於html頁面。</p> </td>
  </tr>
  <tr>
   <td>includeToolbar</td>
   <td>根據預設，管理功能的工具列會呈現在內容Portlet中。 若停用此選項，將不會轉譯任何工具列。</td>
  </tr>
  <tr>
   <td>urlParameterName</td>
   <td><p>可能包含要針對Portlet顯示的新內容URL的替代URL引數名稱清單。 系統會由上而下處理清單，並使用包含值的第一個引數。 如果找不到URL，則會使用預設的URL引數。 提供的URL會照原樣使用，而不會進行任何進一步的修改。</p> <p>此設定是根據已部署的Portlet而設定，也是為了在「Day Portal Director Portlet Bridge」的OSGi設定中全域設定一些url引數。</p> </td>
  </tr>
  <tr>
   <td>偏好設定對話方塊</td>
   <td>AEM中偏好設定對話方塊的路徑 — 如果留空，將會使用內建偏好設定對話方塊。 此預設為/libs/portal/content/prefs.html。</td>
  </tr>
  <tr>
   <td>initialRedirect</td>
   <td>依預設，Portlet會在第一次叫用時，對整個入口網站頁面執行Javascript重新導向。 這是為了支援現代入口網站伺服器的拖放案例。 在生產環境中，很少需要此重新導向，因此可將此偏好設定設為關閉 <em>false</em>.</td>
  </tr>
 </tbody>
</table>

#### OSGi Web主控台 {#osgi-web-console}

假設入口網站伺服器執行於主機localhost、連線埠8080，且AEM portlet Web應用程式已掛載在Web應用程式內容中 *cqportlet*，網頁主控台的url為 `https://localhost:8080/cqportlet/cqbridge/system/console`. 預設的使用者和密碼為 **管理員**.

開啟 **設定** 標籤並選取 **入口網站目錄CQ伺服器設定**. 您可以在此處指定作者和發佈例項的基底URL。 此程式的說明請參閱 [設定Portlet](#configuring-the-portlet).

>[!NOTE]
>
>OSGi Web控制檯僅適用於開發（或測試）期間變更設定。 請務必封鎖生產系統向主控台發出的請求。

### 提供設定 {#providing-configurations}

為了支援自動部署和設定布建，AEM內容Portlet具有內建的設定支援，可嘗試從提供給Portlet應用程式的類別路徑讀取設定。

啟動時，系統屬性 **com.day.cq.portet.config** 會讀取以偵測目前的環境。 通常，此屬性的值類似於 **開發**， **prod**， **測試** 等等。 如果未設定任何環境，則不會讀取任何設定。

如果設定了環境，則會在* *的類別路徑中搜尋設定檔案&#x200B;**com/day/cq/portlet/{env}.config** 位置 **環境** 會取代為環境的實際值。 此檔案應列出此環境的所有組態檔。 系統會根據組態檔的位置來搜尋這些檔案。 例如，如果檔案包含一行 `my.service.xml,` 從類別路徑中讀取此檔案： `com/day/cq/portlet/my.service.config.` 檔案名稱由服務的持續性ID組成，後面接著 **.config**. 在上一個範例中，持續性ID為 **my.service**. 設定檔案的格式為Apache Sling OSGi安裝程式使用的格式。

這表示對於每個環境，都需要新增對應的設定檔案。 應套用至所有環境的設定需要在這些檔案中輸入 — 如果它只用於單一環境，則它只會在該檔案中輸入。 此機制可確保完全控制要在哪個環境中讀取哪個設定。

您可以使用不同的系統屬性來偵測環境。 指定系統屬性 **com.day.cq.portet.configproperty** 包含要使用的系統屬性名稱，而不是 **com.day.cq.portet.config**.

#### 快取和快取失效 {#caching-and-caching-invalidation}

Portlet在其預設設定中，會將其從AEM WCM收到的回應快取到使用者專用的快取中。 當發佈執行個體的內容發生變更時，快取需要失效。 為此，在AEM WCM中，必須在編寫執行個體上設定復寫代理程式。 也可以手動排清快取。 本節將說明這兩個程式。

Portlet可自行設定其快取，以便顯示Portlet中的內容而不需要存取AEM。 入口網站可作為/libs/portal/director中的內容使用。 若要存取內容，請啟動AEM執行個體，並使用CRXDE Lite或Webdav從該位置下載檔案。

您可在執行階段部署此套件，或將其新增至Portlet Web應用程式，網址為 `WEB-INF/lib/resources/bundles` 部署之前。

部署快取後，Portlet會快取來自發佈執行個體的內容。 來自AEM的Dispatcher Flush可讓Portlet快取失效。 若要設定Portlet使用自己的快取：

1. 在作者中設定以入口網站伺服器為目標的復寫代理程式。
1. 假設入口網站伺服器於主機上執行 **localhost**，**連線埠8080 **和AEM portlet web應用程式已掛接在內容中 **cqportlet**，清除快取的url為 `https://localhost:8080/cqportlet/cqbridge/cqpcache?Path=$(path)`. 使用GET作為方法。
   **注意：** 您可以傳送名為的http標頭，而不使用要求引數 **路徑**.

#### 透過復寫代理程式排清快取 {#flushing-the-cache-via-replication-agent}

就像一般的Dispatcher失效一樣，可設定復寫代理程式來鎖定入口網站的AEM Portlet快取。 在您設定復寫代理程式後，每次定期啟用頁面都會排清入口網站快取。

如果您運算元個執行AEM Portlet的入口網站節點，則需要依照此程式中的說明為每個節點建立代理程式。

設定入口網站的復寫代理程式：

1. 登入作者執行個體。
1. 在「網站」標籤中，按一下 *工具* 標籤。
1. 按一下 **新增頁面……** 在復寫代理程式中 **新增……** 功能表。

   ![screen_shot_2012-02-15at40647pm](assets/screen_shot_2012-02-15at40647pm.png)

1. 在 *範本*，選取 *復寫代理*，然後輸入代理程式的名稱。 单击&#x200B;*创建*。

   ![screen_shot_2012-02-15at40817pm](assets/screen_shot_2012-02-15at40817pm.png)

1. 連按兩下您剛建立的復寫代理程式。 它會顯示為無效，因為尚未設定。

   ![screen_shot_2012-02-15at41001pm](assets/screen_shot_2012-02-15at41001pm.png)

1. 按一下 **編輯。**
1. 在 **設定** 索引標籤中，選取 **已啟用** 核取方塊，選取 **Dispatcher排清** 作為序列化型別，並輸入重試逾時(例如60000)。

   ![screen_shot_2012-02-15at42101pm](assets/screen_shot_2012-02-15at42101pm.png)

1. 按一下 **傳輸** 標籤。
1. 在 **URI** 欄位中，輸入Portlet的排清URI (URL)。 URI的格式如下：

   ```xml
   https://<wps-host>:<port>/<wps-context>/<cq5-portlet-context>/cqbridge/cqpcache
   ```

   ![screen_shot_2012-02-15at42322pm](assets/screen_shot_2012-02-15at42322pm.png)

1. 按一下 **延伸** 標籤。

   ![screen_shot_2012-02-15at42515pm](assets/screen_shot_2012-02-15at42515pm.png)

1. 在 **HTTP方法** 欄位，型別 **GET**.
1. 在 **HTTP標頭** 欄位，按一下 **+** 以新增專案及型別 **路徑：{path}**.
1. 如有需要，請按一下 **代理** 索引標籤並輸入代理程式的Proxy資訊。
1. 按一下 **確定** 以儲存變更。
1. 若要測試連線，請按一下 **測試連線** 連結。 此時會出現日誌訊息，指出復寫測試是否成功。 例如：

   ![screen_shot_2012-02-15at42639pm](assets/screen_shot_2012-02-15at42639pm.png)

#### 手動排清Portlet快取 {#manually-flushing-the-portlet-cache}

您可以存取為復寫代理程式設定的相同URL，以手動清除Portlet快取。 另請參閱 [排清快取](#flushing-the-cache-via-replication-agent) （以URL的形式）。 此外，URL需要以URL引數Path=擴充&lt;path> 以指示要排清的專案。

例如：

`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=*` 排清完整快取。 `https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=/content/mypage/xyz` 排清 `/content/mypage/xyz` 從快取中。

### 入口網站安全性 {#portal-security}

入口網站是驅動驗證機制。 您可以透過技術使用者、入口網站使用者、群組等登入AEM。 Portlet無法存取入口網站中使用者的密碼，因此，如果Portlet不知道成功登入使用者的所有認證，則必須使用SSO解決方案。 在此情況下，AEM Portlet會將所有必要資訊轉送至AEM，接著會將此資訊轉送至基礎AEM存放庫。 此行為是可插入的，且可供自訂。

### 發佈時驗證 {#authentication-on-publish}

本節說明Portlet在與基礎AEM WCM執行個體通訊時可使用的驗證模式。

依預設，不會將任何使用者資訊傳送至AEM的發佈執行個體；內容一律顯示為匿名使用者。 如果應從AEM傳送使用者特定資訊，或需要發佈的使用者驗證，則必須開啟此功能。

#### 存取Portlet的驗證設定 {#accessing-the-portlet-s-authentication-configuration}

Portlet在AEM WCM執行個體中使用的驗證設定選項可在Web主控台（OSGi設定）中使用。

>[!NOTE]
>
>使用AEM時，有數種方法可管理OSGi服務的組態設定（主控台或存放庫節點）。
>
>另請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。

若要存取Portlet的驗證設定：

1. 從下列URL存取Web主控台：

   `https://localhost:8080/cqportlet/cqbridge/system/console`

   例如，在其預設設定中：

   `https://wps-host:10040/wps/PA_CQ5_Portlet/cqbridge/system/console`

1. 登入Web控制檯。 預設認證為 `admin/admin`.
1. 在主控台中，選取 **設定**.
1. 在 **設定** 功能表，選取要設定的特定服務。 服務由Portlet在OSGi架構中提供。

   | 服务名称 | 描述 |
   |---|---|
   | Day Portal Director Authenticator | 設定用於AEM WCM執行個體的驗證模式。 根據選取的模式，可以指定技術使用者或SSO Cookie的名稱。 此外，可以啟用AEM WCM發佈執行個體的驗證。 |
   | Day入口網站Director檔案快取 | 設定Portlet如何快取其從AEM WCM執行個體收到的回應的引數。 |
   | Day Portal Director HTTP使用者端服務 | 設定Portlet如何透過HTTP連線至基礎AEM WCM執行個體。 例如，您可以指定Proxy伺服器。 |
   | Day Portal Director地區設定處理常式 | 設定Portlet支援的地區設定。 對AEM WCM執行個體的請求是根據使用者地區設定；例如，使用者語言*德文*會要求 `/content/geometrixx/de/`.... |
   | Day Portal Director許可權管理員 | 設定Portlet是否應根據目前登入的使用者來測試Websites索引標籤。 |
   | Day Portal Director工具列轉譯器 | 自訂Portlet工具列的演算。 |

1. 此外，您也可以設定Web主控台和記錄服務。 例如，您可以按一下Apache Felix OSGi Management Console連結，變更Web Console的管理認證。

#### 技術使用者模式 {#technical-user-mode}

在預設模式中，無論目前的入口網站使用者為何，Portlet針對AEM WCM作者執行個體發出的所有請求都會使用相同的技術使用者進行驗證。 技術使用者模式預設為啟用。 您可以在OSGi管理主控台的個別設定畫面中啟用/停用此模式：

如果符合下列條件，指定的技術使用者必須存在於AEM WCM編寫執行個體和發佈執行個體上 **發佈時驗證** 已啟用。 請務必授予使用者足夠的存取許可權以進行編寫工作。

#### SSO {#sso}

此Portlet支援立即使用AEM執行SSO。 驗證器服務可設定為使用SSO並以格式傳輸目前的入口網站使用者 **基本** 作為名為的Cookie `cqpsso` 至AEM。 AEM應設定為對路徑/使用SSO驗證處理常式。 Cookie名稱也需要在這裡設定。

此 `crx-quickstart/repository/repository.xml` AEM存放庫則需要相應設定：

```xml
<LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
  ...
  <param name="trust_credentials_attribute" value="TrustedInfo"/>
  <param name="anonymous_principal" value="anonymous"/>
</LoginModule>
```

#### SSO驗證模式 {#sso-authentication-mode}

Portlet可以使用單一登入(SSO)配置來驗證AEM WCM。 在此模式中，目前登入入口網站的使用者會以SSO Cookie的形式轉送至AEM WCM。 如果使用SSO模式，則必須讓底層AEM WCM執行個體知道所有可存取AEM Portlet的入口網站使用者，最常見的方式是將AEM WCM連線至LDAP，或事先手動建立使用者。 此外，在Portlet中啟用SSO之前，底層AEM WCM製作例項(和發佈例項，如果 **發佈時驗證** （已啟用）需要設定為接受以SSO為基礎的請求。

若要將Portlet設定為使用SSO驗證模式，請完成以下步驟（以下各節將詳細說明此步驟）：

* 啟用AEM WCM的存放庫以接受信任的認證。
* 在AEM WCM中啟用SSO驗證。
* 在AEM Portlet中啟用SSO驗證。

#### 啟用AEM WCM的存放庫以接受信任的認證 {#enabling-aem-wcm-s-repository-to-accept-trusted-credentials}

在為AEM WCM啟用SSO之前，基礎存放庫需要設定為接受AEM WCM提供的受信任認證。 要執行此操作，請設定AEM repository.xml。

1. 在安裝AEM WCM的檔案系統中，開啟下列檔案：

   `//crx-quickstart/repository/repository.xml`

1. 在XML檔案中，找到 **LoginModule** 並將trust_credentials_attribute新增至其設定：

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
     <param name="anonymous_principal" value="anonymous"/>
   </LoginModule>
   ```

1. 重新啟動AEM WCM以使變更生效。

#### 在AEM WCM中啟用SSO驗證 {#enabling-sso-authentication-in-the-aem-wcm}

若要在AEM WCM中啟用SSO，請存取AEM WCM的Apache Felix Web Management Console (OSGi)中的相關設定專案：

1. 透過其URI (網址為https://)存取主控台&lt;aem-host>：&lt;port>/system/console。
1. 在Configuration功能表中，選取SSO Authentication Handler。 在此範例中，SSO處理常式會根據AEM Portlet提供的Cookie接受所有路徑的SSO要求。 您的設定可能有所不同。

   | 路径 | / | 為所有要求啟用SSO處理常式 |
   |---|---|---|
   | Cookie名稱 | cqpsso | Portlet提供的Cookie名稱，如Portlet的OSGi主控台中所設定。 |

1. 按一下 **儲存** 以啟用SSO。 SSO現在是主要驗證配置。

AEM WCM收到每個請求時，都會先嘗試以SSO為基礎的驗證。 失敗時，會執行一般基本驗證配置的備援。 因此，沒有SSO的AEM WCM仍可正常連線。

#### 在AEM Portlet中啟用SSO驗證 {#enabling-sso-authentication-in-a-aem-portlet}

為了使基礎AEM WCM執行個體接受SSO請求，必須將Portlet的驗證模式從 **技術** 至 **SSO**.

若要在AEM Portlet中啟用SSO驗證：

1. 透過其URI (網址為https://)存取主控台&lt;aem-host>：&lt;port>/system/console。
1. 在「設定」功能表中，從可用設定清單中選取Day Portal Director Authenticator 。
1. 在模式中，選取SSO。 將其他引數保留為其預設值。

   ![chlimage_1-135](assets/chlimage_1-135.png)

1. 按一下儲存，為Portlet啟用SSO。

   出於測試目的，當您在AEM WCM中以管理員許可權建立相同的使用者後，請使用入口網站的管理使用者來存取Portlet。

執行此程式後，會使用SSO驗證要求。 HTTP通訊的典型程式碼片段會顯示下列SSO和Portlet特定標題：

```xml
C-12-#001898 -> [GET /mynet/en/_jcr_content/par/textimage/image.img.png HTTP/1.1 ]
C-12-#001963 -> [cq5:locale: en ]
C-12-#001979 -> [cq5:used-locale: en ]
C-12-#002000 -> [cq5:locales: en,en_US ]
C-12-#002023 -> [cqp:user: wpadmin ]
C-12-#002042 -> [cqp:portal: IBM WebSphere Portal/6.1 ]
C-12-#002080 -> [cqp:windowid: 7_CGAH47L000CE302V2KFNOG0084 ]
C-12-#002124 -> [cqp:windowstate: normal ]
C-12-#002149 -> [cqp:portletmode: view ]
C-12-#002172 -> [User-Agent: Jakarta Commons-HttpClient/3.1 ]
C-12-#002216 -> [Host: 10.0.0.68:4502 ]
C-12-#002238 -> [Cookie: $Version=0; cqpsso=Basic+d3BhZG1pbg%3D%3D ]
C-12-#002289 -> [ ]
```

### 啟用PIN驗證 {#enabling-pin-authentication}

如果您未使用AEM內容Portlet的預設內嵌編輯功能，但希望在AEM編寫執行個體中直接在入口網站外部編寫Portlet和管理部分，則應啟用PIN驗證。 您也需要變更管理按鈕的設定。

若要開啟網站管理頁面或從Portlet編輯頁面，AEM內容Portlet會使用新的pin驗證。 根據預設，釘選驗證已停用，因此，必須在AEM中進行下列設定變更：

1. 在repository.xml檔案中新增信任資訊，以在AEM中啟用信任驗證：

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
   </LoginModule>
   ```

1. 在OSGi設定主控台中，預設為位於https://localhost:4502/system/console/configMgr，選取 **CQ PIN驗證處理常式** 從下拉式功能表。
1. 編輯 **URL根路徑** 引數以只包含單一值 **/**.

### 特权 {#privileges}

Portlet的某些功能受到許可權保護。 目前的使用者需要擁有此許可權，才能存取此函式。 預先定義下列許可權：

* &quot;toolbar&quot; ：這是檢視/使用Portlet中工具列的一般許可權。
* &quot;prefs&quot; ：如果使用者擁有此許可權，則允許使用者檢視/變更Portlet的偏好設定。
* &quot;cq-author：edit&quot; ：透過此許可權，使用者可叫用內容的編輯檢視。
* &quot;cq-author：preview&quot; ：透過此許可權，使用者可檢視預覽。
* &quot;cq-author：siteadmin&quot; ：此許可權可讓使用者在AEM中開啟siteadmin。

管理許可權的最佳方式是使用入口網站角色，並將角色指派給這些許可權。 這可透過OSGi設定完成。 「Day Portal Director Privilege Manager」可針對每個許可權設定一組角色。 如果使用者具有其中一個角色，則使用者具有對應的許可權。

此外，也可以根據每個Portlet執行個體基底來定義此角色型存取。 Portlet的偏好設定對話方塊包含上述每個許可權的輸入欄位。 您可以為每個許可權設定逗號分隔的Portlet角色清單。 如果設定了值，這會覆寫「Day Portal Director Privilege Manager」服務的全域設定，而且由於角色未合併，因此可能需要從此全域設定新增相同的角色！ 如果未指定任何值，則會使用全域設定。

### 自訂AEM Portlet應用程式 {#customizing-the-aem-portlet-application}

提供的AEM Portlet應用程式會在Web應用程式中啟動OSGi容器，就像AEM一樣。 此架構可讓您運用OSGi的所有優點：

* 易於更新和擴充
* 提供Portlet的熱量更新，而不需入口網站伺服器任何互動
* 輕鬆自訂Portlet

### 工具列按鈕 {#toolbar-buttons}

工具列及其按鈕是可設定的，並可以自訂。 您可以將自己的按鈕新增至工具列，或定義哪些按鈕會以何種模式顯示。 每個按鈕都是可透過OSGi設定設定的OSGi服務。

OSGi Web主控台會列出 **設定** 標籤。 對於每個按鈕，您可以定義此按鈕在哪種模式中顯示。 例如，這可讓您移除所有模式來停用按鈕。

依預設，AEM內容Portlet會使用內嵌編輯功能。 不過，如果您偏好切換至AEM編寫執行個體進行編輯，請啟用 **網站管理員按鈕** 和 **ContentFinder按鈕**，但停用 **編輯按鈕**. 在此情況下，請務必在AEM中正確設定PIN驗證。

可透過Portlet的Felix Web主控台安裝套件組合(包含在預先定義位置的自訂CSS/HTML)來自訂Portlet的工具列配置。

#### 組合結構 {#bundle-structure}

以下是範例組合結構：

```xml
$ jar tvf target/toolbarlayout-0.0.1-SNAPSHOT.jar | awk '{print $8}'
META-INF/
META-INF/MANIFEST.MF
/com/day/cq/portlet/toolbar/layout/
/com/day/cq/portlet/toolbar/layout/author.gif
/com/day/cq/portlet/toolbar/layout/back.gif
/com/day/cq/portlet/toolbar/layout/button.html
/com/day/cq/portlet/toolbar/layout/edit.gif
/com/day/cq/portlet/toolbar/layout/manage.html
/com/day/cq/portlet/toolbar/layout/publish.html
/com/day/cq/portlet/toolbar/layout/refresh.gif
/com/day/cq/portlet/toolbar/layout/siteadmin.gif
/com/day/cq/portlet/toolbar/layout/toolbar.css
```

META-INF資料夾包含OSGi識別為套件所需的MANIFEST.MF檔案。 它顯示如下：

```xml
Manifest-Version: 1.0
Built-By: djaeggi
Created-By: Apache Maven Bundle Plugin
Import-Package: com.day.cq.portlet.toolbar.layout
Bnd-LastModified: 1234178347159
Export-Package: com.day.cq.portlet.toolbar.layout
Bundle-Version: 0.0.1.SNAPSHOT
Bundle-Name: Company CQ5 Portal Director Portlet Toolbar Layout
Bundle-Description: This bundle provides a custom layout for the CQ5 P
 ortal Director Portlet Toolbar.
Build-Jdk: 1.5.0_16
Bundle-ManifestVersion: 2
Bundle-SymbolicName: com.day.cq.portlet.company.toolbarlayout
Tool: Bnd-0.0.255
```

HTML/CSS/images位於/com/day/cq/portlet/toolbar/layout資料夾內這個事實是由portlet強制規定的，無法變更。 按照相同的順序，MANIFEST.MF中的Import-Package和Export-Package標頭也必須呼叫/com/day/cq/portlet/toolbar/layout。 Bundle-SymbolicName必須是唯一、完全合格的套件名稱。

您可以使用maven之類的工具來建置它，或手動建立具有相關標頭集的jar檔案，如本節所示。

#### Portlet工具列檢視 {#portlet-toolbar-views}

Portlet的工具列基本上有兩個檢視狀態。 每個檢視和關聯的按鈕都可以使用各自的HTML檔案自訂。

#### 發佈檢視 {#publish-view}

發佈檢視只有一個按鈕，可將工具列切換至「管理」檢視。 發佈檢視由publish.html檔案表示，位於 [上一個組合](/help/sites-deploying/configuring-osgi.md#bundles). 在HTML中，您可以使用下列預留位置，在轉譯時這些預留位置會由Portlet以個別內容取代：

#### 發佈檢視預留位置 {#publish-view-placeholders}

| 預留位置字串 | 描述 |
|---|---|
| {buttonManage} | 預留位置已由 **管理** 按鈕，將portlet狀態切換為管理狀態。 |

#### 管理檢視 {#manage-view}

「管理」檢視有四個按鈕：「編輯」、「網站」標籤、「重新整理」和「上一步」。 管理檢視由manage.html檔案表示，該檔案位於 [上一個組合](/help/sites-deploying/configuring-osgi.md#bundles). 在HTML中，您可以使用下列預留位置，在轉譯時這些預留位置會由Portlet以個別內容取代：

#### 管理檢視預留位置 {#manage-view-placeholders}

| 預留位置字串 | 描述 |
|---|---|
| {buttonEdit} | 預留位置已由 **編輯** 按鈕，在AEM編輯模式下開啟目前頁面的新視窗。 |
| {buttonWebsites索引標籤} | 預留位置，取代為開啟AEM WCM網站標籤的按鈕。 |
| {buttonRefresh} | 重新整理目前的檢視。 |
| {buttonBack} | 將Portlet切換回發佈檢視。 |

#### 按钮 {#buttons}

按鈕無論在哪個檢視中出現，都會使用相同的通用HTML（定義於button.html中）。

在HTML中，您可以使用下列預留位置，在轉譯時這些預留位置會由Portlet以個別內容取代：

#### 管理和發佈檢視按鈕 {#manage-and-publish-view-buttons}

| 預留位置字串 | 描述 |
|---|---|
| {name} | 按鈕的名稱，例如**作者、上一步**重新整理等等。 |
| {id} | 按鈕的CSS ID。 |
| {url} | 按鈕目標的URL。 |
| {text} | 按鈕的標籤。 |
| {onclick} | Javascript **onclick** 函式（包含{url}）。 |

button.html檔案的範例：

```xml
<div class="cqp_button">

 <a href="#" onclick="{onclick}">

 <img src="/wps/PA_CQ5_Portlet/cqbridge/static/{id}.gif" alt="{text}"
title="{text}"/>

 </a>
</div>
```

#### 安裝自訂配置 {#installing-a-custom-layout}

若要安裝自訂配置，請存取Portlet的OSGI Web控制檯**套件**區段，然後上傳套件。

#### 包 {#packages}

如果您需要上傳或建立用於安裝的套件，請參閱AEM檔案中的套件管理員，以取得詳細指示。

### 連結處理 {#link-handling}

所有連結都會被重寫以在入口網站內容中運作。 預設會使用具有轉譯器引數的連結。 可將入口網站DirectorHTML重寫程式設定為改用動作連結。

您也可以定義要查詢以顯示內容路徑的其他請求引數。 這很有用，例如，如果有從外部到特定內容的連結。

此外，入口網站DirectorHTML重寫程式可設定包含定義為連結重寫排除的規則運算式清單。 例如，如果您有外部系統的相對連結，則應將它們新增至此排除清單。

### 本地化 {#localization}

AEM內容Portlet具有內建的本地化功能，可確保來自AEM的內容使用正確的語言。

這需分兩步完成：

1. 入口網站目錄地區設定偵測器會透過從入口網站取得地區設定來偵測入口網站使用者的地區設定。 此服務必須使用AEM中的可用語言清單進行設定。
1. 入口網站Director地區設定處理常式可處理目前要求的當地語系化。 它會採用請求內容的路徑，例如 `/content/geometrixx/en/company.html`根據設定，它會重寫 **en** 與使用者的實際地區設定相符。

入口網站Director地區設定處理常式可設定檢查地區設定資訊的路徑，這通常包括 `/content` 以及路徑中地區設定資訊的位置。 根據預設，地區設定處理常式會遵循AEM中建構多語言網站的通用方式。

如果您的網站對於處理路徑中的地區設定資訊沒有嚴格的規則，則可以使用您自己的實作來取代地區設定處理常式。

### 選購的OSGi服務 {#optional-osgi-services}

您可以實作選用的OSGi服務，以自訂Portlet的各個部分。 每個服務都對應一個Java介面。 此介面可透過套件部署到Portlet中。

<table>
 <tbody>
  <tr>
   <td>RequestTracker</td>
   <td>每當Portlet顯示內容時，要求追蹤器都會收到通知。 這可讓您追蹤Portlet的叫用情形。</td>
  </tr>
  <tr>
   <td>InvocationContextListener</td>
   <td>在對Portlet的每個請求開始和結束時所叫用的監聽器。 監聽器可用來變更或新增目前要求的資訊。<br /> </td>
  </tr>
  <tr>
   <td>ErrorHandler</td>
   <td>轉譯階段期間錯誤的自訂錯誤處理常式。</td>
  </tr>
  <tr>
   <td>HttpProcessor</td>
   <td>此服務可用來將資訊新增至每次http叫用至AEM。</td>
  </tr>
  <tr>
   <td>PortletAction</td>
   <td>將自己的動作新增至Portlet — 此動作可透過Portlet動作連結叫用。</td>
  </tr>
  <tr>
   <td>PortletDecoratorService</td>
   <td>此服務可用來裝飾Portlet的內容。</td>
  </tr>
  <tr>
   <td>ResourceProvider</td>
   <td>新增您自己的資源提供者，透過Portlet資源連結將部分資源傳送至使用者端。</td>
  </tr>
  <tr>
   <td>TextMapper</td>
   <td>可讓您發佈程式HTML、CSS和Javascript檔案。</td>
  </tr>
  <tr>
   <td>ToolbarButton</td>
   <td>將您自己的按鈕新增至工具列。</td>
  </tr>
  <tr>
   <td>UrlMapper</td>
   <td>新增服務以套用自訂url對應或重寫。</td>
  </tr>
  <tr>
   <td>使用者資訊提供者</td>
   <td>新增您自己的使用者資訊。 此服務可用於從入口網站取得資訊至Portlet。</td>
  </tr>
 </tbody>
</table>

#### 取代預設服務 {#replacing-default-services}

下列服務在內容Portlet中具有預設實作（具有對應的Java介面）。 若要自訂，需要將包含新服務實作的套件組合部署到Portlet應用程式中。

實作此類服務時，請務必將 **service.ranking** 正值的服務屬性。 預設實施使用排名**0**，而Portlet使用排名最高的服務。

| **名称** | **描述** | **預設行為** |
|---|---|---|
| 驗證者 | 提供驗證資訊給AEM | 對作者和發佈使用可設定的技術使用者。 或可使用SSO。 |
| htmlrewriter | 重寫連結、影像等。 | 將AEM連結重寫至入口網站連結，可由UrlMapper和TextMapper擴充 |
| HttpClientService | 處理所有http連線 | 標準實作 |
| LocaleHandler | 處理地區設定資訊 | 根據地區設定重寫內容的連結。 |
| LocaleDetector | 偵測使用者的地區設定。 | 使用入口網站提供的地區設定。 |
| PrivilegeManager | 檢查使用者許可權 | 如果允許使用者編輯內容，則檢查對作者執行個體的存取權 |
| 工具列轉譯器 | 轉譯工具列 | 新增工具列功能 |

### Portlet事件 {#portlet-events}

Portlet API (JSR-286)會指定Portlet事件。 AEM內容Portlet具有整合式橋接器，可將AEM Portlet的Portlet事件發佈為OSGi事件，如此一來，處理Portlet事件就變成可插拔。

如果您想要處理特定事件，請在部署描述項中宣告這些事件為接收事件（或透過入口網站伺服器進行設定），並實作宣告EventHandler介面的OSGi服務（請參閱OSGi EventAdmin規格）。

每當Portlet事件發生時，都會傳送特定OSGi事件，並叫用您的處理常式。 處理常式會取得所有內容資訊，並可據以更新Portlet的狀態或傳送新事件。 基本上，在控制代碼方法內部，可以使用Portlet事件階段的所有功能。

## 使用AEM作為入口網站 {#using-aem-as-a-portal}

使用Portlet元件將Portlet視窗新增至AEM頁面。 您安裝至應用程式伺服器的共用程式庫可讓Portlet元件偵測已部署的Portlet應用程式。

若要使用AEM作為入口網站，請執行下列工作：

1. 安裝Portlet元件和共用程式庫。
1. 將Portlet元件新增至Sidekick。
1. 設定並部署包含您要在Portal元件中顯示之Portlet的Web應用程式。
1. 將Portlet元件新增至頁面，並選取要顯示的Portlet。

>[!NOTE]
>
>只有在將AEM部署為Web應用程式時，才能使用Portlet元件。 ([請參閱使用應用程式伺服器安裝AEM](/help/sites-deploying/application-server-install.md).)

### 安裝Portlet元件 {#installing-the-portlet-component}

AEM快速入門JAR檔案包含Portlet元件檔案。 若要取得檔案(cq-portlet-components.zip)，您可以執行「快速入門」或解壓縮內容。

1. 執行或解壓縮Quickstart JAR檔案的內容，並找到相應的cq-portlet-components.zip檔案：

   * 執行Quickstart： crx-quickstart/opt/portal
   * 擷取快速入門內容：static/opt/portal

1. 開啟部署至應用程式伺服器的CQ5編寫執行個體的封裝管理員。 (https://*appserverhost*：*連線埠*/cq5author/crx/packmgr)

1. 使用封裝管理程式： [上傳並安裝](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) cq-portlets-components.zip套件。

   套件會將cq-portlet-director-sharedlibs-x.x.x.jar安裝在存放庫的/libs/portal/director資料夾中。

1. 將cq-portlet-director-sharedlibs-x.x.x.jar複製到您的硬碟。 使用任何方法取得檔案，例如FileVault或WebDAV使用者端。
1. 將cq-portlet-director-sharedlibs.x.x.x.jar檔案移至應用程式伺服器的共用程式庫資料夾，讓類別可供已部署的Portlet應用程式使用。

### 將Portlet元件新增至Sidekick {#adding-the-portlet-component-to-sidekick}

將Portlet元件新增至段落系統，以供作者使用。

1. 在Sidekick中，按一下尺標圖示以進入設計模式。
1. 旁邊 `Design of par` 標題在第一段上方，按一下 **編輯**.

1. 在 **一般** 元件類別中，選取Portlet元件旁的核取方塊，然後按一下確定。

![chlimage_1-25](assets/chlimage_1-25.jpeg)

### 設定和部署您的Portlet應用程式 {#configuring-and-deploying-your-portlet-applications}

將Portlet部署至應用程式伺服器Web容器，以便它們可供Portal元件使用。 部署Portlet應用程式之前，您需要設定應用程式，以便載入AEM入口網站容器Servlet。 此設定可讓Portlet元件存取Portlet。

1. 解壓縮Portlet應用程式WAR檔案的內容。

   **秘訣：** jar xf *nameofapp*.war指令會擷取檔案。

1. 在文字編輯器中開啟web.xml檔案。
1. 在Web應用程式元素中新增下列servlet設定：

   ```xml
   <servlet>
           <servlet-name>slingportal</servlet-name>
           <servlet-class>org.apache.sling.portal.container.api.ContainerServlet</servlet-class>
           <load-on-startup>1</load-on-startup>
   </servlet>
   <servlet-mapping>
           <servlet-name>slingportal</servlet-name>
           <url-pattern>/SlingPortletInvoker</url-pattern>
   </servlet-mapping>
   ```

1. 儲存web.xml檔案並重新封裝WAR檔案。

   **秘訣：** 此 `jar cvf nameofapp.war *` command會將目前目錄的內容新增至nameofapp.war檔案。

1. 將Portlet應用程式部署至應用程式伺服器。 如需詳細資訊，請參閱應用程式伺服器的檔案。

### 將Portlet新增至您的AEM頁面 {#adding-portlets-to-your-aem-page}

使用Portal元件將Portlet視窗新增至您的網頁。 使用元件屬性來指定要顯示的Portlet。

1. 在網頁上，拖曳 **Portlet** 元件從Sidekick中的General群組移至頁面。

   >[!NOTE]
   >
   >將元件拖曳至頁面後，請重新載入頁面以確保其正常運作。

1. 連按兩下元件以開啟Portlet屬性。
1. 在 **Portlet實體** 下拉式功能表，從清單中選取portlet。
1. 選取或清除**隱藏標題列**核取方塊，視您是否要檢視Portlet的標題列而定。
1. 在 **Portlet視窗** 視需要輸入唯一的Portlet視窗ID。

   >[!NOTE]
   >
   >如果您打算在相同頁面上多次使用相同的Portlet，請為每個Portlet指定不同的視窗ID。

1. 单击&#x200B;**确定**。Portlet會顯示在您的AEM頁面上。

   ![chlimage_1-136](assets/chlimage_1-136.png)

## 在Portlet中安裝、設定和使用AEM {#installing-configuring-and-using-aem-in-a-portlet}

若要存取AEM WCM提供的內容，入口網站伺服器必須安裝AEM Portal Director Portlet。 若要這麼做，請使用本節提供的步驟，安裝、設定Portlet並將其新增至入口網站頁面。

依預設，Portlet會連線至localhost：4503的發佈執行個體和localhost：4502的製作執行個體。 這些值可在部署Portlet期間變更。 入口網站導向程式可在/libs/portal/directory下的存放庫中作為內容使用。 您必須先下載應用程式war檔案，才能使用它。

### 正在下載war檔案 {#downloading-the-war-file}

1. 使用Webdav或CRXDE Lite，導覽至/libs/portal/director。

1. 下載 *cq-portlet-webapp.war*.

>[!NOTE]
>
>這些程式使用Websphere入口網站作為範例，儘管它們儘可能通用；請注意，其他入口網站的程式有所不同。 雖然這些步驟對於所有入口網站來說基本上都相同，但您需要為特定入口網站重新使用步驟。

#### 安裝Portlet {#installing-the-portlet}

若要安裝Portlet：

1. 以管理員許可權登入入口網站。
1. 導覽至您入口網站的「Portlet管理」部分。
1. 按一下安裝，然後瀏覽至您下載的AEM portlet應用程式(cq-portlet-webapp.war)，並輸入有關portlet的其他重要資訊。

   如需其他重要的Portlet資訊，您可以接受預設值或變更值。 如果您接受預設值，可在https://取得Portlet&lt;wps-host>：&lt;port>/wps/PA_CQ5_Portlet。 Portlet提供的OSGi管理主控台位於https://&lt;wps-host>：&lt;port>/wps/ PA_CQ5_Portlet/cqbridge/system/console （預設使用者名稱/密碼為admin/admin）。

1. 選取該選項或核取方塊，並儲存變更，以確保Portlet應用程式自動啟動。 您會看到安裝成功的訊息。

#### 設定Portlet {#configuring-the-portlet}

安裝Portlet後，您需要加以設定，好讓它知道基礎AEM執行個體（製作和發佈）的URL。 您也可以設定其他選項。

若要設定Portlet：

1. 在應用程式伺服器的入口網站管理視窗中，導覽至Portlet管理（其中列出所有Portlet），然後選取AEM Portal Director Portlet。
1. 視需要設定Portlet。 例如，您可能需要變更作者和發佈執行個體的URL，以及開始路徑的URL。 有關預設設定的說明，請參見 [Portlet喜好設定](/help/sites-administering/aem-as-portal.md#portlet-preferences).

   >[!NOTE]
   >
   >如果將Portlet設定為連線到在/**以外的內容路徑上執行的AEM作者和發佈執行個體**則需要啟用此強制功能 **CQUrlInfo** 在這些AEM例項的Html資料庫管理員設定中（例如透過Felix Webconsole），或編輯將無法運作，且不會顯示偏好設定對話方塊。

1. 將設定變更儲存在應用程式伺服器中。

1. 導覽至Portlet的OSGI Admin Console。 預設位置為 `https://<wps-host>:<port>/wps/PA_CQ5_Portlet/cqbridge/system/console/configMgr`. 預設的使用者名稱/密碼為 **管理員/管理員**.

1. 選取 **Day Portal Director CQ伺服器設定** 設定並編輯下列值：

   * **作者基本URL**：AEM編寫執行個體的基底URL。
   * **發佈基底URL**：AEM發佈執行個體的基底URL。
   * **作者作為發佈使用**：作者例項是否作為發佈例項（用於開發）？

   ![chlimage_1-137](assets/chlimage_1-137.png)

1. 单击“**保存**”。您現在可以將Portlet新增至入口網站頁面，並使用入口網站。

### 內容URL {#content-urls}

從AEM請求內容時，Portlet會使用目前的顯示模式（發佈或作者）和目前的路徑來組合完整的URL。 使用預設值時，第一個URL為 `https://localhost:4503/content/geometrixx/en.portlet.html`. 的值 `htmlSelector` 會自動新增至副檔名之前的URL。

如果Portlet切換到說明模式，並且 `appendHelpViewModeAsSelector` 選取「 」，然後 `help` 也會附加選擇器，例如 `https://localhost:4503/content/geometrixx/en.portlet.html.help`. 如果Portlet視窗最大化，且 `appendMaxWindowStateAsSelector` ，則會附加選取器，例如， `https://localhost:4503/content/geometrixx/en.portlet.max.help`.

可以在AEM中評估選擇器，不同的選擇器可以使用不同的範本。

### 在AEM中使用內容Url對應 {#using-a-content-url-map-in-aem}

通常起始路徑會直接指向AEM中的內容。 不過，如果您想要在AEM中而不是在Portlet偏好設定中維護開始路徑，您可以在AEM中將開始路徑指向內容地圖，例如 `/var/portlets`. 在這種情況下，在AEM中執行的指令碼可以使用從Portlet提交的資訊來決定哪個URL是起始URL。 它應該會發出重新導向至正確URL的訊息。

#### 將Portlet新增至入口網站頁面 {#adding-the-portlet-to-the-portal-page}

若要將Portlet新增至入口網站頁面：

1. 請確定您位於應用程式伺服器的管理視窗，並導覽至您管理頁面的位置。 (例如，在WebSphere 6.1中，按一下 **管理頁面**)。
1. 選取Portlet的名稱，然後選取現有頁面或建立新頁面。
1. 編輯頁面配置。
1. 選取Portlet並將其新增至容器。
1. 儲存您的變更。

#### 使用Portlet {#using-the-portlet}

若要存取您新增至Portlet的頁面：

1. 在Portlet的個人化功能表中，依照您在入口網站中的設定來設定Portlet。
1. 開啟設定（Portlet會顯示在Portlet設定中設定的發佈開始URL）並視需要進行編輯，然後儲存。
