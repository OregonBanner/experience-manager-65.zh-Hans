---
title: 存取裝置功能
seo-title: Access Device Features
description: 請依照本頁所述操作，瞭解如何建置存取裝置功能的AEM元件。 AEM PhoneGap Kitchen Sink Github存放庫為開發人員提供功能性AEM應用程式，該應用程式可說明如何使用多個核心Cordova API。
seo-description: Follow this page to learn about building AEM components that access device features. The AEM PhoneGap Kitchen Sink Github repository provides developers with a functional AEM app that illustrates the use of a number of core Cordova APIs.
uuid: 1996f017-21d3-4d90-9f55-95c626bc4c60
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 0019e367-8edc-4a23-bfa4-5beda266ace6
exl-id: 385f7924-e8ab-4dcb-83f0-7b81bead3dda
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 2%

---

# 存取裝置功能{#access-device-features}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

## 建置存取裝置功能的AEM元件 {#building-aem-components-that-access-device-features}

此 [AEM PhoneGap廚房水槽](https://github.com/blefebvre/aem-phonegap-kitchen-sink) Github存放庫為開發人員提供了一個功能性AEM應用程式，該應用程式說明了如何使用許多核心Cordova API。 透過PhoneGap CLI在iOS或Android上執行時，應用程式會開啟至下列頁面，其中包括其示範之每個裝置API的連結：

![chlimage_1-107](assets/chlimage_1-107.png)

這些裝置API元件的原始碼都是 [適用於Github](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/apps/brucelefebvre/kitchen-sink/components).

如需每個API使用方式的詳細資訊，我建議您檢視 [Cordova外掛程式檔案](https://docs.phonegap.com/en/4.0.0/cordova_plugins_pluginapis.md.html).

## 后续步骤 {#the-next-steps}

另請參閱 [透過AdobeMobile Analytics追蹤應用程式效能](/help/mobile/phonegap-intro-to-app-analytics.md).
