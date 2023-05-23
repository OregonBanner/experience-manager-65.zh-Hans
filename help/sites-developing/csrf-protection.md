---
title: CSRF保護架構
seo-title: The CSRF Protection Framework
description: 此框架會使用代號來保證使用者端請求是合法的
seo-description: The framework makes use of tokens to guarantee that the client request is legitimate
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: f841e3886771fb00eee6e476d7111d4a335a9d51
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# CSRF保護架構{#the-csrf-protection-framework}

除了Apache Sling反向連結篩選條件外，Adobe還提供新的CSRF保護架構，可抵禦此類攻擊。

此框架會使用代號來保證使用者端請求是合法的。 代號會在表單傳送至使用者端時產生，並在表單傳回伺服器時驗證。

>[!NOTE]
>
>匿名使用者的發佈執行個體上沒有任何權杖。

## 要求 {#requirements}

### 依赖项 {#dependencies}

任何依賴 `granite.jquery` 相依性會自動受益於CSRF保護架構。 若您的任何元件不是這種情況，您必須將相依性宣告至 `granite.csrf.standalone` 之後才能使用架構。

### 複製加密金鑰 {#replicating-crypto-keys}

為了使用權杖，您需要將HMAC二進位檔復寫至部署中的所有執行個體。 另請參閱 [複製HMAC金鑰](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key) 以取得更多詳細資料。

>[!NOTE]
>
>請確定您也做了必要的 [Dispatcher設定變更](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) 以使用CSRF保護架構。

>[!NOTE]
>
>如果您使用資訊清單快取搭配網頁應用程式，請務必新增&quot;**&amp;ast；**」至資訊清單，以確保權杖不會使CSRF權杖產生呼叫離線。 如需詳細資訊，請參閱此 [連結](https://www.w3.org/TR/offline-webapps/).
>
>如需有關CSRF攻擊及緩解這些攻擊之方法的詳細資訊，請參閱 [跨網站請求偽造OWASP頁面](https://owasp.org/www-community/attacks/csrf).
