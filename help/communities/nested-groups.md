---
title: 创作嵌套群组
seo-title: Authoring Nested Groups
description: Create nested groups
seo-description: Create nested groups
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 4%

---

# Authoring Nested Groups{#authoring-nested-groups}

## Creating Groups on Author {#creating-groups-on-author}

在AEM创作实例上，从全局导航中：

* 选择 **[!UICONTROL 社区]** > **[!UICONTROL 站点]**.
* 选择 **[!UICONTROL 参与文件夹]** 打开它。
* 为 **[!UICONTROL 入门教程]** 英文网站。

   * 选择卡片图像。
   * 做 *not* 选择一个图标。

结果是达到 [“组”控制台](/help/communities/groups.md):

![创建组](assets/create-group.png)

组函数将显示为在其中创建组实例的文件夹。 选择Groups文件夹以将其打开。 将显示在发布时创建的组。

![create-new-group](assets/create-new-group.png)

## 创建主要艺术组 {#create-main-arts-group}

可以创建此组，因为参与的站点结构包含组功能。 站点的 `Reference Template` 默认为允许选择任何已启用的组模板。 Thus, the template chosen for this new group is the `Reference Group`.

这些控制台与“社区站点”控制台类似。

* 选择 **[!UICONTROL 创建群组]**

* **社区组模板**:

   * **[!UICONTROL 社区组标题]**:艺术
   * **[!UICONTROL 社区组描述]**:各种艺术团体的家长组
   * **[!UICONTROL 社区组根]**: *默认保留*
   * **[!UICONTROL Additional Available Community Group Language(s)]**: use the drop-down menu to select the available community group language(s). 该菜单显示创建父社区站点的所有语言。 用户可以在这些语言中进行选择，以在此单步中的多个区域设置中创建组。 在相应社区站点的“组”控制台中，会以多种指定语言创建同一组。
   * **[!UICONTROL 社区组名称]**:艺术
   * **[!UICONTROL 模板]**:下拉框选择 `Reference Group`
   * 选择 **[!UICONTROL 下一个]**

![嵌套社区组](assets/parent-to-nestedgroup.png)

使用这些设置继续浏览其他面板：

* **[!UICONTROL Design]**

   * 更改设计或允许默认父网站的设计。
   * 选择&#x200B;**[!UICONTROL 下一步]**。

* **[!UICONTROL 设置]**

   * **[!UICONTROL 审核]**

      * 将留空（从父站点继承）。
   * **[!UICONTROL 成员资格]**

      * Use default `Optional Membership.`

      * **[!UICONTROL 缩略图]**
         * `optional.*`
      * **[!UICONTROL 选择下一步]**。



* 选择&#x200B;**[!UICONTROL 创建]**。

### 艺术组中的嵌套组 {#nesting-groups-within-arts-group}

The `groups` folder now contains two groups (refresh the page).

![Nesting the groups](assets/create-community-group.png)

#### 发布组 {#publish-group}

在创建嵌套在 `arts` 群组中，将鼠标悬停在 `arts` 卡片上，然后选择“发布”图标以发布它。

![publish-site](assets/publish-site.png)

等待确认群组已发布。

![组发布](assets/group-published.png)

的 `arts` 组还应包含 `groups` 文件夹，但是空的，可在其中创建新群组的文件夹。 导航到艺术组文件夹并创建3个嵌套组，每个组具有不同的成员资格设置：

1. **[!UICONTROL 可视]**

   * 标题: `Visual Arts`
   * 名称: `visual`
   * 模板: `Reference Group`
   * 会员资格：选择 `Optional Membership`，公开给所有成员的群组。

1. **[!UICONTROL 听觉]**

   * 标题: `Auditory Arts`
   * 名称: `auditory`
   * 模板: `Reference Group`
   * 会员资格：选择 `Required Membership`，一个打开的组，可供成员加入。

1. **[!UICONTROL 历史]**

   * 标题: `Art History`
   * 名称: `history`
   * 模板: `Reference Group`
   * 会员资格：选择 `Restricted Membership`，秘密组，仅对受邀成员可见。 As an example, invite [demo user](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

刷新页面可查看所有三个嵌套群组（子社区）。

To navigate to the nested groups from the Communities Sites console:

* 选择 **[!UICONTROL 参与文件夹]**
* 选择 **[!UICONTROL 快速入门教程卡]**
* 选择 **[!UICONTROL 群组]** 文件夹
* 选择 **[!UICONTROL 艺术卡]**
* 选择 **[!UICONTROL 群组]** 文件夹

![create-new-group2](assets/create-new-group2.png)

## 发布组 {#publishing-groups}

![publish-site](assets/publish-site.png)

After publishing the main community site:

* 单独发布每个组：

   * 等待确认群组已发布。

* 在发布嵌套在中的所有组之前发布父组：

   * 所有群组都必须以自上而下的方式发布。

![组发布](assets/group-published.png)

## Experience on Publish {#experience-on-publish}

登录后，可能会体验不同的群组，例如使用 [演示用户](/help/communities/tutorials.md#demo-users) 用于：

* 艺术/历史组成员：emily.andrews@mailinator.com
   * 受限（秘密）组艺术/历史可见：
   * Can see optional (public) groups.
   * Can join restricted (open) groups.

* Group manager: aaron.mcdonald@mailinator.com/password

   * 可以查看可选（公共）群组。
   * Can join restricted (open) groups.
   * 看不到受限（密钥）组。

访问社区 [“成员”和“组”控制台](/help/communities/members.md) 创作时，将其他用户添加到与社区组对应的各个成员组。
