---
title: 使用 Sling 适配器
seo-title: Using Sling Adapters
description: Sling提供Adapter模式，方便翻譯實作Adaptable介面的物件
seo-description: Sling offers an Adapter pattern to conveniently translate objects that implement the Adaptable interface
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
exl-id: 6465e2c4-28e5-4fc8-8cca-7b632f10ba5a
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '2318'
ht-degree: 13%

---

# 使用 Sling 适配器{#using-sling-adapters}

[Sling](https://sling.apache.org) 提供 [介面卡模式](https://sling.apache.org/site/adapters.html) 方便翻譯實作 [可調整](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 介面。 此介面提供了一般 [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 將物件轉譯為作為引數傳遞的類別型別的方法。

例如，若要將Resource物件轉譯為對應的Node物件，您只需執行下列操作即可：

```java
Node node = resource.adaptTo(Node.class);
```

## 使用案例 {#use-cases}

有以下使用案例：

* 取得實作特定的物件。

   例如，泛型的JCR型實作 [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) 介面提供對基礎JCR的存取權 [`Node`](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* 建立需要傳遞內部前後關聯物件的物件捷徑。

   例如，以JCR為基礎 [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) 保留請求的 [`JCR Session`](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)，根據該請求工作階段工作的許多物件需要此資訊，例如 [`PageManager`](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) 或 [`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html).

* 服務的捷徑。

   罕見情況 —  `sling.getService()` 也很簡單。

### 空值傳回值 {#null-return-value}

`adaptTo()` 可傳回null。

原因有很多，包括：

* 實作不支援目標型別
* 處理此情況的介面卡工廠未啟用(例如： （因為遺失服務參考）
* 內部條件失敗
* 服務無法使用

請務必妥善處理null案例。 對於jsp轉譯，如果會導致jsp失敗，則最好是讓jsp失敗。

### 缓存 {#caching}

為改善效能，實作可自由快取從傳回的物件 `obj.adaptTo()` 呼叫。 如果 `obj` 相同，則傳回的物件相同。

此快取會針對所有使用者執行 `AdapterFactory` 根據個案。

但是，沒有一般規則 — 物件可能是新例項或現有例項。 這表示您無法依賴任一行為。 因此，這很重要，尤其是在內部 `AdapterFactory`，此情境中物件可重複使用。

### 運作方式 {#how-it-works}

有多種方式可以 `Adaptable.adaptTo()` 可以實作：

* 由物件本身；實作方法本身並對應至特定物件。
* 按 [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)，可對應任意物件。

   物件仍必須實作 `Adaptable` 介面，且必須擴充 [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (會傳遞 `adaptTo` 呼叫中央介面卡管理員)。

   這可讓連結至 `adaptTo` 現有類別的機制，例如 `Resource`.

* 兩者的組合。

對於第一種情況，Javadocs可以陳述以下內容 `adaptTo-targets` 是可能的。 不過，對於特定子類別（例如JCR型資源），通常無法執行此操作。 在後一種情況下，實施 `AdapterFactory` 通常是套件私密類別的一部分，因此不會顯示在使用者端API中，也不會列在javadoc中。 從理論上講，您可以存取所有 `AdapterFactory` 來自的實作 [osgi](/help/sites-deploying/configuring-osgi.md) 服務執行階段並檢視其「可調整性」（來源和目標）設定，但不會相互對應。 最終，這取決於內部邏輯，這必須記錄在案。 因此，請參考此參考資料。

## 引用 {#reference}

### Sling {#sling}

[**資源**](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) 調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>如果這是以JCR節點為基礎的資源，或參照節點的JCR屬性。</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">属性</a></td>
   <td>如果這是JCR屬性型資源。</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">项目</a></td>
   <td>如果這是JCR型資源（節點或屬性）。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">地图</a></td>
   <td>如果這是以JCR節點為基礎的資源（或其他支援值的資源），則傳回屬性的對映。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>如果這是以JCR節點為基礎的資源（或其他支援值的資源對應），則傳回方便使用的屬性對應。 也可以使用（更簡單）達成<br /> <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> （處理null大小寫等）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>延伸功能 <a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">值圖</a> 這允許在尋找屬性時考慮資源的階層。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModifiableValueMap</a></td>
   <td>的擴充功能 <a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">值圖</a>，可讓您修改該節點上的屬性。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">輸入資料流</a></td>
   <td>傳回檔案資源的二進位內容(如果這是以JCR節點為基礎的資源，且節點型別為 <code>nt:file</code> 或 <code>nt:resource</code>；如果這是套件資源；如果這是檔案系統資源，則為檔案內容)或二進位JCR屬性資源的資料。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>傳回資源的URL （如果這是JCR節點型資源，則傳回此節點的存放庫URL；如果這是套件資源，則傳回jar套件URL；如果這是檔案系統資源，則傳回檔案URL）。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">文件</a></td>
   <td>如果這是檔案系統資源。</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>如果此資源是使用sling註冊指令碼引擎的指令碼（例如jsp檔案）。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/products/servlet/2.2/javadoc/javax/servlet/Servlet.html">Servlet</a></td>
   <td>如果此資源是使用sling註冊指令碼引擎的指令碼（例如jsp檔案），或如果這是servlet資源。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">字串</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">布林值</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">長</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html">兩次</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">行事曆</a><br /> <a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">值</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">String[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">布林值[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">行事曆[]</a><br /> <a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Value[]</a></td>
   <td>如果這是以JCR屬性為基礎的資源（且值符合），則傳回值。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>如果這是JCR節點型資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html">页面</a></td>
   <td>如果這是JCR節點型資源，且節點是 <code>cq:Page</code> (或 <code>cq:PseudoPage</code>)。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html">组件</a></td>
   <td>如果這是 <code>cq:Component</code> 節點資源。</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Design.html">设计</a></td>
   <td>如果這是設計節點(<code>cq:Page</code>)。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html">模板</a></td>
   <td>如果這是 <code>cq:Template</code> 節點資源。</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Blueprint</a></td>
   <td>如果這是 <code>cq:Template</code> 節點資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html">资产</a></td>
   <td>如果這是dam：Asset節點資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Rendition.html">演绎版</a></td>
   <td>如果這是dam：Asset轉譯（nt：file，在dam：Assert的轉譯資料夾下）</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html">标记</a></td>
   <td>如果這是 <code>cq:Tag</code> 節點資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">使用者管理員</a></td>
   <td>根據JCR工作階段，如果這是JCR型資源，且使用者有權存取UserManager。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授权</a></td>
   <td>「可授權」是「使用者」和「群組」通用的基本介面。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">用户</a></td>
   <td>使用者是可驗證及模擬的特殊可授權專案。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>在資源下方搜尋(或如果這是JCR型資源，則使用setSearchIn())。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">工作流程狀態</a></td>
   <td>指定頁面/工作流程裝載節點的工作流程狀態。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html">復寫狀態</a></td>
   <td>指定資源或其jcr：content子節點的復寫狀態（請先核取）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/connector/ConnectorResource.html">聯結器資源</a></td>
   <td>如果這是以JCR節點為基礎的資源，則傳回適合某些型別的聯結器資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">配置</a></td>
   <td>如果這是 <code>cq:ContentSyncConfig</code> 節點資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>如果低於 <code>cq:ContentSyncConfig</code> 節點資源。</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html) 調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">工作階段</a></td>
   <td>請求的JCR工作階段（如果這是JCR型資源解析器） （預設）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">元件管理員</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/AssetManager.html">資產管理員</a></td>
   <td>根據JCR工作階段，如果這是JCR型資源解析程式。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/TagManager.html">標籤管理員</a></td>
   <td>根據JCR工作階段，如果這是JCR型資源解析程式。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">使用者管理員</a></td>
   <td>UserManager提供存取許可權和維護可授權物件（即使用者和群組）的方法。 UserManager已繫結至特定工作階段。
   </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授权</a> </td>
   <td>目前使用者。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">用户</a><br /> </td>
   <td>目前使用者。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">Querybuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>用於外部化絕對URL，即使不含請求物件亦然。<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) 調整為：

尚未有目標，但實作了Adaptable，並且可以在自訂AdapterFactory中作為來源使用。

[**SlingHttpServletResponse**](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) 調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>如果這是Sling重寫程式回應。</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[頁面](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)** 調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>頁面的資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>已標示的資源(==此)。</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>頁面節點。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>頁面資源可適應的一切。</td>
  </tr>
 </tbody>
</table>

**[元件](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html)** 調整為：

| [Resource](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 元件的資源。 |
|---|---|
| [LabeledResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | 已標示的資源(==此)。 |
| [節點](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 元件的節點。 |
| ... | 元件資源可適應的一切。 |

**[範本](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)** 調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>範本的資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>已標示的資源(==此)。</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>此範本的節點。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>範本資源可適應的所有內容。</td>
  </tr>
 </tbody>
</table>

#### 安全性 {#security}

**可授權**， **使用者** 和 **群組** 適應：

| [節點](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 傳回使用者/群組主節點。 |
|---|---|
| [復寫狀態](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | 傳回使用者/群組主節點的復寫狀態。 |

#### DAM {#dam}

**資產** 調整為：

| [Resource](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 資產的資源。 |
|---|---|
| [節點](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 資產的節點。 |
| ... | 資產資源可適應的一切。 |

#### 标记 {#tagging}

**標籤** 調整為：

| [Resource](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 標籤的資源。 |
|---|---|
| [節點](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 標籤的節點。 |
| ... | 標籤的資源可適應的一切。 |

#### 其他 {#other}

此外，Sling / JCR / OCM也提供 ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` 自訂OCM ([物件內容對應](https://jackrabbit.apache.org/object-content-mapping.html))物件。
