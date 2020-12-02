---
title: 组模板
seo-title: 组模板
description: 如何访问“组模板”控制台
seo-description: 如何访问“组模板”控制台
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 3%

---


# 组模板 {#group-templates}

组模板控制台与[站点模板](/help/communities/sites.md)控制台类似。 这两者都是构建社区站点的一套预连接页面和功能的蓝图。 区别在于站点模板适用于主社区，而组模板适用于社区组，即嵌套在主社区中的子社区。

通过包括[Groups函数](/help/communities/functions.md#groups-function)将社区组纳入站点模板中（该函数可能不是模板中的第一个也不是唯一的函数）。

从社区[功能包1](/help/communities/deploy-communities.md#latestfeaturepack)开始，可以通过在组模板中包含组功能来嵌套组。

当采取操作创建新社区组时，将选择该组的模板（结构）。 选择取决于在添加到站点或组模板时如何配置组功能。

>[!NOTE]
>
>创建[社区站点](/help/communities/sites-console.md)、[社区站点模板](/help/communities/sites.md)、[社区组模板](/help/communities/tools-groups.md)和[社区功能](/help/communities/functions.md)的控制台仅用于创作环境。

## 组模板控制台{#group-templates-console}

要访问AEM作者环境中的组模板控制台，请执行以下操作：

* 选择&#x200B;**工具 |社区 |组模板，**。

此控制台显示可从中创建[社区站点](/help/communities/sites-console.md)的模板，并允许创建新组模板。

![社区组模板](assets/groups-template.png)

## 创建组模板 {#create-group-template}

要开始创建新组模板，请选择`Create`。

这将显示包含3个子面板的站点编辑器面板：

### 基本信息 {#basic-info}

![site-basic-info](assets/site-basic-info.png)

在“基本信息”面板上，将配置名称、说明以及是否启用或禁用模板：

* **新组模板名称**

   模板名称id。

* **描述**

   模板描述。

* **禁用／启用**

   控制模板是否可引用的切换开关。

#### 缩略图 {#thumbnail}

![站点缩略图](assets/site-thumbnail.png)

（可选）选择上传图像图标以向社区站点的创建者显示缩略图以及名称和说明。

#### 结构 {#structure}

>[!CAUTION]
>
>如果使用AEM 6.1 Communities FP4或更早版本，请勿将组功能添加到组模板。
>
>嵌套组功能从Communities [FP1](/help/communities/communities.md#latestfeaturepack)开始可用。
>
>仍不允许将“组”函数添加为模板中的第一个或唯一函数。

![组模板编辑器](assets/template-editor.png)

要添加社区功能，请按站点菜单链接的显示顺序从右侧向左拖动。 样式将在创建站点时应用于模板。

例如，如果您想要论坛，请将论坛功能从库拖放到模板生成器下。 这将导致打开论坛配置对话框。 有关配置对话框的信息，请参见[函数控制台](/help/communities/functions.md)。

根据此模板，继续拖放子社区站点（组）所需的任何其他社区功能。

![拖动函数](assets/dragfunctions.png)

将所有所需的函数放入模板生成器区域并进行配置后，选择右上角的&#x200B;**保存**。

## 编辑组模板{#edit-group-template}

在主[组模板控制台](#group-templates-console)中查看社区组时，可以选择现有的组模板进行编辑。

编辑组模板不会影响已通过模板创建的社区站点。 可以直接[编辑社区站点](/help/communities/sites-console.md#modify-structure)的结构。

此过程提供与创建组模板[相同的面板。](#create-group-template)
