---
title: 选择您的UI
description: 为了方便用户创作，触屏UI允许在必要时切换到经典UI。
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

# 选择您的UI{#selecting-your-ui}

由于触屏优化UI取代了经典UI，因此AEM实例的用户或管理员必须做出积极决定，以继续使用经典UI。 由于经典UI不再进行维护，因此创作用户无法简单地从经典UI切换到触屏UI中的等效UI。

为了方便用户创作，触屏UI允许在必要时切换到经典UI。 请参阅 [选择您的UI](/help/sites-authoring/select-ui.md) ，以了解详细信息。

>[!NOTE]
>
>从以前版本升级的实例将保留经典UI用于页面创作。
>
>升级后，页面创作不会自动切换到触屏UI，但您可以使用[OSGi配置](/help/sites-deploying/configuring-osgi.md) 的 **WCM创作UI模式服务** ( `AuthoringUIMode` 服务)。 请参阅 [编辑器的UI覆盖](#uioverridesfortheeditor).

## 为实例配置默认UI {#configuring-the-default-ui-for-your-instance}

系统管理员可以使用配置启动和登录时显示的UI [根映射](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

该设置可能会被用户默认设置或会话设置所覆盖。
