---
title: 启用重复资产的检测
description: 了解如何在Experience Manager中启用重复资产的检测。
contentOwner: AG
role: User, Admin
feature: 资产管理，资产报表
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# 启用重复资产的检测 {#enable-detection-of-duplicate-assets}

如果您尝试上传[!DNL Adobe Experience Manager Assets]中存在的资产，重复项检测功能会将其标识为重复项。 默认情况下，重复项检测处于禁用状态。 要启用该功能，请执行以下步骤：

1. 通过访问`https://[aem_server]:[port]/system/console/configMgr`打开[!DNL Experience Manager] Web控制台配置页。
1. 编辑Servlet **[!UICONTROL Day CQ DAM创建资产]**&#x200B;的配置。
1. 选择&#x200B;**[!UICONTROL 检测重复项]**&#x200B;选项，然后单击&#x200B;**[!UICONTROL 保存]**。

   ![在Servlet中选择检测重复项选项](assets/chlimage_1-377.png)

   *图：在Servlet中选择检测重复选项。*

现在，[!DNL Assets]中启用了检测重复功能。 当用户尝试上传[!DNL Experience Manager]中存在的资产时，系统会检查是否存在冲突并指示该冲突。 资产使用存储在`jcr:content/metadata/dam:sha1`的SHA-1哈希进行标识，这意味着无论文件名如何，都会检测到重复的资产。

>[!MORELIKETHIS]
>
>* [在现有存储库中复制资产（社区成员提供的教程）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

