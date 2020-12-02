---
title: 连接到Microsoft Translator
seo-title: 连接到Microsoft Translator
description: 了解如何将AEM连接到Microsoft Translator。
seo-description: 了解如何将AEM连接到Microsoft Translator。
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
translation-type: tm+mt
source-git-commit: 8b6801a4efd45fa49e009e1d6876d21c4cded957
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 1%

---


# 连接到Microsoft Translator{#connecting-to-microsoft-translator}

为Microsoft Translator云服务创建配置，以使用您的Microsoft Translation帐户翻译AEM页面内容、社区内容或资产。

| 属性 | 描述 |
|---|---|
| 翻译标签 | 翻译服务的显示名称。 |
| 翻译归因 | （可选）对于用户生成的内容，在翻译文本旁边显示的属性，例如`Translations by Microsoft`。 |
| 工作区ID | （可选）要使用的自定义Microsoft Translator引擎的ID。 |
| 订阅密钥 | 您的Microsoft Translator订阅密钥。 |

创建配置后，需要[将其激活](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations)。

以下过程使用触屏优化UI创建Microsoft Translator配置。

1. 在边栏上，单击或点按工具>Cloud Services。
1. 在Microsoft Translator区域，单击或点按显示配置。
1. 单击“可用配置”旁边的+链接。

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. 键入配置标题。 标题在Cloud Services控制台以及页面属性下拉列表中标识配置。 默认名称基于标题。 （可选）键入用于存储配置的存储库节点的名称。 您应使用父配置属性的默认值，该属性是存储库节点的路径。
1. 单击创建。
1. 在出现的对话框中，键入属性值，然后单击“确定”。

## Microsoft TranslatorCloud Service配置示例{#sample-microsoft-translator-cloud-service-configurations}

以下Microsoft Translator云服务配置随Geometrixx示例一起安装。 某些示例配置使用试用版Microsoft Translation帐户，该帐户每月最多允许2 000 000个免费翻译字符。

### Microsoft Translator 试用许可证 {#microsoft-translator-trial-license}

Microsoft Translator试用版许可证配置是与Geometrixx Outdoors示例包一起安装的示例配置。 此配置使用Microsoft Translator帐户，该帐户具有免费订阅，允许每月2 000 000个翻译字符。

### Microsoft Translator试用许可证-Geometrixx-户外{#microsoft-translator-trial-license-geometrixx-outdoors}

Microsoft Translator试用许可证-Geometrixx-室外配置是与Geometrixx Outdoors一起安装的示例配置。 此配置使用与Microsoft Translator试用许可证配置相同的免费Microsoft Translator帐户。 该帐户有一个免费订阅，每月允许2 000 000个翻译字符。

此Microsoft Translator配置经过优化，可与Geometrixx Outdoors示例站点的内容类型一起使用。

### 升级Microsoft Translator试用版许可证配置{#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft Translation配置页提供指向Microsoft网站的便捷链接，以获得适合生产系统的帐户订阅。

1. 在边栏上，单击或点按工具>操作>云>Cloud Services。
1. 在“Microsoft Translator”区域，单击或点按显示配置，然后单击或点按Microsoft Translator试用许可证（Microsoft Translator配置）。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 在配置页面上，单击升级订阅。 使用打开的Microsoft网页配置您的帐户。

   ![chlimage_1-384](assets/chlimage_1-384.png)

### 自定义Microsoft Translator引擎{#customizing-your-microsoft-translator-engine}

Microsoft Translation配置页面提供指向Microsoft网站的便捷链接，用于自定义Microsoft Translator引擎。 ([https://hub.microsofttranslator.com](https://hub.microsofttranslator.com/))

1. 在边栏上，单击或点按工具>操作>云>Cloud Services。
1. 在Microsoft Translator区域，单击或点按显示配置，然后单击或点按要自定义的配置。
1. 在配置页面上，单击“自定义转换器”。 使用打开的Microsoft网页自定义您的服务。

## 激活Translator服务配置{#activating-the-translator-service-configurations}

您需要激活云服务配置以支持复制到发布实例的翻译内容。 使用[激活完整部分(tree)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree)的方法激活存储Microsoft Translator或第三方云服务配置的存储库节点。 节点位于以下父节点下：

* Microsoft Translation Service:/libs/settings/cloudconfigs/translation/msft-translation
* 第三方翻译：/etc/cloudservices/machine-translation

