---
title: 创作嵌套组
seo-title: 创作嵌套组
description: 创建嵌套用户组
seo-description: 创建嵌套用户组
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
translation-type: tm+mt
source-git-commit: 5d196d1f6d5f94f2d3ef0d4461cfe38562f8ba8c
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 4%

---


# 创作嵌套组{#authoring-nested-groups}

## 在作者上创建组{#creating-groups-on-author}

在AEM作者实例上，从全局导航：

* 选择&#x200B;**[!UICONTROL 社区]** > **[!UICONTROL 站点]**。
* 选择&#x200B;**[!UICONTROL Engage文件夹]**&#x200B;将其打开。
* 为&#x200B;**[!UICONTROL Getting Started Tutorial]**&#x200B;英语站点选择卡。

   * 选择卡图像。
   * *不*&#x200B;选择一个图标。

结果是到达[组控制台](/help/communities/groups.md):

![创建组](assets/create-group.png)

组函数将显示为创建组实例的文件夹。 选择要打开的组文件夹。 将显示在发布时创建的组。

![create-new-group](assets/create-new-group.png)

## 创建主要艺术组{#create-main-arts-group}

可以创建此组，因为参与的站点结构包含组功能。 站点`Reference Template`中的函数配置默认为允许选择任何已启用的组模板。 因此，为此新组选择的模板是`Reference Group`。

这些控制台与“社区站点”控制台类似。

* 选择&#x200B;**[!UICONTROL 创建组]**。

* **社区组模板**:

   * **[!UICONTROL 社区组标题]**:艺术。
   * **[!UICONTROL 社区组描述]**:不同艺术组的父组。
   * **[!UICONTROL 社区组根]**: *保留为默认值*。
   * **[!UICONTROL 其他可用的社区组语言]**:使用下拉菜单选择可用的社区组语言。该菜单显示创建父社区站点时使用的所有语言。 用户可以在这些语言中进行选择，在此单步中创建多语言环境的用户组。 在相应社区站点的“组”控制台中以多种指定语言创建同一组。
   * **[!UICONTROL 社区组名称]**:艺术。
   * **[!UICONTROL 模板]**:下拉列表选择  `Reference Group.`
   * 选择&#x200B;**[!UICONTROL 下一步]**。

![嵌套社区组](assets/parent-to-nestedgroup.png)

使用以下设置继续浏览其他面板：

* **[!UICONTROL 设计]**

   * 更改设计或允许默认父站点的设计。
   * 选择&#x200B;**[!UICONTROL 下一步]**。

* **[!UICONTROL 设置]**

   * **[!UICONTROL 审核]**

      * 留空（继承父站点）。
   * **[!UICONTROL 成员资格]**

      * 使用默认值`Optional Membership.`

      * **[!UICONTROL 缩略图]**
         * `optional.*`
      * **[!UICONTROL 选择下一步]**。



* 选择&#x200B;**[!UICONTROL 创建]**。

### 艺术组{#nesting-groups-within-arts-group}中的嵌套组

`groups`文件夹现在包含两个用户组（刷新页面）。

![嵌套组](assets/create-community-group.png)

#### 发布组 {#publish-group}

在创建嵌套在`arts`组中的组之前，请将指针悬停在`arts`卡上，然后选择发布图标进行发布。

![发布站点](assets/publish-site.png)

等待确认组已发布。

![组发布](assets/group-published.png)

`arts`组还应包含`groups`文件夹，但该文件夹为空，可在其中创建新组。 导航到艺术组文件夹并创建3个嵌套用户组，每个用户组具有不同的成员资格设置：

1. **[!UICONTROL 可视]**

   * 标题: `Visual Arts`
   * 名称: `visual`
   * 模板: `Reference Group`
   * 会员资格：选择`Optional Membership`（公共组），打开给所有成员。

1. **[!UICONTROL 听觉]**

   * 标题: `Auditory Arts`
   * 名称: `auditory`
   * 模板: `Reference Group`
   * 会员资格：选择`Required Membership`，一个可供成员加入的打开的组。

1. **[!UICONTROL 历史]**

   * 标题: `Art History`
   * 名称: `history`
   * 模板: `Reference Group`
   * 会员资格：选择`Restricted Membership`，一个秘密组，仅对受邀成员可见。 例如，邀请[演示用户](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`。

刷新页面以查看所有三个嵌套组（子社区）。

要从“社区站点”控制台导航到嵌套组，请执行以下操作：

* 选择&#x200B;**[!UICONTROL Engage folder]**
* 选择&#x200B;**[!UICONTROL 教程入门卡]**
* 选择&#x200B;**[!UICONTROL 组]**&#x200B;文件夹
* 选择&#x200B;**[!UICONTROL 艺术卡]**
* 选择&#x200B;**[!UICONTROL 组]**&#x200B;文件夹

![create-new-group2](assets/create-new-group2.png)

## 发布组{#publishing-groups}

![发布站点](assets/publish-site.png)

发布主社区站点后：

* 单独发布每个组：

   * 正在等待确认组已发布。

* 在发布嵌套在以下对象中的所有组之前，先发布父组：

   * 所有组都必须以自上而下的方式发布。

![组发布](assets/group-published.png)

## 发布体验{#experience-on-publish}

登录时，可以体验不同的组，例如，使用[demo用户](/help/communities/tutorials.md#demo-users)进行登录：

* 图稿／历史记录组成员：emily.andrews@mailinator.com
   * 受限（秘密）组艺术／历史可见：
   * 可以查看可选（公共）组。
   * 可以加入受限（打开）组。

* 组管理器：aaron.mcdonald@mailinator.com

   * 可以查看可选（公共）组。
   * 可以加入受限（打开）组。
   * 无法看到受限（机密）组。

访问作者的“社区[成员和组”控制台](/help/communities/members.md)，将其他用户添加到与社区组对应的各种成员组。

