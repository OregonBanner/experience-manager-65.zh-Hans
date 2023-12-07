---
title: SocialUtils重构
description: AEM 6.1中弃用了包com.adobe.cq.social.ugcbase.SocialUtils
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---

# SocialUtils重构 {#socialutils-refactoring}

## 已弃用SocialUtils包 {#socialutils-package-deprecated}

包 `com.adobe.cq.social.ugcbase.SocialUtils` 在AEM 6.1中已弃用。

下表列出了取代的方法 `SocialUtils` 方法。

## SocialResourceUtilities包  {#socialresourceutilities-package}

| com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities中的方法 |
|---|
| 布尔型checkPermission(ResourceResolver resolver， String path， String action) |  |
| SocialResourceProvider getSocialResourceProvider(Resource) |  |
| SocialResourceConfiguration getStorageConfig(Resource) |  |
| 资源getUGCResource(Resource userResource) |  |
| 资源getUGCResource(Resource userResource， ResourceResolverFactory rrf) | 新建 |
| 资源getUGCResource(Resource userResource， ResourceResolverFactory rrf， String resourceTypeHint) | 新建 |
| 资源getUGCResource(Resource userResource， String resourceTypeHint) |  |
| boolean hasModeratePermissions(Resource) |  |
| String resourceToACLPath(Resource) |  |
| String resourceToUGCStoragePath(Resource) | 替换String resourceToUGCPath(Resource) |
| 字符串UGCToResourcePath(Resource) |  |
| 字符串UGCToResourcePath（字符串ugcPath） | 方法签名已更改 |
| 字符串UGCToResourcePath（字符串ugcPath， ResourceResolver resolver） | 新建 |

| 中的方法 `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider(Resource) | 替换SocialResourceProvider getConfiguredProvider(Resource) |

## SCFUtilities包 {#scfutilities-package}

| 中的方法 `com.adobe.cq.social.`utilities.scf.api.SCFUtitles |
|---|
| 字符串getAvatar(UserProperties userProperties) |
| 字符串getAvatar(UserProperties userProperties， int size) |
| 字符串getAvatar(UserProperties userProperties， String absoluteDefaultAvatar) |
| 字符串getAvatar(UserProperties userProperties， String absoluteDefaultAvatar， SocialUtils.AVATAR_SIZE) |
| 页面getContainingPage(Resource) |
| 字符串getSocialProfileURL（字符串用户名，ResourceResolver解析程序，页面） |
| UserProperties getUserProperties(ResourceResolver resolver， String userId) |

## 仅供内部使用 {#for-internal-use-only}

| 布尔值canAddNode（会话会话，字符串路径） |
|---|
| 字符串createUniqueNameHint（字符串消息） |
| 字符串createUniqueNameHint(String message， int numRandomChars) |
| 字符串generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(String path， ResourceResolver resolver) |
| 字符串getPagePath(Resource) |
| 字符串getPagePath（字符串路径） |
| 字符串getResourceTypeForIncludedResource（资源组件，字符串defaultResourceType，字符串designPropertyName） |
| 字符串getResourceTypeFromDesign(Resource， String styleProperty， String defaultValue) |
| boolean isResourceOwner(Resource resource) |
| 字符串mapUGCPath(Resource) |
| 字符串mapUGCPath(String ugcPath， ResourceResolver resolver) |
| 布尔mayPost(ResourceResolver resolver， Resource) |
| String prepareUserGeneratedContent(ResourceResolver resolver， String path) |

## 方法不再可用 {#methods-no-longer-available}

| 节点createNode(ResourceResolver resolver， String path， String nodeType) |
|---|
| 资源getResourceAtPath(ResourceResolver resolver， String path) |
| 资源getResourceAtPath（ResourceResolver解析器，字符串路径，字符串资源类型） |
| 配置getStorageCloudServiceConfig（资源） |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| 布尔值mayAccessUGC(ResourceResolver resolver) |
