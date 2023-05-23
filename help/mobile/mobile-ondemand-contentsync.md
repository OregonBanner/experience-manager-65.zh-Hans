---
title: 透過內容同步處理行動
description: 請依照本頁瞭解Content Sync。 在AEM中編寫的頁面可作為應用程式內容，即使裝置離線亦然。 此外，由於AEM頁面是根據網頁標準，因此可跨平台運作，讓您將其內嵌在任何原生包裝函式中。 此策略可減少開發工作量，並可讓您輕鬆更新應用程式內容。
uuid: 11f74cc5-99a5-4186-9b60-b19351305432
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 8fb70ca4-86fc-477d-9773-35b84d5e85a8
exl-id: a6e59334-09e2-4bb8-b445-1868035da556
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '2995'
ht-degree: 0%

---

# 透過內容同步處理行動{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

使用Content Sync來封裝內容，以便在原生行動應用程式中使用。 在AEM中編寫的頁面可作為應用程式內容，即使裝置離線亦然。 此外，由於AEM頁面是根據網頁標準，因此可跨平台運作，讓您將其內嵌在任何原生包裝函式中。 此策略可減少開發工作量，並可讓您輕鬆更新應用程式內容。

Content Sync架構會建立包含網頁內容的封存檔案。 內容可以是簡單頁面、影像和PDF檔案的任何內容，或是整個網頁應用程式。 內容同步API提供從行動應用程式或建置程式存取封存檔案的許可權，以便內容可擷取並包含在應用程式中。

下列步驟順序說明了Content Sync的典型使用案例：

1. AEM開發人員會建立Content Sync設定，指定要包含的內容。
1. 內容同步架構會收集並快取內容。
1. 在行動裝置上，行動應用程式會啟動，並從伺服器要求內容（以ZIP檔案傳送）。
1. 使用者端會將ZIP內容解壓縮至本機檔案系統。 ZIP檔案中的資料夾結構會模擬使用者端（例如瀏覽器）一般會從伺服器要求的路徑。
1. 使用者端會在內嵌瀏覽器中開啟內容，或以其他方式使用內容。
1. 稍後，使用者端會向伺服器要求更新內容。 內容同步架構提供漸進式更新，以減少下載大小與時間，由於頻寬或資料量有限，這對於行動裝置而言可能很重要。

## 開發內容同步處理常式 {#developing-the-content-sync-handlers}

開發「內容同步處理常式」的部分准則如下：

* 處理常式必須實施 *com.day.cq.contentsync.handler.ContentUpdateHandler* （直接或擴充具有下列功能的類別）
* 處理常式可以擴充 *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 處理常式只有在更新ContentSync快取時，才能報告true。 若誤報true，AEM會在實際並未發生更新時建立更新。
* 只有在內容實際變更時，處理常式才能更新快取。 如果不需要白色，請勿寫入快取。 這會導致建立不必要的更新。

>[!NOTE]
>
>啟用 *ContentSync偵錯記錄* 透過封裝上的OSGI記錄器設定 *com.day.cq.contentsync*. 這允許追蹤哪些處理常式已執行，以及它們是否更新快取並報告更新快取。

## 設定內容同步內容 {#configuring-the-content-sync-content}

建立Content Sync設定，以指定傳送至使用者端的ZIP檔案內容。 您可以建立任意數量的Content Sync設定。 每個設定都有名稱用於識別。

若要建立Content Sync設定，請新增 `cq:ContentSyncConfig` 節點到存放庫，使用 `sling:resourceType` 屬性設定為 `contentsync/config`. 此 `cq:ContentSyncConfig` 節點可以位於存放庫中的任何位置，但AEM發佈執行個體上的使用者必須可以存取該節點。 因此，您應該在下方新增節點 `/content`.

若要指定Content Sync ZIP檔案的內容，請將子節點新增至cq：ContentSyncConfig節點。 每個子節點的下列屬性會識別要包含的內容專案，以及新增時如何處理該專案：

* `path`：內容的位置。
* `type`：用於處理內容的設定型別名稱。 有數種型別可供使用，並在一節中加以說明 *設定型別*.

另請參閱 *內容同步設定範例* 以取得詳細資訊。

建立Content Sync設定後，該設定會顯示在Content Sync主控台中。

>[!NOTE]
>
>內容同步架構不會檢查資產與設計相關檔案的相依性是否包含在內容同步套件中。 請確定在ZIP檔案中包含所有必要的檔案。

### 設定Content Sync下載的存取權 {#configuring-access-to-content-sync-downloads}

指定可從Content Sync下載的使用者或群組。 您可以設定可從所有Content Sync快取下載的預設使用者或群組，也可以覆寫特定Content Sync設定的預設並設定存取權。

安裝AEM後，管理員群組的成員預設可從Content Sync下載。

#### 設定Content Sync下載的預設存取權 {#setting-the-default-access-for-content-sync-downloads}

Day CQ Content Sync Manager服務可控制Content Sync的存取權。 設定此服務以指定預設可從Content Sync下載的使用者或群組。

如果您是 [使用Web主控台設定服務](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)，輸入使用者或群組的名稱，作為「可授權的遞補快取」屬性的值。

如果您是 [在存放庫中設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)，使用下列服務相關資訊：

* PID： com.day.cq.contentsync.impl.ContentSyncManagerImpl
* 屬性名稱： contentsync.fallback.authorizable

#### 覆寫內容同步快取的下載存取權 {#overriding-download-access-for-a-content-sync-cache}

若要設定特定內容同步設定的下載存取權，請將下列屬性新增至 `cq:ContentSyncConfig` 節點：

* 名稱：可授權
* 型別：字串
* 值：可下載的使用者或群組名稱。

例如，您的應用程式可讓使用者直接從Content Sync安裝更新。 若要讓所有使用者都能下載更新，您可以將可授權屬性的值設為 `everyone`.

如果 `cq:ContentSyncConfig` 節點沒有可授權屬性，為Day CQ Content Sync Manager服務的Fallback Cache Authorizable屬性設定的預設使用者或群組會決定誰可以下載。

### 設定使用者以更新內容同步快取 {#configuring-the-user-for-updating-a-content-sync-cache}

當使用者執行內容同步快取的更新時，特定使用者帳戶會代表使用者執行動作。 匿名使用者預設會更新所有Content Sync快取。

您可以覆寫預設使用者，並指定使用者或群組來更新特定的Content Sync快取。

若要覆寫預設使用者，請指定使用者或群組，將下列屬性新增至cq：ContentSyncConfig節點，以針對特定Content Sync設定執行更新：

* 名称: `updateuser`
* 类型: `String`
* 值：可執行更新的使用者或群組名稱。

如果 `cq:ContentSyncConfig` 節點沒有 `updateuser` 屬性，預設 `anonymous` 使用者更新快取。

### 設定型別 {#configuration-types}

處理範圍包括從呈現簡單的JSON到完全呈現頁面（包括其參考資產）。 本節列出可用的組態型別及其特定引數：

**複製** 只要複製檔案和資料夾即可。

* **路徑**  — 如果路徑指向單一檔案，則只會複製該檔案。 如果它指向資料夾（這包含頁面節點），則會複製下面的所有檔案和資料夾。

**內容** 使用標準呈現內容 [Sling請求處理](/help/sites-developing/the-basics.md#sling-request-processing).

* **路徑**  — 應輸出的資源路徑。
* **擴充功能**  — 請求中應使用的擴充功能。 常見範例為 *html* 和 *json*，但任何其他擴充功能皆可使用。

* **選擇器**  — 選用的選取器，以點分隔。 常見範例為 *觸控* 用於呈現頁面的行動版本或 *無限* 用於JSON輸出。

**clientlib** 封裝Javascript或CSS使用者端程式庫。

* **路徑**  — 使用者端資料庫根的路徑。
* **擴充功能**  — 使用者端資料庫的型別。 這應該設定為 *js* 或 *css* 目前。

**資產**

收集資產的原始轉譯。

* **路徑** - /content/dam下方的資產資料夾路徑。

**影像** 收集影像。

* **路徑**  — 影像資源的路徑。

影像型別用於在zip檔案中包含We Retail標誌。

**頁面** 轉譯AEM頁面並收集引用的資產。

* **路徑**  — 頁面的路徑。
* **擴充功能**  — 請求中應使用的擴充功能。 對於頁面，這幾乎永遠都是 *html*，但仍可使用其他選項。

* **選擇器**  — 選用的選取器，以點分隔。 常見範例為 *觸控* 用於轉譯頁面的行動版本。

* **深入**  — 決定是否應包含子頁面的選用布林屬性。 預設值為 *true。*

* **includeImage**  — 決定是否應包含影像的選用布林屬性。 預設值為 *true*.

   依預設，只會考慮包含資源型別為foundation/components/image的影像元件。 您可以透過設定 **Day CQ WCM頁面更新處理常式** 在Web主控台中。

**重寫** rewrite節點會定義如何在匯出的頁面中重新寫入連結。 重寫的連結可以指向zip檔案中包含的檔案，也可以指向伺服器上的資源。

此 `rewrite` 節點必須位於 `page` 節點。

此 `rewrite` 節點可以具有下列一或多個屬性：

* `clientlibs`：重寫clientlibs路徑。

* `images`：重寫影像路徑。
* `links`：重寫連結路徑。

每個屬性可以有下列其中一個值：

* `REWRITE_RELATIVE`：以檔案系統上頁面.html檔案的相對位置重寫路徑。

* `REWRITE_EXTERNAL`：使用AEM指向伺服器上的資源來重寫路徑 [外部化器服務](/help/sites-developing/externalizer.md).

AEM服務已呼叫 **PathRewriterTransformerFactory** 可讓您設定將重寫的特定html屬性。 此服務可在Web主控台中設定，並且每個屬性的設定都為 `rewrite` 節點： `clientlibs`， `images` 和 `links`.

AEM 5.5已新增此功能。

### 內容同步設定範例 {#example-content-sync-configuration}

以下清單顯示Content Sync的設定範例。

```xml
+ weretail_go [cq:ContentSyncConfig]
  - sling:resourceType = "contentsync/config"

  + etc.designs.default [nt:unstructured]
    - path = "/etc/designs/default"
    - type = "copy"

  + etc.designs.mobile [nt:unstructured]
    - path = "/etc/designs/mobile"
    - type = "copy"

  + events.plist [nt:unstructured]
    - path = "/content/weretail_mobile/en/events/jcr:content/par/events"
    - type = "content"
    - extension = "plist"

  + events.touch.html [nt:unstructured]
    - path = "/content/weretail_mobile/en/events"
    - type = "pages"
    - extension = "html"
    - selector = "touch"

  + logo [nt:unstructured]
    - path = "/etc/designs/mobile/jcr:content/mobilecontentpage/logo"
    - type = "logo"

  + manifest [nt:unstructured]
    - indexPage = "/content/weretail_mobile/en/events.touch.html"
    - metadataPlist = "/content/weretail_mobile/en/events/_jcr_content/par/events.plist"

  + ...
```

**etc.designs.default和etc.designs.mobile** 設定的前兩個專案應該相當明顯。 由於我們將包含許多行動頁面，因此我們需要/etc/designs底下的相關設計檔案。 而且由於不需要額外處理，因此只需複製即可。

**events.plist** 此專案有些特殊。 如簡介中所述，應用程式應提供包含事件位置標籤的地圖檢視。 我們將以PLIST格式的個別檔案形式提供必要的位置資訊。 為了讓此功能發揮作用，索引頁面上使用的事件清單元件有一個名為plist.jsp的指令碼。 當以.plist副檔名請求元件的資源時，執行此指令碼。 像往常一樣，元件路徑在path屬性中給出，而型別設定為content，因為我們想要運用 [Sling請求處理](/help/sites-developing/the-basics.md#sling-request-processing).

**events.touch.html** 接下來是將顯示在應用程式中的實際頁面。 path屬性會設定為事件的根頁面。 該頁面下方的所有事件頁面也會包括在內，因為深層屬性預設為true。 我們使用頁面作為設定型別，因此其中會包含任何可從頁面上的影像或下載元件參照的影像或其他檔案。 此外，設定觸控選擇器可提供頁面的行動版本。 Feature Pack中的設定包含更多此類專案，但為了簡單起見，這裡未予列出。

**標誌** 目前尚未提及標誌設定型別，而且不屬於任何內建型別。 不過，內容同步架構在某種程度上可以擴展，以下章節將介紹相關範例。

**資訊清單** 在zip檔案中通常最好包含某種中繼資料，例如內容的起始頁面。 不過，以硬式編碼撰寫這類資訊，可防止您日後輕易加以變更。 內容同步架構可在設定中尋找資訊清單節點，以支援此使用案例，資訊清單節點僅由名稱識別，不需要設定型別。 在該特定節點上定義的每個屬性都會新增至檔案（也稱為manifest），並位於zip檔案的根目錄中。

在此範例中，事件清單頁面應該是初始頁面。 此資訊提供於 **indexPage** 屬性，因此隨時都能輕鬆變更。 第二個屬性會定義 *events.plist* 檔案。 如我們稍後所見，使用者端應用程式現在可以讀取資訊清單並根據資訊清單採取行動。

設定好設定後，您就可以使用瀏覽器或任何其他HTTP使用者端下載內容，或者，如果您正在針對iOS開發，則可以使用專用的WAppKitSync使用者端程式庫。 下載位置由設定的路徑和 *.zip* 擴充功能(例如，使用本機AEM例項時)： *http://localhost:4502/content/weretail_go.zip*

### 內容同步主控台 {#the-content-sync-console}

Content Sync主控台會列出存放庫中的所有Content Sync設定（所有型別的節點） `cq:ContentSyncConfig`)並針對每個設定，允許您進行以下操作：

* 更新快取。
* 清除快取。
* 下載完整的壓縮檔。
* 下載現在與特定日期和時間的壓縮檔。

這對於開發和疑難排解非常有用。

可在以下位置存取主控台：

`http://localhost:4502/libs/cq/contentsync/content/console.html`

如下所示：

![chlimage_1-50](assets/chlimage_1-50.png)

### 擴充內容同步架構 {#extending-the-content-sync-framework}

雖然設定選項的數量已經相當龐大，但可能無法涵蓋您特定使用案例的所有需求。 本節說明Content Sync架構的擴充功能點，以及如何建立自訂設定型別。

每種設定型別都有 *內容更新處理常式*，此元件工廠是為該特定型別註冊的OSGi元件工廠。 這些處理常式會收集和處理內容，然後將其新增至由Content Sync架構維護的快取。 實作下列介面或抽象基底類別：

* `com.day.cq.contentsync.handler.ContentUpdateHandler`  — 所有更新處理常式都需要實作的介面
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler`  — 抽象類別，使用Sling簡化資源的呈現

將類別註冊為OSGi元件工廠，並將其部署在套件組合的OSGi容器中。 這可以透過以下方式完成： [Maven SCR外掛程式](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/apache-felix-maven-scr-plugin-use.html) 使用JavaDoc標籤或註解。 下列範例顯示JavaDoc版本：

```java
/*
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/customtype"
 */
public class CustomTypeUpdateHandler implements ContentUpdateHandler {
    // add your code here
}

/*
 * @scr.component metatype="no" inherit="true"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/othertype"
 */
public class OtherTypeUpdateHandler extends AbstractSlingResourceUpdateHandler {
    // add your code here
}
```

請注意 *工廠* 定義包含通用介面和以斜線分隔的自訂型別。 此策略可讓內容同步架構在辨識設定專案中的自訂型別時，尋找和建立自訂類別的執行個體。 下一節提供自訂更新處理常式的具體範例。

>[!CAUTION]
>
>以AbstractSlingResourceUpdateHandler基底類別建置時，您必須新增 *繼承* 定義。 否則，OSGi容器不會設定在基底類別中宣告的必要參考。

### 實作自訂更新處理常式 {#implementing-a-custom-update-handler}

每個We.Retail Mobile頁面左上角都有標誌，當然是我們要加到zip檔案中。 不過，針對快取最佳化，AEM不會參考影像檔案在存放庫中的實際位置，這可防止我們單純使用 **複製** 設定型別。 反之，我們需要做的是提供我們自己的 **標誌** 在AEM要求的位置提供影像的設定型別。 下列程式碼清單顯示完整的標誌更新處理常式實作：

#### LogoUpdateHandler.java {#logoupdatehandler-java}

```java
package com.day.cq.wcm.apps.weretail.impl;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.day.cq.commons.jcr.JcrUtil;
import com.day.cq.contentsync.config.ConfigEntry;
import com.day.cq.contentsync.handler.ContentUpdateHandler;
import com.day.cq.wcm.foundation.Image;
import com.day.text.Text;

/**
 * The <code>LogoUpdateHandler</code> is used to update the content sync cache
 * with a page logo added using a logo component.
 *
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/logo"
 */
public class LogoUpdateHandler implements ContentUpdateHandler {

    private static final Logger log = LoggerFactory.getLogger(LogoUpdateHandler.class);

    /** @scr.reference policy="static" */
    protected JcrResourceResolverFactory resolverFactory;

    public boolean updateCacheEntry(ConfigEntry configEntry, Long lastUpdated, String configCacheRoot, Session admin, Session session) {
        ResourceResolver resolver = resolverFactory.getResourceResolver(admin);
        Resource resource = resolver.getResource(configEntry.getContentPath());

        Image img = new Image(resource);
        img.setItemName(Image.NN_FILE, "image");
        img.setItemName(Image.PN_REFERENCE, "imageReference");
        img.setSelector("img");

        try {
            if(img.getLastModified() == null || lastUpdated < img.getLastModified().getTime().getTime()) {
                String src = img.getSrc();
                String parentPath = configCacheRoot + Text.getRelativeParent(src, 1);

                Node parent = JcrUtil.createPath(parentPath, "sling:Folder", admin);
                Node image = resolver.getResource(resource.getPath() + "/image").adaptTo(Node.class);
                JcrUtil.copy(image, parent, Text.getName(src));

                admin.save();

                return true;
            }
        } catch (RepositoryException e) {
            log.error("Unexpected error while updating logo: ", e);
        }

        return false;
    }
}
```

此 `LogoUpdateHandler` 類別實作 `ContentUpdateHandler` 介面的 `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` 方法，會採用多個引數：

* A `ConfigEntry` 提供設定專案（其處理常式為之）及其屬性的存取權的執行個體。
* A `lastUpdated` 時間戳記，指出Content Sync上次更新其快取的時間。 處理常式不應更新在該時間戳記之後未修改的內容。
* A `configCacheRoot` 指定快取根路徑的引數。 所有更新的檔案都必須儲存在此路徑下方，才能新增至zip檔案。
* 用於所有快取相關存放庫操作的管理工作階段。
* 可用於更新特定使用者內容中的內容並因此提供某種個人化內容的使用者工作階段。

若要實作自訂處理常式，請先根據設定專案中指定的資源建立Image類別的執行個體。 此程式基本上與頁面上實際的標誌元件所執行的程式相同。 它可確保影像的目標路徑與頁面所參照的路徑相同。

接下來，檢查自上次更新後是否修改了資源。 自訂實施應避免快取不必要的更新，若沒有變更則傳回false。 如果資源已修改，請將影像複製到相對於快取根目錄的預期目標位置。 最後， `true` 會傳回，以向架構指出快取已更新。

## 在使用者端上使用內容 {#using-the-content-on-the-client}

若要在Content Sync提供的行動應用程式中使用內容，您需要透過HTTP或HTTPS連線要求內容。 因此，擷取的內容（封裝在ZIP檔案中）可以擷取並儲存在行動裝置本機。 請注意，內容不僅是指資料，也指邏輯，即完整的網頁應用程式，因此即使沒有網路連線，行動使用者也能執行擷取的Web應用程式和對應資料。

Content Sync會以智慧型方式提供內容：只會提供自上次成功資料同步處理以來的資料變更，藉此減少資料傳輸所需的時間。 自1970年1月1日起，首次執行應用程式資料變更時，系統就會要求變更，但隨後只會要求上次成功同步後變更的資料。 AEM利用iOS的使用者端通訊架構來簡化資料通訊和傳輸，因此只需極少數的原生程式碼，即可啟用以iOS為基礎的網頁應用程式。

所有傳輸的資料都可擷取到相同的目錄結構中，擷取資料時不需要執行額外的步驟（例如相依性檢查）。 若是iOS，所有資料都會儲存在iOS應用程式「檔案」資料夾內的子資料夾中。

iOS型AEM Mobile應用程式的典型執行路徑：

* 使用者在iOS裝置上啟動應用程式。
* 應用程式會嘗試連線至AEM後端，並請求自上次執行以來的資料變更。
* 伺服器會擷取有問題的資料，並將其壓縮到檔案中。
* 資料會傳回至使用者端裝置，並擷取至檔案資料夾。
* UIWebView元件開始/重新整理。

如果無法建立連線，將顯示先前下載的資料。

### 其他资源 {#additional-resources}

若要瞭解管理員和作者的角色和責任，請參閱以下資源：

* [為AEM Mobile On-demand Services編寫AEM內容](/help/mobile/mobile-apps-ondemand.md)
* [管理內容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
