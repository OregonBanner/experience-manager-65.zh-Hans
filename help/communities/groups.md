---
title: 社区组控制台
seo-title: 社区组控制台
description: “组”控制台允许您创建社区组
seo-description: “组”控制台允许您创建社区组
uuid: 21e2bde3-7354-4193-bcb3-c672c6342252
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d381ea40-fe49-4d32-bfad-1379c7a02aba
docset: aem65
pagetitle: Community Groups Console
role: Administrator
exl-id: ef371ff8-6b4f-4e5a-98fb-d7c274927c46
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 2%

---

# 社区组控制台 {#community-groups-console}

当社区站点的[模板结构](/help/communities/sites-console.md#step1)包含[组函数](/help/communities/functions.md#groups-function)时，“组”控制台将提供创建社区组的访问权限。

* AEM Communities支持在其他组内嵌套组。 当新组](/help/communities/tools-groups.md)的[结构包含组函数时，可以进行组嵌套。
* 仅对于创作环境，有一个与站点创建向导类似的组创建向导。
* 无论（或不）成员是否可以在发布环境中创建组，在向社区站点结构或社区组结构添加组功能时，都可以对其进行配置。

在包含的三个组模板中，只有`Reference Group`模板的结构中包含组函数。

社区组的不同方面包括：

* **创建**:可以在创作时创建新群组，也可以（可选）在发布实例上创建新群组。
* **控制**:组可以是打开的，也可以是秘密的。
* **嵌套**:组可以包含零个或多个组。

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.
-->

>[!NOTE]
>
>此群组控制台只能从社区站点控制台访问，不要与成员[群组控制台](/help/communities/members.md)混淆，以管理成员群组。
>
>成员组是在发布环境中注册的用户组，使用[tunnel service](/help/communities/deploy-communities.md#tunnel-service-on-author)从创作环境访问。

## 组创建 {#group-creation}

要访问“组”控制台，请执行以下操作：

* 在创作时，使用管理员权限登录。
* 从全局导航：**[!UICONTROL Communities]** > **[!UICONTROL Sites]**。
* 选择现有社区站点文件夹以将其打开。
* 在文件夹中选择社区站点的实例。

   * 社区站点的结构必须包含组功能。
   * 这些屏幕截图来自[在publish](/help/communities/published-site.md)上创建组后的“快速入门”教程。

   ![创建组](assets/create-group.png)

* 选择&#x200B;**Groups文件夹**&#x200B;以将其打开。

   打开后，所有现有的组（无论是在创作时创建还是发布时创建）都会显示。

   从此“组”控制台中，可以创作新组。

   ![create-new-group](assets/create-new-group.png)

* 选择&#x200B;**创建组**&#x200B;按钮。

### 步骤1:社区组模板{#step-community-group-template}

![多语言社区组](assets/multi-lingual-group.png)

* **社区组标题**

   组的显示标题。
该标题会显示在群组的已发布网站上。

* **社区组描述**

   群组的描述。

* **社区组根路径**

   组的根路径。
默认的根是父站点，但可以将该根移动到网站中的任何位置。 不建议更改。

* **其他可用的社区组语言菜** 单

   使用下拉列表选择可用的社区组语言。 该菜单显示创建父社区站点的所有语言。 用户可以在这些语言中进行选择，以在此单步中的多个区域设置中创建组。 在相应社区站点的“组”控制台中，会以多种指定语言创建同一组。

* **社区组名称**

   在URL中显示的组根页面的名称。

   * 请仔细检查该名称，因为创建组后，该名称不容易更改。
   * 基本URL将显示在`Community Group Name`下。
   * 对于有效的URL，附加“.html”
      *例如*、  `https://localhost:4502/content/sites/mysight/en/mygroup.html`。

* **社区组模** 板菜单

   使用下拉菜单选择可用的[社区组模板](/help/communities/tools.md)。

### 步骤2:设计{#step-design}

### 社区组主题{#community-group-theme}

![社区组主题](assets/communitygrouptheme.png)

该框架使用[TwitterBootstrap](https://twitterbootstrap.org/)为网站引入响应式灵活设计。 可以选择许多预加载的Bootstrap主题之一来设置所选社区组模板的样式，也可以上传Bootstrap主题。

选择后，主题将被覆盖，并显示一个不透明的蓝色复选标记。

可以选择与父网站主题不同的主题。

社区网站发布后，可以[编辑属性](#modifyinggroupproperties)并选择其他主题。

### 社区团体品牌{#community-group-branding}

![社区团体品牌](assets/community-group-branding.png)

社区网站品牌化是在每个页面顶部显示为标题的图像。 可以显示与其他网站页面不同的群组的横幅。

图像的大小应与浏览器中页面的预期显示一样宽，高度应为120像素。

在创建或选择图像时，请记住：

* 图像高度将从图像的上边缘裁剪为120像素
* 图像已固定到浏览器窗口的左边缘
* 图像没有调整大小，因此当图像宽度为：

   * 小于浏览器的宽度，图像将水平重复。
   * 大于浏览器的宽度，图像将被裁剪。

### 步骤3:设置{#step-settings}

**审核**

![选择社区组成员角色](assets/group-admin.png)

**社区组版主**

默认情况下，会继承父社区站点的审核者列表。

可以添加特定于组的审核者。 搜索成员（从发布环境中）以将其添加为审核者

**组管理员**

默认情况下，父社区站点管理员也是群组的管理员。

但是，可以分配独立的组管理员。 群组管理员可以管理其群组（例如G1），并创建嵌套在G1下的子群组。 他们可以为子组进一步分配不同的管理员。

因此，用户U1可以是组G1中的管理员，也可以是其嵌套组G2中的常规用户。

**会员资格**

成员资格设置允许从三种方式中选择一种来保护社区组。

![社区 — 组成员](assets/community-group-membership.png)

* **可选成员资格**

   如果选择，则社区组为公共组。 站点成员无需明确加入组即可参与组和帖子发布。 已选中默认值。

* **必需成员资格**

   如果选择，则社区组为打开的组。 社区站点成员可以查看组的内容，但需要加入组才能发布内容。 通过选择发布环境中的`Join`按钮来加入成员。 未选择默认值。

* **受限制的成员资格**

   如果选中，则社区组为密钥组。 必须明确邀请社区成员。 将在搜索框中输入受邀成员。 稍后可以使用创作环境的[成员和组控制台](/help/communities/members.md)添加成员。 未选择默认值。

**缩略图**

![社区组缩览图](assets/community-group-thumbnail.png)

缩略图是在创作和发布时针对组显示的图像。

组图像的最佳大小为170 x 90像素，采用支持的图像格式（如JPG或PNG）。

如果未添加图像，则会显示默认图像。

![缩略图图像](assets/thumbnail-image.png)

### 步骤4:创建组{#step-create-group}

![社区创建组](assets/community-create-group.png)

如果需要进行任何调整，请使用&#x200B;**Back**&#x200B;按钮进行调整。

选择并启动&#x200B;**创建**&#x200B;后，创建组的过程将无法中断。

完成该过程后，新子社区站点（组）的卡片将显示在社区站点组控制台中，作者可以在此控制台中添加页面内容，或者管理员可以修改站点的属性。

![创建社区组](assets/create-community-groups.png)

>[!NOTE]
>
>该组以所有语言创建，如[步骤1中指定：在相应社区站点的“社区组”控制台中，使用其他可用社区组语言的社区组模板](/help/communities/groups.md#step-community-group-template)。

## 创作组内容{#author-group-content}

![开放站点](assets/open-site.png)

可使用与任何其他AEM页面相同的工具创作群组的页面内容。 要打开组进行创作，请选择将鼠标悬停在组卡片上时显示的打开站点图标。

## 修改组属性{#modify-group-properties}

在社区组创建过程中指定的现有子社区站点的属性可以通过选择编辑站点图标来修改，该图标将鼠标悬停在群组卡片上时会显示：

![编辑站点](assets/edit-site.png)

以下属性的详细信息与[组创建](#group-creation)部分中提供的描述匹配。 无论是在发布环境还是创作环境中创建，都可以修改任何嵌套群组。

![社区群 — 基本](assets/community-group-basic.png)

### 修改基本{#modify-basic}

基本面板允许修改

* 社区组标题
* 社区组描述

不能修改社区组名称。

选择其他社区组模板对现有社区组站点不会产生任何影响，因为模板和站点之间没有任何连接。

可以修改子社区的[STRUCTURE](#modify-structure)。

### 修改结构{#modify-structure}

“结构”面板允许修改最初从从创作或发布环境创建子社区站点时所选的社区组模板创建的结构。 在面板中，可以：

* 将其他[社区函数](/help/communities/functions.md)拖放到站点结构中。
* 在站点结构中社区功能的实例上：

   * **`Gear icon`**
编辑设置，包括显示标题、URL和特权 [成员组](/help/communities/users.md#privilegedmembersgroups)。

   * **`Trashcan icon`**
从站点结构中删除（删除）函数。

   * **`Grid icon`**
修改功能在网站顶级导航栏中显示的顺序。

>[!CAUTION]
>
>虽然显示标题可以更改而不会产生副作用，但不建议编辑属于社区站点的社区函数的URL名称。
>
>例如，重命名URL不会移动现有UGC，因此会产生“丢失”UGC的效果。

>[!CAUTION]
>
>组函数必须&#x200B;*不*&#x200B;是站点结构中的&#x200B;*第一个函数，也不是唯一的*&#x200B;函数。
>
>必须先包含并列出任何其他函数，如[page函数](/help/communities/functions.md#page-function)。

**示例：向子社区（组）结构添加日历功能**

![社区组添加日历](assets/community-group-add-calendar.png)

### 修改设计{#modify-design}

“设计”面板允许修改主题：

* [社区组主题](#community-group-theme)
* [社区组品牌](#community-group-branding)

   * 滚动到面板底部以更改品牌图像。

### 修改设置{#modify-settings}

“设置”面板允许添加社区[审核者](#moderation)。

### 修改成员资格{#modify-membership}

[MEMBERSHIP](#membership)面板仅供参考。 无论是可选的、必需的还是受限的，都无法更改已建立的组成员资格类型。

### 修改缩略图{#modify-thumbnail}

通过[THUMBNAIL](#thumbnail)面板，可以上传图像，以在发布环境以及创作环境的社区站点的“组”控制台中将社区组表示给站点访客。

## 发布组{#publish-the-group}

![publish-site](assets/publish-site.png)

新建或修改社区组后，可以通过选择`Publish Site`图标来发布（激活）该组。

成功发布群组后，将显示一条消息：

![组发布](assets/group-published.png)

>[!CAUTION]
>
>父社区站点和父组应已发布。
>
>社区网站和嵌套群组应以自上而下的方式发布。

## 删除组{#delete-the-group}

![删除图标](assets/deleteicon.png)

通过选择删除组图标（将鼠标悬停在群组上方时显示），从社区组控制台中删除群组。

这会删除与组关联的所有项目，例如，组的所有内容都将被永久删除，用户成员资格也将从系统中删除。
