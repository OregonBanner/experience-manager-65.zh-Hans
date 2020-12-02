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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 4%

---


# 成员和组管理控制台{#members-groups-management-consoles}

## 概述 {#overview}

AEM Communities的功能通常要求在参与发布环境的社区之前注册和登录站点访客。 他们的用户注册只需存在于发布环境中，通常称为&#x200B;*成员*，以区分他们与在创作环境中注册的&#x200B;*用户*。

### 发布{#members-users-on-publish}时的成员（用户）

使用“社区成员”和“组”控制台，可以从&#x200B;*author*&#x200B;环境创建和管理在&#x200B;*publish*&#x200B;环境中注册的成员和成员组。 仅当启用[隧道服务](deploy-communities.md#tunnel-service-on-author)时，才可能出现这种情况。

### 作者{#users-on-author}上的用户

要管理在&#x200B;*author*&#x200B;环境中注册的用户和用户组，必须使用平台的安全控制台：

* 在全局导航中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用户]**。
* 在全局导航中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 组]**。

>[!NOTE]
>
>在部署和启用示例内容后，创作和发布环境中都存在许多示例用户。 运行[nosamplecontent运行模式](../../help/sites-administering/production-ready.md)时，这些用户将不存在。

## 成员控制台{#members-console}

在创作环境中，要访问“成员”控制台，以管理在发布环境中注册的成员：

* 从全局导航中，选择&#x200B;**[!UICONTROL 导航]** > **[!UICONTROL 社区]** > **[!UICONTROL 成员]**

>[!CAUTION]
>
>如果未启用[隧道服务](deploy-communities.md#tunnel-service-on-author)，则将无法使用成员控制台。

![member-console1](assets/member-console1.png)

### 搜索 {#search-features}

选择`Members`标题左侧的侧面板图标以打开搜索侧面板。

![](assets/leftpanel-icon.png)


![member-console2](assets/member-console2.png)

选择`Members`标题左侧的搜索图标以切换关闭的搜索侧面板。

### 成员统计信息{#member-statistics}

当用户是启用了Adobe Analytics[的一个或多个社区站点的成员时，将更新显示`Views`、`Posts`、`Follows`和`Likes`的列。](sites-console.md#analytics)

### 导出 CSV {#export-csv}

选择`Export CSV`链接会将所有成员下载为逗号分隔的列表，适合导入到电子表格中。

列标题为

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 创建新成员 {#create-new-member}

选择`Create Member`以在发布环境中创建用户。

![create-member1](assets/create-member1.png)

### 常规——成员详细信息{#general-member-details}

大多数字段是成员以后可以在其用户档案中填写的可选字段。

* **[!UICONTROL ID]**

（*必需*）可授权的ID是成员的登录ID。
默认情况下，ID设置为所需电子邮件地址的值。
*创建ID后，将无法修改该ID*。

* **[!UICONTROL 电子邮件地址]**

（*必需*）成员的电子邮件地址。
成员在更新其用户档案时可更改其电子邮件地址。I
如果ID默认为电子邮件地址，则当电子邮件地址发生更改时，ID将*不*&#x200B;发生更改。

* **[!UICONTROL 密码]**

   （*必需*）登录密码。

* **[!UICONTROL 重新键入密码]**

   （*必需*）重新输入密码以进行验证。

* **[!UICONTROL 将成员添加到站点]**

   （*可选*）从现有社区站点中进行选择，以将成员添加到社区站点的成员组。

* **[!UICONTROL 将成员添加到组]**

   （*可选*）从现有成员组中进行选择，以将成员添加到该组。

* 选择&#x200B;**[!UICONTROL 保存]**

### 常规——帐户设置{#general-account-settings}

在“帐户设置”下，社区管理员可以：

* **[!UICONTROL 状态]**
   * 禁用
成员无法登录，无法查看页面或参与需要登录的活动。 他们可能仍会匿名访问一个开放的社区站点。

   * 未禁止
会员可以完全访问社区站点。

   默认值为`Not Banned`。

* **[!UICONTROL 贡献限制]**

   如果选中，则成员发布内容的能力将受到限制。
默认值取决于贡献限制的配置。
请参阅[成员贡献限制](limits.md)。

* **[!UICONTROL 更改密码]**

   修改现有成员时存在的链接。 提供社区管理员重置成员口令的功能。

### 常规——照片{#general-photo}

要为成员提供头像，请首先选择&#x200B;**[!UICONTROL 上传图像]**，然后选择。jpg、.png、.tif或。gif类型的图像。 图像的首选大小为240 x 240像素，72 dpi。

### 常规——将成员添加到站点{#general-add-member-to-sites}

该成员可以添加到一个或多个社区站点的成员组。 首先在文本框中输入文本。

### 常规——将成员添加到组{#general-add-member-to-groups}

该成员可以添加到一个或多个成员组。 首先在文本框中输入文本。

### 标记选项卡{#badges-tab}

`BADGES`面板提供手动分配标记以及撤销标记的功能。 徽章可以用于分配角色和通常获得的徽章。

另请参阅[评分和标记](implementing-scoring.md)。

![create-member2](assets/create-member2.png)

* **[!UICONTROL 添加标记]**
   * 开始键入内容以从[可用标记](badges.md)中进行选择。 选择标记后，请选择每个站点或所有站点，在这些站点上应显示标记以及成员的头像。
   * 可以选择多个标记和站点。
* **[!UICONTROL 删除标记]**
   * 选择徽章旁边的垃圾桶图标以将其删除。

## 组控制台{#groups-console}

“组”控制台(可从创作环境中访问)允许创建和管理在发布环境中注册的成员组。 它对以下项目特别有用：
* [特权成员组](users.md#privilegedmembersgroups)
* [启用资源](resources.md)的基于组的分配

要访问“组”控制台，请执行以下操作：
* 从全局导航中，选择&#x200B;**[!UICONTROL 导航]** > **[!UICONTROL 社区]** > **[!UICONTROL 组]**。

>[!CAUTION]
>
>如果未启用[隧道服务](deploy-communities.md#tunnel-service-on-author)，则无法使用组控制台。

### 创建新组 {#create-new-group}

选择`Add Group`以在发布环境中创建组。

![group-console1](assets/group-console1.png)

创建新发布端成员组的必填字段包括：

* **[!UICONTROL ID]**

   （*必需*）组唯一ID。

   *创建ID后，将无法修改该ID。*

* **[!UICONTROL 名称]**

   （*可选*）组的显示名称。

   默认值为ID。

* **[!UICONTROL 描述]**

   （*可选*）组用途和权限的说明。

* **[!UICONTROL 将成员添加到组]**

   （*可选*）选择要作为组初始成员包含的发布端成员。

* 选择&#x200B;**[!UICONTROL 保存]**

## 授权管理员{#authorized-administrators}

在“社区成员”控制台中使用成员时，必须以具有相应权限的用户身份登录，[隧道服务](deploy-communities.md#tunnel-service-on-author)使用的复制代理才能正确配置。

如果登录名不是`admin`，则登录用户必须是`administrators`用户组的成员。

另请参阅[作者](deploy-communities.md#replication-agents-on-author)上的复制代理。
