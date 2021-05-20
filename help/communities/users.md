---
title: 管理用户和用户组
seo-title: 管理用户和用户组
description: AEM Communities用户可以自行注册和编辑其用户档案
seo-description: AEM Communities用户可以自行注册和编辑其用户档案
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
role: Administrator
exl-id: 4237085a-d70d-41de-975d-153f58336daa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 0%

---

# 管理用户和用户组{#managing-users-and-user-groups}

## 概述 {#overview}

在AEM Communities的发布环境中，用户可以自行注册和编辑其配置文件。 如果具有适当的权限，他们还可以：

* 在社区站点中创建子社区（请参阅[社区组](creating-groups.md)）。

* [](moderation.md) 审核用户生成的内容(UGC)。

* 成为[启用资源](resources.md)联系人。

* 拥有[权限](#privileged-members-group)，可为博客、日历、QnA和论坛创建条目。

在发布环境中注册的用户通常称为&#x200B;*社区成员（成员）*，以便与创作环境中的&#x200B;*用户*&#x200B;区分开来。

权限的授予方式为：将成员分配给在从创作环境创建社区站点[](sites-console.md)或[已修改](sites-console.md#modifying-site-properties)时动态创建的[成员（用户）组之一。 ](#publish-group-roles)从创作环境工作时，成员可通过[tunnel service](#tunnel-service)从发布环境中可见。

根据设计，在发布环境中创建的成员和成员组不应显示在创作环境中。 在创作环境中创建的用户和用户组同样可以停留在创作环境中。

当创作用户和发布成员来自同一用户列表（如从同一LDAP目录同步）时，他们在创作和发布环境中不被视为具有相同权限和组成员资格的同一用户。 成员和用户的角色必须在发布和创作时酌情分开建立。

对于[发布场](topologies.md)，需要将一个发布实例上进行的注册和修改与其他发布实例同步，以便它们能够访问相同的用户数据。 有关详细信息，请参阅[User Synchronization](sync.md)，其中包含描述[What When...的部分](sync.md#what-happens-when)。

### 贡献限制 {#contribution-limits}

为了防止垃圾邮件，可以限制成员发布内容的频率。 此外，可自动限制新登记成员的缴款。

有关详细信息，请参阅[成员贡献限制](limits.md)。

### 动态创建的用户组{#dynamically-created-user-groups}

创建新社区站点后，会使用唯一的ID(uid)和相应于在创作环境（请参阅[创作组角色](#author-group-roles)）或发布环境（请参阅[发布组角色](#publish-group-roles)）中管理社区站点所需的各种管理功能动态创建新用户组。

群组的名称是在[社区站点创建](sites-console.md#step13asitetemplate)期间，根据给定站点的名称生成的。 唯一ID可避免同一服务器上名称相似的社区站点和社区组发生命名冲突。

例如，如果对于标题为“We.Retail Engage”的网站，网站名称为“*engage*”，则创建的用户组之一将为：

* 社区&#x200B;*参与*&#x200B;成员

## 创作环境 {#author-environment}

### 隧道服务{#tunnel-service}

使用创作环境创建[站点](sites-console.md)、[修改站点属性](sites-console.md#modifying-site-properties)和[管理社区成员和成员组](members.md)时，必须访问在发布环境中注册的用户和用户组。

隧道服务使用作者上的复制代理提供此访问。

* 有关详细信息，请参阅部署页面上的[配置说明](deploy-communities.md#tunnel-service-on-author) 。

[“社区成员”和“组”控制台](members.md)仅用于管理仅在发布环境中注册的用户（成员）和用户组（成员组）。

要管理在创作环境中注册的用户和用户组，请使用[安全控制台](../../help/sites-administering/security.md)

### 创作组角色{#author-group-roles}

| 如果组成员…… | 主要角色 |
|---|---|
| 管理员 | 管理员组由系统管理员组成，这些系统管理员具有社区管理员的所有能力以及管理社区管理员组的能力。 |
| 社区管理员 | 社区管理员组会自动成为所有社区站点以及网站上创建的任何社区组的成员。 社区管理员组的初始成员是管理员组。 在创作环境中，社区管理员能够创建社区站点、管理站点、管理成员（他们可以禁止社区成员）以及审核内容。 |
| 社区&lt;*站点名称*> Sitecontentmanager | 社区站点内容管理器能够执行传统的AEM创作、内容创建和修改社区站点的页面。 |
| 社区支持经理 | 社区支持管理器组由可供分配的用户组成，这些用户可以管理社区站点的支持管理器组。 |
| 社区&lt;*站点名称* > Siteenablementmanagers | 社区站点启用管理器组由分配给用户以管理社区站点的启用[资源](resources.md)的用户组成。 |
| 无 | 匿名网站访客可能无法访问创作环境。 |

### 系统管理员{#system-administrators}

管理员组的成员是系统管理员，他们能够为创作和发布环境执行AEM安装的初始设置。

出于演示和开发目的，管理员组的成员的用户ID为&#x200B;*admin* ，密码为&#x200B;*admin*。

对于生产环境，应修改默认的管理员组。

确保遵循[安全检查列表](../../help/sites-administering/security-checklist.md)。

## 发布环境 {#publish-environment}

### 成为{#becoming-a-member}成员

在发布环境中，根据社区站点的[设置](sites-console.md#user-management)，站点访客可能会成为社区成员：

* 当社区站点为私有（已关闭）时：
   * 通过邀请
   * 按管理员的操作

* 当社区站点为公共（打开）时：
   * 通过自行注册
   * 通过Facebook和Twitter进行社交登录

>[!NOTE]
>
>如果站点访客注册为一个开放社区站点的成员，则他们会自动成为同一发布环境中其他开放社区站点的成员。

### 发布组角色{#publish-group-roles}

| 如果组成员…… | 主要角色 |
|---|---|
| 社区&lt;*站点名称*>成员 | 社区站点成员是注册用户。 他们可以登录、修改其用户档案、加入开放的社区组、向社区发布内容、向其他成员发送消息，以及关注网站活动。 |
| 社区&lt;*站点名称*>审核者 | 社区站点审核者是受信任的社区成员，能够使用审核控制台或在发布内容的页面上的上下文中批量审核UGC。 |
| 社区&lt;*站点名称*> &lt;*组名称*>成员 | 社区组成员是已加入开放社区组或已受邀加入封闭社区组的社区成员。 他们具有站点内该社区组的成员能力。 |
| 社区&lt;*站点名称*>组管理员 | 社区站点组管理员是受信任的社区成员，被分配来创建和管理社区站点中的子社区（组）。 其中包括提供上下文审核的功能。 |
| *特权成员安全组* | 为限制内容创建而手动创建和维护的用户组。 请参阅[特权成员组](#privileged-members-group)。 |
| 无 | 发现网站的匿名网站访客可以查看和搜索允许匿名访问的社区网站。 要参与和发布内容，用户必须自行注册（如果允许）并成为社区成员。 |

### 为成员分配发布组角色{#assigning-members-to-publish-group-roles}

当[在创作环境中创建社区站点](sites-console.md)时，或者当[修改站点属性时，可以为](sites-console.md#modifying-site-properties)成员分配在发布环境中执行的各种角色，如审核者、组管理员、资源联系人或特权成员。

[启用隧道服](sync.md#accessingpublishusersfromauthor) 务会导致在发布时从成员而不是作者用户那里显示分配选项。

所选成员将被自动分配给[相应的组](#publish-group-roles)，并且在社区网站（重新）发布时将包含其成员关系。

### 拥有权限的成员组 {#privileged-members-group}

特权成员安全组的目的是将为某些社区功能创建内容限制为社区站点成员的特权子集。

特权成员组是使用[Communities Groups Console](members.md)创建和管理的成员组。

创建特权成员组并启用[隧道服务](sync.md#accessingpublishusersfromauthor)后，现有社区站点的结构可以是[modified](sites-console.md#modify-structure)，以编辑其社区功能的配置，使其“允许特权成员”并添加创建的组。

允许指定一个或多个特权成员组的社区功能包括：

* [博客功能](functions.md#blog-function)  — 限制新文章的创建。
* [日历函数](functions.md#calendar-function)  — 限制新事件的创建。
* [论坛功能](functions.md#forum-function)  — 限制新主题的创建。
* [问题解答函数](functions.md#qna-function)  — 限制创建新问题。

当社区功能未得到保护（未分配特权成员组）时，允许所有社区站点成员创建功能内容（文章、事件、主题、问题）。

>[!NOTE]
>
>将用户添加到社区站点的特权成员组时，仅当用户也是同一社区站点的成员时，才会授予他们创建权限。

## 创建社区成员{#creating-community-members}

### 存储库位置{#repository-location}

为了使某些功能正常工作，需要创建具有相应权限的用户和用户组。

在`/home/users/community`中创建成员后，这些成员将继承相应的ACL，为成员的配置文件授予读权限。

同样，应在`/home/groups/community`中创建自定义社区用户组（如特权成员组）。

使用[社区成员和组控制台](members.md)将在这些路径中创建用户和组。

要指定自定义路径，需要使用经典安全UI，该UI可在[https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin)访问。

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

要在所有发布实例上为自定义成员组路径（如/home/groups/mycompany）赋予适当的权限，请设置类似于`/home/groups/community`的ACL:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### 控制台 {#consoles}

只有在创作环境中，才有四个单独的控制台可用：

| 控制台 | 工具、安全性、用户 | 工具、安全性、组 | 社区、成员 | 社区、组 |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 管理 | 创作用户 | 创作时的用户组 | 发布时的成员 | 发布时的成员组 |
| reamires | 管理权限 | 管理权限 | 管理员权限、隧道服务、发布场的用户同步 | 管理员权限、隧道服务、发布场的用户同步 |

### 社区启用管理员角色{#community-enablement-manager-role}

网站访客自行注册的功能通常不允许[启用社区](overview.md#enablement-community)进行注册，因为每个成员都有相关成本。 在创作网站创建期间，为`enablement manager` [的[角色](#author-group-roles)分配了](sites-console.md#enablement) 的用户（添加为组`Community <site-name> Siteenablementmanagers`的成员）管理启用学习者和资源。 `enablement manager`还负责将学习资源](resources.md)分配给创作社区成员。[

只能为全局`Community Enablement Managers`组成员的用户选择特定社区站点的`enablement manager`。

要创建可能被分配`Community Site Enablement Manager`角色的用户，请使用经典UI安全控制台以指定路径：

在创作实例上：

1. 使用管理员权限登录，浏览到经典UI安全控制台。

   例如， [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. 从“编辑”菜单中，选择&#x200B;**[!UICONTROL 创建用户]**。
3. 填写`Create User`对话框。
   * 路径必须为`/home/users/community`。
4. 选择&#x200B;**[!UICONTROL 创建]**。

   ![create-community-user](assets/create-community-user.png)

* 在左窗格中，搜索新创建的用户，然后选择以在右窗格中显示。

   ![社区用户](assets/view-community-user.png)

在左边窗格中：

1. 清除搜索框并选择&#x200B;**[!UICONTROL 隐藏用户]**。
2. 找到并将`community-enablementmanagers`拖到右侧窗格中显示的新用户的&#x200B;**[!UICONTROL 组]**&#x200B;选项卡。

   ![分配组](assets/assign-group.png)

### 社区管理员角色{#community-administrators-role}

如[创作组角色](#author-group-roles)图表中所述，社区管理员组的成员能够创建社区站点、管理站点、管理成员（他们可以禁止社区成员）以及审核内容。

按照与创建用户并将其分配给[启用管理器](#communitysiteenablementmanagerrole)的角色相同的步骤操作，但在用户的“组”选项卡下添加c `ommunity-administrators`组。

### LDAP集成{#ldap-integration}

AEM支持使用LDAP对用户进行身份验证以及创建用户帐户。 有关详细信息，请参见[使用AEM 6](../../help/sites-administering/ldap-config.md)配置LDAP。

以下是特定于社区成员和成员组的一些配置详细信息。

1. 为每个AEM发布实例配置LDAP。
2. [LDAP标识提供程序](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 无特殊说明

3. [同步处理程序](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 设置以下属性：

      * **[!UICONTROL 用户自动成员资格]**:  `community-<site name>-<uid>-members`
      * **[!UICONTROL 用户路径前缀]**:  `/community`
      * **[!UICONTROL 组路径前缀]**:  `/community`

4. [外部登录模块](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 没有特别说明

这会导致用户被自动分配到社区站点的成员组，并且存储库位置为`/home/users/community`和`/home/groups/community`，以便他们继承相应的权限来查看彼此的配置文件。

* `User auto membership`值应为`rep:authorizableId`属性，而不是配置文件中的`givenName`（显示名称）。

## 在AEM实例之间同步用户{#synchronizing-users-among-aem-instances}

使用[发布场](topologies.md)时，请确保用户在每个发布实例上具有相同的路径，方法是先将用户导入一个实例，然后[启用用户同步](sync.md)以Sling将用户分发到其他发布实例。

如果导入用户组，要确保用户组在每个发布实例上具有相同的路径，请导入到一个实例，然后[创建要导出的包](../../help/sites-administering/package-manager.md#creating-a-new-package)，然后在所有其他发布实例上安装该包。

虽然通过用户同步同步对用户组的同步将包含在将来的版本中，但当前只有用户组的&#x200B;*成员资格*&#x200B;将在用户同步运行时同步。

## 关于社区组{#about-community-groups}

讨论组时，有两个不同的主题：

* **[社区组](overview.md#communitygroups)**

   社区组是指在发布环境中为支持创建社区组的社区站点创建的子社区。 创建社区组会导致向网站添加更多页面，并以与其父社区站点类似的方式进行管理。 有关更多信息，请访问[社区组Essentials](essentials-groups.md)（面向开发人员）和[社区组](creating-groups.md)（面向作者）。

* **[成员组](../../help/sites-administering/security.md)**

   成员组是成员可能属于的组，可通过“组”控制台进行管理。 本页讨论的大部分内容都是专门讨论会员组。 自动为社区站点创建的成员组（前缀为&#x200B;*`Community`*）可称为社区组，因此必须考虑讨论的上下文。
