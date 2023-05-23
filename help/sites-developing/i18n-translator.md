---
title: 使用翻譯工具管理字典
seo-title: Using Translator to Manage Dictionaries
description: AEM提供一個主控台，用於管理元件UI中使用的各種文字翻譯
seo-description: AEM provides a console for managing the various translations of texts used in component UI
uuid: 4eea3110-e958-473e-8d22-c84fa435edbd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: adf3364c-11f1-45c6-b41d-2c7d48b626f9
exl-id: a8d50c09-72d0-406e-874e-50a985227a56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2325'
ht-degree: 0%

---

# 使用翻譯工具管理字典{#using-translator-to-manage-dictionaries}

AEM提供一個主控台，用於管理元件UI中使用的各種文字翻譯。 此主控台位於

`https://<hostname>:<port-number>/libs/cq/i18n/translator.html`

使用翻譯工具管理英文字串及其翻譯。 字典建立於存放庫中，例如/apps/myproject/i18n。

請注意，您管理的翻譯工具與字典用於以不同語言呈現元件UI。 如果您想要翻譯頁面或使用者產生的內容，請參閱 [翻譯多語言網站的內容](/help/sites-administering/translation.md) 和 [翻譯使用者產生的內容](/help/communities/translate-ugc.md).

>[!CAUTION]
>
>僅編輯為專案建立且位於下的字典 `/apps`.
>
>此工具中也提供AEM系統字典。 請勿變更AEM系統字典，因為這會導致AEM UI發生問題。 此外，升級時可能會遺失變更。 AEM系統字典位於 `/libs`.

>[!NOTE]
>
>雖然「翻譯工具」具有典型的UI介面，但無論發現片語的介面為何，都將其用於片語的翻譯。

譯者會列出AEM中使用的文字，並附帶各種語言翻譯：

![chlimage_1-205](assets/chlimage_1-205.png)

您可以搜尋、篩選及編輯英文與翻譯過的文字。 您也可以將字典匯出為XLIFF格式進行翻譯，然後將翻譯匯回字典。

您也可以從此主控台將i18n字典新增至翻譯專案。 您可以建立新專案或將其新增至現有專案。

1. 按一下 **翻譯字典**.

   ![chlimage_1-206](assets/chlimage_1-206.png)

1. 視需要選取建立或新增選項。 對話方塊開啟。

   ![chlimage_1-207](assets/chlimage_1-207.png)

1. 視需要填寫欄位，然後按一下「確定」。 ![chlimage_1-208](assets/chlimage_1-208.png)

1. 您現在可以按一下 **確定** 或參閱目標字典。

   >[!NOTE]
   >
   >如需翻譯專案的詳細資訊，請閱讀 [管理翻譯專案](/help/sites-administering/tc-manage.md).

## 建立字典 {#creating-a-dictionary}

建立字典來管理本地化的UI字串。 建立字典後，您可以使用翻譯工具來管理字典。

1. 使用CRXDE Lite新增根節點( `sling:Folder`)作為存放語言定義的結構時，請使用下列文字：

   ` /apps/<projectName>/i18n`

   例如，`/apps/myProject/i18n`

1. 在此根下新增所需的語言結構。 例如：

   ```shell
   /apps/myProject/i18n [sling:Folder]
       - de.json [nt:file] [mix:language]
           + jcr:language = de
       - fr.json [nt:file] [mix:language]
           + jcr:language = fr
   ```

   >[!NOTE]
   >
   >這是以下專案的結構： [Sling i18n模組](https://sling.apache.org/site/internationalization-support.html).

1. 重新載入翻譯程式和字典路徑(例如 `/apps/myProject/i18n`)會顯示在工具列的下拉式選取器中。 選取此項以開始新增字串及其翻譯。

   >[!NOTE]
   >
   >翻譯人員只會儲存路徑下實際存在的語言的翻譯(例如 `/apps/myProject/i18n`)。
   >
   >請確定這些對應至格線中所顯示的語言。

## 管理字典字串 {#managing-dictionary-strings}

使用翻譯工具來管理字典中的字串。 您可以新增、修改和移除英文字串，也可以提供翻譯字串。

>[!CAUTION]
>
>僅編輯為專案建立且位於下的字典 `/apps`.
>
>請勿變更AEM系統字典，因為這會導致AEM UI發生問題。 此外，升級時可能會遺失變更。 AEM系統字典位於 `/libs`.

### 新增、變更和移除字串 {#adding-changing-and-removing-strings}

將英文字串新增至元件已國際化的字典。 僅新增國際化字串，以免翻譯未使用的字串而浪費資源。

您新增至字典的字串必須與程式碼中指定的字串完全相符。 如果程式碼中使用的預設英文字串與字典中的英文字串不符，則轉譯的字串不會視需要出現在UI中。 字串區分大小寫。

**提供翻譯提示**

使用字典字串的Commenet屬性，為翻譯人員提供資訊以釐清字串的含義。 通常UI會協助使用者判斷不明確字詞的含義。 不過，譯者在UI的內容中看不到字串。 翻譯提示可移除模稜兩可之處。 例如，註解可協助翻譯人員瞭解英文單詞Request是用作名詞而非動詞。

翻譯提示也可區分相同或有不同含義的字串。 例如，「搜尋」一詞可以是名詞或動詞，在字典中需要兩個「搜尋」專案，並有兩個不同的翻譯提示。 要求字串的程式碼也包含翻譯提示，以便在UI中使用正確的字串。

**包含索引變數**

在本地化字串中加入變數，將內容涵義建置到句子中。 例如，登入Web應用程式後，首頁會顯示訊息「歡迎回來管理員」。 您的收件匣中有2封郵件。」 頁面內容決定使用者名稱和訊息數。

若要在本地化字串中加入變數，請在get方法的第一個引數中，將括弧內的索引放在變數的位置。 使用本地化提示來說明值。 翻譯人員必須瞭解變數的意義，因為不同的語言會使用不同的句子結構。

請注意 [要求已翻譯字串的程式碼](/help/sites-developing/i18n-dev.md#including-variables-in-localized-sentences) 根據內容提供索引變數的值。

例如，當使用者登入網站時，下列字串會出現，並包含在字典中：

`Welcome back {0}. You have {1} messages.`

下列註解說明變數：

`{0} = the user name, {1} = the number of items in the user's inbox`

**修改字串**

在程式碼中變更或移除英文字串時，變更或移除這些字串。 當您變更字串時，原始字串會持續存在，並會產生反映變更的新字串。 在移除字串之前，請確定沒有程式碼使用它。

使用以下程式來新增字串。

1. 在「字典」下拉式選單中，選取要新增字串的字典。 在下拉式選單中，字典在存放庫中由其路徑表示。
1. 按一下「字串與翻譯」表格上方的「新增」 。

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. 在「新增字串」對話方塊的「字串」方塊中，輸入英文字串。 在「註解」方塊中，視需要鍵入翻譯器的翻譯提示。
1. 单击确定。
1. 单击“保存”。

   ![chlimage_1-210](assets/chlimage_1-210.png)

使用以下程式來變更字典中的字串。

1. 在「字典」下拉式選單中，選取包含要變更之字串的字典。
1. 連按兩下要變更的字串。
1. 在「編輯字串」(Edit String)對話方塊中，選取「修改字串」(Modify String)或「註釋」(Comment) （建立副本）。

   ![chlimage_1-211](assets/chlimage_1-211.png)

1. 修改字串或註解，然後按一下「確定」。
1. 单击“保存”。

   ![chlimage_1-212](assets/chlimage_1-212.png)

使用以下程式，從字典中移除字串。

1. 在「字典」下拉式選單中，選取您要移除字串的字典。
1. 单击删除。

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. 单击“保存”。

   ![chlimage_1-214](assets/chlimage_1-214.png)

### 搜尋字串 {#searching-for-strings}

翻譯工具底部的搜尋列提供字串選取選項：

* **依文字篩選：** 與英文字串、註解或翻譯相符的模式。 只有符合全部或部分圖樣的專案才會出現在表格中。
* **變更：任何、已修改、新增、已刪除：** 顯示已變更但未儲存的專案。

   * 任何：顯示已修改、新增或移除的專案。
   * 已修改：顯示已變更的專案。
   * 新增：顯示新增的專案。
   * 已刪除：顯示要移除的專案。
   * 多重選擇：顯示具有所有選定屬性的專案。

* **有註解**：顯示含有翻譯人員註解的專案。
* **缺少翻譯：** 顯示至少一種語言沒有翻譯的專案。

![chlimage_1-215](assets/chlimage_1-215.png)

1. 在搜尋列上，選取篩選選項。
1. 若要使用選項進行篩選，請按一下「篩選」。
1. 若要移除篩選器並檢視字典中的所有專案，請按一下「清除」。

### 編輯翻譯的字串 {#editing-translated-strings}

將英文字串新增至字典後，您就可以新增字串的翻譯。 您也可以 [匯出字典](/help/sites-developing/i18n-translator.md#exporting-a-dictionary) 讓第三方翻譯它。

1. 選取 [您的專案特定字典](#creating-a-dictionary) 因為它會指定存放庫中儲存翻譯的路徑。 例如，選取 **字典** 作為：

   `/apps/myProject/i18n`

   >[!CAUTION]
   >
   >僅編輯為專案建立且位於下的字典 `/apps`.
   >
   >此工具中也提供AEM系統字典。 請勿變更AEM系統字典，因為這會導致AEM UI發生問題。 此外，升級時可能會遺失變更。 AEM系統字典位於 `/libs`.

1. 若要編輯其中一個字串的翻譯文字，您可以：

   * 連按兩下所需字串的適當語言，即可編輯該單一文字：

   ![chlimage_1-216](assets/chlimage_1-216.png)

   * 按兩下 **字串** 或 **註解** 必要字串的欄位以開啟 **編輯字串** 對話方塊，視需要編輯翻譯，然後按一下 **確定** 若要關閉對話方塊：

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 按一下 **儲存** 以認可您的變更。

   >[!NOTE]
   >
   >按一下 **重設和重新整理** (而非 **儲存**)會回覆先前文字的任何變更。

## 使用協力廠商翻譯人員 {#using-third-party-translators}

為了支援使用協力廠商翻譯服務，翻譯工具可讓您匯出和匯入字典。

### 匯出字典 {#exporting-a-dictionary}

將字典匯出至XLIFF檔案，讓第三方服務可以翻譯字典字串。

* 匯出字典並包含英語和語言的翻譯辭彙。
* 僅匯出部分或全部英文字串。

當您匯出XLIFF檔案並包含語言時，存放庫中字典的節點結構必須包含該語言。 如果未包含語言，則會發生錯誤。 例如，若要匯出法文XLIFF檔案，字典資料夾必須包含 `mix:language` 子節點已命名 `fr`. (請參閱 [建立字典](/help/sites-developing/i18n-translator.md#creating-a-dictionary).)

使用以下程式匯出特定語言的XLIFF檔案。

1. 開啟翻譯工具 `http://<host>:<port>/libs/cq/i18n/translator.html`
1. 使用字典下拉式選單來選取要匯出的字典。
1. 按一下「匯出>完全匯出」 *XX* Xliff選項，其中 *XX* 是兩個字母的語言代碼，例如DE或FR。

   XLIFF檔案會在新標籤或視窗中開啟。

1. 使用Web瀏覽器指令將頁面儲存為檔案系統上的檔案，例如「檔案>另存新檔」。

請使用下列程式匯出全部或部分英文字串。

1. 開啟平移工具。 `http://<host>:<port>/libs/cq/i18n/translator.html`
1. 使用字典下拉式選單來選取要匯出的字典。
1. 如果您要匯出字串的子集，請在字典中選取要匯出的專案。 選取「無專案」會匯出所有專案。
1. 按一下「匯出>將選取專案匯出為Xliff」（僅限字串）。
1. 在出現的對話方塊中，複製文字並將其貼到文字檔案中。

### 匯入字典 {#importing-a-dictionary}

將XLIFF檔案匯入字典以填入字典。 當字典包含英文字串的翻譯，且XLIFF檔案包含相同字串的不同翻譯時，字典翻譯會被取代。

1. 開啟翻譯工具 `http://<host>:<port>/libs/cq/i18n/translator.html`
1. 按一下「匯入> XLIFF翻譯」。
1. 選取要匯入的檔案，然後按一下「確定」。

## 管理支援的語言 {#managing-supported-lanuages}

新增或移除翻譯工具支援的語言，以及提供給網頁使用者的語言。

### 變更字典表格中列出的語言 {#changing-languages-listed-in-the-dictionary-table}

「翻譯工具」在字典表格中包含下列語言：

* de — 德文
* fr — 法文
* it — 義大利文
* es — 西班牙文
* ja — 日文
* pt-br — 巴西葡萄牙文
* zh-cn — 簡體中文
* zh-tw — 繁體中文（有限支援）
* ko-kr — 韓文

請使用下列程式來新增或移除語言。

1. 使用CRXDE Lite建立新節點：

   `/etc/languages`

1. 在此節點上，建立屬性：

   * **名称**: `languages`
   * **类型**: `Multi-String`
   * **值**：您要顯示的語言清單。 例如：

      * fr
      * es

   >[!NOTE]
   >
   >語言程式碼必須為小寫。

1. 按一下 **全部儲存** CRXDE Lite並重新載入轉換器。 格線將會更新以顯示定義的語言。

   >[!NOTE]
   >
   >翻譯人員只會儲存實際語言的翻譯 [出現在字典中](#creating-a-dictionary) (即字典路徑底下，例如 `/apps/myProject/i18n`)。
   >
   >請確定這些對應至格線中所顯示的語言。

### 讓作者可以使用語言 {#making-languages-available-to-authors}

在為AEM執行個體的新語言定義字典後，您需要讓作者可以選取此字典(例如，用於 **偏好設定**)：

1. 若要變更可用的語言清單，請 **偏好設定** 的 **安全性** 主控台：

   1. 在應用程式程式碼中建立覆蓋圖，用於：

      ```
              /libs/cq/security/widgets/source/widgets/security/Preferences.js
       and update as required.
      ```

1. 若要讓語言可用於 **偏好設定** 從 **網站** 主控台：您必須在應用程式中進行下列變更：

   1. 為下方的結構建立覆蓋：

      `/libs/cq/security/content/tools/userProperties`

   1. 在覆蓋圖內更新下方的語言清單：

      `items/common/items /lang/options`

1. 儲存所有內容，然後重新載入適當的主控台。

### 變更語言名稱和預設國家/地區 {#changing-language-names-and-default-countries}

不同的國家/地區使用相同的語言，例如美國、英國和澳洲都使用英文。 這由表示語言和國家/地區的代碼表示，例如 `en_US`， `en_GB` 和 `en_AU`.

顯示旗標時會使用預設國家/地區（例如，在語言副本對話方塊中），它們會用於解析語言代碼的國家/地區。

>[!NOTE]
>
>對於以上譯者所管理的本地化，只有確切的語言才有作用。 如果語言偏好設定下拉式清單使用 `en_uk`，必須有 `en_uk` 存放庫中的字典。

若要變更預設定義：

1. 語言清單儲存在下列位置：

   `/libs/wcm/core/resources/languages`

   複製此檔案至：

   `/apps/wcm/core/resources/languages`

   然後在那裡變更或擴充清單。 屬性 `defaultCountry` 在語言節點上(例如 `ja`)必須包含完整程式碼，例如 `ja_jp`，會定義 `jp` 作為語言的預設國家/地區 `ja`.

1. 更新 **CQ WCM語言管理員**.

   * **語言清單**：

      存放庫中語言清單的路徑。 將此專案設定為用來覆蓋的位置：

      ```
             /apps/wcm/core/resources/languages
      ```
   您可以使用OSGi Web主控台執行此操作：

   ```shell
   https://<hostname>:<port-number>/system/console/configMgr/com.day.cq.wcm.core.impl.LanguageManagerImpl
   ```

## 發佈字典 {#publishing-dictionaries}

將您的字典納入AEM應用程式的發行管理流程。 例如，將字典包含在應用程式的內容套件中，以部署至發佈執行個體。 此策略提供下列優點：

* 字典可用於其發佈環境中的元件。
* 元件UI字串的變更會與更新的翻譯一起部署。

同樣地，字典字串的測試應作為一般軟體開發生命週期的一部分來執行。

>[!NOTE]
>
>不應將一般發佈功能或復寫用於字典。 相反地，字典應被視為與程式碼和設定相同。 這包括使用原始檔控制來追蹤變更，以及使用內容套件來套用變更至作者和發佈。

>[!NOTE]
>
>使用Dispatcher時，您需要 [使快取頁面失效](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html) 在演算後的元件字串中加入新的字典字串。
