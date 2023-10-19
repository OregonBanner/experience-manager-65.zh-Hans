---
title: 翻译用户生成的内容
description: 了解UGC内容的翻译如何让站点访客和成员通过消除语言障碍体验全球社区。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: ac54f06e-1545-44bb-9f8f-970f161ebb72
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%

---

# 翻译用户生成的内容 {#translating-user-generated-content}

Adobe Experience Manager (AEM) Communities的翻译功能扩展了 [翻译页面内容](../../help/sites-administering/translation.md) 发布到社区站点的用户生成内容(UGC)，使用 [社交组件框架(SCF)组件](scf.md).

UGC的翻译使站点访客和成员能够通过消除语言障碍体验全球社区。

例如，假设：

* 一位法国人在一个跨国烹饪网站的社区论坛上发布了一份法文食谱。
* 来自日本的另一位成员使用该翻译功能来触发将配方从法语翻译为日语。
* 看完日文的食谱后，这位日本成员随后用日文发表了一则评论。
* 来自法国的成员使用翻译功能将日语评论翻译为法语。
* 全球通信。

## 概述 {#overview}

此部分具体讨论了翻译服务如何与UGC配合使用。 它还假定您了解如何将AEM连接到 [翻译服务提供商](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) 并通过配置 [翻译集成框架](../../help/sites-administering/tc-tic.md).

当翻译服务提供商与站点相关联时，站点的每个语言副本都会维护其自身通过SCF组件（如注释）发布的UGC线程。

除了翻译服务提供商之外，如果配置了翻译集成，则站点的每个语言副本可能会共享单个UGC线程，从而提供跨语言副本的全局通信。 不是按语言分隔的讨论会话，而是配置的 [全局共享存储](#global-translation-of-ugc) 使整个线程可见，而不管查看的是哪种语言副本。 此外，可以配置多个翻译集成配置，为全局参与者的逻辑分组（例如按区域）指定不同的全局共享存储。

## 默认翻译服务 {#the-default-translation-service}

AEM Communities包含 [试用许可证](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) 对于 [默认翻译服务](../../help/sites-administering/tc-msconf.md) 已为多种语言启用。

时间 [创建社区站点](sites-console.md)，则在以下情况下会启用默认翻译服务 `Allow Machine Translation` 已勾选 [翻译](sites-console.md#translation) 子面板。

>[!CAUTION]
>
>默认翻译服务仅用于演示。
>
>对于生产系统，需要获得许可的翻译服务。 如果未获得许可，则默认翻译服务应为 [已关闭](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## UGC的全局翻译 {#global-translation-of-ugc}

当网站有多个时 [语言副本](../../help/sites-administering/tc-prep.md)，默认翻译服务无法识别在一个站点上输入的UGC是否可能与在另一个站点上输入的UGC相关。 如果UGC由同一组件（包含该组件的页面的语言副本）生成，则为true。

它类似于讨论某个话题的一群人。 与参加同一个对话的大群组中的每个人相比，他们不知道在自己以外的群组中发表的评论。

如果需要“一个组对话”，则可以在具有多语言副本的网站上启用全局翻译，以便查看整个会话，无论查看的是哪种语言副本。

例如，如果在基本站点上建立了论坛，创建了语言副本，并且启用了全局翻译，则发布到论坛的主题将以一种语言副本的形式出现在所有语言副本中。 无论从哪种语言副本输入回复，所有回复都同样如此。 结果是，无论从哪个语言副本查看主题，都可以看到该主题及其整个回复线程。

>[!CAUTION]
>
>在全局翻译之前存在的任何UGC不再可见。
>
>当UGC仍然在 [公用存储](working-with-srp.md)，它位于特定语言的UGC位置下，而配置全局翻译后添加的新内容正在从全局共享存储位置检索。
>
>没有用于将特定语言内容移动或合并到全局共享存储中的迁移工具。

### 翻译集成配置 {#translation-integration-configuration}

要创建翻译集成，它将翻译服务连接器与创作实例上的网站集成，请执行以下操作：

* 以管理员身份登录
* 从 [主菜单](http://localhost:4502/)
* 选择 **[!UICONTROL 工具]**
* 选择 **[!UICONTROL 操作]**
* 选择 **[!UICONTROL 云]**
* 选择 **[!UICONTROL Cloud Service]**
* 向下滚动到 **[!UICONTROL 翻译集成]**

  ![translation-integration](assets/translation-integration.png)

* 选择 **[!UICONTROL 显示配置]**

  ![显示配置](assets/translation-integration1.png)

* 选择 `[+]` 图标旁边 **[!UICONTROL 可用配置]** 以便创建配置。

#### “创建配置”对话框 {#create-configuration-dialog}

![create-configure](assets/translation-integration2.png)

* **[!UICONTROL 父配置]**

  （必需）通常保留为默认值。 默认为 `/etc/cloudservices/translation`.

* **[!UICONTROL 标题]**

  （必需）输入您选择的显示标题。 无默认值。

* **[!UICONTROL 名称]**

  （可选）输入配置的名称。 默认值是基于标题的节点名称。

* 选择 **[!UICONTROL 创建]**

#### 翻译配置对话框 {#translation-config-dialog}

![配置对话框](assets/translation-integration3.png)

有关详细说明，请参阅 [创建翻译集成配置](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration).

* **[!UICONTROL 站点]** 选项卡：可保留为默认值。

* **[!UICONTROL Communities]** 选项卡：
   * **[!UICONTROL 翻译提供商]**
从下拉列表中选择翻译提供商。 默认为 `microsoft`，即试用服务。

   * **[!UICONTROL 内容类别]**
选择描述正在翻译的内容的类别。 默认为 `General.`

   * **[!UICONTROL 选择区域设置……]**
（可选）通过选择存储UGC的区域设置，来自所有语言副本的帖子将显示在一个全局对话中。 按照惯例，选择 [基本语言](sites-console.md#translation) 用于网站。 选择 `No Common Store` 禁用全局翻译。 默认情况下，全局翻译处于禁用状态。

* **[!UICONTROL 资产]** 选项卡：可保留为默认值。
* 选择 **[!UICONTROL 确定]**

#### 激活 {#activation}

必须将新的翻译集成云服务激活到发布环境。 与网站关联时，如果尚未激活，激活工作流会在发布与其关联的页面时提示发布此云服务配置。

## 管理翻译设置 {#managing-translation-settings}

>[!NOTE]
>
>**首选语言**
>
>在检测帖子是否使用与首选语言不同的语言时，必须建立站点访客的首选语言。
>
>首选语言是当网站访客登录并已指定语言首选项时，在用户配置文件中设置的语言首选项。
>
>当网站访客匿名或未在其个人资料中指定语言首选项时，首选语言是页面模板的基本语言。

### 用户首选项 {#user-preference}

#### 用户配置文件 {#user-profile}

所有社区站点都提供一个用户配置文件，登录成员可以编辑该配置文件以在社区中标识自己并设置其首选项。

其中一种设置是是否始终以首选语言显示社区内容。 默认情况下，不设置该设置，而是默认系统设置。 用户可以将设置更改为“On（打开）”或“Off（关闭）”以覆盖系统设置。

当页面自动翻译为用户的首选语言时，仍可以使用用于显示原始文本和改进翻译的UI。

![user-profile](assets/translation-integration4.png)

### 社区站点设置 {#community-site-setting}

创建社区站点后，可以启用和配置翻译选项。 翻译设置对匿名网站访客可以查看的内容有效，但会被用户的配置文件设置覆盖。
