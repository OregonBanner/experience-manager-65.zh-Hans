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

---


# 翻译增强功能{#translation-enhancements}

本页介绍了对AEM翻译管理功能的增量增强和改进。

## 翻译项目自动化 {#translation-project-automation}

已添加一些选项以提高处理翻译项目的工作效率，如自动提升和删除翻译启动项以及计划翻译项目的重复执行。

1. 在您的翻译项目中，单击或点按“翻译摘要”拼贴底部的 **省略号** 。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切换到“高 **级** ”选项卡。 在底部，您可以选择自动提 **升翻译启动项**。

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. 或者，您也可以选择在接收翻译内容后是否应自动提升和删除翻译启动项。

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. 要选择翻译项目的重复执行，请在重复翻译下选择带有下拉框 **的频率**。 重复执行项目将在指定的时间间隔内自动创建和执行翻译作业。

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## 多语言翻译项目 {#multilingual-translation-projects}

可以在翻译项目中配置多种目标语言，以减少创建的翻译项目总数。

1. 在您的翻译项目中，单击或点按“翻译摘要”拼贴底 **部的点** 。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切换到“高 **级** ”选项卡。 您可以在“目标语言”下添 **加多种语言**。

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. 或者，如果要通过站点中的引用边栏启动翻译，请添加语言，然后选择“ **创建多语言翻译项目”**。

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. 将在项目中为每种目标语言创建翻译作业。 可以在项目中逐个启动这些项目，也可以在项目管理员中全局执行项目以同时启动它们。

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## 翻译记忆库更新 {#translation-memory-updates}

翻译内容的手动编辑可以同步回翻译管理系统(TMS)以培训其翻译记忆库。

1. 在站点控制台中，在更新已翻译页面中的文本内容后，选择更新翻 **译内存**。

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. 列表视图显示源代码与已编辑的每个文本组件的翻译的并排比较。 选择应同步到翻译记忆库的翻译更新，然后选择“更 **新记忆库”**。

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

   >[!NOTE]
   >
   >AEM会将选定的字符串发送回翻译管理系统。

## 多级语言副本 {#language-copies-on-multiple-levels}

语言根现在可以分组在节点下（例如，按区域），同时仍被识别为语言副本的根。

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>仅允许一个级别。 例如，以下内容将不允许“es”页面解析为语言副本：
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>
此语 `es` 言副本将不会被检测到，因为它离节点只有2个级别（美洲／中美洲） `en` 。

>[!NOTE]
>
>语言根可以具有任何页面名称，而不仅仅是语言的ISO代码。 AEM将始终首先检查路径和名称，但如果页面名称不标识语言，则AEM将检查页面的cq:language属性以标识语言。

## 翻译状态报告 {#translation-status-reporting}

现在可以在站点列表视图中选择一个属性，该属性显示页面是已翻译、正在翻译中还是尚未翻译。 要显示它，请执行以下操作：

1. 在“站点”中，切换到“列 **表视图”。**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. 单击或点按 **查看设置**。

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. 选中“ **翻译** ”下的“翻译” **复选框** ，然后点按／单 **击更新**。

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

您现在可以看到一 **个“已翻译** ”列，其中显示页面的翻译状态。

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)

