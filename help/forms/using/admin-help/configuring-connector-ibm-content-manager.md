---
title: 設定IBM Content Manager的聯結器
seo-title: Configuring Connector for IBM Content Manager
description: 設定IBM內容管理員的聯結器，以啟用AEM表單與IBM內容管理員之間的通訊。
seo-description: Configure the Connector for IBM Content Manager to enable communication between AEM forms and IBM Content Manager.
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 設定IBM Content Manager的聯結器{#configuring-connector-for-ibm-content-manager}

IBM Content Manager聯結器可啟用AEM Forms與IBM Content Manager之間的通訊。 如需其他背景資訊，請參閱以下的「Connectors for ECM」： [服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 設定IBM內容管理員連線 {#configure-the-ibm-content-manager-connection}

1. 在管理控制檯中，按一下「服務> IBM Content Manager的聯結器」。
1. 在「資料存放區名稱」方塊中，輸入您要連線的IBM Content Manager資料存放區名稱。 如果資料庫是本機資料庫，請輸入資料庫名稱。 如果資料庫是遠端資料庫，請輸入其別名。
1. 在「使用者名稱」方塊中，輸入將連線至IBM Content Manager資料存放區之使用者的使用者ID。
1. 在密碼方塊中，輸入使用者的密碼。
1. （選擇性）在別名連線字串方塊中，輸入其他連線引數。 在大多數情況下，此方塊應該是空的。 如需詳細資訊，請參閱您的IBM檔案。
1. 单击“保存”。

## 驗證服務設定 {#validation-of-service-settings}

如果您輸入不正確的dataStore別名、使用者名稱或密碼，根據IBM Content Manager服務的Content Repository Connector目前是否在執行中，您會得到以下結果：

* 如果服務已停止，當您儲存服務組態資訊時，不會出現任何錯誤。 不過，下次啟動服務時，將會擲回例外狀況，且服務不會啟動。
* 如果服務已啟動，當您儲存服務組態資訊時，服務會立即嘗試驗證認證資訊。 在這種情況下，會發生錯誤且未儲存設定資訊。
