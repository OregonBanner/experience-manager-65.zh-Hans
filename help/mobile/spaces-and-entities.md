---
title: 空間與實體
seo-title: Developing AEM Mobile Content Services
description: 此頁面是開發AEM Mobile Content Services的登陸頁面。
seo-description: This page serves a landing page for developing AEM Mobile Content Services.
uuid: eab5a61b-a9e8-4863-90a3-df1f18510cd8
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ef568577-c74e-4fc2-b66e-eedac2948310
exl-id: 44591900-b01b-4a33-9910-839564477e7d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 1%

---

# 空間與實體{#spaces-and-entities}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

空間是儲存透過Content Services REST API公開之實體的便利位置。 這個方法特別實用，因為應用程式（或任何管道）可以與許多實體相關聯。 強制實體位於空間內會強制將應用程式的需求分組的最佳實務。 或者，您也可以將AEM中的應用程式與少量的空間建立關聯。

>[!NOTE]
>
>若要讓內容服務提供的任何管道都能使用，內容必須位於空格下。

## 建立空間 {#creating-a-space}

如果使用者想要將一棧內容和資產公開至行動應用程式，使用者會使用AEM Mobile儀表板建立空間。

初次有使用者未將Content Services設定為使用空格時，AEM Mobile儀表板在選取後只顯示應用程式 **內容服務**.

>[!CAUTION]
>
>**新增空間的先決條件**
>
>檢查 **啟用AEM內容服務** 以使用空間，並在AEM Mobile應用程式儀表板中啟用它。
>
>另請參閱 [管理內容服務](/help/mobile/developing-content-services.md) 以取得更多詳細資料。

在控制面板中設定空間後，請依照下列步驟建立空間：

1. 選擇 **空間** 來自Content Services。

   ![chlimage_1-83](assets/chlimage_1-83.png)

1. 選擇 **建立** 以建立空間。 輸入 **標題**， **名稱**、和 **說明** 以保留空間。

   单击&#x200B;**创建**。

   ![chlimage_1-84](assets/chlimage_1-84.png)

## 管理空間 {#managing-a-space}

建立空間後，按一下左側的「 」以管理清單中的空間。

您可以檢視空間的屬性、刪除空間，或將空間及其內容發佈到AEM發佈執行個體。

![chlimage_1-85](assets/chlimage_1-85.png)

**檢視和編輯空間屬性**

1. 從清單中選取空間
1. 選擇 **屬性** （從工具列）
1. 按一下 **關閉** 完成時

**發佈空間** 發佈空間時，也會發佈該空間中的所有資料夾和實體。

1. 按一下空間控制檯清單中的空間圖示以選取空間
1. 選擇 **發佈樹狀結構**

>[!NOTE]
>
>您可以 **取消發佈** 空格，會從發佈執行個體中移除空格。
>
>下圖說明發佈空間後可以執行的動作。

![chlimage_1-86](assets/chlimage_1-86.png)

## 使用空間中的資料夾 {#working-with-folders-in-a-space}

空間可包含資料夾，以協助進一步組織空間的內容和資產。 使用者可以在空間下建立自己的階層。

### 创建文件夹 {#creating-a-folder}

1. 按一下空間控制檯清單中的空間，然後按一下 **建立資料夾**

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. 輸入 **標題**， **名稱，** 和 **說明** 針對資料夾

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 按一下 **建立** 在空間中建立資料夾

## 语言复制 {#language-copy}

>[!CAUTION]
>
>語言副本無法在這個版本中完整運作。 它只會設定結構。

此 **語言副本** 功能可讓作者複製其主要語言副本，然後建立專案和工作流程以自動翻譯內容。 語言副本會建立正確的結構。 在分享空間新增資料夾後，您可以將語言副本新增至分享空間。

>[!NOTE]
>
>建議將所有可能翻譯的內容放在「語言副本」節點下。

### 新增語言副本 {#adding-language-copy}

1. 建立空間後，按一下該空間可建立語言副本。

   按一下 **建立** 並選擇 **語言副本**.

   ![chlimage_1-89](assets/chlimage_1-89.png)

   >[!NOTE]
   >
   >語言副本節點只能作為空間的直接子項存在。

1. 選擇 **內容套件語言&amp;ast；** 並輸入 **標題(&amp;A)；** 在 **建立語言副本** 對話方塊。

   单击&#x200B;**创建**。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 建立語言副本後，它就會顯示在您的分享空間中 **語言主版**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   >[!NOTE]
   >
   >選取 **語言主版** 以檢視語言副本資料夾。

### 從空間移除資料夾 {#removing-a-folder-from-the-space}

1. 從空間內容清單中選取資料夾
1. 按一下 **刪除** （從工具列）

   >[!NOTE]
   >
   >若要導覽至資料夾並檢視其內容或新增子資料夾或實體，請按一下空間內容清單中資料夾的標題。

## 使用空間中的實體 {#working-with-entities-in-a-space}

實體代表透過Web服務端點公開的內容。 實體儲存在空格中，以便輕鬆找到，並保持獨立於儲存其相關內容的AEM存放庫結構。

您可能想要在某些邏輯收集中將實體群組在一起。 若要這麼做，您可以建立任意數量的資料夾。

如果為資料建模收集了屬於其他圖元的圖元子項，則開發人員使用者可以從「圖元群組」模型型別建立特定的「群組模型」（現成可用）。

>[!NOTE]
>
>實體一律與空間相關聯，因此大多數實體使用者介面都是透過空間控制檯來存取。

### 建立實體 {#creating-an-entity}

1. 開啟分享空間主控台，然後按一下分享空間的標題。

   或者，您可以按一下清單中資料夾的標題，導覽至該資料夾。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 選擇圖元的模型。 這是您要建立的實體型別。 单击下一步。

   ![chlimage_1-93](assets/chlimage_1-93.png)

   >[!NOTE]
   >
   >您可以選擇使用 **資產模型**， **頁面模型**，或是您之前建立的圖元型別模型。
   >
   >另請參閱 [建立模型](/help/mobile/administer-mobile-apps.md)，以建立自訂實體。

1. 輸入 **標題**， **名稱**， **說明**、和 **標籤** 實體的。 单击&#x200B;**创建**。

   ![chlimage_1-94](assets/chlimage_1-94.png)

   完成後，實體會顯示在您空間的子代中。

### 編輯實體 {#editing-an-entity}

1. 建立實體後，請前往資料夾或分享空間，然後從分享空間控制檯中選擇要編輯的實體。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 選取要編輯的實體，然後按一下 **編輯**.

   ![chlimage_1-96](assets/chlimage_1-96.png)

   >[!CAUTION]
   >
   >根據您選擇建立實體的範本，用於編輯和檢視實體屬性的UI將有所不同。 如需更多詳細資訊，請參閱下列步驟。

   ***如果您選擇將實體建立為資產模型的範本***，按一下 **編輯** 可讓您新增資產，如下圖所示：

   ![chlimage_1-97](assets/chlimage_1-97.png)

   或者，您可以按一下 **預覽** 以檢視json連結。

   ![chlimage_1-98](assets/chlimage_1-98.png)

   ***如果您選擇用來建立實體作為頁面模型的範本***，按一下 **編輯** 可讓您新增資產，如下圖所示：

   ![chlimage_1-99](assets/chlimage_1-99.png)

   按一下 **路徑** 以新增資產

   ![chlimage_1-100](assets/chlimage_1-100.png)

   >[!NOTE]
   >
   >新增實體後，必須儲存該實體才能讓預覽連結運作。 若要檢視預覽，請按一下 **儲存**. 按一下 **預覽** 顯示新增資產的json，如下圖所示：

   ![chlimage_1-101](assets/chlimage_1-101.png)

   >[!NOTE]
   >
   >將資產新增至實體後，您可以選擇 **儲存** 儲存變更或選擇 **儲存並關閉** 以儲存並重新導向至已定義實體的空間控制檯清單。

   此外，從空間控制檯清單中選取一個實體，然後按一下 **屬性** 檢視和編輯已定義圖元的屬性。

   ![chlimage_1-102](assets/chlimage_1-102.png)

   您可以編輯標題、說明、標籤並將資產新增至實體。

   ![chlimage_1-103](assets/chlimage_1-103.png)

### 移除實體 {#removing-an-entity}

1. 從空間內容清單中選取實體

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. 按一下 **刪除** 從工具列移除特定實體

### 發佈實體 {#publishing-an-entity}

您可以選擇下列選項 **發佈樹狀結構** 或 **快速發佈** 以發佈您的實體。

1. 從空間控制檯清單中選取一個實體，然後按一下**發佈樹狀結構**以發佈該實體及其子項。

   ![chlimage_1-105](assets/chlimage_1-105.png)

   **或者**,

   按一下 **快速發佈** 以發佈該特定實體。
