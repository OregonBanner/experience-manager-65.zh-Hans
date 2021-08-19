---
title: 体验已发布的网站
seo-title: 体验已发布的网站
description: 浏览到已发布的网站
seo-description: 浏览到已发布的网站
uuid: 44594e9e-27ad-475d-953d-3611b04f0df8
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: dd0cbc05-a361-46bc-b9f1-d045f8f23890
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 1%

---

# 体验已发布的网站 {#experience-the-published-site}

## 在发布时浏览到新站点 {#browse-to-new-site-on-publish}

现在，新创建的社区站点已发布，浏览到创建站点时显示的URL，但在发布服务器上显示，例如：

* 作者URL = https://localhost:4502/content/sites/engage/en.html
* 发布URL = https://localhost:4503/content/sites/engage/en.html

为了最大限度地减少在创作和发布时登录到哪个成员的混淆，建议对每个实例使用不同的浏览器。

首次访问已发布的网站时，网站访客通常尚未登录，且为匿名访客。

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![authorpublished](assets/authorpublished.png)

## 匿名网站访客 {#anonymous-site-visitor}

匿名网站访客在UI中看到以下内容：

* 网站标题（快速入门教程）
* 无配置文件链接
* 无消息链接
* 无通知链接
* 搜索字段
* 登录链接
* 品牌横幅
* 引用站点模板中包含的组件的菜单链接。

如果选择各种链接，则会发现它们处于只读模式。

### 阻止对JCR的匿名访问 {#prevent-anonymous-access-on-jcr}

已知限制通过jcr内容和json向匿名访客公开社区网站内容，但是&#x200B;**允许匿名访问**&#x200B;对于网站内容禁用。 但是，可以使用Sling限制作为解决方法来控制此行为。

要保护您的社区站点内容免遭匿名用户通过jcr内容和json访问，请执行以下步骤：

1. 在AEM创作实例上，转到https:// hostname:port/editor.html/content/site/sitename.html。

   >[!NOTE]
   >
   >请勿转到本地化的站点。

1. 转到&#x200B;**Page Properties**。

   ![page-properties](assets/page-properties.png)

1. 转到&#x200B;**Advanced**&#x200B;选项卡。

1. 启用&#x200B;**身份验证要求**。

   ![网站验证](assets/site-authentication.png)

1. 添加登录页面的路径。 例如，**/content/......./GetStarted**。
1. 发布页面。

## 受信任的社区成员 {#trusted-community-member}

此体验假定[Aaron McDonald](/help/communities/tutorials.md#demo-users)被分配了[社区经理和审查方](/help/communities/create-site.md#roles)的角色。 如果没有，请返回创作环境以[修改站点设置](/help/communities/sites-console.md#modifying-site-properties)，然后选择Aaron McDonald作为社区经理和审查方。

在右上角，选择`Log in`，然后使用用户名(aaron.mcdonald@mailinator.com)和密码（密码）进行签名。 请注意使用Twitter或Facebook凭据登录的功能。

![登录](assets/login.png)

以注册的社区成员身份登录后，请注意以下菜单项，以单击并浏览您的社区站点：

* **** “配置文件”选项允许您查看和编辑配置文件。
* [](/help/communities/configure-messaging.md) 消息选项将引导您转到直接消息传送部分，在该部分中，您可以：

   1. 查看您收到的私信（收件箱）、发送的私信（已发送的邮件）和删除的私信（垃圾桶）。
   1. 撰写要发送给个人和群组的新私信。

* [](/help/communities/notifications.md) 通知选项将引导您转到通知部分，您可以在此处查看感兴趣的事件并编辑通知设置。
* [](/help/communities/published-site.md#moderationlink) 如果您拥有审核权限，则管理会将您引导至AEM Communities审核页面。

![adminscreen](assets/adminscreen.png)

请注意，日历页面是主页，因为所选的引用站点模板首先包含日历函数，然后是活动流函数、论坛函数等。 此结构可从[站点模板](/help/communities/sites.md#edit-site-template)控制台中查看，或在创作环境中修改站点属性时：

![站点模板](assets/sitetemplate.png)

>[!NOTE]
>
>有关社区组件和功能的更多信息，请访问：
>
>* [社区组件](/help/communities/author-communities.md) （供作者使用）
>* [组件、函数和功能要点](/help/communities/essentials.md) （适用于开发人员）


### 论坛链接 {#forum-link}

通过选择“论坛”链接，查看基本论坛功能。

成员可以发布新主题或关注主题。

网站访客能够查看帖子并以各种方式对其进行排序。

![forumlink](assets/forumlink.png)

### 群组链接 {#groups-link}

由于Aaron是群组管理员，因此选择群组链接将允许Aaron通过选择群组模板、图像（无论群组是开放还是保密）并邀请成员来创建新的社区群组。

例如，会在发布环境中创建群组。

组也可以在创作环境中创建并在创作环境的社区站点（[社区组控制台](/help/communities/groups.md)）中进行管理。 本教程的下一步是[在作者](/help/communities/nested-groups.md)上创建组的体验。

![groupling](assets/grouplink.png)

创建引用组：

1. 选择&#x200B;**新建组**
1. **“设置”选项卡**

   * 组名称 : `Sports`
   * 描述 : `A parent group for various sporting groups`.
   * 组 URL 名称 : `sports`
   * 选择`Open Group`（允许任何社区成员通过加入来参与）

1. **“模板”选项卡**

   * 选择`Reference Group`（在其结构中包含允许嵌套组的组函数）

1. 选择&#x200B;**创建组**

   ![creategroup](assets/creategroup.png)

创建新组后，**选择新的体育组**，以在其中创建两个组（嵌套）。 由于网站结构不能以组功能开头，因此在打开“体育”组后，需要选择“组”链接：

![grouplink1](assets/grouplink1.png)

第二组以`Blog`开头的链接属于当前选定的组`Sports`组。 通过选择“体育”`Groups`链接，可以在“体育”组中嵌套两个组。

例如，添加两个`new groups`。

* 一个名为`Baseball`

   * 将其保留设置为`Open Group`（必需的成员资格）。
   * 在“模板”选项卡上，选择`Conversational Group`。

* 一个名为`Gymnastics`

   * 将其设置更改为`Member Only Group`（成员资格受限）。
   * 在“模板”选项卡上，选择`Conversational Group`。

**通知**:

* 在显示两个组之前，可能需要刷新页面。
* 此模板&#x200B;*不*&#x200B;包含组函数，因此不可能进一步嵌套组。
* 在创作时， [组控制台](/help/communities/groups.md)提供了第三个选项 — `Public Group`（可选成员资格）。

创建两个组后，选择打开的组“棒球组”，并注意其链接：

`Discussions` `What's New` `Members`

群组的链接显示在主网站链接的下方，并会显示以下内容：

![grouplink2](assets/grouplink2.png)

在创作时 — 具有管理权限，导航到[社区组控制台](/help/communities/members.md)，并将Weston McCall添加到`Community Engage Gymnastics <uid> Members`组。

继续发布内容，以Aaron McDonald身份登录，并以匿名网站访客的身份查看体育组中的群组：

* 从主页
* 选择`Groups`链接
* 选择`Sports`链接
* 选择Sports&#39; `Groups`链接

只有棒球组可见。

以Weston McCall(weston.mccall@dodgit.com /密码)的身份登录，然后导航到同一位置。 请注意，Weston能够`Join`打开的`Baseball`组和`enter or Leave`专用`Gymnastics`组。

![grouplink3](assets/grouplink3.png)

### 网页链接 {#web-page-link}

通过选择网页链接查看网站中包含的基本网页。 标准AEM创作工具可用于在创作环境中向此页面添加内容。

例如，转到&#x200B;**author**&#x200B;实例，在[Communities Sites控制台](/help/communities/sites-console.md)中打开`engage`文件夹，选择&#x200B;**打开Site**&#x200B;图标以进入创作编辑模式。 然后选择预览模式以选择`Web Page`链接，然后选择编辑模式以添加标题和文本组件。 最后，只重新发布页面或整个网站。

![webpagelink](assets/webpagelink.png)

### 审核链接 {#moderationlink}

当社区成员拥有审核权限时，将显示“审核”链接，选择该链接后，将显示已发布的社区内容，并允许其以与创作环境中的[审核控制台](/help/communities/moderation.md)类似的方式[审核](/help/communities/moderate-ugc.md)。

使用浏览器的“返回”按钮返回到已发布的网站。 大多数控制台无法在发布环境中通过全局导航访问。

![审核链接](assets/moderationlink.png)

## 自注册 {#self-registration}

注销后，可以创建新用户注册。

* 选择 `Log In`
* 选择 `Sign up for a new account`

![注册](assets/registration.png)

![注册](assets/signup.png)

默认情况下，电子邮件地址为登录ID。 如果未选中，则访客可以输入自己的登录ID（用户名）。 在发布环境中，用户名必须唯一。

指定用户的名称、电子邮件和密码后，选择`Sign Up`将创建用户并允许他们进行签名。

登录后，显示的第一个页面是其`Profile`页面，它们可以对其进行个性化设置。

![配置文件](assets/profile.png)

如果成员忘记了其登录ID，则可以使用其电子邮件地址进行恢复。

![forgotusername](assets/forgotusername.png)
