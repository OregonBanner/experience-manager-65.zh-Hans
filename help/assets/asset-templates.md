---
title: 資產範本
description: 瞭解中的資產範本 [!DNL Adobe Experience Manager Assets] 以及如何使用資產範本建立行銷宣傳品。
contentOwner: AG
role: User
feature: Asset Management,Developer Tools
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---

# 資產範本 {#asset-templates}

資產範本是一種特殊型別的資產，可促進將視覺豐富的內容快速重新用於數位和印刷媒體。 資產範本包含固定傳訊區段及可編輯區段兩個部分。 固定傳訊區段可包含專有內容，例如品牌標誌和已停用編輯的版權資訊。 可編輯區段可在欄位中包含視覺和文字內容，您可編輯這些欄位來自訂訊息。

在確保全球招牌的同時進行有限編輯的彈性，使資產範本成為快速內容改寫和發佈的理想建置區塊，成為各種功能的內容成品。 重新調整內容用途有助於降低管理列印和數位頻道的成本，並在這些頻道中提供整體且一致的體驗。

身為行銷人員，您可以透過以下方式儲存和管理範本： [!DNL Experience Manager Assets] 並使用單一基本範本，輕鬆建立多種個人化列印體驗。 您可以建立各種型別的行銷宣傳品，包括小冊子、傳單、明信片、名片等，以便向客戶清楚傳達行銷訊息。 您也可以組合現有或新列印輸出的多頁列印輸出。 最重要的是，您可以同時輕鬆提供數位和列印體驗，為使用者提供一致的整合式體驗。

雖然資產範本多半是 [!DNL Adobe InDesign] 檔案，熟練掌握 [!DNL Adobe InDesign] 不會成為製造光彩照人的障礙。 您不需要對應 [!DNL Adobe InDesign] 範本以及您在建立目錄時所需的產品欄位。 您可以直接在Web介面上以WYSIWYG模式編輯範本。 但是，對於 [!DNL Adobe InDesign] 若要處理您的編輯變更，您必須先設定 [!DNL Experience Manager Assets] 若要與整合 [!DNL Adobe InDesign Server].

編輯功能 [!DNL Adobe InDesign] 網頁介面的範本有助於促進創意和行銷人員之間的更大合作。 提升的內容速度可縮短行銷宣傳品的上市時間。

您可以使用資產範本達成下列目標：

* 從網頁介面修改可編輯的範本欄位。
* 控制文字的基本樣式，例如標籤層級的字型大小、樣式和文字。
* 使用內容選擇器變更範本中的影像。
* 預覽範本編輯。
* 合併多個範本檔案以建立多頁成品。

當您選擇附屬資料的範本時， [!DNL Experience Manager Assets] 建立您可編輯的範本復本。 原始範本會保留，以確保您的全域招牌保持不變，並可重複使用以強制執行品牌一致性。

您可以在父資料夾中以INDD、PDF或JPG格式匯出更新的檔案。 您也可以將這些格式的輸出下載到您的本機檔案系統。

## 建立附屬資料 {#creating-a-collateral}

假設您要建立數位可列印的宣傳品（例如手冊、傳單，以及即將推出的行銷活動的廣告），並與全球折扣商店分享。 根據範本建立宣傳品有助於跨管道提供統一的客戶體驗。 設計人員可使用創意解決方案（例如）建立行銷活動範本（單頁或多頁） [!DNL InDesign] 並將範本上傳至 [!DNL Experience Manager Assets] 敬請參考使用。 在建立宣傳品之前，請先上傳一或多個INDD範本，並可在以下位置使用： [!DNL Experience Manager] 事前準備。

1. 在 [!DNL Experience Manager] 介面點按 [!UICONTROL 資產].

1. 從選項中選擇 **[!UICONTROL 範本]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. 按一下 **[!UICONTROL 建立]**，然後從功能表中選擇您要建立的附屬資料。 例如，選擇 **[!UICONTROL 手冊]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 上傳一個或多個INDD範本並在以下位置提供： [!DNL Experience Manager] 事前準備。 選擇手冊的範本，然後按一下 **[!UICONTROL 下一個]**.
1. 指定手冊的名稱和說明（選用）。

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. （可選）按一下 **[!UICONTROL 標籤]** 並選取手冊的一或多個標籤。 按一下 **[!UICONTROL 確認]** 以確認您的選取。
1. 单击&#x200B;**[!UICONTROL 创建]**。對話方塊會確認已建立新手冊。 按一下 **[!UICONTROL 開啟]** ，以在編輯模式中開啟手冊。

   <!--![chlimage_1-106](assets/.png) -->

   或者，您也可以關閉對話方塊，並導覽至您開始使用的「範本」頁面中的資料夾，以檢視您建立的手冊。 宣傳品的型別會顯示在卡片檢視的縮圖上。 例如，在此案例中， [!UICONTROL 手冊] 都會顯示在縮圖上。

   ![chlimage_1-107](assets/chlimage_1-312.png)

## 編輯宣傳品 {#editing-a-collateral}

您可以在建立附屬資料後立即加以編輯。 或者，您也可從 [!UICONTROL 範本] 頁面或資產頁面。

1. 若要開啟要編輯的附屬資料，請執行下列任一項作業：

   * 開啟您在步驟7中建立的宣傳品（在此案例中是宣傳冊）， [建立附屬資料](/help/assets/asset-templates.md#creating-a-collateral).
   * 從「範本」頁面，瀏覽至您建立附屬資料的資料夾，然後按一下 [!UICONTROL 編輯] 在附屬資料的縮圖上快速動作。
   * 在附屬資產的頁面中，按一下 **[!UICONTROL 編輯]** （從工具列）。
   * 選取附屬資料，然後按一下 **[!UICONTROL 編輯]** （從工具列）。

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   資產尋找器和文字編輯器會顯示在頁面左側。 文字編輯器預設為開啟。

   您可以使用文字編輯器來修改要顯示在文字欄位中的文字。 您可以在標籤層級修改字型大小、樣式、顏色和文字。

   使用資產尋找器，您可以瀏覽或搜尋內的影像 [!DNL Experience Manager Assets] 和將範本中可編輯的影像取代為您選擇的影像。

   ![chlimage_1-109](assets/chlimage_1-314.png)

   可編輯內容會顯示在右側。 讓欄位可以在中編輯 [!DNL Experience Manager Assets]，範本中對應的欄位必須標籤 [!DNL InDesign]. 換言之，它們應該在中標籤為可編輯 [!DNL InDesign].

   >[!NOTE]
   >
   >確保您的 [!DNL Experience Manager] 部署已與 [!DNL InDesign Server] 以啟用 [!DNL Experience Manager Assets] 以從擷取資料 [!DNL InDesign] 範本並使其可用於編輯。 如需詳細資訊，請參閱 [將Experience Manager Assets與InDesign Server整合](/help/assets/indesign.md).

1. 若要修改可編輯欄位中的文字，請從可編輯欄位清單中按一下文字欄位，然後編輯欄位中的文字。

   ![chlimage_1-111](assets/chlimage_1-316.png)

   您可以使用提供的選項來編輯文字屬性，例如字型樣式、顏色和大小。

1. 按一下 **[!UICONTROL 預覽]** 以預覽文字變更。

1. 若要交換影像，請按一下 **[!UICONTROL 資產尋找器]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. 從可編輯欄位清單中選取影像欄位，然後將所需的影像從資產選擇器拖曳至可編輯欄位。

   ![chlimage_1-114](assets/chlimage_1-319.png)

   您也可以使用關鍵字、標籤，並根據其發佈狀態來搜尋影像。 您可以瀏覽 [!DNL Experience Manager Assets] 存放庫並導覽至所需影像的位置。

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. 按一下 **[!UICONTROL 預覽]** 以預覽影像。
1. 若要編輯多頁附屬資料中的特定頁面，請使用底部的頁面導覽器。

1. 按一下 **[!UICONTROL 預覽]** 以預覽所有變更。 按一下 **[!UICONTROL 完成]** 以儲存對附屬資料的編輯變更。

   >[!NOTE]
   >
   >只有當附屬資料內的可編輯影像欄位沒有任何遺漏圖示時，才會啟用「預覽」和「完成」選項。 如果您的附屬資料中缺少圖示，原因如下 [!DNL Experience Manager] 無法解析中的影像 [!DNL InDesign] 範本。 通常 [!DNL Experience Manager] 無法解析下列情況的影像：
   >
   >* 影像未內嵌在基礎中 [!DNL InDesign] 範本。
   >* 從本機檔案系統連結影像。

   >
   >若要啟用 [!DNL Experience Manager] 若要解析影像，請執行下列動作：
   >
   >* 建立時內嵌影像 [!DNL InDesign] 範本(請參閱 [關於連結與內嵌圖形](https://helpx.adobe.com/indesign/using/graphics-links.html))。
   >* 掛載 [!DNL Experience Manager] 至您的本機檔案系統，然後將遺失的圖示與中的現有資產對應 [!DNL Experience Manager].

   >
   >如需有關使用的詳細資訊 [!DNL InDesign] 檔案，請參閱 [使用Experience Manager中InDesign檔案的最佳實務](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. 若要產生手冊的PDF轉譯，請在對話方塊中選取Acrobat選項，然後按一下 **[!UICONTROL 繼續]**.
1. 附屬資料會在您開始使用的資料夾中建立。 若要檢視轉譯，請開啟宣傳品並選擇 **[!UICONTROL 轉譯]** 從GlobalNav清單。

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. 按一下轉譯清單中的PDF轉譯，即可下載PDF檔案。 開啟PDF檔案以檢閱附屬資料。

   ![chlimage_1-119](assets/chlimage_1-324.png)

## 合併附屬資料 {#merge-collateral}

1. 在 [!DNL Experience Manager] 介面點按 [!UICONTROL 資產] （位於導覽頁面）。

1. 從選項中選擇 **[!UICONTROL 範本]**.

1. 按一下 **[!UICONTROL 建立]** 和選擇 **[!UICONTROL 合併]** 功能表中的。

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. 從 [!UICONTROL 範本合併] 頁面，按一下 **[!UICONTROL 合併]** ![新增資產](assets/do-not-localize/assets_add_icon.png).

1. 切換作業選項至您要合併的附屬資產位置，按一下您要合併之附屬資產的縮圖，以選取它們。

   ![chlimage_1-122](assets/chlimage_1-327.png)

   您也可以從Omnisearch方塊搜尋範本。

   您可以瀏覽 [!DNL Experience Manager Assets] 存放庫或集合，然後導覽至所需範本的位置，然後選取它們以合併。

   您可以套用各種篩選器來搜尋所需的範本。 例如，您可以根據檔案型別或標籤來搜尋範本。

1. 按一下 **[!UICONTROL 下一個]** （從工具列）。
1. 在 **[!UICONTROL 預覽與重新排序]** 視需要重新排列範本，並預覽要合併的範本選擇。 然後，按一下 **[!UICONTROL 下一個]** （從工具列）。

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. 在 [!UICONTROL 設定範本] 畫面，指定附屬資料的名稱。 選擇性地指定您認為合適的任何標籤。 如果要以PDF格式匯出輸出，請選取 **[!UICONTROL Acrobat (.PDF)]**. 依預設，附屬品會以JPG匯出，並且 [!DNL InDesign] 格式。 若要變更多頁附屬資料的顯示縮圖，請按一下 **[!UICONTROL 變更縮圖]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. 按一下 **[!UICONTROL 儲存]** 然後按一下 **[!UICONTROL 確定]** 以關閉對話方塊。 多頁附屬資料會在您開始使用的資料夾中建立。

   >[!NOTE]
   >
   >您稍後無法編輯合併的宣傳品，也無法使用它來建立其他宣傳品。

## 最佳作法和限制 {#best-practices-limitations-tips}

* 此 [!DNL InDesign] 中的編輯器 [!DNL Experience Manager] 適用於標籤層級，且單一標籤下的所有文字都視為單一實體。 若要在編輯時保留文字格式和樣式，請分別標籤每個段落（或使用不同樣式的文字）。
