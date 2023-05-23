---
title: SocialUtils重構
seo-title: SocialUtils Refactoring
description: AEM 6.1已棄用套件com.adobe.cq.social.ugcbase.SocialUtils
seo-description: The package com.adobe.cq.social.ugcbase.SocialUtils was deprecated in AEM 6.1
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 1%

---

# SocialUtils重構 {#socialutils-refactoring}

## 已棄用SocialUtils套件 {#socialutils-package-deprecated}

套件 `com.adobe.cq.social.ugcbase.SocialUtils` 在AEM 6.1中已過時。

下表列出取代的方法 `SocialUtils` 方法。

## SocialResourceUtilities套件  {#socialresourceutilities-package}

| com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities中的方法 |
|---|
| 布林值checkPermission(ResourceResolver resolver， String path， String action) |  |
| SocialResourceProvider getSocialResourceProvider(Resource) |  |
| SocialResourceConfiguration getStorageConfig(Resource) |  |
| 資源getUGCResource(Resource userResource) |  |
| 資源getUGCResource(Resource userResource， ResourceResolverFactory rrf) | 新建 |
| 資源getUGCResource(Resource userResource， ResourceResolverFactory rrf， String resourceTypeHint) | 新建 |
| 資源getUGCResource(Resource userResource， String resourceTypeHint) |  |
| 布林值hasModeratePermissions(Resource) |  |
| 字串resourceToACLPath(Resource) |  |
| 字串resourceToUGCStoragePath(Resource) | 取代String resourceToUGCPath（資源） |
| 字串UGCToResourcePath(Resource) |  |
| 字串UGCToResourcePath（字串ugcPath） | 方法簽章已變更 |
| 字串UGCToResourcePath（字串ugcPath， ResourceResolver resolver） | 新建 |

| 中的方法 `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider(Resource) | 取代SocialResourceProvider getConfiguredProvider(Resource) |

## SCFUtilities套件 {#scfutilities-package}

| 中的方法 `com.adobe.cq.social.`utilities.scf.api.SCFUtitles |
|---|
| 字串getAvatar(UserProperties userProperties) |
| 字串getAvatar(UserProperties userProperties， int size) |
| 字串getAvatar(UserProperties userProperties， String absoluteDefaultAvatar) |
| 字串getAvatar(UserProperties userProperties， String absoluteDefaultAvatar， SocialUtils.AVATAR_SIZE) |
| 頁面getContainingPage(Resource) |
| 字串getSocialProfileURL（字串使用者名稱、ResourceResolver解析器、頁面頁面） |
| UserProperties getUserProperties(ResourceResolver resolver， String userId) |

## 僅供內部使用 {#for-internal-use-only}

| 布林值canAddNode（工作階段，字串路徑） |
|---|
| 字串createUniqueNameHint（字串訊息） |
| 字串createUniqueNameHint(String message， int numRandomChars) |
| 字串generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| 頁面getPage（字串路徑， ResourceResolver resolver） |
| 字串getPagePath（資源） |
| 字串getPagePath（字串路徑） |
| 字串getResourceTypeForIncludedResource（資源元件，字串defaultResourceType，字串designPropertyName） |
| 字串getResourceTypeFromDesign(Resource， String styleProperty， String defaultValue) |
| 布林值isResourceOwner(Resource) |
| 字串mapUGCPath（資源） |
| 字串mapUGCPath(String ugcPath， ResourceResolver resolver) |
| 布林值mayPost(ResourceResolver resolver， Resource) |
| 字串prepareUserGeneratedContent（ResourceResolver resolver，字串路徑） |

## 方法已無法使用 {#methods-no-longer-available}

| 節點createNode(ResourceResolver resolver， String path， String nodeType) |
|---|
| 資源getResourceAtPath（ResourceResolver resolver，字串路徑） |
| 資源getResourceAtPath（ResourceResolver resolver，字串路徑，字串資源型別） |
| 設定getStorageCloudServiceConfig（資源） |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| 布林值mayAccessUGC(ResourceResolver resolver) |
