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
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# 翻译用户生成的内容 {#translating-user-generated-content}

AEM Communities的翻译功能将页面内容翻译的概念扩展 [到使用社交组件框架(SCF)组件发布到社区站点的用](../../help/sites-administering/translation.md) 户生成的内容(UGC) [](scf.md)。

UGC的翻译使网站访客和会员能通过消除语言障碍体验到全球社区。

例如，假设：

* 一位来自法国的成员用法语向一个跨国烹饪网站的社区论坛张贴了一个菜谱。
* 另一位来自日本的会员使用翻译功能触发将菜谱从法语翻译成日语。
* 读完日文菜谱后，这位来自日本的会员用日文发表评论。
* 来自法国的成员使用翻译功能将日语评论翻译成法语。
* 全球通信。

## 概述 {#overview}

本部分专门讨论了翻译服务如何与UGC一起使用，同时假设了解如何将AEM连接到翻译服务提供商 [，并通过配置翻译集成框架将该服务集成到](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) 网站中 [](../../help/sites-administering/tc-tic.md)。

当翻译服务提供商与站点相关联时，站点的每个语言副本将维护其自己通过SCF组件（如注释）发布的UGC线程。

当在翻译服务提供商之外配置翻译集成框架时，站点的每个语言副本都可能共享单个UGC线程，从而提供跨语言副本的全局通信。 所配置的全局共享存储使整个线程能够可见，而不管 [从哪个语言副本查看它](#global-translation-of-ugc) ，都不是按语言分隔的讨论线程。 此外，可以配置多个翻译集成配置以指定不同的全局共享存储，用于全局参与者的逻辑分组，例如按区域。

## 默认翻译服务 {#the-default-translation-service}

AEM Communities附带针对为多种语 [言启用的](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license)[默认翻译服务的试](../../help/sites-administering/tc-msconf.md) 用许可证。

在创 [建社区站点时](sites-console.md)，当从TRANSLATION子面板中选中 `Allow Machine Translation` 时，将启用默 [认翻译服务](sites-console.md#translation) 。

>[!CAUTION]
>
>默认翻译服务仅用于演示。
>
>对于生产系统，需要获得许可的翻译服务。 如果未获得许可，则应关闭默认翻译 [服务](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors)。


## UGC的全球翻译 {#global-translation-of-ugc}

当网站有多个语言副本时 [](../../help/sites-administering/tc-prep.md)，默认翻译服务不会识别在一个站点上输入的UGC可能与在另一个站点上输入的UGC相关，因为UGC实质上是由同一组件（包含该组件的页面的语言副本）生成的。

与参加一次对话的一个大组中的每个人相比，讨论一个主题的人群并不知道这些评论是在他们自己的组中做出的。

如果需要“一个组对话”，则可以跨具有多语言副本的网站启用全局翻译，这样，无论查看哪个语言副本，整个线程都可见。

例如，如果在基本站点上建立了论坛，创建了语言副本，并启用了全局翻译，则发布到论坛的主题（以一种语言副本制作）将显示在所有语言副本中。 任何回复也是如此，无论从哪种语言输入回复。 结果是，无论查看主题的语言副本来自何种语言，主题及其整个回复线程都将可见。

>[!CAUTION]
>
>在全局翻译之前存在的任何UGC都不再可见。
>
>虽然UGC仍位于公 [共商店](working-with-srp.md)，但它位于特定于语言的UGC位置下，而配置全局转换后添加的新内容则从全局共享商店位置检索。
>
>没有用于将特定语言的内容移动或合并到全局共享存储的迁移工具。


### 翻译集成配置 {#translation-integration-configuration}

要创建新的翻译集成，它将翻译服务连接器与创作实例上的网站相集成：

* 以管理员身份登录
* 从主 [菜单](http://localhost:4502/)
* 选择工 **[!UICONTROL 具]**
* 选择操 **[!UICONTROL 作]**
* 选择 **[!UICONTROL 云]**
* 选择 **[!UICONTROL 云服务]**
* 向下滚动到翻译 **[!UICONTROL 集成]**

   ![chlimage_1-65](assets/chlimage_1-65.png)

* 选择显 **[!UICONTROL 示配置]**

   ![chlimage_1-66](assets/chlimage_1-66.png)

* 选择“ `[+]` 可用配置” **[!UICONTROL 旁边的图标]** ，以创建新配置

#### 创建配置对话框 {#create-configuration-dialog}

![chlimage_1-67](assets/chlimage_1-67.png)

* **[!UICONTROL 父配置]**

   （必需）通常保留为默认值。 Default is `/etc/cloudservices/translation`.

* **[!UICONTROL 标题]**

   （必需）输入您选择的显示标题。 无默认值。

* **[!UICONTROL 名称]**

   （可选）输入配置的名称。 默认为基于标题的节点名称。

* Select **[!UICONTROL Create]**

#### 翻译配置对话框 {#translation-config-dialog}

![chlimage_1-68](assets/chlimage_1-68.png)

有关详细说明，请 [访问创建翻译集成配置](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)

* **[!UICONTROL “站点]** ”选项卡：可以保留为默认值。

* **[!UICONTROL “社区]** ”选项卡：
   * **[!UICONTROL 翻译提供]**&#x200B;者从下拉列表中选择翻译提供者。 默认为 `microsoft`试用服务。

   * **[!UICONTROL 内容类别]**&#x200B;选择描述要翻译的内容的类别。 Default is `General.`

   * **[!UICONTROL 选择区域设置……]**（可选）通过选择存储UGC的区域设置，来自所有语言副本的帖子将显示在一个全局对话中。 根据惯例，为网站的基 [本语言](sites-console.md#translation) 选择区域设置。 选择 `No Common Store` 将禁用全局翻译。 默认情况下，全局翻译处于禁用状态。

* **[!UICONTROL “资产]** ”选项卡：可以保留为默认值。
* 选择确 **[!UICONTROL 定]**

#### 激活 {#activation}

新的翻译集成云服务需要激活到发布环境。 当与网站关联时，如果尚未激活，则激活工作流会在与其关联的页面发布时提示发布此云服务配置。

## 管理翻译设置 {#managing-translation-settings}

>[!NOTE]
>
>**首选语言**
>
>为了检测帖子是否使用不同于首选语言的语言，必须建立网站访客的首选语言。
>
>首选语言是用户用户档案中设置的语言首选项，当站点访客登录并指定了语言首选项时。
>
>当站点访客为匿名内容或在其用户档案中未指定语言首选项时，首选语言是页面模板的基本语言。


### 用户首选项 {#user-preference}

#### 用户个人资料 {#user-profile}

所有社区站点都提供了用户用户档案，登录会员可以编辑该用户区域，以便向社区标识自己并设置其首选项。

一种设置是是否始终以其首选语言显示社区内容。 默认情况下，设置未设置，将默认为系统设置。 用户可以将设置更改为“开”或“关”，从而覆盖系统设置。

当页面自动翻译为用户首选语言时，用于显示原始文本和改进翻译的UI仍然可用。

![chlimage_1-69](assets/chlimage_1-69.png)

### 社区站点设置 {#community-site-setting}

创建社区站点后，可以启用和配置翻译选项。 翻译设置对于匿名网站访客可能视图的内容有效，但由用户的用户档案设置覆盖。
