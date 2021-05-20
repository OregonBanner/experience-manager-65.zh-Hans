---
title: 使用Apache Tika检测MIME类型的资产
description: 启用Apache Tika以帮助 [!DNL Experience Manager Assets] 在上传操作期间（而不是文件扩展名）从内容流中检测资产的MIME类型。
contentOwner: AG
role: Administrator, Architect
feature: 元数据，开发人员工具，资产管理
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# 使用[!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}检测资产的MIME类型

通常，[!DNL Adobe Experience Manager Assets]会检测您从资产的文件扩展名上传的资产的MIME类型。

如果您使用[!DNL Apache Tika]上传资产，则[!DNL Assets]会在上传操作期间（而不是文件扩展名）从内容流中检测其MIME类型。

此功能默认处于禁用状态。 要启用该功能，请从[!UICONTROL Configuration Manager]配置&#x200B;**[!UICONTROL Day CQ DAM Mime Type]**&#x200B;服务。

>[!NOTE]
>
>使用[!DNL Apache Tika]库的MIME类型检测是一项资源密集型操作。

1. 要打开Configuration Manager Web控制台，请访问`https://[aem_server]:[port]/system/console/configMgr`。

1. 在服务列表中，找到&#x200B;**[!UICONTROL Day CQ DAM Mime类型服务]**&#x200B;并单击&#x200B;**[!UICONTROL 编辑]**。

1. 选择&#x200B;**[!UICONTROL 从内容中检测MIME]**&#x200B;选项，以启用解析已上传资产以确定其MIME类型，同时忽略文件扩展名。 默认情况下，此选项处于取消选中状态。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 单击&#x200B;**[!UICONTROL Save]**&#x200B;以保存更改。
