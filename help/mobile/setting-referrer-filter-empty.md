---
title: 將反向連結篩選設定為允許空白
seo-title: Setting Your Referrer Filter to Allow Empty
description: 請依照本頁面的說明了解反向連結篩選條件。 為了允許AEM Mobile應用程式檢視器在您的Author執行個體上檢視應用程式，您需要將HTML反向連結篩選設定為「允許空白」。
seo-description: Follow this page to learn about Referrer Filter. In order to allow the AEM Mobile Application Viewer to view apps on your Author instance, you'll need to set your HTML referrer filter to 'allow empty'.
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 3%

---

# 將反向連結篩選設定為允許空白{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

為了允許AEM Mobile應用程式檢視器在您的Author執行個體上檢視應用程式，您需要將HTML反向連結篩選設定為「允許空白」。

如果您不打算使用Application Viewer來檢閱處於開發和測試狀態的應用程式，則不需要變更反向連結篩選器的預設設定。

在您執行中的AEM作者例項中，導覽至： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) 和搜尋「Apache Sling反向連結篩選器」。 按一下以編輯反向連結篩選條件，並勾選「允許空白」核取方塊（請參閱下圖）。 接著，按一下「儲存」按鈕並關閉瀏覽器頁面。

![反向連結篩選設定](assets/chlimage_1-106.png)
