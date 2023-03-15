---
title: 多语言资产和资产翻译
description: 了解如何自动化工作流以将资源（包括二进制文件、元数据和标记）翻译成多种语言。
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

[!DNL Adobe Experience Manager Assets] 允许您自动执行资产（包括二进制文件、元数据和标记）上的翻译工作流，以生成其他语言的资产以用于多语言项目。

要自动化翻译工作流，您需要将翻译服务提供商与 [!DNL Experience Manager] 并创建项目以将资产翻译成多种语言。 [!DNL Experience Manager] 支持人工翻译工作流和机器翻译工作流。

人工翻译：已翻译资产将返回并导入 [!DNL Experience Manager]. 当您的翻译提供商与集成时 [!DNL Experience Manager]，资源会在以下时间之间自动发送： [!DNL Experience Manager] 以及翻译提供商。

机器翻译：机器翻译服务会立即翻译资产的元数据和标记。

翻译资产包括以下各项：

1. [将Experience Manager连接到翻译服务提供商](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [创建翻译集成框架配置](/help/sites-administering/tc-tic.md)
1. [准备要翻译的资产](preparing-assets-for-translation.md)
1. [将翻译云服务应用到文件夹](transition-cloud-services.md)
1. [创建翻译项目](translation-projects.md)

如果您的翻译服务提供商不提供连接器来与集成 [!DNL Experience Manager]，使用 [替代流程](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

另请参阅， [为内容片段创建翻译项目](creating-translation-projects-for-content-fragments.md).
