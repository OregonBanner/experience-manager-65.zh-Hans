---
title: 使用Apache Tika检测MIME类型的资产
description: 启用Apache Tika以 [!DNL Experience Manager Assets] 帮助在上传操作（而非文件扩展名）期间检测内容流中的MIME类型资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# 使用检测MIME类型的资产 [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

通常 [!DNL Adobe Experience Manager Assets] ，会检测您从其文件扩展名上传的资产的MIME类型。

如果您使 [!DNL Apache Tika] 用上传资产， [!DNL Assets] 则在上传操作（而非文件扩展名）期间，会从内容流检测其MIME类型。

此功能默认为禁用状态。 要启用该功能，请从 **[!UICONTROL Configuration Manager配置Day]** CQ DAM Mime类 [!UICONTROL 型服务]。

>[!NOTE]
>
>使用库的MIME类 [!DNL Apache Tika] 型检测是资源密集型操作。

1. 要打开Configuration Manager Web控制台，请访问 `https://[aem_server]:[port]/system/console/configMgr`。

1. 在服务列表中，找到Day **[!UICONTROL CQ DAM MIME类型服务]** ，然后单 **[!UICONTROL 击编辑]**。

1. 选择从 **[!UICONTROL 内容检测MIME]** 选项，以启用解析已上传的资产以确定其MIME类型，同时忽略文件扩展名。 默认情况下，此选项处于未选中状态。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Click **[!UICONTROL Save]** to save the changes.
