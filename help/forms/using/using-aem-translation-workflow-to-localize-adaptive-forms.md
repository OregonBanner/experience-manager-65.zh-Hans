---
title: 使用AEM翻译工作流程本地化自适应表单和记录文档
seo-title: 使用AEM翻译工作流程本地化自适应表单和记录文档
description: 了解如何使用AEM翻译工作流程本地化自适应表单和记录文档。
seo-description: 了解如何使用AEM翻译工作流程本地化自适应表单和记录文档。
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# 使用AEM翻译工作流程本地化自适应表单和记录文档 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

本地化的表单可帮助您跨地域为更多受众提供服务。 Adobe Experience Manager翻译工作流程可帮助您本地化自适应表单及其记录文档。 您可以使用机 **器翻译** , **或人工翻** 译器来本地化自适应表单。

本文介绍将AEM翻译工作流与自适应表单和记录文档结合使用的过程。

## 使用机器翻译来定位自适应表单和记录文档 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

机器翻译服务会立即以自适应形式和记录文档翻译您的内容。 AEM Forms已预配置为使用Microsoft Translator试用版进行机器翻译。 执行以下步骤，为自适应表单和记录文档启用机器翻译：

1. 在AEM表单UI中，选择一个表单，然后点按添 **加词典** 。
1. 在“ **将词典添加到翻译项目** ”屏幕中，选择“创 **建新的翻译项目** ”或“添 **加到现有的翻译项目”选项** 。
1. 在“项 **目标题** ”字段中，指定标题。 For example, `Government Reference Site - German locale.`
1. 在“目 **标语言** ”字段中，指定区域设置(例如， `German(de)`)，然后单击“完 **成”**。 您可以指定多个区域设置。 表单将翻译为“目标语言”字段中指定的所 **有语言** 。
1. 在“已添加词典”对话框中，单击“ **打开项目”**。 在“项目”屏幕中，打开新创建的项目。
1. 单击“ **翻译摘要** ”拼贴底部 **的省略号** 。 “翻译摘要”屏幕随即打开。
1. 单击“ **翻译摘要** ”屏幕顶部的“编 **辑”图标** 。 打开“翻 **译** ”选项卡，在“翻译方法”屏幕中选 **择“机器翻译** ”。 选择相应的 **翻译提供商** 和 **云配置**。 Click the **Done** icon at the top of the screen.
1. 在翻译作 **业拼贴中** ，单击 ![aem62forms_downarrow图标](assets/aem62forms_downarrow.png) ，然后单击“开 **始”**。 拼贴的状态将更改为“草稿”。 翻译完成后，状态将变为“准 **备审阅”**。 几分钟后刷新页面并验证状态。
1. 在“翻译作业”拼贴 **上的状态变为** “准 **备审核”后** ，在浏览器窗口中打开表单。 此时将显示表单的本地化版本。

   >[!NOTE]
   >
   >* 在浏览器窗口中打开表单的本地化版本之前，请确保将浏览器的区域设置设置为与表单的区域设置相匹配。 例如，如果表单翻译为德语(de)语言，则将浏览器的区域设置设置为德语(de)。
   >* 自适应表单组件不支持从右到左(RTL)语言。 例如，希伯来语。


   与自适应表单一起，自动生成的记录文档也已本地化。

   有关记录文档设置和配置的详细信息，请参阅：

   [记录文档模板配置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [记录文档设置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [自定义记录文档的品牌信息](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) ，并确保浏览器区域设置设置为您使用机器语言本地化自适应表单的同一语言。 浏览器区域设置有助于在记录文档中本地化品牌信息。
1. 要查看本地化的记录文档，请点按生成预览。 记录PDF文档将在您浏览器的新选项卡中生成并打开。

## 使用人工翻译将自适应表单及其记录文档本地化 {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

在人文翻译中，内容将发送给翻译提供商并由专业翻译人员翻译。 完成后，将返回译文内容并将其导入AEM。 将翻译提供商与AEM集成后，内容会在AEM与翻译提供商之间自动发送。

对于翻译，将与专业翻译人员共享包含XLIFF格式文件的词典。 词典包括每个区域设置的单独XLIFF文件。 每个XLIFF文件都包含将向最终用户显示的文本以及相应本地化文本的占位符。

使用Human Translators，执行以下步骤本地化表单及其记录文档：

1. [将AEM与翻译服务提供商连接](/help/sites-administering/tc-tic.md) ，并 [创建翻译集成框架配置](/help/sites-administering/tc-tic.md)。

1. [将语言主页的页面与翻译服务](/help/sites-administering/tc-tic.md) 和框架配置相关联。

1. [确定要翻译的内容类型](/help/sites-administering/tc-rules.md) 。

1. [通过创作语言母版](/help/sites-administering/tc-prep.md) ，并创建语言副本的根页面，准备要翻译的内容。

1. [创建翻译项目](/help/sites-administering/tc-manage.md) ，以收集要翻译的内容并准备翻译过程。

1. 使用翻译项目管 [理内容翻译流程](/help/sites-administering/tc-manage.md)。

>[!NOTE]
>
>* 自适应表单组件不支持从右到左(RTL)语言。 例如，希伯来语。
>



