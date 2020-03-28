---
title: 配置启用功能
seo-title: 配置启用功能
description: 在社区中配置启用功能
seo-description: 在社区中配置启用功能
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# 配置启用功能 {#configuring-enablement-features}

## 概述 {#overview}

支持功能提供了创建支持社区 [的功能](overview.md#enablement-community)。

* 此功能需要额外的许可才能用于生产环境。

使用支持功能需要：

安装：

* **SCORM**

   可共享内容对象参考模型(SCORM)是电子教学的标准和规范的集合。 SCORM还定义如何将内容打包到可转让的ZIP文件中。

* **MySQL**

   MySQL是关系数据库，主要用于SCORM跟踪和报告数据（用于启用），以及用于跟踪视频进度的表。 SCORM for enablement功能包需要MySQL JDBC驱动程序。

* **FFmpeg**

   FFmpeg是用于转换和流式播放音频和视频的解决方案，安装后用于正确转码视 [频资产](../../help/sites-authoring/default-components-foundation.md#video)。 对于启用社区，它在创作环境中用于获取已上传资源的元数据，并生成在列出资源时显示的缩略图。

设置：

* **社区管理员**

   对于启用社区，只能向用户组的成 `Community Enablement Managers` 员分配其角色 `Community Site Enablement Manager`，其权限可能包括发布环境中的内容创建、分配和成员管理。

可选配置：

* **Adobe Analytics**

   与Adobe Analytics集成可添加全面的报告功能，并支持将视频心跳添加到Analytics中。

* **Dispatcher**

## 配置步骤 {#configuration-steps}

以下是启用社区所需的步骤。

每个步骤都链接到提供必要详细信息的文档。

**在所有作者／发布实例上：**

1. **[安装MySQL的JDBC驱动程序](deploy-communities.md#jdbc-driver-for-mysql)**

   使用Web控制台（捆绑包）:http://localhost:4502/system/console/bundles安 *装* SCORM包前 ** 安装

1. **[安装SCORM包](deploy-communities.md#scorm-package)**使用包管理器：*http://localhost:4502/crx/packmgr/*

**在任何服务器上：**

1. **[安装MySQL、MySQL Workbench](mysql.md)**

1. **[安装MySQL数据库](mysql.md#database-setup)**

   执行从作者实例下载的SQL脚本使用MySQL Workbench

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

   使用工具、部署、云服务控制台： *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[配置FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   使用工作流／模型控制台

1. **[启用隧道服务](deploy-communities.md#tunnel-service-on-author)**

   使用Web控制台(configMgr): *http://localhost:4502/system/console/configMgr*

1. **[创建社区管理员](users.md#creating-community-members)**

   对于创作环境，请使用经典UI安全控制台：http://localhost:4502/useradmin *创*&#x200B;建路径为= /home/users/community的用户

   * 将成员添加到以下用户组：

      * 社区支持经理
      * 社区管理员

## Dispatcher {#dispatcher}

当部署包括 [AEM的Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)，为了使启用功能正常工作，需要修改 `clientheader` 该部 `filter` 分和部分。 请参 [阅配置Dispatcher for Communities](dispatcher.md#enablement)。
