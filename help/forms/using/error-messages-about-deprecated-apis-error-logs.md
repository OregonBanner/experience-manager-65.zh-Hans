---
title: 有关错误日志中已弃用API的错误消息
description: 有关错误日志中已弃用API的错误消息
source-git-commit: b05666883645ca11784292e4bfb5bf9c1e35a43b
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---


# 有关错误日志中已弃用API的错误消息 {#error-messages-about-deprecated-apis-in-error-logs}

此问题适用于以下版本：

* Experience Manager6.5Forms

## 带有 OS 剪贴板 {#issue}

* error.log文件中显示以下错误消息：
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)

## 解决方法 {#workaround}

1. 安装 [Experience Manager Forms Service Pack 13或更高版本(6.5.13.0或更高版本)](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
1. 使用以下链接从Software Distribution下载包（具有分辨率的.jar文件）：

   https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]pack/com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar

1. 打开Experience Manager配置管理器并安装下载的com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar文件。

问题已解决。