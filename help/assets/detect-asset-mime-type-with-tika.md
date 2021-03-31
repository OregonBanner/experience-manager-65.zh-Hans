---
title: 使用Apache Tika检测MIME类型的资产
description: 启用Apache Tika可帮助 [!DNL Experience Manager Assets] 在上载操作（而非文件扩展名）期间检测内容流中的MIME类型资产。
contentOwner: AG
role: 管理员、架构师
feature: 元数据，开发人员工具，资产管理
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# 使用[!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}检测资产的MIME类型

通常，[!DNL Adobe Experience Manager Assets]会检测您从其文件扩展名上传的资产的MIME类型。

如果您使用[!DNL Apache Tika]来上传资产，则[!DNL Assets]会在上传操作（而非文件扩展名）期间从内容流中检测其MIME类型。

默认情况下，此功能处于禁用状态。 要启用该功能，请从[!UICONTROL Configuration Manager]配置&#x200B;**[!UICONTROL Day CQ DAM Mime类型]**&#x200B;服务。

>[!NOTE]
>
>使用[!DNL Apache Tika]库的MIME类型检测是一项资源密集型操作。

1. 要打开Configuration Manager Web控制台，请访问`https://[aem_server]:[port]/system/console/configMgr`。

1. 在服务列表中，找到&#x200B;**[!UICONTROL Day CQ DAM Mime类型服务]**&#x200B;并单击&#x200B;**[!UICONTROL 编辑]**。

1. 选择&#x200B;**[!UICONTROL 从内容]**&#x200B;检测MIME选项，以启用对已上传资产的分析，以在忽略文件扩展名时确定其MIME类型。 默认情况下，此选项处于未选中状态。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改。
