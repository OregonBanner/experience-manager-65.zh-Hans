---
title: 安全性
seo-title: Security
description: 應用程式安全性在開發階段啟動
seo-description: Application Security starts during the development phase
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: c55b70ec11842d3f7d82adbf552b2624c1dcc599
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 安全性{#security}

Application Security在開發階段啟動。 Adobe建議套用下列安全性最佳實務。

## 使用請求工作階段 {#use-request-session}

根據最低許可權原則，Adobe建議使用繫結至使用者要求的工作階段和適當的存取控制，來完成每個存放庫存取權。

## Protect避免跨網站指令碼(XSS) {#protect-against-cross-site-scripting-xss}

跨網站指令碼(XSS)可讓攻擊者將程式碼插入其他使用者檢視的網頁中。 惡意的網頁使用者可以利用這個安全性弱點來略過存取控制。

AEM會套用輸出時篩選所有使用者提供內容的原則。 在開發和測試期間，防止XSS都被賦予最高優先權。

AEM提供的XSS保護機制是以 [AntiSamy Java資料庫](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 提供者 [OWASP (Open Web Application Security Project)](https://www.owasp.org/). 預設AntiSamy設定可在以下網址找到：

`/libs/cq/xssprotection/config.xml`

請務必透過覆蓋設定檔案來調整此設定，以符合您自己的安全性需求。 官方 [AntiSamy檔案](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 會提供您實作安全性需求所需的所有資訊。

>[!NOTE]
>
>我們強烈建議您務必使用 [AEM提供的XSSAPI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

此外，Web應用程式防火牆，例如 [Apache適用的mod_security](https://www.modsecurity.org)，可提供部署環境安全性的可靠集中控制，並抵禦先前未偵測到的跨網站指令碼攻擊。

## 存取Cloud Service資訊 {#access-to-cloud-service-information}

>[!NOTE]
>
>Cloud Service資訊的ACL以及保護執行個體所需的OSGi設定，會隨著以下步驟而自動化： [生產就緒模式](/help/sites-administering/production-ready.md). 雖然這表示您不需要手動進行設定變更，但建議您先檢閱變更，然後再開始部署。

當您 [將您的AEM執行個體與Adobe Marketing Cloud整合](/help/sites-administering/marketing-cloud.md) 您使用 [Cloud Service設定](/help/sites-developing/extending-cloud-config.md). 這些組態的相關資訊以及所收集的任何統計資料都會儲存在儲存區域中。 如果您使用此功能，建議您檢閱此資訊的預設安全性是否符合您的需求。

webservicesupport模組會將統計資料和設定資訊寫入下列位置：

`/etc/cloudservices`

使用預設許可權：

* 作者環境： `read` 的 `contributors`

* 發佈環境： `read` 的 `everyone`

## Protect抵禦跨網站請求偽造攻擊 {#protect-against-cross-site-request-forgery-attacks}

如需AEM用於緩解CSRF攻擊的安全性機制的詳細資訊，請參閱 [Sling查閱者篩選器](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 安全性檢查清單的區段及 [CSRF Protection Framework檔案](/help/sites-developing/csrf-protection.md).
