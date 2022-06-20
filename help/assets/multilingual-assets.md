---
title: 多语言资产和资产翻译
description: 了解如何自动化工作流，将资产（包括二进制文件、元数据和标记）翻译成多种语言。
contentOwner: AG
feature: Asset Management
role: Admin
exl-id: edccf23c-087e-4253-babb-dd4c6610517d
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 11%

---

# 多语言资产 {#multilingual-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/translate-assets.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-64/assets/using/multilingual-assets.html?lang=en) |

[!DNL Adobe Experience Manager Assets] 允许您自动执行资产（包括二进制文件、元数据和标记）的翻译工作流，以生成其他语言版本的资产，以供在多语言项目中使用。

要自动执行翻译工作流，您需要将翻译服务提供商与 [!DNL Experience Manager] 并创建将资产翻译成多种语言的项目。 [!DNL Experience Manager] 支持人工翻译工作流和机器翻译工作流。

人文翻译：已换算资产会退回及导入 [!DNL Experience Manager]. 将翻译提供商与 [!DNL Experience Manager]，则会在 [!DNL Experience Manager] 和翻译提供商。

机器翻译：机器翻译服务会立即翻译资产的元数据和标记。

换算资产包括以下各项：

1. [将Experience Manager与翻译服务提供商连接](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [创建翻译集成框架配置](/help/sites-administering/tc-tic.md)
1. [准备资产以进行翻译](preparing-assets-for-translation.md)
1. [将翻译云服务应用到文件夹](transition-cloud-services.md)
1. [创建翻译项目](translation-projects.md)

如果您的翻译服务提供商没有提供要与集成的连接器 [!DNL Experience Manager]，使用 [替代过程](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

另请参阅 [为内容片段创建翻译项目](creating-translation-projects-for-content-fragments.md).
