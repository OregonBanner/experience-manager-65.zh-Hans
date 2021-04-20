---
title: 多语言资产和资产翻译
description: 了解如何自动工作流将资产（包括二进制文件、元数据和标记）翻译为多种语言。
contentOwner: AG
feature: Asset Management
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 3%

---


# 多语言资源{#multilingual-assets}

[!DNL Adobe Experience Manager Assets] 允许您对资产（包括二进制文件、元数据和标记）进行自动翻译工作流，以生成其他语言的资产，以便在多语言项目中使用。

要实现翻译工作流的自动化，您需要将翻译服务提供商与[!DNL Experience Manager]集成，并创建项目以将资产翻译为多种语言。 [!DNL Experience Manager] 支持人和机器翻译工作流。

人文翻译：转换后的资产将返回并导入到[!DNL Experience Manager]中。 将翻译提供程序与[!DNL Experience Manager]集成后，资产会自动在[!DNL Experience Manager]和翻译提供程序之间发送。

机器翻译：机器翻译服务会立即转换资产的元数据和标记。

折算资产包括：

1. [连接Experience Manager与翻译服务提供商](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [创建翻译集成框架配置](/help/sites-administering/tc-tic.md)
1. [准备翻译资产](preparing-assets-for-translation.md)
1. [将翻译云服务应用到文件夹](transition-cloud-services.md)
1. [创建翻译项目](translation-projects.md)

如果翻译服务提供商不提供与[!DNL Experience Manager]集成的连接器，请使用[替代进程](/help/sites-administering/tc-manage.md#exporting-a-translation-job)。

另请参阅[为内容片段](creating-translation-projects-for-content-fragments.md)创建翻译项目。
