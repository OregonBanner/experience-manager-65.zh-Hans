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
translation-type: tm+mt
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# 社区组控制台 {#community-groups-console}

当社区站点的模板结构包括组功能时，“组”控制台 [提供了创建社](/help/communities/sites-console.md#step1) 区 [组的权限](/help/communities/functions.md#groups-function)。

* AEM Communities支持在其他组内嵌套组。 当新组的结构包含 [组函数时](/help/communities/tools-groups.md) ，可进行组嵌套。
* 仅对于作者环境，存在一个与站点创建向导类似的组创建向导。
* 在向社区站点结构或社区组结构添加“组”功能时，成员是否可以在发布环境中创建组，可对其进行配置。

在包含的三个用户组模板中，只有该模 `Reference Group` 板在其结构中包含用户组功能。

社区组的不同方面包括：

* **创建**:可以在作者上和发布实例上（可选）创建新组。
* **控制**:组可以是开放的或秘密的。
* **嵌套**:组可以包含零个或多个组。

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.-->

>[!NOTE]
>
>此“组”控制台仅可从“社区站点”控制台访问，不要与用于管理成员组的“成 [员组”控制台相混淆](/help/communities/members.md) 。
>
>成员组是在发布环境中注册的用户组，使用隧道服务从创作环境访 [问它们](/help/communities/deploy-communities.md#tunnel-service-on-author)。


## 组创建 {#group-creation}

要访问“组”控制台，请执行以下操作：

* 在创作时，使用管理员权限登录。
* 从全局导航：“ **[!UICONTROL 社区]** ”>“ **[!UICONTROL 站点”]**。
* 选择现有社区站点文件夹以将其打开。
* 在文件夹中选择社区站点的实例。

   * 社区站点的结构必须包括组功能。
   * 这些屏幕快照来自发布时创建组 [后的入门教程](/help/communities/published-site.md)。

* 选择“ **组”文件夹** ，以将其打开。

   打开后，将显示所有现有用户组（无论是在创作时创建还是发布时创建）。

   通过此“组”控制台，可以创作新组。

   ![chlimage_1-200](assets/chlimage_1-200.png)

* 选择“ **创建组** ”按钮。

### 第1步：社区组模板 {#step-community-group-template}

![多语言社区组](assets/multi-lingual-group.png)

* **社区组标题**

   组的显示标题。
标题显示在组的已发布站点上。

* **社区组描述**

   用户组的说明。

* **社区组根路径**

   组的根路径。
默认的根是父站点，但根可以移到网站中的任意位置。 建议不要更改它。

* **其他可用的社区组语言菜单**

   使用下拉列表选择可用的社区组语言。 该菜单显示创建父社区站点时所用的所有语言。 用户可以在这些语言中进行选择，以在此单步中创建多个区域设置的用户组。 在相应社区站点的“组”控制台中，以多种指定语言创建同一组。

* **社区组名称**

   URL中显示的组根页面的名称。

   * 多次检查名称，因为创建组后该名称不易更改。
   * 基本URL将显示在下方 `Community Group Name`。
   * 对于有效的URL，请附加“.html”
      *例如*, `https://localhost:4502/content/sites/mysight/en/mygroup.html`。

* **“社区组模板** ”菜单

   使用下拉列表选择可用的社 [区组模板](/help/communities/tools.md)。

### 第2步：设计 {#step-design}

### COMMUNITY GROUP THEME {#community-group-theme}

该框架使 [用Twitter Bootstrap](https://twitterbootstrap.org/) ，为网站提供响应迅速、灵活的设计。 可以选择多个预先加载的Bootstrap主题之一来设置所选社区组模板的样式，也可以上传Bootstrap主题。

选择后，主题将用不透明的蓝色复选标记覆盖。

可以选择与父站点的主题不同的主题。

发布社区站点后，可以编辑属性 [并选择其](#modifyinggroupproperties) 他主题。

### COMMUNITY GROUP BRANDING {#community-group-branding}

![chlimage_1-201](assets/chlimage_1-201.png)

社区站点品牌是显示为每个页面顶部标题的图像。 可以显示与其他站点页面不同的组的横幅。

图像的大小应与浏览器中页面的预期显示大小相同，高度应为120像素。

创建或选择图像时，请牢记：

* 图像高度将从图像的上边缘裁切为120像素
* 图像被固定到浏览器窗口的左边缘
* 图像不会调整大小，因此当图像宽度为：

   * 小于浏览器的宽度，图像将水平重复。
   * 大于浏览器的宽度后，图像将看起来会被裁掉。

### 第3步：设置 {#step-settings}

**协调**

![选择社区组成员角色](assets/group-admin.png)

**社区组版主**

默认情况下，父社区站点的版主列表是继承的。

可以添加特定于组的审核者。 搜索成员(从发布环境中)以将其添加为版主

**组管理员**

默认情况下，父社区站点管理员也是组的管理员。

但是，可以分配独立的组管理员。 组管理员可以管理其组（例如G1），并创建嵌套在G1下的子组。 他们可以进一步为子组分配不同的管理员。

因此，用户U1可以是组G1中的管理员，也可以是其嵌套组G2中的常规用户。

**会员资格**

通过会员资格设置，可以选择三种方式之一来保护社区组。

![chlimage_1-202](assets/chlimage_1-202.png)

* **可选成员资格**

   如果选择此选项，则社区组为公共组。 站点成员可以加入组并发布内容，而无需明确加入组。 默认为选中状态。

* **必需成员资格**

   如果选择此选项，则社区组为打开的组。 社区站点成员可以视图组的内容，但需要加入组才能发布内容。 通过选择发布环境 `Join` 中的按钮加入成员。 未选择默认值。

* **受限制的成员资格**

   如果选择此选项，则社区组为机密组。 必须明确邀请社区成员。 已邀请的成员将在搜索框中输入。 以后可以使用作者环境的“成员 [”和“组”控制台](/help/communities/members.md) ，添加成员。 未选择默认值。

**缩略图**

![chlimage_1-203](assets/chlimage_1-203.png)

缩略图是创作和发布时要为组显示的图像。

组图像的最佳大小是支持的图像格式（如JPG或PNG）的170 x 90像素。

如果未添加图像，则显示默认图像。

![chlimage_1-204](assets/chlimage_1-204.png)

### 第4步：创建组 {#step-create-group}

![chlimage_1-205](assets/chlimage_1-205.png)

如果需要进行任何调整，请使用“返回”按钮进行调整。

选 **择并启动** “创建”后，创建组的过程将无法中断。

完成该过程后，新的子社区站点（组）的卡片将显示在“社区站点组”控制台中，作者可以从中添加页面内容，或管理员可以修改站点的属性。

![创建社区组](assets/create-community-groups.png)

>[!NOTE]
>
>按照第1步中的指定，用户组将以所有语言 [创建：社区组模板](/help/communities/groups.md#step-community-group-template) ，位于各个社区站点的“社区组”控制台中，使用其他可用的社区组语言。


## 作者组内容 {#author-group-content}

![chlimage_1-206](assets/chlimage_1-206.png)

可以使用与任何其他AEM页面相同的工具创作组的页面内容。 要打开创作组，请选择将鼠标悬停在组卡上时显示的“打开站点”图标。

## 修改组属性 {#modify-group-properties}

在社区组创建过程中指定的现有子社区站点的属性可以通过选择将鼠标悬停在组卡上时显示的编辑站点图标进行修改：

![chlimage_1-207](assets/chlimage_1-207.png)

以下属性的详细信息与“组创建”部分中提供 [的说明相符](#group-creation) 。 无论是在发布环境还是作者环境中创建，都可以修改任何嵌套组。

![chlimage_1-208](assets/chlimage_1-208.png)

### 修改基本 {#modify-basic}

BASIC面板允许修改

* 社区组标题
* 社区组描述

不能修改社区组名称。

选择其他社区组模板不会影响现有的社区组站点，因为模板和站点之间没有连接。

相反，可 [以修改](#modify-structure) 子社区的STRUCTURE。

### 修改结构 {#modify-structure}

通过“结构”面板，可以修改最初根据从作者或发布环境创建子社区站点时选择的社区组模板创建的结构。 从面板中，可以：

* 将其他社区功能拖 [放到站点结](/help/communities/functions.md) 构中。
* 在站点结构中社区功能的实例上：

   * **`Gear icon`**
编辑设置，包括显示标题和URL名称*以及特权 [成员组](/help/communities/users.md#privilegedmembersgroups)。

   * **`Trashcan icon`**
从站点结构中删除（删除）功能。

   * **`Grid icon`**
修改站点顶级导航栏中显示的功能顺序。

>[!CAUTION]
>
>虽然显示标题可以在不产生副作用的情况下进行更改，但不建议编辑属于社区站点的社区功能的URL名称。
>
>例如，重命名URL不会移动现有UGC，因此具有“丢失”UGC的效果。


>[!CAUTION]
>
>组函数不能*是站点结构 *中的第一个* ，也不能是唯一的函数。
>
>必须首先包含并列出任何其 [他函数](/help/communities/functions.md#page-function)，如页面函数。


**示例：向子社区（组）结构添加日历功能**

![chlimage_1-209](assets/chlimage_1-209.png)

### 修改设计 {#modify-design}

“设计”面板允许修改主题：

* [社区组主题](#community-group-theme)
* [社区组品牌](#community-group-branding)

   * 滚动到面板底部以更改品牌图像。

### 修改设置 {#modify-settings}

通过“设置”面板，可以添加社区版主 [者](#moderation)。

### 修改会员资格 {#modify-membership}

MEMBERSHIP [面板](#membership) (MEMBERSHIP panel)仅供参考。 无论是可选的、必需的还是受限的，都无法更改已建立的组成员关系类型。

### 修改缩略图 {#modify-thumbnail}

通过 [THUMBNAIL](#thumbnail) 面板，可以上传图像，以将社区组表示到发布环境中的站点访客以及创作环境中的社区站点的“组”控制台中。

## 发布组 {#publish-the-group}

![chlimage_1-210](assets/chlimage_1-210.png)

在新创建或修改社区组后，可以通过选择图标发布（激活）该 `Publish Site` 组。

成功发布组后，将显示一条消息：

![chlimage_1-211](assets/chlimage_1-211.png)

>[!CAUTION]
>
>父社区站点和父组应已发布。
>
>社区站点和嵌套组应以自上而下的方式发布。


## 删除组 {#delete-the-group}

![删除图标]()

通过选择“删除组”图标，从社区组控制台中删除组，该图标将鼠标悬停在组上时显示。

这将删除与组关联的所有项目，例如，将永久删除组的所有内容，并从系统中删除用户成员关系。
