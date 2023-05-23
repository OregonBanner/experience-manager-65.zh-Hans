---
title: 錯誤記錄中有關已棄用API的錯誤訊息
description: 錯誤記錄中有關已棄用API的錯誤訊息
source-git-commit: b05666883645ca11784292e4bfb5bf9c1e35a43b
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---


# 錯誤記錄中有關已棄用API的錯誤訊息 {#error-messages-about-deprecated-apis-in-error-logs}

此問題適用於下列版本：

* Experience Manager6.5 Forms

## 问题 {#issue}

* error.log檔案中出現下列錯誤訊息：
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)

## 解决方法 {#workaround}

1. 安裝 [Experience Manager Forms Service Pack 13或更新版本（6.5.13.0或更新版本）](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
1. 使用以下連結，從Software Distribution下載套件（解析度為.jar檔案）：

   https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]pack/com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar

1. 開啟Experience Manager設定管理員並安裝下載的com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar檔案。

問題已解決。