---
title: 翻译增强功能
seo-title: 翻译增强功能
description: AEM中的翻译增强功能。
seo-description: AEM中的翻译增强功能。
uuid: 0563603f-327b-48f1-ac14-6777c06734b9
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 42df2db3-4d3c-4954-a03e-221e2f548305
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---


# 转换增强{#translation-enhancements}

本页介绍了AEM翻译管理功能的增量增强和改进。

## 翻译项目自动化{#translation-project-automation}

已添加各种选项以提高翻译项目的工作效率，如自动提升和删除翻译启动项以及计划翻译项目的重复执行。

1. 在您的翻译项目中，单击或点按&#x200B;**翻译摘要**&#x200B;拼贴底部的省略号。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切换到&#x200B;**高级**&#x200B;选项卡。 在底部，您可以选择&#x200B;**自动提升转换启动项**。

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. （可选）您可以选择在接收翻译内容后，是否应自动提升和删除翻译启动项。

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. 要选择翻译项目的重复执行，请在&#x200B;**重复翻译**&#x200B;下选择带下拉框的频率。 重复项目执行将在指定的时间间隔内自动创建和执行转换作业。

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## 多语言翻译项目{#multilingual-translation-projects}

可以在翻译项目中配置多种目标语言，从而减少创建的翻译项目总数。

1. 在您的翻译项目中，单击或点按&#x200B;**翻译摘要**&#x200B;拼贴底部的点。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切换到&#x200B;**高级**&#x200B;选项卡。 您可以在&#x200B;**目标语言**&#x200B;下添加多种语言。

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. 或者，如果要通过站点中的引用边栏启动翻译，请添加语言，然后选择&#x200B;**创建多语言翻译项目**。

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. 将在项目中为每种目标语言创建翻译作业。 可以在项目中逐个启动它们，也可以通过在项目管理员中全局执行项目同时启动它们。

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## 翻译内存更新{#translation-memory-updates}

翻译内容的手动编辑可以同步回翻译管理系统(TMS)以培训其翻译记忆库。

1. 在站点控制台中，在更新已翻译页面中的文本内容后，选择&#x200B;**更新翻译内存**。

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. 列表视图会并排显示源代码与已编辑的每个文本组件的翻译。 选择应同步到Translation Memory的转换更新，然后选择&#x200B;**更新Memory**。

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

   >[!NOTE]
   >
   >AEM会将所选字符串发送回翻译管理系统。

## 多级语言副本{#language-copies-on-multiple-levels}

语言根现在可以分组在节点下，例如按区域进行分组，同时仍被识别为语言副本的根。

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>只允许一个级别。 例如，以下内容将不允许“es”页面解析为语言副本：
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`

>
>
此`es`语言副本将不被检测到，因为它离`en`节点只有2个级别（美洲／中美洲）。

>[!NOTE]
>
>语言根可以有任何页面名称，而不仅仅是语言的ISO代码。 AEM将始终首先检查路径和名称，但如果页面名称不标识语言，AEM将检查页面的cq:language属性以标识语言。

## 转换状态报告{#translation-status-reporting}

现在可以在站点列表视图中选择一个属性，该属性显示页面是已翻译、已翻译还是尚未翻译。 要显示它，请执行以下操作：

1. 在站点中，切换到&#x200B;**列表视图。**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. 单击或点按&#x200B;**视图设置**。

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. 选中&#x200B;**Translation**&#x200B;下的&#x200B;**Translated**&#x200B;复选框，然后点按／单击&#x200B;**Update**。

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

现在，您可以看到一个&#x200B;**Translated**&#x200B;列，它显示页面的翻译状态。

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)

