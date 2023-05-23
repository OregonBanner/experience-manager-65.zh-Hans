---
title: AEM中的封閉式使用者群組
seo-title: Closed User Groups in AEM
description: 瞭解AEM中的封閉式使用者群組。
seo-description: Learn about Closed User Groups in AEM.
uuid: 83396163-86ce-406b-b797-2457ed975ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: a2bd7045-970f-4245-ad5d-a272a654df0a
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Security
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '6872'
ht-degree: 0%

---

# AEM中的封閉式使用者群組{#closed-user-groups-in-aem}

## 简介 {#introduction}

自AEM 6.3起，推出新的封閉使用者群組實作，旨在解決現有實作帶來的效能、擴充性和安全性問題。

>[!NOTE]
>
>為了簡單起見，本檔案將使用CUG縮寫。

新實作的目標是在必要時涵蓋現有功能，同時解決舊版本的問題和設計限制。 結果產生具有下列特性的新CUG設計：

* 明確區分驗證和授權元素，可個別或結合使用；
* 專用授權模型，反映已設定之CUG樹狀結構的受限讀取存取，而不會干擾其他存取控制設定和許可權要求；
* 將限制讀取存取的存取控制設定（通常在編寫執行個體上需要）與許可權評估（通常僅在發佈上需要）分開；
* 編輯受限制的讀取存取權而不提升許可權；
* 專用的節點型別擴充功能，可標示驗證需求；
* 與驗證需求相關聯的選擇性登入路徑。

### 新的自訂使用者群組實作 {#the-new-custom-user-group-implementation}

在AEM的環境中已知的CUG包含下列步驟：

* 限制需要保護的樹狀結構上的讀取存取權，並只允許讀取在特定CUG執行個體中列出或完全從CUG評估中排除的主參與者。 這稱為 **授權** 元素。
* 在指定的樹狀結構上強制執行驗證，並選擇性地為該樹狀結構指定後續排除的專用登入頁面。 這稱為 **驗證** 元素。

新實作的設計目的，是為了在驗證和授權元素之間劃出一條界線。 自AEM 6.3起，您可以限制讀取存取權，而不明確新增驗證需求。 例如，如果指定的執行個體完全需要驗證，或指定的樹狀結構已經位在需要驗證的子樹狀結構中。

同樣地，指定樹狀結構可標示驗證需求，而不需變更有效許可權設定。 組合和結果會列在 [結合CUG原則和驗證需求](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement) 區段。

## 概述 {#overview}

### 授權：限制讀取存取權 {#authorization-restricting-read-access}

CUG的主要功能是限制內容存放庫指定樹狀結構上，選取的主參與者以外的所有人的讀取存取權。 新實作不會即時操控預設存取控制內容，而是會透過定義代表CUG的專用型別存取控制政策，採取不同的方法。

#### CUG的存取控制原則 {#access-control-policy-for-cug}

此新型別的原則具有以下特性：

* org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy型別的存取控制原則（由Apache Jackrabbit API定義）；
* PrincipalSetPolicy授予許可權給可修改的主體集；
* 授與的許可權和原則的範圍是實作詳細資訊。

用於表示CUG的PrincipalSetPolicy實作還定義了：

* CUG原則僅授予一般JCR專案的讀取存取權（例如，排除存取控制內容）；
* 範圍由存取CUG原則的存取控制節點定義；
* CUG原則可以巢狀，巢狀CUG會啟動新的CUG，而不會繼承「父」CUG的主體集；
* 如果已啟用評估，則原則的效果會繼承至整個子樹狀結構下至下一個巢狀CUG。

這些CUG原則會透過名為oak-authorization-cug的獨立授權模組部署至AEM執行個體。 此模組提供自己的存取控制管理和許可權評估。 換言之，預設的AEM設定會提供結合了多個授權機制的Oak內容存放庫設定。 如需詳細資訊，請參閱 [Apache Oak檔案上的此頁面](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

在此複合設定中，新的CUG不會取代附加至目標節點的現有存取控制內容，而是設計為補充內容，稍後也可以移除，而不會影響原始存取控制(在AEM中預設為存取控制清單)。

相較於前者，新的CUG政策一律會被辨識及視為存取控制內容。 這表示它們是使用JCR存取控制管理API建立和編輯的。 如需詳細資訊，請參閱 [管理CUG原則](#managing-cug-policies) 區段。

#### CUG原則的許可權評估 {#permission-evaluation-of-cug-policies}

除了CUG的專用存取控制管理外，新的授權模型還允許有條件地啟用其原則的許可權評估。 這允許在中繼環境中設定CUG原則，並且僅在複製到生產環境後啟用有效許可權評估。

CUG原則的許可權評估，以及與預設或任何其他授權模型的互動，遵循為Apache Jackrabbit Oak中的多個授權機制設計的模式：若且唯若所有模型都授予存取權時，才會授予給定的一組許可權。 另請參閱 [此頁面](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) 以取得更多詳細資料。

以下特性適用於與設計用來處理和評估CUG原則的授權模型相關聯的許可權評估：

* 它只會處理一般節點和屬性的讀取許可權，不會讀取存取控制內容
* 它不處理修改受保護的JCR內容所需的寫入許可權或任何型別的許可權（存取控制、節點型別資訊、版本設定、鎖定或使用者管理等等）；這些許可權不受CUG原則影響，也不會由關聯的授權模型評估。 是否授予這些許可權取決於安全性設定中設定的其他模型。

單一CUG原則對許可權評估的影響可概述如下：

* 除了包含原則中所列排除的主體或主體的主體之外，拒絕所有人的讀取存取權；
* 此原則會在存放原則及其屬性的存取控制節點上生效；
* 該效果會另外沿階層繼承，即由存取控制節點定義的專案樹狀結構；
* 但是，它不會影響存取控制節點的同層級或祖系；
* 特定CUG的繼承會在巢狀CUG停止。

#### 最佳实践 {#best-practices}

在透過CUG定義受限讀取存取權時，應考量下列最佳實務：

* 針對您對CUG的需求是否與限制讀取存取權或驗證要求相關做出明智的決策。 若是後者，或同時需要這兩者，請參閱最佳實務一節，以取得驗證需求的詳細資訊
* 為需要保護的資料或內容建立威脅模型，以識別威脅邊界，並清楚瞭解資料的敏感度以及與授權存取相關的角色
* 為存放庫內容和CUG建模，並牢記一般授權相關方面和最佳實務：

   * 請記住，只有在特定CUG和設定授權中部署的其他模組評估允許特定主題讀取特定存放庫專案時，才會授予讀取許可權
   * 避免建立讀取存取權已受其他授權模組限制的備援CUG
   * 對巢狀CUG的過度需求可能會突顯內容設計中的問題
   * 對CUG的需求過度（例如，在每個單頁上）可能表示需要自訂授權模式，可能更適合符合手頭應用程式和內容的特定安全性需求。

* 將CUG原則支援的路徑限制在存放庫中的幾個樹狀結構，以允許最佳化的效能。 例如，僅允許/content節點底下的CUG作為自AEM 6.3以來的預設值出貨。
* CUG原則的設計目的，是要授予一小部分主體讀取許可權。 大量主體的需求可能會突顯內容或應用程式設計中的問題，並應重新考慮。

### 驗證：定義驗證需求 {#authentication-defining-the-auth-requirement}

CUG功能的驗證相關部分允許標籤需要驗證的樹狀結構，並選擇性地指定專用登入頁面。 根據舊版，新實作允許標籤需要在內容存放庫中驗證的樹狀結構，並有條件地啟用與 `Sling org.apache.sling.api.auth.Authenticator`負責最終強制要求並重新導向至登入資源。

這些需求會透過驗證器註冊，驗證器會透過提供 `sling.auth.requirements` 註冊屬性。 然後會使用這些屬性來動態擴充驗證需求。 如需詳細資訊，請參閱 [Sling檔案](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### 使用專用的Mixin型別定義驗證需求 {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

基於安全理由，新實作會以名為的專用mixin型別，取代剩餘JCR屬性的使用 `granite:AuthenticationRequired`，會為登入路徑定義STRING型別的單一選用屬性 `granite:loginPath`. 只有與此mixin型別相關的內容變更，才會導致更新向Apache Sling Authenticator註冊的要求。 在持續進行任何暫時性修改時會追蹤修改，因此需要 `javax.jcr.Session.save()` 呼叫以生效。

同樣的情況適用於 `granite:loginPath` 屬性。 只有當它是由驗證需求相關的mixin型別定義時，才會被遵守。 在非結構化JCR節點中新增具有此名稱的剩餘屬性將不會顯示所需的效果，並且負責更新OSGi註冊的處理常式將忽略該屬性。

>[!NOTE]
>
>設定登入路徑屬性是選擇性的，只有在需要驗證的樹狀結構無法回覆為預設或繼承的登入頁面時才需要。 請參閱 [登入路徑的評估](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) 下方的。

#### 向Sling驗證者註冊驗證需求和登入路徑 {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

由於這類驗證需求應僅限於某些執行模式以及內容存放庫中的一小部分樹狀結構，因此追蹤需求mixin型別和登入路徑屬性是有條件的，並繫結到定義支援路徑的對應設定（請參閱下面的設定選項）。 因此，只有這些支援路徑範圍內的變更才會觸發OSGi註冊的更新，其他位置的mixin型別和屬性都會被忽略。

預設AEM設定現在會使用此設定，方法是允許在作者執行模式下設定mixin，但只有在複製到發佈執行個體時才會生效。 另請參閱 [此頁面](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) 以瞭解Sling如何執行驗證要求的詳細資訊。

新增 `granite:AuthenticationRequired` 設定的支援路徑中的mixin型別將導致負責處理常式的OSGi註冊被更新，其中包含新的、額外的專案 `sling.auth.requirements` 屬性。 如果指定的驗證需求指定了選擇性 `granite:loginPath` 屬性中，為了排除在驗證需求之外，值另外會向驗證器註冊「 — 」首碼。

#### 驗證需求的評估與繼承 {#evaluation-and-inheritance-of-the-authentication-requirement}

應透過頁面或節點階層繼承Apache Sling驗證需求。 繼承和評估驗證需求（例如順序和優先順序）的詳細資訊會被視為實作詳細資訊，而不會記錄在本文中。

#### 登入路徑的評估 {#evaluation-of-login-path}

評估登入路徑並在驗證後重新導向至對應資源目前是AdobeGranite登入選擇器驗證處理常式的實作詳細資料( `com.day.cq.auth.impl.LoginSelectorHandler`)，這是預設以AEM設定的Apache Sling AuthenticationHandler。

通話時 `AuthenticationHandler.requestCredentials` 此處理常式會嘗試判斷要將使用者重新導向到的對應登入頁面。 此工作流程包含下列步驟：

* 區分過期密碼和需要定期登入作為重新導向的原因；
* 若是定期登入，會測試登入路徑是否可依下列順序取得：

   * 由新程式實作的LoginPathProvider `com.adobe.granite.auth.requirement.impl.RequirementService`，
   * 舊有已棄用的CUG實作，
   * 從「登入頁面對應」，如 `LoginSelectorHandler`，
   * 最後，請退回預設登入頁面，如與定義相同。 `LoginSelectorHandler`.

* 透過上述呼叫取得有效的登入路徑後，使用者的請求就會重新導向至該頁面。

本檔案的目標是評估內部公開的登入路徑 `LoginPathProvider` 介面。 自AEM 6.3以來所推出的實作會採取下列動作：

* 登入路徑的註冊取決於區分過期密碼和需要定期登入作為重新導向的原因
* 若為一般登入，會測試登入路徑是否可依下列順序取得：

   * 從 `LoginPathProvider` 由新版實作 `com.adobe.granite.auth.requirement.impl.RequirementService`，
   * 舊有已棄用的CUG實作，
   * 從「登入頁面對應」，如 `LoginSelectorHandler`，
   * 以及最後回覆至預設登入頁面（與一起定義）。 `LoginSelectorHandler`.

* 透過上述呼叫取得有效的登入路徑後，使用者的請求就會重新導向至該頁面。

此 `LoginPathProvider` 由Granite中新的驗證需求支援實作，會公開由定義的登入路徑 `granite:loginPath` 屬性，這些屬性又由mixin型別定義，如上所述。 儲存登入路徑的資源路徑與屬性值本身的對應會保留在記憶體中，並將進行評估，以找出適用於階層中其他節點的登入路徑。

>[!NOTE]
>
>評估只會針對與位於已設定支援路徑中的資源相關聯的請求執行。 對於任何其他請求，將會評估判斷登入路徑的替代方法。

#### 最佳实践 {#best-practices-1}

定義驗證需求時，應考量下列最佳實務：

* 避免巢狀驗證需求：在樹狀結構開頭放置單一驗證需求標籤，應該就足夠了，而且會繼承至目標節點定義的整個子樹狀結構。 該樹狀結構中的其他驗證需求應視為備援，並在評估Apache Sling中的驗證需求時可能導致效能問題。 透過將授權和驗證相關的CUG區域分離，可以透過CUG或其他型別的原則來限制讀取存取權，同時強制整個樹狀結構的驗證。
* 為存放庫內容建模，以便驗證需求適用於整個樹狀結構，而無需再次從需求中排除巢狀子樹狀結構。
* 若要避免指定並隨後註冊多餘的登入路徑，請執行下列動作：

   * 依賴繼承並避免定義巢狀登入路徑，
   * 請勿將選擇性登入路徑設為對應至預設值或繼承值的值，
   * 應用程式開發人員應識別哪些登入路徑應設定在與關聯的全域登入路徑設定（預設和對應） `LoginSelectorHandler`.

## 在存放庫中的表示方式 {#representation-in-the-repository}

### 存放庫中的CUG原則表示 {#cug-policy-representation-in-the-repository}

Oak檔案說明新的CUG原則如何反映在存放庫內容中。 如需詳細資訊，請參閱 [此頁面](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### 存放庫中的驗證需求 {#authentication-requirement-in-the-repository}

將專用mixin節點型別置於目標節點的存放庫內容中，會反映需要單獨的驗證要求。 mixin型別會定義選擇性屬性，以指定目標節點所定義之樹狀結構的專用登入頁面。

與登入路徑相關聯的頁面可能位於該樹狀結構內部或外部。 它將被排除在驗證需求之外。

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## 管理CUG原則和驗證需求 {#managing-cug-policies-and-authentication-requirement}

### 管理CUG原則 {#managing-cug-policies}

限制對CUG的讀取存取的新型別的存取控制原則是使用JCR存取控制管理API來管理，並遵循 [JCR 2.0規格](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).

#### 設定新的CUG原則 {#set-a-new-cug-policy}

此程式碼適用於在之前未設定CUG的節點套用新的CUG原則。 請注意 `getApplicablePolicies` 只會傳回之前未設定的新原則。 最後，原則需要回寫，且變更需要持續存在。

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

AccessControlPolicyIterator it = acMgr.getApplicablePolicies(path);
while (it.hasNext()) {
        AccessControlPolicy policy = it.nextAccessControlPolicy();
        if (policy instanceof PrincipalSetPolicy) {
           cugPolicy = (PrincipalSetPolicy) policy;
           break;
        }
}

if (cugPolicy == null) {
   log.debug("no applicable policy"); // path not supported or no applicable policy (e.g.
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### 編輯現有的CUG原則 {#edit-an-existing-cug-policy}

編輯現有CUG原則需要以下步驟。 請注意，修改過的原則需要回寫，變更需要透過以下方式持續存在： `javax.jcr.Session.save()`.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
     if (policy instanceof PrincipalSetPolicy) {
        cugPolicy = (PrincipalSetPolicy) policy;
        break;
     }
}

if (cugPolicy == null) {
   log.debug("no policy to edit"); // path not supported or policy not set before
   return;
}

if (cugPolicy.addPrincipals(toAdd1, toAdd2) || cugPolicy.removePrincipals(toRemove)) {
   acMgr.setPolicy(path, cugPolicy);
   session.save();
} else {
     log.debug("cug policy not modified");
}
```

### 擷取有效的CUG原則 {#retrieve-effective-cug-policies}

JCR存取控制管理會定義最大努力方法，以擷取在指定路徑生效的原則。 由於評估CUG原則是條件式的，並取決於要啟用的對應設定，呼叫 `getEffectivePolicies` 是確認特定CUG原則在指定安裝中是否生效的便利方法。

>[!NOTE]
>
>請注意兩者之間的差異 `getEffectivePolicies` 以及後續的程式碼範例，此範例會向上瀏覽階層來尋找給定路徑是否已是現有CUG的一部分。

```java
String path = [...] // needs to be a supported, absolute path

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

// log an debug message of all CUG policies that take effect at the given path
// there could be zero, one or many (creating nested CUGs is possible)
for (AccessControlPolicy policy : acMgr.getEffectivePolicies(path) {
     if (policy instanceof PrincipalSetPolicy) {
        String policyPath = "-";
        if (policy instanceof JackrabbitAccessControlPolicy) {
           policyPath = ((JackrabbitAccessControlPolicy) policy).getPath();
        }
        log.debug("Found effective CUG for path '{}' at '{}', path, policyPath);
     }
}
```

#### 擷取繼承的CUG原則 {#retrieve-inherited-cug-policies}

尋找已在指定路徑定義的所有巢狀CUG，無論它們是否生效。 如需詳細資訊，請參閱 [設定選項](/help/sites-administering/closed-user-groups.md#configuration-options) 區段。

```java
String path = [...]

List<AccessControlPolicy> cugPolicies = new ArrayList<AccessControlPolicy>();
while (isSupportedPath(path)) {
     for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
         if (policy instanceof PrincipalSetPolicy) {
            cugPolicies.add(policy);
         }
      }
      path = (PathUtils.denotesRoot(path)) ? null : PathUtils.getAncestorPath(path, 1);
}
```

#### 依主要專案管理CUG原則 {#managing-cug-policies-by-pincipal}

擴充功能定義自 `JackrabbitAccessControlManager` 允許依主體編輯存取控制原則的存取控制原則並非以CUG存取控制管理實作，因為根據定義，CUG原則一律會影響所有主體：以 `PrincipalSetPolicy` 正在被授予讀取存取權，而所有其他主體將阻止讀取目標節點定義的樹狀結構中的內容。

對應方法一律會傳回空的原則陣列，但不會擲回例外狀況。

### 管理驗證需求 {#managing-the-authentication-requirement}

新驗證需求的建立、修改或移除是通過變更目標節點的有效節點型別來實現的。 然後可以使用一般JCR API來寫入選用的登入路徑屬性。

>[!NOTE]
>
>上述對指定目標節點的修改將只會反映在Apache Sling Authenticator，如果 `RequirementHandler` 已設定，且目標包含在由支援的路徑定義的樹狀結構中（請參閱設定選項區段）。
>
>如需詳細資訊，請參閱 [指派Mixin節點型別](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3指派Mixin節點型別)和 [新增節點及設定屬性](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4新增節點及設定屬性)

#### 新增驗證需求 {#adding-a-new-auth-requirement}

建立新驗證需求的步驟詳述如下。 請注意，在以下情況下，此要求只會向Apache Sling Authenticator註冊： `RequirementHandler` 已為包含目標節點的樹狀結構設定。

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### 使用登入路徑新增驗證需求 {#add-a-new-auth-requirement-with-login-path}

建立包含登入路徑的新驗證需求的步驟。 請注意，只有在符合以下條件時，才會向Apache Sling驗證器註冊登入路徑的需要和排除： `RequirementHandler` 已為包含目標節點的樹狀結構設定。

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### 修改現有登入路徑 {#modify-an-existing-login-path}

變更現有登入路徑的步驟詳述如下。 修改作業只會在 `RequirementHandler` 已為包含目標節點的樹狀結構設定。 先前的登入路徑值將從註冊中移除。 此修改不會影響與目標節點相關聯的驗證需求。

```java
Node targetNode = [...]
String newLoginPath = [...] // STRING property

if (targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", newLoginPath);
   session.save();
} else {
     log.debug("cannot modify login path property; mixin type missing");
}
```

#### 移除現有的登入路徑 {#remove-an-existing-login-path}

移除現有登入路徑的步驟。 登入路徑專案只有在以下情況下才會從Apache Sling驗證程式取消註冊： `RequirementHandler` 已為包含目標節點的樹狀結構設定。 與目標節點相關聯的驗證需求不受影響。

```java
Node targetNode = [...]

if (targetNode.hasProperty("granite:loginPath") &&
   targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", null);
   session.save();
} else {
     log.debug("cannot remove login path property; mixin type missing");
}
```

或者，您也可以使用下列方法達到相同目的：

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### 移除驗證需求 {#remove-an-auth-requirement}

移除現有驗證需求的步驟。 只有在 `RequirementHandler` 已為包含目標節點的樹狀結構設定。

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 擷取有效的驗證需求 {#retrieve-effective-auth-requirements}

沒有專用的公開API可讀取在Apache Sling Authenticator中註冊的所有有效驗證需求。 不過，此清單會顯示在下列位置的系統主控台中： `https://<serveraddress>:<serverport>/system/console/slingauth` 在&quot;**驗證需求設定**「 」區段。

下圖顯示具有示範內容的AEM發佈執行個體的驗證需求。 社群頁面醒目提示的路徑說明本檔案中說明的實作新增的需求如何反映在Apache Sling驗證器中。

>[!NOTE]
>
>在此範例中，未設定選擇性登入路徑屬性。 因此，沒有向驗證者註冊第二個專案。

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### 擷取有效登入路徑 {#retrieve-the-effective-login-path}

目前沒有公用API可擷取匿名存取需要驗證的資源時將生效的登入路徑。 如需有關如何擷取登入路徑的實作詳細資訊，請參閱登入路徑的評估區段。

但請注意，除了此功能定義的登入路徑之外，還有其他方法可指定重新導向至登入，在設計內容模型和特定AEM安裝的驗證要求時，應將這些方法列入考量。

#### 擷取繼承的驗證需求 {#retrieve-the-inherited-auth-requirement}

就像登入路徑一樣，沒有公用API可擷取內容中定義的繼承驗證需求。 下列範例說明如何列出已使用指定階層定義的所有驗證需求，無論其是否生效。 如需詳細資訊，請參閱 [設定選項](/help/sites-administering/closed-user-groups.md#configuration-options).

>[!NOTE]
>
>建議依賴繼承機制來滿足驗證需求和登入路徑，並避免建立巢狀驗證需求。
>
>如需詳細資訊，請參閱 [驗證需求的評估與繼承](#evaluation-and-inheritance-of-the-authentication-requirement)， [登入路徑的評估](#evaluation-of-login-path) 和 [最佳實務](#best-practices).

```java
String path = [...]
Node node = session.getNode(path);

Map<String, String> authRequirements = new ArrayList<String, String>();
while (isSupported(node)) {
     if (node.isNodeType("granite:AuthenticationRequired")) {
         String loginPath = (node.hasProperty("granite:loginPath") ?
                                     node.getProperty("granite:loginPath").getString() :
                                     "";
        authRequirements.put(node.getPath(), loginPath);
        node = node.getParent();
     }
}
```

### 結合CUG原則和驗證需求 {#combining-cug-policies-and-the-authentication-requirement}

下表列出CUG原則的有效組合，以及透過設定啟用兩個模組的AEM執行個體中的驗證需求。

| **需要驗證** | **登入路徑** | **限制的讀取存取權** | **預期效果** |
|---|---|---|---|
| 是 | 是 | 是 | 如果有效的許可權評估授予存取權，則指定的使用者將只能檢視標示為CUG原則的子樹狀結構。 未經驗證的使用者將被重新導向至指定的登入頁面。 |
| 是 | 否 | 是 | 如果有效的許可權評估授予存取權，則指定的使用者將只能檢視標示為CUG原則的子樹狀結構。 未經驗證的使用者將被重新導向至繼承的預設登入頁面。 |
| 是 | 是 | 否 | 未經驗證的使用者將被重新導向至指定的登入頁面。 是否允許檢視標示驗證需求的樹狀結構，取決於該子樹狀結構中個別專案的有效許可權。 沒有專用的CUG限制讀取存取權。 |
| 是 | 否 | 否 | 未經驗證的使用者將被重新導向至繼承的預設登入頁面。 是否允許檢視標示驗證需求的樹狀結構，取決於該子樹狀結構中個別專案的有效許可權。 沒有專用的CUG限制讀取存取權。 |
| 否 | 否 | 是 | 如果有效的許可權評估授予存取權，則指定的已驗證或未驗證使用者將只能檢視標籤有CUG原則的子樹狀結構。 系統會對未經驗證的使用者一視同仁，不會將他們重新導向至登入。 |

>[!NOTE]
>
>「驗證需求」=「否」和「登入路徑」=「是」的組合未在上方列出，因為「登入路徑」是與驗證需求相關聯的選擇性屬性。 指定具有該名稱的JCR屬性而不新增定義mixin型別將沒有作用，且將被對應的處理常式忽略。

## OSGi元件和設定 {#osgi-components-and-configuration}

本節提供OSGi元件的概觀，以及新CUG實作引入的個別設定選項。

另請參閱CUG對應檔案，瞭解舊實作和新實作之間的設定選項完整對應。

### 授權：設定與設定 {#authorization-setup-and-configuration}

新的授權相關零件包含在 **Oak CUG授權** 組合( `org.apache.jackrabbit.oak-authorization-cug`)，這是AEM預設安裝的一部分。 該套件定義了一個單獨的授權模型，旨在部署作為管理讀取存取權的額外方法。

#### 設定CUG授權 {#setting-up-cug-authorization}

有關設定CUG授權的詳細說明，請參閱 [相關Apache檔案](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). 依預設，AEM在所有執行模式中都會部署CUG授權。 在需要不同授權設定的安裝中，也可以使用逐步指示來停用CUG授權。

#### 設定反向連結篩選 {#configuring-the-referrer-filter}

您也需要設定 [Sling查閱者篩選器](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) 所有可用於存取AEM的主機名稱；例如，透過CDN、負載平衡器和任何其他裝置。

如果未設定反向連結篩選，則當使用者嘗試登入CUG網站時，會出現類似下列的錯誤：

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi元件的特性 {#characteristics-of-osgi-components}

以下兩個OSGi元件已匯入以定義驗證需求和指定專用登入路徑：

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>标签</td>
   <td>Apache Jackrabbit Oak CUG設定</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>專用於設定和評估CUG許可權的授權設定。</td>
  </tr>
  <tr>
   <td>配置属性</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>另請參閱 <a href="#configuration-options">設定選項</a> 下方的。</p> </td>
  </tr>
  <tr>
   <td>設定原則</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>引用</td>
   <td><code>CugExclude (ReferenceCardinality.OPTIONAL_UNARY)</code></td>
  </tr>
 </tbody>
</table>

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl**

<table>
 <tbody>
  <tr>
   <td>标签</td>
   <td>Apache Jackrabbit Oak CUG排除清單</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>允許從CUG評估中排除具有設定名稱的主體。</td>
  </tr>
  <tr>
   <td>配置属性</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>另請參閱下方的設定選項一節。</p> </td>
  </tr>
  <tr>
   <td>設定原則</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>引用</td>
   <td>NA</td>
  </tr>
 </tbody>
</table>

#### 設定選項 {#configuration-options}

主要組態選項包括：

* `cugSupportedPaths`：指定可能包含CUG的子樹狀結構。 未設定預設值
* `cugEnabled`：為目前的CUG原則啟用許可權評估的設定選項。

與CUG-authorization模組相關的可用設定選項已列出，並詳見 [Apache Oak檔案](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### 從CUG評估排除主參與者 {#excluding-principals-from-cug-evaluation}

先前實施已採用免除個別主參與者進行CUG評估。 新的CUG授權透過名為CugExclude的專用介面來涵蓋此功能。 Apache Jackrabbit Oak 1.4隨附預設實施，排除了固定的主體集合，以及允許設定個別主體名稱的延伸實施。 後者是在AEM發佈執行個體中設定。

AEM 6.3之後的預設值，可防止下列主體受到CUG原則的影響：

* 管理主體（管理員使用者、管理員群組）
* 服務使用者主體
* 存放庫內部系統主體

如需詳細資訊，請參閱 [自AEM 6.3以來的預設設定](#default-configuration-since-aem) 區段底下。

排除「管理員」群組可在的系統主控台的「 」設定區段中變更或展開 **Apache Jackrabbit Oak CUG排除清單**.

或者，也可以提供和部署CugExclude介面的自訂實作，以調整排除的主體集以因應特殊需求。 請參閱以下說明檔案： [CUG可插拔性](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) 以取得詳細資訊和實作範例。

### 驗證：設定和組態 {#authentication-setup-and-configuration}

新的驗證相關零件包含在 **AdobeGranite驗證處理常式** 組合( `com.adobe.granite.auth.authhandler` 5.6.48版)。 此套件組合是AEM預設安裝的一部分。

為了設定取代已棄用CUG支援的驗證需求，在指定的AEM安裝中，必須存在並啟用某些OSGi元件。 如需詳細資訊，請參閱 **OSGi元件的特性** 下方的。

>[!NOTE]
>
>由於RequirementHandler的強制組態選項，只有透過指定一組支援的路徑來啟用該功能時，驗證相關零件才會啟用。 在標準AEM安裝中，此功能在製作執行模式中停用，並在發佈執行模式中為/content啟用。

**OSGi元件的特性**

下列2個OSGi元件已匯入，以定義驗證需求並指定專用登入路徑：

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirement.impl.RequirementService**

<table>
 <tbody>
  <tr>
   <td>标签</td>
   <td>-</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>用於驗證需求的專用OSGi服務，可針對影響驗證需求的內容變更註冊觀察者(透過 <code>granite:AuthenticationRequirement</code> mixin type)和的登入路徑會公開給 <code>LoginSelectorHandler</code>. </td>
  </tr>
  <tr>
   <td>配置属性</td>
   <td>-</td>
  </tr>
  <tr>
   <td>設定原則</td>
   <td><code>ConfigurationPolicy.OPTIONAL</code></td>
  </tr>
  <tr>
   <td>引用</td>
   <td>
    <ul>
     <li><code>RequirementHandler (ReferenceCardinality.MANDATORY_UNARY)</code></li>
     <li><code>Executor (ReferenceCardinality.MANDATORY_UNARY)</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

**com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler**

| 标签 | AdobeGranite驗證需求和登入路徑處理常式 |
|---|---|
| 描述 | `RequirementHandler` 此實作會更新Apache Sling驗證要求，以及相關登入路徑的對應排除。 |
| 配置属性 | `supportedPaths` |
| 設定原則 | `ConfigurationPolicy.REQUIRE` |
| 引用 | NA |

#### 設定選項 {#configuration-options-1}

CUG重寫的驗證相關部分只隨附與AdobeGranite驗證需求和登入路徑處理常式關聯的單一組態選項：

**「驗證需求和登入路徑處理常式」**

<table>
 <tbody>
  <tr>
   <td>属性</td>
   <td>类型</td>
   <td>默认值</td>
   <td>描述</td>
  </tr>
  <tr>
   <td><p>標籤=支援的路徑</p> <p>名稱= 'supportedPaths'</p> </td>
   <td>設定&lt;string&gt;</td>
   <td>-</td>
   <td>此處理常式會遵循其驗證要求的路徑。 如果您想要新增 <code>granite:AuthenticationRequirement</code> mixin型別到節點而不強制執行（例如，在作者執行個體上）。 如果遺失，則功能會停用。 </td>
  </tr>
 </tbody>
</table>

## 自AEM 6.3以來的預設設定 {#default-configuration-since-aem}

AEM的新安裝預設會將新實施用於CUG功能的授權和驗證相關部分。 舊版實作「AdobeGranite封閉式使用者群組(CUG)支援」已過時，並預設會在所有AEM安裝中停用。 新的實作將改為啟用，如下所示：

### 作者執行個體 {#author-instances}

| **「Apache Jackrabbit Oak CUG設定」** | **解释** |
|---|---|
| 支援的路徑 `/content` | 已啟用CUGpolicies的存取控制管理。 |
| CUG評估啟用FALSE | 許可權評估已停用。 CUG原則不會生效。 |
| 等级 | 200 | 請參閱Oak檔案。 |

>[!NOTE]
>
>沒有設定 **Apache Jackrabbit Oak CUG排除清單** 和 **AdobeGranite驗證需求和登入路徑處理常式** 會出現在預設的編寫執行個體上。

### 發佈執行個體 {#publish-instances}

| **「Apache Jackrabbit Oak CUG設定」** | **解释** |
|---|---|
| 支援的路徑 `/content` | 在設定的路徑下方啟用CUG原則的存取控制管理。 |
| CUG評估啟用TRUE | 已針對設定的路徑啟用許可權評估。 CUG政策生效日期 `Session.save()`. |
| 等级 | 200 | 請參閱Oak檔案。 |

| **「Apache Jackrabbit Oak CUG排除清單」** | **解释** |
|---|---|
| 主體名稱管理員 | 從CUG評估中排除管理員主體。 |

| **「AdobeGranite驗證需求和登入路徑處理常式」** | **解释** |
|---|---|
| 支援的路徑  `/content` | 存放庫中定義的驗證需求，是透過 `granite:AuthenticationRequired` mixin型別在下方生效 `/content` 於 `Session.save()`. Sling驗證器已更新。 在支援的路徑之外新增mixin型別會被忽略。 |

## 停用CUG授權與驗證需求 {#disabling-cug-authorization-and-authentication-requirement}

如果指定的安裝未使用CUG或使用不同的驗證和授權方式，則可能完全停用新實作。

### 停用CUG授權 {#disable-cug-authorization}

請參閱 [CUG可插拔性](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) 有關如何從複合授權設定中移除CUG授權模型的詳細資訊檔案。

### 停用驗證需求 {#disable-the-authentication-requirement}

為了停用對驗證需求的支援，請參閱 `granite.auth.authhandler` 模組，足以移除與關聯的設定 **AdobeGranite驗證需求和登入路徑處理常式**.

>[!NOTE]
>
>但請注意，移除設定並不會取消註冊mixin型別，這仍然適用於節點，而不會生效。

## 與其他模組的互動 {#interaction-with-other-modules}

### Apache Jackrabbit API {#apache-jackrabbit-api}

為了反映CUG授權模型使用的新型別的存取控制原則，Apache Jackrabbit定義的API已擴充。 自2.11.0版的 `jackrabbit-api` 模組會定義名為的新介面 `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`，延伸自 `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

已調整Apache Jackrabbit FileVault的匯入機制，以處理型別的存取控制原則 `PrincipalSetPolicy`.

### Apache Sling內容發佈 {#apache-sling-content-distribution}

請參閱上文 [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) 區段。

### AdobeGranite復寫 {#adobe-granite-replication}

復寫模組已稍作調整，以便能夠在不同的AEM執行個體之間復寫CUG原則：

* `DurboImportConfiguration.isImportAcl()` 會逐字解譯，且只會影響實作的存取控制原則 `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` 只會針對真正的ACL遵守此設定
* 其他原則，例如 `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` CUG授權模型建立的例項一律會被複製，且會提供設定選項 `DurboImportConfiguration.isImportAcl`()將被忽略。

複製CUG原則有一個限制。 如果未移除對應的mixin節點型別，則會移除指定的CUG原則 `rep:CugMixin,` 復寫時不會反映移除。 原則移除時一律移除mixin即可解決此問題。 然而，如果手動新增mixin型別，則可能會顯示此限制。

### AdobeGranite驗證處理常式 {#adobe-granite-authentication-handler}

驗證處理常式 **AdobeGranite HTTP標頭驗證處理常式** 隨附於 `com.adobe.granite.auth.authhandler` 束包含參照 `CugSupport` 由相同模組定義的介面。 它用於在特定情況下計算「範圍」，回退到使用處理常式設定的範圍。

已調整此設定，以參照 `CugSupport` 選用此項，以便在指定設定決定重新啟用已棄用的實作時，確保最大的回溯相容性。 使用實作的安裝將不會再從CUG實作中擷取領域，而是一律顯示領域，定義方式如下 **AdobeGranite HTTP標頭驗證處理常式**.

>[!NOTE]
>
>根據預設， **AdobeGranite HTTP標頭驗證處理常式** 只會在發佈執行模式下以「停用登入頁面」( `auth.http.nologin`)選項已啟用。

### AEM LiveCopy {#aem-livecopy}

在存放庫中搭配LiveCopy設定CUG時，會加上一個額外的節點和一個額外的屬性，如下所示：

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

這兩個元素都是在 `cq:Page`. 使用目前的設計時，MSM只會處理 `cq:PageContent` (`jcr:content`)節點。

因此，CUG群組無法從Blueprint轉出至即時副本。 请在配置 Live Copy 时对此进行规划。

## 新CUG實作的變更 {#changes-with-the-new-cug-implementation}

本節旨在提供對CUG功能所做變更的概述，以及舊實作與新實作的比較。 其中列出影響CUG支援設定方式的變更，並說明在存放庫內容中如何及由誰管理CUG。

### CUG設定和組態的差異 {#differences-in-cug-setup-and-configuration}

過時的OSGi元件 **Adobe Granite封閉式使用者群組(CUG)支援** ( `com.day.cq.auth.impl.cug.CugSupportImpl`)已由新元件取代，以便能夠分別處理舊版CUG功能的授權和驗證相關部分。

## 管理存放庫內容中CUG的差異 {#differences-in-managing-cugs-in-the-repository-content}

以下各節從實作和安全性角度說明舊實作與新實作之間的差異。 雖然新實作旨在提供相同的功能，但在使用新CUG時，有一些重要的細微變化需要知道。

### 與授權的差異 {#differences-with-regards-to-authorization}

授權觀點的主要差異概述於以下清單：

**CUG的專用存取控制內容**

在舊版實作中，預設授權模型用於操控發佈時的存取控制清單原則，以CUG強制執行的設定取代任何現有的ACE。 觸發此事件的是撰寫定期的剩餘JCR屬性，並在發佈時加以解譯。

在新實作中，預設授權模型的存取控制設定不受任何建立、修改或移除的CUG影響。 而是名為的新原則型別 `PrincipalSetPolicy` 會套用作為目標節點的額外存取控制內容。 此額外原則將位於目標節點的子節點中，而且如果存在，將成為預設原則節點的同層級。

**在存取控制管理中編輯CUG原則**

從剩餘JCR屬性移動到專用存取控制原則會影響建立或修改CUG功能的授權部分所需的許可權。 由於這被視為存取控制內容的修改，因此需要 `jcr:readAccessControl` 和 `jcr:modifyAccessControl` 許可權，以便寫入存放庫。 因此，只有有權修改頁面存取控制內容的內容作者才能設定或修改此內容。 這與舊版實作形成對比，舊版實作中寫入一般JCR屬性的能力已足夠，進而造成許可權提升。

**原則定義的目標節點**

CUG原則應建立在JCR節點上，該節點會定義受限制讀取存取的子樹狀結構。 這可能是個AEM頁面，以防預期CUG會影響整個樹狀結構。

請注意，只將CUG原則放在位於指定頁面下方的jcr：content節點上，只會限制對指定頁面內容s.str的存取，而不會對任何同級或子頁面生效。 這可能是有效的使用案例，並且可以使用允許套用精細存取內容內容的存放庫編輯器來達成。 不過，這和之前在jcr：content節點上放置cq：cugEnabled屬性會在內部重新對應至頁面節點的實作不同。 不再執行此對應。

**使用CUG原則進行許可權評估**

從舊的CUG支援移至其他授權模式，會變更評估有效讀取許可權的方式。 如 [Jackrabbit檔案](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)，允許檢視的指定主體 `CUGcontent` 只有在Oak存放庫中設定的所有模型許可權評估都授予讀取存取權時，才會授予讀取存取權。

換言之，為了評估有效許可權， `CUGPolicy` 和預設的存取控制專案會納入考量，而且只有在這兩種原則都授與的情況下，才會授與CUG內容的讀取存取權。 在預設AEM發佈安裝中，完整版的讀取存取權 `/content` 樹狀結構會授與給每個人，CUG政策的作用將與舊實作相同。

**隨選評估**

CUG授權模型允許個別開啟存取控制管理和許可權評估：

* 如果模組有一個或多個支援的路徑可以建立CUG，則會啟用存取控制管理
* 僅在選項為時啟用許可權評估 **CUG評估已啟用** 另外會勾選。

在新的AEM預設設定CUG原則評估中，它僅能以「發佈」執行模式啟用。 欲知詳情，請參閱 [自AEM 6.3以來的預設設定](#default-configuration-since-aem) 以取得更多詳細資料。 這可以透過比較指定路徑的有效原則與內容中儲存的原則來驗證。 只有啟用CUG的許可權評估時，才會顯示有效原則。

如上所述，CUG存取控制原則現在一律會儲存在內容中，但只有在 **CUG評估已啟用** 在Apache Jackrabbit Oak的系統主控台中開啟 **CUG設定。** 預設情況下，僅在「發佈」執行模式中啟用它。

### 與驗證的差異 {#differences-with-regards-to-authentication}

與驗證相關的差異如下所述。

#### 驗證需求的專用Mixin型別 {#dedicated-mixin-type-for-authentication-requirement}

在之前的實作中，CUG的授權和驗證層面都是由單一JCR屬性( `cq:cugEnabled`)。 就驗證而言，這會產生與Apache Sling Authenticator實作一起儲存的驗證需求更新清單。 在新實作中，使用專用的mixin型別( `granite:AuthenticationRequired`)。

#### 排除登入路徑的屬性 {#property-for-excluding-login-path}

mixin型別會定義單一、選用的屬性，稱為 `granite:loginPath`，基本上對應至 `cq:cugLoginPage` 屬性。 相較於先前的實作，只有當登入路徑屬性的宣告節點型別是上述的mixin時，才會採用登入路徑屬性。 在不設定mixin型別的情況下新增具有該名稱的屬性不會有任何效果，並且登入路徑的新要求或排除專案都不會報告給驗證者。

#### 驗證要求的許可權 {#privilege-for-authentication-requirement}

新增或移除mixin型別需要 `jcr:nodeTypeManagement` 正在授與許可權。 在上一個實作中， `jcr:modifyProperties` 許可權用於編輯剩餘屬性。

至此 `granite:loginPath` 擔心新增、修改或移除屬性需要相同的許可權。

#### 由Mixin型別定義的目標節點 {#target-node-defined-by-mixin-type}

驗證需求預期會在JCR節點建立，該節點會定義要強制登入的子樹狀結構。 這可能是個AEM頁面，以防預期CUG會影響整個樹狀結構，而新實作的UI隨後會在頁面節點上新增驗證需求mixin型別。

將CUG原則僅放置在位於指定頁面下方的jcr：content節點上，只會限制對內容的存取，而不會對頁面節點本身或任何子頁面產生影響。

這可能是有效的案例，並且可在允許將mixin放在任何節點的存放庫編輯器中進行。 不過，此行為與之前的實作不同，在之前的實作中，在jcr：content節點上放置cq：cugEnabled或cq：cugLoginPage屬性最終會在內部重新對應至頁面節點。 不再執行此對應。

#### 已設定的支援路徑 {#configured-supported-paths}

兩者皆有 `granite:AuthenticationRequired` mixin型別和granite：loginPath屬性只能在 **支援的路徑** 設定選項與一起出現 **AdobeGranite驗證需求和登入路徑處理常式**. 如果未指定任何路徑，則會完全停用驗證需求功能。 在此情況下，將mixin型別nor屬性新增或設定至指定JCR節點時，就會生效。

### JCR內容、OSGi服務與設定的對應 {#mapping-of-jcr-content-osgi-services-and-configurations}

以下檔案提供舊實作與新實作之間的OSGi服務、設定和存放庫內容的完整對應。

自AEM 6.3以來的CUG對應

[获取文件](assets/cug-mapping.pdf)

## 升級CUG {#upgrade-cug}

### 使用已棄用CUG的現有安裝 {#existing-installations-using-the-deprecated-cug}

舊的CUG支援實作已過時，並將在未來版本中移除。 從AEM 6.3之前的版本升級時，建議改用新的實作。

對於升級的AEM安裝，請務必確保僅啟用一個CUG實作。 新的和舊的已棄用CUG支援的組合未經測試，並可能會導致不良行為：

* Sling驗證程式中與驗證需求的衝突
* 當與舊CUG相關的ACL設定與新CUG原則衝突時，拒絕讀取存取權。

### 移轉現有CUG內容 {#migrating-existing-cug-content}

Adobe提供移轉至新CUG實作的工具。 若要使用它，請執行下列步驟：

1. 前往 `https://<serveraddress>:<serverport>/system/console/cug-migration` 以存取該工具。
1. 輸入您要檢查CUG的根路徑，然後按 **執行試用** 按鈕。 這會在選取的位置掃描符合轉換資格的CUG。
1. 檢閱結果後，按下 **執行移轉** 按鈕以移轉至新實作。

>[!NOTE]
>
>如果您遇到問題，可以在以下位置設定特定記錄器： **偵錯** 層級於 `com.day.cq.auth.impl.cug` 以取得移轉工具的輸出。 另請參閱 [記錄](/help/sites-deploying/configure-logging.md) 以取得如何執行此動作的詳細資訊。
