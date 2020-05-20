---
title: 使用Apache Tika检测MIME类型的资产
description: 启用Apache Tika可帮助AEM资产在上传操作（而非文件扩展名）期间检测内容流中资产的MIME类型。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# Detect MIME type of assets using Apache Tika {#detecting-mime-type-of-assets-using-apache-tika}

通常，Adobe Experience Manager(AEM)资产会检测您从其文件扩展名上传的资产的MIME类型。

如果您使用Apache Tika上传资产，AEM资产会在上传操作（而非文件扩展名）期间从内容流检测其MIME类型。

此功能默认为禁用状态。 要启用该功能，请从 **[!UICONTROL Configuration Manager配置Day]** CQ DAM Mime类 [!UICONTROL 型服务]。

>[!NOTE]
>
>使用Apache Tika库的MIME类型检测是一项资源密集型操作。

1. 要打开Configuration Manager Web控制台，请访问 `https://[aem_server]:[port]/system/console/configMgr`。

1. 在服务列表中，找到Day **[!UICONTROL CQ DAM MIME类型服务]** ，然后单 **[!UICONTROL 击编辑]**。

1. 选择从 **[!UICONTROL 内容检测MIME]** 选项，以启用解析已上传的资产以确定其MIME类型，同时忽略文件扩展名。 默认情况下，此选项处于未选中状态。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Click **[!UICONTROL Save]** to save the changes.
