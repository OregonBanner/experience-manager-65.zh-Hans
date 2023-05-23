---
title: 使用CRXDE Lite開發
seo-title: Developing with CRXDE Lite
description: CRXDE Lite內嵌於AEM中，可讓您在瀏覽器中執行標準開發工作
seo-description: CRXDE Lite is embedded into AEM and enables you to perform standard development tasks in the browser
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
exl-id: 9e88ca55-ac3d-4857-b6b2-aeb732562664
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 2%

---

# 使用CRXDE Lite開發{#developing-with-crxde-lite}

本節說明如何使用CRXDE Lite開發您的AEM應用程式。

請參閱概述檔案，深入瞭解可用的不同開發環境。

CRXDE Lite內嵌於AEM中，可讓您在瀏覽器中執行標準開發工作。 使用CRXDE Lite，您可以在記錄時建立專案、建立和編輯檔案(如.jsp和.java)、資料夾、範本、元件、對話方塊、節點、屬性和組合。
當您無法直接存取AEM伺服器、透過擴充或修改現成元件和Java套件組合來開發應用程式，或當您不需要專用的除錯程式、程式碼完成和語法醒目提示時，建議使用CRXDE Lite。

>[!NOTE]
>
>從AEM 6.5.5.0開始，已無法再匿名存取CRXDE Lite。
>系統會將使用者重新導向至登入畫面。


>[!NOTE]
>
>建議使用 [Eclipse適用的AEM開發人員工具](/help/sites-developing/aem-eclipse.md) 和 [AEM HTL Brackets擴充功能](/help/sites-developing/aem-brackets.md) 專案開發期間。

## CRXDE Lite快速入門 {#getting-started-with-crxde-lite}

若要開始使用CRXDE Lite，請依照下列步驟進行：

1. 安裝AEM。
1. 在您的瀏覽器中，輸入 `https://<host>:<port>/crx/de`. 默认情况下，这是 `https://localhost:4502/crx/de`。
1. 輸入您的 **使用者名稱** 和 **密碼**. 預設為 `admin` 和 `admin`.

1. 单击&#x200B;**确定**。

CRXDE Lite使用者介面在瀏覽器中看起來如下所示：

![chlimage_1-18](assets/crx-interface.jpg)

您現在可以使用CRXDE Lite來開發您的應用程式。

## 使用者介面概觀 {#overview-of-the-user-interface}

CRXDE Lite提供下列功能：

<table>
 <tbody>
  <tr>
   <td>頂端切換列</td>
   <td>可讓您在CRXDE Lite、封裝管理器和封裝共用之間快速切換。</td>
  </tr>
  <tr>
   <td>節點路徑Widget</td>
   <td><p>顯示目前所選節點的路徑。</p> <p>您也可以使用它來跳至節點，方法是手動輸入路徑，或從其他位置貼上路徑，然後按下Enter。</p> <p>此外，也支援尋找具有特定節點名稱的節點。 輸入您要尋找的節點名稱，然後等待（或按一下右側的搜尋符號）。 您可以嘗試輸入（例如）字串 <em>oak</em> 放入Widget中，檢視其運作方式。 如果指定的節點載入到總管窗格中，清單將會顯示，您可以選取路徑並按一下Enter以導覽至該路徑。 請注意，它僅適用於瀏覽器中目前載入CRXDE使用者端應用程式的節點。 如果您想要搜尋整個存放庫，請使用工具，然後使用查詢。</p> </td>
  </tr>
  <tr>
   <td>總管窗格</td>
   <td><p>顯示存放庫中所有節點的樹狀結構。</p> <p>按一下節點，即可在以下位置顯示其屬性： <strong>屬性</strong> 標籤。 按一下節點後，您可以在工具列中選取動作。 再按一下節點以重新命名。</p> <p>樹狀結構導覽篩選（雙目圖示）：可讓您篩選儲存庫名稱中包含輸入文字的節點。 它僅適用於本機載入的節點。<br /> </p> </td>
  </tr>
  <tr>
   <td>編輯窗格</td>
   <td><p><strong>首頁</strong> 索引標籤：可讓您搜尋內容和/或檔案，並存取開發人員資源（檔案、開發人員部落格、知識庫）和支援(Adobe首頁和支援中心)。<br /> </p> <p>連按兩下 <strong>總管</strong> 窗格以顯示其內容，例如.jsp或.java檔案。 然後您可以修改並儲存變更。</p> <p>在中編輯檔案後 <strong>編輯</strong> 窗格內，工具列上提供下列工具：<br /> </p> - <strong>在樹狀結構中顯示： </strong>會在存放庫樹狀結構中顯示檔案。<br /> - <strong>搜尋/取代……</strong>：搜尋或取代。<br /> <br /> 連按兩下 <strong>編輯</strong> 窗格開啟 <strong>移至行</strong> 對話方塊，讓您輸入特定行號前往。<br /> </td>
  </tr>
  <tr>
   <td>“属性”选项卡<br /> </td>
   <td>顯示您已選取之節點的特性。 您可以新增屬性或刪除現有屬性。<br /> </td>
  </tr>
  <tr>
   <td>存取控制標籤</td>
   <td><p>根據目前路徑、存放庫層級或主體顯示許可權。</p> <p>這些許可權可劃分為</p> <p>- <strong>適用的存取控制原則</strong>：可套用至目前選取範圍的原則。</p> <p>- <strong>本機存取控制原則</strong>：目前的原則已套用至本機目前的選取範圍。</p> <p>- <strong>有效的存取控制原則</strong>：套用至目前選取範圍的目前原則，可能在本機設定或從父節點繼承。</p> <p>注意. 若要能夠檢視存取控制資訊，登入CRXDE Lite的使用者必須擁有讀取ACL專案的許可權。 匿名使用者預設無法看到此資訊 — 請以管理員身分登入以檢視資訊。</p> </td>
  </tr>
  <tr>
   <td>「復寫」標籤</td>
   <td><p>顯示目前節點的復寫狀態。 您可以復寫和復寫刪除目前節點。</p> </td>
  </tr>
  <tr>
   <td>主控台索引標籤<br /> </td>
   <td><p><strong>服务器日志</strong>:</p> <p>顯示記錄訊息。 您可以設定記錄層級、清除主控台、釘選選取的捲動位置，以及啟用/停用訊息顯示。<br /> </p> <p><strong>版本控制</strong>:</p> <p>顯示版本控制訊息。<br /> </p> </td>
  </tr>
  <tr>
   <td>建置資訊索引標籤<br /> </td>
   <td>在建置組合時顯示資訊。<br /> </td>
  </tr>
  <tr>
   <td>刷新<br /> </td>
   <td>重新整理目前的選取範圍。 來自其他使用者的變更會在您的存放庫檢視中更新。 您所做的變更不受影響。<br /> </td>
  </tr>
  <tr>
   <td>全部保存</td>
   <td><p><strong>全部保存</strong>:<br /> </p> <p>儲存您所做的所有變更。 在您按一下「儲存」之前，變更是暫時性的，當您退出主控台時，將會遺失。</p> <p><strong>还原</strong>:</p> <p>捨棄您自上次儲存動作後在所選節點上所做的所有變更，然後重新載入所選節點的存放庫目前狀態。</p> <p><strong>全部恢复</strong>:</p> <p>捨棄您自上次儲存動作以來在整個存放庫中所做的所有變更，然後重新載入存放庫的目前狀態。</p> </td>
  </tr>
  <tr>
   <td>创建 ...<br /> </td>
   <td><p>下拉式功能表，在選取的節點下建立下列專案：<br /> </p> <p>- <strong>節點</strong>：具有任意節點型別的節點<br /> </p> <p>- <strong>檔案</strong>： nt：file節點及其nt：resource子節點</p> <p>- <strong>資料夾</strong>： nt：folder節點</p> <p>- <strong>範本</strong>： AEM範本</p> <p>- <strong>元件</strong>： AEM元件</p> <p>- <strong>對話方塊</strong>： AEM對話方塊</p> </td>
  </tr>
  <tr>
   <td>删除<br /> </td>
   <td>刪除選取的節點。<br /> </td>
  </tr>
  <tr>
   <td>复制</td>
   <td>複製選取的節點。<br /> </td>
  </tr>
  <tr>
   <td>粘贴<br /> </td>
   <td>將複製的節點貼在所選節點下。<br /> </td>
  </tr>
  <tr>
   <td>移动 ...<br /> </td>
   <td>將選取的節點移至透過對話方塊設定的節點。</td>
  </tr>
  <tr>
   <td>重命名 ...<br /> </td>
   <td>重新命名選取的節點。<br /> </td>
  </tr>
  <tr>
   <td>Mixin...<br /> </td>
   <td>可讓您將mixin型別新增至節點型別。 mixin型別主要用於新增進階功能，例如版本設定、存取控制、參照和鎖定節點。</td>
  </tr>
  <tr>
   <td>工具<br /> </td>
   <td><p>包含下列工具的下拉式功能表：</p> <p>- <strong>伺服器設定……</strong>：存取Felix主控台。</p> <p>- <strong>查詢……</strong>：查詢存放庫。</p> <p>- <strong>許可權……</strong>：開啟許可權管理，您可以在其中檢視及新增許可權。</p> <p>- <strong>測試存取控制……</strong>：您可以在此處測試特定路徑和/或主體的許可權。</p> <p>- <strong>匯出節點型別</strong>：將系統中的節點型別匯出為cnd標籤法。</p> <p>- <strong>匯入節點型別……</strong>：使用cnd標籤法匯入節點型別。</p> <p>- <strong>安裝SiteCatalyst偵錯工具……</strong>：如何安裝Analytics Debugger的說明。</p> </td>
  </tr>
  <tr>
   <td>登入Widget<br /> </td>
   <td><p>顯示目前登入的使用者及其登入的工作區，例如admin@crx.default。</p> <p>按一下以登入或以特定使用者身分重新登入。 如果您未指定要登入的工作區，則會登入預設的工作區crx.default。</p> <p>如果您想以匿名使用者的身份瀏覽存放庫，請使用 <strong>匿名</strong> 作為登入名稱，以及任何密碼（例如空格或點）。<br /> </p> <p>如果您的授權不再有效（例如，已過期），登入Widget會顯示"<strong>未獲授權 — 登入……</strong>「。 按一下以重新登入。</p> </td>
  </tr>
 </tbody>
</table>

## 创建文件夹 {#creating-a-folder}

若要建立具有CRXDE Lite的資料夾：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在「導覽」窗格中，以滑鼠右鍵按一下要在其下建立新資料夾的資料夾，然後選取 **建立……**，則 **建立資料夾……**.

1. 輸入資料夾 **名稱** 並按一下 **確定**.

1. 按一下 **全部儲存** 以將變更儲存在伺服器上。

## 建立範本 {#creating-a-template}

若要使用CRXDE Lite建立範本：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在導覽窗格中，以滑鼠右鍵按一下要建立範本的資料夾，然後選取 **建立……**，則 **建立範本……**.

1. 輸入 **標籤**， **標題**， **說明**， **資源型別** 和 **排名** 範本的。 单击&#x200B;**下一步**。

1. 此步驟為選用：設定 **允許的路徑**. 按一下 **下一個**

1. 此步驟為選用：設定 **允許的父項**. 单击&#x200B;**下一步**。

1. 此步驟為選用：設定 **允許的子項**. 单击&#x200B;**确定**。

1. 按一下 **全部儲存** 以將變更儲存在伺服器上。

它會建立：

* 型別節點 `cq:Template` 具有範本屬性

* 型別的子節點 `cq:PageContent` 具有頁面內容屬性

您可以將屬性新增至範本：請參閱 [建立屬性](#creating-a-property) 區段。

## 建立元件 {#creating-a-component}

此處說明的功能僅在安裝了CQ5 （即節點型別）時可用 `cq:Component` 在存放庫中提供。

若要以CRXDE Lite建立元件：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在導覽窗格中，以滑鼠右鍵按一下要建立元件的資料夾，然後選取 **建立……**，則 **建立元件……**.

1. 輸入 **標籤**， **標題**， **說明**， **超級資源型別** 和 **群組** 元件的。 单击&#x200B;**下一步**。

1. 此步驟為選用：設定元件屬性 **為容器，** **無裝飾**， **儲存格名稱** 和 **對話方塊路徑**. 单击&#x200B;**下一步**。

1. 此步驟為選用：設定元件屬性 **允許的父項**. 单击&#x200B;**下一步**。

1. 此步驟為選用：設定元件屬性 **允許的子項**. 单击&#x200B;**确定**。

1. 按一下 **全部儲存** 以將變更儲存在伺服器上。

它會建立：

* 型別節點 `cq:Component`
* 元件屬性
* 元件.jsp指令碼

## 建立對話方塊 {#creating-a-dialog}

若要使用CRXDE Lite建立對話方塊：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在「導覽」窗格中，以滑鼠右鍵按一下要建立對話方塊的元件，然後選取 **建立……**，則 **建立對話方塊……**.

1. 輸入 **標籤** 和 **標題**. 单击&#x200B;**确定**。

1. 按一下 **全部儲存** l儲存伺服器上的變更。

它會建立具有下列結構的對話方塊：

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

您現在可以修改屬性或建立新節點，讓對話方塊符合您的需求。

您也可以使用對話方塊編輯器來編輯對話方塊。 連按兩下CRXDE Lite中的對話方塊節點將會開啟編輯器。 有關「對話方塊編輯器」的更多資訊可以找到 [此處](/help/sites-developing/dialog-editor.md).

## 建立節點 {#creating-a-node}

若要使用CRXDE Lite建立節點：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在導覽窗格中，以滑鼠右鍵按一下要建立新節點的節點，然後選取 **建立……**，則 **建立節點……**.
1. 輸入 **名稱** 和 **型別**. 单击&#x200B;**确定**。
1. 按一下 **全部儲存** 以將變更儲存在伺服器上。

您現在可以修改屬性或建立新節點，以調整節點以符合您的需求。

>[!NOTE]
>
>大部分的編輯操作（包括「建立節點」）都會保留記憶體中的所有變更，並且只會在儲存時將它們儲存在存放庫中（透過「儲存全部」按鈕）。 不過，某些作業（例如移動）會自動持續存在。
>
>有關父節點的節點型別是否允許新建立的節點的驗證，也會在儲存變更時先由JCR存放庫執行。 如果您在儲存節點時收到錯誤訊息，請檢查內容結構是否有效(例如，您無法建立 `nt:unstructured` 作為子項的節點 `nt:folder` 節點)。

## 建立屬性 {#creating-a-property}

若要使用CRXDE Lite建立屬性：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在「導覽」窗格中，選取您要新增屬性的節點。
1. 在 **屬性** 標籤下，輸入 **名稱**，則 **型別** 和 **值**. 按一下 **新增**.

1. 按一下 **全部儲存** 以將變更儲存在伺服器上。

## 建立指令碼 {#creating-a-script}

若要建立新指令碼：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在導覽窗格中，以滑鼠右鍵按一下要建立指令碼的元件，然後選取 **建立……**，則 **建立檔案……**.

1. 輸入檔案 **名稱** 包括其擴充功能。 单击&#x200B;**确定**。

1. 新檔案會在「編輯」窗格中開啟作為索引標籤。
1. 編輯檔案。
1. 按一下 **全部儲存** 以儲存變更。

## 匯出和匯入節點型別 {#exporting-and-importing-node-types}

使用CRXDE Lite，您可以匯入和/或匯出節點型別定義於 [CND （壓縮名稱空間和節點型別定義）標籤法](https://jackrabbit.apache.org/jcr/node-type-notation.html).

若要匯出節點型別定義，請執行下列動作：

1. 在瀏覽器中開啟CRXDE Lite。
1. 選取您需要的節點。
1. 選取 **工具** 則 **匯出節點型別**.

1. 定義會以筆記號顯示，並會顯示在您的瀏覽器中。 視需要儲存資訊。

若要匯入節點型別定義，請執行下列動作：

1. 在瀏覽器中開啟CRXDE Lite。
1. 選取 **工具** 則 **匯入節點型別……**.

1. 在文字方塊中輸入定義的CND記號。
1. Check **允許更新** 如果您要更新現有的定義。
1. 按一下 **匯入**.

## 日志记录 {#logging}

您可以使用CRXDE Lite顯示檔案 `error.log` 檔案系統上的 `<crx-install-dir>/crx-quickstart/server/logs` 並使用適當的記錄層級加以篩選。 請依照下列步驟進行：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在 **主控台** 定位字元，在視窗底部的下拉式功能表中，選取 **伺服器記錄檔**.

1. 按一下 **停止** 圖示來顯示訊息。

您可以：

* 在Felix主控台中調整記錄引數，方法是按一下 **記錄設定** 圖示。
* 按一下 **筆刷** 圖示。
* 按一下「 」，將訊息釘選到目前的選取範圍 **釘選** 圖示。
* 按一下「 」，啟用或停用訊息顯示 **停止** 圖示。

## 访问控制 {#access-control}

>[!NOTE]
>
>另請參閱 [使用者、群組和存取許可權管理](/help/sites-administering/user-group-ac-admin.md) 以取得詳細資訊。
