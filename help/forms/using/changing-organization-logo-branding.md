---
title: 變更品牌推廣的組織標誌
seo-title: Changing the organization logo for branding
description: 若要品牌化AEM Forms工作區，請自訂預設標誌，以提供您組織的標誌。
seo-description: To brand AEM Forms workspace provide the logo of your organization by customizing the default logo.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# 變更品牌推廣的組織標誌 {#changing-the-organization-logo-for-branding}

組織標誌會顯示在AEM Forms工作區的左上角。 若要更新標誌，請遵循 [AEM Forms工作區自訂的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) 然後執行下列步驟。

1. 建立標誌並將檔案命名為 `NewWorkspace.png`. 使用WebDAV使用者端將影像檔案放入/apps/ws/images資料夾。

   >[!NOTE]
   >
   >建議使用的標誌影像大小為218畫素×20畫素。

   >[!NOTE]
   >
   >如需有關WebDAV存取的詳細資訊，請參閱 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans).

1. 新增下列樣式，以參考樣式表中的新標誌影像：/apps/ws/css/newStyle.css。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
