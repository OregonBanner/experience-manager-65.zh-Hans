---
title: 將資產匯入及匯出至AEM Forms
seo-title: Importing and exporting assets to AEM Forms
description: 您可以從內匯入最適化表單和範本，也可以從內匯出至AEM執行個體。 這有助於移轉表單或跨系統移動表單。
seo-description: You can import and export adaptive forms and templates from and in to AEM instances. This helps in migrating forms or moving them across systems.
uuid: 937daedd-56f3-4e02-b695-b194b494d9bf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 69210727-dde3-495a-87b7-2e8173e6b664
docset: aem65
role: Admin
exl-id: b5f6a54e-92d1-4631-a1d1-184f37d174b6
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2516'
ht-degree: 0%

---

# 將資產匯入及匯出至AEM Forms{#importing-and-exporting-assets-to-aem-forms}

您可以在不同AEM Forms執行個體之間移動表單和相關資產、主題、資料字典、檔案片段和字母。 將系統或表單從中繼伺服器移轉至生產伺服器時，需要執行這種移動。 對於支援透過AEM Forms UI上傳和匯入的資產，建議使用Forms UI進行匯出或匯入。 不建議使用AEM Package Manager匯出或匯入這類資產。

>[!NOTE]
>
>* 在AEM 6.4 Forms中，crx-repository的結構和路徑已變更。 如果您將資產從舊版匯入至AEM 6.4 Forms，且表單對舊版結構有一些相依性，則必須手動匯出相依性。 如需存放庫結構和路徑變更的詳細資訊，請參閱 [AEM中的存放庫重組](/help/sites-deploying/repository-restructuring.md).
>


## 下載或上傳Forms &amp; Documents資產 {#download-or-upload-forms-amp-documents-assets}

AEM Forms使用者介面可讓您從AEM執行個體匯出資產，方法是將這些資產下載為AEM CRX套件或二進位檔案。 然後，您可以將下載的AEM CRX套件或二進位檔案匯入另一個AEM執行個體。

除了最適化表單範本和最適化表單內容原則外，所有資產都支援透過AEM Forms使用者介面匯出和匯入。 因此，從AEM Forms UI匯出調適型表單時，不會像其他相關的資產一樣自動匯出相關的調適型表單範本和內容原則。

對於這些資產型別，您必須使用AEM Package Manager在來源AEM伺服器上建立CRX套件，並在目的地伺服器上安裝套件。 如需建立及安裝套件的詳細資訊，請參閱 [使用封裝](/help/sites-administering/package-manager.md).

### 下載Forms &amp; Documents資產 {#download-forms-amp-documents-assets}

若要下載Forms &amp; Documents資產：

1. 登入AEM Forms執行個體。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![指南針](assets/compass.png) 圖示> Forms > Forms和檔案。
1. 選取表單資產，然後點選 **下載** 圖示。
1. 在「下載資產」中，選擇下列其中一個選項，然後點選 **下載**.

   * **下載為CRX套件：** 使用選項從AEM Forms執行個體下載及移動所有選取的資產和相關相依性至另一個執行個體。 它會將所有資產和資料夾下載為crx套件。 任何表單資產，包括在AEM （最適化表單、互動式通訊和最適化表單片段）、表單集、表單範本、PDF檔案和資源（XSD、XFS、影像）中創作的表單，都可以從AEM Forms UI以套件形式下載。
以套件形式下載資產的優點在於，它也可以下載被選取來下載的資產所使用的資產。 例如，如果您有使用表單範本、XSD和影像的最適化表單。 當您選取此最適化表單並將其下載為套件時，下載的套件也包含表單範本、XSD和影像。 也會下載與資產相關聯的所有中繼資料屬性（包括自訂屬性）。

   * **將資產下載為二進位檔案：** 使用選項僅下載表單範本(XDP)、PDF forms(PDF)、檔案(PDF)和資源（影像、結構描述、樣式表）。 您可以使用外部應用程式編輯這些資產。 它會將具有二進位檔(例如XSD、XDP、影像、PDF和XDP)的表單資產下載為.zip檔案。
您無法下載最適化表單、互動式通訊、最適化表單片段、主題和表單集， **將資產下載為二進位檔案** 選項。 若要下載這些資產，您應使用 **下載為CRX套件** 選項。

   選取的資產會下載為封存（.zip檔案）。

   >[!NOTE]
   >
   >AEM套件和二進位檔案都會下載為封存（.zip檔案）。 資產的範本不會隨資產一起下載。 您需要個別匯出資產範本。

### 上傳Forms和檔案資產 {#upload-forms-amp-documents-assets}

若要上傳Forms &amp; Documents資產：

>[!VIDEO](https://vimeo.com/)

1. 登入AEM Forms執行個體。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![指南針](assets/compass.png) 圖示> Forms> Forms與檔案。
1. 點選 **建立** >**檔案上傳**. 上傳表單或封裝對話方塊隨即顯示。
1. 在對話方塊中，瀏覽並選取要匯入的封裝或封存。 您也可以選取PDF檔案、XSD、影像、樣式表和XDP表單。 點選 **開啟**. 您選取的資料夾或檔案名稱不得包含任何特殊字元。

   在對話方塊中，確認上傳資產的詳細資訊，然後點選 **上傳**.

   如果您上傳現有表單資產，資產會隨之更新。

   >[!NOTE]
   >
   >上傳套件不會取代現有的資料夾階層。 例如，如果您在單一伺服器上的/content/dam/formsanddocuments位置有一個名為「Training」的最適化表單。 您下載最適化表單並將表單上傳到其他伺服器。 第二部伺服器也有一個名為&#39;Training&#39;的資料夾，位於相同位置/content/dam/formsanddocuments。 上傳失敗。

## 下載或上傳主題 {#downloading-or-uploading-a-theme}

透過AEM Forms，您可以建立、下載或上傳主題。 主題會像其他資產（如表單、檔案和信件）一樣建立。 您可以建立佈景主題、下載佈景主題，然後將其上傳到個別的執行個體來重複使用。 如需主題的詳細資訊，請參閱 [AEM Forms中的主題](../../forms/using/themes.md).

### 下載主題 {#downloading-a-theme}

您可以匯出AEM Forms中的主題，並用於其他專案或執行個體。 AEM可讓您將主題下載為zip檔案，以便在執行個體上上傳。

若要下載佈景主題：

1. 登入AEM Forms執行個體。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![指南針](assets/compass.png) 圖示> Forms>主題。
1. 選取主題並點選 **下載**. 主題會下載為封存（.zip檔案）。

### 上傳主題 {#uploading-a-theme}

您可以在專案上將已建立的主題與樣式預設集搭配使用。 您可以將其他人建立的主題套件上傳到您的專案中，藉此匯入這些套件。

上傳佈景主題：

1. 在Experience Manager中，導覽至 **Forms >主題**.
1. 在「佈景主題」頁面中，按一下 **建立>檔案上傳**.
1. 在「檔案上傳」提示中，瀏覽並選取電腦上的主題套件，然後按一下 **上傳**.
上傳的主題可在主題頁面中取得。

1. 登入AEM Forms執行個體。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![指南針](assets/compass.png) 圖示> Forms>主題。
1. 按一下 **建立** > **檔案上傳**. 在「檔案上傳」提示中，瀏覽並選取電腦上的主題套件，然後按一下 **上傳**. 主題已上傳。

## 在Correspondence Management中匯入和匯出資產 {#import-and-export-assets-in-correspondence-management}

若要在兩個不同的「通訊管理」實作之間共用資產（例如資料字典、信件和檔案片段），您可以建立和共用.cmp檔案。 .cmp檔案可包含一或多個資料字典、字母、檔案片段和表單。

### 匯出檔案片段、字母和/或資料字典 {#export-document-fragments-letters-and-or-data-dictionaries}

1. 在信件、檔案片段或資料字典頁面中，點選並選取您要匯出至單一封裝的資產，然後點選「佇列以下載」。 資產會排成一行以供匯出。
1. 如有需要，請重複上述步驟以新增字母、檔案片段和資料字典。
1. 點選 **下載**.
1. 通訊管理會顯示「下載資產」對話方塊，其中包含匯出清單中的資產清單。

   ![匯出](assets/export.png)

1. 若要檢視匯出的相依性，請點選「解決」。 或跳至下一個步驟。 即使您未點選「解決」，相依性仍會匯出。
1. 若要下載.cmp檔案，請點選 **確定**.
1. Correspondence Management會下載.cmp檔案至您的電腦。

   .cmp檔案包含匯出的資產。 您可以與其他人共用.cmp檔案。 其他使用者可以在不同的伺服器匯入.cmp檔案，以取得新伺服器中的所有資產。

### 將所有對應管理資產匯出為套件 {#export-all-the-correspondence-management-assets-as-a-package}

使用此選項可從AEM Forms執行個體以套件形式下載所有Correspondence Management資產和相關相依性。

例如，如果「通訊管理」有使用影像和文字的信件，則下載的套件也包含與信件相關的影像和文字。 也會下載與資產相關聯的所有中繼資料屬性（包括自訂屬性）。 下載套件(.cmp)後，您可以 [將套件匯入至不同的AEM Forms執行個體](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p).

若要以套件形式下載所有Correspondence Management資產和相關相依性，請完成以下步驟：

1. 以表單使用者身分登入AEM Forms伺服器。
1. 點選 **Adobe Experience Manager** 全域導覽列中的。
1. 點選工具( ![工具](assets/tools.png))，然後點選 **Forms**.
1. 點選 **匯出對應管理資產**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   (「匯出所有通訊管理資產」頁面會出現，並顯示上次嘗試匯出程式的相關資訊，以及下載上次成功匯出的封裝的連結。

   ![export-last-run-details](assets/export-last-run-details.png)

1. 點選 **匯出** 然後，在確認訊息中，點選 **確定**.

   批次程式完成後，上次執行的詳細資訊和下載套件的連結會更新。 這包括管理員登入和批次是否成功執行的資訊。 資產會匯出至套件，且會出現「下載匯出的套件」連結。

   >[!NOTE]
   >
   >「匯出所有資產」程式一經啟動便無法取消。 此外，當匯出所有操作仍在進行時，請勿建立、刪除、修改或發佈任何資產，或啟動「發佈所有資產」程式。a

1. 點選 **下載匯出的封裝** 下載套件檔案的連結。

   若要將套件中的資產新增至通訊管理的另一個執行個體， [將套件匯入至AEM Forms執行個體](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p).

### 將檔案片段、信函和/或資料字典匯入通訊管理 {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

您可以匯入已匯出至.cmp檔案的資產。 .cmp檔案可以有一或多個字母、資料字典、檔案片段和相依資產。

>[!NOTE]
>
>匯入舊的Correspondence Management資產進行移轉時，請使用管理員帳戶登入。 如需移轉舊通訊管理資產的詳細資訊，請參閱 [將通訊管理資產移轉至AEM 6.1表單](/help/forms/using/migration-utility.md).

1. 在資料字典、字母或檔案片段頁面上，點選 **建立>檔案上傳** 並選取.cmp檔案。
1. 「通訊管理」會顯示「匯入資產」對話方塊，其中包含已匯入的資產清單。 點選 **匯入**.

   匯入資產後，資產的下列屬性會更新，而其他屬性會維持不變：

   * 作者：顯示將資產匯入伺服器的使用者ID
   * 已修改：將資產匯入至伺服器的時間

   >[!NOTE]
   >
   >若要讓您能夠上傳XDP （作為cmp檔案的一部分或以其他方式上傳），您需要成為forms-power-users群組的一部分。 如需存取許可權，請聯絡管理員。

## 匯出工作流程應用程式 {#export-a-workflow-application}

您可以使用AEM封裝管理程式來匯出工作流程應用程式。 程式如下：

1. 開啟AEM Forms封裝管理員。 封裝管理程式的URL為https://&lt;server>：&lt;port>/crx/packmgr.
1. 按一下 **[!UICONTROL 建立封裝]**. 此 **[!UICONTROL 新封裝]** 對話方塊隨即顯示。
1. 指定套件的名稱、版本和群組。 单击&#x200B;**[!UICONTROL 确定]**。
1. 按一下 **[!UICONTROL 編輯]** 並開啟 **[!UICONTROL 篩選器]** 標籤。 按一下 **[!UICONTROL 新增篩選器]**. 指定工作流程應用程式的路徑。 例如，/etc/fd/dashboard/startpoints/homemortgage。 按一下 **[!UICONTROL 新增規則]**.

1. 打开&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。選取 **[!UICONTROL 合併]** 或 **[!UICONTROL 覆寫]** 在ACL處理欄位中。 单击“**[!UICONTROL 保存]**”。
1. 按一下 **[!UICONTROL 建置]** 以建立封裝。

   建置套件後，您可以下載套件並將其匯入至其他伺服器。 工作流程應用程式會出現在上傳套件的伺服器上。

   >[!NOTE]
   >
   >為使工作流程應用程式正常運作，請一併匯出對應的最適化表單和工作流程模型。

## 資料夾和組織資產 {#folders-and-organizing-assets}

AEM Forms使用者介面會使用資料夾來排列資產。 這些資料夾用於排列AEM Forms使用者介面中建立的資產。 您可以重新命名、建立子資料夾，以及將資產和檔案儲存在這些資料夾中。 在資料夾中組織檔案和資產可讓您將檔案群組在一起，以便輕鬆管理。 您可以選取資料夾並選擇下載或刪除。

若要建立資料夾，請完成下列步驟：

### 建立資料夾 {#create-a-folder}

1. 登入AEM Forms使用者介面，網址為 `https://<server>:<port>/aem/forms.html`.
1. 導覽至您要建立資料夾的位置。
1. 點選「建立>資料夾」。
1. 輸入下列詳細資料：

   * **標題：** 資料夾的顯示名稱
   * **名稱：** *（必要）* 要在存放庫中儲存資料夾的節點名稱

   >[!NOTE]
   >
   >依預設，名稱欄位的值會自動從標題中填入。 名稱只能包含英數字元，或連字型大小(-)和底線(_)特殊字元。 在標題中輸入的任何其他特殊字元都會自動取代為連字型大小，並提示您確認新名稱。 您可以選擇繼續使用建議的名稱或進一步編輯。

1. 具有您定義標題的新資料夾會顯示在資產清單中的目前位置。

   如果存在具有指定名稱的資料夾，提交會失敗並出現錯誤。 您可以將滑鼠懸停在錯誤上，檢視錯誤訊息 ![aem6forms_error_alert](assets/aem6forms_error_alert.png) 圖示顯示在名稱欄位旁。

   您可以點選新建立的資料夾以進入資料夾並在資料夾中建立資產或資料夾。 此外，您可以選取資料夾，並選擇將資料夾排入下載佇列、刪除資料夾或編輯資料夾名稱。

   ![editdeletedownloadafolder](assets/editdeletedownloadafolder.png)

### 建立一個或多個資產或信函的復本 {#create-copies-of-one-or-more-assets-or-letters}

您可以使用現有的資產和字母，快速建立具有類似屬性、內容和繼承資產的資產和字母。 您可以複製並貼上資料字典、檔案片段和字母。

完成下列步驟以建立資產和信函的復本：

1. 在相關的「資產」或「信件」頁面中，選取一或多個資產/信件。 UI會顯示「複製」圖示。
1. 点按复制。UI會顯示「貼上」圖示。 您也可以選擇在貼上之前，先在資料夾中前往/導覽。 不同的資料夾可以包含名稱相同的資產。 如需檔案夾的詳細資訊，請參閱 [資料夾和組織資產](#folders-and-organizing-assets).
1. 點選「貼上」。 「貼上」對話方塊隨即顯示。 系統會自動產生資產/字母新副本的名稱和標題，但您可以編輯資產/字母的標題和名稱。

   如果您要在相同位置複製和貼上資產/信件，則會將尾碼「 — CopyXX」新增至資產/信件的現有名稱。 如果複製的資產/信函沒有標題，則自動產生的標題欄位會保持空白。

1. 如有需要，請編輯您要用來儲存資產/信函副本的標題和名稱。
1. 點選「貼上」。 已複製資產的新副本隨即建立。

## 搜索 {#search-forms}

AEM Forms UI可讓您搜尋內容。 使用頂端列，您可以點選「搜尋」 **[A]** 以搜尋內容中的資產和檔案等資源。

搜尋資產時，AEM Forms會顯示側面板。 您也可以點選 ![assets-browser-content-only](assets/assets-browser-content-only.png) >篩選 **[B]** 以叫用側面板。 使用側面板中的各種篩選器，您可以縮小搜尋範圍。 側面板也可讓您儲存搜尋。

![search_topbar](assets/search_topbar.png)

**答：** 搜尋 **B.** 篩選

![側面板 — 篩選器](assets/search_sidepanel.png)

側面板 — 篩選器

在側面板上，您可以使用以下來縮小搜尋結果的範圍：

* 搜尋目錄
* 标记
* 搜尋條件；例如，修改日期、發佈狀態、即時副本狀態。

側面板也可讓您以所選名稱儲存搜尋設定。

如需有關使用搜尋、篩選器、儲存的搜尋和側面板的詳細資訊和指示，請參閱 [搜尋](/help/sites-authoring/search.md).
