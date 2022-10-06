---
title: 使用Apache Tika检测MIME类型的资产
description: 启用Apache Tika以帮助 [!DNL Experience Manager Assets] 在上传操作期间（而不是文件扩展名）从内容流中检测资产的MIME类型。
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 使用检测资产的MIME类型 [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

通常， [!DNL Adobe Experience Manager Assets] 会检测您从资产的文件扩展名上传的资产的MIME类型。

如果您使用 [!DNL Apache Tika] 上传资产， [!DNL Assets] 在上传操作期间（而不是文件扩展名）会从内容流中检测其MIME类型。

此功能默认处于禁用状态。 要启用该功能，请配置 **[!UICONTROL Day CQ DAM Mime类型]** 服务 [!UICONTROL 配置管理器].

>[!NOTE]
>
>使用 [!DNL Apache Tika] 库是一个资源密集型操作。

1. 要打开Configuration Manager Web控制台，请访问 `https://[aem_server]:[port]/system/console/configMgr`.

1. 在服务列表中，找到 **[!UICONTROL Day CQ DAM Mime类型服务]** 单击 **[!UICONTROL 编辑]**.

1. 选择 **[!UICONTROL 从内容中检测MIME]** 选项，以在忽略文件扩展名时启用解析已上传资产以确定其MIME类型。 默认情况下，此选项处于取消选中状态。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 单击 **[!UICONTROL 保存]** 以保存更改。
