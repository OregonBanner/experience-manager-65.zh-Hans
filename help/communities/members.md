---
title: 成员和组管理控制台
description: 如何访问成员和组管理控制台
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 3%

---


# 成员和组管理控制台 {#members-groups-management-consoles}

## 概述 {#overview}

AEM Communities功能通常要求网站访客先注册并登录，然后才能在发布环境中加入社区。 它们的用户注册只需要存在于发布环境中，通常称为 *成员* 来区分他们 *用户* 已在创作环境中注册。

### 发布中的成员（用户） {#members-users-on-publish}

使用在中注册的社区成员和组控制台、成员和成员组 *发布* 可以从以下位置创建和管理环境 *作者* 环境。 只有当 [通道服务](deploy-communities.md#tunnel-service-on-author) 已启用。

### 作者中的用户 {#users-on-author}

用于管理在中注册的用户和组 *作者* 环境，必须使用平台的安全控制台：

* 在全局导航中，选择 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 用户]**.
* 在全局导航中，选择 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 组]**.

>[!NOTE]
>
>部署和启用示例内容后，创作和发布环境中都会存在许多示例用户。 运行以下内容时，这些用户将不会出现： [nosamplecontent运行模式](../../help/sites-administering/production-ready.md).

## 成员控制台 {#members-console}

在创作环境中，要访问成员控制台以管理在发布环境中注册的成员，请执行以下操作：

* 在全局导航中，选择 **[!UICONTROL 导航]** > **[!UICONTROL Communities]** > **[!UICONTROL 成员]**

>[!CAUTION]
>
>在以下情况下，将无法使用成员控制台： [通道服务](deploy-communities.md#tunnel-service-on-author) 未启用。

![成员控制台](assets/member-console1.png)

### 搜索 {#search-features}

选择左侧的侧面板图标 `Members` 标题以切换打开搜索侧面板。

![搜索侧面板图标。](assets/leftpanel-icon.png)


![成员控制台的筛选器选项](assets/member-console2.png)

选择左侧的搜索图标 `Members` 标题以关闭搜索侧面板。

### 成员统计信息 {#member-statistics}

显示的列 `Views`， `Posts`， `Follows` 和 `Likes` 当用户是具有Adobe Analytics的一个或多个社区站点的成员时，将更新 [已启用](sites-console.md#analytics).

### 导出 CSV {#export-csv}

选择 `Export CSV` 链接会以逗号分隔值列表的形式下载所有成员，适合导入到电子表格中。

列标题为

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 创建新成员 {#create-new-member}

选择 `Create Member` 以在发布环境中创建用户。

![创建新成员窗口](assets/create-member1.png)

### 常规 — 成员详细信息 {#general-member-details}

大多数字段是可选字段，成员以后可在其配置文件中填写。

* **[!UICONTROL ID]**

(*必填*)可授权ID是成员的登录ID。
默认情况下，ID设置为所需电子邮件地址的值。
*ID创建后即无法修改*.

* **[!UICONTROL 电子邮件地址]**

(*必填*)成员的电子邮件地址。
成员可以在更新用户档案时更改其电子邮件地址。I如果ID默认使用电子邮件地址，则ID将 *非* 更改电子邮件地址时进行更改。

* **[!UICONTROL 密码]**

  (*必填*)登录密码。

* **[!UICONTROL 重新键入密码]**

  (*必填*)重新输入验证密码。

* **[!UICONTROL 将成员添加到站点]**

  (*可选*)从现有社区站点中选择以将该成员添加到社区站点的成员组。

* **[!UICONTROL 将成员添加到组]**

  (*可选*)从现有成员组中选择以将该成员添加到该组。

* 选择 **[!UICONTROL 保存]**

### 常规 — 帐户设置 {#general-account-settings}

在“帐户设置”下，社区管理员可以：

* **[!UICONTROL 状态]**
   * 已禁止成员无法登录，导致他们无法查看页面或参与需要登录的活动。 他们仍可匿名访问开放的社区站点。

   * 未禁止成员具有对社区站点的完全访问权限。

  默认为 `Not Banned`.

* **[!UICONTROL 贡献限制]**

  如果选中，则成员发布内容的能力有限。
默认值取决于贡献限制的配置。
请参阅 [成员贡献限制](limits.md).

* **[!UICONTROL 更改密码]**

  修改现有成员时显示的链接。 使社区管理员能够重置成员的密码。

### 常规 — 照片 {#general-photo}

要为成员提供头像，请从选择 **[!UICONTROL 上传图像]** 并选择.jpg、.png、.tif或.gif类型的图像。 图像的首选大小为240 x 240像素(72 dpi)。

### 常规 — 将成员添加到站点 {#general-add-member-to-sites}

可以将成员添加到一个或多个社区站点的成员组。 首先在文本框中输入文本。

### 常规 — 将成员添加到组 {#general-add-member-to-groups}

可以将成员添加到一个或多个成员组。 首先在文本框中输入文本。

### 徽章选项卡 {#badges-tab}

此 `BADGES` 面板提供手动分配徽章以及撤销徽章的功能。 该徽章可能是用于分配的角色，也可能是通常获得的徽章。

另请参阅 [评分和徽章](implementing-scoring.md).

![编辑成员资格设置窗口](assets/create-member2.png)

* **[!UICONTROL 添加徽章]**
   * 开始键入以从中进行选择 [可用徽章](badges.md). 选择徽章后，选择每个站点或所有站点，徽章应随成员的头像一起显示在这些站点上。
   * 可以选择多个徽章和站点。
* **[!UICONTROL 删除徽章]**
   * 选择徽章旁边的垃圾桶图标以将其删除。

## 组控制台 {#groups-console}

通过可在创作环境中使用的组控制台，可创建和管理在发布环境中注册的成员组。 它尤其可用于 [拥有权限的成员组](users.md#privilegedmembersgroups).

要访问“组”控制台，请执行以下操作：
* 在全局导航中，选择 **[!UICONTROL 导航]** > **[!UICONTROL Communities]** > **[!UICONTROL 组]**.

>[!CAUTION]
>
>在以下情况下，将无法使用组控制台： [通道服务](deploy-communities.md#tunnel-service-on-author) 未启用。

### 创建新组 {#create-new-group}

选择 `Add Group` 以在发布环境中创建组。

![创建新组窗口](assets/group-console1.png)

创建新发布端成员组的必填字段包括：

* **[!UICONTROL ID]**

  (*必填*)组的唯一ID。

  *ID创建后即无法修改。*

* **[!UICONTROL 名称]**

  (*可选*)组的显示名称。

  默认值为ID。

* **[!UICONTROL 描述]**

  (*可选*)对组用途和权限的描述。

* **[!UICONTROL 将成员添加到组]**

  (*可选*)选择要作为组的初始成员包括的发布端成员。

* 选择 **[!UICONTROL 保存]**

## 授权管理员 {#authorized-administrators}

使用“社区”成员控制台中的成员时，需要以具有适当权限的用户身份登录，并且还需要使用复制代理。 [通道服务](deploy-communities.md#tunnel-service-on-author) 进行正确配置。

如果未登录为 `admin`，则登录用户必须是 `administrators` 用户组。

另请参阅 [创作实例上的复制代理](deploy-communities.md#replication-agents-on-author).
