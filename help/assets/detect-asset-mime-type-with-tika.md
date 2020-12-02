---
title: 使用Apache Tika检测MIME类型的资产
description: 启用Apache Tika以帮助 [!DNL Experience Manager Assets] 在上传操作（而非文件扩展名）期间检测内容流中资产的MIME类型。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# 使用[!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}检测资产的MIME类型

通常，[!DNL Adobe Experience Manager Assets]会检测您从其文件扩展名上传的资产的MIME类型。

如果使用[!DNL Apache Tika]上传资产，则[!DNL Assets]会在上传操作（而非文件扩展名）期间从内容流检测其MIME类型。

此功能默认为禁用状态。 要启用该功能，请从[!UICONTROL Configuration Manager]配置&#x200B;**[!UICONTROL Day CQ DAM Mime类型]**&#x200B;服务。

>[!NOTE]
>
>使用[!DNL Apache Tika]库的MIME类型检测是资源密集型操作。

1. 要打开Configuration Manager Web控制台，请访问`https://[aem_server]:[port]/system/console/configMgr`。

1. 在服务列表中，找到&#x200B;**[!UICONTROL Day CQ DAM MIME类型服务]**&#x200B;并单击&#x200B;**[!UICONTROL 编辑]**。

1. 选择&#x200B;**[!UICONTROL 从内容]**&#x200B;检测MIME选项，以启用解析已上传的资产以确定其MIME类型，同时忽略文件扩展名。 默认情况下，此选项处于未选中状态。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改。
