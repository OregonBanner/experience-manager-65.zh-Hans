---
title: 翻译用户生成的内容
seo-title: Translating User Generated Content
description: 翻译功能的工作原理
seo-description: How the translation feature works
uuid: 7ee3242c-2aca-4787-a60d-b807161401ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: bfaf80c5-448b-47fb-9f22-57ee0eb169b2
role: Admin
exl-id: ac54f06e-1545-44bb-9f8f-970f161ebb72
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 0%

---

# 翻译用户生成的内容 {#translating-user-generated-content}

AEM Communities的翻译功能扩展了 [翻译页面内容](../../help/sites-administering/translation.md) 发布到社区站点的用户生成内容(UGC)，使用 [社交组件框架(SCF)组件](scf.md).

UGC的翻译使站点访客和成员能够通过消除语言障碍而体验全球社区。

例如，假设：

* 一位来自法国的成员在一家跨国烹饪网站的社区论坛上发布了一份法文食谱。
* 另一位日本成员使用该翻译功能触发将配方从法语翻译为日语。
* 在阅读了日文的食谱后，这位日本成员随后用日文发表了评论。
* 来自法国的成员使用翻译功能将日语评论翻译为法语。
* 全球通信。

## 概述 {#overview}

本文档的这一部分具体讨论了翻译服务如何与UGC配合使用，同时假定您了解如何将AEM连接到 [翻译服务提供商](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) 并通过配置 [翻译集成框架](../../help/sites-administering/tc-tic.md).

当翻译服务提供商与站点关联时，站点的每个语言副本都维护其自身的通过SCF组件（如注释）发布的UGC线程。

当除了翻译服务提供商之外还配置翻译集成框架时，站点的每个语言副本可以共享单个UGC线程，从而提供跨语言副本的全局通信。 不是按语言分隔的讨论会话，而是配置的 [全局共享存储](#global-translation-of-ugc) 使整个线程可见，无论查看的是哪种语言副本。 此外，可以配置多个翻译集成配置，为诸如按区域的全局参与者的逻辑分组指定不同的全局共享存储。

## 默认翻译服务 {#the-default-translation-service}

AEM Communities包含 [试用许可证](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) 对于 [默认翻译服务](../../help/sites-administering/tc-msconf.md) 已为多种语言启用。

时间 [创建社区站点](sites-console.md)，则默认翻译服务在以下情况下启用： `Allow Machine Translation` 是从 [翻译](sites-console.md#translation) 子面板。

>[!CAUTION]
>
>默认翻译服务仅用于演示。
>
>对于生产系统，需要获得许可的翻译服务。 如果未获得许可，则默认翻译服务应为 [已关闭](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## UGC的全局翻译 {#global-translation-of-ugc}

当网站有多个时 [语言副本](../../help/sites-administering/tc-prep.md)，则默认翻译服务不会识别一个站点上输入的UGC可能与另一个站点上输入的UGC相关，例如，当UGC基本上由同一组件（包含该组件的页面的语言副本）生成时。

这类似于讨论一个话题的人群，他们不知道自己以外的小组正在发表评论，而同一个大小组中的每个人参加一个对话。

如果需要“一个组对话”，则可以在具有多语言副本的网站中启用全局翻译，以便无论查看的是哪种语言副本，整个线程都可见。

例如，如果在基本站点上建立了论坛，创建了语言副本，并启用了全局翻译，则使用一种语言副本发布到论坛的主题将显示在所有语言副本中。 无论从哪种语言副本输入回复，任何回复都同样如此。 结果是，无论从哪个语言副本查看主题，都可以看到该主题及其整个回复线程。

>[!CAUTION]
>
>在全局翻译之前存在的任何UGC都不再可见。
>
>当UGC仍在 [公用存储](working-with-srp.md)，它位于特定语言的UGC位置下，而正在从全局共享存储位置检索在配置全局翻译后添加的新内容。
>
>没有迁移工具可以将特定于语言的内容移动或合并到全局共享存储中。

### 翻译集成配置 {#translation-integration-configuration}

要创建新的翻译集成，它将翻译服务连接器与创作实例上的网站集成，请执行以下操作：

* 以管理员身份登录
* 从 [主菜单](http://localhost:4502/)
* 选择 **[!UICONTROL 工具]**
* 选择 **[!UICONTROL 操作]**
* 选择 **[!UICONTROL 云]**
* 选择 **[!UICONTROL Cloud Services]**
* 向下滚动到 **[!UICONTROL 翻译集成]**

   ![translation-integration](assets/translation-integration.png)

* 选择 **[!UICONTROL 显示配置]**

   ![显示配置](assets/translation-integration1.png)

* 选择 `[+]` 图标旁边 **[!UICONTROL 可用配置]** 创建新配置

#### “创建配置”对话框 {#create-configuration-dialog}

![create — 配置](assets/translation-integration2.png)

* **[!UICONTROL 父配置]**

   （必需）通常保留为默认值。 默认为 `/etc/cloudservices/translation`.

* **[!UICONTROL 标题]**

   （必需）输入您选择的显示标题。 无默认值。

* **[!UICONTROL 名称]**

   （可选）输入配置的名称。 默认值是基于标题的节点名称。

* 选择 **[!UICONTROL 创建]**

#### 翻译配置对话框 {#translation-config-dialog}

![配置 — 对话框](assets/translation-integration3.png)

有关详细说明，请访问 [创建翻译集成配置](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)

* **[!UICONTROL 站点]** 选项卡：可保留为默认值。

* **[!UICONTROL Communities]** 选项卡：
   * **[!UICONTROL 翻译提供商]**
从下拉列表中选择翻译提供商。 默认为 
`microsoft`，试用服务。

   * **[!UICONTROL 内容类别]**
选择描述正在翻译的内容的类别。 默认为 
`General.`

   * **[!UICONTROL 选择区域设置……]**
（可选）通过选择存储UGC的区域设置，来自所有语言副本的帖子将显示在一个全局对话中。 按照惯例，选择 [基本语言](sites-console.md#translation) 用于网站。 选择 `No Common Store` 将禁用全局翻译。 默认情况下，全局翻译处于禁用状态。

* **[!UICONTROL 资产]** 选项卡：可保留为默认值。
* 选择 **[!UICONTROL 确定]**

#### 激活 {#activation}

需要将新的翻译集成云服务激活到发布环境。 与网站关联时，如果尚未激活，则激活工作流会在发布与其关联的页面时提示发布此云服务配置。

## 管理翻译设置 {#managing-translation-settings}

>[!NOTE]
>
>**首选语言**
>
>为了检测帖子是否使用与首选语言不同的语言，必须建立站点访客的首选语言。
>
>首选语言是当网站访客登录并指定语言首选项时，用户配置文件中设置的语言首选项。
>
>当网站访客匿名或未在其配置文件中指定语言首选项时，首选语言是页面模板的基本语言。

### 用户首选项 {#user-preference}

#### 用户配置文件 {#user-profile}

所有社区站点都提供一个用户配置文件，登录成员可以编辑该配置文件以在社区中标识他们自己并设置他们的首选项。

其中一项设置是是否始终以首选语言显示社区内容。 默认情况下，未设置该设置，它将默认为系统设置。 用户可以将该设置更改为“On（开）”或“Off（关）”，从而覆盖系统设置。

当页面自动翻译成用户的首选语言时，仍可以使用用于显示原始文本和改进翻译的UI。

![user-profile](assets/translation-integration4.png)

### 社区站点设置 {#community-site-setting}

创建社区站点后，可以启用和配置翻译选项。 翻译设置对匿名网站访客可以查看的内容有效，但会被用户的配置文件设置覆盖。
