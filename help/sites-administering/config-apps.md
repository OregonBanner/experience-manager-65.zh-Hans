---
title: 為AEM應用程式進行設定
seo-title: Configuring for AEM Apps
description: 瞭解如何設定AEM應用程式。
seo-description: Learn how to configure AEM Apps.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 為AEM應用程式進行設定{#configuring-for-aem-apps}

Adobe Experience Manager應用程式可讓您透過無線方式更新應用程式的內容(OTA)。 更新的內容會儲存在發佈執行個體上。 若要允許裝置上的應用程式連線至發佈執行個體並檢查更新，需要將發佈執行個體設定為允許空的反向連結標頭。

## 設定空的反向連結標頭 {#configuring-empty-referrer-header}

若要設定反向連結篩選服務：

* 開啟Apache Felix主控台(**設定**)於：
* https://&lt;server>：&lt;port_number>/system/console/configMgr
* 以管理員身分登入。
* 在 **設定** 功能表，選取： *Apache Sling查閱者篩選器*
* 勾選「允許空白」欄位，以允許空白/缺少反向連結標題。
* 按一下 **儲存** 以儲存變更。

![chlimage_1-58](assets/chlimage_1-58a.png)

請參閱 [OSGI組態設定](/help/sites-deploying/osgi-configuration-settings.md) 和 [安全性檢查清單 — 跨網站請求偽造問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 以取得更多詳細資料。
