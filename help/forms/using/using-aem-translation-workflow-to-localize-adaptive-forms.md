---
title: 使用AEM翻译工作流将自适应表单和记录文档本地化
seo-title: 使用AEM翻译工作流将自适应表单和记录文档本地化
description: 了解如何使用AEM翻译工作流将自适应表单和记录文档本地化。
seo-description: 了解如何使用AEM翻译工作流将自适应表单和记录文档本地化。
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: 自适应表单
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---

# 使用AEM翻译工作流将自适应表单和记录文档{#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}本地化

本地化的表单可帮助您在不同的地理位置为更多受众提供服务。 Adobe Experience Manager翻译工作流程可帮助您将自适应表单及其记录文档本地化。 您可以使用&#x200B;**机器翻译**&#x200B;或&#x200B;**人工翻译器**&#x200B;将自适应表单本地化。

本文介绍了将AEM翻译工作流与自适应表单和记录文档结合使用的过程。

## 使用机器翻译将自适应表单和记录文档本地化{#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

机器翻译服务会立即以自适应形式和记录文档来翻译您的内容。 AEM Forms已预配置为使用Microsoft Translator试用版进行机器翻译。 执行以下步骤，为自适应表单和记录文档启用机器翻译：

1. 在AEM Forms UI中，选择一个表单，然后点按&#x200B;**添加字典**&#x200B;选项。
1. 在&#x200B;**将字典添加到翻译项目**&#x200B;屏幕中，选择&#x200B;**创建新翻译项目**&#x200B;或&#x200B;**添加到现有翻译项目**&#x200B;选项。
1. 在&#x200B;**项目标题**&#x200B;字段中，指定标题。 例如，`Government Reference Site - German locale.`
1. 在&#x200B;**目标语言**&#x200B;字段中，指定区域设置（例如`German(de)`），然后单击&#x200B;**完成**。 您可以指定多个区域设置。 表单已翻译为&#x200B;**目标语言**&#x200B;字段中指定的所有区域设置。
1. 在“添加的词典”对话框中，单击&#x200B;**打开项目**。 在项目屏幕中，打开新创建的项目。
1. 单击&#x200B;**翻译摘要**&#x200B;拼贴底部的&#x200B;**省略号**。 将打开“翻译摘要”屏幕。
1. 单击&#x200B;**翻译摘要**&#x200B;屏幕顶部的&#x200B;**编辑**&#x200B;图标。 打开&#x200B;**Translation**&#x200B;选项卡，然后在&#x200B;**Translation Method**&#x200B;屏幕中选择Machine Translation。 选择相应的&#x200B;**翻译提供程序**&#x200B;和&#x200B;**云配置**。 单击屏幕顶部的&#x200B;**Done**&#x200B;图标。
1. 在&#x200B;**翻译作业**&#x200B;拼贴中，单击![aem62forms_downarrow](assets/aem62forms_downarrow.png)图标，然后单击&#x200B;**开始**。 图块的状态将变为“草稿”。 翻译完成后，状态将变为&#x200B;**准备审阅**。 几分钟后刷新页面并验证状态。
1. 在&#x200B;**翻译作业**&#x200B;拼贴中的状态变为&#x200B;**准备审阅**&#x200B;后，在浏览器窗口中打开表单。 将显示表单的本地化版本。

   >[!NOTE]
   >
   >* 在浏览器窗口中打开表单的本地化版本之前，请确保将浏览器的区域设置设置为与表单的区域设置匹配。 例如，如果表单已翻译为德语(de)语言，则将浏览器的区域设置设置为德语(de)。
   >* 自适应表单组件不支持从右到左(RTL)语言。 例如，希伯来语。


   与自适应表单一起，自动生成的记录文档也会进行本地化。

   有关“记录文档”设置和配置的详细信息，请参阅：

[记录文档模板配置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[记录文档设置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [自定义记录文档的品牌信](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 息，并确保将浏览器区域设置设置为与您使用机器语言本地化自适应表单时所使用的语言相同的语言。浏览器区域设置有助于将记录文档中的品牌信息本地化。
1. 要查看记录的本地化文档，请点按生成预览。 记录PDF的文档将在浏览器的新选项卡中生成并打开。

## 使用人文翻译本地化自适应表单及其记录文档{#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

在人文翻译中，内容被发送给翻译提供商，并由专业翻译员翻译。 完成后，将返回翻译内容并将其导入AEM。 将您的翻译提供商与AEM集成后，内容会在AEM和翻译提供商之间自动发送。

对于翻译，将与专业翻译人员共享包含XLIFF格式文件的字典。 词典包含每个区域设置的单独XLIFF文件。 每个XLIFF文件都包含将向最终用户显示的文本以及相应本地化文本的占位符。

使用人文翻译员执行以下步骤，将表单及其记录文档本地化：

1. [将AEM与您的翻译服务提供商](/help/sites-administering/tc-tic.md) 连接并 [创建翻译集成框架配置](/help/sites-administering/tc-tic.md)。

1. [将语言母版的页面与](/help/sites-administering/tc-tic.md) 翻译服务和框架配置相关联。

1. [识别要翻译的](/help/sites-administering/tc-rules.md) 内容类型。

1. [通过创作语言](/help/sites-administering/tc-prep.md) 主控并创建语言副本的根页面，准备翻译内容。

1. [创建翻](/help/sites-administering/tc-manage.md) 译项目以收集要翻译的内容并准备翻译过程。

1. 使用翻译项目到[管理内容翻译流程](/help/sites-administering/tc-manage.md)。

>[!NOTE]
>
>* 自适应表单组件不支持从右到左(RTL)语言。 例如，希伯来语。

>


