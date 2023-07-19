---
title: 社区组控制台
seo-title: Community Groups Console
description: 群组控制台允许您创建社区群组
seo-description: Groups console lets you create Community groups
uuid: 21e2bde3-7354-4193-bcb3-c672c6342252
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d381ea40-fe49-4d32-bfad-1379c7a02aba
docset: aem65
pagetitle: Community Groups Console
role: Admin
exl-id: ef371ff8-6b4f-4e5a-98fb-d7c274927c46
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 2%

---

# 社区组控制台 {#community-groups-console}

“组”控制台提供在社区站点的 [模板结构](/help/communities/sites-console.md#step1) 包括 [组函数](/help/communities/functions.md#groups-function).

* AEM Communities支持在其他组内嵌套组。 在以下情况下，可以进行组嵌套 [新组的结构](/help/communities/tools-groups.md) 包含组函数。
* 仅对于创作环境，有一个与站点创建向导类似的组创建向导。
* 成员是否可以在发布环境中创建组，当向社区站点结构或社区组结构添加组功能时，可以对其进行配置。

在包括的三个组模板中，只有 `Reference Group` 模板的结构中包含组函数。

社区组的不同方面包括：

* **创建**：可以在创作实例上创建新组，也可以在发布实例上创建新组（可选）。
* **控制**：组可以是开放组或机密组。
* **嵌套**：组可以包含零个或多个组。

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.
-->

>[!NOTE]
>
>此组控制台只能从社区站点控制台访问，切勿与成员混淆 [组控制台](/help/communities/members.md) 用于管理成员组。
>
>成员组是在发布环境中注册的用户组，可使用从创作环境访问 [隧道服务](/help/communities/deploy-communities.md#tunnel-service-on-author).

## 组创建 {#group-creation}

要访问“组”控制台，请执行以下操作：

* 在作者中，使用管理员权限登录。
* 从全局导航： **[!UICONTROL Communities]** > **[!UICONTROL 站点]**.
* 选择现有社区站点文件夹以将其打开。
* 在文件夹中选择社区站点的实例。

   * 社区站点的结构必须包括分组功能。
   * 这些屏幕截图来自之后的快速入门教程 [在发布时创建组](/help/communities/published-site.md).

  ![create-group](assets/create-group.png)

* 选择 **组文件夹** 打开它。

  打开后，将显示所有现有组（无论是在创作中还是发布中创建）。

  通过此“组”控制台，可以创作新组。

  ![create-new-group](assets/create-new-group.png)

* 选择 **创建组** 按钮。

### 步骤1：社区组模板 {#step-community-group-template}

![多语言社区组](assets/multi-lingual-group.png)

* **社区组标题**

  组的显示标题。
标题会显示在组的已发布站点上。

* **社区组描述**

  组的描述。

* **社区组根路径**

  组的根路径。
默认根是父站点，但根可以移动到网站内的任何位置。 不建议更改此设置。

* **其他可用的社区组语言** 菜单

  使用下拉菜单选择可用的社区组语言。 该菜单显示创建父社区站点时采用的所有语言。 用户可以在这些语言中进行选择，以便通过此单一步骤在多个区域设置中创建组。 在相应社区站点的“组”控制台中，使用多种指定语言创建同一个组。

* **社区组名称**

  显示在URL中的组的根页面的名称。 避免在组名中使用下划线字符(_)和关键字（如资源和配置）。

   * 双击该名称，因为创建组后更改它并不容易。
   * 基本URL将显示在 `Community Group Name`.
   * 对于有效的URL，附加“.html”
     *例如*， `https://localhost:4502/content/sites/mysight/en/mygroup.html`.

* **社区组模板** 菜单

  使用下拉菜单选择一个可用的 [社区组模板](/help/communities/tools.md).

### 第2步：设计 {#step-design}

### 社区组主题 {#community-group-theme}

![社区组主题](assets/communitygrouptheme.png)

框架使用 `Twitter Bootstrap` 为站点提供响应式灵活设计。 可以选择多个预加载的Bootstrap主题之一来设置所选社区组模板的样式，或者可以上传Bootstrap主题。

选中后，主题将覆盖一个不透明的蓝色复选标记。

可以选择与父站点主题不同的主题。

在社区站点发布后，可以 [编辑属性](#modifyinggroupproperties) 并选择其他主题。

### 社区组品牌化 {#community-group-branding}

![社区组品牌化](assets/community-group-branding.png)

社区站点品牌推广是作为标题显示在每个页面顶部的图像。 可以显示与其他网站页面不同的组的横幅。

图像大小应设置为与页面在浏览器中的预期显示宽度一样宽，高度为120像素。

创建或选择图像时，请记住：

* 图像高度将裁剪为从图像的上边缘开始测量的120像素
* 图像已固定到浏览器窗口的左边缘
* 不调整图像大小，因此当图像宽度为：

   * 小于浏览器的宽度，图像将水平重复。
   * 大于浏览器的宽度，图像似乎将被裁剪。

### 步骤3：设置 {#step-settings}

**审核**

![选择社区组成员角色](assets/group-admin.png)

**社区组版主**

默认情况下，父社区站点的版主列表会被继承。

可以添加特定于组的审查方。 搜索成员（从发布环境）以将其添加为审查方

**组管理员**

默认情况下，父社区站点管理员也是组的管理员。

但是，可以分配独立的组管理员。 组管理员可以管理其组（例如G1），并创建一个嵌套在G1下的子组。 他们还可以为子组分配不同的管理员。

因此，用户U1可以是组G1的管理员，也可以是嵌套组G2的常规用户。

**会员资格**

成员资格设置允许从三种方式中选择一种来保护社区组。

![community-group-mbership](assets/community-group-membership.png)

* **可选成员资格**

  如果选择，则社区组为公共组。 站点成员可以参与组并发布帖子，而无需明确加入组。 默认处于选中状态。

* **必需成员资格**

  如果选择，则社区组为开放组。 社区站点成员可以查看组的内容，但需要加入组才能发布内容。 成员通过选择 `Join` 按钮。 未选择默认值。

* **受限制的成员资格**

  如果选中此项，则社区组是一个机密组。 必须明确邀请社区成员。 在搜索框中输入受邀成员。 稍后可以使用添加成员 [成员和组控制台](/help/communities/members.md) 创作环境。 未选择默认值。

**缩略图**

![community-group-thumbnail](assets/community-group-thumbnail.png)

缩略图是要在创作和发布时为组显示的图像。

对于支持的图像格式(如JPG或PNG)，组图像的最佳大小为170 x 90像素。

如果未添加图像，则显示默认图像。

![thumbnail-image](assets/thumbnail-image.png)

### 步骤4：创建组 {#step-create-group}

![community-create-group](assets/community-create-group.png)

如果需要任何调整，请使用 **返回** 按钮来制作它们。

一次 **创建** 选择并启动，则创建组的过程无法中断。

该过程完成后，新的子社区站点（组）的卡将显示在社区站点组控制台中，作者可以在其中添加页面内容，管理员可以修改站点的属性。

![创建社区组](assets/create-community-groups.png)

>[!NOTE]
>
>将按中指定的所有语言创建组 [步骤1：社区组模板](/help/communities/groups.md#step-community-group-template) 在其他可用的社区组语言中，位于各个社区站点的社区组控制台中。

## 作者组内容 {#author-group-content}

![open-site](assets/open-site.png)

可以使用与任何其他AEM页面相同的工具创作组的页面内容。 要打开组进行创作，请选择将鼠标悬停在组信息卡上时显示的“打开站点”图标。

## 修改组属性 {#modify-group-properties}

在社区组创建过程中指定的现有子社区站点的属性，可以通过选择将鼠标悬停在组信息卡上时显示的“编辑站点”图标进行修改：

![edit-site](assets/edit-site.png)

以下属性的详细信息与 [组创建](#group-creation) 部分。 可以修改任何嵌套组，无论是在发布环境还是创作环境中创建。

![community-group-basic](assets/community-group-basic.png)

### 修改基本 {#modify-basic}

BASIC面板允许修改

* 社区组标题
* 社区组描述

不能修改社区组名称。

选择其他社区组模板不会影响现有社区组站点，因为模板和站点之间没有连接。

相反， [结构](#modify-structure) 可以修改子社区的。

### 修改结构 {#modify-structure}

“结构”面板允许修改最初从作者或发布环境创建子社区站点时选择的社区组模板创建的结构。 在面板中，可以：

* 拖放其他 [社区功能](/help/communities/functions.md) 放入站点结构中。
* 在站点结构中的社区功能实例上：

   * **`Gear icon`**
编辑设置，包括显示标题、URL和 [拥有权限的成员组](/help/communities/users.md#privilegedmembersgroups).

   * **`Trashcan icon`**
从站点结构中移除（删除）函数。

   * **`Grid icon`**
修改网站顶级导航栏中显示的函数顺序。

>[!CAUTION]
>
>尽管显示标题可以更改且不会产生副作用，但建议不要编辑属于社区站点的社区函数的URL名称。
>
>例如，重命名URL将不会移动现有UGC，因此会导致“丢失”UGC。

>[!CAUTION]
>
>组函数必须 *非* 是 *第一个也不是唯一的* 在站点结构中的函数。
>
>任何其他函数，例如 [页面函数](/help/communities/functions.md#page-function)必须先包含并列出。

**示例：将日历函数添加到子社区（组）结构**

![community-group-add-calendar](assets/community-group-add-calendar.png)

### 修改设计 {#modify-design}

“设计”面板允许修改主题：

* [社区组主题](#community-group-theme)
* [社区组品牌](#community-group-branding)

   * 滚动到面板底部以更改品牌图像。

### 修改设置 {#modify-settings}

利用“设置”面板，可添加社区 [审查方](#moderation).

### 修改成员资格 {#modify-membership}

此 [会员资格](#membership) 面板仅用于提供信息。 无法更改已建立的组成员资格类型，无论它是可选的、必需的还是受限制的。

### 修改缩略图 {#modify-thumbnail}

此 [缩略图](#thumbnail) 通过面板，可以上传图像以向发布环境中的站点访客表示社区组，并在创作环境中的社区站点的“组”控制台中表示。

## 发布组 {#publish-the-group}

![publish-site](assets/publish-site.png)

新建或修改社区组后，可以通过选择 `Publish Site` 图标。

成功发布组后，将显示一条消息：

![已发布组](assets/group-published.png)

>[!CAUTION]
>
>父社区站点和父组应已发布。
>
>社区站点和嵌套组应以自上而下的方式发布。

## 删除组 {#delete-the-group}

![删除图标](assets/deleteicon.png)

通过选择“删除组”图标（将鼠标悬停在组上时出现），从社区“组”控制台中删除组。

这将删除与组关联的所有项目，例如，永久删除组的所有内容并从系统中删除用户成员资格。
