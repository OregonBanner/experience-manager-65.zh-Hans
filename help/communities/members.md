---
title: 成员和组管理控制台
seo-title: 成员和组管理控制台
description: 如何访问“成员”和“组”管理控制台
seo-description: 如何访问“成员”和“组”管理控制台
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 成员和组管理控制台 {#members-groups-management-consoles}

## 概述 {#overview}

AEM Communities功能通常要求站点访问者在参与发布环境中的社区之前进行注册和登录。 他们的用户注册只需要在发布环境中存在，并且通常称为 *成员* ，以区分它们与在创作环境中 *注册的用户* 。

### 发布时的成员（用户） {#members-users-on-publish}

使用“社区成员”和“组”控制台，可以从创作环境创建和管理在 *发布环境中注册的成员* 和成员 *组* 。 只有在启用隧道服务 [时](deploy-communities.md#tunnel-service-on-author) ，才可能这样做。

### 作者用户 {#users-on-author}

要管理在创作环境中注册的用 *户和用户组* ，必须使用平台的安全控制台：

* 从全局导航中选择 `Tools, Security, Users`
* 从全局导航中选择 `Tools, Security, Groups`

>[!NOTE]
>
>在部署和启用示例内容后，创作和发布环境中都存在许多示例用户。 这些用户在运行nosamplecontent运行模式时 [不会出现](../../help/sites-administering/production-ready.md)。

## 成员控制台 {#members-console}

在创作环境中，要访问“成员”控制台来管理在发布环境中注册的成员，请执行以下操作：

* 从全局导航：“导 **[!UICONTROL 航”>“社区”>“成员”]**

>[!CAUTION]
>
>如果未启用通道服务，则无法使 [用成员](deploy-communities.md#tunnel-service-on-author) 控制台。

![chlimage_1-119](assets/chlimage_1-119.png)

### 搜索 {#search-features}

选择标题左侧的侧面板图标以 `Members` 打开搜索侧面板。

![chlimage_1-120](assets/chlimage_1-120.png) ![chlimage_1-121](assets/chlimage_1-121.png)

选择标题左侧的搜索图标以 `Members` 切换关闭的搜索侧面板。

### 会员统计 {#member-statistics}

当用户是启用 `Views`了Adobe `Posts`Analytics的一个或多 `Follows`个社区站点的成员时，显示、更新和更新 `Likes` 的列 [](sites-console.md#analytics)。

### 导出 CSV {#export-csv}

选择链 `Export CSV` 接会导致下载所有成员，作为逗号分隔值列表，适用于导入到电子表格中。

列标题为

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 创建新成员 {#create-new-member}

选择 `Create Member` 以在发布环境中创建用户。

![chlimage_1-122](assets/chlimage_1-122.png)

### 常规——会员详细信息 {#general-member-details}

大多数字段是成员以后可以在其配置文件中填写的可选字段。

* **[!UICONTROL ID]**(*必需*)可授权的ID是成员的登录ID。
默认情况下，ID设置为所需电子邮件地址的值。
   *创建ID后，将无法修改该ID。*

* **[!UICONTROL 电子邮件地址]**(*必需*)成员的电子邮件地址。
成员在更新其个人资料时可以更改其电子邮件地址。如果ID默认为电子邮件地址，则 *ID在电子邮件地址发生更改时* ，不会更改。

* **[!UICONTROL 密码]**(*必需*)登录密码。

* **[!UICONTROL 重新键入密]**&#x200B;码&#x200B;*(必*&#x200B;需)重新输入密码以进行验证。

* **[!UICONTROL 将成员添加到站点]**(*可选*)从现有社区站点中进行选择，以将成员添加到社区站点的成员组。

* **[!UICONTROL 将成员添加到组]**(*可选*)从现有成员组中进行选择，以将成员添加到该组。

* Select **[!UICONTROL Save]**

### 常规——帐户设置 {#general-account-settings}

在“帐户设置”下，社区管理员可以

* **[!UICONTROL 状态]**
   * 禁止会员无法登录，无法查看页面或参与需要登录的活动。 他们可能仍会匿名访问一个开放的社区站点。

   * 未禁止会员有权完全访问社区站点。
   Default is `Not Banned`.

* **[!UICONTROL 贡献限]**制如果选中此项，则会员发布内容的能力将受到限制。
默认值取决于贡献限制的配置。
请参 [阅会员贡献限制](limits.md)。

* **[!UICONTROL 更改口]**&#x200B;令修改现有成员时显示的链接。 提供社区管理员重置成员口令的功能。

### 常规——照片 {#general-photo}

要为成员提供头像，请首先选择“上 **[!UICONTROL 传图像]** ”，然后选择。jpg、.png、.tif或。gif类型的图像。 图像的首选大小为240 x 240像素，72 dpi。

### GENERAL - Add Member to Sites {#general-add-member-to-sites}

该成员可以添加到一个或多个社区站点的成员组。 首先在文本框中输入文本。

### GENERAL - Add Member to Groups {#general-add-member-to-groups}

该成员可以添加到一个或多个成员组。 首先在文本框中输入文本。

### 标记选项卡 {#badges-tab}

该 `BADGES` 面板提供手动分配标记以及撤销标记的功能。 标记可以用于分配的角色以及通常获得的标记。

另请参阅 [评分和徽章](implementing-scoring.md)。

![chlimage_1-123](assets/chlimage_1-123.png)

* **[!UICONTROL 添加标记]**
   * 开始键入内容以从可用标记 [中进行选择](badges.md)。 选择一个徽章后，请选择每个站点或所有站点，在这些站点上应显示该徽章和成员的头像。
   * 可以选择多个标记和站点。
* **[!UICONTROL 删除标记]**
   * 选择徽章旁边的垃圾桶图标以将其删除

## 组控制台 {#groups-console}

“组”控制台可从创作环境中访问，它允许创建和管理在发布环境中注册的成员组。 它对以下项目特别有用：
* [特权成员组](users.md#privilegedmembersgroups)
* 基于组的启用资 [源分配](resources.md)

要访问“组”控制台，请执行以下操作：
* 从全局导航：“导 **[!UICONTROL 航”>“社区”>“组”]**

>[!CAUTION]
>
>如果未启用通道服务，则无法使用“ [组”控制台](deploy-communities.md#tunnel-service-on-author) 。

### 创建新组 {#create-new-group}

选择 `Add Group` 以在发布环境中创建组。

![chlimage_1-124](assets/chlimage_1-124.png)

创建新发布端成员组的必填字段包括：

* **[!UICONTROL ID]**(*必需*)组唯一ID。
   *创建ID后，将无法修改该ID。*

* **[!UICONTROL 名称]**(*可选*)组的显示名称。

   默认值是ID。

* **[!UICONTROL 说明]**(*可选*)组用途和权限的说明。

* **[!UICONTROL 将成员添加到组]**(*可选*)选择要作为组初始成员包含的发布端成员。

* Select **[!UICONTROL Save]**

## 授权管理员 {#authorized-administrators}

在“社区成员”控制台中使用成员时，必须以具有相应权限的用户身份登录，以及要正确配置隧道服务使用的复 [制代理](deploy-communities.md#tunnel-service-on-author) 。

如果登录名不是 `admin`作为，则登录用户必须是用户组的 `administrators` 成员。

另请参阅作 [者上的复制代理](deploy-communities.md#replication-agents-on-author)。
