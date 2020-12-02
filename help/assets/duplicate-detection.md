---
title: 启用重复资产检测
description: 了解如何在Experience Manager中启用重复资产检测。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---


# 启用重复资产检测{#enable-detection-of-duplicate-assets}

如果您尝试上传[!DNL Adobe Experience Manager Assets]中存在的资产，重复检测功能会将其标识为重复。 重复检测默认为禁用。 要启用该功能，请执行以下步骤：

1. 通过访问`https://[aem_server]:[port]/system/console/configMgr`打开[!DNL Experience Manager] Web控制台配置页。
1. 编辑servlet **[!UICONTROL Day CQ DAM创建资产]**&#x200B;的配置。
1. 选择&#x200B;**[!UICONTROL 检测重复]**&#x200B;选项，然后单击&#x200B;**[!UICONTROL 保存]**。

   ![在servlet中选择检测重复选项](assets/chlimage_1-377.png)

   *图：在servlet中选择检测重复选项。*

检测重复功能现在在[!DNL Assets]中启用。 当用户尝试上传[!DNL Experience Manager]中存在的资产时，系统会检查是否存在冲突并指示它。 资产使用存储在`jcr:content/metadata/dam:sha1`的SHA-1哈希进行标识，这意味着无论文件名如何，都会检测重复资产。

>[!MORELIKETHIS]
>
>* [重复现有存储库中的资产（社区成员的教程）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

