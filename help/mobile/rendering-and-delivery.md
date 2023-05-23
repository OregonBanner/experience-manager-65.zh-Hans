---
title: 呈現和傳遞
seo-title: Rendering and Delivery
description: 呈現和傳遞
seo-description: null
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
exl-id: f0c543ae-33ed-40bb-9eb7-0dc3bdea69e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 6%

---

# 呈現和傳遞{#rendering-and-delivery}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

AEM內容可透過以下方式輕鬆呈現： [Sling預設Servlet](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) 要轉譯 [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) 和其他格式。

這些現成可用的轉譯器通常會導覽存放庫並依原樣傳回內容。

AEM （透過Sling）也支援開發和部署自訂Sling轉譯器，以完全控制轉譯的結構與內容。

Content Services Default Renderer可填補現成可用的Sling Defaults和自訂開發之間的空白，以便在不開發的情況下自訂和控制呈現內容的許多方面。

下圖顯示內容服務的呈現方式。

![chlimage_1-15](assets/chlimage_1-15.png)

## 請求JSON {#requesting-json}

使用 **&lt;resource.caas span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; />.[&lt;export-config span=&quot;&quot; id=&quot;0&quot; translate=&quot;no&quot; />.][&lt;export-config span=&quot;&quot; id=&quot;0&quot; translate=&quot;no&quot; />.json** 以請求JSON。]

<table>
 <tbody>
  <tr>
   <td>資源</td>
   <td>/content/entities下的實體資源<br /> 或 <br /> /content下的內容資源</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>可選</strong><br /> </p> <p>在/apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG下找到的匯出設定<br /> <br /> 如果省略，將會套用預設匯出設定 </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td><strong>可選</strong><br /> <br /> 呈現子項的深度遞回，如Sling呈現中所用</td>
  </tr>
 </tbody>
</table>

## 建立匯出設定 {#creating-export-configs}

可建立匯出設定來自訂JSON轉譯。

您可以在下方建立設定節點 */apps/mobileapps/caas/exportConfigs。*

| 节点名称 | 設定的名稱（用於呈現選擇器） |
|---|---|
| jcr:primaryType | nt:unstructured |

下表顯示「匯出設定」的特性：

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>預設（如果，未設定）</strong></td>
   <td><strong>价值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>字符串[]</td>
   <td>包含所有內容</td>
   <td>sling:resourceType</td>
   <td>從JSON匯出排除具有指定sling：resourceType的節點的詳細資料</td>
  </tr>
  <tr>
   <td>excludecomponents</td>
   <td>字符串[]</td>
   <td>不排除任何專案</td>
   <td>sling:resourceType</td>
   <td>僅包含具有來自JSON匯出的指定sling：resourceType的節點的詳細資料</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>字符串[]</td>
   <td>不排除任何專案</td>
   <td>屬性首碼</td>
   <td>從JSON匯出排除以指定首碼開頭的屬性</td>
  </tr>
  <tr>
   <td>excludeproperties</td>
   <td>字符串[]</td>
   <td>不排除任何專案</td>
   <td>屬性名稱</td>
   <td>從JSON匯出排除指定的屬性</td>
  </tr>
  <tr>
   <td>includeproperties</td>
   <td>字符串[]</td>
   <td>包含所有內容</td>
   <td>屬性名稱</td>
   <td><p>如果設定了excludePropertyPrefixes<br /> 這包括指定的屬性，儘管前置詞是被排除的，</p> <p>否則（排除忽略的屬性）只會包含這些屬性</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>字符串[]</td>
   <td>包含所有內容</td>
   <td>子名稱</td>
   <td>從JSON匯出排除指定的子系</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>字符串[]<br /> <br /> </td>
   <td>不排除任何專案</td>
   <td>子名稱</td>
   <td>從JSON匯出僅包含指定的子項，排除其他</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>字符串[]<br /> <br /> </td>
   <td>不重新命名任何內容</td>
   <td>&lt;actual_property_name&gt;，&lt;replacement_property_name&gt;</td>
   <td>使用取代物重新命名屬性</td>
  </tr>
 </tbody>
</table>

### 資源型別匯出覆寫 {#resource-type-export-overrides}

在下建立設定節點 */apps/mobileapps/caas/exportConfigs。*

| name | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

下表顯示屬性：

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>預設（如果，未設定）</strong></td>
   <td><strong>价值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>&lt;SELECTOR_TO_INC&gt;</td>
   <td>字符串[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>對於以下sling資源型別，請勿傳回預設的CaaS json匯出。<br /> 將資源呈現為，以傳回客戶json匯出；<br /> &lt;resource&gt;.&lt;selector_to_inc&gt;.json </td>
  </tr>
 </tbody>
</table>

### 現有的Content Services匯出設定 {#existing-content-services-export-configs}

Content Services包含兩個匯出設定：

* 預設（未指定設定）
* 頁面（轉譯網站頁面）

#### 預設匯出設定 {#default-export-configuration}

如果在請求的URI中指定了配置，則將套用Content Services預設匯出配置。

&lt;resource>.caas[.&lt;depth-int>].json

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>excludeproperties</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>jcr：，sling：，cq：，oak：，pge-</td>
  </tr>
  <tr>
   <td>includeproperties</td>
   <td>jcr：text，text<br /> jcr：title，title<br /> jcr：description，description<br /> jcr：lastModified，lastModified<br /> cq：tags，tags<br /> cq：lastModified，lastModified</td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludecomponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sling JSON覆寫</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### 頁面匯出設定 {#page-export-configuration}

此設定會擴充預設值，以包含子節點下的群組子項。

&lt;site_page>.caas.page[.&lt;depth-int>].json

### 其他资源 {#additional-resources}

請參閱下列資源，瞭解內容服務中的其他主題：

* [開發模型](/help/mobile/administer-mobile-apps.md)
* [製作內容服務](/help/mobile/develop-content-as-a-service.md)
* [管理內容服務](/help/mobile/developing-content-services.md)
