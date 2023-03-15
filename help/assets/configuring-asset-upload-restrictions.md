---
title: 配置资产上传限制
description: 限制用户可以上传的资产（文件）类型
contentOwner: AG
role: Developer, Admin, Architect
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 19%

---

# 配置资产上传限制 {#configuring-asset-upload-restrictions}

您可以配置 [!DNL Adobe Experience Manager Assets] 以限制用户可以上传的资源类型。 它有助于防止意外上传不需要的格式和恶意文件。 此 `Day CQ DAM Asset Upload Restriction` 服务使您能够控制用户可以上传的文件类型。 默认情况下， [!DNL Assets] 允许用户上传所有MIME类型的资产。 但是，您可以将服务配置为限制用户仅上传特定MIME类型的文件。

1. 打开Configuration Manager web控制台。 访问 `https://[aem_server]:[port]/system/console/configMgr`.
1. 打开 **[!UICONTROL Day CQ DAM资产上传限制]** 编辑模式下的服务。 默认情况下， **允许所有MIME** 选项时，允许用户上传所有MIME类型的文件。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 要限制用户仅上传特定MIME类型的文件，请取消选择 **[!UICONTROL 允许所有MIME]** 选项，并在 **[!UICONTROL 允许的资产MIME（正则表达式）]** 使用正则表达式的字段。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 单击 **[!UICONTROL 保存]** 以保存更改。 如果为允许的MIME类型指定MIME字符串，则对于MIME类型与这些字段中配置的MIME字符串不匹配的任何资产，上传操作都将失败。
