---
title: 內容片段範本
seo-title: Content Fragment Templates
description: 建立內容片段時會選取範本，並為新片段提供基本結構、元素和變數
seo-description: Templates are selected when creating a content fragmen and provide the new fragment with the basic structure, element, and variation
uuid: d147bac8-b710-40ed-9664-decb5ffcf8e7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: a975ea2e-5e24-4a96-bd62-63bb98836ff2
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
source-git-commit: a2b1bd5462ae1837470e31cfeb87a95af1c69be5
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 3%

---

# 內容片段範本{#content-fragment-templates}

>[!CAUTION]
>
>[內容片段模型](/help/assets/content-fragments/content-fragments-models.md) 建議用於建立所有新的內容片段。
>
>內容片段模型用於WKND中的所有範例。

>[!NOTE]
>
>在AEM 6.3之前，內容片段是根據範本而非模型建立的。
>
>內容片段範本現已棄用。 它們仍可用於建立片段，但建議改用內容片段模型。 片段範本不會新增任何新功能，而會在未來版本中移除。

建立內容片段時會選取範本。 它們為新片段提供基本結構、元素和變數。 用於內容片段的範本須遵守Granite Configuration Manager。

現成可用的範本位於下方：

* `/libs/settings/dam/cfm/templates`

您可以在下列位置為內容片段建立網站專屬的範本：

* `/apps/settings/dam/cfm/templates`
覆蓋現成範本或提供客戶特定且應用程式範圍範本（在執行階段不會擴充/變更）的位置。

* `/conf/global/settings/dam/cfm/templates`
必須在執行階段變更的執行個體範圍客戶特定範本的位置。

優先順序為（遞減順序） `/conf`， `/apps`， `/libs`.

>[!CAUTION]
>
>您 ***必須*** 不變更中的任何專案 `/libs` 路徑。
>
>這是因為 `/libs` 下次升級執行個體時會被覆寫（而您在套用hotfix或feature pack時很可能會被覆寫）。
>
>設定和其他變更的建議方法是：
>
>1. 重新建立所需專案（即該專案存在於中） `/libs`)下 `/apps`
>
>1. 進行任何變更 `/apps`

>


範本的基本結構位於下方：

```xml
conf
  global
    settings
      dam
        cfm
          templates
            <template-name>
              ...
```

特定結構為：

```xml
+ <template-name>
    - jcr:primaryType
    - jcr:title
    - jcr:description
    - initialAssociatedContent
    - precreateElements
    - version
    + elements
        - jcr:primaryType
        + <element-name>
            - jcr:primaryType
            - jcr:title
            - defaultContent
            - initialContentType
            - name
        ... + other element definitions
    + variations
        - jcr:primaryType
        + <variation-name>
            - jcr:primaryType
            - jcr:title
            - jcr:description
            - name
        ... + other variation definitions
```

有關節點及其屬性的更多詳細資訊如下：

* **模板**

   <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>价值</th>
    </tr>
    <tr>
     <td><code>&lt;<em>template-name</em>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>此節點是每個範本的根。 此為必填欄位，且應具有唯一名稱。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必填<br /> </p> </td>
     <td>範本的標題(顯示在 <strong>建立片段</strong> 精靈)。</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>可選</p> </td>
     <td>說明範本用途的文字(顯示在 <strong>建立片段</strong> 精靈)。</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>可選</p> </td>
     <td>一個陣列，其中包含集合的路徑，依預設應關聯至新建立的內容片段。</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>必填</p> </td>
     <td><p><code>true</code>，表示內容片段元素（主元素除外）的子資產應在建立內容片段時建立； <em>false</em> 是否應「即時」建立。</p> <p><strong>注意</strong>：此引數目前必須設定為 <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>必填</p> </td>
     <td><p>內容結構的版本；目前支援：</p> <p><strong>注意</strong>：此引數目前必須設定為 <code>2</code>.<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **元素**

   <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>价值</th>
    </tr>
    <tr>
     <td><code>elements</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>必填</p> </td>
     <td><p>包含內容片段元素定義的節點。 這是強制性的，而且至少需要包含一個子節點 <strong>主要</strong> 元素，但可以包含[1..n]個子節點。</p> <p>使用範本時，元素子分支會複製到片段的模型子分支。</p> <p>第一個元素(在CRXDE Lite中檢視時)會自動視為 <i>主要</i> 元素；節點名稱不相關，且節點本身除了由主要資產表示外，沒有特殊意義；其他元素會作為子資產處理。</p> </td>
    </tr>
   </tbody>
  </table>

* **元素名称**

   <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>价值</th>
    </tr>
    <tr>
     <td><code>&lt;<i>element-name</i>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>此節點會定義一個元素。 此為必填欄位，且應具有唯一名稱。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必填</p> </td>
     <td>元素的標題（顯示在片段編輯器的元素選擇器中）。</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>默认: ""</p> </td>
     <td>元素的初始內容；僅用於 <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>默认: <code>text/html</code></p> </td>
     <td><p>元素的初始內容型別；僅用於 <code>precreateElements</code><i> = </i><code>true</code>；目前支援：</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>必填</p> </td>
     <td>元素的內部名稱；對於片段型別必須是唯一的。</td>
    </tr>
   </tbody>
  </table>

* **变体**

   <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>价值</th>
    </tr>
    <tr>
     <td><code>variations</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>可選</p> </td>
     <td>此選用節點包含內容片段初始變數的定義。</td>
    </tr>
   </tbody>
  </table>

* **變數名稱**

   <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>价值</th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>如果存在變數節點，則為必要</p> </td>
     <td><p>定義初始變數。<br /> 依預設，變數會新增至內容片段的所有元素。</p> <p>變數會有與個別元素相同的初始內容(請參閱 <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必填</p> </td>
     <td>變數的標題(顯示在片段編輯器的 <strong>變數</strong> 標籤（左側邊欄）。</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>默认: ""</p> </td>
     <td>提供變數說明的文字 <span>(顯示在片段編輯器的 <strong>變數</strong> 標籤（左側邊欄）。</code></td>
    </tr>
   </tbody>
  </table>
