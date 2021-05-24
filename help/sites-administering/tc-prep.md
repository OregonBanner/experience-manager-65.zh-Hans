---
title: 准备翻译内容
seo-title: 准备翻译内容
description: 了解如何准备翻译内容。
seo-description: 了解如何准备翻译内容。
uuid: 369630a8-2ed7-48db-973e-bd8213231d49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 8bd67d71-bcb7-4ca0-9751-3ff3ee054011
feature: 语言复制
exl-id: 81978733-89a6-4436-bcf1-4bde962ed54f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# 准备翻译内容{#preparing-content-for-translation}

多语言网站通常提供多种语言的一定数量的内容。 网站以一种语言创作，然后翻译成其他语言。 通常，多语言站点由页面的分支组成，其中每个分支包含使用不同语言的站点页面。

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

网站的每个语言分支都称为语言副本。 语言副本的根页面（称为语言根）标识语言副本中内容的语言。 例如，`/content/geometrixx/fr`是法语语言副本的语言根。 语言副本必须使用正确配置的语言根](/help/sites-administering/tc-prep.md#creating-a-language-root)，以便在执行源站点的翻译时能够找到正确的语言。[

最初为其创作网站内容的语言副本是语言主控。 语言主控是翻译成其他语言的源。

请按照以下步骤来准备网站进行翻译：

1. 创建语言的语言根主控。 例如，英语Geometrixx演示站点的语言根目录为/content/geometrixx/en。 确保根据[创建语言根](/help/sites-administering/tc-prep.md#creating-a-language-root)中的信息正确配置语言根。
1. 创作语言的内容主控。
1. 为您的站点创建每个语言副本的语言根目录。 例如，Geometrixx示例站点的法语语言副本为/content/geometrixx/fr。

在准备翻译内容后，您可以在语言副本和关联的翻译项目中自动创建缺失的页面。 （请参阅[创建翻译项目](/help/sites-administering/tc-manage.md)。） 有关AEM中内容翻译过程的概述，请参阅[多语言网站内容翻译](/help/sites-administering/translation.md)。

## 创建语言根{#creating-a-language-root}

将语言根创建为语言副本的根页面，以标识内容的语言。 创建语言根目录后，可以创建包含语言副本的翻译项目。

要创建语言根，请创建页面并使用ISO语言代码作为Name属性的值。 语言代码必须采用以下格式之一：

* `<language-code>`例如，支持的语言代码是由ISO-639-1定义的双字母代码 `en`。

* `<language-code>_<country-code>` 或 `<language-code>-<country-code>`支持的国家/地区代码是由ISO 3166定义的小写字母或大写双字母代码， `en_US`例如 `en_us`、 `en_GB`、 `en-gb`。

您可以根据为全局网站选择的结构，使用任一格式。  例如，Geometrixx站点的法语语言副本的根页面将`fr`作为Name属性。 请注意， Name属性将用作存储库中页面节点的名称，从而确定页面的路径。 (http://localhost:4502/content/geometrixx/fr.html)

以下过程使用触屏优化UI创建网站的语言副本。 有关使用经典UI的说明，请参阅[使用经典UI创建语言根](/help/sites-administering/tc-lroot-classic.md)。

1. 导航到站点。
1. 单击或点按要创建语言副本的网站。

   例如，要创建Geometrixx Outdoors网站的语言副本，您可以单击或点按Geometrixx Outdoors网站。

1. 单击或点按创建，然后单击或点按创建页面。

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. 选择页面模板，然后单击或点按下一步。
1. 在“名称”字段中，键入格式为`<language-code>`或`<language-code>_<country-code>`的国家/地区代码，例如`en`、`en_US`、`en_us`、`en_GB`、`en_gb`。 键入页面的标题。

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. 单击或点按创建。在确认对话框中，单击或点按&#x200B;**Done**&#x200B;以返回到站点控制台，或单击或点按&#x200B;**Open**&#x200B;以打开语言副本。

## 看语言根的状态{#seeing-the-status-of-language-roots}

触屏优化UI提供了一个“引用”面板，其中显示了已创建的语言根列表。

![chlimage_1-23](assets/chlimage_1-23a.png)

以下过程使用触屏优化UI打开页面的引用面板。

1. 在站点控制台中，选择站点的某个页面，然后单击或点按&#x200B;**引用**。

   ![chlimage_1-24](assets/chlimage_1-24a.png)

1. 在引用面板中，单击或点按&#x200B;**语言副本**。 语言副本面板显示网站的语言副本。
