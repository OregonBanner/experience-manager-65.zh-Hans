---
title: 多语言资产和资产翻译
description: 了解如何自动化工作流，将资产（包括二进制文件、元数据和标记）翻译成多种语言。
contentOwner: AG
feature: 资产管理
role: Admin
exl-id: edccf23c-087e-4253-babb-dd4c6610517d
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 2%

---

# 多语言资产 {#multilingual-assets}

[!DNL Adobe Experience Manager Assets] 允许您自动执行资产（包括二进制文件、元数据和标记）的翻译工作流，以生成其他语言版本的资产，以供在多语言项目中使用。

要自动执行翻译工作流，您需要将翻译服务提供商与[!DNL Experience Manager]集成，并创建项目以将资产翻译成多种语言。 [!DNL Experience Manager] 支持人文和机器翻译工作流。

人文翻译：翻译后的资产将返回并导入[!DNL Experience Manager]。 将您的翻译提供程序与[!DNL Experience Manager]集成后，资产将自动在[!DNL Experience Manager]和翻译提供程序之间发送。

机器翻译：机器翻译服务会立即翻译资产的元数据和标记。

换算资产包括以下各项：

1. [将Experience Manager与翻译服务提供商连接](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [创建翻译集成框架配置](/help/sites-administering/tc-tic.md)
1. [准备资产以进行翻译](preparing-assets-for-translation.md)
1. [将翻译云服务应用到文件夹](transition-cloud-services.md)
1. [创建翻译项目](translation-projects.md)

如果您的翻译服务提供商未提供与[!DNL Experience Manager]集成的连接器，请使用[替代进程](/help/sites-administering/tc-manage.md#exporting-a-translation-job)。

另请参阅[为内容片段创建翻译项目](creating-translation-projects-for-content-fragments.md)。
