---
title: 体验发布的站点
seo-title: 体验发布的站点
description: 浏览到已发布的站点
seo-description: 浏览到已发布的站点
uuid: 44594e9e-27ad-475d-953d-3611b04f0df8
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: dd0cbc05-a361-46bc-b9f1-d045f8f23890
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 1%

---


# 体验发布的站点 {#experience-the-published-site}

## 在发布时浏览到新站点 {#browse-to-new-site-on-publish}

新创建的社区站点已发布后，浏览到创建站点时显示的URL，但浏览到发布服务器，例如：

* 作者URL = https://localhost:4502/content/sites/engage/en.html
* 发布URL = https://localhost:4503/content/sites/engage/en.html

为最大限度地减少在创作和发布时登录到哪个成员的混淆，建议对每个实例使用不同的浏览器。

首次访问发布的站点时，站点访客通常尚未登录，并且为匿名内容。

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![署名](assets/authorpublished.png)

## 匿名网站访客 {#anonymous-site-visitor}

匿名站点访客在UI中可以看到以下内容：

* 站点标题（入门教程）
* 无用户档案链接
* 无消息链接
* 无通知链接
* 搜索字段
* 登录链接
* 品牌横幅
* 引用站点模板中包含的组件的菜单链接。

如果您选择了各种链接，您会发现它们处于只读模式。

### 防止对JCR进行匿名访问 {#prevent-anonymous-access-on-jcr}

已知限制通过jcr内容和json将社区站点内容公开给匿名访客，但 **对于站点的内容** ，允许匿名访问是禁用的。 但是，可以使用Sling Restrictions作为解决方法来控制此行为。

要保护您的社区站点的内容免受匿名用户通过jcr内容和json访问，请执行以下步骤：

1. 在AEM作者实例上，转到https:// hostname:port/editor.html/content/site/sitename.html。

   >[!NOTE]
   >
   >请勿转到本地化的站点。

1. 转到页 **面属性**。

   ![page-properties](assets/page-properties.png)

1. 转至“高 **级** ”选项卡。

1. Enable **Authentication Requirement**.

   ![站点身份验证](assets/site-authentication.png)

1. 添加登录页面的路径。 例如， **/content/....../GetStarted**。
1. 发布页面。

## 受信任的社区成员 {#trusted-community-member}

此体验假设 [Aaron](/help/communities/tutorials.md#demo-users) McDonald被分配为社区 [经理和主持人角色](/help/communities/create-site.md#roles)。 如果不是，请返回作者环境修 [改站点设置](/help/communities/sites-console.md#modifying-site-properties) ，并选择Aaron McDonald作为社区经理和版主。

在右上角，选择并 `Log in`使用用户名(aaron.mcdonald@mailinator.com)和密码（密码）进行签名。 注意使用Twitter或Facebook凭据登录的能力。

![登录](assets/login.png)

以注册社区成员身份登录后，请注意以下菜单项，单击并浏览您的社区站点：

* **用户档案** 选项允许您视图和编辑用户档案。
* [“消息](/help/communities/configure-messaging.md) ”选项将指向“直接消息”部分，在该部分，您可以：

   1. 视图您收到的（收件箱）、发送（已发送项目）和删除（垃圾桶）的直接邮件。
   1. 编写新的直接消息以发送给个人和组。

* [通知](/help/communities/notifications.md) 选项会指引您进入通知部分，您可以在该部分视图您感兴趣的事件并编辑通知设置。
* [管理](/help/communities/published-site.md#moderationlink) （如果您具有审核权限）会将您定向到AEM Communities审核页面。

![adminstree](assets/adminscreen.png)

请注意，“日历”页面是主页，因为所选的“参考站点模板”首先包含“日历”功能，然后是“活动流”功能、“论坛”功能等。 此结构可从站点模板控 [制台中](/help/communities/sites.md#edit-site-template) ，或在创作环境中修改站点属性时显示：

![站点模板](assets/sitetemplate.png)

>[!NOTE]
>
>有关Communities组件和功能的更多信息，请访问：
>
>* [社区组件](/help/communities/author-communities.md) （针对作者）
>* [组件、功能和功能要件](/help/communities/essentials.md) （针对开发人员）


### 论坛链接 {#forum-link}

视图基本论坛功能，方法是选择论坛链接。

成员可以发布新主题或关注主题。

站点访客能够视图帖子并以各种方式对其进行排序。

![forumlink](assets/forumlink.png)

### 组链接 {#groups-link}

由于Aaron是组管理员，选择“组”链接将允许Aaron通过选择组模板、图像、组是开放还是秘密以及邀请成员来创建新的社区组。

这是在发布环境中创建组的示例。

用户组也可以在作者环境中创建，并在创作环境（“社区组”控制台）的社[区站点内进行](/help/communities/groups.md)管理。 本教程的 [下一个内容是](/help/communities/nested-groups.md) ，在创作时创建组。

![上行](assets/grouplink.png)

创建引用组：

1. 选择 **新组**
1. **“设置”选项卡**

   * 组名称 : `Sports`
   * 描述 : `A parent group for various sporting groups`.
   * 组 URL 名称 : `sports`
   * 选 `Open Group` 择（允许任何社区成员通过加入来参加）

1. **模板选项卡**

   * 选 `Reference Group` 择（在其结构中包含组函数以允许嵌套组）

1. 选择 **创建组**

   ![creategroup](assets/creategroup.png)

创建新组后，选 **择新的“体育组** ”，以便在其中创建两个组（嵌套）。 由于站点结构不能从组功能开始，在打开运动组后，必须选择组链接：

![grouplink1](assets/grouplink1.png)

第二组链接(从开始 `Blog`)属于当前选定的组，即 `Sports` 组。 通过选择“体 `Groups` 育”链接，可以在“体育”组内嵌套两个组。

例如，添加两个 `new groups`。

* 一个 `Baseball`

   * 将其设置为(必 `Open Group` 需的会员资格)。
   * 在“模板”选项卡上，选择 `Conversational Group`。

* 一个 `Gymnastics`

   * 将其设置更改为 `Member Only Group` （受限会员资格）。
   * 在“模板”选项卡上，选择 `Conversational Group`。

**通知**:

* 在显示两个组之前，可能需要刷新页面。
* 此模板不 *包含* “组”函数，因此不可能进一步嵌套组。
* 在创作时，“ [组”控制台](/help/communities/groups.md) 提供第三个选择- `Public Group` （可选成员资格）。

创建两个组后，选择“棒球”组、打开的组，并注意其链接：

`Discussions` `What's New` `Members`

组的链接显示在主站点的链接下方，并会显示以下内容：

![grouplink2](assets/grouplink2.png)

在创作时——具有管理权限，导航到“ [社区组”控制台](/help/communities/members.md) ，并将Weston McCall添加到 `Community Engage Gymnastics <uid> Members` 组中。

继续发布内容，以Aaron McDonald的身份注销，并以匿名网站访客的身份视图体育团体中的团体：

* 从主页
* 选择链 `Groups` 接
* 选择链 `Sports` 接
* 选择体育链 `Groups` 接

只有棒球组可见。

以Weston McCall(weston.mccall@dodgit.com /密码)身份登录，然后导航到同一位置。 请注意，Weston能够访问 `Join` 打开 `Baseball` 的组和 `enter or Leave` 私有 `Gymnastics` 组。

![grouplink3](assets/grouplink3.png)

### 网页链接 {#web-page-link}

视图包含在站点中的基本网页，方法是选择网页链接。 标准AEM创作工具可用于在创作环境中向此页面添加内容。

例如，转到作 **者实例** ，在“社区站点” `engage` 控制台中打 [开文件夹](/help/communities/sites-console.md)，选择“打开站点 **** ”图标以进入作者编辑模式。 然后选择预览模式以选择链 `Web Page` 接，然后选择编辑模式以添加标题和文本组件。 最后，只重新发布页面或整个站点。

![webpagelink](assets/webpagelink.png)

### 审核链接 {#moderationlink}

当社区成员具有审核权限时，“审核”链接将可见，选择该链接后，将显示已发布的社区内容，并允许以与创作环境中的审核控制台 [类似](/help/communities/moderate-ugc.md) 的方 [式进行审核](/help/communities/moderation.md) 。

使用浏览器的返回按钮返回已发布的站点。 大多数控制台都无法通过发布环境中的全局导航访问。 [](/help/communities/moderate-ugc.md)

![版本链接](assets/moderationlink.png)

## 自助注册 {#self-registration}

注销后，可以创建新用户注册。

* 选择 `Log In`
* 选择 `Sign up for a new account`

![注册](assets/registration.png)

![注册](assets/signup.png)

默认情况下，电子邮件地址为登录ID。 如果未选中，访客可以输入自己的登录ID（用户名）。 用户名在发布环境中必须唯一。

指定用户名、电子邮件和密码后，选择 `Sign Up` 将创建用户并允许其签名。

登录后，显示的第一页即为其页 `Profile` 面，他们可以个性化。

![配置文件](assets/profile.png)

如果成员忘记了其登录ID，则可以使用其电子邮件地址进行恢复。

![forgotusername](assets/forgotusername.png)

