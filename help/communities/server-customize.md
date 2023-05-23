---
title: 伺服器端自訂
seo-title: Server-side Customization
description: 在AEM Communities中自訂伺服器端
seo-description: Customizing server-side in AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# 伺服器端自訂 {#server-side-customization}

| **[⇐ Feature Essentials](essentials.md)** | **[使用者端自訂⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>從一個主要版本升級至下一個主要版本時，Communities API的套件位置可能會有所變更。

### SocialComponent介面 {#socialcomponent-interface}

SocialComponents是POJO，代表AEM Communities功能的資源。 理想情況下，每個SocialComponent代表特定的resourceType，其中包含公開的GETters，可提供資料給使用者端，以便準確表示資源。 所有商業邏輯和檢視邏輯都會封裝在SocialComponent中，包括網站訪客的工作階段資訊（如有必要）。

介面定義了一組代表資源所需的基本GETter。 重要的是，介面中指定了&lt;string object=&quot;&quot;> 為了呈現Handlebars範本和公開資源的GETJSON端點所必需的getAsMap()和String toJSONString()方法。

所有SocialComponent類別都必須實作介面 `com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent介面 {#socialcollectioncomponent-interface}

SocialCollectionComponent介面可擴充SocialComponent介面，以便更妥善地表示屬於其他資源集合的資源。

所有SocialCollectionComponent類別都必須實作介面com.adobe.cq.social.scf.SocialCollectionComponent

### SocialComponentFactory介面 {#socialcomponentfactory-interface}

SocialComponentFactory （工廠）會向架構註冊SocialComponent。 工廠提供一種方法，讓架構知道哪些SocialComponents適用於指定的resourceType，以及識別多個SocialComponents時它們的優先順序排名。

SocialComponentFactory負責建立所選SocialComponent的執行個體，以便使用DI實務從工廠插入SocialComponent所需的所有相依性。

SocialComponentFactory是OSGi服務，可存取其他OSGi服務，這些服務可透過建構函式傳遞給SocialComponent。

所有SocialComponentFactory類別都必須實作介面 `com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority()方法的實作應傳回最高值，才能讓Factory用於getResourceType()傳回的指定resourceType。

### SocialComponentFactoryManager介面 {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager （管理員）會管理在架構中註冊的所有SocialComponents，並負責選取要用於指定資源(resourceType)的SocialComponentFactory。 如果沒有為特定resourceType註冊工廠，則管理員會傳回給定資源具有最近超級型別的工廠。

SocialComponentFactoryManager是OSGi服務，可存取其他OSGi服務，這些服務可透過建構函式傳遞給SocialComponent。

透過叫用取得OSGi服務的控制代碼 `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API -POST要求 {#http-api-post-requests}

#### PostOperation類別 {#postoperation-class}

HTTP APIPOST端點是由實作 `SlingPostOperation` 介面（套件） `org.apache.sling.servlets.post`)。

此 `PostOperation` 端點實作集 `sling.post.operation` 操作將回應的值。 所有POST要求中的：operation引數設定為該值，都將委派給此實作類別。

此 `PostOperation` 叫用 `SocialOperation` 會執行作業所需的動作。

此 `PostOperation` 接收來自的結果 `SocialOperation` 並傳回適當的回應給使用者端。

#### SocialOperation類別 {#socialoperation-class}

每個 `SocialOperation` 端點延伸AbstractSocialOperation類別並覆寫方法 `performOperation()`. 此方法會執行完成作業所需的所有動作，並傳回 `SocialOperationResult` 否則會擲回 `OperationException`在這種情況下，會傳回包含訊息的HTTP錯誤狀態（如果可用），以取代一般JSON回應或成功HTTP狀態代碼。

延伸 `AbstractSocialOperation` 使得重複使用 `SocialComponents` 傳送JSON回應。

#### SocialOperationResult類別 {#socialoperationresult-class}

此 `SocialOperationResult` 類別會傳回，作為 `SocialOperation` 並且由 `SocialComponent`、HTTP狀態碼和HTTP狀態訊息。

此 `SocialComponent` 代表受作業影響的資源。

對於「建立」作業， `SocialComponent` 包含在 `SocialOperationResult` 代表剛建立的資源，而針對「更新」作業，則代表作業變更的資源。 否 `SocialComponent` 針對「刪除」作業傳回。

使用的成功HTTP狀態碼為：

* 201 （建立作業）
* 200 （更新作業）
* 204 （刪除作業）

#### OperationException類別 {#operationexception-class}

一個 `OperationExcepton` 執行作業時，如果要求無效或發生其他錯誤（例如內部錯誤、引數值錯誤、許可權不當等），可能會擲回。 一個 `OperationException` 由HTTP狀態代碼和錯誤訊息組成，這些會作為對 `PostOperatoin`.

#### OperationService類別 {#operationservice-class}

社交元件架構建議不要在內實作負責執行作業的商業邏輯， `SocialOperation` 類別，而是委派給OSGi服務。 將OSGi服務用於商業邏輯可允許 `SocialComponent`，由 `SocialOperation` 端點，以便與其他程式碼整合併套用不同的商業邏輯。

全部 `OperationService` 類別擴充 `AbstractOperationService`，允許連結至正在執行之作業的其他擴充功能。 服務中的每個操作都由 `SocialOperation` 類別。 此 `OperationExtensions` 類別可在作業執行期間透過呼叫方法叫用

* `performBeforeActions()`

   允許預先檢查/預先處理和驗證
* `performAfterActions()`

   允許進一步修改資源或叫用自訂事件、工作流程等

#### OperationExtension類別 {#operationextension-class}

`OperationExtension` 類別是可插入作業的自訂程式碼片段，允許根據業務需求自訂作業。 元件的消費者可以動態且逐步地將功能新增至元件。 擴充功能/掛接模式可讓開發人員專注於擴充功能本身，且無須複製及覆寫整個作業和元件。

## 程式碼範例 {#sample-code}

程式碼範例位於 [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) 存放庫。 搜尋前置詞為的專案 `aem-communities` 或 `aem-scf`.

## 最佳实践 {#best-practices}

檢視 [編碼准則](code-guide.md) 區段以瞭解AEM Communities開發人員的各種編碼准則和最佳作法。

另請參閱 [UGC的儲存資源提供者(SRP)](srp.md) 以瞭解如何存取使用者產生的內容。

| **[⇐ Feature Essentials](essentials.md)** | **[使用者端自訂⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |
