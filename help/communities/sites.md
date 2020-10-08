---
title: 站点模板
seo-title: 站点模板
description: 如何访问站点模板控制台
seo-description: 如何访问站点模板控制台
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 4%

---


# 站点模板 {#site-templates}

“站点模板”控制台与“组模板” [控制台非常相似](tools-groups.md) ，该控制台侧重于社区组所关注的功能。

>[!NOTE]
>
>创建社区站点的控 [制台](sites-console.md)、社 [区站点模板](sites.md)、社 [区组模板](tools-groups.md)[和社区功](functions.md) 能的控制台仅在作者环境中使用。

## 站点模板控制台 {#site-templates-console}

在创作环境中，要访问社区站点控制台：

* 从全局导航： **[!UICONTROL “工具”>“社区”>“站点模板”]**

此控制台显示可从中创建社 [区站点](sites-console.md) 的模板，并允许创建新站点模板。

![站点模板](assets/site-template.png)

## 创建站点模板 {#create-site-template}

要开始创建新站点模板，请选择 `Create`。

这将显示包含3个子面板的站点编辑器面板：

### Basic info {#basic-info}

![站点模板——基础信息](assets/site-template-basicinfo.png)

在“基本信息”面板上，将配置名称、说明以及是否启用或禁用模板：

* **[!UICONTROL 社区站点模板名称]**

   模板名称id。

* **[!UICONTROL 社区站点模板描述]**

   模板描述。

* **[!UICONTROL 禁用／启用]**

   控制模板是否可引用的切换开关。

### 缩略图 {#thumbnail}

![站点缩略图](assets/site-thumbnail.png)

（可选）选择上传图像图标，以便向社区站点的创建者显示缩略图以及名称和说明。

### 结构 {#structure}

![站点结构](assets/site-structure.png)

要添加社区功能，请按站点菜单链接的显示顺序从右侧向左拖动。 样式将在创建站点时应用于模板。

例如，如果您想要主页，请将页面功能从库拖放到模板生成器下。 这将导致打开页面配置对话框。 有关配置 [对话框](functions.md) ，请参阅函数控制台。

根据此模板，继续拖放社区站点所需的任何其他社区功能。

页面功能提供空页面。 组功能提供在社区站点内创建组站点（子社区）的功能。

>[!CAUTION]
>
>组函数不 *能是* 站 *点结构中* 的第一个，也不能是唯一的函数。
>
>任何其他函数(如页 [面函数](functions.md#page-function))必须首先包含并列出。

![站点编辑器](assets/site-editor.png)

### 组功能的组模板 {#group-templates-for-groups-function}

当在站点模板中包含组功能时，配置需要指定在发布环境中创建新组时允许的组模板选择。

>[!CAUTION]
>
>“组”函 *数不* 能是 *站点结构中* 的第一个，也不能是唯一的函数。

![站点功能](assets/site-functions.png)

通过选择两个或多个社区组模板，当在社区中实际创建新组时，将向组管理员提供一个选项。

![站点功能](assets/site-functions1.png)

## 编辑站点模板{#edit-site-template}

在主站点模板控制台中 [查看站点模板](#site-templates-console)，可以选择现有的站点模板进行编辑。

此过程提供的面板与创 [建站点模板相同](#create-site-template)。
