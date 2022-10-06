---
title: 使用AEM翻译工作流将自适应表单和记录文档本地化
seo-title: Using AEM translation workflow to localize adaptive forms and document of record
description: 了解如何使用AEM翻译工作流将自适应表单和记录文档本地化。
seo-description: Learn to use AEM translation workflows to localize adaptive forms and document of record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: Adaptive Forms
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 15%

---

# 使用AEM翻译工作流将自适应表单和记录文档本地化 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

本地化的表单可帮助您在不同的地理位置为更多受众提供服务。 Adobe Experience Manager翻译工作流程可帮助您将自适应表单及其记录文档本地化。 您可以使用 **机器翻译** 或 **人类翻译** 将自适应表单本地化。

本文介绍了将AEM翻译工作流与自适应表单和记录文档结合使用的过程。

## 使用机器翻译将自适应表单和记录文档本地化 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

机器翻译服务会立即以自适应形式和记录文档来翻译您的内容。 AEM Forms已预配置为使用Microsoft Translator试用版进行机器翻译。 执行以下步骤，为自适应表单和记录文档启用机器翻译：

1. 在AEM Forms UI中，选择一个表单，然后点按 **添加字典** 选项。
1. 在 **将字典添加到翻译项目** 屏幕，选择 **创建新的翻译项目** 或 **添加到现有翻译项目** 选项。
1. 在 **项目标题** 字段中，指定标题。 例如，`Government Reference Site - German locale.`
1. 在 **目标语言** 字段中，指定区域设置(例如， `German(de)`)，然后单击 **完成**. 您可以指定多个区域设置。 表单将翻译为 **目标语言** 字段。
1. 在“添加的词典”对话框中，单击 **打开项目**. 在项目屏幕中，打开新创建的项目。
1. 单击 **省略号** 在 **翻译摘要** 拼贴。 将打开“翻译摘要”屏幕。
1. 单击 **编辑** 图标 **翻译摘要** 屏幕。 打开 **翻译** ，然后在 **翻译方法** 屏幕。 选择相应的 **翻译提供商** 和 **云配置**. 单击 **完成** 图标。
1. 在 **翻译作业** 拼贴，单击 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) ，然后单击 **开始**. 图块的状态将变为“草稿”。 翻译完成后，状态将更改为 **准备审阅**. 几分钟后刷新页面并验证状态。
1. 在状态更改为 **准备审阅** 在 **翻译作业** 平铺，在浏览器窗口中打开表单。 将显示表单的本地化版本。

   >[!NOTE]
   >
   >* 在浏览器窗口中打开表单的本地化版本之前，请确保将浏览器的区域设置设置为与表单的区域设置匹配。 例如，如果表单已翻译为德语(de)语言，则将浏览器的区域设置设置为德语(de)。
   >* 自适应表单组件不支持从右到左(RTL)语言。 例如，希伯来语。


   与自适应表单一起，自动生成的记录文档也会进行本地化。

   有关“记录文档”设置和配置的详细信息，请参阅：

[记录文档模板配置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[记录文档设置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [自定义记录文档的品牌信息](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 并确保将浏览器区域设置设置为与您使用机器语言本地化自适应表单时所使用的语言相同的语言。 浏览器区域设置有助于将记录文档中的品牌信息本地化。
1. 要查看记录的本地化文档，请点按生成预览。 记录PDF的文档将在浏览器的新选项卡中生成并打开。

## 使用人工翻译本地化自适应表单及其记录文档 {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

在人文翻译中，内容被发送给翻译提供商，并由专业翻译员翻译。 完成后，将返回翻译的内容并将其导入 AEM。当您的翻译提供商与 AEM 集成时，内容会在 AEM 和翻译提供商之间自动发送。

对于翻译，将与专业翻译人员共享包含XLIFF格式文件的字典。 词典包含每个区域设置的单独XLIFF文件。 每个XLIFF文件都包含将向最终用户显示的文本以及相应本地化文本的占位符。

使用人文翻译员执行以下步骤，将表单及其记录文档本地化：

1. [将 AEM 连接到翻译服务提供商](/help/sites-administering/tc-tic.md)和[创建翻译集成框架配置](/help/sites-administering/tc-tic.md)。

1. [将语言母版页面关联到](/help/sites-administering/tc-tic.md)翻译服务和框架配置。

1. [标识要翻译的内容类型](/help/sites-administering/tc-rules.md)。

1. 通过创作语言母版并创建语言副本的根页面来[准备内容以进行翻译](/help/sites-administering/tc-prep.md)。

1. [创建翻译项目](/help/sites-administering/tc-manage.md)以收集要翻译的内容并准备翻译过程。

1. 使用翻译项目[管理内容翻译过程](/help/sites-administering/tc-manage.md)。

>[!NOTE]
>
>* 自适应表单组件不支持从右到左(RTL)语言。 例如，希伯来语。
>

