---
title: 创作嵌套组
description: 了解如何为Adobe Experience Manager Communities站点创建嵌套组。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 4%

---

# 创作嵌套组{#authoring-nested-groups}

## 创建创作组 {#creating-groups-on-author}

在AEM创作实例上，从全局导航：

* 选择 **[!UICONTROL Communities]** > **[!UICONTROL 站点]**.
* 选择 **[!UICONTROL engage文件夹]** 打开它。
* 选择卡 **[!UICONTROL 快速入门教程]** 英文网站。

   * 选择卡片图像。
   * Do *非* 选择一个图标。

结果是达到 [群组控制台](/help/communities/groups.md)：

![create-group](assets/create-group.png)

“组”功能将显示为文件夹，可在其中创建组的实例。 要打开该文件夹，请选择“组”文件夹。 发布时创建的组可见。

![create-new-group](assets/create-new-group.png)

## 创建主艺术组 {#create-main-arts-group}

可以创建此组，因为用于接合的站点结构包括组的功能。 站点中函数的配置 `Reference Template` 默认为允许选择任何已启用的组模板。 因此，为新组选择的模板是 `Reference Group`.

这些控制台与社区站点控制台类似。

* 选择 **[!UICONTROL 创建组]**

* **社区组模板**:

   * **[!UICONTROL 社区组标题]**：艺术
   * **[!UICONTROL 社区组描述]**：各种艺术团体的父组
   * **[!UICONTROL 社区组根目录]**： *保留为默认值*
   * **[!UICONTROL 其他可用的社区组语言]**：使用下拉菜单选择可用的社区组语言。 该菜单显示创建父社区站点时采用的所有语言。 用户可以在这些语言中进行选择，以便通过此单一步骤在多个区域设置中创建组。 在相应社区站点的“组”控制台中，以多种指定语言创建同一组。
   * **[!UICONTROL 社区组名称]**：艺术
   * **[!UICONTROL 模板]**：用于选择的下拉列表 `Reference Group`
   * 选择 **[!UICONTROL 下一个]**

![嵌套社区组](assets/parent-to-nestedgroup.png)

使用这些设置继续浏览其他面板：

* **[!UICONTROL Design]**

   * 更改设计或允许默认父站点的设计。
   * 选择&#x200B;**[!UICONTROL 下一步]**。

* **[!UICONTROL 设置]**

   * **[!UICONTROL 审核]**

      * 留空（继承自父站点）。

   * **[!UICONTROL 成员资格]**

      * 使用默认值 `Optional Membership.`

      * **[!UICONTROL 缩略图]**
         * `optional.*`

      * **[!UICONTROL 选择下一步]**。

* 选择&#x200B;**[!UICONTROL 创建]**。

### 艺术组内的嵌套组 {#nesting-groups-within-arts-group}

此 `groups` 文件夹现在包含两个组（刷新页面）。

![嵌套组](assets/create-community-group.png)

#### 发布组 {#publish-group}

在创建嵌套在 `arts` 组，将鼠标悬停在 `arts` 信息卡并选择“发布”图标以进行发布。

![publish-site](assets/publish-site.png)

等待确认该组已发布。

![已发布组](assets/group-published.png)

此 `arts` 组还应包含 `groups` 文件夹，但为空的文件夹，可在其中创建新组。 导航到艺术组文件夹并创建三个嵌套的艺术组，每个艺术组具有不同的成员资格设置：

1. **[!UICONTROL 可视化]**

   * 标题: `Visual Arts`
   * 名称：`visual`
   * 模板: `Reference Group`
   * 成员资格：选择 `Optional Membership`，一个公共组，对所有成员开放。

1. **[!UICONTROL 听觉]**

   * 标题: `Auditory Arts`
   * 名称：`auditory`
   * 模板: `Reference Group`
   * 成员资格：选择 `Required Membership`，开放组，可供成员加入。

1. **[!UICONTROL 历史]**

   * 标题: `Art History`
   * 名称：`history`
   * 模板: `Reference Group`
   * 成员资格：选择 `Restricted Membership`，一个机密组，仅对受邀成员可见。 例如，邀请 [演示用户](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

刷新页面，以便您能够查看所有三个嵌套的组（子社区）。

要从社区站点控制台导航到嵌套组，请执行以下操作：

* 选择 **[!UICONTROL engage文件夹]**
* 选择 **[!UICONTROL 快速入门教程信息卡]**
* 选择 **[!UICONTROL 组]** 文件夹
* 选择 **[!UICONTROL 艺术卡]**
* 选择 **[!UICONTROL 组]** 文件夹

![create-new-group2](assets/create-new-group2.png)

## 发布组 {#publishing-groups}

![publish-site](assets/publish-site.png)

发布主社区站点后：

* 单独发布每个组：

   * 正在等待确认该组已发布。

* 发布父组后再发布嵌套在以下内容中的任何组：

   * 必须以自上而下的方式发布所有组。

![已发布组](assets/group-published.png)

## 发布体验 {#experience-on-publish}

在登录时可能会体验不同的组，例如，使用 [演示用户](/help/communities/tutorials.md#demo-users) 用于：

* 艺术/历史组成员： `emily.andrews@mailinator.com/password`
   * 受限（机密）组“艺术/历史”可见：
   * 能够查看可选（公共）组。
   * 能够加入受限（开放）组。

* 组管理器： `aaron.mcdonald@mailinator.com/password`

   * 能够查看可选（公共）组。
   * 能够加入受限（开放）组。
   * 无法查看受限（机密）组。

访问社区 [成员和组控制台](/help/communities/members.md) 对作者，将其他用户添加到与社区组对应的各种成员组。
