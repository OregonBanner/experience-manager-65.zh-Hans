---
title: 社区组
seo-title: Community Groups
description: 创建社区组
seo-description: Creating community groups
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 3%

---

# 社区组 {#community-groups}

社区组功能是允许子社区由发布和创作环境中的授权用户（社区成员和作者）在社区站点内动态创建。

当 [组函数](/help/communities/functions.md#groups-function) 在 [社区网站](/help/communities/sites-console.md) 结构。

A [社区组模板](/help/communities/tools-groups.md) 在动态创建社区组时，提供社区组页面的设计。

当将功能添加到社区站点的结构或社区站点模板时，为组功能选择一个或多个组模板。 此组模板列表将呈现给从社区站点中动态创建新组的成员或作者。

## 创建新组 {#creating-a-new-group}

能否创建新的社区组取决于是否存在一个社区站点，该站点包含组功能，例如使用 [参考网站模板](/help/communities/sites.md).

以下示例使用通过 `Reference Site Template` 如 [开始使用AEM Communities](/help/communities/getting-started.md) 教程。

这是在 **群组** 菜单项：

![新组](assets/new-group.png)

当您选择 **新建组** 图标，此时将打开编辑对话框。

在 **设置** 选项卡，可提供组的基本功能：

![组设置](assets/group-settings.png)

* **组名称**

   要在社区网站上显示的组的标题。 避免在组名称中使用下划线字符(_)和诸如资源和配置等关键字。

* **描述**

   要在社区网站上显示的群组描述。

* **邀请**

   要邀请加入群组的成员列表。 提前键入搜索将提供社区成员邀请的建议。

* **组 URL 名称**

   成为URL一部分的群组页面的名称。

* **开放组**

   选择 `Open Group` 指示任何匿名网站访客都可以查看内容，并将取消选择 `Member Only Group`.

* **仅限成员加入的组**

   选择 `Member Only Group` 仅指示组成员可以查看内容，并将取消选择 `Open Group`.

在 **模板** 选项卡是从社区组模板列表中进行选择的功能，这些模板在将组功能包含在社区站点结构或社区站点模板中时指定。

![组模板](assets/group-template.png)

在 **图像** 选项卡是在社区站点的“组”页面上上传要显示的组图像的功能。 默认样式表会将图像的大小调整为170 x 90像素。

![组图像](assets/group-image.png)

通过选择 **创建群组** 按钮时，将根据所选模板创建群组的页面，并为成员资格创建用户群组，此时将更新群组页面以显示新的子社区。

例如，标题为“焦点组”的新子社区的“组”页面（已上传图像缩略图）将如下所示（仍以社区组管理员身份登录）：

![群组页面](assets/group-page.png)

选择 `Focus Group` 链接将在浏览器中打开焦点组页面，该页面具有基于所选模板的初始外观，并在主社区站点的菜单下方包含一个子菜单：

![open-group-page](assets/open-group-page.png)

### 社区组成员列表组件 {#community-group-member-list-component}

的 `Community Group Member List` 组件供组模板的开发人员使用。

### 附加信息 {#additional-information}

有关 [社区组要点](/help/communities/essentials-groups.md) 页面。

有关社区组的其他信息，请访问 [管理用户和用户组](/help/communities/users.md).
