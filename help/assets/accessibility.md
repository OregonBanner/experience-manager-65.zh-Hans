---
title: 的易存取功能與介面 [!DNL Experience Manager Assets]
description: 瞭解中的協助工具功能 [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] 協助殘障使用者。
contentOwner: AG
feature: Asset Management
role: User, Architect, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
source-git-commit: 399ae241593b5cc14ef1c2efd090f0d1fae7c2df
workflow-type: tm+mt
source-wordcount: '1924'
ht-degree: 2%

---

<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, etc.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, etc.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# 中的協助工具功能 [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager] 可讓內容建立者和發佈者在網路上提供令人驚豔的體驗。 Adobe致力於透過改善的協助工具，將身心障礙的創作者也涵蓋在內 [!DNL Experience Manager]. 本軟體持續強化，以符合各類使用者的需求，並符合全球標準，包括視覺、聽覺、行動能力或其他殘疾人士。

[!DNL Experience Manager] 發佈一致性資訊，說明其遵循的標準、概述產品中的協助工具功能，以及說明相容性等級。 協助工具合規報告說明 [!DNL Experience Manager] 使用者瞭解各項標準的遵守程度。 在中完成的增強功能 [!DNL Assets] 讓所有使用者透過鍵盤、熒幕閱讀器、放大鏡和其他輔助技術輕鬆使用介面。

[!DNL Experience Manager] 針對下列標準提供不同等級的支援：

* [Web 内容无障碍准则 (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [修訂《康復法》第508條](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines).
* [協助工具計畫 — 由W3C提供的協助工具多樣化網際網路應用程式(WAI-ARIA)](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549).

若要閱讀包含規範遵循層級詳細資訊的報告，請參閱 [協助工具符合性報表](https://www.adobe.com/cn/accessibility/compliance.html) (ACR)頁面。

瞭解如何 [!DNL Dynamic Media] 可存取，請參閱 [中的協助工具 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

## 輔助技術 {#at-support}

殘障使用者經常依賴硬體與軟體來存取網頁內容及使用軟體產品。 這些工具稱為輔助技術。 [!DNL Experience Manager Assets] 使用軟體的核心功能時，可以使用下列型別的輔助技術(AT)：

* 熒幕助讀程式和熒幕放大鏡。
* 語音辨識軟體。
* 鍵盤使用方式 — 導覽和捷徑。
* 輔助硬體，包括開關控制項、可重新整理的點字顯示器，以及其他電腦輸入裝置。
* UI放大工具。

## [!DNL Experience Manager Assets] 可存取的使用案例 {#accessible-assets-use-cases}

在 [!DNL Experience Manager]，協助工具功能可滿足的兩個主要需求 [!DNL Experience Manager] 使用者及其客戶。

* 對於內容設計人員和建立者而言，有建立及發佈無障礙內容的功能，而這些內容又由其客戶和網站訪客使用。 身心障礙人士可在輔助技術的協助下使用內容。 如需詳細資訊，請參閱 [網頁協助工具准則](/help/managing/web-accessibility.md).
* [!DNL Experience Manager] 也可讓身心障礙的使用者和管理員存取使用者介面和控制，以建立和管理內容。 殘障人士可使用輔助技術導覽、使用及管理 [!DNL Assets] 功能。

中的核心功能 [!DNL Assets] 比以往更容易存取，並定期更新，以符合全球標準。 中的CRUD作業 [!DNL Assets] 內建一定程度的協助工具。 DAM工作流程（例如新增、管理、搜尋和分發資產）可透過鍵盤快速鍵、熒幕助讀程式文字、顏色對比等工具進行存取。

## 支援使用鍵盤 {#keyboard-use}

許多可使用指標點選或操作的使用者介面元素，也可以使用鍵盤來配合。 使用鍵盤，使用者就能專注於UI元素並採取適當的動作。 使用者可以直接使用鍵盤快速鍵來觸發命令或動作，而無需專注於UI元素並使用鍵盤來觸發。 例如，使用者可以使用鍵盤瀏覽至使用者介面控制項，然後選取「 」，以在使用者介面的左側開啟資產的時間軸 `Return`，並選取 `Alt + 2` 鍵盤快速鍵。

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### 中的鍵盤快速鍵 [!DNL Assets] {#keyboard-shortcuts}

中的下列動作 [!DNL Assets] 使用列出的鍵盤快速鍵。 大多數適用的鍵盤快速鍵 [!DNL Experience Manager] 主控台也適用於 [!DNL Assets]. 另請參閱 [主控台的鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). 瞭解如何 [啟用或停用鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts).

| 使用者介面或情境 | 鍵盤快速鍵 | 操作 |
|---|---|---|
| 中的欄檢視 [!DNL Assets] 使用者介面 | 向上鍵和向下鍵 | 導覽至相同階層中的檔案和資料夾。 |
| 中的欄檢視 [!DNL Assets] 使用者介面 | 向左鍵和向右鍵 | 導覽至目前資料夾上方或下方的檔案和資料夾。 |
| 瀏覽資料夾於 [!DNL Assets] | `/` | 開啟Omnisearch方塊以叫用搜尋。 |
| [!DNL Assets] 控制台 | &amp;grave； | 切换侧边栏 |
| [!DNL Assets] 控制台 | `Alt + 1` | 開啟內容樹狀結構。 |
| [!DNL Assets] 控制台 | `Alt + 2` | 開啟 [!UICONTROL 導覽] 左側欄。 |
| [!DNL Assets] 控制台 | `Alt + 3` | 顯示 [!UICONTROL 時間表] 所選資產的ID。 |
| [!DNL Assets] 控制台 | `Alt + 4` | 開啟所選資產的即時副本參考。 |
| [!DNL Assets] 控制台 | `Alt + 5` | 在選取的資料夾中開始搜尋和搜尋。 |
| 已選取資產或資料夾 | 退格符 | 刪除選取的資產或資料夾。 |
| 已選取資產或資料夾 | `p` | 開啟所選資產的「屬性」頁面。 |
| 已選取資產或資料夾 | `e` | 編輯選取的資產。 |
| 已選取資產或資料夾 | `m` | 移動選取的資產。 |
| 已選取資產或資料夾 | `Ctrl + c` | 複製選取的資產。 |
| 已選取資產或資料夾 | `Esc` | 取消選取。 |
| 對話方塊開啟，並位於焦點中 | `Esc` | 關閉對話方塊。 |
| 在DAM的資料夾內 | `Ctrl + v` | 貼上複製的資產。 |
| [!DNL Assets] 控制台 | `Ctrl + A` | 選取所有資產。 |
| 資產屬性頁面 | `Ctrl + S` | 儲存變更。 |
| [!DNL Assets] 控制台 | `?` | 請參閱鍵盤快速鍵清單。 |

## 登入並導覽 [!DNL Assets] 使用者介面 {#login}

使用者可以使用鍵盤導覽並填寫登入欄位以登入。 每次發生錯誤時，熒幕助讀程式都會通知由於登入頁面上的使用者名稱和密碼組合不正確而導致的錯誤訊息。

登入後，DAM使用者可以在以下位置導覽： [!DNL Assets] 使用鍵盤的使用者介面。 使用者介面元素（如左側邊欄、功能表、使用者設定檔、搜尋列、檔案和資料夾）以及管理和組態設定都可使用鍵盤導覽。 鍵盤導覽順序為由左至右、由上至下。 使用鍵盤導覽時，如果聚焦時有一個可操作的選項，可藉由較佳的色彩對比加以反白顯示，熒幕助讀程式則會提供旁白。 適當時，熒幕助讀程式會朗讀功能表中焦點選項的狀態（例如展開、摺疊和混合狀態）。 此外，熒幕助讀程式會朗讀可操作選項的用途，而非外觀或介面位置。

如果使用者從功能表展開說明或使用者設定檔選項，熒幕助讀程式會朗讀適當的選項或狀態。 如果使用者展開使用者設定檔選項，則可使用鍵盤選取可用選項。 例如，管理員可以模擬不同的使用者。 如果使用者從 [!UICONTROL 說明] 選項，朗讀程式會朗讀「搜尋說明」以表示搜尋正在進行中。

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## 瀏覽資產並檢視相關資訊 {#browse}

在 [!DNL Assets] 使用者介面，使用者可以使用鍵盤來瀏覽DAM存放庫中現有數位資產清單、預覽或下載資產、檢視產生的轉譯、切換檢視、檢視產生的轉譯、檢視時間軸和版本歷史記錄、檢視註釋和引用，以及檢視和管理中繼資料。

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

瀏覽資產存放庫時，以下功能可改善協助工具：

* 熒幕助讀程式會朗讀描述圖示用途或功能（而非其名稱）的替代文字。
* 使用者可以使用鍵盤按鍵存取和聚焦資產參考清單中的互動式使用者介面選項。
* 清單檢視中每列的元素會由熒幕朗讀程式宣告為同一列的元素。
* 使用導覽時 `Tab` 鍵，焦點可在版本預覽中移至關閉選項。
* 使用鍵盤瀏覽時，反白顯示的可操作使用者介面選項具有更突出的視覺焦點以及增強的對比。 這可讓使用者更容易識別重點區域。
* 使用 `Esc` 從縮圖檢視中移除快速動作圖示的鍵不會從最後一個焦點專案移除鍵盤焦點。
* 選取資產後，選取 `Alt + 4` 鍵盤快速鍵會開啟 [!UICONTROL 引用] 清單中找到。 使用 `Tab` 鍵，使用者可瀏覽非零參考專案。 僅瀏覽非零參照專案也可節省工作量和按鍵動作。
* 資產時間軸中提供了資產上的註解。 若使用鍵盤或鍵盤快速鍵存取左側邊欄，即可存取。
* [!UICONTROL 檢視設定] 在 [!DNL Experience Manager] 可使用鍵盤存取。 使用者可以使用方向鍵瀏覽可用的卡片大小，並選取和Tab鍵瀏覽瀏覽並設定現有「檢視設定」檢視中的其他元素。

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## 管理数字资源 {#manage-assets}

許多資產管理工作（例如CRUD作業、下載資產、新增中繼資料）都可不同程度的存取。 [!DNL Assets] 可讓您使用熒幕助讀程式和鍵盤等各種輔助技術完成工作。

觀看如何使用鍵盤的影片示範 [瀏覽存放庫並下載資產](https://youtu.be/K3dgqMRQJys).

對於通常由行銷人員和管理員等角色完成的中繼資料操作，以下功能可改善協助工具：

* [!UICONTROL 儲存並關閉] 資產選項 [!UICONTROL 屬性] 現在可以使用鍵盤存取頁面。
* 熒幕助讀程式會朗讀刪除所選標籤的選項 [!UICONTROL 基本] 資產索引標籤 [!UICONTROL 屬性].
* 使用者可以使用鍵盤的日期選擇器快顯對話方塊。 Datepicker使用者介面元素可用來設定開啟時間和關閉時間，以及選取日期。
* 使用鍵盤的拖曳功能在中可正確運作 [!UICONTROL 中繼資料結構編輯器] 在熒幕助讀程式的瀏覽模式中。
* 使用者可以使用鍵盤將焦點移動到下方的新增使用者或群組欄位 [!UICONTROL 已關閉的使用者群組] 在 [!UICONTROL 許可權] 資料夾索引標籤 [!UICONTROL 屬性].

## 搜尋數位資產 {#search-assets}

快速且順暢的資產搜尋體驗可加快內容速度。 內容速度使用案例是核心的一部分 [!DNL Assets] 功能。 若要從Omnisearch列開始搜尋，使用者可以使用鍵盤快速鍵 `/` 或使用 `Tab` 以及熒幕助讀程式，以快速找到搜尋選項。 當焦點在搜尋選項上時，熒幕助讀程式會將選項名稱旁白為「搜尋按鈕」 ![搜尋選項](assets/do-not-localize/search_icon.png). 使用者可以選擇 `Return` 以開啟Omnisearch方塊。 熒幕助讀程式不僅會提供在搜尋方塊中輸入之關鍵字的旁白，也會提供建議的旁白 [!DNL Experience Manager Assets]. 使用者可以使用方向鍵的組合， `Return`、和 `Tab` 以存取各種選項來觸發搜尋。

搜尋功能可透過以下功能存取：

* 頁面標題（可供熒幕助讀程式使用）有助於將頁面識別為資產的搜尋頁面。
* 使用者從Omnisearch欄位中搜尋資產。 使用者可以使用鍵盤導覽或鍵盤快速鍵來開啟它 `/`.
* 使用者可以開始輸入搜尋關鍵字，然後使用方向鍵選取自動建議。 反白顯示的建議可透過以下方式選取： `Return` 索引鍵和資產會加以搜尋，以尋找選取的建議。
* 熒幕朗讀程式可以在篩選搜尋結果時，識別並朗讀混合狀態核取方塊（除非您選取所有巢狀述詞，否則不會選取並刪除第一層核取方塊）。
* 關閉Omnisearch方塊後，使用者焦點會移至搜尋選項。

篩選搜尋結果時：

* 搜尋結果頁面具有資訊標題，可讓熒幕助讀程式使用者更容易瞭解。
* 熒幕助讀程式會朗讀搜尋篩選器中的選項作為可展開的摺疊式功能表。
* 熒幕朗讀程式會朗讀具有混合狀態選項的述詞。

## 共享资源 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

共用資產時，下列功能可改善協助工具：

* 使用者可以使用鍵盤在連結共用對話方塊中的搜尋和新增電子郵件位址列位中移動焦點。

* 在連結共用對話方塊中，以瀏覽模式導覽時，熒幕助讀程式會：

   * 載入對話方塊時不要提供表格資訊的旁白。
   * 可瀏覽至列出的所有建議。
   * 為新增電子郵件地址和搜尋欄位提供所顯示建議的旁白。

## 無障礙檔案 {#accessible-docs}

[!DNL Experience Manager] 提供無障礙說明檔案，以供身心障礙人士使用。 以下內容有助於讓內容立即可供存取，同時Adobe會繼續改善範本和內容：

* 熒幕助讀程式可以閱讀文字。
* 影像和插圖有可用的替代文字。
* 可以使用鍵盤導覽。
* 對比率有助於強調說明檔案網站的某些部分。

## 提供意見回饋 {#a11y-feedback}

若要提供與協助工具相關的意見回饋、詢問問題和請求產品增強功能，請使用下列方法：

* 填寫表單于 [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html).
* 請寄電子郵件給我們：access@adobe.com。

>[!MORELIKETHIS]
>
>* [中的協助工具功能 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).
>* [每個Service Pack版本中完成的增強功能發行說明](/help/release-notes/release-notes.md).
>* [[!DNL Adobe Experience Manager] 無障礙指引](/help/managing/web-accessibility.md).
>* [Adobe解決方案的符合性報表(ACR)和VPAT清單](https://www.adobe.com/cn/accessibility/compliance.html).

