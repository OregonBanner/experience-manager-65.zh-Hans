---
title: 更改品牌的组织徽标
seo-title: 更改品牌的组织徽标
description: 要品牌AEM Forms工作区，请通过自定义默认徽标来提供您组织的徽标。
seo-description: 要品牌AEM Forms工作区，请通过自定义默认徽标来提供您组织的徽标。
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# 更改品牌{#changing-the-organization-logo-for-branding}的组织徽标

组织徽标显示在AEM Forms工作区的左上角。 要更新标志，请按照AEM Forms工作区自定义](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization)的[常规步骤操作，然后执行以下步骤。

1. 创建标志并将文件命名为`NewWorkspace.png`。 使用WebDAV客户端将图像文件放入/apps/ws/images文件夹。

   >[!NOTE]
   >
   >徽标图像的建议大小为218 px × 20 px。

   >[!NOTE]
   >
   >有关WebDAV访问的详细信息，请参阅[https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)。

1. 通过添加以下样式，在样式表/apps/ws/css/newStyle.css中引用新的徽标图像。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
