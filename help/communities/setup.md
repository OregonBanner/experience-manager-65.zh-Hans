---
title: 初始设置
seo-title: Initial Setup
description: 设置社区
seo-description: Setting up Communities
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 2%

---

# 初始设置 {#initial-setup}

## 开始创作和发布实例 {#start-author-and-publish-instances}

出于开发和演示目的，需要运行一个作者和一个发布实例。

为此，请遵循基本的AEM [快速入门](../../help/sites-deploying/deploy.md#getting-started) 说明，这将导致：

* 上的创作环境 [localhost:4502](http://localhost:4502/)
* 发布环境 [localhost:4503](http://localhost:4503/)

对于AEM Communities,

* 创作环境适用于：

   * 开发网站、模板和组件。
   * 管理和配置任务。

* 发布环境适用于：

   * 发布和审核内容的社区体验。
   * 创建社区组、成员和成员组。

>[!NOTE]
>
>如果不熟悉AEM，请查看 [基本操作](../../help/sites-authoring/basic-handling.md) 和 [页面创作快速指南](../../help/sites-authoring/qg-page-authoring.md).

## 安装最新的Communities版本 {#install-latest-communities-release}

本教程将创建 [参与社区网站](overview.md#engagement-community) 和基于AEM Communities 6.2功能包版本1.10。

要确保安装了最新功能包，请访问：

* [最新版本](deploy-communities.md#latest-releases)

对于创建 [启用社区网站](overview.md#enablement-community)，访问 [AEM Communities启用入门](getting-started-enablement.md).

## 配置 Analytics {#configure-analytics}

When [Adobe Analytics已为社区站点配置](analytics.md)，提供有关社区活动的信息，可增强社区成员的体验并向网站管理员提供反馈。

与Adobe Analytics集成是可选的。

## 为通知配置电子邮件 {#configure-email-for-notifications}

通知功能，默认情况下，该功能可用于使用 `Communities Sites` 控制台中为通知提供了电子邮件渠道。

需要为网站正确配置电子邮件。

请参阅 [配置电子邮件](email.md).

## 启用隧道服务 {#enable-the-tunnel-service}

在创作环境中创建社区站点时，隧道服务允许将角色分配给在发布环境中注册的受信任社区成员。 隧道服务还允许从 [“成员”和“组”控制台](members.md) 在创作环境中。

公约适用于在发布环境中创建的成员和成员组，这些成员组将 *not* 在创作环境中重新创建。 有关详细信息，请参阅 [管理用户和用户组](users.md).

有关在 **作者** 实例，请参阅 [隧道服务](deploy-communities.md#tunnel-service-on-author).

## 社区管理员角色 {#community-administrator-role}

社区管理员组的成员能够创建社区站点、管理站点、管理成员（他们可以禁止社区成员）以及审核内容。

### 创建用户 {#create-user}

在上创建用户 *作者*，分配了社区管理员角色的用户：

* 在创作实例上

   * 例如， [http://localhost:4502/](http://localhost:4503/)

* 使用管理员权限登录

   * 例如，用户名“admin”/密码“admin”

* 从主控制台中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 安全性]** > **[!UICONTROL 用户]**.
* 从 **编辑** 菜单，选择 **[!UICONTROL 添加用户]**

* 在 `Create New User` 对话框输入：

   * **[!UICONTROL ID]**:天狼星
   * **[!UICONTROL 电子邮件地址]**:sirius.nilson@mailinator.com
   * **[!UICONTROL 密码]**:密码
   * **[!UICONTROL 确认密码(&amp;A);]**:密码
   * **[!UICONTROL 名字]**:天狼星
   * **[!UICONTROL 姓氏]**:尼尔森

### 将Sirius分配给社区管理员组 {#assign-sirius-to-community-administrators-group}

向下滚动到 `Add User to Groups`:

* 输入“C”进行搜索

   * 选择 `Community Administrators`
   * 选择 `Community Enablement Managers`

* 选择&#x200B;**[!UICONTROL 保存]**。

![create-user](assets/create-user.png)

## 启用社交登录 {#enable-social-login}

在使用Facebook和Twitter的社交登录演示版本之前，必须

1. 安装修复包或 [最新功能包](deploy-communities.md#latestfeaturepack) (2017年3月Facebook API更改)。
1. [启用OAuth提供程序](social-login.md#adobe-granite-oauth-authentication-handler) 中。

对于生产服务器，需要创建提供社交登录所需的云服务。

请参阅 [使用Facebook和Twitter进行社交登录](social-login.md).

## 创建教程标记 {#create-tutorial-tags}

使用标记命名空间创建要用于参与和支持教程的标记 `Tutorial`.

使用 [标记控制台](../../help/sites-administering/tags.md#tagging-console) 要创建以下标记，请执行以下操作：

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

然后，按照以下说明操作：

1. [设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [发布标记](../../help/sites-administering/tags.md#publishing-tags).

为AEM Communities快速入门Tutorials创建的标记包示例

[获取文件](assets/tutorial_tags-v63.zip)

## 用于UGC公共存储的MongoDB {#mongodb-for-ugc-common-store}

建议设置，但是可选 [MSRP](msrp.md) (MongoDB)作为 [公用商店](working-with-srp.md) 以体验从发布和/或创作环境审核所有UGC的灵活性。

有关说明，请访问 [如何为演示设置MongoDB](demo-mongo.md).

默认情况下，安装创作和发布AEM实例会导致将用户生成的内容(UGC)存储在 [JCR Tar存储](../../help/sites-deploying/platform.md) 使用 [JSRP](jsrp.md). JSRP不是常用存储，这意味着UGC仅在输入JSRP的实例上可见。 通常，UGC是在发布实例上输入的，在创作环境中不可见，从而导致所有审核任务都需要使用发布实例。
