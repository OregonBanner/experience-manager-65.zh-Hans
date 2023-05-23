---
title: AEM Communities 6.4的存放庫重組
seo-title: Repository Restructuring for AEM Communities in 6.4
description: 瞭解如何進行必要的變更，以移轉至適用於社群的AEM 6.4中的新存放庫結構。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.4 for Communities.
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
feature: Upgrading
exl-id: 4d2bdd45-a29a-4936-b8da-f7e011d81e83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 3%

---

# AEM Communities 6.5的存放庫重組 {#repository-restructuring-for-aem-communities-in}

如父項所述 [AEM 6.4中的存放庫重組](/help/sites-deploying/repository-restructuring.md) 頁面，升級至AEM 6.5的客戶應使用此頁面評估與影響AEM Communities解決方案的存放庫變更相關的工作量。 有些變更需要在AEM 6.5升級過程中投入精力，而其他變更則可能延遲到未來升級。

**6.5版升級**

* [電子郵件通知範本](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [訂閱設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**未來升級之前**

* [徽章設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [Classic Communities主控台設計](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [facebook社交登入設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [語言選項設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [pinterest社交登入設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [評分設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [twitter社交登入設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [其他](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## 6.5版升級 {#with-upgrade}

### 電子郵件通知範本 {#e-mail-notification-templates}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>重組指引</strong></td>
   <td><p>如果您想要移至「 」下的新路徑，則需要手動移轉<code>/apps/settings</code>「。 您可以使用Granite Configuration Manager來執行移轉。</p> <p>您可以設定屬性來執行移轉 <code>mergeList</code> 至 <code>true</code> 於"<code>/libs/settings/community/subscriptions</code>「節點並新增 <code>nt:unstructured</code> 子節點。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 訂閱設定 {#subscription-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>重組指引</strong></td>
   <td><p>如果您想要移至「 」下的新路徑，則需要手動移轉<code>/apps/settings</code>「。 您可以使用Granite Configuration Manager來執行移轉。</p> <p>您可以設定屬性來執行移轉 <code>mergeList</code> 至 <code>true</code> 於"<code>/libs/settings/community/subscriptions</code>「節點並新增 <code>nt:unstructured</code> 子節點。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 關注字詞設定 {#watchwords-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td>/etc/watchwords</td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td>/libs/community/watchwords</td>
  </tr>
  <tr>
   <td><strong>重組指引</strong></td>
   <td>延遲移轉工作可用於清除Communities設定。<br /> <p>「任務」會將關注字詞從 <code>/etc/watchwords</code> 至 <code>/conf/global/settings/community/watchwords</code>.</p> <p>如果自訂標語儲存在SCM中，則應將其部署到 <code>/apps/settings/...</code> 而且您必須確保沒有覆蓋 <code>/conf/global/settings/...</code> 優先的設定。</p> <p>移轉任務已移除 <code>/etc</code> 位置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

## 未來升級之前 {#prior-to-upgrade}

### 徽章設定 {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><strong>徽章規則：</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>徽章影像：</strong></p> <p>對於預設影像： <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>對於自訂影像： <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重組指引</strong></td>
   <td><p>需要手動移轉。</p> <p>如果您的執行個體已自訂徽章/評分規則，則沒有自動化方式可將所有規則放在貯體下。 需要客戶輸入您要用於您網站的conf bucket （全域或網站特定）。</p> <p>沒有可用於設定網站徽章和評分的UI。</p> <p>若要與新的存放庫結構保持一致：</p>
    <ol>
     <li>使用建立網站內容貯體 <strong>設定瀏覽器</strong> 在 <strong>工具</strong></li>
     <li>前往網站根目錄</li>
     <li>設定 <code>cq:confproperty</code> 儲存貯體路徑，您想在此儲存所有設定。 可透過網站進行相同設定 <strong>編輯精靈 — 設定雲端設定輸入</strong>.</li>
     <li>移動相關徽章規則和評分規則 <code>/etc/community/*</code> 至上一步中建立的網站內容貯體。</li>
     <li>調整網站根目錄上的徽章規則和評分規則屬性，使其具有新規則位置的相對參照。
      <ol>
       <li>例如，如果屬性 <code>cq:conf = /conf/we-retail</code>，則 <code>badgingRules [] = community/badging/rules</code> 如果規則現在移至此新貯體。</li>
      </ol> </li>
     <li>同樣地，調整徽章規則節點中評分規則的參考，以擁有相對路徑。</li>
    </ol> <p> </p> <p>最後，移除資源以清除 <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Classic Communities主控台設計 {#classic-communities-console-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/designs/social/console</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/social/console</code></p> <p><code>/apps/settings/wcm/designs/social/console</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指引</strong></td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### facebook社交登入設定 {#facebook-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/cloudservices/facebookconnect</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/facebookconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重組指引</strong></td>
   <td><p>任何新的Facebook雲端設定都必須移轉至新位置。</p>
    <ol>
     <li>將先前位置中的現有設定移轉到新位置。
      <ol>
       <li>透過AEM編寫UI手動重新建立新的Facebook社交登入設定，網址為 <strong>「工具&gt;Cloud Services&gt; Facebook社交登入設定」</strong>.<br /> 或 <br /> </li>
       <li>將任何新的Facebook雲端設定從先前位置複製到適當的新位置，位於 <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>更新任何AEM CommunitiesFacebook網站根目錄，透過設定 <code>[cq:Page]/jcr:content@cq:conf</code> 屬性至新建位置的絕對路徑。</li>
     <li>解除舊版Facebook ConnectCloud Service與任何更新以參照新位置的AEM Communities網站根的關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 語言選項設定 {#language-options-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/social/config/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>重組指引</strong></td>
   <td>不适用<br /> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### pinterest社交登入設定 {#pinterest-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/cloudservices/pinterestconnect</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/pinterestconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重組指引</strong></td>
   <td><p>任何新的Pinterest雲端設定都必須移轉至新位置。</p>
    <ol>
     <li>將先前位置中的現有設定移轉到新位置。
      <ol>
       <li>透過AEM編寫UI手動重新建立新的Pinterest社交登入設定，網址為 <strong>「工具&gt;Cloud Services&gt; Pinterest社交登入設定」</strong>.<br /> 或</li>
       <li>將任何新的Pinterest雲端設定從先前的位置複製到下的適當新位置 <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>更新任何AEM Communities網站根目錄，透過設定參考新的Pinterest社交登入設定。 <code>[cq:Page]/jcr:content@cq:conf</code> 屬性至新建位置的絕對路徑。</li>
     <li>解除舊版Pinterest ConnectCloud Service與任何更新以參照新位置的AEM Communities網站根的關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 評分設定 {#scoring-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>重組指引</strong></td>
   <td><p>為了與新的存放庫結構保持一致，評分規則可以儲存在 <code>/apps/settings/</code> 或/<code>conf/.../settings</code></p>
    <ol>
     <li>對象 <code>/apps/settings</code>，這會當作在SCM中管理的全域或預設規則。</li>
    </ol> <p>在中建立內容感知設定 <code>/conf/</code> 使用CRXDELite：</p>
    <ol>
     <li>建立所需設定 <code>/conf/.../settings</code> 位置<br /> </li>
     <li>社群網站必須具備 <code>cq:conf </code>屬性屬性集。
      <ol>
       <li>若否 <code>cq:conf</code> 已設定，評分規則會直接從屬性的指定路徑讀取'<code>scoringRules</code>'位於網站的根節點，例如： <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>清除：移除資源 <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### twitter社交登入設定 {#twitter-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/cloudservices/twitterconnect</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/twitterconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重組指引</strong></td>
   <td><p>任何新的Twitter雲端設定都必須移轉至新位置。</p>
    <ol>
     <li>將先前位置中的現有設定移轉到新位置。
      <ol>
       <li>透過AEM編寫UI手動重新建立新的Twitter社交登入設定，網址為 <strong>「工具&gt;Cloud Services&gt; Twitter社交登入設定」</strong>.<br /> 或 <br /> </li>
       <li>將任何新的Twitter雲端設定從先前位置複製到適當的新位置，位於 <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>更新任何AEM CommunitiesTwitter網站根目錄，透過設定 <code>[cq:Page]/jcr:content@cq:conf</code> 屬性至新建位置的絕對路徑。</li>
     <li>解除舊版Twitter ConnectCloud Service與任何更新以參照新位置的AEM Communities網站根的關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 其他 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>重組指引</strong></td>
   <td><p>Adobe已在以下位置提供移轉公用程式：</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>現有的自訂範本將移至 <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>
