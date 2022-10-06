---
title: 连接到 Microsoft Translator
seo-title: Connecting to Microsoft Translator
description: 了解如何将AEM连接到Microsoft Translator。
seo-description: Learn how to connect AEM to Microsoft Translator.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 35%

---

# 连接到 Microsoft Translator{#connecting-to-microsoft-translator}

为Microsoft Translator云服务创建配置，以使用您的Microsoft翻译帐户翻译AEM页面内容、社区内容或资产。

| 属性 | 描述 |
|---|---|
| 翻译标签 | 翻译服务的显示名称。 |
| 翻译属性 | （可选）对于用户生成的内容，为已翻译文本旁边显示的属性，例如 `Translations by Microsoft`。 |
| 工作区 ID | （可选）要使用的自定义 Microsoft Translator 引擎的 ID。 |
| 订阅密钥 | 您的 Microsoft Translator 的 Microsoft 订阅密钥。 |

在创建配置后，您需要[激活它](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations)。

以下过程使用触屏优化UI创建Microsoft Translator配置。

1. 在边栏中，单击或点按工具>Cloud Services。
1. 在Microsoft Translator区域，单击或点按显示配置。
1. 单击可用配置旁边的+链接。

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. 为您的配置键入标题。标题在云服务控制台中以及页面属性下拉列表中标识该配置。默认名称基于标题。 （可选）键入一个名称以用于存储该配置的存储库节点。您应使用父配置属性的默认值，该属性是存储库节点的路径。
1. 单击创建。
1. 在出现的对话框中，键入属性的值，然后单击“确定”。

## Microsoft TranslatorCloud Service配置示例 {#sample-microsoft-translator-cloud-service-configurations}

随Geometrixx示例安装了以下Microsoft Translator云服务配置。 某些示例配置使用试用版Microsoft翻译帐户，该帐户每月最多允许2000 000个免费翻译字符。

### Microsoft Translator 试用许可证 {#microsoft-translator-trial-license}

Microsoft Translator试用版许可证配置是随Geometrixx Outdoors示例包一起安装的示例配置。 此配置使用Microsoft Translator帐户，该帐户具有免费订阅，每月允许2 000 000个翻译字符。

### Microsoft Translator试用许可证 — Geometrixx室 {#microsoft-translator-trial-license-geometrixx-outdoors}

Microsoft Translator试用版许可证 — Geometrixx — 户外配置是随Geometrixx Outdoors一起安装的一个示例配置。 此配置使用与Microsoft Translator试用许可证配置相同的免费Microsoft Translator帐户。 该帐户有免费订购，每月可翻译2 000 000个字符。

此Microsoft Translator配置已优化，可与Geometrixx Outdoors示例网站的内容类型一起使用。

### 升级 Microsoft Translator 试用许可证配置 {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft Translation 配置页面提供了指向 Microsoft 网站的便利链接，可用于获取足够用于生产系统的帐户订阅。

1. 在边栏中，单击或点按工具>操作>云>Cloud Services。
1. 在Microsoft Translator区域中，单击或点按显示配置，然后单击或点按Microsoft Translator试用版许可证(Microsoft翻译配置)。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 在配置页面上，单击升级订阅。 使用打开的Microsoft网页配置您的帐户。

   ![chlimage_1-384](assets/chlimage_1-384.png)

### 自定义 Microsoft Translator 引擎 {#customizing-your-microsoft-translator-engine}

Microsoft Translation 配置页面提供了指向 Microsoft 网站的便利链接，可用于自定义 Microsoft Translator 引擎。([https://hub.microsofttranslator.com](https://hub.microsofttranslator.com/))

1. 在边栏中，单击或点按工具>操作>云>Cloud Services。
1. 在Microsoft Translator区域中，单击或点按显示配置，然后单击或点按要自定义的配置。
1. 在配置页面上，单击自定义翻译器。 使用打开的 Microsoft 网页来自定义您的服务。

## 激活 Translator 服务配置 {#activating-the-translator-service-configurations}

您需要激活云服务配置以支持复制到发布实例的已翻译内容。使用的方法 [激活完整部分（树）](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree) 用于激活存储Microsoft Translator或第三方云服务配置的存储库节点。 这些节点位于以下父节点的下方：

* Microsoft翻译服务：/libs/settings/cloudconfigs/translation/msft-translation
* 第三方翻译：/etc/cloudservices/machine-translation
