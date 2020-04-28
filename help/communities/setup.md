---
title: 初始设置
seo-title: 初始设置
description: 设置社区
seo-description: 设置社区
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
translation-type: tm+mt
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

---


# 初始设置 {#initial-setup}

## 开始作者实例和发布实例 {#start-author-and-publish-instances}

为了进行开发和演示，需要运行一个作者和一个发布实例。

为此，请按照基本的AEM [快速入门说明](../../help/sites-deploying/deploy.md#getting-started) ，这将导致：

* Localhost上的作 [者环境:4502](http://localhost:4502/)
* Publish环境 [在localhost:4503](http://localhost:4503/)

对于AEM Communities,

* 作者环境适用于：

   * 开发站点、模板和组件。
   * 管理和配置任务。

* 发布环境适用于：

   * 发布和审核内容的社区体验。
   * 创建社区组、成员和成员组。

>[!NOTE]
>
>如果不熟悉AEM，请视图有关基本操作 [的文档](../../help/sites-authoring/basic-handling.md) ，以 [及页面创作快速指南](../../help/sites-authoring/qg-page-authoring.md)。


## 安装最新的Communities版本 {#install-latest-communities-release}

本教程创建了 [一个参与社区站点](overview.md#engagement-community) ，并基于AEM Communities 6.2功能包版本1.10。

要确保安装了最新的功能包，请访问：

* [最新版本](deploy-communities.md#latest-releases)

有关创建Enablement Communities站点 [的教程](overview.md#enablement-community)，请访 [问Enablement的AEM Communities快速入门](getting-started-enablement.md)。

## 配置 Analytics {#configure-analytics}

为社区站点配置 [Adobe Analytics后](analytics.md)，会提供社区活动信息，以增强社区成员的体验并向站点管理员提供反馈。

与Adobe Analytics集成是可选的。

## 为通知配置电子邮件 {#configure-email-for-notifications}

默认情况下，通知功能可用于使用控制台创建的所 `Communities Sites` 有站点，它为通知提供电子邮件渠道。

必须为站点正确配置电子邮件。

See [Configuring Email](email.md).

## 启用隧道服务 {#enable-the-tunnel-service}

在创作环境中创建社区站点时，通道服务允许向发布环境中注册的受信任社区成员分配角色。 隧道服务还允许从创作环境的“成员”和“ [组”控制台访问社区成员](members.md) 。

该约定适用于在发布环境中创建的成员和成员组，以 *便不* 在创作环境中重新创建。 For more information see [Managing Users and User Groups](users.md).

有关在作者实例上启用隧道服务的简 **单说明** ，请参阅 [隧道服务](deploy-communities.md#tunnel-service-on-author)。

## 社区管理员角色 {#community-administrator-role}

社区管理员组的成员可以创建社区站点、管理站点、管理成员（他们可以禁止社区成员）和审核内容。

### 创建用户 {#create-user}

创建作者用 *户*，该用户被分配有“社区管理员”角色：

* 在创作实例上

   * 例如， [http://localhost:4502/](http://localhost:4503/)

* 使用管理员权限登录

   * 例如，用户名“admin”/密码“admin”

* 在主控制台中，导航到工 **[!UICONTROL 具]** >操 **[!UICONTROL 作]** > **[!UICONTROL Security]** > **** Users。
* 从“编辑 **”菜单&#x200B;**，选择“添**[!UICONTROL 加用户”]**

* 在对话 `Create New User` 框中输入：

   * **[!UICONTROL ID]**:天狼星
   * **[!UICONTROL 电子邮件地址]**:sirius.nilson@mailinator.com
   * **[!UICONTROL 密码]**:口令
   * **[!UICONTROL 确认密码&amp;ast;]**:口令
   * **[!UICONTROL 名字]**:天狼星
   * **[!UICONTROL 姓氏]**:尼尔森

### 将Sirius分配给社区管理员组 {#assign-sirius-to-community-administrators-group}

向下滚动到 `Add User to Groups`:

* 输入“C”以搜索

   * 选择 `Community Administrators`
   * 选择 `Community Enablement Managers`

* 选择&#x200B;**[!UICONTROL 保存]**。

![chlimage_1-301](assets/chlimage_1-301.png)

## 启用社交登录 {#enable-social-login}

在可能使用Facebook和Twitter的社交登录演示版之前，必须

1. 安装修复包或最 [新功能包](deploy-communities.md#latestfeaturepack) （2017年3月Facebook API更改）。
1. [在发布环境中启用OAuth提供程序](social-login.md#adobe-granite-oauth-authentication-handler) 。

对于生产服务器，必须创建提供社交登录所必需的云服务。

请参 [阅使用Facebook和Twitter进行社交登录](social-login.md)。

## 创建教程标记 {#create-tutorial-tags}

使用的标记命名空间创建用于参与和支持教程的标记 `Tutorial`。

使用“标 [记”控制台](../../help/sites-administering/tags.md#tagging-console) ，可创建以下标记：

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![chlimage_1-302](assets/chlimage_1-302.png)

然后，按照说明操作：

1. [设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)。
1. [发布标记](../../help/sites-administering/tags.md#publishing-tags)。

为AEM Communities快速入门教程创建的标记包示例

[获取文件](assets/tutorial_tags-v63.zip)

## 用于UGC公用商店的MongoDB {#mongodb-for-ugc-common-store}

建议将 [MSRP](msrp.md) (MongoDB)设置为公用商店( [](working-with-srp.md) MongoDB)，以体验从发布和／或作者环境调节所有UGC的灵活性。

有关说明，请 [访问How to Setup MongoDB for Demo](demo-mongo.md)。

默认情况下，安装作者和发布AEM实例会导致用户生成的内容(UGC)存储在 [JCR Tar存储中](../../help/sites-deploying/platform.md) ，该使用 [JSRP访问](jsrp.md)。 JSRP不是通用商店，这意味着UGC仅在输入它的实例上可见。 通常，UGC是在发布实例上输入的，并且在创作环境中不可见，这会导致所有审核任务都需要使用发布实例。