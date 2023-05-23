---
title: 正在設定watched資料夾端點
seo-title: Configuring watched folder endpoints
description: 瞭解如何設定watched資料夾端點。
seo-description: Learn how to configure watched folder endpoints.
uuid: 01fb5ff8-2071-44bd-9241-7d5d41a5b26e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 761e7909-43ba-4642-bcfc-8d76f139b9a3
exl-id: ec169a01-a113-47eb-8803-bd783ea2c943
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '7163'
ht-degree: 0%

---

# 正在設定watched資料夾端點 {#configuring-watched-folder-endpoints}

管理員可以設定網路資料夾，稱為 *觀察資料夾*，因此當使用者將檔案(例如PDF檔案)放入watched資料夾時，將會叫用已設定的服務操作並操作該檔案。 服務執行指定的操作後，會將修改的檔案儲存在指定的輸出資料夾中。

## 設定Watched資料夾服務 {#configuring-the-watched-folder-service}

設定Watched資料夾端點之前，請先設定Watched資料夾服務。 Watched資料夾服務的設定引數有兩個用途：

* 設定所有watched資料夾端點的共同屬性
* 為所有watched資料夾端點提供預設值

在設定Watched資料夾服務後，您為目標服務新增Watched資料夾端點。 新增端點時，您可以設定值，例如將檔案或資料夾放在已設定之Watched Folder服務的輸入資料夾中時，要叫用的服務名稱和操作名稱。 如需設定Watched資料夾服務的詳細資訊，請參閱 [Watched資料夾服務設定](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).

## 建立watched資料夾 {#creating-a-watched-folder}

您可以透過下列兩種方式建立watched資料夾：

* 設定watched資料夾端點的設定時，請在「路徑」方塊中輸入父目錄的完整路徑，並附加要建立的watched資料夾名稱，如下列範例所示：
   `  C:\MyPDFs\MyWatchedFolder`由於MyWatchedFolder資料夾尚不存在，AEM表單會嘗試在該位置建立它。

* 在設定watched資料夾端點之前，在檔案系統上建立資料夾，然後在[路徑]方塊中輸入完整路徑。

在叢集環境中，將用作watched資料夾的資料夾必須在檔案系統或網路上可存取、可寫入和共用。 在此案例中，叢集的每個應用程式伺服器執行個體都必須具備相同共用資料夾的存取權。

在Windows中，如果應用程式伺服器是以服務的形式執行，則必須透過下列其中一種方式，以適當的共用資料夾存取權來啟動應用程式伺服器：

* 設定應用程式伺服器服務登入身份 **引數** 以具有共用監看資料夾適當存取權的特定使用者身份開始。
* 將應用程式伺服器服務啟動為本機系統選項設定為允許服務與案頭互動。 此選項要求所有人都能存取及寫入共用的watched資料夾。

## 將監看資料夾鏈結在一起 {#chaining-together-watched-folders}

Watched資料夾可以鏈結在一起，因此一個watched資料夾的結果檔案是下一個watched資料夾的輸入檔案。 每個watched資料夾都可以叫用不同的服務。 透過以這種方式設定watched資料夾，可以叫用多項服務。 例如，一個watched資料夾可以將PDF檔案轉換為Adobe PostScript®而另一個watched資料夾可以將PostScript檔案轉換為PDF/A格式。 若要這麼做，只需將 *結果* 您第一個端點所定義的watched資料夾的資料夾，指向以下專案： *輸入* 您第二個端點所定義的watched資料夾資料夾。

第一次轉換的輸出會變成\path\result。 第二個轉換的輸入為\path\result，而第二個轉換的輸出會移至\path\result\result （或您在第二個轉換的「結果資料夾」方塊中定義的目錄）。

## 使用者如何與watched資料夾互動 {#how-users-interact-with-watched-folders}

對於Watched資料夾端點，使用者可以從案頭複製或拖曳輸入檔案或資料夾到Watched資料夾，以叫用。 系統會依檔案到達的順序來處理這些檔案。

對於watched資料夾端點，如果作業只需要一個輸入檔案，使用者可以將該檔案複製到watched資料夾的根目錄。

如果作業包含多個輸入檔案，使用者必須在包含所有必要檔案的watched資料夾階層之外建立資料夾。 這個新資料夾應該包含輸入檔案(以及選擇性包含的DDX檔案（如果處理序需要）)。 在建構工作資料夾後，使用者將其複製到watched資料夾的輸入資料夾中。

>[!NOTE]
>
>確定應用程式伺服器已刪除Watched資料夾中檔案的存取權。 如果AEM Forms在掃描檔案後無法從輸入資料夾中刪除這些檔案，則會無限期叫用關聯的程式。

## 監看資料夾輸出 {#watched-folder-output}

當輸入為資料夾且輸出包含多個檔案時，AEM forms會建立與輸入資料夾同名的輸出資料夾，並將輸出檔案複製到該資料夾中。 當輸出包含包含索引鍵/值組的檔案結構圖（例如輸出程式的輸出）時，將使用索引鍵作為輸出檔案名稱。

端點程式產生的輸出檔案名稱不能包含字母、數字和句點(.)以外的字元 在副檔名之前。 AEM表單會將其他字元轉換為其十六進位值。

使用者端應用程式會從watched資料夾結果資料夾中擷取結果檔案。 處理程式錯誤記錄在watched資料夾失敗資料夾中。

## Watched資料夾如何運作 {#how-watched-folder-works}

Watched資料夾模組包含下列服務：

* Watched資料夾服務
* provider.file_scan_service
* provider.file_write_results_service

除了上述服務之外，Watched Folder還取決於其他服務，包括用於排程工作的排程器服務，以及支援非同步呼叫目標服務的工作管理員服務。

### Watched資料夾如何處理呼叫要求 {#how-watched-folder-processes-an-invocation-request}

Watched資料夾服務會處理端點的建立、更新及刪除。 管理員建立端點後，會根據指定的重複間隔或cron運算式，將端點排定由排程器服務觸發。

此圖表說明Watched資料夾如何處理呼叫請求。

![en_watchedfolder](assets/en_watchedfolder.png)

使用watched資料夾叫用服務的程式如下：

1. 使用者端應用程式會將檔案或資料夾置於watched資料夾輸入資料夾中。
1. 當作業掃描間隔發生時，排程器服務會呼叫provider.file_scan_service來處理輸入資料夾中的檔案或資料夾。
1. provider.file_scan_service會執行下列工作：


   * 掃描輸入資料夾中符合包含檔案模式的檔案或資料夾，並排除指定排除檔案模式的檔案或資料夾。 系統會先擷取最舊的檔案或資料夾。 也會擷取超過等待時間的檔案和資料夾。 在一次掃描中，處理的檔案或資料夾數目取決於批次大小。 如需檔案模式的詳細資訊，請參閱 [關於檔案模式](configuring-watched-folder-endpoints.md#about-file-patterns). 如需關於設定批次大小的資訊，請參閱 [Watched資料夾服務設定](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).
   * 挑選要處理的檔案或資料夾。 如果檔案或資料夾未完全下載，則會在下次掃描時擷取它們。 為確保資料夾完全下載，管理員應使用排除檔案模式建立具有名稱的資料夾。 在資料夾擁有所有檔案後，必須將其重新命名為包含檔案模式中指定的模式。 此步驟可確保資料夾具有呼叫服務所需的所有必要檔案。 如需確認資料夾已完全下載的詳細資訊，請參閱 [Watched資料夾的提示與秘訣](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).
   * 選取要處理的檔案或資料夾後，將其移至舞台資料夾。
   * 根據端點輸入引數對映，將stage資料夾中的檔案或資料夾轉換為適當的輸入。 如需輸入引數對應的範例，請參閱 [Watched資料夾的提示與秘訣](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).


1. 系統會以同步或非同步方式叫用為端點設定的目標服務。 使用為端點設定的使用者名稱和密碼叫用目標服務。

   * 同步叫用會直接呼叫目標服務並立即處理回應。
   * 非同步叫用時，會透過「作業管理員」服務呼叫目標服務，將請求置於佇列中。 「工作管理員服務」接著會呼叫provider.file_write_results_service來處理結果。

1. provider.file_write_results_service會處理目標服務呼叫的回應或失敗。 成功後，會根據端點設定將輸出儲存到結果資料夾。 如果端點設定為在成功完成時保留結果，provider.file_write_results_service也會保留來源。

   當呼叫目標服務導致失敗時，provider.file_write_results_service會將失敗的原因記錄在failure.log檔案中，並將該檔案放在失敗資料夾中。 失敗資料夾是根據為端點指定的設定引數建立的。 當管理員為端點組態設定「失敗時保留」選項時，provider.file_write_results_service也會將來源檔案複製到失敗資料夾。 如需有關從失敗資料夾中復原檔案的資訊，請參閱 [失敗點和復原](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Watched資料夾端點設定 {#watched-folder-endpoint-settings}

使用下列設定來設定watched資料夾端點。

**名稱：** （必要）識別端點。 請勿包含&lt;字元，因為這會截斷工作區中顯示的名稱。 如果您輸入URL作為端點的名稱，請確定它符合RFC1738中指定的語法規則。

**說明：** 端點的說明。 請勿包含&lt;字元，因為這會截斷工作區中顯示的說明。

**路徑：** （必要）指定watched資料夾位置。 在叢集環境中，此設定必須指向可從叢集中的每台電腦存取的共用網路資料夾。

**非同步：** 將呼叫型別識別為非同步或同步。 預設值為非同步。 建議將非同步處理用於長效處理作業，而建議將同步處理用於暫時性或短效處理作業。

**Cron運算式：** 如果必須使用cron運算式排程watched資料夾，請輸入cron運算式。 設定此設定時，會忽略「重複間隔」。

**重複間隔：** 掃描watched資料夾以進行輸入的間隔（以秒為單位）。 除非啟用「節流閥」設定，否則「重複間隔」應比處理平均作業的時間長；否則，系統可能會過載。 默认值为 5。如需詳細資訊，請參閱「批次大小」的說明。

**重複計數：** 觀察資料夾掃描資料夾或目錄的次數。 值–1表示無限掃描。 預設值為–1。

**節流：** 選取此選項時，會限制AEM表單在任何指定時間處理的監看資料夾工作數目。 最大工作數量由「批次大小」值決定。 （請參閱關於節流）。

**使用者名稱：** （必要）從watched資料夾叫用目標服務時使用的使用者名稱。 預設值為SuperAdmin。

**網域名稱：** （必要）使用者的網域。 預設值為DefaultDom。

**批次大小：** 每次掃描要擷取的檔案或資料夾數目。 用於防止系統過載；一次掃描太多檔案可能會導致當機。 默认值为 2。

「重複間隔」和「批次大小」設定決定Watched Folder在每次掃描中擷取多少檔案。 Watched資料夾使用Quartz執行緒集區來掃描輸入資料夾。 執行緒集區會與其他服務共用。 如果掃描間隔很小，執行緒會經常掃描輸入資料夾。 如果檔案經常被拖放到watched資料夾中，則您應該將掃描間隔保持較小。 如果檔案不常被捨棄，請使用較大的掃描間隔，讓其他服務可以使用執行緒。

如果捨棄了大量的檔案，請讓批次大小變大。 例如，如果watched資料夾端點叫用的服務每分鐘可以處理700個檔案，且使用者以相同速率將檔案放入輸入資料夾，則將「批次大小」設定為350秒，並將「重複間隔」設定為30秒，可協助Watched資料夾發揮效能，而不會產生經常掃描watched資料夾的成本。

當檔案被拖放到watched資料夾中時，它會列出輸入中的檔案，如果每秒都進行掃描，可能會降低效能。 增加掃描間隔可以改善效能。 如果要刪除的檔案量很小，請相應地調整「批次大小」和「重複間隔」。 例如，如果每秒丟棄10個檔案，請嘗試將「重複間隔」設定為1秒，並將「批次大小」設定為10。

**等待時間：** 建立資料夾或檔案後，掃描資料夾或檔案前的等待時間（毫秒）。 例如，如果等待時間為3,600,000毫秒（一小時），且檔案是在一分鐘前建立的，則系統會在59分鐘或更長時間後擷取此檔案。 默认值为 0。

此設定對於確保檔案或資料夾完全複製到輸入資料夾非常有用。 例如，如果您有大型檔案要處理，且檔案下載需要10分鐘，請將等待時間設定為10&amp;ast；60 &amp;ast；1000毫秒。 這可防止watched資料夾在檔案不是十分鐘之前掃描檔案。

**排除檔案模式：** 分號 **；** Watched資料夾用來決定要掃描和擷取哪些檔案和資料夾的分隔模式清單。 任何具有此模式的檔案或資料夾都不會掃描以進行處理。

當輸入是具有多個檔案的資料夾時，此設定會很有用。 資料夾的內容可以複製到一個資料夾中，其名稱會由watched資料夾擷取。 這可防止watched資料夾在資料夾完全複製到輸入資料夾之前擷取資料夾進行處理。

您可以使用檔案模式來排除：

* 具有特定副檔名的檔案；例如，&amp;ast；.dat、&amp;ast；.xml、&amp;ast；.pdf。
* 具有特定名稱的檔案；例如，資料。&amp;ast；會排除名為的檔案和資料夾(&amp;a) *data1*， *data2*、等等。
* 在名稱和副檔名中有複合運算式的檔案，如下列範例所示：

   * 資料[0-9][0-9][0-9].[dD][aA]&#39;連線埠&#39;
   * &amp;ast；。[dD][Aa]&#39;連線埠&#39;
   * &amp;ast；。[Xx][公厘][Ll]

如需檔案模式的詳細資訊，請參閱 [關於檔案模式](configuring-watched-folder-endpoints.md#about-file-patterns).

**包含檔案模式：** （必要）分號 **；** Watched資料夾用來決定要掃描和擷取哪些資料夾和檔案的分隔模式清單。 例如，如果「包含檔案模式」是input&amp;ast；，則會擷取符合input&amp;ast；的所有檔案和資料夾。 這包括名為input1、input2等的檔案和資料夾。

預設值為&amp;ast；，表示所有檔案和資料夾。

您可以使用檔案模式來包含：

* 具有特定副檔名的檔案；例如，&amp;ast；.dat、&amp;ast；.xml、&amp;ast；.pdf。
* 具有特定名稱的檔案；例如，資料。&amp;ast；將包含名為的檔案和資料夾 *data1*， *data2*、等等。
* 在名稱和副檔名中有複合運算式的檔案，如下列範例所示：

   * 資料[0-9][0-9][0-9].[dD][aA]&#39;連線埠&#39;
   * &amp;ast；。[dD][Aa]&#39;連線埠&#39;
   * &amp;ast；。[Xx][公厘][Ll]

如需檔案模式的詳細資訊，請參閱 [關於檔案模式](configuring-watched-folder-endpoints.md#about-file-patterns).


**結果資料夾：** 儲儲存儲存存結果的資料夾。 如果結果未出現在此資料夾中，請檢查失敗資料夾。 唯讀檔案不會處理，且會儲存在失敗資料夾中。 此值可以是具有下列檔案模式的絕對或相對路徑：

* %F =檔案名稱前置詞
* %E =副檔名
* %Y =年（完整）
* %y =年（最後兩位數）
* %M =月
* %D =日期
* %d =一年中的第幾天
* %H =小時（24小時時鐘）
* %h =小時（12小時時鐘）
* %m =分鐘
* %s =秒
* %l =毫秒
* %R =隨機數字（介於0到9之間）
* %P =處理程式或工作識別碼

例如，如果是2009年7月17日晚上8點，而您指定 `C:/Test/WF0/failure/%Y/%M/%D/%H/`，結果資料夾為 `C:/Test/WF0/failure/2009/07/17/20`.

如果路徑不是絕對路徑而是相對路徑，則會在watched資料夾內建立資料夾。 預設值為result/%Y/%M/%D/，這是Watched資料夾內的Result資料夾。 如需檔案模式的詳細資訊，請參閱 [關於檔案模式](configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
>結果資料夾大小越小，Watched資料夾的效能就越好。 例如，如果watched資料夾的估計負載為每小時1000個檔案，請嘗試以下模式 `result/%Y%M%D%H` 因此每小時會建立一個新的子資料夾。 如果負載較小（例如，每天1000個檔案），您可以使用以下模式 `result/%Y%M%D`.

**保留資料夾：** 成功掃描和擷取後儲存檔案的位置。 路徑可以是絕對、相對或Null目錄路徑。 您可以使用檔案模式，如「結果資料夾」中所述。 預設值為preserve/%Y/%M/%D/。

**失敗資料夾：** 儲存失敗檔案的資料夾。 此位置永遠是相對於watched資料夾。 您可以使用檔案模式，如「結果資料夾」中所述。

唯讀檔案不會處理，且會儲存在失敗資料夾中。

預設值為failure/%Y/%M/%D/。

**失敗時保留：** 如果無法對服務執行操作，請保留輸入檔案。 預設值為true。

**覆寫重複的檔案名稱：** 當設定為True時，結果資料夾和保留資料夾中的檔案會被覆寫。 設定為False時，名稱會使用具有數值索引尾碼的檔案和資料夾。 預設值為False。

**清除持續時間：** （必要）當結果資料夾中的檔案和資料夾早於此值時，系統便會清除這些檔案和資料夾。 此值以天為單位。 此設定對於確保結果資料夾未填滿非常有用。

值–1天表示從不刪除結果資料夾。 預設值為–1。

**作業名稱：** （必要）可指派給watched資料夾端點的作業清單。

**輸入引數對應：** 用於設定處理服務和操作所需的輸入。 可用的設定視使用watched資料夾端點的服務而定。 以下是兩種輸入型別：

**常值：** Watched資料夾會使用在顯示的欄位中輸入的值。 支援所有基本Java型別。 例如，如果API使用字串、long、int和Boolean等輸入，則字串會轉換為適當型別並叫用服務。

**變數：** 輸入的值是watched資料夾用來挑選輸入的檔案模式。 例如，在加密密碼服務的情況下，輸入檔案必須是PDF檔案，使用者可以使用&amp;ast；.pdf作為檔案模式。 Watched資料夾會擷取Watched資料夾中符合此模式的所有檔案，並叫用每個檔案的服務。 使用變數時，所有輸入檔案都會轉換為檔案。 僅支援使用「檔案」作為輸入型別的API。

**輸出引數對應：** 用於設定服務和操作的輸出。 可用的設定視使用watched資料夾端點的服務而定。

監看資料夾輸出可以是單一檔案、檔案清單或檔案地圖。 然後，使用「輸出引數對應」中指定的模式，將這些輸出檔案儲存在結果資料夾中。

>[!NOTE]
>
>指定產生唯一輸出檔案名稱的名稱，可改善效能。 例如，假設服務傳回一個輸出檔案，而「輸出引數對應」將其對應到 `%F.%E` （輸入檔案的檔案名稱和副檔名）。 在此情況下，如果使用者每分鐘都捨棄具有相同名稱的檔案，則結果資料夾會設定為 `result/%Y/%M/%D`，且「覆寫重複檔案名稱」設定為關閉， Watched Folder會嘗試解析重複的檔案名稱。 解析重複檔案名稱的程式可能會影響效能。 在此情況下，將輸出引數對應變更為 `%F_%h_%m_%s_%l` 將小時、分鐘、秒和毫秒新增至名稱，或確保捨棄的檔案具有唯一名稱可改善效能。

## 關於檔案模式 {#about-file-patterns}

管理員可以指定可以叫用服務的檔案型別。 可以為每個watched資料夾建立多個檔案模式。 檔案模式可以是下列其中一個檔案屬性：

* 具有特定副檔名的檔案；例如，&amp;ast；.dat、&amp;ast；.xml、&amp;ast；.pdf，；
* 具有特定名稱的檔案；例如，資料。&amp;ast；
* 在名稱和副檔名中有複合運算式的檔案，如下列範例所示：

   * 資料[0-9][0-9][0-9].[dD][aA]&#39;連線埠&#39;
   * &amp;ast；。[dD][Aa]&#39;連線埠&#39;
   * &amp;ast；。[Xx][公厘][Ll]

管理員可以定義儲存結果的輸出資料夾的檔案模式。 對於輸出資料夾（結果、保留和失敗），管理員可以指定以下任何檔案模式：

* %Y =年（完整）
* %y =年（最後兩位數）
* %M =月，
* %D =日期，
* %d =一年中的第幾天，
* %h =小時，
* %m =分鐘，
* %s =秒，
* %R =介於0到9之間的隨機數
* %J =工作名稱

例如，結果資料夾的路徑可能是 `C:\Adobe\Adobe_Experience_Manager_forms\BarcodedForms\%y\%m\%d`.

輸出引數對應也可以指定其他模式，例如：

* %F =來源檔案名稱
* %E =來源副檔名

如果輸出引數對應模式以「File.separator」（即路徑分隔符號）結尾，則會建立資料夾並將內容複製到該資料夾。 如果模式不是以「File.separator」結尾，則會以該名稱建立內容（結果檔案或資料夾）。 如需輸出引數對應的詳細資訊，請參閱 [Watched資料夾的提示與秘訣](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).

## 關於節流 {#about-throttling}

為監看資料夾端點啟用節流時，會限制可在任何指定時間處理的監看資料夾工作數目。 作業的最大數量由「批次大小」值決定，此值也可以在Watched資料夾端點中設定。 當達到節流限制時，不會輪詢watched資料夾輸入目錄中的傳入檔案。 檔案也會保留在輸入目錄中，直到其他監看資料夾工作完成且進行另一次輪詢嘗試為止。 在同步處理的情況下，即使作業是在單一執行緒中連續處理，在單一輪詢中處理的所有作業都將計入節流限制中。

>[!NOTE]
>
>節流不會隨叢集縮放。 啟用節流時，叢集作為一個整體不會在任何指定時間處理超過批次大小中指定的作業數。 此限制是整個叢集，並非叢集中的每個節點所特有。 例如，當批次大小為2時，單一節點處理兩個作業即可達到節流限制，而其中一個作業完成前，沒有其他節點會輪詢輸入目錄。

### 節流如何運作 {#how-throttling-works}

Watched Folder會在每個重複間隔掃描輸入資料夾，挑選在「批次大小」中指定的檔案數，然後為每一個檔案叫用目標服務。 例如，如果「批次大小」為4，則每次掃描時，Watched Folder會挑選四個檔案、建立四個叫用請求，然後叫用目標服務。 在完成這些要求之前，如果叫用Watched Folder，則無論前四個工作是否已完成，它都會再次啟動四個工作。

節流功能可防止Watched資料夾在先前工作未完成時叫用新工作。 Watched資料夾會偵測進行中的工作，並根據批次大小減去進行中的工作來處理新工作。 例如，在第二個叫用中，如果完成的工作數目只有三個，而一個工作仍在進行中，則Watched Folder只會叫用另外三個工作。

* Watched資料夾取決於Stage資料夾中存在的檔案數量，以找出有多少工作正在進行中。 如果Stage資料夾中的檔案仍未處理，Watched Folder將不會叫用任何其他工作。 例如，如果批次大小為四且有三個工作已停止，Watched Folder在後續的叫用中將只會叫用一個工作。 有多個情況可能會導致Stage資料夾中的檔案保持未處理狀態。 當工作停止時，管理員可以終止表單工作流程管理頁面上的程式，以便Watched Folder將檔案移出Stage資料夾。
* 如果表單伺服器在Watched Folder可以叫用工作之前關閉，管理員可以將檔案移出Stage資料夾。 如需詳細資訊，請參閱 [失敗點和復原](configuring-watched-folder-endpoints.md#failure-points-and-recovery).
* 如果Forms伺服器正在執行，但Watched Folder在Job Manager服務回撥時未執行（當服務未依順序啟動時發生），管理員可以將檔案移出stage資料夾。 如需詳細資訊，請參閱 [失敗點和復原](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## 效能與擴充性 {#performance-and-scalability}

Watched資料夾可在單一節點上提供總計100個資料夾。 Watched資料夾的效能取決於表單伺服器的效能。 對於非同步叫用，效能更取決於系統載入和「作業管理員」佇列中的作業。

將節點新增至叢集可改善Watched資料夾效能。 Watched資料夾工作會透過Quartz排程器散佈到叢集節點，在非同步要求的情況下，則由Job Manager服務散佈。 所有工作都會保留在資料庫中。

Watched Folder依賴排程器服務來排程、取消排程和重新排程工作。 其他服務，例如「事件管理」服務、「使用者管理員」服務，以及「電子郵件提供者」服務，都可共用排程器服務執行緒集區。 這可能會影響Watched資料夾效能。 當所有服務都開始使用排程器服務執行緒集區時，需要對其進行調整。

## 叢集中的Watched資料夾 {#watched-folders-in-a-cluster}

在叢集中，Watched資料夾依靠Quartz排程器和Job Manager服務來負載平衡和容錯移轉。 如需Quartz叢集行為的詳細資訊，請參閱 [Quartz檔案](https://www.quartz-scheduler.org/documentation).

Watched Folder會在每次輪詢時執行以下三個主要工作：

* 掃描資料夾
* 叫用目標服務
* 處理結果

負載平衡和容錯移轉行為會依據監視資料夾是設定為同步或非同步叫用而改變。

### 叢集中的同步監看資料夾 {#synchronous-watched-folder-in-a-cluster}

對於同步叫用，Quartz負載平衡器會決定哪個節點會取得輪詢事件。 取得輪詢事件的節點會執行所有工作：掃描資料夾、叫用目標服務及處理結果。

![en_synchwatchedfoldercluster](assets/en_synchwatchedfoldercluster.png)

對於同步叫用，當一個節點失敗時，Quartz排程器會傳送新的輪詢事件到其他節點。 在失敗節點上啟動的呼叫將會遺失。 如需有關如何復原與失敗工作相關聯的檔案的詳細資訊，請參閱 [失敗點和復原](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


### 叢集中的非同步Watched資料夾 {#asynchronous-watched-folder-in-a-cluster}

對於非同步叫用，Quartz負載平衡器會決定哪個節點會取得輪詢事件。 取得輪詢事件的節點會掃描輸入資料夾，並透過將請求放入Job Manager服務佇列來叫用目標服務。 工作管理員服務負載平衡器會負責決定哪個節點將處理叫用請求。 即使節點A建立了叫用請求，節點B最終也可能處理該請求。 或者，啟動啟動請求的節點最終也可能處理請求。

![en_asynchwatchedfoldercluster](assets/en_asynchwatchedfoldercluster.png)

對於非同步呼叫，當一個節點失敗時，Quartz排程器會傳送新的輪詢事件給其他節點。 在失敗節點上建立的叫用要求將會在「工作管理員」服務佇列中，並會傳送至其他節點以供處理。 未建立叫用請求的檔案將保留在階段資料夾中。 如需有關如何復原與失敗工作相關聯的檔案的詳細資訊，請參閱 [失敗點和復原](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## 失敗點和復原 {#failure-points-and-recovery}

在每個輪詢事件中，Watched Folder會鎖定輸入資料夾、將符合包含檔案模式的檔案移動到舞台資料夾，然後解除鎖定輸入資料夾。 需要鎖定，這樣兩個執行緒就不會擷取同一組檔案並處理它們兩次。 較小的重複間隔和較大的批次大小，會增加發生此情況的機率。 檔案移至stage資料夾後，輸入資料夾會解除鎖定，以便其他執行緒可以掃描該資料夾。 此步驟有助於提供高輸送量，因為其他執行緒可以在一個執行緒處理檔案時進行掃描。

檔案移至Stage資料夾後，系統會為每個檔案建立叫用請求，並叫用目標服務。 Watched Folder可能無法復原Stage資料夾中的檔案：

* 如果伺服器在Watched Folder建立啟動請求之前關閉，stage資料夾中的檔案會保留在stage資料夾中，且不會復原。
* 如果Watched Folder已順利為stage資料夾中的每個檔案建立叫用要求，且伺服器當機，則根據叫用型別有兩種行為：

**同步：** 如果Watched Folder設定為同步叫用服務，stage資料夾中的所有檔案在stage資料夾中仍保持未處理狀態。

**非同步：** 在此情況下，Watched資料夾會仰賴「工作管理員」服務。 如果「工作管理員服務」回撥Watched資料夾，系統會根據叫用的結果，將stage資料夾中的檔案移至preserve或failure資料夾。 如果「工作管理員」服務沒有回撥Watched資料夾，檔案在Stage資料夾中仍會保持未處理狀態。 當「工作管理員」回撥時，Watched資料夾未執行，就會發生這種情況。

### 正在復原Stage資料夾中未處理的來源檔案 {#recovering-unprocessed-source-files-in-the-stage-folder}

當Watched Folder無法處理階段資料夾中的來源檔案時，您可以復原未處理的檔案。

1. 重新啟動應用程式伺服器或節點。
1. （選用）停止Watched資料夾處理新輸入檔案。 如果您略過此步驟，將更難判斷哪些檔案在Stage資料夾中未處理。 若要防止Watched資料夾處理新的輸入檔案，請執行下列其中一項工作：

   * 在「應用程式和服務」中，將watched資料夾端點的「包含檔案模式」引數變更為不符合任何新輸入檔案的引數(例如，輸入 `NOMATCH`)。
   * 暫停建立新輸入檔案的程式。
   等候AEM表單復原並處理所有檔案。 大多數檔案應該會復原，任何新輸入檔案都會正確處理。 您等待Watched資料夾復原及處理檔案的時間長度將取決於要叫用的作業長度和要復原的檔案數目。

1. 判斷哪些檔案無法處理。 如果您已等待適當的時間且已完成上一步驟，但舞台資料夾中仍存在未處理的檔案，請前往下一個步驟。

   >[!NOTE]
   >
   >您可以檢視階段目錄中檔案的日期和時間戳記。 根據檔案數量和正常處理時間，您可以確定哪些檔案的年齡足以被視為卡住。

1. 將未處理的檔案從stage目錄複製到輸入目錄。
1. 如果您在步驟2中阻止Watched資料夾處理新的輸入檔案，請將「包含檔案模式」變更為先前的值，或重新啟用您停用的程式。

## watched資料夾的安全性考量 {#security-considerations-for-watched-folders}

每個監看資料夾都設定有使用者名稱和密碼。 叫用服務時會使用這些認證。 Watched資料夾仰賴共用資料夾受基礎安全性檔案系統保護，因此只有watched資料夾的擁有者才能存取該共用資料夾。

## Watched資料夾的提示與秘訣 {#tips-and-tricks-for-watched-folders}

以下是設定Watched資料夾端點時的一些秘訣和技巧：

* 如果您在Windows上有處理影像檔案的Watched資料夾，請指定「包含檔案模式」或「排除檔案模式」選項的值，以防止Windows自動產生的Thumbs.db檔案由Watched資料夾輪詢。
* 如果指定cron運算式，則會忽略重複間隔。 cron運算式使用方式是根據Quartz開放原始碼作業排程系統1.4.0版。
* 批次大小是每次掃描watched資料夾時擷取的檔案或資料夾數目。 如果批次大小設定為2和10個檔案或資料夾放入watched資料夾輸入資料夾，則每次掃描只會擷取2個檔案或資料夾。 下次掃描（將在重複間隔中指定的時間後進行）時，將會擷取下兩個檔案。
* 對於檔案模式，管理員可以指定規則運算式，並新增對萬用字元模式的支援，以指定檔案模式。 Watched資料夾修改規則運算式以支援萬用字元模式，例如&amp;ast；。&amp;ast；或&amp;ast；.pdf。 規則運算式不支援這些萬用字元模式。
* Watched Folder會掃描輸入資料夾以取得輸入，並且不知道來源檔案或資料夾是否已完全複製到輸入資料夾，然後開始處理檔案或資料夾。 若要確保在擷取檔案或資料夾之前，將來源檔案或資料夾完全複製到watched資料夾的輸入資料夾，請執行下列工作：

   * 使用等待時間，這是觀察資料夾從上次修改時間開始等待的時間（以毫秒為單位）。 如果您有大型檔案需要處理，請使用此功能。 例如，如果檔案需要10分鐘下載，請將等待時間指定為10&amp;ast；60 &amp;ast；1000毫秒。 這會防止Watched Folder在10分鐘內擷取檔案。
   * 使用排除檔案模式與包含檔案模式。 例如，如果排除檔案模式為 `ex*` 而且包含檔案模式為 `in*`，Watched Folder會挑選以「in」開頭的檔案，不會挑選以「ex」開頭的檔案。 若要複製大型檔案或資料夾，請先重新命名檔案或資料夾，使名稱以「ex」開頭。 將名為「ex」的檔案或資料夾完全複製到監視資料夾後，將其重新命名為「in&amp;ast；」。

* 使用清除持續時間保持結果資料夾乾淨。 Watched資料夾會清除所有超過清除期間中提及之期間的檔案。 持續時間以天為單位。
* 新增Watched資料夾端點時，在選取操作名稱之後，會填入輸入引數對應。 對於操作的每個輸入，都會產生一個輸入引數對應欄位。 以下是輸入引數對應的範例：

   * 對象 `com.adobe.idp.Document` input：如果服務操作有型別的輸入 `Document`，管理員可以將對應型別指定為 `Variable`. Watched Folder會根據為輸入引數指定的檔案模式，從watched資料夾的輸入資料夾中擷取輸入。 如果管理員指定 `*.pdf` 做為引數，系統將會擷取每個副檔名為.pdf的檔案，並轉換為 `com.adobe.idp.Document`，並叫用服務。
   * 對象 `java.util.Map` input：如果服務操作有型別的輸入 `Map`，管理員可以將對應型別指定為 `Variable` 並輸入對應值，其模式如下 `*.pdf`. 例如，服務需要兩個的地圖 `com.adobe.idp.Document` 代表輸入資料夾（例如1.pdf和2.pdf）中兩個檔案的物件。 Watched Folder會建立以索引鍵作為檔案名稱，以值作為的地圖 `com.adobe.idp.Document`.
   * 對象 `java.util.List` 輸入：如果服務作業具有型別「清單」的輸入，則管理員可以將對應型別指定為 `Variable` 並輸入對應值，其模式如下 `*.pdf`. 將PDF檔案放入輸入資料夾時，Watched Folder會建立 `com.adobe.idp.Document` 代表這些檔案並叫用目標服務的物件。
   * 對象 `java.lang.String`：管理員有兩個選項。 首先，管理員可以指定對應型別 `Literal` 和輸入對應值作為字串，例如 `hello.` Watched資料夾將使用字串叫用服務 `hello`. 其次，管理員可以將對應型別指定為 `Variable` 並輸入對應值，其模式如下 `*.txt`. 在後一種情況下，副檔名為.txt的檔案會讀為檔案，以字串形式強迫來叫用服務。
   * Java基本型別：管理員可以指定對應型別 `Literal` 並提供值。 Watched資料夾將使用指定的值叫用服務。

* Watched資料夾適用於處理檔案。 支援的輸出包括 `com.adobe.idp.Document`， `org.w3c.Document`， `org.w3c.Node`以及這些型別的清單和對應。 任何其他型別都會導致失敗資料夾中的失敗輸出。
* 如果結果不在結果資料夾中，請驗證失敗資料夾以檢視是否發生失敗。
* Watched資料夾在非同步模式下使用時效果最佳。 在此模式中，Watched資料夾會將叫用要求放入佇列並回撥。 然後會以非同步方式處理佇列。 如果未設定「非同步」選項，Watched Folder會同步叫用目標服務，而Process Engine會等待服務完成要求並產生結果。 如果目標服務需要很長時間來處理請求，Watched資料夾可能會發生逾時錯誤。
* 建立watched資料夾以進行匯入和匯出作業時，無法擷取副檔名。 使用watched資料夾叫用Form Data Integration服務時，輸出檔案的副檔名型別可能與檔案物件型別的預期輸出格式不符。 例如，如果呼叫匯出作業的監看資料夾的輸入檔案是包含資料的XFA表單，則輸出應該是XDP資料檔案。 若要取得副檔名正確的輸出檔案，您可以在輸出引數對應中指定它。 在此範例中，您可以使用%F.xdp作為輸出引數對應。
* Watched Folder可能會先處理輸入檔案，然後才將其完全複製到資料夾。 在UNIX上不強制鎖定檔案，因為它在Windows上是。 因此，當檔案被複製到watched資料夾時，Watched資料夾可能會將檔案移動到舞台，而不需要等待檔案複製完成。 此行為只會造成輸入檔案的一部分被處理。 目前有兩個因應措施：

   * 因應措施1

      1. 指定「排除檔案模式」的模式，例如temp&amp;ast；.ps。
      1. 將以temp開頭的檔案（例如temp1.ps）複製到watched資料夾。
      1. 將檔案完全複製到watched資料夾後，重新命名檔案以對應於「包含檔案模式」指定的模式。 Watched Folder然後將完成的檔案移至舞台。
   * 因應措施2

      如果您知道將檔案複製到watched資料夾所需的最長時間，請指定「等待時間」的時間（以秒為單位）。 Watched Folder接著會等待指定的時間長度，再將檔案移至舞台。

      這不是Windows上的檔案問題，因為Windows會在寫入執行緒時鎖定檔案。 不過，這是Windows資料夾的問題。 針對資料夾，您必須遵循因應措施1中的步驟。


* 如果Watched資料夾的「保留資料夾名稱」端點屬性設定為Null目錄路徑，則不會清除暫存目錄。 目錄仍包含已處理的檔案和暫存資料夾。

## Watched資料夾的服務特定建議 {#service-specific-recommendations-for-watched-folders}

對於所有服務，您應該調整Watched資料夾的批次大小和重複間隔，以便Watched資料夾挑選新檔案和資料夾進行處理的速率不會超過AEM表單伺服器可以處理的工作速率。 實際使用的引數可能會有所不同，這取決於設定的Watched資料夾數目、哪些服務使用的是Watched資料夾，以及工作在處理器上的密集程度。

### 產生PDF服務建議 {#generate-pdf-service-recommendations}

* 「產生PDF」服務一次只能轉換下列檔案型別的一個檔案：Microsoft Word、Microsoft Excel、Microsoft PowerPoint、Microsoft Project、AutoCAD、Adobe Photoshop®、Adobe FrameMaker®和AdobePageMaker®。 這些是長時間執行的工作；因此，請務必將批次大小保持在低設定。 如果叢集中有更多節點，也請增加重複間隔。
* 針對PostScript (PS)、Encapsulated PostScript (EPS)和影像檔案型別，產生PDF服務可同時處理多個檔案。 您應該根據伺服器的容量和叢集中的節點數目，仔細調整工作階段Bean集區大小（這會控制並行進行的轉換數目）。 然後增加批次大小，使其等於您嘗試轉換之檔案型別的工作階段Bean集區大小。 輪詢頻率應該由叢集中的節點數目來指定；但是，由於「產生PDF」服務處理這些型別的作業的速度很快，因此您可以將重複間隔設定為較低的值，例如5或10。
* 即使「產生PDF」服務一次只能轉換一個OpenOffice檔案，轉換速度還是相當快。 PS、EPS和影像轉換的上述邏輯也適用於OpenOffice轉換。
* 若要在叢集中啟用均勻負載分佈，請將批次大小保持低並增加重複間隔。

### 條碼式表單服務建議 {#barcoded-forms-service-recommendations}

* 為了在處理條碼式表單（小型檔案）時獲得最佳效能，請輸入 `10` 批次大小和 `2` 重複間隔。
* 將許多檔案放在輸入資料夾中時，出現隱藏檔案的錯誤，稱為 *thumbs.db* 可能會發生。 因此，建議您將include檔案的「包含檔案模式」(Include File Pattern)設定為與針對輸入變數指定的值相同(例如， `*.tiff`)。 這會導致Watched資料夾無法處理DB檔案。
* 批次大小值 `5` 和重複間隔 `2` 通常就足夠了，因為條碼Forms服務通常需要大約0.5秒來處理一個條碼。
* Watched Folder不會等候Process Engine完成工作，然後才挑選新檔案或資料夾。 它會持續掃描watched資料夾並叫用目標服務。 此行為可能會導致引擎過載，造成資源問題和逾時。 請確定您使用重複間隔和批次大小來限制Watched資料夾輸入。 如果存在更多監看資料夾或在端點上啟用節流，您可以增加重複間隔並降低批次大小。 如需節流的相關資訊，請參閱 [關於節流](configuring-watched-folder-endpoints.md#about-throttling).
* Watched資料夾會模擬使用者名稱和網域名稱中指定的使用者。 如果直接叫用或程式短暫執行，Watched資料夾會叫用此使用者身分的服務。 對於長效處理序，會使用System前後關聯叫用處理序。 管理員可以設定Watched資料夾的作業系統原則，以判斷允許或拒絕存取的使用者。
* 使用檔案模式來組織結果、失敗和保留資料夾。 (請參閱 [關於檔案模式](configuring-watched-folder-endpoints.md#about-file-patterns).)

* Watched資料夾仰賴Quartz排程器掃描watched資料夾。 Quartz排程器有執行緒集區來掃描它們。 如果watched資料夾的重複間隔非常低（&lt; 5秒）且批次大小高(> 2)，就可能發生競爭條件。 當這種情況發生時，兩個Quartz執行緒會擷取一個檔案：

   * 其中一個執行緒成功找到檔案，並叫用該檔案的目標服務。
   * 第二個執行緒會看到檔案，但嘗試找出檔案是否有效（讀取或寫入檔案）時失敗，這會造成錯誤失敗，指出檔案因唯讀而無法處理。 只有低重複間隔和高批次大小時才會發生這種情況。
