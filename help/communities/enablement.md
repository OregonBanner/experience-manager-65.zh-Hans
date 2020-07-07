---
title: 配置Enablement Features
seo-title: 配置Enablement Features
description: 在社区中配置启用功能
seo-description: 在社区中配置启用功能
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
translation-type: tm+mt
source-git-commit: ce21755263a2e8a3f0e97acb7f586e32cedde83a
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---


# 配置Enablement Features {#configuring-enablement-features}

## 概述 {#overview}

支持功能提供了创建支持社 [区的能力](overview.md#enablement-community)。

* 此功能需要额外的许可才能用于生产环境。

使用支持功能需要：

安装：

* **SCORM**

   可共享内容对象参考模型(SCORM)是电子教学标准和规范的集合。 SCORM还定义如何将内容打包到可转让的ZIP文件中。

* **MySQL**

   MySQL是关系报告库，主要用于SCORM跟踪和Enablement数据，以及用于跟踪视频进度的表。 SCORM for enablement功能包需要MySQL JDBC驱动程序。

* **FFmpeg**

   FFmpeg是用于转换音频和视频并实现流化的解决方案，安装后用于对视频资产进行正确 [的转码](../../help/sites-authoring/default-components-foundation.md#video)。 对于Enablement Communities，它在创作环境中用于获取已上传资源的元数据，并在列出资源时生成要显示的缩略图。

设置：

* **社区管理员**

   对于启用社区，只能为用户组 `Community Enablement Managers` 的成员分配角色，其权限可 `Community Site Enablement Manager`能包括发布环境中的内容创建、分配和成员管理。

可选配置：

* **AdobeAnalytics**

   与AdobeAnalytics的集成增加了全面的报告功能，并支持Analytics的视频心跳。

* **Dispatcher**

## 配置步骤 {#configuration-steps}

以下是支持社区所需的步骤。

每个步骤都链接到提供必要详细信息的文档。

**在所有作者／发布实例上：**

1. **[为MySQL安装JDBC驱动程序](deploy-communities.md#jdbc-driver-for-mysql)**

   使用Web控制台（捆绑包）: *http://localhost:4502/system/console/bundles*

   安装 *SCORM* 包前进行安装

1. **[安装SCORM包](deploy-communities.md#scorm-package)**


   使用包管理器： *http://localhost:4502/crx/packmgr/*

**在任何服务器上：**

1. **[安装MySQL、MySQL Workbench](mysql.md)**

1. **[安装MySQL数据库](mysql.md#database-setup)**

   执行从创作实例下载的SQL脚本

   使用MySQL Workbench

**在承载作者实例的同一服务器上：**

1. **[安装FFmpeg](ffmpeg.md)**

**在所有作者／发布实例上：**

1. **[配置JDBC连接池](mysql.md#configure-jdbc-connections)**

   使用Web控制台(configMgr): *http://localhost:4502/system/console/configMgr*

1. **[配置SCORM引擎服务](mysql.md#aem-communities-scormengine-service)**

   使用Web控制台(configMgr): *http://localhost:4502/system/console/configMgr*

1. **[配置CSRF过滤器](mysql.md#adobe-granite-csrf-filter)**

   使用Web控制台(configMgr): *http://localhost:4502/system/console/configMgr*

**在创作实例上：**

1. (可&#x200B;*选*)配 **[置Analytics服务](analytics.md)**

   使用工具、部署、Cloud Service控制台： *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[配置FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   使用工作流／模型控制台

1. **[启用隧道服务](deploy-communities.md#tunnel-service-on-author)**

   使用Web控制台(configMgr): *http://localhost:4502/system/console/configMgr*

1. **[创建社区管理员](users.md#creating-community-members)**

   对于作者环境，请使用经典UI安全控制台： *http://localhost:4502/useradmin*

   创建路径= /home/users/community的用户

   * 将成员添加到以下组：

      * 社区支持经理
      * 社区管理员

## Dispatcher {#dispatcher}

当部署包 [括AEM的Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)，为了使启用功能正常工作， `clientheader` 需要修改 `filter` 这些部分。 请参 [阅为社区配置Dispatcher](dispatcher.md#enablement)。
