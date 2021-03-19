---
title: 使用经典UI创建语言根
seo-title: 使用经典UI创建语言根
description: 了解如何使用经典UI创建语言根目录。
seo-description: 了解如何使用经典UI创建语言根目录。
uuid: 62e40d39-2868-4d3d-9af7-c60a1a658be0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: b88edad4-2a2e-429b-86a2-cc68ba69697e
docset: aem65
feature: 语言复制
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 2%

---


# 使用经典UI创建语言根{#creating-a-language-root-using-the-classic-ui}

以下过程使用经典UI创建站点的语言根。 有关详细信息，请参阅[创建语言根](/help/sites-administering/tc-prep.md#creating-a-language-root)。

1. 在网站控制台的网站树中，选择站点的根页面。 ([http://localhost:4502/siteadmin#](http://localhost:4502/siteadmin#))
1. 添加一个表示站点语言版本的新子页面：

   1. 单击新建>新建页面。
   1. 在对话框中，指定标题和名称。 名称的格式必须为`<language-code>`或`<language-code>_<country-code>`，例如en、en_US、en_us、en_GB、en_gb。

      * 支持的语言代码为ISO-639-1定义的小写字母、双字母代码
      * 支持的国家/地区代码为ISO 3166定义的小写或大写、双字母代码
   1. 选择模板，然后单击创建。

   ![newpagefr](assets/newpagefr.png)

1. 在网站控制台的网站树中，选择站点的根页面。
1. 在“工具”菜单中，选择“语言副本”。

   ![工具](assets/toolslanguagecopy.png)

   “语言副本”对话框显示可用语言版本和网页的矩阵。 语言列中的x表示页面使用该语言。

   ![语言](assets/languagecopydialog.png)

1. 要将现有页面或页面树复制到语言版本，请在语言列中选择该页面的单元格。 单击箭头，然后选择要创建的复制类型。

   在以下示例中，设备/太阳镜/irian页面被复制到法语版本。

   ![苦荞](assets/languagecopydilogdropdown.png)

   | 语言副本的类型 | 描述 |
   |---|---|
   | auto | 使用父页面中的行为 |
   | 忽略 | 不创建此页面及其子页面的副本 |
   | `<language>+` （例如，法语+） | 复制页面及其所有子代 |
   | `<language>` （例如法语） | 仅复制该语言中的页面 |

1. 单击确定以关闭对话框。
1. 在下一个对话框中，单击是以确认副本。

