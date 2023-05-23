---
title: JCR整合
seo-title: JCR Integration
description: 您必須何時在JCR層級整合的秘訣
seo-description: Tips for when you must integrate at the JCR level
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
exl-id: 170474c1-c7f4-446c-bda4-84768d44a078
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# JCR整合{#jcr-integration}

## 與JCR API相比，偏好Sling Resource API {#prefer-the-sling-resource-api-to-jcr-api}

Sling API的運作方式比JCR API更高、更抽象。 這可讓您的程式碼可重複使用且獨立於基礎儲存空間。 這可讓您可以視需要透過ResourceProvider機制包含外部虛擬資料更容易。

## 儘可能避免查詢 {#avoid-queries-wherever-possible}

導覽存放庫以擷取資料的速度一律比執行查詢來得快。 在某些情況下需要查詢，例如一般使用者查詢或需要從整個存放庫尋找結構化內容，但對於所有其他情況，最好導覽至必要的節點。 在轉譯邏輯（例如導覽元件、「最近專案清單」、專案計數等）中應一律避免查詢。 在這些情況下，最好是逐步瀏覽階層或預先快取結果，以便在轉譯時可直接使用。

## 限制JCR觀察的範圍 {#restrict-the-scope-of-jcr-observation}

在監聽存放庫中的事件時，請務必儘可能縮小範圍。 例如，聆聽位於以下位置的事件，會好很多 `/etc/mycompany` 比聆聽更重要 `/etc`. 永遠不要接聽存放庫根目錄中的事件。 此外，請確定回呼方法會在沒有可做的事情時儘快執行。

## 不再使用JCR管理員存取權 {#eliminate-use-of-jcr-admin-access}

自AEM 6起，登入管理功能已過時，例如從ResourceResolverFactory取得管理工作階段。 而是應該為需要此類存取權的後台作業建立服務帳號，並且可以使用ResourceResolverFactory來取得此帳號的ResourceResolver。
