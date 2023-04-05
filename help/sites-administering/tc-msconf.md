---
title: 连接到Microsoft&reg;翻译人员
description: 了解如何将AEM连接到Microsoft&reg;翻译。
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 11%

---

# 连接到Microsoft® Translator{#connecting-to-microsoft-translator}

为Microsoft® Translator云服务创建配置，以使用Microsoft®翻译帐户翻译AEM页面内容、社区内容或资产。

| 属性 | 描述 |
|---|---|
| 翻译标签 | 翻译服务的显示名称。 |
| 翻译属性 | （可选）对于用户生成的内容，为已翻译文本旁边显示的属性，例如 `Translations by Microsoft`。 |
| 工作区 ID | （可选）要使用的自定义Microsoft® Translator引擎的ID。 |
| 订阅密钥 | 您的Microsoft®Microsoft® Translator订阅密钥。 |

创建配置后，您必须 [激活](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

以下过程使用触屏优化UI创建Microsoft® Translator配置。

1. 在边栏中，单击或点按工具>Cloud Services。
1. 在“Microsoft®转换器”区域，选择“显示配置”。
1. 单击可用配置旁边的+链接。

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. 为您的配置键入标题。标题可在“Cloud Services”控制台和“页面属性”下拉列表中标识配置。 默认名称基于标题。 （可选）键入一个名称以用于存储该配置的存储库节点。对“父配置”属性使用默认值，该属性是存储库节点的路径。
1. 单击创建。
1. 在出现的对话框中，键入属性的值，然后单击“确定”。

## 示例Microsoft® TranslatorCloud Service配置 {#sample-microsoft-translator-cloud-service-configurations}

随Geometrixx示例安装了以下Microsoft® Translator云服务配置。 某些示例配置使用试用版Microsoft®翻译帐户，该帐户每月最多允许2000 000个免费翻译字符。

### Microsoft® Translator试用许可 {#microsoft-translator-trial-license}

Microsoft® Translator试用版许可证配置是随Geometrixx Outdoors示例包一起安装的示例配置。 此配置使用Microsoft® Translator帐户，该帐户具有免费订阅，每月允许2 000 000个翻译字符。

### Microsoft® Translator试用许可 — Geometrixx室 {#microsoft-translator-trial-license-geometrixx-outdoors}

Microsoft® Translator试用版许可证 — Geometrixx — 户外配置是随Geometrixx Outdoors一起安装的一个示例配置。 此配置使用与Microsoft® Translator试用许可证配置相同的免费Microsoft® Translator帐户。 该帐户有免费订购，每月可翻译2 000 000个字符。

此Microsoft® Translator配置已优化，可与Geometrixx Outdoors示例网站的内容类型一起使用。

### 升级Microsoft® Translator试用版许可证配置 {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft®翻译配置页面提供了指向Microsoft®网站的便捷链接，以便获取适合生产系统的帐户订阅。

1. 在边栏中，单击或点按工具>操作>云>Cloud Services。
1. 在“Microsoft®翻译器”区域，单击或点按显示配置，然后单击或点按Microsoft®翻译器试用许可证(Microsoft®翻译配置)。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 在配置页面上，单击升级订阅。 使用打开的Microsoft®网页配置您的帐户。

   ![chlimage_1-384](assets/chlimage_1-384.png)

### 自定义您的Microsoft® Translator引擎 {#customizing-your-microsoft-translator-engine}

Microsoft®翻译配置页面提供了一个指向Microsoft®网站的便捷链接，用于自定义Microsoft®翻译器引擎。 ([https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/](https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/))

1. 在边栏中，单击或点按工具>操作>云>Cloud Services。
1. 在Microsoft®翻译器区域，单击或点按显示配置，然后单击或点按要自定义的配置。
1. 在配置页面上，单击自定义翻译器。 使用打开的Microsoft®网页自定义您的服务。

## 激活 Translator 服务配置 {#activating-the-translator-service-configurations}

要支持复制到发布实例的翻译内容，请激活您的云服务配置。 要激活存储Microsoft® Translator或第三方云服务配置的存储库节点，请使用 [激活完整部分（树）](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree). 这些节点位于以下父节点的下方：

* Microsoft®翻译服务：/libs/settings/cloudconfigs/translation/msft-translation
* 第三方翻译：/etc/cloudservices/machine-translation
