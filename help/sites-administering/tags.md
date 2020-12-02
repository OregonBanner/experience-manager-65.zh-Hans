---
title: 管理标记
seo-title: 管理标记
description: 了解如何在AEM中管理标记。
seo-description: 了解如何在AEM中管理标记。
uuid: 77e1280a-feea-4edd-94b6-4fb825566c42
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 69253ee9-8c28-436b-9331-6fb875f64cba
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 5%

---


# 管理标记{#administering-tags}

标记是用于对网站中的内容进行分类的简单快捷方法。可以将它们视为关键字或标签（元数据），以便在搜索结果中更快地找到内容。

在Adobe Experience Manager(AEM)中，标签可以是

* 页面的内容节点（请参阅[使用标记](/help/sites-authoring/tags.md)）

* 资产的元数据节点（请参阅[管理数字资产的元数据](/help/assets/metadata.md)）

除了页面和资产外，标记还用于AEM Communities功能

* 用户生成的内容（请参阅[标记UGC）](/help/communities/tag-ugc.md)

* Enablement Resources（请参阅[标记Enablement Resources](/help/communities/functions.md#catalog-function)）

## 标记功能{#tag-features}

AEM中标记的一些功能包括：

* 标记可分为多种命名空间。 通过此类层次结构可以构建分类。这些分类在整个AEM中都是全球性的。
* 新创建标记的主要限制是它们在特定命名空间中必须是唯一的。
* 标记的标题不应包含标记路径分隔字符（如果存在，也将显示它们）

   * 冒号`:` —— 分隔命名空间标记
   * 正斜杠`/` —— 分隔子标签

* 标记可由作者和站点访客应用。 在分配给页面或进行搜索时，所有形式的标记都可供选择，与其创建者无关。
* “tag-administrators”组的成员和对`/content/cq:tags`具有修改权限的成员可以创建标记并修改其分类。

   * 包含子标记的标记称为容器标记
   * 非容器标签的标签称为叶标签
   * 标签命名空间是叶标签或容器标签

* [搜索组件](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html)使用标记来方便查找内容。
* [Teaser组件](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html)使用标记，它监视用户的标记云以提供目标内容。
* 如果标记是内容的重要方面

   * 确保将标记打包到使用这些标记的页面
   * 确保[标记权限](#setting-tag-permissions)启用读取访问

## 标记控制台{#tagging-console}

“标记”控制台用于创建和管理标记及其分类。 一个目标是避免与基本相同的事情相关的许多类似标签：例如，页面和页面，鞋类和鞋。

通过将标记分组到命名空间中、在创建新标记之前查看现有标记的使用情况以及在不断开标记与当前引用内容的连接的情况下重新组织来管理标记。

要访问Tagging控制台，请执行以下操作：

* 在作者
* 以管理权限登录
* 从全局导航

   * 选择&#x200B;**`Tools`**
   * 选择&#x200B;**`General`**
   * 选择&#x200B;**`Tagging`**

![managing_tags_usingthetagasministrationconsole](assets/managing_tags_usingthetagasministrationconsolea.png)

### 创建命名空间{#creating-a-namespace}

要创建新命名空间，请选择&#x200B;**`Create Namespace`**&#x200B;图标。

命名空间本身是一个标记，不需要包含任何子标记。 但是，要继续创建分类，[创建子标签](#creating-tags)，子标签又可以是leaf标签或容器标签。

![chlimage_1-183](assets/chlimage_1-183a.png) ![ creating_tags_andnamespaces](assets/creating_tags_andnamespacesa.png)

* **标题**

   *（必需）* 命名空间的显示标题。

* **名称**
   *（可选）* 命名空间的名称。如果未指定，则从标题创建有效节点名称。 请参阅[TagID](/help/sites-developing/framework.md#tagid)。

* **描述**

   *（可选）* 命名空间的描述。

输入所需信息后

* 选择&#x200B;**创建**

### 对标记{#operations-on-tags}的操作

选择命名空间或其他标记可执行以下操作：

* [查看属性](#viewing-tag-properties)
* [引用](#showing-tag-references)
* [创建标记](#creating-tags)
* [编辑](#editing-tags)
* [移动](#moving-tags)
* [合并](#merging-tags)
* [发布](#publishing-tags)
* [取消发布](#unpublishing-tags)
* [删除](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

当浏览器窗口的宽度不足以显示所有图标时，最右边的图标将组合在&#x200B;**`... More`**&#x200B;图标下，该图标将显示隐藏操作图标的下拉列表。

![chlimage_1-185](assets/chlimage_1-185.png)

### 选择命名空间标记{#selecting-a-namespace-tag}

首次选择时，如果命名空间不包含任何标记，则属性显示在右侧，否则显示子标记。 所选的每个标记将显示其包含的标记或其属性（如果它没有子标记）。

要选择操作的标记，并要进行多选，请仅选择标题旁的图标。 选择标题将仅显示属性或打开标记以显示其内容。

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### 查看标记属性{#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

选择命名空间或其他标记后，选择&#x200B;**`View Properties`**&#x200B;图标会显示有关`name`、上次编辑时间和引用数的信息。 如果已发布，则显示上次发布的时间和发布者的id。 此信息将显示在标记列左侧的列中。

![chlimage_1-109](assets/chlimage_1-189.png)

### 显示标记引用{#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

选择命名空间或其他标记后，选择&#x200B;**引用**&#x200B;图标将标识已应用标记的内容。

初始显示是应用的标记计数。

![chlimage_1-111](assets/chlimage_1-191.png)

通过选择计数右侧的箭头，将列出引用名称。

将鼠标悬停在参照上时，参照的路径将显示为工具提示。

![chlimage_1-112](assets/chlimage_1-192.png)

### 创建标记{#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

当选择命名空间或其他标记（通过选择标题旁的图标）时，可以通过选择&#x200B;**`Create Tag`**&#x200B;图标为当前标记创建子标记。

![chlimage_1-194](assets/chlimage_1-194.png)

* **标题**
*（必需）*标记的显示标题。

* **名称**
*（可选）*标记的名称。如果未指定，则从标题创建有效节点名称。 请参阅[TagID](/help/sites-developing/framework.md#tagid)。

* **描述**
*（可选）*标记的描述。

输入所需信息后

* 选择&#x200B;**创建**

### 编辑标记 {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

选择命名空间或其他标记后，可以更改标题、说明，并通过选择**`Edit`**图标提供标题的本地化。

进行编辑后，选择&#x200B;**保存**。

有关添加语言翻译的详细信息，请参阅[管理不同语言的标记](#managing-tags-in-different-languages)一节。

![chlimage_1-196](assets/chlimage_1-196.png)

### 移动标记 {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

选择命名空间或其他标记后，选择&#x200B;**`Move`**&#x200B;图标将允许标记管理员和开发人员通过将标记移动到新位置或重命名来清理分类。 当所选标记是容器标记时，移动标记也会移动所有子标记。

>[!NOTE]
>
>建议仅允许作者编辑[标记的`title`](#editing-tags)，而不要移动或重命名标记。

![chlimage_1-198](assets/chlimage_1-198.png)

* **路径**

   *（只读）* 选定标记的当前路径。

* **移**
动到浏览到要移动标记的新路径。

* **重命**
名为最初显示当前 
`name`标签。可以输入新的`name`。

* 选择&#x200B;**保存**

### 合并标记 {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

当有重复的分类时，可以使用合并标记。当标记A合并到标记B中时，使用标记A标记的所有页面都将使用标记B标记，并且标记A不再对作者可用。

选择命名空间或其他标记后，选择&#x200B;**合并**&#x200B;图标将打开一个面板，其中可以选择要合并到其中的路径。

![chlimage_1-200](assets/chlimage_1-200.png)

* **路径**

   *（只读）* 选定要合并到其他标记中的标记的路径。

* **合并**
到浏览以选择要合并到的标记的路径。

>[!NOTE]
>
>合并后，最初选择的&#x200B;**路径**&#x200B;将（实际上）不再存在。
>
>移动或合并引用的标记时，该标记不会物理删除，因此可以保留引用。

### 发布标记 {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

选择命名空间或其他标记后，选择&#x200B;**发布**&#x200B;图标以在发布环境中激活标记。 与页面内容类似，只发布选定的标记，而不管它是否是容器标记。

要发布分类(命名空间和子标签)，最佳做法是创建命名空间的[包](/help/sites-administering/package-manager.md)（请参阅[分类根节点](/help/sites-developing/framework.md#taxonomy-root-node)）。 在创建包之前，请务必[将权限](#setting-tag-permissions)应用到命名空间。

### 取消发布标记{#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

选择命名空间或其他标记后，选择&#x200B;**取消发布**&#x200B;图标将取消激活创作环境中的标记，并将其从发布环境中删除。 与`Delete`操作类似，如果所选标记是容器标记，则其所有子标记将在创作环境中停用并从发布环境中删除。

### 删除标记 {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

选择命名空间或其他标记后，选择&#x200B;**删除**&#x200B;图标将从创作环境永久删除标记。 如果标记已发布，则也会从发布环境中删除该标记。 如果所选标记是容器标记，则其所有子标记也将被删除。

## 设置标记权限{#setting-tag-permissions}

标记权限为[&#39;secure（默认）&#39;](/help/sites-administering/production-ready.md);发布环境的最佳实践，它要求明确允许标记读取权限。 基本上，这是通过在对作者设置权限后创建标记命名空间的包，并在所有发布实例上安装该包来完成的。

* 在创作实例中

   * 以管理权限登录
   * 访问[安全控制台](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

      * 例如，浏览到http://localhost:4502/useradmin
   * 在左窗格中，选择要授予[读权限](/help/sites-administering/security.md#permissions)的组（或用户）
   * 在右窗格中，找到“标记”命名空间的**路径**

      * 例如`/content/cq:tags/mycommunity`
   * 在&#x200B;**读取**&#x200B;列中选择`checkbox`
   * 选择&#x200B;**保存**



![chlimage_1-204](assets/chlimage_1-204.png)

* 确保所有发布实例具有相同的权限

   * 一种方法是创建作者命名空间的[包](/help/sites-administering/package-manager.md#package-manager)

      * 在`Advanced`选项卡上，对于`AC Handling`，选择`Overwrite`
   * 复制包

      * 从包管理器中选择`Replicate`


## 管理不同语言的标记 {#managing-tags-in-different-languages}

标记的`title`属性可以翻译为多种语言。 翻译后，可根据用户语言或页面语言显示相应的标签`title`。

### 用多种语言定义标记标题 {#defining-tag-titles-in-multiple-languages}

下面介绍如何将标记&#x200B;**Animals**&#x200B;的`title`从英语翻译成德语和法语。

开始，在&#x200B;**图片库**&#x200B;命名空间下选择标记，然后选择**`Edit`**图标（请参阅[编辑标记](#editing-tags)部分）。

“编辑标记”面板提供选择标记标题本地化为的语言的功能。

当选择每种语言时，将显示一个文本输入框，可在其中输入译文标题。

输入所有转换后，选择&#x200B;**保存**&#x200B;退出编辑模式。

![chlimage_1-205](assets/chlimage_1-205.png)

通常，为标记选择的语言是从页面语言（如果有）中获取的。 当在其他情况下（例如在表单或对话框中）使用[ `tag`构件](/help/sites-developing/building.md#tagging-on-the-client-side)时，标记语言取决于上下文。

Tagging控制台不使用页面语言设置，而是使用用户语言设置。 在“标记”控制台中，对于“Animals”标记，将为用户属性中将语言设置为法语的用户显示“Animaux”。

要向对话框添加新语言，请参阅[向“编辑标记”对话框添加新语言](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog)。

>[!NOTE]
>
>标准页面组件中的标记云和元关键字根据页面语言使用本地化的标记`titles`（如果可用）。

## 资源 {#resources}

* [为开发人员添加标签](/help/sites-developing/tags.md)

   有关标记框架以及在自定义应用程序中扩展和包括标记的信息。

* [经典UI标记控制台](/help/sites-administering/classic-console.md)

