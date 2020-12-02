---
title: 设置Dynamic Media
description: 要设置Dynamic Media，您需要配置Dynamic Media并管理图像预设和查看器预设
uuid: bcd1f9ab-4201-4222-9e4a-ba82b3c7cd6c
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 36a4a4e7-8bb2-4853-b335-cf9148be410c
translation-type: tm+mt
source-git-commit: df89d5cfd5060d493babb89e92a9a98e851b8879
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 17%

---


# 设置Dynamic Media {#setting-up-dynamic-media}

[Dynamic Media 可按需提供丰富的产品销售和市场营销可视资产，还能根据 Web、移动设备、社交网站等不同销售渠道的各种需求自动调整资产供应情况，是您资产管理工作的得力助手。](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html)Dynamic Media使用一组主源资源，通过其全局、可扩展、性能优化的网络实时生成和交付多种形式的丰富内容。

>[!NOTE]
>
>本文档描述了直接集成到AEM的Dynamic Media功能。 如果您使用集成到AEM中的Dynamic Media Classic(以前称为Scene7)，请参阅[Dynamic Media Classic集成文档](/help/sites-administering/scene7.md)。
>
>请参阅[双重使用方案](/help/sites-administering/scene7.md#dual-use-scenario)，以了解您可能希望将AEM与Dynamic Media Classic及Dynamic Media集成的时间。

如果您要管理 Dynamic Media，以下主题会很有用：

* [配置Dynamic Media-Scene7模式](config-dms7.md) —如果您是新Dynamic Media客户，请使用此配置。
* [配置Dynamic Media-Hybrid模式](config-dynamic.md) -如果您是升级AEM的现有Dynamic Media客户，请使用此配置。
* [管理图像预设](managing-image-presets.md)
* [管理查看器预设](managing-viewer-presets.md)
* [Dynamic Media疑难解答-Scene7模式](troubleshoot-dms7.md)

另请参阅以下主题：

* [视频编码和视频用户档案](video-profiles.md)
* [图像配置文件](image-profiles.md)

>[!NOTE]
>
>**如果要升级：**
>
>* 在AEM启动并运行后，您上传的任何资产都会自动启用Dynamic Media（除非系统管理员明确禁用它）。 如果您是AEM的升级实例，并且是Dynamic Media的新实例，则可能需要重新处理资产以启用Dynamic Media。