---
title: 启用重复资产检测
description: 了解如何在Experience Manager中启用重复资源检测。
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# 启用重复资产检测 {#enable-detection-of-duplicate-assets}

如果您尝试上传中存在的资产 [!DNL Adobe Experience Manager Assets]，则重复项检测功能会将其标识为重复项。 默认情况下禁用重复检测。 要启用该功能，请执行以下步骤：

1. 打开 [!DNL Experience Manager] 通过访问Web Console配置页 `https://[aem_server]:[port]/system/console/configMgr`.
1. 编辑servlet的配置 **[!UICONTROL Day CQ DAM创建资产]**.
1. 选择 **[!UICONTROL 检测重复项]** 选项，然后单击 **[!UICONTROL 保存]**.

   ![在servlet中选择检测重复项选项](assets/chlimage_1-377.png)

   *图：在servlet中选择检测重复项选项。*

现在在中启用了检测重复项功能 [!DNL Assets]. 当用户尝试上传中存在的资产时 [!DNL Experience Manager]，系统会检查冲突并指示冲突。 使用存储在以下位置的SHA-1哈希标识资产： `jcr:content/metadata/dam:sha1`，这意味着不论文件名如何，都会检测到重复的资产。

>[!MORELIKETHIS]
>
>* [复制现有存储库中的资产（社区成员的教程）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

