---
title: 创建示例页面
seo-title: 创建示例页面
description: 创建示例社区站点
seo-description: 创建示例社区站点
uuid: 04a8f027-b7d8-493a-a9bd-5c4a6715d754
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
discoiquuid: a03145f7-6697-4797-b73e-6f8d241ce469
translation-type: tm+mt
source-git-commit: 56c2e6b55964ea5f3e180b17bd2a244882aa62ea
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 2%

---


# 创建示例页面 {#create-a-sample-page}

自AEM 6.1 Communities起，创建示例页面的最简单方法是创建一个简单的社区站点，该站点仅包含页面功能。

这将包括parsys组件，以便您能够启 [用组件进行创作](basics.md#accessing-communities-components)。

探索示例组件的另一种方法是使用“社区组件指南”中 [提供的功能](components-guide.md)。

## 创建社区站点 {#create-a-community-site}

这与创建新站点(如AEM Communities入门 [中所述)非常相似](getting-started.md)。

主要区别在于本教程将创建一个仅包含页面功能的 [新社区站点模板](functions.md#page-function) ，以创建一个简单的社区站点，该站点没有其他功能（除了所有社区站点基本的预连线功能）。

### 创建新站点模板 {#create-new-site-template}

要开始使用，请创建一个简 [单的社区站点模板](sites.md)。

从创作实例的全局导航中，选 **[!UICONTROL 择工具]** > **[!UICONTROL 社区]** > **[!UICONTROL 站点模板]**。

![chlimage_1-82](assets/chlimage_1-82.png)

* 选择 `Create button`
* 基本信息

   * `Name`: 单页模板
   * `Description`: 由单个页面功能组成的模板。
   * 选择 `Enabled`

![chlimage_1-83](assets/chlimage_1-83.png)

* 结构

   * 将函数 `Page` 拖动到Template Builder
   * 对于配置函数详细信息，输入

      * `Title`: 单页
      * `URL`: 页

![chlimage_1-84](assets/chlimage_1-84.png)

* 选 **`Save`** 择配置
* 选 **`Save`** 择站点模板

### 创建新社区站点 {#create-new-community-site}

现在，基于简单的站点模板创建一个新的社区站点。

创建站点模板后，从全局导航中选择“社 **[!UICONTROL 区”>“站点]**”。

![chlimage_1-85](assets/chlimage_1-85.png)

* 选择图 **`Create`** 标

* 步骤 `1 - Site Template`

   * `Title`: 简单社区站点
   * `Description`: 一个社区站点，它包含单个试验页面。
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: 样本

      * url = http://localhost:4502/content/sites/sample

      * `Template`: 选择 `Single Page Template`
      ![chlimage_1-86](assets/chlimage_1-86.png)


* 选择 `Next`
* 步骤 `2 - Design`

   * 选择任何设计

* 选择 `Next`
* 选择 `Next`

   （接受所有默认设置）

* 选择 `Create`

   ![chlimage_1-87](assets/chlimage_1-87.png)

## 发布站点 {#publish-the-site}

![chlimage_1-88](assets/chlimage_1-88.png)

从社区 [站点控制台](sites-console.md)，选择要发布站点的发布图标，默认情况下，该图标会发布到http://localhost:4503。

## 在编辑模式下打开作者网站 {#open-the-site-on-author-in-edit-mode}

![chlimage_1-89](assets/chlimage_1-89.png)

选择打开的站点图标以在编辑模式下视图站点。

该URL将为 [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![chlimage_1-90](assets/chlimage_1-90.png)

在简单的主页下，您可以查看通过社区功能和模板预先连接的内容，并尝试添加和配置社区组件。

## 视图发布站点 {#view-site-on-publish}

发布页面后，在发布实例上打 [开页面](http://localhost:4503/content/sites/sample/en.html) ，以匿名站点访客、登录成员或管理员的身份尝试这些功能。 除非管理员登录，否则在创作环境中可见的“管理”链接将不会显示在发布环境中。
