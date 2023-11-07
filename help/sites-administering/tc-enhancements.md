---
title: 翻译增强功能
description: AEM翻译管理功能的增量增强和细化。
topic-tags: site-features
content-type: reference
feature: Language Copy
exl-id: 2011a976-d506-4c0b-9980-b8837bdcf5ad
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 27%

---

# 翻译增强功能{#translation-enhancements}

本页介绍AEM翻译管理功能的增量增强和细化。

## 翻译项目自动化 {#translation-project-automation}

添加了用于提高处理翻译项目的工作效率的选项，如自动提升和删除翻译启动项，以及计划翻译项目的定期执行。

1. 在您的翻译项目中，单击或点按底部的省略号 **翻译摘要** 磁贴。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切换到 **高级** 选项卡。 在底部，您可以选择 **自动提升翻译启动项**.

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. 或者，您可以选择在收到已翻译内容后，是否应该自动提升和删除翻译启动项。

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. 要选择翻译项目的定期执行，请选择频率，下拉菜单位于 **重复翻译**. 循环项目执行将在指定的时间间隔内自动创建和执行翻译作业。

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## 多语言翻译项目 {#multilingual-translation-projects}

可以在翻译项目中配置多个目标语言，以减少创建的翻译项目总数。

1. 在您的翻译项目中，单击或点按 **翻译摘要** 磁贴。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切换到 **高级** 选项卡。 您可以在下面添加多种语言 **目标语言**.

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. 或者，如果您通过站点中的引用边栏启动翻译，请添加您的语言并选择 **创建多语言翻译项目**.

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. 将在项目中为每个目标语言创建翻译作业。 可以在项目中逐个启动它们，也可以通过在项目管理员中全局执行项目来一次启动所有它们。

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## 翻译记忆库更新 {#translation-memory-updates}

翻译内容的手动编辑可以同步回翻译管理系统 (TMS)，以训练其翻译记忆。

1. 在站点控制台中，更新已翻译页面中的文本内容后，选择 **更新翻译记忆库**.

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. 列表视图显示每个已编辑的文本组件的源和翻译的并排比较。选择应将哪些翻译更新同步到翻译记忆库，然后选择 **更新内存**.

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

AEM 会更新已配置的 TMS 的翻译记忆中现有字符串的翻译。

* 该操作会更新已配置的 TMS 的翻译记忆中现有字符串的翻译。
* 它不会创建新的翻译工作。
* 它通过 AEM 翻译 API（见下文）将翻译发送回 TMS。

要使用此功能：

* TMS 必须配置为可与 AEM 一起使用。
* 连接器需要执行该方法[`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html)。
   * 此方法中的代码确定翻译记忆更新请求的情况。
   * AEM 翻译框架通过实施该方法来将字符串值对（原始和更新的翻译）发送回 TMS。

对于使用专有翻译记忆的情况，可以拦截翻译记忆更新并将其发送到自定义目标。

## 多个级别的语言副本 {#language-copies-on-multiple-levels}

现在可以在节点下对语言根进行分组（例如，按区域），同时仍被识别为语言副本的根。

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>仅允许一个级别。例如，以下内容将不允许“es”页面解析为语言副本：
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>此 `es` 不会检测到语言副本，因为它与 `en` 节点。

>[!NOTE]
>
>语言根可以具有任何页面名称，而不仅仅是语言的ISO代码。 AEM将始终首先检查路径和名称，但如果页面名称未标识语言，则AEM将检查页面的cq：language属性以标识语言。

## 翻译状态报告 {#translation-status-reporting}

现在，可以在站点列表视图中选择一个属性，该属性显示页面是已翻译、正在翻译还是尚未翻译。 要显示它，请执行以下操作：

1. 在Sites中，切换到 **列表视图。**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. 单击或点按 **查看设置**.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. Check **已翻译** 下的复选框 **翻译** 然后点按/单击 **更新**.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

您现在可以看到 **已翻译** 列，其中显示页面的翻译状态。

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)
