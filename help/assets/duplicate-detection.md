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


# 启用重复资产检测 {#enable-detection-of-duplicate-assets}

如果您尝试上传中存在的资产， [!DNL Adobe Experience Manager Assets]重复检测功能会将其标识为重复。 重复检测默认为禁用。 要启用该功能，请执行以下步骤：

1. 通过访 [!DNL Experience Manager] 问打开Web控制台配置页 `https://[aem_server]:[port]/system/console/configMgr`。
1. Edit the configuration for the servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Select the **[!UICONTROL detect duplicate]** option, and click **[!UICONTROL Save]**.

   ![Select detect duplicate option in the servlet](assets/chlimage_1-377.png)

   *Figure: Select detect duplicate option in the servlet.*

The detect duplicate feature is now enabled in [!DNL Assets]. 当用户尝试上传中存在的资产时，系 [!DNL Experience Manager]统会检查是否存在冲突并指示它。 资产使用存储在的SHA-1哈希进行标识，这 `jcr:content/metadata/dam:sha1`意味着无论文件名如何，都会检测重复资产。

>[!MORELIKETHIS]
>
>* [重复现有存储库中的资产（社区成员的教程）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

