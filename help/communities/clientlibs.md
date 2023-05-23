---
title: Communities元件的Clientlibs
seo-title: Clientlibs for Communities Components
description: 適用於社群的使用者端程式庫
seo-description: Client-side libraries for Communities
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# Communities元件的Clientlibs {#clientlibs-for-communities-components}

## 简介 {#introduction}

本檔案本節說明如何將使用者端程式庫(clientlibs)新增至Communities元件的頁面。

如需基本資訊，請造訪：

* [使用使用者端資料庫](/help/sites-developing/clientlibs.md) 其中會提供使用方式詳細資訊以及偵錯工具
* [適用於SCF的Clientlibs](/help/communities/client-customize.md#clientlibs) 提供自訂SCF元件時的實用資訊


## 為何需要Clientlibs {#why-clientlibs-are-required}

元件正常運作(JavaScript)和樣式(CSS)需要Clientlibs。

當存在 [社群功能](/help/communities/functions.md) 針對功能，所有必要的元件和設定（包括必要的clientlibs）都會顯示在社群網站中。 只有當作者可以使用其他元件時，才需要新增其他clientlibs。

當缺少必要的clientlibs時， [將Communities元件新增至頁面](/help/communities/author-communities.md) 可能會導致javascript錯誤及意外外觀。

### 範例：置入的評論沒有Clientlibs {#example-placed-reviews-without-clientlibs}

![置入的評論](assets/placed-reviews.png)

### 範例：使用Clientlibs置入稽核 {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## 識別必要的Clientlibs {#identifying-required-clientlibs}

開發人員的基本功能資訊可識別所需的clientlibs。

此外，從AEM執行個體瀏覽至 [社群元件指南](/help/communities/components-guide.md) 提供元件所需clientlib類別清單的存取權。

例如，在最上方的 [評論頁面](https://localhost:4502/content/community-components/en/reviews.html) 列出的必要clientlibs包括

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## 新增必要的Clientlibs {#adding-required-clientlibs}

當想要將Communities元件新增到頁面時，如果元件尚未出現，則需要新增必要的clientlibs。

使用 [CRXDE|Lite](#using-crxde-lite) 修改社群網站頁面的現有clientlibslist。

若要使用為社群網站新增clientlib [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)：

* 瀏覽至 [https://&lt;server>：&lt;port>/crx/de](https://localhost:4502/crx/de).
* 找到 `clientlibslist` 要新增元件的頁面節點：

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* 替換為 `clientlibslist` 選取的節點：

   * 找到字串[] 屬性 `scg:requiredClientLibs`.
   * 選取其 `Value` 以存取字串陣列對話方塊。

      * 如有需要，向下捲動。
      * 選取+以輸入新的使用者端資源庫。

         * 重複以上步驟以新增更多使用者端程式庫。

         * 選取 **確定**.
   * 選取 **全部儲存**.


>[!NOTE]
>
>如果網站不是社群網站，則需要探索用於網站的使用者端程式庫的存在或位置。

使用 [AEM Communities快速入門](/help/communities/getting-started.md) 範例，其中 `site-name` 是 *參與*，這是新增檢閱元件時clientliblist的顯示方式：

![review-component](assets/review-component.png)
