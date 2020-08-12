---
title: 通过Dynamic Media使CDN缓存失效
description: 使CDN(内容投放网络)缓存内容失效后，您可以快速更新Dynamic Media交付的资源，而无需等待缓存过期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 9e67e252348f471c052f6c3e88aea61d7a309241
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 4%

---


# 通过Dynamic Media使CDN缓存失效 {#invalidating-cdn-cache-for-dm-assets}

CDN(内容投放网络)会缓存Dynamic Media资源，以便快速投放给客户。 但是，当您更新这些资产时，您可能希望这些更改立即在您的网站上生效。 清除或取消验证CDN缓存可让您快速更新Dynamic Media交付的资产。 您可以在Dynamic Media中发送请求，使缓存立即过期，而不是使用TTL（生存时间）值（默认为10小时）等待缓存过期。

>[!IMPORTANT]
>
>这些步骤仅适用于AEM 6.5、Service Pack 6或更高版本中的Dynamic Media -Scene7模式。 <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

另请参 [阅Dynamic Media中的缓存概述](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)。

**要使Dynamic Media资产的CDN缓存内容失效，请执行以下操作：**

1. 在AEM 6.5.6或更高版本中，点 **[!UICONTROL 按工具>资源> CDN失效。]**

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-path.png)

1. 在“CDN失效”页面上，设置所需的选项：

   | 选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 使 CDN 中与资产关联的图像预设失效]** | 选中此选项后，您可以选择一个或多个Dynamic Media资产（无论MIME类型如何）及其关联的图像预设以使缓存失效。<br>虽然您可以选择一个或多个包含资产的文件夹，但Adobe不建议使用此方法。 而应选择单个资产文件。<br>继续执行下一步。 |
   | **[!UICONTROL 基于模板的失效]** | 选中此选项后，您可以选择Dynamic Media资产以及您之前创建的失效模板。 将此选项与 |
   | **[!UICONTROL 添加资产]** | 巴拉 |
   | **[!UICONTROL 添加 URL]** | 手动添加要使其缓存失效的Dynamic Media资产的完整URL路径。 |

1. 
1. 点按 **[!UICONTROL 下一步。]**
1. 
