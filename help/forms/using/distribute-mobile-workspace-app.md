---
title: 發佈AEM Forms應用程式
seo-title: Distribute AEM Forms app
description: 使用行動裝置管理(MDM)在行動裝置上大規模部署應用程式。
seo-description: Use Mobile Device Management (MDM) for the large-scale deployment of apps on mobile devices.
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# 發佈AEM Forms應用程式 {#distribute-aem-forms-app}

行動裝置管理(MDM)可讓您在行動裝置上大規模部署應用程式。

>[!NOTE]
>
>此發佈僅適用於iOS和Android裝置。

## MDM解決方案通常提供的主要功能： {#main-features-generally-provided-by-mdm-solutions}

* 在您的企業環境中啟用裝置註冊
* 允許設定和更新裝置設定
* 強制執行安全性法規遵循。
* 以行動裝置安全地存取公司資源

MDM解決方案搭配行動應用程式管理，可讓您透過企業內的行動裝置，管理內部、公開和購買的應用程式。

MDM管理員可以將ipa和apk檔案上傳到MDM伺服器，並控制可以存取ipa或apk檔案的使用者。 管理員也可以控制每個應用程式對應的設定檔設定。

## 影響AEM Forms應用程式的設定檔設定 {#profile-settings-affecting-the-aem-forms-app-br}

裝置上的下列設定檔設定將會影響裝置上AEM Forms應用程式的運作：

* **允許使用相機** 在 **裝置功能** 區段

如果您停用 **允許使用相機**，的相機功能 [像片註解](/help/forms/using/add-attachments.md) 將無法運作。 您必須啟用此選項，才能在應用程式中使用相機。

* **需要裝置上的密碼** 在密碼原則區段中

若要啟用 **應用程式資料的加密**，建議您啟用 **密碼** 在您的裝置上。 如果未在裝置上設定密碼，則儲存在裝置上的應用程式資料不會加密。
