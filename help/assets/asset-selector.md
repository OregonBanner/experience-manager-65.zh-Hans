---
title: 資產選擇器
description: 瞭解如何使用資產選擇器來搜尋、篩選、瀏覽和擷取Adobe Experience Manager資產中的資產中繼資料。 也瞭解如何自訂資產選擇器介面。
contentOwner: Adobe
feature: Asset Management,Metadata,Search
role: User
exl-id: 4b518ac0-5b8b-4d61-ac31-269aa1f5abe4
source-git-commit: 0c6c269e9f0cbdcc0c5e3b925ef09b9923cbb2b3
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# 資產選擇器 {#asset-selector}

>[!NOTE]
>
>已呼叫資產選擇器 [資產選取器](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) 在舊版中 [!DNL Experience Manager].

資產選擇器可讓您瀏覽、搜尋及篩選中的資產 [!DNL Adobe Experience Manager] 資產。 您也可以擷取使用資產選擇器選取的資產中繼資料。 若要自訂資產選擇器介面，您可以使用支援的請求引數來啟動它。 這些引數會為特定案例設定資產選擇器的內容。

目前，您可以傳遞請求引數 `assettype` (*影像/影片/文字*)和選取範圍 `mode` (*單一/多個*)做為資產選擇器的內容相關資訊，在整個選取範圍中維持不變。

資產選擇器使用HTML5 **Window.postMessage** 傳送所選資產的資料給收件者的訊息。

資產選擇器以Granite的基礎選取器辭彙為基礎。 依預設，資產選擇器會以瀏覽模式運作。 不過，您可以使用Omnisearch體驗套用篩選器，以縮小特定資產的搜尋範圍。

您可以將任何網頁（無論它是否為CQ容器的一部分）與資產選擇器(`https://[AEM_server]:[port]/aem/assetpicker.html`)。

## 內容引數 {#contextual-parameters}

您可以在URL中傳遞下列請求引數，以啟動特定內容中的資產選擇器：

| 名称 | 值 | 示例 | 用途 |
|---|---|---|---|
| 資源字尾(B) | 在URL中作為資源尾碼的資料夾路徑：`http://localhost:4502/aem/`<br>`assetpicker.html/<folder_path>` | 在選取特定資料夾的情況下（例如使用資料夾）啟動資產選擇器 `/content/dam/we-retail/en/activities` 選取時，URL的格式應為： `http://localhost:4502/aem/assetpicker.html`<br>`/content/dam/we-retail/en/activities?assettype=images` | 如果您在啟動資產選擇器時要求選擇特定資料夾，請將其傳遞為資源尾碼。 |
| 模式 | 單一，多個 | `http://localhost:4502/aem/assetpicker.html`<br>`?mode=multiple` <br> `http://localhost:4502/aem/assetpicker.html`<br>`?mode=single` | 在多重模式中，您可以使用資產選擇器同時選取多個資產。 |
| 对话框 | true， false | `http://localhost:4502/aem/assetpicker.html`<br>`?dialog=true` | 使用這些引數開啟資產選擇器作為Granite對話方塊。 只有當您透過Granite路徑欄位啟動資產選擇器，並將其設定為pickerSrc URL時，此選項才適用。 |
| 根 | `<folder_path>` | `http://localhost:4502/aem/`<br>`assetpicker.html?assettype=images`<br>`&root=/content/dam/we-retail/en/activities` | 使用此選項可指定資產選擇器的根資料夾。 在此情況下，資產選擇器可讓您僅選取根資料夾下的子資產（直接/間接）。 |
| 檢視模式 | 搜索 |  | 若要在搜尋模式中啟動資產選擇器，請使用assettype和mimetype引數。 |
| assettype (S) | 影像、檔案、多媒體、封存 | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives`</li> | 使用此選項可依據傳遞的值來篩選資產型別。 |
| mimetype | mimetype (`/jcr:content/metadata/dc:format`) （也支援萬用字元） | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=image/png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&?mimetype=*png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=*presentation`</li>  <li>`http://localhost:4502/aem/assetpicker?viewmode=search&mimetype=*presentation&mimetype=*png`</li></ul> | 使用它根據MIME型別篩選資產 |

## 使用資產選擇器 {#using-the-asset-selector}

1. 若要存取資產選擇器介面，請前往 `https://[AEM_server]:[port]/aem/assetpicker`.
1. 導覽至所需的資料夾，然後選取一或多個資產。

   ![chlimage_1-441](assets/chlimage_1-441.png)

   或者，您也可以從OmniSearch方塊搜尋所需的資產，然後選取該資產。

   ![chlimage_1-442](assets/chlimage_1-442.png)

   如果您使用OmniSearch方塊來搜尋資產，您可以從 **[!UICONTROL 篩選器]** 窗格以縮小搜尋範圍。

   ![chlimage_1-443](assets/chlimage_1-443.png)

1. 點選/按一下 **[!UICONTROL 選取]** （從工具列）。
