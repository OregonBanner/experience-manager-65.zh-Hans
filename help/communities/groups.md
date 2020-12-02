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
source-git-commit: 807a81045fca19ab83b9d7872684a5f8a9ed70f1
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 2%

---


# 社区组控制台{#community-groups-console}

当社区站点的[模板结构](/help/communities/sites-console.md#step1)包括[组函数](/help/communities/functions.md#groups-function)时，“组”控制台提供创建社区组的权限。

* AEM Communities支持在其他群体内嵌套群体。 当新组](/help/communities/tools-groups.md)的[结构包含组函数时，可以进行组嵌套。
* 仅对于作者环境，存在与站点创建向导类似的组创建向导。
* 在发布环境下，成员是否可以创建组，在将组功能添加到社区站点结构或社区组结构时，可以配置该组。

在包含的三个组模板中，只有`Reference Group`模板在其结构中包含组函数。

社区组的不同方面包括：

* **创建**:可以在作者上和发布实例上创建新组（可选）。
* **控制**:组可以是开放的或秘密的。
* **嵌套**:组可以包含零个或多个组。

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.
-->

>[!NOTE]
>
>此“组”控制台仅可从“社区站点”控制台访问，不要与成员[“组”控制台](/help/communities/members.md)混淆，以管理成员组。
>
>成员组是在发布环境中注册的用户组，使用[隧道服务](/help/communities/deploy-communities.md#tunnel-service-on-author)从作者环境访问。

## 组创建 {#group-creation}

要访问“组”控制台，请执行以下操作：

* 在创作时，使用管理员权限登录。
* 从全局导航：**[!UICONTROL 社区]** > **[!UICONTROL 站点]**。
* 选择现有社区站点文件夹以将其打开。
* 在文件夹内选择社区站点的实例。

   * 社区站点的结构必须包括组功能。
   * 这些屏幕快照来自[在发布](/help/communities/published-site.md)上创建组后的入门教程。

   ![创建组](assets/create-group.png)

* 选择&#x200B;**Groups文件夹**&#x200B;以将其打开。

   打开后，将显示所有现有组，无论是在作者创建还是发布创建。

   通过此“组”控制台，可以创作新组。

   ![create-new-group](assets/create-new-group.png)

* 选择&#x200B;**创建组**&#x200B;按钮。

### 第1步：社区组模板{#step-community-group-template}

![多语言社区组](assets/multi-lingual-group.png)

* **社区组标题**

   组的显示标题。
标题显示在组的已发布站点上。

* **社区组描述**

   组的描述。

* **社区组根路径**

   组的根路径。
默认根站点是父站点，但根站点可以移动到网站中的任意位置。 不建议更改它。

* **其他可用的社区组语言菜** 单

   使用下拉列表选择可用的社区组语言。 该菜单显示创建父社区站点时使用的所有语言。 用户可以在这些语言中进行选择，在此单步中创建多语言环境的用户组。 在相应社区站点的“组”控制台中以多种指定语言创建同一组。

* **社区组名称**

   组的根页面的名称，该页面显示在URL中。

   * 多次检查名称，因为创建组后该名称不易更改。
   * 基本URL将显示在`Community Group Name`下。
   * 对于有效的URL，附加“.html”
      *例如*, `https://localhost:4502/content/sites/mysight/en/mygroup.html`。

* **社区组模** 板菜单

   使用下拉框选择可用的[社区组模板](/help/communities/tools.md)。

### 第2步：设计{#step-design}

### 社区组主题{#community-group-theme}

![社区组主题](assets/communitygrouptheme.png)

该框架使用[TwitterBootstrap](https://twitterbootstrap.org/)为站点引入响应式、灵活的设计。 可以选择预加载的Bootstrap主题之一来设置所选社区组模板的样式，也可以上传Bootstrap主题。

选中后，主题将用不透明的蓝色复选标记覆盖。

可以选择与父站点的主题不同的主题。

发布社区站点后，可以[编辑属性](#modifyinggroupproperties)并选择其他主题。

### 社区组品牌{#community-group-branding}

![社区组品牌](assets/community-group-branding.png)

社区站点品牌是显示为每个页面顶部标题的图像。 可以显示组的横幅，该横幅不同于其他网站页面。

图像的大小应与浏览器中页面的预期显示大小相同，高度应为120像素。

创建或选择图像时，请牢记：

* 图像高度将从图像的上边缘裁剪为120像素
* 图像已固定到浏览器窗口的左边缘
* 图像不会调整大小，因此当图像宽度为：

   * 小于浏览器的宽度，图像将水平重复。
   * 图像的宽度大于浏览器的宽度后，图像将被裁剪。

### 第3步：设置{#step-settings}

**协调**

![选择社区组成员角色](assets/group-admin.png)

**社区组版主**

默认情况下，继承父社区站点的版主列表。

可以添加特定于组的版主。 搜索成员(从发布环境)以将其添加为版主

**组管理员**

默认情况下，父社区站点管理员也是组的管理员。

但是，可以分配独立的组管理员。 组管理员可以管理其组（例如G1），并创建嵌套在G1下的子组。 他们可以进一步为子组分配不同的管理员。

因此，用户U1可以是组G1中的管理员，也可以是其嵌套组G2中的常规用户。

**会员资格**

通过会员资格设置，可以选择三种保护社区组的方式之一。

![社区——组成员](assets/community-group-membership.png)

* **可选成员资格**

   如果选择，则社区组为公共组。 站点成员可以加入组并发布内容，而无需明确加入组。 选中默认值。

* **必需成员资格**

   如果选中，则社区组为打开的组。 社区站点成员可以视图组的内容，但需要加入组才能发布内容。 通过选择发布环境中的`Join`按钮加入成员。 未选择默认值。

* **受限制的成员资格**

   如果选中，则社区组是机密组。 必须明确邀请社区成员。 邀请的成员将输入搜索框中。 以后可以使用作者环境的[成员和组控制台](/help/communities/members.md)添加成员。 未选择默认值。

**缩略图**

![社区组缩略图](assets/community-group-thumbnail.png)

缩略图是创作和发布时组要显示的图像。

组图像的最佳大小是支持的图像格式（如JPG或PNG）的170 x 90像素。

如果未添加图像，则显示默认图像。

![缩略图](assets/thumbnail-image.png)

### 第4步：创建组{#step-create-group}

![社区创建组](assets/community-create-group.png)

如果需要调整，请使用&#x200B;**返回**&#x200B;按钮进行调整。

选择并启动&#x200B;**创建**&#x200B;后，创建组的过程将无法中断。

完成该过程后，新子社区站点（组）的卡片将显示在“社区站点组”控制台中，作者可以从该控制台添加页面内容，管理员也可以修改站点的属性。

![创建社区组](assets/create-community-groups.png)

>[!NOTE]
>
>按照[步骤1中的指定，组以所有语言创建：社区组模板](/help/communities/groups.md#step-community-group-template)，位于相应社区站点的“社区组”控制台中，其中包含其他可用社区组语言。

## 作者组内容{#author-group-content}

![开放站点](assets/open-site.png)

可以使用与任何其他AEM页面相同的工具创作组的页面内容。 要打开组进行创作，请选择将鼠标悬停在组卡上时显示的“打开站点”图标。

## 修改组属性{#modify-group-properties}

在社区组创建过程中指定的现有子社区站点的属性可以通过选择将鼠标悬停在组卡上时显示的“编辑站点”图标进行修改：

![edit-site](assets/edit-site.png)

以下属性的详细信息与[组创建](#group-creation)部分中提供的说明相符。 无论是在发布环境还是作者环境中创建，都可以修改任何嵌套组。

![社区组——基本](assets/community-group-basic.png)

### 修改基本{#modify-basic}

BASIC面板允许修改

* 社区组标题
* 社区组描述

不能修改社区组名称。

选择其他社区组模板不会影响现有社区组站点，因为模板和站点之间没有任何连接。

相反，可以修改子社区的[STRUCTURE](#modify-structure)。

### 修改结构{#modify-structure}

通过“结构”面板，可修改最初根据从作者或发布环境创建子社区站点时所选的社区组模板创建的结构。 在该面板中，可以：

* 将额外的[社区函数](/help/communities/functions.md)拖放到站点结构中。
* 在站点结构中社区功能的实例上：

   * **`Gear icon`**
编辑设置，包括显示标题、URL和特权 [成员组](/help/communities/users.md#privilegedmembersgroups)。

   * **`Trashcan icon`**
从站点结构中删除（删除）函数。

   * **`Grid icon`**
修改在站点的顶级导航栏中显示的功能顺序。

>[!CAUTION]
>
>虽然可以更改显示标题而不会产生副作用，但不建议编辑属于社区站点的社区功能的URL名称。
>
>例如，重命名URL不会移动现有UGC，因此具有“丢失”UGC的效果。

>[!CAUTION]
>
>组函数必须&#x200B;*不是*&#x200B;是&#x200B;*的第一个函数，也不是站点结构中唯一的*&#x200B;函数。
>
>必须首先包含并列出任何其他函数，如[页函数](/help/communities/functions.md#page-function)。

**示例：向子社区（组）结构添加日历功能**

![community-group-add-calendar](assets/community-group-add-calendar.png)

### 修改设计{#modify-design}

DESIGN面板允许修改主题：

* [社区组主题](#community-group-theme)
* [社区组品牌](#community-group-branding)

   * 滚动到面板底部以更改品牌图像。

### 修改设置{#modify-settings}

“设置”面板允许添加社区[版主](#moderation)。

### 修改成员资格{#modify-membership}

[MEMBERSHIP](#membership)面板仅供参考。 无论是可选的、必需的还是受限的，都无法更改已建立的组成员关系类型。

### 修改缩略图{#modify-thumbnail}

[THUMBNAIL](#thumbnail)面板允许上传图像，以将社区组表示到发布环境以及创作环境中社区站点的“组”控制台中的站点访客。

## 发布组{#publish-the-group}

![发布站点](assets/publish-site.png)

新建或修改社区组后，可以通过选择`Publish Site`图标来发布（激活）该组。

成功发布组后，将显示一条消息：

![组发布](assets/group-published.png)

>[!CAUTION]
>
>父社区站点和父组应已发布。
>
>社区站点和嵌套组应以自上而下的方式发布。

## 删除组{#delete-the-group}

![删除图标](assets/deleteicon.png)

通过选择“删除组”图标，从社区组控制台中删除组，该图标将鼠标悬停在组上方时显示。

这将删除与组关联的所有项目，例如，将永久删除组的所有内容，并从系统中删除用户成员资格。
