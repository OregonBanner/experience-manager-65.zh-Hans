---
title: 將翻譯雲端服務套用至資料夾
description: 將翻譯雲端服務套用至資料夾
contentOwner: AG
role: Admin
feature: Translation
exl-id: f17a33d7-eb2f-406b-8d6c-a3bf564c8702
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 43%

---

# 將翻譯雲端服務套用至資料夾 {#applying-translation-cloud-services-to-folders}

[!DNL Adobe Experience Manager] 可讓您使用所選翻譯提供者提供的雲端型翻譯服務，確保您的資產已根據需求翻譯。

您可以將翻譯雲端服務直接套用至資產資料夾，以便在翻譯工作流程期間使用這些服務。

## 套用翻譯服務 {#applying-the-translation-services}

將翻譯雲端服務直接套用至您的資產資料夾，讓您在建立或更新翻譯工作流程時無需設定翻譯服務。

1. 從 [!DNL Assets] 使用者介面，選取您要套用翻譯服務的資料夾。
1. 在工具列中按一下 **[!UICONTROL 屬性]** 以顯示 **[!UICONTROL 資料夾屬性]** 頁面。

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. 导航到&#x200B;**[!UICONTROL 云服务]**&#x200B;选项卡。
1. 從「Cloud Service設定」清單中，選擇所需的翻譯提供者。 例如，如果您想從Microsoft使用翻譯服務，請選擇 **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. 選擇翻譯提供者的聯結器。

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 在工具列中按一下 **[!UICONTROL 儲存]**，然後按一下 **[!UICONTROL 確定]** 關閉對話方塊。翻譯服務會套用至資料夾。

## 套用自訂翻譯聯結器  {#applying-custom-translation-connector}

如果要为要在翻译工作流程中使用的翻译服务应用自定义连接器。要应用自定义连接器，请首先从“包管理器”安装连接器。然后，从云服务控制台配置连接器。配置连接器后，该连接器会显示在[应用翻译服务](transition-cloud-services.md#applying-the-translation-services)中所述的“云服务”选项卡的连接器列表中。应用自定义连接器并运行翻译工作流后，翻译项目的&#x200B;**[!UICONTROL 翻译摘要]**&#x200B;拼贴会在&#x200B;**[!UICONTROL 提供程序]**&#x200B;和&#x200B;**[!UICONTROL 方法]**&#x200B;标题下显示连接器详细信息。

1. 從「封裝管理員」安裝聯結器。
1. 按一下 [!DNL Experience Manager] 標誌，並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 在&#x200B;**[!UICONTROL 云服务]**&#x200B;页面的&#x200B;**[!UICONTROL 第三方服务]**&#x200B;下找到安装的连接器。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 按一下 **[!UICONTROL 立即設定]** 開啟「 」的連結 **[!UICONTROL 建立設定]** 對話方塊。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 指定聯結器的標題和名稱，然後按一下 **[!UICONTROL 建立]**. 自定义连接器位于[应用翻译服务](#applying-the-translation-services)步骤 5 中所述的&#x200B;**[!UICONTROL 云服务]**&#x200B;选项卡的连接器列表中。
1. 在应用自定义连接器后，运行[创建翻译项目](translation-projects.md)中描述的任何翻译工作流。在&#x200B;**[!UICONTROL 项目]**&#x200B;控制台中验证翻译项目的&#x200B;**[!UICONTROL 翻译摘要]**&#x200B;拼贴中连接器的详细信息。

   ![chlimage_1-220](assets/chlimage_1-220.png)
