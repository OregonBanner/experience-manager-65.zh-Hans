---
title: 配置资产上传限制
description: '限制用户可以上传的资产（文件）类型 '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 15%

---


# 配置资产上传限制 {#configuring-asset-upload-restrictions}

您可以配 [!DNL Adobe Experience Manager Assets] 置以限制用户可以上传的资产类型。 它有助于防止意外上传不需要的格式和恶意文件。 该服 `Day CQ DAM Asset Upload Restriction` 务允许您控制用户可以上传的文件类型。 默认情况下， [!DNL Assets] 允许用户上传所有MIME类型的资产。 但是，您可以配置服务以限制用户仅上传特定MIME类型的文件。

1. 打开Configuration Manager Web控制台。 访问 `https://[aem_server]:[port]/system/console/configMgr`.
1. 在编辑模 **[!UICONTROL 式下打开Day CQ DAM资产上传限]** 制服务。 默认情况下， **会选中** “允许所有MIME”选项，此选项允许用户上传所有MIME类型的文件。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. To restrict users to upload files of certain MIME types only, unselect the **[!UICONTROL Allow all MIME]** option and specify allowed MIME types in the **[!UICONTROL Allowed Asset MIMEs (regex)]** fields using regular expressions.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Click **[!UICONTROL Save]** to save the changes. 如果为允许的MIME类型指定MIME字符串，则对于MIME类型与这些字段中配置的MIME字符串不匹配的任何资产，上传操作都将失败。
