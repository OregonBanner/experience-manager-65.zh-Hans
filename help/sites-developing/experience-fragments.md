---
title: AEM Sites開發中的體驗片段
description: 瞭解如何自訂體驗片段。
uuid: fc9f7e59-bd7c-437a-8c63-de8559b5768d
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c02e713e-15f3-408b-879a-d5eb014aef02
docset: aem65
exl-id: c4fb1b5e-e15e-450e-b882-fe27b165ff9f
source-git-commit: a8616b3b30ac04ea24c4a869cabd47518af1a35f
workflow-type: tm+mt
source-wordcount: '1781'
ht-degree: 1%

---

# 体验片段{#experience-fragments}

## 基本知識 {#the-basics}

一個 [體驗片段](/help/sites-authoring/experience-fragments.md) 是一組一或多個元件，包括可在頁面中參考的內容和版面。

體驗片段主要和/或變體使用：

* `sling:resourceType` ： `/libs/cq/experience-fragments/components/xfpage`

因為沒有 `/libs/cq/experience-fragments/components/xfpage/xfpage.html` 它還原為

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## 纯 HTML 演绎版 {#the-plain-html-rendition}

使用 `.plain.` 在URL的選擇器中，您可以存取純HTML轉譯。

這可從瀏覽器取得，但其主要目的是讓其他應用程式（例如協力廠商網頁應用程式、自訂行動實作）僅使用URL直接存取體驗片段的內容。

純HTML轉譯會將通訊協定、主機和內容路徑新增至以下路徑：

* 型別： `src`， `href`，或 `action`

* 或結尾為： `-src`，或 `-href`

例如：

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>連結一律會參考發佈執行個體。 這些連結旨在由第三方使用，因此將一律從發佈執行個體而不是作者呼叫連結。

![xf-14](assets/xf-14.png)

純轉譯選擇器使用轉換器，而非其他指令碼； [Sling重寫程式](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) 會作為轉換器使用。 此設定於

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### 設定HTML轉譯產生 {#configuring-html-rendition-generation}

HTML轉譯是使用Sling重寫程式管道產生的。 管道定義於 `/libs/experience-fragments/config/rewriter/experiencefragments`. HTML轉換器支援下列選項：

* `allowedCssClasses`
   * 符合應留在最終轉譯中的CSS類別的RegEx運算式。
   * 如果客戶想要移除某些特定的CSS類別，這將很有用
* `allowedTags`
   * 最終轉譯中允許的HTML標籤清單。
   * 預設允許下列標籤（不需要設定）： html、head、title、body、img、p、span、ul、li、a、b、i、em、strong、h1、h2、h3、h4、h5、h6、br、noscript、div、link和script

建議使用覆蓋來設定重寫程式。 另請參閱 [覆蓋](/help/sites-developing/overlays.md)

## 社交變數 {#social-variations}

社交變體可發佈在社群媒體（文字和影像）上。 在AEM中，這些社交變體可包含元件；例如，文字元件、影像元件。

社交貼文的影像和文字可從任何深度層級的影像資源型別或文字資源型別取得（在建置區塊或版面配置容器中）。

社交變數也允許建置區塊，並在進行社交動作（在發佈環境中）時加以考慮。

若要將正確的文字和影像發佈到社群媒體網路，如果您正在開發自己的自訂元件，則需要遵守一些慣例。

為此，必須使用以下屬性：

* 用於擷取影像

   * `fileReference`
   * `fileName`

* 用於擷取文字

   * `text`

未使用此慣例的元件不會納入考量。

## 體驗片段的範本 {#templates-for-experience-fragments}

>[!CAUTION]
>
>***僅限*** [可編輯的範本](/help/sites-developing/page-templates-editable.md) 體驗片段支援。

為體驗片段開發新範本時，您可以遵循的標準做法 [可編輯的範本](/help/sites-developing/page-templates-editable.md).

若要建立由偵測到的體驗片段範本 **建立體驗片段** 精靈，您必須遵循下列其中一個規則集：

1. 兩者：

   1. 樣板的資源型別（初始節點）必須繼承自：
      `cq/experience-fragments/components/xfpage`

   1. 範本名稱的開頭必須是：
      `experience-fragments`
這可讓使用者在/content/experience-fragments中建立體驗片段，作為 
`cq:allowedTemplates` 此資料夾的屬性包含名稱開頭為的所有範本 `experience-fragment`. 客戶可以更新此屬性，以包含自己的命名配置或範本位置。

1. [允許的範本](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) 可在體驗片段主控台中設定。

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## 體驗片段的元件 {#components-for-experience-fragments}

[開發元件](/help/sites-developing/components.md) 搭配/在體驗片段中使用時，請遵循標準實務。

唯一額外的設定是確保元件能夠 [在範本上允許，這是透過內容原則達成](/help/sites-developing/page-templates-editable.md#content-policies).

## 體驗片段連結重寫器提供者 — HTML {#the-experience-fragment-link-rewriter-provider-html}

在AEM中，您可以建立體驗片段。 体验片段：

* 由一組元件及配置圖組成，
* 可以獨立於AEM頁面存在。

這類群組的使用案例之一，是將內容內嵌於第三方接觸點，例如Adobe Target。

### 預設連結重寫 {#default-link-rewriting}

使用 [匯出至目標](/help/sites-administering/experience-fragments-target.md) 功能，您可以：

* 建立體驗片段，
* 新增元件，
* 然後以HTML格式或JSON格式將其匯出為Adobe Target選件。

此功能可以 [已在AEM的作者執行個體上啟用](/help/sites-administering/experience-fragments-target.md#Prerequisites). 它需要有效的Adobe Target設定，以及Link Externalizer設定。

Link Externalizer可用來判斷建立Target選件的HTML版本時所需的正確URL，此版本隨後會傳送至Adobe Target。 這是必要的，因為Adobe Target要求可以公開存取TargetHTML選件內的所有連結；這表示連結參照的任何資源以及體驗片段本身，都必須先發佈，才能使用。

根據預設，當您建構TargetHTML選件時，要求會傳送至AEM中的自訂Sling選取器。 此選取器稱為 `.nocloudconfigs.html`. 顧名思義，它會建立體驗片段的純HTML轉譯，但不包括雲端設定（這會是多餘的資訊）。

產生HTML頁面後，Sling重寫程式管線會修改輸出：

1. 此 `html`， `head`、和 `body` 元素取代為 `div` 元素。 此 `meta`， `noscript` 和 `title` 元素會被移除（它們是原始元素的子元素） `head` 元素，當此元素被取代時，不會考慮和 `div` 元素)。

   這麼做是為了確保HTMLTarget選件可包含在Target活動中。

1. AEM會修改HTML中出現的任何內部連結，使其指向已發佈的資源。

   若要決定要修改的連結，AEM會對HTML元素的屬性遵循此模式：

   1. `src` 屬性
   1. `href` 屬性
   1. `*-src` 屬性（如data-src、custom-src等）
   1. `*-href` 屬性(類似 `data-href`， `custom-href`， `img-href`、等)

   >[!NOTE]
   >
   >在大多數情況下，HTML中的內部連結是相對連結，但自訂元件在HTML中可能會提供完整URL的情況。 依預設，AEM會忽略這些完整的URL且不會進行任何修改。

   這些屬性中的連結會透過AEM Link Externalizer執行 `publishLink()` 以便將URL重新建立為在已發佈的例項上，而且是公開可用的。

使用現成可用的實作時，上述流程應足以從體驗片段產生Target選件，然後將其匯出至Adobe Target。 不過，此程式並未說明部分使用案例，其中包括：

* Sling對應僅在發佈執行個體上可用
* Dispatcher重新導向

對於這些使用案例，AEM會提供連結重寫程式提供者介面。

### 連結重寫程式提供者介面 {#link-rewriter-provider-interface}

>[!NOTE]
>
>此介面已在以下內容中介紹： [AEM 6.5 SP1 (6.5.1.0)](/help/release-notes/previous/6.5.1.md).

對於較複雜的情況，不在 [預設](#default-link-rewriting)，AEM提供連結重寫程式提供者介面。 這是 `ConsumerType` 介面，可實作於套件組合中，作為服務。 它會繞過AEM對HTML選件的內部連結（從體驗片段轉譯）執行的修改。 此介面可讓您自訂重寫內部HTML連結的程式，以符合您的業務需求。

實作此介面作為服務的使用案例範例包括：

* Sling對應已在發佈執行個體上啟用，但在作者執行個體上未啟用
* Dispatcher或類似技術可用來在內部重新導向URL
* 有 `sling:alias mechanisms` 資源就位

>[!NOTE]
>
>此介面只會處理來自所產生Target選件的內部HTML連結。

連結重寫程式提供者介面( `ExperienceFragmentLinkRewriterProvider`)如下所示：

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### 如何使用連結重寫程式提供者介面 {#how-to-use-the-link-rewriter-provider-interface}

若要使用介面，您首先需要建立包含實作連結重寫程式提供者介面的新服務元件的組合。

此服務將用於插入Experience Fragment Export to Target重新寫入，以便存取各種連結。

例如， `ComponentService`：

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

為了讓服務發揮作用，現在需要在服務內實作三種方法：

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

您需要向系統指出在對特定體驗片段變數進行匯出到Target呼叫時，它是否需要重寫連結。 若要這麼做，請實作方法：

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

例如：

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

此方法會以引數的形式接收「匯出至目標」系統目前正在重寫的體驗片段變數。

在上述範例中，我們想要重寫：

* 中的連結 `src`

* `href` 僅限屬性

* 針對特定體驗片段：
   `/content/experience-fragment/master`

任何透過「匯出至目標」系統的其他體驗片段會遭忽略，且不會受到此服務中實作的變更影響。

#### rewriteLink {#rewritelink}

針對受重寫程式影響的體驗片段變數，它會繼續讓服務處理連結重寫。 每當內部HTML中出現連結時，就會叫用下列方法：

`rewriteLink(String link, String tag, String attribute)`

作為輸入，方法會接收引數：

* `link`不为目标组件考虑  
`String` 表示目前處理中的連結。 這通常是指向作者執行個體上資源的相對URL。

* `tag`
目前處理中的HTML元素名稱。

* `attribute`
確切的屬性名稱。

例如，如果「匯出至目標」系統目前正在處理此元素，您可以定義 `CSSInclude` 作為：

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

對的呼叫 `rewriteLink()` 方法可使用下列引數完成：

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

建立服務時，您可以根據指定的輸入進行決策，然後相應地重寫連結。

舉例來說，我們想要移除 `/etc.clientlibs` URL的一部分並新增適當的外部網域。 為了簡單起見，我們將考慮我們有權存取您服務的資源解析器，例如 `rewriteLinkExample2`：

>[!NOTE]
>
>如需有關如何透過服務使用者取得資源解析器的詳細資訊，請參閱 [AEM中的服務使用者](/help/sites-administering/security-service-users.md).

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>如果上述方法傳回 `null`，則「匯出至Target」系統將保持連結不變，即資源的相對連結。

#### 優先順序 — getPriority {#priorities-getpriority}

需要多個服務來迎合不同體驗片段的型別並不罕見，甚至需要有一個通用服務來處理所有體驗片段的外部化和對應。 在這些情況下，可能會發生與使用哪個服務相關的衝突，因此AEM提供了定義 **優先順序** 適用於不同服務。 使用下列方法指定優先順序：

* `getPriority()`

此方法允許使用多項服務，其中 `shouldRewrite()` 對於相同的體驗片段，方法會傳回true。 從中傳回最高數字的服務 `getPriority()`方法是處理體驗片段變數的服務。

例如，您可以建立 `GenericLinkRewriterProvider` 會處理所有體驗片段的基本對應，以及當 `shouldRewrite()` 方法傳回 `true` 適用於所有體驗片段變數。 針對數個特定體驗片段，您可能需要特殊處理，因此在此情況下，您可以提供 `SpecificLinkRewriterProvider` 對於 `shouldRewrite()` 方法只會傳回部分體驗片段變數的true。 若要確保 `SpecificLinkRewriterProvider` 被選擇用於處理這些體驗片段變數，它必須返回其 `getPriority()` 方法數字大於 `GenericLinkRewriterProvider.`
