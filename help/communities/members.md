---
title: 成员和组管理控制台
seo-title: 成员和组管理控制台
description: 如何访问成员和组管理控制台
seo-description: 如何访问成员和组管理控制台
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
role: Administrator
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 4%

---

# 成员和组管理控制台{#members-groups-management-consoles}

## 概述 {#overview}

AEM Communities功能通常要求网站访客在参与发布环境的社区之前先进行注册和登录。 其用户注册只需要存在于发布环境中，通常称为&#x200B;*members*，以便与在创作环境中注册的&#x200B;*用户*&#x200B;区分开来。

### 发布{#members-users-on-publish}时的成员（用户）

使用“社区成员”和“组”控制台，可以从&#x200B;*author*&#x200B;环境中创建和管理在&#x200B;*publish*&#x200B;环境中注册的成员和成员组。 只有在启用[隧道服务](deploy-communities.md#tunnel-service-on-author)时，才可以这样做。

### 创作{#users-on-author}的用户

要管理在&#x200B;*author*&#x200B;环境中注册的用户和组，必须使用平台的安全控制台：

* 从全局导航中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用户]**。
* 从全局导航中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 组]**。

>[!NOTE]
>
>部署并启用了示例内容后，许多示例用户同时存在于创作和发布环境中。 使用[nosamplecontent运行模式](../../help/sites-administering/production-ready.md)运行时，这些用户将不存在。

## 成员控制台{#members-console}

在创作环境中，要访问“成员”控制台以管理在发布环境中注册的成员，请执行以下操作：

* 从全局导航中，选择&#x200B;**[!UICONTROL 导航]** > **[!UICONTROL 社区]** > **[!UICONTROL 成员]**

>[!CAUTION]
>
>如果未启用[隧道服务](deploy-communities.md#tunnel-service-on-author)，则无法使用成员控制台。

![member-console1](assets/member-console1.png)

### 搜索 {#search-features}

选择`Members`标题左侧的侧面板图标可切换打开搜索侧面板。

![](assets/leftpanel-icon.png)


![member-console2](assets/member-console2.png)

选择`Members`标题左侧的搜索图标，以关闭搜索侧面板。

### 成员统计数据{#member-statistics}

当用户是一个或多个社区站点的成员且启用了Adobe Analytics [时，将更新显示`Views`、`Posts`、`Follows`和`Likes`的列。](sites-console.md#analytics)

### 导出 CSV {#export-csv}

选择`Export CSV`链接会导致下载所有成员作为逗号分隔值列表，这些值适用于导入到电子表格中。

列标题为

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 创建新成员 {#create-new-member}

选择`Create Member`以在发布环境中创建用户。

![create-member1](assets/create-member1.png)

### 常规 — 成员详细信息{#general-member-details}

大多数字段是成员稍后可以在其配置文件中填写的可选字段。

* **[!UICONTROL ID]**

（*必需*）可授权的ID是成员的登录ID。
默认情况下，ID会设置为所需电子邮件地址的值。
*创建ID后，无法修改该ID*。

* **[!UICONTROL 电子邮件地址]**

（*必需*）成员的电子邮件地址。
成员在更新其用户档案时可更改其电子邮件地址。
如果ID默认为电子邮件地址，则ID在更改电子邮件地址时将*not*&#x200B;更改。

* **[!UICONTROL 密码]**

   （*必需*）登录密码。

* **[!UICONTROL 重新键入密码]**

   （*必需*）重新输入密码以进行验证。

* **[!UICONTROL 将成员添加到站点]**

   （*可选*）从现有社区站点中选择，以将成员添加到社区站点的成员组。

* **[!UICONTROL 将成员添加到组]**

   （*可选*）从现有成员组中选择，以将成员添加到该组。

* 选择&#x200B;**[!UICONTROL Save]**

### 常规 — 帐户设置{#general-account-settings}

在“帐户设置”下，社区管理员可以：

* **[!UICONTROL 状态]**
   * 被禁
会员无法登录，无法查看页面或参与需要登录的活动。 他们可能仍会匿名访问一个开放的社区网站。

   * 未禁用
会员拥有社区站点的完全访问权限。

   默认值为`Not Banned`。

* **[!UICONTROL 贡献限制]**

   如果选中此项，则成员发布内容的能力会受到限制。
默认值取决于贡献限制的配置。
请参阅[成员贡献限制](limits.md)。

* **[!UICONTROL 更改密码]**

   修改现有成员时存在的链接。 提供社区管理员为成员重置密码的功能。

### 常规 — 照片{#general-photo}

要为成员提供头像，请首先选择&#x200B;**[!UICONTROL 上传图像]**，然后选择.jpg、.png、.tif或.gif类型的图像。 图像的首选大小为240 x 240像素，为72 dpi。

### 常规 — 将成员添加到站点{#general-add-member-to-sites}

可以将成员添加到一个或多个社区站点的成员组中。 首先，在文本框中输入文本。

### 常规 — 将成员添加到组{#general-add-member-to-groups}

该成员可以添加到一个或多个成员组。 首先，在文本框中输入文本。

### “徽章”选项卡{#badges-tab}

`BADGES`面板提供手动分配徽章以及撤消徽章的功能。 这些徽章可用于分配的角色以及通常获得的徽章。

另请参阅[评分和徽章](implementing-scoring.md)。

![create-member2](assets/create-member2.png)

* **[!UICONTROL 添加徽章]**
   * 开始键入内容以从[可用徽章](badges.md)中进行选择。 选择标记后，选择每个网站或所有网站，该标记应与成员的头像一起显示在这些网站上。
   * 可以选择多个徽章和站点。
* **[!UICONTROL 删除徽章]**
   * 选择徽章旁边的垃圾桶图标以将其删除。

## 组控制台{#groups-console}

“组”控制台（可从创作环境中访问）允许创建和管理在发布环境中注册的成员组。 它特别适用于：
* [特权成员组](users.md#privilegedmembersgroups)
* 基于组的[启用资源](resources.md)分配

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

   *创建ID后，无法修改该ID。*

* **[!UICONTROL 名称]**

   （*可选*）组的显示名称。

   默认值为ID。

* **[!UICONTROL 描述]**

   （*可选*）群组用途和权限的描述。

* **[!UICONTROL 将成员添加到组]**

   （*可选*）选择要作为组初始成员包含的发布端成员。

* 选择&#x200B;**[!UICONTROL Save]**

## 授权管理员{#authorized-administrators}

在社区成员控制台中与成员合作时，必须以具有适当权限的用户身份登录，并且要正确配置[隧道服务](deploy-communities.md#tunnel-service-on-author)使用的复制代理。

如果未以`admin`的形式登录，则登录用户必须是`administrators`用户组的成员。

另请参阅[创作](deploy-communities.md#replication-agents-on-author)上的复制代理。
