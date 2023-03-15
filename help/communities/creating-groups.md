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

社区组功能允许子社区由发布和创作环境中的授权用户（社区成员和作者）在社区站点中动态创建。

此功能在以下情况下存在 [组函数](/help/communities/functions.md#groups-function) 中存在于 [社区站点](/help/communities/sites-console.md) 结构。

A [社区组模板](/help/communities/tools-groups.md) 在动态创建社区组时提供社区组页面的设计。

将功能添加到社区站点的结构或社区站点模板时，会为组功能选择一个或多个组模板。 此组模板列表会呈现给从社区站点动态创建新组的成员或作者。

## 创建新组 {#creating-a-new-group}

创建新社区组的能力取决于社区站点的存在，该站点包括组功能，例如从创建的社区站点。 [引用站点模板](/help/communities/sites.md).

下面的示例使用从创建的社区站点 `Reference Site Template` 如 [AEM Communities快速入门](/help/communities/getting-started.md) 教程。

这是发布时加载的页面，当 **组** 已选择菜单项：

![new-group](assets/new-group.png)

当您选择 **新建组** 图标，此时会打开一个编辑对话框。

在 **设置** 选项卡，提供组的基本功能：

![组设置](assets/group-settings.png)

* **组名称**

   要在社区站点上显示的组的标题。 避免在组名中使用下划线字符(_)和关键字（如资源和配置）。

* **描述**

   要在社区站点上显示的组的描述。

* **邀请**

   邀请加入组的成员列表。 提前输入搜索将提供社区成员邀请的建议。

* **组 URL 名称**

   成为URL一部分的组页面的名称。

* **开放组**

   选择 `Open Group` 指示任何匿名网站访客可以查看内容，并将取消选择 `Member Only Group`.

* **仅限成员加入的组**

   选择 `Member Only Group` 表示只有组的成员可以查看内容，并且将取消选择 `Open Group`.

在 **模板** 选项卡用于从社区组模板列表中进行选择的功能，在社区站点的结构或社区站点模板中包含组功能时，会指定这些模板。

![group-template](assets/group-template.png)

在 **图像** 选项卡是上传图像以在社区站点的“组”页面上为组显示的功能。 默认样式表会将图像大小调整为170 x 90像素。

![组图像](assets/group-image.png)

通过选择 **创建组** 按钮，将根据所选模板创建组的页面，并为成员资格创建用户组，并且将更新“组”页面以显示新的子社区。

例如，标题为“焦点组”的新子社区（已为其上传图像缩略图）的“组”页面将显示如下（仍以社区组管理员身份登录）：

![group-page](assets/group-page.png)

选择 `Focus Group` 链接将在浏览器中打开“焦点组”页面，该页面的初始外观基于所选模板，并在主社区站点的菜单下包含一个子菜单：

![open-group-page](assets/open-group-page.png)

### 社区组成员列表组件 {#community-group-member-list-component}

此 `Community Group Member List` 组件专供组模板的开发人员使用。

### 附加信息 {#additional-information}

欲知更多信息，请访问 [社区组要点](/help/communities/essentials-groups.md) 适用于开发人员的页面。

有关社区组的其他信息，请访问 [管理用户和用户组](/help/communities/users.md).
