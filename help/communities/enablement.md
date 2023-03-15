---
title: 配置启用功能
seo-title: Configuring Enablement Features
description: 在社区中配置启用功能
seo-description: Configure enablement features in Communities
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
role: Admin
exl-id: b635e2ed-4637-4b2f-a746-ec8dc7541bab
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 1%

---

# 配置启用功能 {#configuring-enablement-features}

## 概述 {#overview}

启用功能提供创建 [启用社区](overview.md#enablement-community).

* 此功能需要额外的许可才能在生产环境中使用。

使用支持功能需要满足以下条件：

安装：

* **SCORM**

   可共享内容对象参考模型(SCORM)是电子学习标准和规范的集合。 SCORM还定义如何将内容打包到可传输的ZIP文件中。

* **MySQL**

   MySQL是一个关系数据库，主要用于SCORM跟踪和报告用于启用的数据，以及用于跟踪视频进度的表。 SCORM for enablement功能包需要MySQL JDBC驱动程序。

* **FFmpeg**

   FFmpeg是一种用于转换和流式传输音频和视频的解决方案，在安装后用于正确的转码 [视频资产](../../help/sites-authoring/default-components-foundation.md#video). 对于启用社区，它用在创作环境中，为上传的资源获取元数据，并生成缩略图以在列出资源时显示。

设置：

* **社区管理员**

   对于启用社区，仅 `Community Enablement Managers` 可以为用户组分配角色 `Community Site Enablement Manager`，其权限可能包括发布环境中的内容创建、分配和成员管理。

可选配置：

* **Adobe Analytics**

   与Adobe Analytics的集成添加了全面的报表功能，并支持将视频心率添加到Analytics。

* **Dispatcher**

## 配置步骤 {#configuration-steps}

以下是启用社区所需的步骤。

每个步骤都链接到提供必要详细信息的文档。

**在所有创作/发布实例上：**

1. **[安装适用于MySQL的JDBC驱动程序](deploy-communities.md#jdbc-driver-for-mysql)**

   使用Web控制台（包）： *http://localhost:4502/system/console/bundles*

   安装 *早于* 安装SCORM包

1. **[安装SCORM包](deploy-communities.md#scorm-package)**


   使用包管理器： *http://localhost:4502/crx/packmgr/*

**在任何服务器上：**

1. **[安装MySQL、MySQL Workbench](mysql.md)**

1. **[安装MySQL数据库](mysql.md#database-setup)**

   执行从创作实例下载的SQL脚本

   使用MySQL Workbench

**在托管创作实例的同一服务器上：**

1. **[安装FFmpeg](ffmpeg.md)**

**在所有创作/发布实例上：**

1. **[配置JDBC连接池](mysql.md#configure-jdbc-connections)**

   使用Web控制台(configMgr)： *http://localhost:4502/system/console/configMgr*

1. **[配置SCORM引擎服务](mysql.md#aem-communities-scormengine-service)**

   使用Web控制台(configMgr)： *http://localhost:4502/system/console/configMgr*

1. **[配置CSRF筛选器](mysql.md#adobe-granite-csrf-filter)**

   使用Web控制台(configMgr)： *http://localhost:4502/system/console/configMgr*

**在创作实例上：**

1. (*可选*) **[配置Analytics服务](analytics.md)**

   使用“工具”、“部署”、“Cloud Services”控制台： *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[配置FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   使用工作流/模型控制台

1. **[启用通道服务](deploy-communities.md#tunnel-service-on-author)**

   使用Web控制台(configMgr)： *http://localhost:4502/system/console/configMgr*

1. **[创建社区管理员](users.md#creating-community-members)**

   对于创作环境，请使用经典UI安全控制台： *http://localhost:4502/useradmin*

   创建用户，路径为= /home/users/community

   * 将成员添加到以下组：

      * 社区启用管理员
      * Communities管理员

## Dispatcher {#dispatcher}

当部署包括 [AEM调度程序](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)，为了使支持功能正常工作， `clientheader` 和 `filter` 部分内容需要修改。 参见 [为社区配置Dispatcher](dispatcher.md#enablement).
