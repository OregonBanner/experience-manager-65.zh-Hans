---
title: 站点模板
description: 如何访问站点模板控制台
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 4%

---

# 站点模板 {#site-templates}

站点模板控制台类似于 [组模板](tools-groups.md) 控制台，侧重于社区组感兴趣的功能。

>[!NOTE]
>
>用于创建的控制台 [社区站点](sites-console.md)， [社区站点模板](sites.md)， [社区组模板](tools-groups.md)、和 [社区功能](functions.md) 仅供在创作环境中使用。

## 站点模板控制台 {#site-templates-console}

在创作环境中，要访问社区站点控制台，请执行以下操作：

* 从全局导航： **[!UICONTROL 工具>社区>站点模板]**

此控制台显示从中创建 [社区站点](sites-console.md) 可以创建，并允许创建新站点模板。

![site-template](assets/site-template.png)

## 创建站点模板 {#create-site-template}

要开始创建站点模板，请选择 `Create`.

这将打开站点编辑器面板，其中包含三个子面板：

### 基本信息 {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

在“基本信息”面板上，配置了名称、描述以及模板是启用还是禁用：

* **[!UICONTROL 社区站点模板名称]**

  模板名称id。

* **[!UICONTROL 社区站点模板描述]**

  模板描述。

* **[!UICONTROL 已禁用/已启用]**

  控制模板是否可引用的切换开关。

### 缩略图 {#thumbnail}

![site-thumnail](assets/site-thumbnail.png)

（可选）选择上传图像图标以显示缩略图，以及社区站点创建者的名称和描述。

### 结构 {#structure}

![站点结构](assets/site-structure.png)

要添加社区功能，请按照站点菜单链接出现的顺序，从右向左拖动。 样式在创建站点期间应用到模板。

例如，如果您希望创建主页，请从库拖动“页面”函数，然后将其放到模板生成器下。 这将导致打开页面配置对话框。 请参阅 [函数控制台](functions.md) 有关配置对话框的信息。

继续拖放基于此模板的社区站点所需的任何其他社区功能。

page函数提供一个空页面。 使用“组”功能，可在社区站点中创建组站点（子社区）。

>[!CAUTION]
>
>“组”功能必须 *不是第一个，也不是唯一的* 在站点结构中的函数。
>
>任何其他函数，如 [页面函数](functions.md#page-function)，必须先包含并列出。

![站点编辑器](assets/site-editor.png)

### 组功能组模板 {#group-templates-for-groups-function}

在站点模板中包括“组”功能时，配置要求指定在发布环境中创建新组时允许的组模板选项。

>[!CAUTION]
>
>“组”功能必须 *不是第一个，也不是唯一的* 在站点结构中的函数。

![站点功能](assets/site-functions.png)

通过选择两个或多个社区组模板，可在社区中实际创建组时为组管理员提供一个选择。

![站点功能](assets/site-functions1.png)

## 编辑站点模板 {#edit-site-template}

在主视图中查看站点模板时 [站点模板控制台](#site-templates-console)，则可以选择要编辑的现有站点模板。

此过程提供的面板与相同 [创建站点模板](#create-site-template).
