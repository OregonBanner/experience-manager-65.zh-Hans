---
title: AEM 标记框架
seo-title: AEM Tagging Framework
description: 標籤內容並運用AEM標籤基礎結構
seo-description: Tag content and leverage the AEM Tagging infrastructure
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: efb4f9f8a97baf8d3d02160226e4f4d3f8f64c89
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 0%

---

# AEM 标记框架 {#aem-tagging-framework}

若要標籤內容並運用AEM標籤基礎結構：

* 標籤必須作為型別的節點存在 ` [cq:Tag](#tags-cq-tag-node-type)` 在 [分類根節點](#taxonomy-root-node)

* 標籤的內容節點的NodeType必須包含 [ `cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin
* 此 [標籤ID](#tagid) 新增至內容節點的 [ `cq:tags`](#tagged-content-cq-tags-property) 屬性並解析為型別的節點 ` [cq:Tag](#tags-cq-tag-node-type)`

## 標籤：cq：Tag節點型別  {#tags-cq-tag-node-type}

標籤的宣告會擷取到存放庫中的型別節點中 `cq:Tag.`

標籤可以是簡單的字詞（例如sky），或代表階層式分類法（例如fruit/apple，表示類屬水果和較特定的蘋果）。

標籤由唯一的TagID識別。

標籤具有可選的中繼資訊，例如標題、當地語系化的標題和說明。 出現時，標題應顯示在使用者介面中，而不是TagID。

標籤架構也提供將作者和網站訪客限製為僅使用特定、預先定義的標籤的功能。

### 標籤特性 {#tag-characteristics}

* 節點型別為 `cq:Tag`
* 節點名稱是 ` [TagID](#tagid)`
* 此 ` [TagID](#tagid)` 一律包含 [名稱空間](#tag-namespace)

* 可選 `jcr:title` 屬性（在UI中顯示的標題）

* 可選 `jcr:description` 屬性

* 包含子節點時，稱為 [容器標籤](#container-tags)
* 儲存在存放庫中，位於名為的基本路徑下方 [分類根節點](#taxonomy-root-node)

### 标记 ID {#tagid}

TagID會識別解析為存放庫中的標籤節點的路徑。

通常TagID是以名稱空間開頭的速記TagID，也可以是以 [分類根節點](#taxonomy-root-node).

標籤內容時，如果內容尚不存在， ` [cq:tags](#tagged-content-cq-tags-property)` 屬性會新增至內容節點，而TagID會新增至屬性的String陣列值。

TagID包含 [名稱空間](#tag-namespace) 後面接著本機TagID。 [容器標籤](#container-tags) 具有代表分類法中階層順序的子標籤。 子標籤可用於參照與任何本機TagID相同的標籤。 例如，即使內容是包含子標籤的容器標籤，例如「fruit/apple」和「fruit/banana」，也允許使用「fruit」標籤內容。

### 分類根節點 {#taxonomy-root-node}

分類根節點是存放庫中所有標籤的基本路徑。 分類根節點必須 *not* 為型別的節點 `  cq   :Tag`.

在AEM中，基底路徑為 `/content/  cq   :tags` 且根節點的型別為 `  cq   :Folder`.

### 標籤名稱空間 {#tag-namespace}

名稱空間允許將專案分組。 最典型的使用案例是每個（網站） （例如公用、內部和入口網站）或大型應用程式（例如WCM、Assets、Communities）都有一個名稱空間，但名稱空間可用於各種其他需求。 在使用者介面中使用名稱空間，以僅顯示適用於目前內容的標籤子集（即特定名稱空間的標籤）。

標籤的名稱空間是分類子樹狀結構中的第一個層級，也就是 [分類根節點](#taxonomy-root-node). 名稱空間是型別的節點 `cq:Tag` 其父項不是 `cq:Tag`節點型別。

所有標籤都有名稱空間。 如果未指定名稱空間，則會將標籤指派給預設名稱空間TagID `default` (標題為 `Standard Tags),`即 `/content/cq:tags/default.`

### 容器標籤 {#container-tags}

容器標籤是型別的節點 `cq:Tag` 包含任何數量及型別的子節點，可讓您使用自訂中繼資料來增強標籤模型。

此外，分類法中的容器標籤（或超級標籤）是所有子標籤的彙總：例如，以水果/蘋果標籤的內容也被視為以水果標籤，也就是說，搜尋僅以水果標籤的內容也會找到以水果/蘋果標籤的內容。

### 解析標籤ID {#resolving-tagids}

如果標籤ID包含冒號「：」，冒號會將名稱空間與標籤或子分類法分開，然後再以一般斜線「/」分隔。 如果標籤ID沒有冒號，則會隱含預設名稱空間。

標籤的標準且唯一位置位於/content/cq：tags之下。

參照不存在的路徑或不指向cq：Tag節點的路徑的標籤會被視為無效並被忽略。

下表顯示一些TagID範例、其元素，以及TagID如何解析為存放庫中的絕對路徑：

下表顯示一些TagID範例、其元素，以及TagID如何解析為存放庫中的絕對路徑：

<table>
 <tbody>
  <tr>
   <td><strong>标记 ID<br /> </strong></td>
   <td><strong>命名空间</strong></td>
   <td><strong>本機ID</strong></td>
   <td><strong>容器標籤</strong></td>
   <td><strong>分葉標籤</strong></td>
   <td><strong>存放庫<br /> 絕對標籤路徑</strong></td>
  </tr>
  <tr>
   <td>dam：fruit/apple/braeburn</td>
   <td>dam</td>
   <td>水果/蘋果/布雷本</td>
   <td>果實，蘋果</td>
   <td>braeburn</td>
   <td>/content/cq：tags/dam/fruit/apple/braeburn</td>
  </tr>
  <tr>
   <td>顏色/紅色</td>
   <td>默认</td>
   <td>顏色/紅色</td>
   <td>颜色</td>
   <td>紅色</td>
   <td>/content/cq：tags/default/color/red</td>
  </tr>
  <tr>
   <td>天空</td>
   <td>默认</td>
   <td>天空</td>
   <td>(无)</td>
   <td>天空</td>
   <td>/content/cq：tags/default/sky</td>
  </tr>
  <tr>
   <td>dam：</td>
   <td>dam</td>
   <td>(无)</td>
   <td>(无)</td>
   <td>（無，名稱空間）</td>
   <td>/content/cq：tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq：tags/category/car</td>
   <td>類別</td>
   <td>car</td>
   <td>car</td>
   <td>car</td>
   <td>/content/cq：tags/category/car</td>
  </tr>
 </tbody>
</table>

### 標籤標題本地化 {#localization-of-tag-title}

當標籤包含可選標題字串( `jcr:title`)可以新增屬性，將顯示的標題當地語系化 `jcr:title.<locale>`.

如需詳細資訊，請參閱

* [不同語言的標籤](/help/sites-developing/building.md#tags-in-different-languages)  — 說明API的使用
* [管理不同語言的標籤](/help/sites-administering/tags.md#managing-tags-in-different-languages)  — 說明「標籤」主控台的使用

### 访问控制 {#access-control}

標籤會作為節點存在於下的存放庫中 [分類根節點](#taxonomy-root-node). 若要允許或拒絕作者和網站訪客在指定的名稱空間中建立標籤，可在存放庫中設定適當的ACL。

此外，拒絕特定標籤或名稱空間的讀取許可權將控制將標籤套用至特定內容的能力。

典型做法包括：

* 允許 `tag-administrators` 群組/角色對所有名稱空間的寫入許可權(新增/修改 `/content/cq:tags`)。 此群組隨附AEM立即可用。

* 允許使用者/作者讀取他們應該可以讀取的所有名稱空間（幾乎全部）。
* 允許使用者/作者寫入對標籤應由使用者/作者自由定義的名稱空間的存取權(下方的add_node `/content/cq:tags/some_namespace`)

## 可標籤內容：cq：Taggable Mixin {#taggable-content-cq-taggable-mixin}

為了讓應用程式開發人員將標籤附加到內容型別，節點的註冊([CND](https://jackrabbit.apache.org/node-type-notation.html))必須包含 `cq:Taggable` mixin或 `cq:OwnerTaggable` mixin.

此 `cq:OwnerTaggable` mixin，繼承自 `cq:Taggable`，表示內容可依所有者/作者分類。 在AEM中，它只是 `cq:PageContent` 節點。 此 `cq:OwnerTaggable` 標籤框架不需要mixin。

>[!NOTE]
>
>建議僅在彙總內容專案的頂層節點（或其jcr：content節點）上啟用標籤。 範例包括：
>
>* 頁面( `cq:Page`)其中 `jcr:content`節點屬於型別 `cq:PageContent` 其中包括 `cq:Taggable` mixin.
>
>* 資產( `cq:Asset`)其中 `jcr:content/metadata` 節點一律具有 `cq:Taggable` mixin.
>


### 節點型別標籤法(CND) {#node-type-notation-cnd}

節點型別定義以CND檔案的形式存在於存放庫中。 CND標籤法定義為JCR檔案的一部分 [此處](https://jackrabbit.apache.org/node-type-notation.html).

AEM中包含的「節點型別」的基本定義如下：

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## 標籤內容： cq：tags屬性 {#tagged-content-cq-tags-property}

此 `cq:tags` 屬性是字串陣列，用來儲存作者或網站訪客套用至內容的一或多個TagID。 屬性只有在新增至使用定義的節點時才有意義 `[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin.

>[!NOTE]
>
>若要運用AEM標籤功能，自訂開發的應用程式不應定義以外的標籤屬性 `cq:tags`.

## 移動和合併標籤 {#moving-and-merging-tags}

以下說明使用移動或合併標籤時，在存放庫中所產生的效果 [標籤主控台](/help/sites-administering/tags.md)：

* 將標籤A移動或合併至下的標籤B時 `/content/cq:tags`：

   * 標籤A未刪除並取得 `cq:movedTo` 屬性。
   * 標籤B已建立（若發生移動），並取得 `cq:backlinks` 屬性。

* `cq:movedTo` 指向標籤B。此屬性表示標籤A已移動或合併到標籤B中。移動標籤B會相應地更新此屬性。 標籤A因此會隱藏，並只會保留在存放庫中，以解析指向標籤A的內容節點中的標籤ID。標籤垃圾回收器會移除標籤A之類的標籤，而內容節點不再指向這些標籤。
的特殊值 `cq:movedTo` 屬性為 `nirvana`：此變數會在標籤刪除時套用，但無法從存放庫中移除，因為有子標籤具有 `cq:movedTo` 必須保留。

   >[!NOTE]
   >
   >此 `cq:movedTo` 只有在符合下列任一條件時，屬性才會新增至移動或合併的標籤：
   >
   >1. 標籤用於內容中（表示它有參考）或
   >1. 標籤具有已移動的子系。


* `cq:backlinks` 會將參照保持在另一個方向，即會保留所有已移至標籤B或與標籤B合併的標籤清單。這通常需要保留 `cq:movedTo`屬性是當標籤B移動/合併/刪除或是當標籤B啟動時的最新狀態，在這種情況下，其所有反向連結標籤也必須啟動。

   >[!NOTE]
   >
   >此 `cq:backlinks` 只有在符合下列任一條件時，屬性才會新增至移動或合併的標籤：
   >
   >1. 標籤用於內容中（表示它有參考）或
   >1. 標籤具有已移動的子系。


* 讀取 `cq:tags` 內容節點的屬性涉及以下解析：

   1. 如果底下沒有相符專案 `/content/cq:tags`，不會傳回任何標籤。
   1. 如果標籤具有 `cq:movedTo` 屬性集，則會接著參考的標籤ID。
只要後續的標籤具有 `cq:movedTo` 屬性。

   1. 如果追蹤的標籤沒有 `cq:movedTo` 屬性，則會讀取標籤。

* 若要在移動或合併標籤後發佈變更，請 `cq:Tag` 節點及其所有反向連結都必須複製：當標籤在標籤管理主控台中啟動時，就會自動完成此操作。

* 稍後更新頁面的 `cq:tags` 屬性會自動清除「舊」參考。 由於透過API解析移動的標籤會傳回目的地標籤，因此會觸發此動作，進而提供目的地標籤ID。

>[!NOTE]
>
>標籤的移動與標籤的移轉不同。

## 標籤移轉 {#tags-migration}

Experience Manager6.4以後的標籤儲存於 `/content/cq:tags`，之前儲存於 `/etc/tags`. 不過，在Adobe Experience Manager已從舊版升級的情況下，標籤仍會顯示在舊位置下 `/etc/tags`. 在已升級的系統中，標籤需要移轉至 `/content/cq:tags`.

>[!NOTE]
>
>在標籤頁面的頁面屬性中，建議使用標籤ID (`geometrixx-outdoors:activity/biking`)而不是以硬式編碼方式編寫標籤基本路徑(例如， `/etc/tags/geometrixx-outdoors/activity/biking`)。
>
>若要列出標籤， `com.day.cq.tagging.servlets.TagListServlet` 可使用。

>[!NOTE]
>
>建議使用標籤管理員API作為資源。

### 如果升級的AEM執行個體支援TagManager API {#upgraded-instance-support-tagmanager-api}

1. 在元件啟動時，TagManager API會偵測元件是否為升級的AEM執行個體。 在升級後的系統中，標籤儲存在 `/etc/tags`.

1. TagManager API接著以回溯相容模式執行，這表示API會使用 `/etc/tags` 作為基礎路徑。 如果沒有，則會使用新位置 `/content/cq:tags`.

1. 更新標籤位置。

1. 將標籤移轉至新位置後，請執行以下指令碼：

```java
import org.apache.sling.api.resource.*
import javax.jcr.*

ResourceResolverFactory resourceResolverFactory = osgi.getService(ResourceResolverFactory.class);
ResourceResolver resolver = resourceResolverFactory.getAdministrativeResourceResolver(null);
Session session = resolver.adaptTo(Session.class);

def queryManager = session.workspace.queryManager;
def statement = "/jcr:root/content/cq:tags//element(*, cq:Tag)[jcr:contains(@cq:movedTo,\'/etc/tags\') or jcr:contains(@cq:backlinks,\'/etc/tags\')]";
def query = queryManager.createQuery(statement, "xpath");

println "query = ${query.statement}\n";

def tags = query.execute().getNodes();


tags.each { node ->
  def tagPath = node.path;
  println "tag = ${tagPath}";

  if(node.hasProperty("cq:movedTo") && node.getProperty("cq:movedTo").getValue().toString().startsWith("/etc/tags"))
    {
     def movedTo = node.getProperty("cq:movedTo").getValue().toString();

     println "cq:movedTo = ${movedTo} \n";

     movedTo = movedTo.replace("/etc/tags","/content/cq:tags");
     node.setProperty("cq:movedTo",movedTo);
     } else if(node.hasProperty("cq:backlinks")){

     String[] backLinks = node.getProperty("cq:backlinks").getValues();
     int count = 0;

     backLinks.each { value ->
             if(value.startsWith("/etc/tags")){
                     println "cq:backlinks = ${value}\n";
                     backLinks[count] = value.replace("/etc/tags","/content/cq:tags");
    }
             count++;
     }

    node.setProperty("cq:backlinks",backLinks);
  }
}
session.save();

println "---------------------------------Success-------------------------------------"
```

指令碼會擷取所有具有 `/etc/tags` 在的值中 `cq:movedTo/cq:backLinks` 屬性。 然後它會逐一檢視擷取的結果集並解析 `cq:movedTo` 和 `cq:backlinks` 屬性值至 `/content/cq:tags` 路徑(在此案例中為 `/etc/tags` 在值中偵測到)。

### 如果升級的AEM執行個體在傳統UI上執行 {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>傳統UI不符合零停機規範，不支援新的標籤庫路徑。 如果您想要使用傳統UI，而非 `/etc/tags` 需要建立，接著 `cq-tagging` 元件重新啟動。

如果TagManager API支援升級的AEM執行個體，並在傳統UI中執行：

1. 參照舊標籤基底路徑一次 `/etc/tags` 取代為使用tagId或新標籤位置 `/content/cq:tags`，您可以將標籤移轉至新位置 `/content/cq:tags` 在CRX中，之後重新啟動元件。

1. 將標籤移轉至新位置後，請執行上述指令碼。
