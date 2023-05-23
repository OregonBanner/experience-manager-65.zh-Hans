---
title: 多語言資產
description: 瞭解如何自動化將資產（包括二進位檔案、中繼資料和標籤）翻譯成多種語言的工作流程。
contentOwner: AG
feature: Asset Management
role: Admin
exl-id: edccf23c-087e-4253-babb-dd4c6610517d
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 8%

---

# 多語言資產 {#multilingual-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/translate-assets.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets] 可讓您自動化資產（包括二進位檔案、中繼資料和標籤）的翻譯工作流程，以產生其他語言的資產，以用於多語言專案。

若要自動化翻譯工作流程，您可以將翻譯服務提供者與 [!DNL Experience Manager] 以及建立專案，將資產翻譯成多種語言。 [!DNL Experience Manager] 支持人工翻译工作流和机器翻译工作流。

人工翻譯：系統會傳回已翻譯的資產並將其匯入 [!DNL Experience Manager]. 當您的翻譯提供者與整合時 [!DNL Experience Manager]，資產會在以下時間之間自動傳送： [!DNL Experience Manager] 以及翻譯提供者。

機器翻譯：機器翻譯服務會立即翻譯資產的中繼資料和標籤。

翻譯資產包括下列專案：

1. [將Experience Manager與翻譯服務提供者連線](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [建立翻譯整合框架設定](/help/sites-administering/tc-tic.md)
1. [準備要翻譯的資產](preparing-assets-for-translation.md)
1. [將翻譯雲端服務套用至資料夾](transition-cloud-services.md)
1. [建立翻譯專案](translation-projects.md)

如果您的翻譯服務提供者未提供聯結器來與整合 [!DNL Experience Manager]，使用 [替代程式](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

另請參閱 [建立內容片段的翻譯專案](creating-translation-projects-for-content-fragments.md).
