---
title: 大量安全資訊傳遞
seo-title: High-volume secure information delivery
description: Document Security支援將授權與使用者相關聯，而不是與大量生產環境中的檔案相關聯。
seo-description: Document security supports the association of licenses to users, rather than to the documents in mass production environments.
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
feature: Document Security
exl-id: 616e8821-ca96-4471-9120-0e1076a06178
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# 大量安全資訊傳遞 {#high-volume-secure-information-delivery}

在大量生產環境中（例如為電信公司產生每月安全發票的環境），建立每個檔案特定的授權可能會成為資源密集的過程。 在這種情況下，Document Security支援將授權與使用者相關聯，而不是與檔案相關聯。 為使用者產生的授權將用於為該使用者保護的所有檔案。

此方法的一個優點是Document Security資料庫的大小不會隨著檔案線性增加，而是隨著使用者人數線性增加。 此外，由於您只需為使用者建立一次授權，因此透過這些原則後續保護檔案的速度會更快。 所有這類檔案都支援離線存取、檔案到期和撤銷等功能。

Document Security也支援抽象原則。 抽象原則是包含所有原則屬性（例如Document Security設定和使用許可權）但不包含主參與者清單的原則範本。 管理員可以從抽象原則建立任意數量的原則，這些原則包含應該具有檔案存取權的不同主體。 對抽象原則所做的變更不會影響從抽象原則產生的實際原則。

在電信公司每月產生發票的情況下，您可以建立抽象原則、建立使用者，然後為每個使用者產生唯一授權。 授權稍後會套用至每個使用者的檔案。

僅支援透過Document Security Java SDK建立抽象原則。 但是，您可以管理從Document Security網頁的抽象原則建立的原則。 使用此方法建立的原則，其行為與從Document Security網頁建立的原則相同。

另請參閱 [使用AEM表單程式設計](https://www.adobe.com/go/learn_aemforms_programming_63) 以取得詳細資訊。
