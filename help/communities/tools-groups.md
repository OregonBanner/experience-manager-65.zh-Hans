---
title: 组模板
seo-title: Group Templates
description: 如何访问“组模板”控制台
seo-description: How to access the Group Templates console
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# 组模板 {#group-templates}

“组模板”控制台与 [站点模板](/help/communities/sites.md) 控制台。 两者都是构成社区站点的一组预布线页面和功能的蓝图。 不同之处在于，站点模板适用于主社区，组模板适用于社区组（嵌套在主社区中的子社区）。

社区组通过包含 [组功能](/help/communities/functions.md#groups-function) （该功能可能不是模板中的第一个或唯一函数）。

截至社区 [功能包1](/help/communities/deploy-communities.md#latestfeaturepack)，可通过在组模板中包含组函数来嵌套组。

执行操作创建新社区组后，即会选择该组的模板（结构）。 选择取决于组功能在添加到站点或组模板时的配置方式。

>[!NOTE]
>
>用于创建的控制台 [社区站点](/help/communities/sites-console.md)， [社区站点模板](/help/communities/sites.md)， [社区组模板](/help/communities/tools-groups.md) 和 [社区功能](/help/communities/functions.md) 仅用于创作环境。

## 组模板控制台 {#group-templates-console}

要访问AEM创作环境中的“组模板”控制台，请执行以下操作：

* 选择 **工具 |社区 |组模板，** 从全局导航中。

此控制台显示模板，其中 [社区站点](/help/communities/sites-console.md) 可以创建，并允许创建新的组模板。

![社区组模板](assets/groups-template.png)

## 创建组模板 {#create-group-template}

要开始创建新组模板，请选择 `Create`.

这将显示站点编辑器面板，其中包含3个子面板：

### 基本信息 {#basic-info}

![site-basic-info](assets/site-basic-info.png)

在“基本信息”面板上，配置了名称、说明以及模板是启用还是禁用：

* **新组模板名称**

   模板名称id。

* **描述**

   模板描述。

* **已禁用/已启用**

   控制模板是否可引用的切换开关。

#### 缩略图 {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

（可选）选择“上传图像”图标以显示缩略图，以及社区站点创建者的名称和描述。

#### 结构 {#structure}

>[!CAUTION]
>
>如果使用AEM 6.1 Communities FP4或更低版本，请勿将组函数添加到组模板。
>
>嵌套群组功能自社区起可用 [FP1](/help/communities/communities.md#latestfeaturepack).
>
>仍不允许将组函数添加为模板中的第一个或唯一函数。

![组模板编辑器](assets/template-editor.png)

要添加社区功能，请按站点菜单链接出现的顺序从右侧向左拖动。 样式将在创建站点期间应用于模板。

例如，如果您需要论坛，请将论坛函数从库中拖放到模板生成器下。 这将导致论坛配置对话框打开。 请参阅 [函数控制台](/help/communities/functions.md) 有关配置对话框的信息。

基于此模板，继续拖放子社区站点（组）所需的任何其他社区功能。

![拖动函数](assets/dragfunctions.png)

将所有需要的函数放入模板生成器区域并进行配置后，选择 **保存** 在右上角。

## 编辑组模板 {#edit-group-template}

在主页中查看社区组时 [组模板控制台](#group-templates-console)，则可以选择要编辑的现有组模板。

编辑组模板不会影响已从该模板创建的社区站点。 可以直接执行以下操作 [编辑社区站点](/help/communities/sites-console.md#modify-structure)的构造替换为。

此流程提供的面板与 [创建组模板](#create-group-template).
