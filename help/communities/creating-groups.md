---
title: 社区组
seo-title: 社区组
description: 创建社区组
seo-description: 创建社区组
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
translation-type: tm+mt
source-git-commit: 6337a57ea12f1e026f6c754a083307ce018a1c13
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---


# 社区组 {#community-groups}

社区组功能是允许通过发布和作者环境授权用户（社区成员和作者）在社区站点内动态创建子社区的功能。

当[社区站点](/help/communities/sites-console.md)结构中存在[组函数](/help/communities/functions.md#groups-function)时，存在此功能。

当动态创建社区组时，[社区组模板](/help/communities/tools-groups.md)提供社区组页面的设计。

当该功能被添加到社区站点的结构或社区站点模板时，为该组功能选择一个或多个组模板。 此组模板列表将呈现给从社区站点动态创建新组的成员或作者。

## 创建新组{#creating-a-new-group}

创建新社区组的能力取决于是否存在包含组功能的社区站点，如从[参考站点模板](/help/communities/sites.md)创建的社区站点。

下面的示例使用从`Reference Site Template`创建的社区站点，如[AEM Communities](/help/communities/getting-started.md)入门教程中所述。

选择&#x200B;**组**&#x200B;菜单项时，此页面在发布时加载：

![新组](assets/new-group.png)

选择&#x200B;**新建组**&#x200B;图标时，将打开一个编辑对话框。

在&#x200B;**设置**&#x200B;选项卡下，您提供组的基本功能：

![组设置](assets/group-settings.png)

* **组名称**

   要在社区站点上显示的组的标题。

* **描述**

   要在社区站点上显示的组的描述。

* **邀请**

   邀请加入组的成员列表。 预先键入搜索将提供社区成员邀请的建议。

* **组 URL 名称**

   成为URL一部分的组页面的名称。

* **开放组**

   选择`Open Group`表示任何匿名站点访客都可以视图内容，并将取消选择`Member Only Group`。

* **仅限成员加入的组**

   选择`Member Only Group`表示只有组成员可以视图内容，并将取消选择`Open Group`。

在&#x200B;**模板**选项卡下，可以
从社区组模板的列表中进行选择，这些模板是在将组功能包括在社区站点的结构或社区站点模板中时指定的。

![组模板](assets/group-template.png)

在&#x200B;**图像**&#x200B;选项卡下，可以上传图像，以便在社区站点的“组”页上显示组。 默认样式表将图像大小调整为170 x 90像素。

![组图像](assets/group-image.png)

通过选择&#x200B;**创建组**&#x200B;按钮，将根据所选模板创建组的页面，并为成员创建用户组，并且将更新“组”页面以显示新的子社区。

例如，带有标题为“焦点组”的新子社区的“组”页面（已为其上传图像缩略图）将显示如下（仍以社区组管理员身份登录）:

![组页](assets/group-page.png)

选择`Focus Group`链接将打开浏览器中的“焦点组”页面，该页面具有基于所选模板的初始外观，并在主社区站点的菜单下包含一个子菜单：

![open-group-page](assets/open-group-page.png)

### 社区组成员列表组件{#community-group-member-list-component}

`Community Group Member List`组件供组模板的开发者使用。

### 附加信息 {#additional-information}

有关开发人员的详细信息，请参阅[Community Group Essentials](/help/communities/essentials-groups.md)页。

有关社区组的其他信息，请访问[管理用户和用户组](/help/communities/users.md)。
