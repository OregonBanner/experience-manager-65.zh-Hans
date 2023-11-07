---
title: 编辑内容页面属性
description: 在Adobe Experience Manager中为页面定义所需的属性。
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1871'
ht-degree: 43%

---

# 编辑页面属性{#editing-page-properties}

您可以为页面定义所需的属性。这些属性会因页面性质而异。例如，某些页面可能已连接到Live Copy，而其他页面未连接到，因此Live Copy信息会根据需要变得可用。

## 页面属性 {#page-properties}

属性分布于多个选项卡中。

### 基本 {#basic}

* **标题**

  页面的标题会显示在各种不同的位置。 例如， **网站** 选项卡列表和 **站点** 卡片/列表视图。

  这是必填字段。

* **标记**

  在此，可以通过更新选择框中的列表在页面中添加或删除标记：

   * 选择某个标记后，该标记会列在选择框的下方。 您可以使用“x”从此列表中移除标记。
   * 通过在空的选择框中键入名称可输入新标记。

      * 当您按Enter键时，将创建新标记。
      * 新标记将在右侧显示一个小星号，指示它是新标记。

   * 利用下拉功能，您可以从现有标记中进行选择。
   * 当您将鼠标悬停在选择框中的标记条目上时，会显示 x，用于为此页面删除该标记。

  有关标记的更多信息，请访问[使用标记](/help/sites-authoring/tags.md)。

* **隐藏导航**

  指示在生成的站点的页面导航中是显示还是隐藏页面。

* **品牌化**

  通过将品牌概要附加到每个页面标题，跨页面应用一致的品牌识别。此功能需要使用 2.14.0 版或更高版本的[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)中的页面组件。

   * **覆盖** – 选中可在此页面上定义品牌概要。
      * 该值会由任何子页面继承，除非它们也设置了&#x200B;**覆盖**&#x200B;值。
   * **覆盖值** – 要附加到页面标题的品牌概要的文本。
      * 该值附加到页面标题后的竖线字符后，例如“骑行 Tuscany | 始终准备好使用 WKND”
* **页面标题**

  要在页面上使用的标题。 通常由标题组件使用。如果留空，则会使用&#x200B;**标题**。

* **导航标题**

  您可以指定单独的标题以便在导航中使用（例如，当您希望某些内容能更加简洁时）。 如果留空，则会使用&#x200B;**标题**。

* **子标题**

  要在页面上使用的子标题。

* **描述**

  页面的描述、用途或要添加的任何其他详细信息。

* **开始时间**

  激活已发布页面的日期和时间。 发布后，此页面在指定时间之前一直处于休眠状态。

  对于要立即发布的页面（正常场景），请将这些字段留空。

* **结束时间**

  已发布页面被停用时的时间。

  再次将这些字段留空以便立即执行操作。

* **虚 URL**

  输入此页面的虚URL，这样可让您的URL长度更短和/或更具有表现性。

  例如，如果将虚URL设置为 `welcome`到由路径标识的页面 `/v1.0/startpage`用于网站 `http://example.com,` 则 `http://example.com/welcome`将成为的虚URL `http://example.com/content/v1.0/startpage`

  >[!CAUTION]
  >
  >虚 URL：
  >
  >* 必须是唯一的。 确保其他页面尚未使用该值。
  >* 不支持正则表达式模式。
  >* 不应设置为现有页面。
  >

  配置Dispatcher以启用对虚名URL的访问。 请参阅 [启用对虚名URL的访问](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls) 以了解更多详细信息。

* **重定向虚 URL**

  指示您是否希望页面使用虚 URL。

### 高级 {#advanced}

* **语言**

  页面语言。

* **语言根目录**

  如果页面是语言副本的根，则必须选中。

* **重定向**

  指示此页面应自动重定向到的页面。

* **Design**

  指示 [设计](/help/sites-developing/designer.md) 将用于此页面。

* **别名**

  指定要用于此页面的别名。

   * 例如，如果您为页面 `/content/wknd/us/en/magazine/members-only` 定义别名 `private`，则也可以通过 `/content/wknd/us/en/magazine/private` 访问此页面
   * 创建别名将设置页面节点上的 `sling:alias` 属性，这只会影响资源，而不会影响存储库路径。
   * 无法发布编辑器中按别名处理的页面。编辑器中的[发布选项](/help/sites-authoring/publishing-pages.md)仅适用于通过其实际路径访问的页面。
   * 有关更多详细信息，请参阅 [SEO和URL管理最佳实践下的本地化页面名称](/help/managing/seo-and-url-management.md#localized-page-names).

* **继承自&lt;*路径*>**

  指示是否继承页面。 以及来自何处。

* **云配置**

  配置的路径。

* **允许的模板**

  [定义可用的模板列表](/help/sites-authoring/templates.md#allowingatemplate) 在该支行内。

* **启用** （身份验证要求）

  启用（或禁用）身份验证，以便您可以访问该页面。

  >[!NOTE]
  >
  >页面的已关闭的用户组在&#x200B;**[权限](/help/sites-authoring/editing-page-properties.md#permissions)**&#x200B;选项卡上定义。

  >[!CAUTION]
  >
  >此 **[权限](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** 选项卡允许根据是否存在 `granite:AuthenticationRequired` mixin。 如果页面权限是使用已弃用的CUG配置进行配置，则根据是否存在 `cq:cugEnabled` 属性，下将显示一条警告消息 **身份验证要求** 并且选项不可编辑，也不是 [权限](/help/sites-authoring/editing-page-properties.md#permissions) 可编辑。
  >
  >
  >在这种情况下，必须在中编辑CUG权限 [经典UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

* **登录页面**

  用于登录的页面。

* **导出配置**

  指定导出配置。

### 缩略图 {#thumbnail}

显示页面缩略图图像。 您可以：

* **生成预览**

  生成要用作缩略图的页面预览。

* **上传图像**

  上传要用作缩略图的图像。

* **选择图像**

  选择要用作缩略图的现有资源。

* **还原**

  在更改缩略图后，此选项将变得可用。 如果不想保留您的更改，可以在保存前还原更改。

### 社交媒体 {#social-media}

* **社交媒体共享**

  定义页面上可用的共享选项。 显示可用于的选项 [共享核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/sharing.html?lang=en).

   * **为Facebook启用用户共享**
   * **为Pinterest启用用户共享**
   * **首选体验片段变量**
定义用于为页面生成元数据的体验片段变量

### Cloud Service {#cloud-services}

* **Cloud Service**

  定义属性 [云服务](/help/sites-developing/extending-cloud-config.md).

### 个性化 {#personalization}

* **ContextHub 配置**

  选择 [ContextHub配置](/help/sites-developing/ch-configuring.md) 和 [区段路径](/help/sites-administering/segmentation.md).

* **定位配置**

  选择一个[品牌以指定定位的范围](/help/sites-authoring/target-adobe-campaign.md)。

  >[!NOTE]
  >此选项要求用户帐户属于 `Target Adminstrators` 组。

### 权限 {#permissions}

* **权限**

  在此选项卡中，您可以：

   * [添加权限](/help/sites-administering/user-group-ac-admin.md)
   * [编辑已关闭的用户组](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * 查看[有效权限](/help/sites-administering/user-group-ac-admin.md)

  >[!CAUTION]
  >
  >此 **权限** 选项卡允许根据是否存在以下项编辑CUG配置 `granite:AuthenticationRequired` mixin。 如果页面权限是使用已弃用的CUG配置进行配置，则根据是否存在 `cq:cugEnabled` 属性，将显示一条警告消息，并且CUG权限不可编辑，上的身份验证要求也不是 [高级](/help/sites-authoring/editing-page-properties.md#advanced) 选项卡可编辑。
  >
  >
  >在这种情况下，必须在中编辑CUG权限 [经典UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

  >[!NOTE]
  >
  >“权限”选项卡不允许创建空的CUG组，通过这种简单的方式可以拒绝每个用户访问。 为此，必须使用CRX Explorer。 查看文档 [用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md) 以了解更多信息。

### Blueprint {#blueprint}

* **Blueprint**

  在中定义Blueprint页面的属性 [多站点管理](/help/sites-administering/msm.md). 控制将修改传播到Live Copy的情况。

### Live Copy {#live-copy}

* **Live Copy**

  在中定义Live Copy页面的属性 [多站点管理](/help/sites-administering/msm.md). 控制从Blueprint传播修改的情况。

### 站点结构 {#site-structure}

* 提供具有全站点功能的页面的链接，例如 **注册页面**， **脱机页面**，等等。

## 编辑页面属性 {#editing-page-properties-1}

您可以定义页面属性：

* 从&#x200B;**Sites**&#x200B;控制台中：

   * [创建页面](/help/sites-authoring/managing-pages.md#creating-a-new-page) （一部分资产）

   * 单击或点按&#x200B;**属性**

      * 单页面
      * 多个页面（只有一部分属性可用于整体编辑）

* 从页面编辑器中：

   * 使用&#x200B;**页面信息**（然后&#x200B;**打开属性**）

### 从 Sites 控制台中 – 单个页面 {#from-the-sites-console-single-page}

单击或点按&#x200B;**属性**&#x200B;以定义页面属性：

1. 使用&#x200B;**Sites**&#x200B;控制台，导航到要查看和编辑属性的页面位置。

1. 使用以下任一方式为所需的页面选择&#x200B;**属性**&#x200B;选项：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#selectionmode)

   此时会使用相应的选项卡显示页面属性。

1. 查看或编辑所需的属性。

1. 然后使用 **保存** 以保存您的更新，然后 **关闭** 以便返回控制台。

### 编辑页面时 {#when-editing-a-page}

在编辑页面时，您可以使用 **页面信息** 要定义页面属性，请执行以下操作：

1. 打开要编辑属性的页面。

1. 选择&#x200B;**页面信息**&#x200B;图标以打开选择菜单：

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. 选择 **打开属性** 此时将打开一个对话框，允许您编辑按相应选项卡排序的属性。 工具栏右侧还提供以下按钮：

   * **取消**
   * **保存并关闭**

1. 使用&#x200B;**保存并关闭**&#x200B;按钮以保存更改。

### 从 Sites 控制台中 – 多个页面 {#from-the-sites-console-multiple-pages}

从 **站点** 控制台中，您可以选择多个页面，然后使用 **查看属性** 查看和/或编辑页面属性。 这称为批量编辑页面属性。

>[!NOTE]
>
>也可以对资源使用批量编辑属性功能。两者相似，但在几个方面有所不同。 请参阅 [编辑多个资产的属性](/help/assets/metadata.md) 以了解详细信息。
>
>还有 [批量编辑器](/help/sites-administering/bulk-editor.md). 通过此编辑器，您可以使用GQL(Google查询语言)从多个页面搜索内容，然后直接使用批量编辑器编辑内容，再将更改保存到原始页面。

可以通过多种方法选择要批量编辑的多个页面，这些方法包括：

* 在浏览 **Sites** 控制台时
* 在使用&#x200B;**搜索**&#x200B;找到一组页面后

![epp-01](assets/epp-01.png)

选择页面后，单击或点按&#x200B;**属性选项**，此时会显示批量属性：

![epp-02](assets/epp-02.png)

只有符合以下条件的页面才能进行批量编辑：

* 属于同一资源类型
* 不是 Live Copy 的一部分

   * 如果有任何页面在 Live Copy 中，则会在属性打开时显示一条消息。

进入“批量编辑”后，可以执行以下操作：

* **查看**

  查看多个页面的页面属性时，您可以看到以下内容：

   * 受影响的页面列表

      * 您可以根据需要进行选择/取消选择

   * 选项卡

      * 与查看单页面的属性时一样，这些属性按选项卡进行排序。

   * 一部分属性

      * 将显示所有选定页面的可用属性，这些属性已明确定义为可批量编辑。
      * 如果将选择的页面减少到一页，则会显示所有属性。

   * 具有相同值的通用属性

      * 在“查看”模式中，只显示具有相同值的属性。
      * 当字段有多个值时（例如，“标记”），则仅在以下情况下显示值 *所有* 很常见。 如果只有一些是通用的，则仅在编辑时才显示它们。

  如果不存在具有相同值的属性，则会显示一条消息。

* **编辑**

  编辑多个页面的页面属性时：

   * 您可以更新可用字段中的值。

      * 当您选择&#x200B;**完成**&#x200B;时，新值会应用于所有选定页面。
      * 当字段有多个值时（例如，“标记”），您可以附加新值或删除公共值。

   * 如果不同页面具有相同的字段，但这些字段的值不同，则会用一个特殊的值表示它们，例如文本 `<Mixed Entries>`.

>[!NOTE]
>
>可以对页面组件进行配置，以指定可批量编辑的字段。请参阅 [配置页面以批量编辑页面属性](/help/sites-developing/bulk-editing.md).
