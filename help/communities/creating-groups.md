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
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---

# 社区组 {#community-groups}

社区组功能是允许子社区由发布和创作环境中的授权用户（社区成员和作者）在社区站点内动态创建。

当[groups函数](/help/communities/functions.md#groups-function)在[社区站点](/help/communities/sites-console.md)结构中存在时，即存在此功能。

[社区组模板](/help/communities/tools-groups.md)在动态创建社区组时提供社区组页面的设计。

当将功能添加到社区站点的结构或社区站点模板时，为组功能选择一个或多个组模板。 此组模板列表将呈现给从社区站点中动态创建新组的成员或作者。

## 创建新组{#creating-a-new-group}

能否创建新的社区组取决于是否存在包含组函数的社区站点，例如从[引用站点模板](/help/communities/sites.md)创建的社区站点。

以下示例使用从`Reference Site Template`创建的社区站点，如[AEM Communities](/help/communities/getting-started.md)快速入门教程中所述。

选择&#x200B;**Groups**&#x200B;菜单项时，在发布时加载的页面如下：

![新组](assets/new-group.png)

选择&#x200B;**新建组**&#x200B;图标时，将打开一个编辑对话框。

在&#x200B;**设置**&#x200B;选项卡下，提供组的基本功能：

![组设置](assets/group-settings.png)

* **组名称**

   要在社区网站上显示的组的标题。

* **描述**

   要在社区网站上显示的群组描述。

* **邀请**

   要邀请加入群组的成员列表。 提前键入搜索将提供社区成员邀请的建议。

* **组 URL 名称**

   成为URL一部分的组页面的名称。

* **开放组**

   选择`Open Group`表示任何匿名网站访客都可以查看该内容，并将取消选择`Member Only Group`。

* **仅限成员加入的组**

   选择`Member Only Group`表示只有组成员可以查看内容，并将取消选择`Open Group`。

在&#x200B;**Template**选项卡下，可以
从社区组模板列表中进行选择，当组功能包含在社区站点的结构或社区站点模板中时，会指定这些模板。

![组模板](assets/group-template.png)

在&#x200B;**Image**&#x200B;选项卡下，可以上传图像以在社区站点的“组”页面上显示组。 默认样式表会将图像的大小调整为170 x 90像素。

![组图像](assets/group-image.png)

通过选择&#x200B;**创建组**&#x200B;按钮，将根据所选模板创建组的页面，并为成员创建用户组，此时将更新“组”页面以显示新的子社区。

例如，标题为“焦点组”的新子社区的“组”页面（已上传图像缩略图）将如下所示（仍以社区组管理员身份登录）：

![群组页面](assets/group-page.png)

选择`Focus Group`链接将在浏览器中打开焦点组页面，该页面具有基于所选模板的初始外观，并在主社区站点的菜单下包含一个子菜单：

![open-group-page](assets/open-group-page.png)

### 社区组成员列表组件{#community-group-member-list-component}

`Community Group Member List`组件供组模板的开发人员使用。

### 附加信息 {#additional-information}

有关更多信息，请参阅面向开发人员的[Community Group Essentials](/help/communities/essentials-groups.md)页面。

有关社区组的其他信息，请访问[管理用户和用户组](/help/communities/users.md)。
