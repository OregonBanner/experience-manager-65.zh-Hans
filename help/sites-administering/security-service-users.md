---
title: AEM中的服務使用者
seo-title: Service Users in AEM
description: 瞭解AEM中的服務使用者。
seo-description: Learn about Service Users in AEM.
uuid: 4efab5fb-ba11-4922-bd68-43ccde4eb355
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 9cfe5f11-8a0e-4a27-9681-a8d50835c864
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Security
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 0%

---

# AEM中的服務使用者{#service-users-in-aem}

## 概述 {#overview}

在AEM中取得管理工作階段或資源解析程式的主要方式是使用 `SlingRepository.loginAdministrative()` 和 `ResourceResolverFactory.getAdministrativeResourceResolver()` Sling提供的方法。

然而，這兩種方法都不是針對 [最低許可權原則](https://en.wikipedia.org/wiki/Principle_of_least_privilege) 並且讓開發人員很容易不去為內容規劃適當的結構和對應的存取控制層級(ACL)。 如果此類服務中存在漏洞，則通常會導致將許可權升級至 `admin` 使用者，即使程式碼本身不需要管理許可權即可運作。

## 如何逐步淘汰管理員工作階段 {#how-to-phase-out-admin-sessions}

### 優先順序0：功能是否啟用/需要/已棄用？ {#priority-is-the-feature-active-needed-derelict}

某些情況下可能未使用管理員工作階段，或功能完全停用。 如果您的實作是這種情況，請確定您完全移除功能或將其符合 [NOP代碼](https://en.wikipedia.org/wiki/NOP).

### 優先順序1：使用請求工作階段 {#priority-use-the-request-session}

儘可能重構您的功能，以便使用已驗證的指定請求工作階段來讀取或寫入內容。 如果無法這麼做，通常可依照下列優先順序套用優先順序來達成。

### 優先順序2：重新建構內容 {#priority-restructure-content}

許多問題都可透過重新建構內容來解決。 進行重新建構時，請記住以下簡單規則：

* **變更存取控制**

   * 確定真正需要存取許可權的使用者或群組確實擁有存取權；

* **調整內容結構**

   * 將其移至其他位置，例如存取控制與可用的請求工作階段相符的位置；
   * 變更內容粒度；

* **重構您的程式碼以成為適當的服務**

   * 將商業邏輯從JSP程式碼移動到服務。 這允許不同的內容模式。

此外，請確定您開發的任何新功能都遵守以下原則：

* **安全性需求應驅動內容結構**

   * 管理存取控制應該感覺很自然
   * 存取控制必須由存放庫而非應用程式執行

* **使用節點型別**

   * 限制可設定的屬性集

* **尊重隱私權設定**

   * 若是私人設定檔，其中一個範例是不公開私人設定檔圖片、電子郵件或全名 `/profile` 節點。

## 嚴格存取控制 {#strict-access-control}

無論您在重新建構內容時套用存取控制，還是為新的服務使用者執行此動作時，都必須儘可能套用最嚴格的ACL。 使用存取控制的所有可能設施：

* 例如，不要套用 `jcr:read` 於 `/apps`，僅將其套用至 `/apps/*/components/*/analytics`

* 使用 [限制](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* 為節點型別套用ACL
* 限制許可權

   * 例如，當只需要編寫屬性時，不要給出 `jcr:write` 許可權；使用 `jcr:modifyProperties` 而非

## 服務使用者和對應 {#service-users-and-mappings}

如果上述操作失敗，Sling 7提供服務使用者對應服務，可設定套件與使用者對應和兩個對應的API方法： ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)` 和 ` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` 只會傳回具有已設定使用者許可權的工作階段/資源解析程式。 這些方法具有下列特性：

* 它們允許對應服務到使用者
* 它們使得定義子服務使用者成為可能
* 中心設定點為： `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [ 「：」子服務名稱 ] 

* `service-id` 對應到資源解析程式和/或JCR存放庫使用者ID以進行驗證
* `service-name` 是提供服務的套件組合之符號名稱

## 其他Recommendations {#other-recommendations}

### 以服務使用者取代管理工作階段 {#replacing-the-admin-session-with-a-service-user}

服務使用者是JCR使用者，沒有設定密碼以及執行特定工作所需的最小許可權集。 未設定密碼表示無法以服務使用者登入。

取代管理工作階段的方法是使用服務使用者工作階段來取代它。 如有需要，也可由多位子服務使用者取代。

若要以服務使用者取代管理工作階段，您應該執行下列步驟：

1. 識別您服務的必要許可權，並牢記最低許可權原則。
1. 檢查是否有使用者可完全依照您需要的許可權設定使用。 如果沒有任何現有使用者符合您的需求，請建立新的系統服務使用者。 需要RTC才能建立新的服務使用者。 有時候，建立多個子服務使用者（例如，一個用於寫入，一個用於讀取）以進一步劃分存取權是有意義的。
1. 為您的使用者設定和測試ACE。
1. 新增 `service-user` 對應您的服務和 `user/sub-users`

1. 讓服務使用者sling功能可供您的套件使用：更新至最新版本的 `org.apache.sling.api`.

1. 取代 `admin-session` 在程式碼中使用 `loginService` 或 `getServiceResourceResolver` API。

## 建立新的服務使用者 {#creating-a-new-service-user}

在您確認AEM服務使用者清單中的任何使用者都不適用於您的使用案例，且對應的RTC問題已核准後，您可以繼續並將新使用者新增至預設內容。

建議的方法是建立服務使用者，以便在以下位置使用存放庫總管： *https://&lt;server>：&lt;port>/crx/explorer/index.jsp*

目標是取得有效的 `jcr:uuid` 屬性，這是透過內容套件安裝建立使用者時的必要屬性。

您可以透過以下方式建立服務使用者：

1. 前往存放庫總管： *https://&lt;server>：&lt;port>/crx/explorer/index.jsp*
1. 以管理員身分登入，方法是按下 **登入** 連結（位於畫面的左上角）。
1. 接下來，建立您的系統使用者並為其命名。 若要將使用者建立為系統使用者，請將中間路徑設定為 `system` 並根據您的需求新增可選的子資料夾：

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. 確認您的系統使用者節點如下所示：

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >請注意，沒有任何與服務使用者相關聯的mixin型別。 這表示系統使用者沒有存取控制原則。

將對應的.content.xml新增至套件組合的內容時，請確定您已設定 `rep:authorizableId` 而且主要型別為 `rep:SystemUser`. 看起來應該像這樣：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## 新增組態修正至ServiceUserMapper組態 {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

若要將服務對應新增至對應的系統使用者，您需要為建立工廠組態 ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)` 服務。 若要保持此模組化，可以使用 [Sling修正機制](https://issues.apache.org/jira/browse/SLING-3578). 建議在套件中安裝此類設定的方式是使用 [Sling初始內容載入](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html)：

1. 在套件的src/main/resources資料夾下方建立子資料夾SLING-INF/content
1. 在此資料夾中建立名為org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.modified-&lt;some unique=&quot;&quot; name=&quot;&quot; for=&quot;&quot; your=&quot;&quot; factory=&quot;&quot; configuration=&quot;&quot;>.xml與工廠設定的內容（包括所有子服務使用者對應）。 示例:

1. 建立 `SLING-INF/content` 資料夾位於 `src/main/resources` 資料夾；
1. 在此資料夾中建立檔案 `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` 包含您工廠設定的內容，包括所有子服務使用者對應。

   為了方便說明，請取一個名為 `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <node>
       <primaryNodeType>sling:OsgiConfig</primaryNodeType>
       <property>
           <name>user.default</name>
           <value></value>
       </property>
       <property>
           <name>user.mapping</name>
           <values>
               <value>com.adobe.granite.auth.saml=authentication-service</value>
           </values>
       </property>
   </node>
   ```

1. 在的設定中參考Sling初始內容 `maven-bundle-plugin` 在 `pom.xml` 您的套件組合。 示例:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. 安裝您的套件組合，並確認已安裝工廠組態。 您可以执行以下操作来实现此目标：

   * 前往網頁主控台： *https://serverhost:serveraddress/system/console/configMgr*
   * 搜尋 **Apache Sling Service使用者對應程式服務修正**
   * 按一下連結，檢視是否有正確的設定。

## 在服務中處理共用工作階段 {#dealing-with-shared-sessions-in-services}

呼叫目標 `loginAdministrative()` 通常會與共用工作階段一起出現。 這些工作階段會在服務啟動時取得，並只會在服務停止後登出。 雖然這是常見做法，但會導致兩個問題：

* **安全性：** 此類管理工作階段用於快取和傳回繫結至共用工作階段的資源或其他物件。 稍後在呼叫棧疊中，這些物件可以適應具有更高許可權的工作階段或資源解析器，並且呼叫者通常不清楚它是否是他們正在操作的管理員工作階段。
* **效能：** 在Oak共用工作階段中，可能會導致效能問題，目前不建議使用它們。

針對安全性風險最明顯的解決方案是直接取代 `loginAdministrative()` 使用呼叫 `loginService()` 一對一給具有受限制許可權的使用者。 但是，這不會對任何潛在的效能降低造成任何影響。 緩解這種情況的一個可能方式是，將所有請求的資訊包裝在與工作階段無關聯的物件中。 接著，依需求建立（或銷毀）工作階段。

建議的方法是重構服務的API，讓呼叫者能夠控制工作階段的建立/破壞。

## JSP中的管理階段作業 {#administrative-sessions-in-jsps}

JSP無法使用 `loginService()`，因為沒有關聯的服務。 不過，JSP中的管理階段作業通常是違反MVC範例的標誌。

此問題可透過兩種方式修正：

1. 重新建構內容，以便透過使用者工作階段操控內容；
1. 將邏輯擷取至提供可供JSP使用的API的服務。

首選方法是第一個方法。

## 處理事件、複製前置處理器和工作 {#processing-events-replication-preprocessors-and-jobs}

處理事件或作業時，以及在某些情況下，工作流程通常會遺失觸發事件的對應工作階段。 這會導致事件處理常式和工作處理常式使用管理工作階段來執行其工作。 解決此問題的各種可行方法各有優缺點：

1. 傳遞 `user-id` 在事件裝載中，並使用模擬。

   **優點：** 使用方便。

   **缺點：** 仍使用 `loginAdministrative()`. 它會重新驗證已驗證的請求。

1. 建立或重新使用可存取資料的服務使用者。

   **優點：** 與目前的設計一致。 需要最小的變更。

   **缺點：** 需要功能非常強大的服務使用者靈活處理，這很容易導致許可權提升。 規避安全性模型。

1. 傳遞序列化 `Subject` 在事件裝載中，並建立 `ResourceResolver` 根據該主題而定。 例如，使用JAAS `doAsPrivileged` 在 `ResourceResolverFactory`.

   **優點：** 從安全性角度來重新定義實作。 它可避免重新驗證，並以原始許可權運作。 安全性相關程式碼對事件的消費者而言是透明的。

   **缺點：** 需要重構。 安全性相關程式碼對事件的取用者而言是透明的，也可能會導致問題。

第三種方法是目前偏好的處理技術。

## 工作流程程式 {#workflow-processes}

在工作流程流程實作中，通常會遺失觸發工作流程的對應使用者工作階段。 這會導致工作流程處理經常使用管理工作階段來執行其工作。

若要修正這些問題，建議您使用中提到的相同方法 [處理事件、複製前置處理器和工作](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) 使用。

## SlingPOST處理器與已刪除的頁面 {#sling-post-processors-and-deleted-pages}

SlingPOST處理器實作中有幾個管理工作階段。 管理工作階段通常用於存取正在處理的POST內擱置刪除的節點。 因此，無法再透過請求工作階段使用這些變數。 可能會存取擱置刪除的節點，以公開原本不可存取的中繼資料。
