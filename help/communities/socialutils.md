---
title: SocialUtils重构
seo-title: SocialUtils重构
description: AEM 6.1中已弃用com.adobe.cq.social.ugcbase.SocialUtils包
seo-description: AEM 6.1中已弃用com.adobe.cq.social.ugcbase.SocialUtils包
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# SocialUtils重构{#socialutils-refactoring}

## 已弃用SocialUtils包{#socialutils-package-deprecated}

AEM 6.1中已弃用包`com.adobe.cq.social.ugcbase.SocialUtils`。

下表列表了用于代替`SocialUtils`方法的方法。

## SocialResourceUtilities包{#socialresourceutilities-package}

| com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities中的方法 |
|---|
| Boolean checkPermission(ResourceResolver, String path, String action) |  |
| SocialResourceProvider getSocialResourceProvider（资源资源） |  |
| SocialResourceConfiguration getStorageConfig（资源资源） |  |
| 资源getUGCResource（资源用户资源） |  |
| 资源getUGCResource（资源用户资源，资源解析器工厂rrf） | 新版 |
| 资源getUGCResource(Resource userResource、ResourceResolverFactory rrf、String resourceTypeHint) | 新版 |
| 资源getUGCResource（资源用户资源，字符串资源类型提示） |  |
| boolean hasMedeatePermissions（资源资源） |  |
| 字符串资源ToACLPath（资源资源） |  |
| 字符串资源ToUGCStoragePath（资源资源） | 替换字符串resourceToUGCPath（资源资源） |
| 字符串UGCToResourcePath（资源资源） |  |
| 字符串UGCToResourcePath（字符串ugcPath） | 更改了签名 |
| 字符串UGCToResourcePath（字符串ugcPath，资源解析程序） | 新版 |

| `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities中的方法 |
|---|
| SocialResourceProvider getSocialResourceProvider（资源资源） | 替换SocialResourceProvider getConfiguredProvider（资源资源） |

## SCFUtilities包{#scfutilities-package}

| `com.adobe.cq.social.`utilities.scf.api.SCFUtilites中的方法 |
|---|
| 字符串getAvatar(UserProperties userProperties) |
| 字符串getAvatar(UserProperties userProperties, int size) |
| 字符串getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| 字符串getAvatar（UserProperties userProperties，字符串绝对DefaultAvatar, SocialUtils.AVATAR_SIZE） |
| 页getContainingPage（资源资源） |
| 字符串getSocialProfileURL（字符串用户名，资源解析程序，页面） |
| UserProperties getUserProperties(ResourceResolver, String userId) |

## 仅供内部使用{#for-internal-use-only}

| boolean canAddNode(Session session, String path) |
|---|
| 字符串createUniqueNameHint（字符串消息） |
| 字符串createUniqueNameHint（字符串消息， int numRandomChars） |
| 字符串generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| 页getPage（字符串路径，资源解析程序） |
| 字符串getPagePath（资源） |
| 字符串getPagePath（字符串路径） |
| 字符串getResourceTypeForIncludedResource（资源组件，字符串defaultResourceType，字符串designPropertyName） |
| 字符串getResourceTypeFromDesign（资源，字符串样式属性，字符串默认值） |
| 布尔型isResourceOwner（资源资源） |
| 字符串mapUGCPath（资源资源） |
| 字符串mapUGCPath（字符串ugcPath，资源解析程序） |
| boolean mayPost(ResourceResolver, Resource) |
| 字符串prepareUserGeneratedContent（ResourceResolver，字符串路径） |

## 方法不再可用{#methods-no-longer-available}

| Node createNode(ResourceResolver, String path, String nodeType) |
|---|
| 资源getResourceAtPath(ResourceResolver, String path) |
| 资源getResourceAtPath(ResourceResolver, String path, String resourceType) |
| 配置getStorageCloudServiceConfig（资源资源） |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| boolean mayAccessUGC(ResourceResolver) |

