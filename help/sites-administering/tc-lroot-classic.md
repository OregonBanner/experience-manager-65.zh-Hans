---
title: 使用经典UI创建语言根
seo-title: Creating a Language Root Using the Classic UI
description: 了解如何使用Classic UI创建语言根。
seo-description: Learn how to create a language root using the Classic UI.
uuid: 62e40d39-2868-4d3d-9af7-c60a1a658be0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: b88edad4-2a2e-429b-86a2-cc68ba69697e
docset: aem65
feature: Language Copy
exl-id: 1ae21d80-0683-4ab9-afaa-4d733ff47720
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 使用经典UI创建语言根{#creating-a-language-root-using-the-classic-ui}

以下过程使用经典UI创建站点的语言根。 有关更多信息，请参阅 [创建语言根](/help/sites-administering/tc-prep.md#creating-a-language-root).

1. 在网站控制台的网站树中，选择站点的根页面。 ([http://localhost:4502/siteadmin#](http://localhost:4502/siteadmin#))
1. 添加表示站点语言版本的新子页面：

   1. 单击“新建”>“新建页面”。
   1. 在对话框中，指定标题和名称。 名称格式必须为 `<language-code>` 或 `<language-code>_<country-code>`，例如en、en_US、en_us、en_GB、en_gb。

      * 支持的语言代码是由ISO-639-1定义的小写双字母代码
      * 支持的国家/地区代码是由ISO 3166定义的小写或大写形式的双字母代码

   1. 选择模板并单击创建。

   ![newpagefr](assets/newpagefr.png)

1. 在网站控制台的网站树中，选择站点的根页面。
1. 在“工具”菜单中，选择“语言复制”。

   ![toolslanguagecopy](assets/toolslanguagecopy.png)

   语言复制对话框显示可用语言版本和网页的矩阵。 语言列中的x表示该页面在该语言中可用。

   ![languagecopydialog](assets/languagecopydialog.png)

1. 要将现有页面或页面树复制到语言版本，请在语言列中选择该页面的单元格。 单击箭头并选择要创建的副本类型。

   在以下示例中，设备/太阳镜/爱尔兰页面将被复制到法语版本。

   ![languagecopydilogdropdown](assets/languagecopydilogdropdown.png)

   | 语言副本类型 | 描述 |
   |---|---|
   | auto | 使用父页面的行为 |
   | 忽略 | 不创建此页面及其子页面的副本 |
   | `<language>+` （例如，French+） | 从该语言复制页面及其所有子页面 |
   | `<language>` （例如，法语） | 仅复制该语言的页面 |

1. 单击“确定”关闭对话框。
1. 在下一个对话框中，单击“是”以确认复制。
