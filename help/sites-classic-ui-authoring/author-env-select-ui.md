---
title: 選取您的UI
description: 為了方便編寫使用者，觸控式UI在必要時可切換至傳統UI。
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 選取您的UI{#selecting-your-ui}

由於觸控式UI會取代傳統UI，AEM執行個體的使用者或管理員必須做出有效決定，才能繼續使用傳統UI。 由於傳統UI已不再受到維護，因此編寫使用者無法僅從傳統UI切換至觸控式UI中的同等專案。

為了方便編寫使用者，觸控式UI在必要時可切換至傳統UI。 請參閱 [選取您的UI](/help/sites-authoring/select-ui.md) 詳細資訊，請參閱標準撰寫檔案。

>[!NOTE]
>
>從舊版升級的執行個體將保留傳統UI以進行頁面編寫。
>
>升級後，頁面製作功能不會自動切換至觸控式UI，但您可以使用[OSGi設定](/help/sites-deploying/configuring-osgi.md) 的 **WCM編寫UI模式服務** ( `AuthoringUIMode` 服務)。 另請參閱 [編輯器的使用者介面覆寫](#uioverridesfortheeditor).

## 為您的執行個體設定預設UI {#configuring-the-default-ui-for-your-instance}

系統管理員可以使用設定啟動時看到的UI和登入 [根對應](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

這可以由使用者預設值或工作階段設定來覆寫。
