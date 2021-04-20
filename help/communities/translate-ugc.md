---
title: 翻译用户生成的内容
seo-title: 翻译用户生成的内容
description: 翻译功能的工作原理
seo-description: 翻译功能的工作原理
uuid: 7ee3242c-2aca-4787-a60d-b807161401ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: bfaf80c5-448b-47fb-9f22-57ee0eb169b2
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 0%

---


# 翻译用户生成的内容{#translating-user-generated-content}

AEM Communities的翻译功能将[翻译页面内容](../../help/sites-administering/translation.md)的概念扩展到使用[社交组件框架(SCF)组件](scf.md)发布到社区站点的用户生成内容(UGC)。

UGC的翻译使网站访客和会员能够通过消除语言障碍体验全球社区。

例如，假设：

* 一位来自法国的成员在一家跨国烹饪网站的社区论坛上贴出了法文菜谱。
* 另一位来自日本的成员使用翻译功能触发将菜谱从法语翻译成日语。
* 读完日文菜谱后，这位来自日本的会员随后用日文发表了评论。
* 来自法国的成员使用翻译功能将日语评论翻译成法语。
* 全球通信。

## 概述 {#overview}

本文档的这一部分专门讨论翻译服务如何与UGC协作，同时假定了解如何将AEM连接到[翻译服务提供商](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider)，并通过配置[翻译集成框架](../../help/sites-administering/tc-tic.md)将该服务集成到网站。

当翻译服务提供商与站点关联时，站点的每个语言副本都会维护其自己通过SCF组件（如注释）发布的UGC线程。

当在翻译服务提供商之外配置翻译集成框架时，站点的每个语言副本可以共享UGC的单个线程，从而跨语言副本提供全局通信。 配置的[全局共享存储](#global-translation-of-ugc)使整个线程可见，而不是由语言隔离的讨论线程。 此外，可以配置多个翻译集成配置，以指定用于全局参与者的逻辑分组的不同全局共享存储，例如按区域。

## 默认翻译服务{#the-default-translation-service}

AEM Communities包含针对为多种语言启用的[默认翻译服务](../../help/sites-administering/tc-msconf.md)的[试用许可证](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license)。

当[创建社区站点](sites-console.md)时，当从[TRANSLATION](sites-console.md#translation)子面板中选中`Allow Machine Translation`时，将启用默认翻译服务。

>[!CAUTION]
>
>默认翻译服务仅用于演示。
>
>对于生产系统，需要授权翻译服务。 如果未获得许可，则默认翻译服务应关闭[](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors)。

## UGC {#global-translation-of-ugc}的全局翻译

当网站有多个[语言副本](../../help/sites-administering/tc-prep.md)时，默认翻译服务不识别在一个站点上输入的UGC可能与在另一个站点上输入的UGC相关，因为当UGC实质上是由同一组件（包含该组件的页面的语言副本）生成时。

这与讨论一个话题的一群人相似，他们对一个话题一无所知，他们不是自己的群体，而是与参与一个对话的一个大群体中的每个人都不同。

如果需要“一个组对话”，则可以在具有多个语言副本的网站上启用全局翻译，这样，无论查看哪个语言副本，整个线程都可见。

例如，如果在基站上建立了论坛，创建了语言副本，并启用了全局翻译，则以一个语言副本发布到论坛的主题将显示在所有语言副本中。 对于任何回复，无论回复是从哪个语言版本输入的，情况都是如此。 结果是，无论从哪种语言副本查看主题，主题及其回复的整个主题都是可见的。

>[!CAUTION]
>
>在全局翻译之前存在的任何UGC都不再可见。
>
>虽然UGC仍位于[公用存储](working-with-srp.md)中，但它位于特定于语言的UGC位置下，而配置全局转换后添加的新内容则从全局共享存储位置检索。
>
>没有用于将特定语言的内容移动或合并到全局共享存储的迁移工具。

### 翻译集成配置{#translation-integration-configuration}

要创建新的翻译集成，将翻译服务连接器与创作实例上的网站集成：

* 以管理员身份登录
* 从[主菜单](http://localhost:4502/)
* 选择&#x200B;**[!UICONTROL 工具]**
* 选择&#x200B;**[!UICONTROL 操作]**
* 选择&#x200B;**[!UICONTROL 云]**
* 选择&#x200B;**[!UICONTROL Cloud Services]**
* 向下滚动到&#x200B;**[!UICONTROL 转换集成]**

   ![翻译集成](assets/translation-integration.png)

* 选择&#x200B;**[!UICONTROL 显示配置]**

   ![show-configuration](assets/translation-integration1.png)

* 选择&#x200B;**[!UICONTROL 可用配置]**&#x200B;旁边的`[+]`图标以创建新配置

#### 创建配置对话框{#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL 父配置]**

   （必需）通常保留为默认值。 默认值为`/etc/cloudservices/translation`。

* **[!UICONTROL 标题]**

   （必需）输入您选择的显示标题。 没有默认值。

* **[!UICONTROL 名称]**

   （可选）输入配置的名称。 默认为基于标题的节点名称。

* 选择&#x200B;**[!UICONTROL 创建]**

#### 翻译配置对话框{#translation-config-dialog}

![configuration-dialog](assets/translation-integration3.png)

有关详细说明，请访问[创建翻译集成配置](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)

* **[!UICONTROL 站]** 点标签：可以保留为默认值。

* **** Communitiestab:
   * **[!UICONTROL 翻译提]**
供程序从下拉列表中选择翻译提供程序。默认为 
`microsoft`，试用服务。

   * **[!UICONTROL 内容]**
类别选择描述所翻译内容的类别。默认为 
`General.`

   * **[!UICONTROL 选择区域设置……]**
（可选）通过选择存储UGC的区域设置，来自所有语言副本的帖子将显示在一个全局对话中。根据惯例，为网站的[基本语言](sites-console.md#translation)选择区域设置。 选择`No Common Store`将禁用全局转换。 默认情况下，全局翻译处于禁用状态。

* **[!UICONTROL 资]** 产选项卡：可以保留为默认值。
* 选择&#x200B;**[!UICONTROL 确定]**

#### 激活 {#activation}

需要将新的翻译集成云服务激活到发布环境。 与网站关联时，如果尚未激活，则在与其关联的页面发布时，激活工作流将提示发布此云服务配置。

## 管理翻译设置{#managing-translation-settings}

>[!NOTE]
>
>**首选语言**
>
>为了检测帖子是否使用不同于首选语言的语言，必须建立网站访客的首选语言。
>
>首选语言是在登录网站用户档案并指定了语言首选项时，在用户的访客中设置的语言首选项。
>
>当站点访客为匿名或未在其用户档案中指定语言首选项时，首选语言是页面模板的基本语言。

### 用户首选项{#user-preference}

#### 用户个人资料 {#user-profile}

所有社区站点都提供用户用户档案，登录成员可进行编辑，以便向社区标识自己并设置其首选项。

其中一种设置是是否始终以其首选语言显示社区内容。 默认情况下，设置未设置，将默认设置为系统设置。 用户可以将设置更改为开或关，从而覆盖系统设置。

当页面自动翻译为用户的首选语言时，用于显示原始文本和改进翻译的UI仍然可用。

![用户用户档案](assets/translation-integration4.png)

### 社区站点设置{#community-site-setting}

创建社区站点后，可以启用和配置翻译选项。 翻译设置对匿名网站访客可能视图的内容有效，但由用户的用户档案设置覆盖。
