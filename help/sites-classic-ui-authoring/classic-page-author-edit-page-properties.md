---
title: 编辑页面属性
description: 页面的属性可能会因页面的性质而异。 例如，某些页面可能已连接到Live Copy，而其他页面则未连接，Live Copy信息将根据需要提供。
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
exl-id: 1a77e4cd-bbf8-4d05-bb35-fd43c02eaf30
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 26%

---

# 编辑页面属性{#editing-page-properties}

您可以为页面定义所需的属性。这些属性会因页面性质而异。例如，某些页面可能会连接到 Live Copy，而其他页面则可能不会，Live Copy 信息将在适当情况下才可用。

## 页面属性 {#page-properties}

属性分布在多个选项卡中：

### 基本 {#basic}

* **标题**

   页面的标题会显示在不同的位置。 例如， **网站** 选项卡列表和 **站点** 卡片/列表视图。

   这是必填字段。

* **标记**

   在此，您可以通过更新选择框中的列表在页面中添加或删除标记：

   * 选择标记后，它会列在选择框下。您可以使用“x”从此列表中移除标记。
   * 可通过在空白选择框中键入名称输入全新标记。

      按Enter将实际创建新标记。 随后，新标记将显示在框中，右侧带有一个小星形，表示该标记为新标记。

   * 使用下拉列表功能，可从现有标记中进行选择。
   * 将鼠标悬停在选择框中的标记条目上时，会显示x;这可用于删除此页面的该标记。

* **隐藏导航**

   一个切换开关，用于指示在页面导航中是显示还是隐藏页面。

* **页面标题**

   要在页面上使用的标题。

* **导航标题**

   您可以指定单独的标题以在导航中使用（例如，如果您希望某些内容能更加简洁）。 如果为空，则 **标题** 中，将使用。

* **子标题**

   要在页面上使用的子标题。

* **描述**

   您对页面的描述、用途或要添加的任何其他详细信息。

* **开始时间**

   激活已发布页面的日期和时间。 发布后，此页面在指定的时间之前将保持休眠。

   对于要立即发布的页面，请将这些字段留空（正常情况）。

* **结束时间**

   将停用已发布页面的时间。

   对于要立即发布的页面，请再次将这些字段留空。

* **虚 URL**

   允许您为此页面输入虚URL。 这样，您的URL就更短、表达更清楚。

   例如，如果虚URL设置为w `elcome`到路径/标识的页面 `v1.0/startpage`网站h `ttp://example.com,` 然后 `ttp://example.com/welcome`应该是h的虚URL `ttp://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >虚 URL：
   >
   >* 必须是唯一的，因此您应该注意该值尚未被其他页面使用。
   >* 不支持正则表达式模式。


* **重定向虚 URL**

   指示您是否希望页面使用虚 URL。

### 高级 {#advanced}

* **语言**

   页面语言。

* **重定向**

   指示此页面应自动重定向到的页面。

* **Design**

   指示 [设计](/help/sites-developing/designer.md) 用于此页面。

* **别名**

   指定要用于此页的别名。

* **启用已关闭的用户组**

   启用（或禁用） [封闭用户组](/help/sites-administering/cug.md) (CUG)。

* **登录页面**

   要用于登录的页面。

* **公认组**

   有资格登录CUG的组。

* **领域**

   CUG的领域名称。

* **导出配置**

   指定导出配置。

### 缩略图 {#thumbnail}

* **页面缩略图**

   显示页面缩略图图像。 您可以：

   * **生成预览**

      生成要用作缩略图的页面预览。

   * **上传图像**

      上传要用作缩略图的图像。

### Cloud Service {#cloud-services}

* **Cloud Service**

   为定义属性 [云服务](/help/sites-developing/extending-cloud-config.md).

### 个性化 {#personalization}

* **个性化**

   选择一个[品牌以指定定位的范围](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)。

### 权限 {#permissions}

* **权限** （触屏优化UI）

   查看 [有效权限和添加新权限](/help/sites-administering/user-group-ac-admin.md).

### Blueprint {#blueprint}

* **Blueprint**

   为 [多站点管理](/help/sites-administering/msm.md). 控制将修改传播到Live Copy的情况。

### Live Copy {#live-copy}

* **Live Copy**

   为 [多站点管理](/help/sites-administering/msm.md). 控制将从Blueprint中传播修改的情况。

### 站点结构 {#site-structure}

* 提供具有全站点功能的页面的链接，例如&#x200B;**注册页面**、**脱机页面**&#x200B;以及其他。

## 编辑页面属性 {#editing-page-properties-2}

### 编辑特定页面的页面属性 {#editing-page-properties-for-a-specific-page}

页面属性定义页面在网站和其他页面上显示时的各种属性，如标题。

1. 打开要编辑的页面。

1. 在Sidekick中，打开 **页面** 选项卡，然后选择 **页面属性……**

   这将打开一个包含多个选项卡的对话框。

1. 进行所需的更改，然后单击 **确定** 保存。
