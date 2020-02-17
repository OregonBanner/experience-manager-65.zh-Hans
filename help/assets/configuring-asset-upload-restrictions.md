---
title: 配置资产上传限制
description: '限制用户可上传的资产（文件）类型 '
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 配置资产上传限制 {#configuring-asset-upload-restrictions}

您可以配置Adobe Experience Manager(AEM)资产，以限制用户可上传的资产（文件）类型。 此功能可帮助您消除用户以不希望的格式上传资产或上传任何恶意文件的可能性。 该 `Day CQ DAM Asset Upload Restriction` 服务允许您控制用户可以上传的文件类型。 默认情况下，AEM资产允许用户上传所有MIME类型的资产。 但是，您可以配置服务以限制用户仅上传特定MIME类型的文件。

1. 打开Configuration Manager web控制台。 访问 `https://[aem_server]:[port]/system/console/configMgr`.
1. 在编辑模 **[!UICONTROL 式下打开Day CQ DAM资产上传限制]** 。 默认情况下，“ **允许所有MIME** ”选项处于选中状态，此选项允许用户上传所有MIME类型的文件。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 要限制用户仅上传某些MIME类型的文件，请取消选择 **[!UICONTROL Allow all MIME]** (允许所有MIME **[!UICONTROL )选项，并使用正则表达式在允许的资产MIME（正则表达式）字]** 段中指定允许的MIME类型。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Click/tap **[!UICONTROL Save]** to save the changes. 如果为允许的MIME类型指定MIME字符串，则对于MIME类型与这些字段中配置的MIME字符串不匹配的任何资产，上传操作都将失败。
