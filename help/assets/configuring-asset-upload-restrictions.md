---
title: 配置资源上传限制
description: 限制使用者可上傳的資產型別（檔案）
contentOwner: AG
role: Developer, Admin, Architect
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 19%

---

# 配置资源上传限制 {#configuring-asset-upload-restrictions}

您可以設定 [!DNL Adobe Experience Manager Assets] 以限制使用者可上傳的資產型別。 它有助於防止意外上傳不需要的格式和惡意檔案。 此 `Day CQ DAM Asset Upload Restriction` 服務可讓您控制使用者可上傳的檔案型別。 依預設， [!DNL Assets] 可讓使用者上傳所有MIME型別的資產。 不過，您可以將服務設定為限制使用者僅上傳特定MIME型別的檔案。

1. 開啟Configuration Manager Web主控台。 访问 `https://[aem_server]:[port]/system/console/configMgr`.
1. 開啟 **[!UICONTROL Day CQ DAM資產上傳限制]** 編輯模式下的服務。 根據預設， **允許所有MIME** 選項時，可讓使用者上傳所有MIME型別的檔案。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 若要限制使用者僅上傳特定MIME型別的檔案，請取消選取 **[!UICONTROL 允許所有MIME]** 選項並在 **[!UICONTROL 允許的資產MIME （規則運算式）]** 使用規則運算式的欄位。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 按一下 **[!UICONTROL 儲存]** 以儲存變更。 如果为允许的MIME类型指定MIME字符串，则对于MIME类型与这些字段中配置的MIME字符串不匹配的任何资产，上传操作都将失败。
