---
title: 多语言资产和资产翻译.
description: 了解如何自动工作流将资产（包括二进制文件、元数据和标记）翻译为多种语言。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 2%

---


# 多语言资源 {#multilingual-assets}

[!DNL Adobe Experience Manager Assets] 允许您对资产（包括二进制文件、元数据和标记）进行自动翻译工作流，以生成其他语言的资产以用于多语言项目。

要实现翻译工作流的自动化，您可以将翻译与 [!DNL Experience Manager] 翻译服务提供商相集成，并创建将资产翻译为多种语言的项目。 [!DNL Experience Manager] 支持人类和机器翻译工作流。

人文翻译： 转换后的资产会返回并导入 [!DNL Experience Manager]。 当您的翻译提供商与之集成 [!DNL Experience Manager]后，资产会在与翻译提供 [!DNL Experience Manager] 商之间自动发送。

机器翻译： 机器翻译服务会立即转换资产的元数据和标记。

换算资产包括：

1. [连接Experience Manager与翻译服务提供商](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [创建翻译集成框架配置](/help/sites-administering/tc-tic.md)
1. [准备要翻译的资产](preparing-assets-for-translation.md)
1. [将翻译云服务应用到文件夹](transition-cloud-services.md)
1. [创建翻译项目](translation-projects.md)

如果您的翻译服务提供商不提供要与之集成的连接 [!DNL Experience Manager]器，请使用 [替代过程](/help/sites-administering/tc-manage.md#exporting-a-translation-job)。

另请参阅为 [内容片段创建翻译项目](creating-translation-projects-for-content-fragments.md)。
