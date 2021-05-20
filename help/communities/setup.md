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
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 2%

---

# 初始设置{#initial-setup}

## 启动创作实例和发布实例{#start-author-and-publish-instances}

出于开发和演示目的，需要运行一个作者和一个发布实例。

为此，请按照基本的AEM [快速入门](../../help/sites-deploying/deploy.md#getting-started)说明操作，这将导致：

* [localhost:4502](http://localhost:4502/)上的创作环境
* 在[localhost:4503](http://localhost:4503/)上发布环境

对于AEM Communities,

* 创作环境适用于：

   * 开发网站、模板和组件。
   * 管理和配置任务。

* 发布环境适用于：

   * 发布和审核内容的社区体验。
   * 创建社区组、成员和成员组。

>[!NOTE]
>
>如果不熟悉AEM，请查看有关[基本操作](../../help/sites-authoring/basic-handling.md)和[页面创作快速指南的文档](../../help/sites-authoring/qg-page-authoring.md)。

## 安装最新的Communities版本{#install-latest-communities-release}

本教程将创建一个[参与社区站点](overview.md#engagement-community)，且基于AEM Communities 6.2功能包版本1.10。

要确保安装了最新功能包，请访问：

* [最新版本](deploy-communities.md#latest-releases)

有关创建[启用社区站点](overview.md#enablement-community)的教程，请访问[启用AEM Communities快速入门](getting-started-enablement.md)。

## 配置 Analytics {#configure-analytics}

为社区站点](analytics.md)配置[Adobe Analytics后，将提供有关社区活动的信息，该信息可增强社区成员的体验，并向站点管理员提供反馈。

与Adobe Analytics集成是可选的。

## 为通知配置电子邮件{#configure-email-for-notifications}

默认情况下，通知功能可用于使用`Communities Sites`控制台创建的所有站点，它为通知提供电子邮件渠道。

需要为网站正确配置电子邮件。

请参阅[配置Email](email.md)。

## 启用隧道服务{#enable-the-tunnel-service}

在创作环境中创建社区站点时，隧道服务允许将角色分配给在发布环境中注册的受信任社区成员。 隧道服务还允许从创作环境的[成员和组控制台](members.md)访问社区成员。

约定适用于在发布环境中创建到&#x200B;*not*&#x200B;的成员和成员组在创作环境中重新创建。 有关更多信息，请参阅[管理用户和用户组](users.md)。

有关在&#x200B;**author**&#x200B;实例上启用隧道服务的简单说明，请参阅[隧道服务](deploy-communities.md#tunnel-service-on-author)。

## 社区管理员角色{#community-administrator-role}

社区管理员组的成员能够创建社区站点、管理站点、管理成员（他们可以禁止社区成员）以及审核内容。

### 创建用户 {#create-user}

在&#x200B;*author*&#x200B;上创建一个用户，该用户被分配了社区管理员的角色：

* 在创作实例上

   * 例如， [http://localhost:4502/](http://localhost:4503/)

* 使用管理员权限登录

   * 例如，用户名“admin”/密码“admin”

* 在主控制台中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 安全]** > **[!UICONTROL 用户]**。
* 从&#x200B;**编辑**&#x200B;菜单中，选择&#x200B;**[!UICONTROL 添加用户]**

* 在`Create New User`对话框中，输入：

   * **[!UICONTROL ID]**:天狼星
   * **[!UICONTROL 电子邮件地址]**:sirius.nilson@mailinator.com
   * **[!UICONTROL 密码]**:密码
   * **[!UICONTROL 确认密码(&amp;A);]**:密码
   * **[!UICONTROL 名字]**:天狼星
   * **[!UICONTROL 姓氏]**:尼尔森

### 将Sirius分配给社区管理员组{#assign-sirius-to-community-administrators-group}

向下滚动到`Add User to Groups`:

* 输入“C”进行搜索

   * 选择 `Community Administrators`
   * 选择 `Community Enablement Managers`

* 选择&#x200B;**[!UICONTROL 保存]**。

![create-user](assets/create-user.png)

## 启用社交登录{#enable-social-login}

在使用Facebook和Twitter的社交登录演示版本之前，必须

1. 安装修补程序包或[最新功能包](deploy-communities.md#latestfeaturepack)(用于2017年3月对Facebook API所做的更改)。
1. [在发布环境](social-login.md#adobe-granite-oauth-authentication-handler) 中启用OAuth提供程序。

对于生产服务器，需要创建提供社交登录所需的云服务。

请参阅[使用Facebook和Twitter进行社交登录](social-login.md)。

## 创建教程标记{#create-tutorial-tags}

使用`Tutorial`的标记命名空间创建要用于参与和支持教程的标记。

使用[Tagging console](../../help/sites-administering/tags.md#tagging-console)创建以下标记：

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

然后，按照以下说明操作：

1. [设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)。
1. [发布标记](../../help/sites-administering/tags.md#publishing-tags)。

为AEM Communities快速入门Tutorials创建的标记包示例

[获取文件](assets/tutorial_tags-v63.zip)

## 用于UGC常用存储的MongoDB {#mongodb-for-ugc-common-store}

建议将[MSRP](msrp.md)(MongoDB)设置为[公共存储](working-with-srp.md)，以体验从发布和/或创作环境审核所有UGC的灵活性。

有关说明，请访问[如何为Demo](demo-mongo.md)设置MongoDB。

默认情况下，安装创作和发布AEM实例会导致用户生成的内容(UGC)存储在[JCR Tar存储](../../help/sites-deploying/platform.md)中，该存储使用[JSRP](jsrp.md)进行访问。 JSRP不是常用存储，这意味着UGC仅在输入JSRP的实例上可见。 通常，UGC是在发布实例上输入的，在创作环境中不可见，从而导致所有审核任务都需要使用发布实例。
