---
title: 准备内容以进行翻译
seo-title: Preparing Content for Translation
description: 了解如何准备内容以进行翻译。
seo-description: Learn how to prepare content for translation.
uuid: 369630a8-2ed7-48db-973e-bd8213231d49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 8bd67d71-bcb7-4ca0-9751-3ff3ee054011
feature: Language Copy
exl-id: 81978733-89a6-4436-bcf1-4bde962ed54f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 61%

---

# 准备内容以进行翻译{#preparing-content-for-translation}

多语言网站通常以多种语言提供一定数量的内容。使用一种语言创作该站点的内容，然后将此内容翻译成其他语言。通常，多语言站点包含多个页面分支，每个分支均包含采用其他语言的站点页面。

示例Geometrixx演示网站包含多个语言分支，并使用以下结构：

```xml
/content
    |- geometrixx
             |- en
             |- fr
             |- de
             |- es
             |- it
             |- ja
             |- zh
```

站点的每个语言分支均称为语言副本。语言副本的根页面（称为语言根）标识了语言副本中内容的语言。例如，`/content/geometrixx/fr` 是法语副本的语言根。语言副本必须使用[准确配置的语言根](/help/sites-administering/tc-prep.md#creating-a-language-root)，以便在翻译源站点内容时使用正确的语言。

您最初为其创作站点内容的语言副本是语言母版。语言母版是翻译成其他语言的源。

使用以下步骤可准备站点以进行翻译：

1. 创建语言母版的语言根。例如，英语Geometrixx演示站点的语言根目录为/content/geometrixx/en。 确保根据[创建语言根](/help/sites-administering/tc-prep.md#creating-a-language-root)中的信息来正确配置语言根。
1. 创作语言母版的内容。
1. 创建站点的每个语言副本的语言根。例如，Geometrixx示例站点的法语语言副本为/content/geometrixx/fr。

准备好内容以进行翻译后，您可以在语言副本和相关翻译项目中自动创建缺失的页面。（请参阅[创建翻译项目](/help/sites-administering/tc-manage.md)。）有关 AEM 中内容翻译过程的概述，请参阅[翻译多语言网站的内容](/help/sites-administering/translation.md)。

## 创建语言根 {#creating-a-language-root}

创建语言根作为标识了内容语言的语言副本的根页。创建语言根后，您可以创建包含语言副本的翻译项目。

要创建语言根，您需要创建一个页面并使用 ISO 语言代码作为名称属性的值。语言代码必须采用下列格式之一：

* `<language-code>`支持的语言代码是由ISO-639-1定义的双字母代码，例如 `en`.

* `<language-code>_<country-code>` 或 `<language-code>-<country-code>`支持的国家/地区代码是ISO 3166定义的小写或大写双字母代码，例如 `en_US`, `en_us`, `en_GB`, `en-gb`.

根据您为全球站点选择的结构，您可以使用任一格式。例如，Geometrixx站点的法语语言副本的根页面具有 `fr` 作为Name属性。 请注意， Name属性将用作存储库中页面节点的名称，从而确定页面的路径。 (http://localhost:4502/content/geometrixx/fr.html)

以下过程使用触屏优化UI创建网站的语言副本。 有关使用经典UI的说明，请参阅 [使用经典UI创建语言根](/help/sites-administering/tc-lroot-classic.md).

1. 导航到站点。
1. 单击或点按要为其创建语言副本的站点。

   例如，要创建Geometrixx Outdoors网站的语言副本，您可以单击或点按Geometrixx Outdoors网站。

1. 单击或点按创建，然后单击或点按创建页面。

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. 选择页面模板，然后单击或点按下一步。
1. 在名称字段中，用 `<language-code>` 或 `<language-code>_<country-code>` 格式键入国家/地区代码，例如 `en`、`en_US`、`en_us`、`en_GB`、`en_gb`。为页面键入标题。

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. 单击或点按创建。在确认对话框中，单击或点按&#x200B;**完成**&#x200B;以返回站点控制台，或者单击或点按&#x200B;**打开**&#x200B;打开语言副本。

## 查看语言根的状态 {#seeing-the-status-of-language-roots}

触屏优化UI提供了一个“引用”面板，其中显示了已创建的语言根列表。

![chlimage_1-23](assets/chlimage_1-23a.png)

以下过程使用触屏优化UI打开页面的引用面板。

1. 在站点控制台中，选择站点的某个页面，然后单击或点按 **引用**.

   ![chlimage_1-24](assets/chlimage_1-24a.png)

1. 在引用面板中，单击或点按 **语言副本**. 语言副本面板显示网站的语言副本。
