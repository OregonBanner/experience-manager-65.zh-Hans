---
title: 管理用户和用户组
seo-title: 管理用户和用户组
description: AEM Communities的用户可以自行注册和编辑其用户档案
seo-description: AEM Communities的用户可以自行注册和编辑其用户档案
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
translation-type: tm+mt
source-git-commit: 2422ed41b18bc558f0cfc9e80f7eb6f4923aa07c

---


# Managing Users and User Groups {#managing-users-and-user-groups}

## 概述 {#overview}

在AEM Communities中的发布环境中，用户可以自行注册并编辑其用户档案。 如果拥有相应的权限，他们还可能：

* 在社区站点内创建子社区(请参阅 [社区组](creating-groups.md))。

* [审核用户生成的内容](moderation.md) (UGC)。

* 成为 [启用资源联系](resources.md) 。

* 有权 [为博客](#privileged-members-group) 、日历、问题与答案和论坛创建条目。

在发布环境中注册的用户通常称为社 *区成员（成员）* ，以区分他们与创 *作环境中的用* 户。

通过将成员分配给在从创作环境创建或修 [改社区站点时动态创建的成员（用户）组之一](#publish-group-roles) ，来授予权 [限](sites-console.md)[,](sites-console.md#modifying-site-properties) 即可授予权限。 在创作环境中工作时，成员可通过隧道服务从发布环境中 [看到](#tunnel-service)。

根据设计，在发布环境中创建的成员和成员组不应显示在创作环境中。 在创作环境中创建的用户和用户组同样希望保留在创作环境中。

当创作用户和发布成员来自同一用户列表（如从同一LDAP目录同步）时，他们在创作和发布环境中不被视为具有相同权限和用户组成员关系的同一用户。 成员和用户的角色必须根据需要在发布和创作时分别建立。

对于发 [布场](topologies.md)，在一个发布实例上进行的注册和修改需要与其他发布实例同步，以便它们能够访问相同的用户数据。 有关详细信息， [请参阅用户同步](sync.md)，该同步包含一个描述 [何时发生……的部分](sync.md#what-happens-when).

### 贡献限制 {#contribution-limits}

为了防止垃圾邮件，可以限制会员发布内容的频率。 此外，可以自动限制新登记的成员的捐款。

有关详细信息，请参 [阅会员贡献限制](limits.md)。

### 动态创建的用户组 {#dynamically-created-user-groups}

创建新社区站点时，将使用唯一的id(uid)和权限动态创建新用户组，这些权限适用于在创作环境(请参阅作者组角色 [)或发布环境(请参阅](#author-group-roles)发布组角色 [](#publish-group-roles))中管理社区站点所需的各种管理功能。

在社区站点创建过程中，这些组的名称是根据给定站点 [的名称生成的](sites-console.md#step13asitetemplate)。 唯一ID可避免同一服务器上同名社区站点和社区组的命名冲突。

例如，如果网站名称为“*We.Retail Engage*”的网站，则创建的用户组包括：

* 社区参 *与会员*

## 创作环境 {#author-environment}

### 隧道服务 {#tunnel-service}

使用创作环境创 [建站点](sites-console.md)、修改站点属性 [、管理社区成](sites-console.md#modifying-site-properties) 员和成员组时 [](members.md)，必须访问在发布环境中注册的用户和用户组。

隧道服务使用作者上的复制代理提供此访问。

* 有关详细信息，请参 [阅部署页面上](deploy-communities.md#tunnel-service-on-author) 的配置说明。

“社 [](members.md) 区成员”和“组”控制台仅用于管理仅在发布环境中注册的用户（成员）和用户组（成员组）。

要管理在创作环境中注册的用户和用户组，请使用安全 [控制台](../../help/sites-administering/security.md)

### 作者组角色 {#author-group-roles}

| 如果组成员…… | 主要角色 |
|---|---|
| 管理员 | 管理员组由系统管理员组成，这些管理员具有社区管理员的所有功能以及管理社区管理员组的能力。 |
| 社区管理员 | “社区管理员”组自动成为所有社区站点以及在站点上创建的任何社区组的成员。 社区管理员组的初始成员是管理员组。 在创作环境中，社区管理员可以创建社区站点、管理站点、管理成员（他们可以禁止社区成员）和审核内容。 |
| 社区&lt;*站点名称*> Sitecontentmanager | 社区站点内容管理器能够执行传统的AEM创作、内容创建和修改社区站点的页面。 |
| 社区支持经理 | 社区启用管理者组由可用于分配以管理社区站点的Enablement Managers组的用户组成。 |
| 社区&lt;站&#x200B;*点名称* > Siteenablementmanagers | 社区站点启用管理器组由分配给管理社区站点启用资源的用户组 [成](resources.md)。 |
| 无 | 匿名网站访客可能无法访问作者环境。 |

### 系统管理员 {#system-administrators}

管理员组的成员是系统管理员，他们可以为创作和发布环境执行AEM安装的初始设置。

出于演示和开发目的，管理员组的用户ID为admin，密 *码为* admin *的成员*。

对于生产环境，应修改默认管理员组。

请务必按照安全核 [对清单操作](../../help/sites-administering/security-checklist.md)。

## 发布环境 {#publish-environment}

### 成为会员 {#becoming-a-member}

在发布环境中，根据社 [区站点的设](sites-console.md#user-management) 置，站点访客可能成为社区成员：

* 当社区站点为私有（已关闭）时：
   * 按邀请
   * 按管理员的操作

* 当社区站点为公共站点时（打开）:
   * 通过自助注册
   * 通过Facebook和Twitter进行社交登录

>[!NOTE]
>
>如果站点访客注册为一个开放社区站点的成员，则它们会自动成为同一发布环境中其他开放社区站点的成员。


### 发布组角色 {#publish-group-roles}

| 如果组成员…… | 主要角色 |
|---|---|
| 社区&lt;*站点名称*>成员 | 社区站点成员是注册用户。 他们可以登录、修改其用户档案、加入一个开放的社区组、向社区发布内容、向其他成员发送消息以及遵循站点活动。 |
| 社区&lt;*站点名称*>版主 | 社区站点审查方是可信的社区成员，可以在发布内容的页面上批量审核UGC，也可以使用审核控制台审核，或在上下文中审核。 |
| 社区&lt;*站点名称*> &lt;*组名称*>成员 | 社区组成员是已加入开放社区组或已受邀加入封闭社区组的社区成员。 他们具有站点内该社区组的成员的能力。 |
| 社区&lt;*站点名称*>组管理员 | 社区站点组管理员是受信任的社区成员，被分配来在社区站点中创建和管理子社区（组）。 包括提供上下文内协调的功能。 |
| *特权成员安全组* | 为限制内容创建而手动创建和维护的用户组。 请参阅 [特权成员组](#privileged-members-group)。 |
| 无 | 发现该网站的匿名网站访客可能会视图和搜索允许匿名访问的社区网站。 要参与和发布内容，用户必须自行注册（如果允许）并成为社区成员。 |

### 将成员分配到发布组角色 {#assigning-members-to-publish-group-roles}

在创 [作环境中创建社区站点](sites-console.md) ，或在修改站点属性时， [](sites-console.md#modifying-site-properties) ，可能会为成员分配在发布环境中执行的各种角色，如审核者、组管理员、资源联系人或特权成员。

[启用隧道服务](sync.md#accessingpublishusersfromauthor) ，将导致从发布时的成员而不是作者用户显示分配选项。

所选成员将自动分配到相 [应的组](#publish-group-roles) ，并且在社区站点发布（重新发布）时，将包括其成员关系。

### 拥有权限的成员组 {#privileged-members-group}

特权成员安全组的目的是将某些社区功能的内容的创建限制到社区站点成员的特权子集。

特权成员组是使用“社区组”控制台创建和管理的 [成员组](members.md)。

创建特权成员组后，在启用 [tunnel服务的情况下](sync.md#accessingpublishusersfromauthor)[](sites-console.md#modify-structure) ，可以修改现有社区站点的结构以将其社区功能的配置编辑为“允许特权成员”并添加创建的组。

允许指定一个或多个特权成员组的社区功能包括：

* [博客功能](functions.md#blog-function) -限制创建新文章的创建。
* [日历函数](functions.md#calendar-function) -限制创建新事件。
* [论坛功能](functions.md#forum-function) -限制创建新主题。
* [问题与答案](functions.md#qna-function) -限制创建新问题的创建。

当社区功能未得到保护（未分配特权成员组）时，所有社区站点成员都可以创建功能内容(文章、事件、主题、问题)。

>[!NOTE]
>
>将用户添加到社区站点的特权成员组仅会在用户也是同一社区站点的成员时授予他们创建权限。


## 创建社区成员 {#creating-community-members}

### 存储库位置 {#repository-location}

为了使某些功能正常工作，需要创建具有相应权限的用户和用户组。

在中创建成员后， `/home/users/community`这些成员将继承为成员的用户档案授予读取权限的正确ACL。

同样，自定义社区用户组（如特权成员组）应在中创建 `/home/groups/community`。

使用“社 [区成员”和“组”控制台](members.md) ，将在这些路径中创建用户和组。

要指定自定义路径，需要使用经典安全UI，可从 [https://&lt;server>:&lt;port>/useradmin访问该UI](http://localhost:4503/useradmin)。

要为自定义成员路径授予读取权限，请在所有发布实例上设置ACL，类似于 `/home/users/community`:

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

要为自定义成员组路径（如/home/groups/mycompany）赋予适当的权限，请在所有发布实例上设置ACL，如下所示 `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### 控制台 {#consoles}

只有四个单独的控制台在创作环境中可用：

| console | 工具、安全性、用户 | 工具、安全性、组 | 社区、成员 | 社区、组 |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 管理 | 创作用户 | 作者用户组 | 发布时的成员 | 发布时的成员组 |
| read | 管理员权限 | 管理员权限 | admin权限，隧道服务，用户同步发布场 | admin权限，隧道服务，用户同步发布场 |

### 社区支持管理者角色 {#community-enablement-manager-role}

通常，支持社区不允许站点访客自行注册 [](overview.md#enablement-community) ，因为每个成员都有相关费用。 在创建站点时，启用学员和资源由分配了 [角色](#author-group-roles) （作为组成员添加）的用 `enablement manager` 户管理 [](sites-console.md#enablement)`Community <site-name> Siteenablementmanagers`。 还负 `enablement manager` 责将学习资 [源分配给社区成员](resources.md) （作者）。

只有作为全局用户组的成员 `Community Enablement Managers` 的用户才能被选择为特 `enablement manager` 定社区站点的用户。

要创建可能被分配了角色的用户，请 `Community Site Enablement Manager`使用经典UI安全控制台以指定路径：

在作者实例上：

1. 以管理员权限登录，浏览至经典UI安全控制台。

   例如， [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. 从“编辑”菜单中，选择“创 **[!UICONTROL 建用户”]**。
3. 填写对 `Create User` 话框。
   * 路径必须 `/home/users/community`是。
4. 选择&#x200B;**[!UICONTROL 创建]**。

   ![chlimage_1-130](assets/chlimage_1-130.png)

* 在左窗格中，搜索新创建的用户并选择显示在右窗格中。

   ![chlimage_1-135](assets/chlimage_1-131.png)

在左边窗格中：

1. 清除搜索框，然后选择“隐 **[!UICONTROL 藏用户”]**。
2. 找到并拖 `community-enablementmanagers` 动到右 **[!UICONTROL 窗格中显示的]** “新用户的组”选项卡。

   ![chlimage_1-132](assets/chlimage_1-132.png)

### 社区管理员角色 {#community-administrators-role}

如作者组角色图 [表中所述](#author-group-roles) ，社区管理员组的成员可以创建社区站点、管理站点、管理成员（他们可以禁止社区成员）和审核内容。

按照创建用户并将其分配给Enablement Manager角色的相同步 [骤](#communitysiteenablementmanagerrole)，但在用户的“组”选项 `ommunity-administrators` 卡下添加c组。

### LDAP集成 {#ldap-integration}

AEM支持使用LDAP验证用户身份以及创建用户帐户。 在使用AEM 6配 [置LDAP中详细介绍](../../help/sites-administering/ldap-config.md)。

以下是特定于社区成员和成员组的一些配置详细信息。

1. 为每个AEM发布实例配置LDAP。
2. [LDAP标识提供者](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 无特殊说明

3. [同步处理函数](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 设置以下属性：

      * **[!UICONTROL 用户自动会员资格]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL 用户路径前缀]**: `/community`
      * **[!UICONTROL 组路径前缀]**: `/community`

4. [外部登录模块](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 没有特别说明

这会导致用户被自动分配到社区站点的成员组以及存储库位置 `/home/users/community` 和 `/home/groups/community`，以便他们继承相应的权限来查看彼此的用户档案。

* 该 `User auto membership` 值应该是属 `rep:authorizableId` 性，而不 `givenName` 是用户档案的（显示名称）。

## 在AEM实例之间同步用户 {#synchronizing-users-among-aem-instances}

使用发 [布场时](topologies.md)，通过首先将用户导入一个实例并启用用户同步 [](sync.md) Sling将用户分发到其他发布实例，确保用户在每个发布实例上具有相同的路径。

如果导入用户组，要确保用户组在每个发布实例上具有相同的路径，请导入到一个实例，然后创建一个要导出的包 [](../../help/sites-administering/package-manager.md#creating-a-new-package) ，并将该包安装到所有其他发布实例上。

虽然用户组通过用户同步的同步将包括在将来的版本中，但当前只有用户 *同步运行时* ，用户组的成员关系才会同步。

## 关于社区组 {#about-community-groups}

讨论组时，有两个不同的主题：

* **[社区组](overview.md#communitygroups)**

   社区组是在社区站点的发布环境中可以创建的子社区，该社区支持社区组的创建。 创建社区组会导致向网站添加更多页面，并以与其父社区站点类似的方式进行管理。 有关详细信息，请 [访问Community Group Essentials](essentials-groups.md) for developers和 [Community Group](creating-groups.md) for authors。

* **[成员组](../../help/sites-administering/security.md)**

   成员组是成员可能属于的组，并通过“组”控制台进行管理。 本页讨论的大部分内容都集中在成员组中。 为社区站点自动创建的成员组(前缀为 *`Community`*)可称为社区组，因此必须考虑讨论的上下文。
