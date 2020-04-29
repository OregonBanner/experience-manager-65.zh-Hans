---
title: SocialUtils重构
seo-title: SocialUtils重构
description: com.adobe.cq.social.ugcbase.SocialUtils包已在AEM 6.1中弃用
seo-description: com.adobe.cq.social.ugcbase.SocialUtils包已在AEM 6.1中弃用
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
translation-type: tm+mt
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# SocialUtils重构 {#socialutils-refactoring}

## 已弃用SocialUtils包 {#socialutils-package-deprecated}

AEM 6. `com.adobe.cq.social.ugcbase.SocialUtils` 1中已弃用该包。

下表列表了用于代替SocialUtils方法的方法。

## SocialResourceUtilities包 {#socialresourceutilities-package}

| com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities中的方法 |
|---|
| Boolean checkPermission（ResourceResolver解析程序，字符串路径，字符串操作） |  |
| SocialResourceProvider getSocialResourceProvider（资源资源） |  |
| SocialResourceConfiguration getStorageConfig（资源资源） |  |
| 资源getUGCResource（资源用户资源） |  |
| 资源getUGCResource(Resource userResource, ResourceResolverFactory rrf) | 新版 |
| 资源getUGCResource(Resource userResource、ResourceResolverFactory rrf、String resourceTypeHint) | 新版 |
| 资源getUGCResource(Resource userResource, String resourceTypeHint) |  |
| boolean hasMeadePermissions（资源资源） |  |
| 字符串resourceToACLPath（资源资源） |  |
| 字符串resourceToUGCStoragePath（资源资源） | 替换字符串resourceToUGCPath（资源资源） |
| 字符串UGCToResourcePath（资源资源） |  |
| 字符串UGCToResourcePath（字符串ugcPath） | 更改了签名 |
| 字符串UGCToResourcePath（字符串ugcPath, ResourceResolver） | 新版 |

| utilities.resource.api. `com.adobe.cq.social.`SocialResourceUtilities中的方法 |
|---|
| SocialResourceProvider getSocialResourceProvider（资源资源） | 替换SocialResourceProvider getConfiguredProvider（资源资源） |

## SCFUtilities包 {#scfutilities-package}

| utilities.scf.api. `com.adobe.cq.social.`SCFUtilites中的方法 |
|---|
| 字符串getAvatar(UserProperties userProperties) |
| 字符串getAvatar(UserProperties userProperties, int size) |
| 字符串getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| 字符串getAvatar(UserProperties userProperties, String absoluteDefaultAvatar, SocialUtils.AVATAR_SIZE) |
| 页面getContainingPage（资源） |
| 字符串getSocialProfileURL（字符串用户名， ResourceResolver，页面） |
| UserProperties getUserProperties(ResourceResolver, String userId) |

## For Internal Use Only {#for-internal-use-only}

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
| 字符串getResourceTypeFromDesign（资源，字符串样式属性，字符串defaultValue） |
| boolean isResourceOwner（资源资源） |
| 字符串mapUGCPath（资源资源） |
| 字符串mapUGCPath(String ugcPath, ResourceResolver)解析程序 |
| boolean mayPost(ResourceResolver, Resource resource) |
| 字符串prepareUserGeneratedContent(ResourceResolver, String path) |

## 方法不再可用 {#methods-no-longer-available}

| Node createNode（ResourceResolver解析程序，字符串路径， String nodeType） |
|---|
| 资源getResourceAtPath(ResourceResolver, String path) |
| 资源getResourceAtPath（ResourceResolver解析程序，字符串路径，字符串资源类型） |
| 配置getStorageCloudServiceConfig（资源资源） |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| boolean mayAccessUGC(ResourceResolver) |

