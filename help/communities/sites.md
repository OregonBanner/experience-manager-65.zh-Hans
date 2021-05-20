---
title: 站点模板
seo-title: 站点模板
description: 如何访问“站点模板”控制台
seo-description: 如何访问“站点模板”控制台
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
role: Administrator
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 4%

---

# 站点模板 {#site-templates}

“站点模板”控制台与[组模板](tools-groups.md)控制台非常相似，该控制台侧重于社区组所关注的功能。

>[!NOTE]
>
>用于创建[社区站点](sites-console.md)、[社区站点模板](sites.md)、[社区组模板](tools-groups.md)和[社区功能](functions.md)的控制台仅供在创作环境中使用。

## 站点模板控制台{#site-templates-console}

在创作环境中，要访问社区站点控制台，请执行以下操作：

* 从全局导航：**[!UICONTROL 工具>社区>网站模板]**

此控制台显示可从中创建[社区站点](sites-console.md)的模板，并允许创建新站点模板。

![站点模板](assets/site-template.png)

## 创建站点模板 {#create-site-template}

要开始创建新站点模板，请选择`Create`。

这将显示包含3个子面板的站点编辑器面板：

### 基本信息{#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

在“基本信息”面板上，配置了模板的名称、说明以及是启用还是禁用了模板：

* **[!UICONTROL 社区站点模板名称]**

   模板名称id。

* **[!UICONTROL 社区站点模板描述]**

   模板描述。

* **[!UICONTROL 已禁用/已启用]**

   控制模板是否可引用的切换开关。

### 缩略图 {#thumbnail}

![网站缩略图](assets/site-thumbnail.png)

（可选）选择上传图像图标，以向社区站点的创建者显示缩略图以及名称和描述。

### 结构 {#structure}

![站点结构](assets/site-structure.png)

要添加社区功能，请按网站菜单链接的显示顺序从右侧向左拖动。 样式将在站点创建期间应用于模板。

例如，如果您想要某个主页，请将库中的Page函数拖放到模板生成器下。 这将导致打开页面配置对话框。 有关配置对话框的信息，请参阅[函数控制台](functions.md)。

继续拖放基于此模板的社区站点所需的任何其他社区功能。

页面函数提供一个空页面。 群组功能提供在社区站点内创建群组站点（子社区）的功能。

>[!CAUTION]
>
>组函数必须&#x200B;*不*&#x200B;是站点结构中的&#x200B;*第一个函数，也不是唯一的*&#x200B;函数。
>
>必须先包含并列出任何其他函数，如[page函数](functions.md#page-function)。

![站点编辑器](assets/site-editor.png)

### 组函数{#group-templates-for-groups-function}的组模板

在站点模板中包含组功能时，配置要求指定在发布环境中创建新组时允许的组模板选项。

>[!CAUTION]
>
>组函数必须&#x200B;*不*&#x200B;是站点结构中的&#x200B;*第一个函数，也不是唯一的*&#x200B;函数。

![网站功能](assets/site-functions.png)

通过选择两个或更多社区组模板，在社区中实际创建新组时，可向组管理员提供选择。

![网站功能](assets/site-functions1.png)

## 编辑站点模板{#edit-site-template}

在主[站点模板控制台](#site-templates-console)中查看站点模板时，可以选择现有的站点模板进行编辑。

此过程提供与创建站点模板](#create-site-template)相同的面板。[
