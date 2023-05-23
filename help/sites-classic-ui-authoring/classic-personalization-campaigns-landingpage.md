---
title: 登录页面
seo-title: Landing Pages
description: 登入頁面功能可讓您快速輕鬆地直接將設計和內容匯入AEM頁面。 網頁開發人員可以準備HTML和其他資產，這些資產可以匯入為完整頁面或僅頁面的一部分。
seo-description: The landing pages feature allows quick and easy importing of a design and content right into an AEM page. A web developer can prepare the HTML and additional assets that can be imported as a full page or only a part of a page.
uuid: b294c43f-63ae-4b5b-bef0-04566e350b63
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 061dee36-a3bb-4166-a9c1-3ab7e4de1d1d
docset: aem65
exl-id: 0f1014a7-b0ba-4455-b3a4-5023bcd4c5a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3335'
ht-degree: 1%

---

# 登录页面{#landing-pages}

登入頁面功能可讓您快速輕鬆地直接將設計和內容匯入AEM頁面。 網頁開發人員可以準備HTML和其他資產，這些資產可以匯入為完整頁面或僅頁面的一部分。 對於建立僅在有限時間內生效且需要快速建立的行銷登入頁面，此功能非常有用。

此頁面說明下列內容：

* AEM中的登陸頁面（包括可用元件）外觀
* 如何建立登入頁面以及如何匯入設計套件
* 如何在AEM中使用登入頁面
* 如何設定行動登陸頁面

準備設計套件以進行匯入的相關說明請參閱 [擴充和設定Design Importer](/help/sites-administering/extending-the-design-importer-for-landingpages.md). 與Adobe Analytics整合的說明請參閱 [整合登入頁面與Adobe Analytics。](/help/sites-administering/integrating-landing-pages-with-adobe-analytics.md)

>[!CAUTION]
>
>Design Importer，用於匯入登入頁面， [已由AEM 6.5取代](/help/release-notes/deprecated-removed-features.md#deprecated-features).

>[!CAUTION]
>
>因為Design Importer需要存取 `/apps`，它無法在容器化的雲端環境中運作，因為 `/apps` 不可變動。

## 什麼是登陸頁面？ {#what-are-landing-pages}

登陸頁面是單一或多頁網站，是行銷宣傳的「端點」 — 例如電子郵件、廣告詞/橫幅、社群媒體。 登陸頁面有多種用途，但有一個共同點，即訪客應完成一項任務，並定義登陸頁面的成功。

AEM中的登陸頁面功能可讓行銷人員與代理商或內部創意團隊的網頁設計人員合作，建立可輕鬆匯入AEM中，且行銷人員仍可編輯的頁面設計，並發佈於與其他AEM支援網站的治理之下。

在AEM中，您可以執行下列步驟來建立登入頁面：

1. 在AEM中建立包含登入頁面畫布的頁面。 AEM隨附一個範例，稱為 **匯入工具頁面**.

1. [準備HTML和資產。](/help/sites-administering/extending-the-design-importer-for-landingpages.md)
1. 將資源封裝成ZIP檔案（這裡稱為「設計封裝」）。
1. 在匯入工具頁面上匯入設計套件。
1. 修改並發佈頁面。

### 案頭登陸頁面 {#desktop-landing-pages}

AEM中的範例登入頁面如下所示：

![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 行動登陸頁面 {#mobile-landing-pages}

登入頁面也可以有頁面的行動版本。 若要使用不同的行動版登入頁面，匯入設計必須擁有兩個html檔案： *index.htm(l)* 和 *mobile.index.htm(l)*.

登陸頁面匯入程式與一般登陸頁面的程式相同，登陸頁面設計會有一個與行動登陸頁面對應的額外html檔案。 此html檔案也必須有畫布 `div` 替換為 `id=cqcanvas` 就像案頭登陸頁面html一樣，其支援案頭登陸頁面所述的所有可編輯元件。

行動登陸頁面會建立為案頭登陸頁面的子頁面。 若要開啟此頁面，請導覽至網站中的登陸頁面，然後開啟子頁面。

![chlimage_1-22](assets/chlimage_1-22.png)

>[!NOTE]
>
>如果案頭登陸頁面被刪除或停用，行動登陸頁面會與案頭登陸頁面一起被刪除/停用。

## 登陸頁面元件 {#landing-page-components}

若要讓匯入的HTML部分可在AEM內編輯，您可以直接將登入頁面HTML內的內容對應至AEM元件。 設計匯入工具瞭解下列預設元件：

* 文字，適用於任何文字
* 標題，適用於H1-6標籤中的內容
* 影像，適用於應該可交換的影像
* 行動號召：

   * 點進連結
   * 图形链接

* CTA銷售機會表單，用於擷取使用者資訊
* 段落系統(Parsys)，以允許新增任何元件，或轉換上述元件

此外，您也可以擴充此功能並支援自訂元件。 本節詳細說明元件。

### 文本 {#text}

文字元件可讓您使用WYSIWYG編輯器輸入文字區塊。 另請參閱 [文字元件](/help/sites-authoring/default-components.md#text) 以取得詳細資訊。

![chlimage_1-23](assets/chlimage_1-23.png)

以下為登入頁面上的文字元件範例：

![chlimage_1-24](assets/chlimage_1-24.png)

#### 标题 {#title}

標題元件可讓您顯示標題並設定大小(h1-6)。 另請參閱 [標題元件](/help/sites-authoring/default-components.md#title) 以取得詳細資訊。

![chlimage_1-25](assets/chlimage_1-25.png)

以下為登入頁面上的標題元件範例：

![chlimage_1-26](assets/chlimage_1-26.png)

#### 图像 {#image}

影像元件會顯示您可以從「內容尋找器」拖放或按一下以上傳的影像。 另請參閱 [影像元件](/help/sites-authoring/default-components.md) 以取得詳細資訊。

![chlimage_1-27](assets/chlimage_1-27.png)

以下是登陸頁面上影像元件的範例：

![chlimage_1-28](assets/chlimage_1-28.png)

#### 呼叫動作(CTA) {#call-to-action-cta}

登陸頁面設計可能包含數個連結 — 其中某些連結的目的可能為「行動號召」。

行動號召(CTA)是用來讓訪客在登陸頁面上立即採取行動，例如「立即訂閱」、「檢視此影片」、「限時觀看」等。

* 點進連結 — 可讓您新增文字連結，當按一下連結時，會將訪客導向至目標URL。
* 圖形連結 — 可讓您新增影像，在按一下時讓訪客前往目標URL。

兩個CTA元件都有類似的選項。 點進連結有其他RTF文字選項。 以下段落將詳細介紹這些元件。

#### 點進連結 {#click-through-link}

此CTA元件可用來在登入頁面上新增文字連結。 可以按一下該連結，將使用者引導至元件屬性中指定的目標URL。 它是「號召性用語」群組的一部分。

![chlimage_1-29](assets/chlimage_1-29.png)

**標籤** 使用者看到的文字。 您可以使用RTF編輯器修改格式。

**目標URL** 輸入使用者按一下文字時要造訪的URI。

**演算選項** 說明轉譯選項。 您可從下列專案選取：

* 在新浏览器窗口中加载页面
* 在当前窗口中加载页面
* 在父框架中載入頁面
* 取消所有框架，並在完整瀏覽器視窗中載入頁面

**CSS** 在「樣式」標籤上，輸入CSS樣式表的路徑。

**ID** 在「樣式」標籤上，輸入元件的ID以進行唯一識別。

以下是點進連結的範例：

![chlimage_1-30](assets/chlimage_1-30.png)

#### 图形链接 {#graphical-link}

此CTA元件可用來新增登陸頁面上具有連結的任何圖形影像。 影像可以是簡單的按鈕，也可以是任何圖形影像作為背景。 按一下影像時，使用者會被帶往元件屬性中指定的目標URL。 它是 **行動號召** 群組。

![chlimage_1-31](assets/chlimage_1-31.png)

**標籤** 使用者在圖形中看到的文字。 您可以使用RTF編輯器修改格式。

**目標URL** 輸入使用者按一下影像時要造訪的URI。

**演算選項** 說明轉譯選項。 您可從下列專案選取：

* 在新浏览器窗口中加载页面
* 在当前窗口中加载页面
* 在父框架中載入頁面
* 取消所有框架，並在完整瀏覽器視窗中載入頁面

**CSS** 在「樣式」標籤上，輸入CSS樣式表的路徑。

**ID** 在「樣式」標籤上，輸入元件的ID以進行唯一識別。

以下是範例圖形連結：

![chlimage_1-32](assets/chlimage_1-32.png)

### 呼叫動作(CTA)銷售機會表單 {#call-to-action-cta-lead-form}

潛在客戶表單是用於收集訪客/潛在客戶設定檔資訊的表單。 此資訊可以儲存並稍後使用，以根據資訊進行有效的行銷。 此資訊通常包括標題、名稱、電子郵件、出生日期、地址、興趣等。 它是 **CTA銷售機會表單** 群組。

CTA銷售機會表單範例看起來像這樣：

![chlimage_1-33](assets/chlimage_1-33.png)

CTA銷售機會表單由數個不同的元件組成：

* **潛在客戶表單**
潛在客戶表單元件會定義頁面上新潛在客戶表單的開始和結束。 其他元件可置於這些元素之間，例如電子郵件ID、名字等。

* **表單欄位和元素**
表單欄位和元素可包含文字方塊、選項按鈕、影像等。 使用者通常會在表單欄位中完成動作，例如輸入文字。 如需詳細資訊，請參閱個別表單元素。

* **設定檔元件**
個人資料元件與用於社交合作和需要訪客個人化的其他領域的訪客個人資料相關。

上圖顯示了一個範例表單；它由 **潛在客戶表單** 元件（開始和結束），使用 **名字** 和 **電子郵件ID** 用於輸入和的欄位 **提交** 欄位

在sidekick中，以下元件可用於CTA銷售機會表單：

![chlimage_1-34](assets/chlimage_1-34.png)

#### 許多潛在客戶表單元件的通用設定 {#settings-common-to-many-lead-form-components}

雖然每個銷售機會表單元件都有不同的用途，但許多是由類似的選項和引數所組成。

設定任何表單元件時，可在對話方塊中使用下列標籤：

* **標題和文字**
您需要在此指定基本資訊，例如元件的標題和任何隨附文字。 在適當的情況下，它也可讓您定義其他關鍵資訊，例如欄位是否可多重選取，以及是否可供選取的專案。

* **初始值**
可讓您指定預設值。

* **限制**
您可以在此指定欄位是否為必要欄位，並將限制放置在該欄位上（例如，必須是數值等）。

* **樣式**
指示欄位的大小和樣式。

>[!NOTE]
>
>您看到的欄位會依個別元件而異。
>
>並非所有潛在客戶表單元件都可使用所有選項。 如需這些專案的詳細資訊，請參閱Forms [通用設定](/help/sites-authoring/default-components.md#formsgroup).

#### 潛在客戶表單元件 {#lead-form-components}

下節說明號召性用語潛在客戶表單可用的元件。

**關於** 可讓使用者新增關於資訊。

![chlimage_1-35](assets/chlimage_1-35.png)

**位址列位** 允許使用者輸入地址資訊。 設定此元件時，您必須在對話方塊中輸入元素名稱。 元素名稱是表單元素的名稱。 這表示儲存資料在存放庫中的位置。

![chlimage_1-36](assets/chlimage_1-36.png)

**出生日期** 使用者可以輸入出生日期資訊。

![chlimage_1-37](assets/chlimage_1-37.png)

**電子郵件ID** 允許使用者輸入電子郵件地址（識別碼）。

![chlimage_1-38](assets/chlimage_1-38.png)

**名字** 提供欄位讓使用者輸入其名字。

![chlimage_1-39](assets/chlimage_1-39.png)

**性別** 使用者可從下拉式清單中選取其性別。

![chlimage_1-40](assets/chlimage_1-40.png)

**姓氏** 使用者可以輸入姓氏資訊。

![chlimage_1-41](assets/chlimage_1-41.png)

**潛在客戶表單** 新增此元件以將潛在客戶表單新增至您的登入頁面。 潛在客戶表單會自動包含「潛在客戶表單的開始」和「潛在客戶表單的結束」欄位。 在兩者之間，您新增本節中說明的Lead Form元件。

![chlimage_1-42](assets/chlimage_1-42.png)

「銷售機會表單」元件使用 **表單開始** 和 **表單結尾** 元素。 兩者一律成對，以確保表單已正確定義。

新增銷售機會表單後，您可以按一下「 」，設定表單的開頭或結尾 **編輯** 在對應列中。

**潜在客户表单的开头**

有兩個標籤可供設定 **表單** 和 **進階**：

![chlimage_1-43](assets/chlimage_1-43.png)

**感謝頁面** 要參照以感謝訪客提供其輸入的頁面。 如果保留為空白，表單會在提交後重新顯示。

**開始工作流程** 決定提交潛在客戶表單後觸發的工作流程。

![chlimage_1-44](assets/chlimage_1-44.png)

**張貼選項** 下列張貼選項可供使用：

* 创建潜在客户
* 電子郵件服務：建立訂閱者並新增至清單 — 如果您使用ExactTarget等電子郵件服務提供者，請使用。
* 電子郵件服務：傳送自動回應的電子郵件 — 如果您使用ExactTarget等電子郵件服務提供者，請使用。
* 電子郵件服務：從清單中取消訂閱使用者 — 如果您使用ExactTarget等電子郵件服務提供者，請使用。
* 取消訂閱使用者

**表單識別碼** 表單識別碼可唯一識別潛在客戶表單。 如果您在單一頁面上有多個表單，請使用表單識別碼；請確定它們有不同的識別碼。

**載入路徑** 是節點屬性的路徑，用於將預先定義的值載入潛在客戶表單欄位。

此選擇性欄位指定存放庫中節點的路徑。 當此節點具有符合欄位名稱的屬性時，則表單上的適當欄位將使用這些屬性的值預先載入。 如果不存在相符專案，則欄位包含預設值。

**使用者端驗證** 指出此表單是否需要使用者端驗證（伺服器驗證一律發生）。 這可與Forms Captcha元件搭配使用。

**驗證資源型別** 如果您想要驗證整個潛在客戶表單（而不是個別欄位），請定義表單驗證資源型別。

如果您要驗證完整的表單，請一併包含下列其中一項：

* 使用者端驗證的指令碼：
   ` /apps/<myApp>/form/<myValidation>/formclientvalidation.jsp`

* 伺服器端驗證的指令碼：
   ` /apps/<myApp>/form/<myValidation>/formservervalidation.jsp`

**動作設定** 根據「發佈選項」中的選取專案，「動作組態」會變更。 例如，當您選取「建立銷售機會」時，可以設定要新增銷售機會的清單。

![chlimage_1-45](assets/chlimage_1-45.png)

* **顯示提交按鈕**
指示是否應該顯示提交按鈕。

* **提交名稱**
識別碼（如果您在表單中使用多個提交按鈕）。

* **提交標題**
按鈕上顯示的名稱，例如「提交」或「傳送」。

* **顯示重設按鈕**
選取核取方塊以顯示「重設」按鈕。

* **重設標題**
顯示在[重設]按鈕上的名稱。

* **說明**
顯示在按鈕下方的資訊。

## 建立登入頁面 {#creating-a-landing-page}

建立登入頁面時，您需要執行三個步驟：

1. 建立匯入工具頁面。
1. [準備HTML以匯入。](/help/sites-administering/extending-the-design-importer-for-landingpages.md)
1. 匯入設計封裝。

### 使用設計匯入工具 {#use-of-the-design-importer}

由於匯入頁面涉及準備HTML、驗證和測試頁面，因此匯入登入頁面旨在作為管理員任務。 作為管理員，執行匯入的使用者需要對下列專案的讀取、寫入、建立和刪除許可權： `/apps`. 如果使用者沒有這些許可權，匯入將會失敗。

>[!NOTE]
>
>由於設計匯入工具旨在作為管理工具，需要下列專案的讀取、寫入、建立及刪除許可權： `/apps`，Adobe不建議在生產環境中使用設計匯入工具。

Adobe建議在中繼執行個體上使用設計匯入工具。 在中繼執行個體上，開發人員可測試和驗證匯入，然後負責將程式碼部署到生產執行個體。

### 建立匯入工具頁面 {#creating-an-importer-page}

您必須先建立匯入工具頁面，才能匯入登入頁面設計，例如在行銷活動底下。 「匯入者頁面」範本可讓您匯入完整的HTML登陸頁面。 此頁面包含一個放置方塊，可在其中使用拖放功能匯入登入頁面設計套件。

>[!NOTE]
>
>依預設，您只能在行銷活動底下建立Importer頁面，但您也可以覆蓋此範本，以便在下方建立登入頁面 `/content/mysite`.

若要建立新的登入頁面：

1. 前往 **網站** 主控台。
1. 在左窗格中選取您的行銷活動。
1. 按一下 **新增** 以開啟 **建立頁面** 視窗。
1. 選取 **匯入工具頁面** 範本並新增標題，也可選擇新增名稱，然後按一下 **建立**.

   ![chlimage_1-1-1](assets/chlimage_1-1-1.png)

   此時會顯示您的新匯入工具頁面。

### 準備匯入的HTML {#preparing-the-html-for-import}

在匯入設計套件之前，需要準備HTML。 另請參閱 [延伸與設定設計匯入](/help/sites-administering/extending-the-design-importer-for-landingpages.md) 以取得詳細資訊。

### 匯入設計封裝 {#importing-the-design-package}

建立匯入工具頁面後，您可以將設計封裝匯入到該頁面上。 有關建立設計套件及其建議結構的詳細資訊，請參閱 [延伸與設定設計匯入](/help/sites-administering/extending-the-design-importer-for-landingpages.md).

假設您已準備好設計封裝，下列步驟會說明如何將設計封裝匯入至匯入工具頁面。

1. 開啟匯入工具頁面，您 [建立時間較早](#creatingablankcanvaspage).

   ![chlimage_1-46](assets/chlimage_1-46.png)

1. 將設計套件拖放至投寄箱上。 請注意，當將套件拖曳到它上面時，箭頭會改變方向。
1. 拖放後，您會看到登陸頁面，而非Importer頁面。 您的HTML登陸頁面已成功匯入。

   ![chlimage_1-2-1](assets/chlimage_1-2-1.png)

>[!NOTE]
>
>匯入時，標籤會因為安全性原因而經過消毒，以避免匯入和發佈無效的標籤。 這假設僅限HTML的標籤和所有其他形式的元素(例如內嵌SVG或Web元件)將被篩選掉。

>[!NOTE]
>
>如果您無法匯入設計套件，請參閱 [疑難排除](/help/sites-administering/extending-the-design-importer-for-landingpages.md#troubleshooting).

## 使用登入頁面 {#working-with-landing-pages}

登入頁面的設計和資產通常由設計人員建立，而設計人員可能會在其常用的工具(例如Adobe Photoshop或Adobe Dreamweaver)中於代理商處進行。 設計完成後，設計人員會傳送包含所有資產的zip檔案給行銷。 然後，行銷中的聯絡人負責將zip檔案拖放到AEM中並發佈內容。

此外，設計人員可能需要在登入頁面匯入後透過編輯或刪除內容及設定號召動作元件對其進行修改。 最後，行銷人員會想要預覽登入頁面，然後啟動行銷活動以確保登入頁面已發佈。

本節說明如何執行下列作業：

* 刪除登入頁面
* 下載設計封裝
* 檢視匯入資訊
* 重設登入頁面
* [設定CTA元件並將內容新增至頁面](#call-to-action-cta)
* 預覽登入頁面
* 啟用/發佈登入頁面

當您匯入設計封裝時， **清除設計** 和 **下載匯入的壓縮檔** 可在頁面的「設定」功能表中取得：

![chlimage_1-3-1](assets/chlimage_1-3-1.png)

### 下載匯入的設計封裝 {#downloading-the-imported-design-package}

下載zip檔案可讓您記錄哪一個zip檔案已使用特定登陸頁面匯入。 請注意，頁面上所做的變更不會新增至zip。

若要下載匯入的設計封裝，請按一下 **下載Zip** （位於登入頁面工具列中）。

### 檢視匯入資訊 {#viewing-import-information}

您可以隨時在傳統使用者介面中按一下登陸頁面頂端的藍色驚歎號，以檢視上次匯入的相關資訊。

![chlimage_1-47](assets/chlimage_1-47.png)

如果匯入的設計封裝發生一些問題，例如，如果它參照的影像/指令碼在封裝內不存在，則設計匯入工具會以清單的形式顯示此類問題。 若要檢視問題清單，請在典型的使用者介面中，按一下登陸頁面工具列中的「問題」連結。 在下圖中，按一下 **問題** 連結會開啟「匯入問題」視窗。

![chlimage_1-3](assets/chlimage_1-3.jpeg)

### 重設登入頁面 {#resetting-a-landing-page}

如果您想在對登入頁面設計套件進行某些變更後重新匯入此套件，您可以按一下「 」來「清除」登入頁面 **清除** 在傳統使用者介面的登入頁面頂端，或按一下觸控最佳化使用者介面之設定功能表中的「清除」 。 這麼做會刪除匯入的登陸頁面，並建立空白的匯入工具頁面。

清除登入頁面時，您可以移除內容變更。 如果您按一下 **否**，則會保留內容變更，即下的結構 `jcr:content/importer`「 」會保留，且只會保留importer頁面元件和中的資源 `etc/design` 已移除。 然而，如果您按一下 **是**，則 `jcr:content/importer` 也會被移除。

>[!NOTE]
>
>如果您決定移除內容變更，則您在匯入的登陸頁面上進行的所有變更，以及所有頁面屬性，都會在您按一下時遺失 **清除**.

### 在登入頁面上修改和新增元件 {#modifying-and-adding-components-on-a-landing-page}

若要修改登入頁面上的元件，請連按兩下這些元件，以開啟它們並像編輯任何其他元件一樣進行編輯。

若要在登入頁面上新增元件，請拖放元件至登入頁面（從傳統使用者介面中的Sidekick或從觸控最佳化使用者介面中的「元件」窗格），並視需要編輯。

>[!NOTE]
>
>如果登入頁面上的元件無法編輯，您必須在之後重新匯入zip檔案 [修改HTML檔案。](/help/sites-administering/extending-the-design-importer-for-landingpages.md) 這表示在匯入期間，不可編輯的零件未轉換為AEM元件。

### 刪除登入頁面 {#deleting-a-landing-page}

刪除登入頁面就像刪除一般AEM頁面。

唯一的例外是當您刪除案頭登陸頁面時，也會刪除對應的行動登陸頁面（如果存在），但反之則不會。

### 發佈登入頁面 {#publishing-a-landing-page}

您可以發佈登入頁面及其所有相依性，就像發佈一般頁面一樣。

>[!NOTE]
>
>發佈案頭登入頁面也會發佈其對應的行動版本（如果有的話）。 但發佈行動登陸頁面不會發佈案頭版本。
