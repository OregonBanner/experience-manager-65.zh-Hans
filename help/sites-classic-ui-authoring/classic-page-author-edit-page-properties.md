---
title: 编辑页面属性
seo-title: 编辑页面属性
description: 页面属性会因页面性质而异。例如，某些页面可能会连接到 Live Copy，而其他页面则可能不会，Live Copy 信息将在适当情况下才可用。
seo-description: 页面属性会因页面性质而异。例如，某些页面可能会连接到 Live Copy，而其他页面则可能不会，Live Copy 信息将在适当情况下才可用。
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 编辑页面属性{#editing-page-properties}

您可以为页面定义所需的属性。这些属性会因页面性质而异。例如，某些页面可能会连接到 Live Copy，而其他页面则可能不会，Live Copy 信息将在适当情况下才可用。

## 页面属性 {#page-properties}

属性分布于多个选项卡：

### 基本 {#basic}

* **标题**

   页面的标题会显示在各种不同的位置。例如，**网站**&#x200B;选项卡列表和&#x200B;**站点**&#x200B;卡片/列表视图。

   这是必填字段。

* **标记**

   在此，可以通过更新选择框中的列表在页面中添加或删除标记：

   * 选择标记后，它会列在选择框下。您可以使用“x”从此列表中删除标记。
   * 可通过在空白选择框中键入名称输入全新标记。

      按 Enter 将实际创建新标记。新标记随后将显示在框中，并且右侧带有一个小星星，表示该标记为新标记。

   * 使用下拉列表功能，可从现有标记中进行选择。
   * 当您将鼠标停留在选择框中的标记条目之上时，会显示 x；此 x 可用于为此页面删除该标记。

* **隐藏导航**

   一个切换开关，用于指示在页面导航中显示还是隐藏页面。

* **页面标题**

   要在页面中使用的标题。

* **导航标题**

   您可以指定单独的标题以便在导航中使用（例如，如果您想用一种更加简洁明了的说法）。如果留空，则将使用&#x200B;**标题**。

* **子标题**

   要在页面中使用的子标题。

* **描述**

   页面的描述、用途或要添加的任何其他详细信息。

* **开始时间**

   将激活已发布页面的日期和时间。发布后，此页面在指定时间之前将一直保持休眠。

   对于要立即发布的页面，将这些字段保留为空（正常情况）。

* **结束时间**

   将取消激活已发布页面的时间。

   对于要立即发布的页面，也将这些字段保留为空。

* **虚 URL**

   允许您为此页面输入虚 URL。通过这种方式，您可以使用更短并且含意更清楚的 URL。

   例如，如果虚URL设置为w, `elcome`则对于网站h，如果路径/ `v1.0/startpage`标识的页面 `ttp://example.com,` h，则h `ttp://example.com/welcome`应该是h的虚URL `ttp://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >虚 URL：
   >
   >* 必须是唯一的，因此您应该确保该值没有被其他页面使用。
   >* 不支持正则表达式模式。


* **重定向虚 URL**

   指示您是否希望页面使用虚 URL。

### 高级 {#advanced}

* **语言**

   页面语言。

* **重定向**

   指示此页面应自动重定向到的页面。

* **设计**

   指示要用于此页面的[设计](/help/sites-developing/designer.md)。

* **别名**

   指定要用于此页面的别名。

* **启用已关闭的用户组**

   启用（或禁用）[已关闭的用户组](/help/sites-administering/cug.md) (CUG)。

* **登录页面**

   要用于登录的页面。

* **公认组**

   有资格登录 CUG 的组。

* **领域**

   用于 CUG 的领域名称。

* **导出配置**

   指定导出配置。

### 缩略图 {#thumbnail}

* **页面缩略图**

   显示页面缩略图图像。您可以：

   * **生成预览**

      生成要用作缩略图的页面预览。

   * **上传图像**

      上传要用作缩略图的图像。

### 云服务 {#cloud-services}

* **云服务**

   为[云服务](/help/sites-developing/extending-cloud-config.md)定义属性。

### 个性化 {#personalization}

* **个人信息**

   选择一个[品牌以指定定位的范围](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)。

### 权限 {#permissions}

* **权限**（触屏优化 UI）

   查看[有效权限，以及添加新权限](/help/sites-administering/user-group-ac-admin.md)。

### Blueprint {#blueprint}

* **Blueprint**

   在[多站点管理](/help/sites-administering/msm.md)中为 Blueprint 页面定义属性。控制将修改传播到 Live Copy 的情况。

### Live Copy {#live-copy}

* **Live Copy**

   在[多站点管理](/help/sites-administering/msm.md)中为 Live Copy 页面定义属性。控制将从 Blueprint 中传播修改的情况。

### 站点结构 {#site-structure}

* 提供具有全站点功能的页面的链接，例如&#x200B;**注册页面**、**脱机页面**&#x200B;以及其他。

## 编辑页面属性 {#editing-page-properties-2}

### 编辑特定页面的页面属性 {#editing-page-properties-for-a-specific-page}

页面属性定义页面在网站和其他位置显示时的各个属性，如标题。

1. 打开要编辑的页面。

1. 在 Sidekick 中，打开“**页面**”选项卡，然后选择“**页面属性...**”

   这会打开一个包含多个选项卡的对话框。

1. 进行所需的更改，然后单击“**确定**”以保存。

