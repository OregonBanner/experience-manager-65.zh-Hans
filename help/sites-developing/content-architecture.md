---
title: 內容架構
seo-title: Content Architecture
description: 架構內容的秘訣（提示 — 一切都是內容）
seo-description: Tips for architecting your content in Adobe Experience Manager (AEM). (hint - everything is content)
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# 內容架構{#content-architecture}

## 遵循David的模式 {#follow-david-s-model}

David&#39;s Model是由David Nuescheler在多年前所撰寫，但現今的想法仍然成立。 David模型的主要原則如下：

* 資料為先，結構為後。 可能會。
* 推動內容階層，不要讓它發生。
* 工作區用於 `clone()`， `merge()`、和 `update()`.
* 注意同名的同層級。
* 參照會被視為有害。
* 檔案就是檔案。
* ID是邪惡的。

David的模型可在Jackrabbit維基百科上找到，網址為 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### 一切都是內容 {#everything-is-content}

所有資料都應儲存在存放庫中，而不是依賴獨立的第三方資料來源，例如資料庫。 這適用於編寫的內容、二進位資料，例如影像、程式碼、設定等。 這可讓我們使用一組API來管理所有內容，並透過復寫管理此內容的促銷活動。 此外，我們還可以獲得備份、記錄等單一來源。

### 使用「內容模型優先」設計原則 {#use-the-content-model-first-design-principle}

建立新功能時，請一律先設計JCR內容結構，然後考慮使用預設的Sling servlet閱讀和寫入內容。 這可讓您確保實作可搭配現成可用的存取控制機制運作，並讓您避免產生不必要的CRUD樣式servlet。

### Be RESTful {#be-restful}

Servlet應根據resourceTypes而不是路徑來定義。 這可讓您使用JCR存取控制、遵守REST原則，並使用在請求中提供給我們的資源和資源解析器。 這也允許我們變更在伺服器端轉譯URL的指令碼，而不需要變更使用者端的URL，同時隱藏使用者端的伺服器端實作詳細資料，以提升安全性。

### 避免定義新節點型別 {#avoid-defining-new-node-types}

節點型別在基礎結構層中的作用較低，大多數需求都可以通過使用指派給nt：unstructured、oak：Unstructured、sling：Folder或cq：Page節點型別的sling：resourceType來滿足。 節點型別等同於存放庫中的結構描述，之後變更節點型別可能會非常昂貴。

### 遵守JCR中的命名慣例 {#adhere-to-naming-conventions-in-the-jcr}

遵循命名慣例可增加程式碼庫的一致性，降低缺陷的發生率，並提升開發人員在系統中工作的速度。 Adobe在開發AEM時會使用下列慣例：

* 節點名稱

   * 全部小寫
   * 使用連字型大小分隔文字

* 屬性名稱

   * 駝峰式大小寫，以小寫字母開頭

* 元件(JSP/HTML)

   * 全部小寫
   * 使用連字型大小分隔文字
