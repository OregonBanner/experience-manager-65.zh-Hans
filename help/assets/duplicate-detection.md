---
title: 支持检测重复的资产
description: 了解如何在AEM中启用重复资产检测。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 07c1a4102539ba4678c55dee3a4882101e39864f

---


# 支持检测重复的资产 {#enable-detection-of-duplicate-assets}

如果您尝试上传Adobe Experience Manager(AEM)资产中存在的资产，重复项检测功能会将其标识为重复项。 默认情况下，重复项检测处于禁用状态。 要启用该功能，请执行以下步骤：

1. 通过访问打开“AEM Web Console配置”页 `https://[aem_server]:[port]/system/console/configMgr`面。
1. Edit the configuration for the servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Select the **[!UICONTROL detect duplicate]** option, and click/tap **[!UICONTROL Save]**.

   ![在servlet中选择检测重复项选项](assets/chlimage_1-377.png)


   *图：在servlet中选择检测重复项选项*

AEM资产中现已启用检测重复项功能。 当用户尝试上传AEM中存在的资产时，系统会检查是否存在冲突并指示它。 资产使用存储在的SHA-1哈希值进行标识 `jcr:content/metadata/dam:sha1`，这意味着无论文件名如何，都会检测到重复的资产。

>[!MORELIKETHIS]
>
>* [复制现有存储库中的资产（社区成员提供的教程）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

