---
title: 管理用户和用户组
seo-title: 管理用户和用户组
description: AEM Communities用户可以自行注册和编辑用户档案
seo-description: AEM Communities用户可以自行注册和编辑用户档案
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 0%

---


# 管理用户和用户组{#managing-users-and-user-groups}

## 概述 {#overview}

在AEM Communities，在发布环境中，用户可以自行注册并编辑其用户档案。 如果具有相应的权限，则还可以：

* 在社区站点中创建子社区（请参阅[社区组](creating-groups.md)）。

* [版](moderation.md) 本用户生成的内容(UGC)。

* 成为[启用资源](resources.md)联系人。

* 具有[特权](#privileged-members-group)可创建博客、日历、QnA和论坛的条目。

在发布环境中注册的用户通常称为&#x200B;*社区成员（成员）*，以在创作环境中区分他们与&#x200B;*用户*。

通过将成员分配给在从创作环境创建[或[修改](sites-console.md#modifying-site-properties)社区站点时动态创建的[成员（用户）组](#publish-group-roles)中的一个，授予权限。 ](sites-console.md)当从作者环境工作时，通过[隧道服务](#tunnel-service)从发布环境查看成员。

根据设计，在发布环境中创建的成员和成员组不应显示在作者环境中。 在创作环境中创建的用户和用户组也同样希望保留在创作环境中。

当创作用户和发布成员来自相同的用户列表（如从同一LDAP目录同步）时，在创作和发布环境中，他们不被视为具有相同权限和组成员关系的同一用户。 成员和用户的角色必须根据需要分别在发布和创作时设置。

对于[发布场](topologies.md)，在一个发布实例上进行的注册和修改需要与其它发布实例同步，以便它们能够访问同一用户数据。 有关详细信息，请参阅[用户同步](sync.md)，其中包括描述[当时发生的情况的部分……](sync.md#what-happens-when)。

### 贡献限制 {#contribution-limits}

为了防止垃圾邮件，可以限制成员发布内容的频率。 此外，可以自动限制新登记成员的捐款。

有关详细信息，请参阅[成员贡献限制](limits.md)。

### 动态创建的用户组{#dynamically-created-user-groups}

创建新社区站点时，将使用唯一的id(uid)和权限动态创建新用户组，这些权限适用于在创作环境（请参阅[作者组角色](#author-group-roles)）或发布环境（请参阅[发布组角色](#publish-group-roles)）中管理社区站点所需的各种管理功能。

在[社区站点创建](sites-console.md#step13asitetemplate)期间，根据给定站点的名称生成组的名称。 唯一id可避免同一服务器上名称相似的社区站点和社区组的命名冲突。

例如，如果标题为“We.Retail Engage”的站点的站点名称为“*engage*”，则创建的用户组之一是：

* 社区&#x200B;*参与*&#x200B;成员

## 创作环境 {#author-environment}

### 隧道服务{#tunnel-service}

使用作者环境创建站点](sites-console.md)、[修改站点属性](sites-console.md#modifying-site-properties)和[管理社区成员和成员组](members.md)时，必须访问在发布环境中注册的用户和用户组。[

隧道服务使用作者上的复制代理提供此访问。

* 有关详细信息，请参阅部署页上的[配置说明](deploy-communities.md#tunnel-service-on-author)。

[“社区成员”和“组”控制台](members.md)仅用于管理仅在发布环境中注册的用户（成员）和用户组（成员组）。

要管理在创作环境中注册的用户和用户组，请使用[安全控制台](../../help/sites-administering/security.md)

### 作者组角色{#author-group-roles}

| 如果组成员…… | 主角色 |
|---|---|
| 管理员 | 管理员组由系统管理员组成，这些管理员具有社区管理员的所有功能以及管理社区管理员组的能力。 |
| 社区管理员 | 社区管理员组自动成为所有社区站点以及在该站点上创建的任何社区组的成员。 社区管理员组的初始成员是管理员组。 在创作环境中，社区管理员可以创建社区站点、管理站点、管理成员（他们可以禁止社区成员）以及审核内容。 |
| 社区&lt;*站点名称*> Sitecontentmanager | 社区站点内容管理器能够执行传统的AEM创作、内容创建和修改社区站点的页面。 |
| 社区支持经理 | 社区Enablement Managers组由可分配用于管理社区站点的Enablement Managers组的用户组成。 |
| 社区&lt;*站点名称* > Siteenablementmanagers | 社区站点启用管理器组由已分配用于管理社区站点启用[资源](resources.md)的用户组成。 |
| 无 | 匿名网站访客不能访问作者环境。 |

### 系统管理员{#system-administrators}

管理员组的成员是系统管理员，他们能够为作者和发布环境执行AEM安装的初始设置。

出于演示和开发目的，管理员组的用户ID为&#x200B;*admin*，密码为&#x200B;*admin*。

对于生产环境，应修改默认管理员组。

请务必按照[安全清单](../../help/sites-administering/security-checklist.md)进行操作。

## 发布环境 {#publish-environment}

### 成为成员{#becoming-a-member}

在发布环境中，根据社区站点的[设置](sites-console.md#user-management)，站点访客可以成为社区成员：

* 当社区站点为私有（已关闭）时：
   * 按邀请
   * 按管理员的操作

* 当社区站点公开时（打开）:
   * 通过自助注册
   * 通过Facebook和Twitter进行社交登录

>[!NOTE]
>
>如果站点访客注册为一个开放社区站点的成员，则他们会自动成为同一发布环境下其他开放社区站点的成员。

### 发布组角色{#publish-group-roles}

| 如果组成员…… | 主角色 |
|---|---|
| 社区&lt;*站点名称*&#x200B;成员 | 社区站点成员是注册用户。 他们可以登录、修改用户档案、加入一个开放的社区组、向社区发布内容、向其他成员发送消息以及遵循站点活动。 |
| 社区&lt;*站点名称*>版主 | 社区站点审查方是可信的社区成员，可以批量审核发布内容的页面上的UGC，也可以使用审核控制台审核，也可以在上下文中审核内容。 |
| 社区&lt;*站点名称*> &lt;*组名称*&#x200B;成员 | 社区组成员是已加入开放社区组或已受邀加入封闭社区组的社区成员。 他们具有站点内该社区组的成员能力。 |
| 社区&lt;*站点名称*&#x200B;组管理员 | 社区站点组管理员是受信任的社区成员，被指定在社区站点中创建和管理子社区（组）。 包括提供上下文协调的功能。 |
| *特权成员安全组* | 为限制内容创建而手动创建和维护的用户组。 请参阅[特权成员组](#privileged-members-group)。 |
| 无 | 发现网站的匿名网站访客可能会视图和搜索允许匿名访问的社区网站。 要参与和发布内容，用户必须自行注册（如果允许）并成为社区成员。 |

### 将成员分配到发布组角色{#assigning-members-to-publish-group-roles}

当[在创作环境中创建社区站点](sites-console.md)或[修改站点属性时，](sites-console.md#modifying-site-properties)成员可以被分配到发布环境中执行的各种角色，如主持人、组管理员、资源联系人或特权成员。

[启用隧道服](sync.md#accessingpublishusersfromauthor) 务会导致分配选择从发布时的成员而不是作者的用户显示。

所选成员将自动分配给[相应的组](#publish-group-roles)，并且当社区站点被（重新）发布时，将包括其成员资格。

### 拥有权限的成员组 {#privileged-members-group}

特权成员安全组的目的是限制为特定社区功能创建内容的权限子集为社区站点的成员。

特权成员组是使用[社区组控制台](members.md)创建和管理的成员组。

创建特权成员组并启用[隧道服务](sync.md#accessingpublishusersfromauthor)后，可以[修改](sites-console.md#modify-structure)现有社区站点的结构，以将其社区功能的配置编辑为“允许特权成员”并添加所创建的组。

允许指定一个或多个特权成员组的社区功能包括：

* [博客功能](functions.md#blog-function) -限制创建新文章。
* [日历函数](functions.md#calendar-function) -限制创建新事件。
* [论坛功能](functions.md#forum-function) -限制创建新主题。
* [问题与答案](functions.md#qna-function) -限制创建新问题的创建。

当社区功能未得到保护（未分配特权成员组）时，将允许所有社区站点成员创建功能内容(文章、事件、主题、问题)。

>[!NOTE]
>
>将用户添加到社区站点的特权成员组将仅授予用户创建权限（如果用户也是同一社区站点的成员）。

## 创建社区成员{#creating-community-members}

### 存储库位置{#repository-location}

为了使某些功能正常工作，需要创建具有相应权限的用户和用户组。

在`/home/users/community`中创建成员时，它们将继承为成员的用户档案授予读取权限的正确ACL。

同样，应在`/home/groups/community`中创建自定义社区用户组（如特权成员组）。

使用[社区成员和组控制台](members.md)将在这些路径中创建用户和组。

要指定自定义路径，需要使用经典安全UI，可通过[https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin)访问。

要为自定义成员路径授予读取权限，请在所有发布实例上设置类似于`/home/users/community`的ACL:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="everyone"
  rep:privileges="{Name}[jcr:read]" >
  <rep:restrictions
    jcr:primaryType="rep:Restrictions"
    rep:glob="*/profile*" />
</allow>
```

要为自定义成员组路径（如/home/groups/mycompany）赋予适当的权限，请在所有发布实例上设置类似于`/home/groups/community`的ACL:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### 控制台 {#consoles}

只有在创作环境中提供四个单独的控制台：

| 控制台 | 工具、安全性、用户 | 工具、安全性、组 | 社区、成员 | 社区、组 |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 管理 | 创作用户 | 作者用户组 | 发布时的成员 | 发布时的成员组 |
| reader | 管理员权限 | 管理员权限 | 管理权限，隧道服务，用户同步发布场 | 管理权限，隧道服务，用户同步发布场 |

### 社区Enablement Manager角色{#community-enablement-manager-role}

通常，[启用社区](overview.md#enablement-community)不允许站点访客自行注册，因为每个成员都有相关费用。 在创作站点创建过程中，由分配了`enablement manager` [的[角色](#author-group-roles)的用户（添加为组`Community <site-name> Siteenablementmanagers`的成员）管理启动学习者和资源。 ](sites-console.md#enablement)`enablement manager`还负责将学习资源](resources.md)分配给创作社区成员。[

只有全局`Community Enablement Managers`组成员的用户才能被选择为特定社区站点的`enablement manager`。

要创建可以分配`Community Site Enablement Manager`角色的用户，请使用经典UI安全控制台来指定路径：

在作者实例上：

1. 以管理员权限登录，浏览至经典UI安全控制台。

   例如，[http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. 从“编辑”菜单中，选择&#x200B;**[!UICONTROL 创建用户]**。
3. 填写`Create User`对话框。
   * 路径必须为`/home/users/community`。
4. 选择&#x200B;**[!UICONTROL 创建]**。

   ![create-community-user](assets/create-community-user.png)

* 在左窗格中，搜索新创建的用户，然后选择以在右窗格中显示。

   ![社区用户](assets/view-community-user.png)

在左边窗格中：

1. 清除搜索框，然后选择&#x200B;**[!UICONTROL 隐藏用户]**。
2. 找到并将`community-enablementmanagers`拖动到右窗格中显示的新用户的&#x200B;**[!UICONTROL 组]**&#x200B;选项卡。

   ![分配组](assets/assign-group.png)

### 社区管理员角色{#community-administrators-role}

如[作者组角色](#author-group-roles)图表中所述，社区管理员组的成员可以创建社区站点、管理站点、管理成员（他们可以禁止社区成员）和审核内容。

按照创建用户并将其分配给[enablement manager](#communitysiteenablementmanagerrole)角色的相同步骤操作，但在用户的“组”选项卡下添加c `ommunity-administrators`组。

### LDAP集成{#ldap-integration}

AEM支持使用LDAP验证用户以及创建用户帐户。 这在[使用AEM 6](../../help/sites-administering/ldap-config.md)配置LDAP中有详细介绍。

以下是特定于社区成员和成员组的一些配置详细信息。

1. 为每个AEM发布实例配置LDAP。
2. [LDAP标识提供者](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 无特殊说明

3. [同步处理函数](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 设置以下属性：

      * **[!UICONTROL 用户自动成员资格]**:  `community-<site name>-<uid>-members`
      * **[!UICONTROL 用户路径前缀]**:  `/community`
      * **[!UICONTROL 组路径前缀]**:  `/community`

4. [外部登录模块](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 没有特别说明

这会导致用户自动被分配到社区站点的成员组，存储库位置为`/home/users/community`和`/home/groups/community`，这样，用户就继承了相应的权限，可以看到彼此的用户档案。

* `User auto membership`值应为`rep:authorizableId`属性，而不是用户档案的`givenName`（显示名称）。

## 在AEM实例之间同步用户{#synchronizing-users-among-aem-instances}

使用[发布场](topologies.md)时，通过将用户首先导入一个实例和使用户同步](sync.md)能够将用户分发到其他发布实例，确保用户在每个发布实例上具有相同的路径。[

如果导入用户组，要确保用户组在每个发布实例上具有相同的路径，请导入到一个实例，然后[创建要导出的包](../../help/sites-administering/package-manager.md#creating-a-new-package)，并将该包安装到所有其他发布实例上。

虽然用户组通过用户同步的同步将包括在将来的版本中，但当用户同步运行时，当前仅用户组的&#x200B;*成员*&#x200B;将同步。

## 关于社区组{#about-community-groups}

讨论组时，有两个不同的主题：

* **[社区组](overview.md#communitygroups)**

   社区组是在社区站点的发布环境中可以创建的子社区，支持社区组的创建。 创建社区组会生成更多添加到网站的页面，并以类似于其父社区站点的方式进行管理。 有关详细信息，请访问[开发人员的社区组基本工具](essentials-groups.md)和作者的[社区组](creating-groups.md)。

* **[成员组](../../help/sites-administering/security.md)**

   成员组是成员可能属于的组，并通过“组”控制台进行管理。 本页讨论的大部分内容都集中在成员组。 为社区站点自动创建的成员组（前缀为&#x200B;*`Community`*）可称为社区组，因此必须考虑讨论的上下文。
