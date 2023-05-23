---
title: AEM Forms中的Watched資料夾
seo-title: Watched folder in AEM Forms
description: 管理員可將資料夾置於監看狀態，並在檔案置於監看資料夾中時啟動工作流程、服務或指令碼作業。
seo-description: An administrator can put a folder on watch and start a workflow, service, or script operation when a file is placed in the folder being watched.
uuid: 39eac0fd-8212-46ff-b75d-8b4320d448a9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: db38972c-be3f-49fd-8cc1-45b16ed244af
docset: aem65
exl-id: fbf5c7c3-cb01-4fda-8e5d-11d56792d4bf
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '7149'
ht-degree: 0%

---

# AEM Forms中的Watched資料夾{#watched-folder-in-aem-forms}

管理員可以設定網路資料夾（稱為Watched資料夾），以便在使用者將檔案(例如PDF檔案)放入Watched資料夾時，會啟動預先設定的工作流程、服務或指令碼操作，以處理新增的檔案。 服務執行指定的操作後，會將結果檔案儲存在指定的輸出資料夾中。 如需工作流程、服務和指令碼的詳細資訊，請參閱 [處理檔案的各種方法](#variousmethodsforprocessingfiles).

## 建立Watched資料夾 {#create-a-watched-folder}

您可以使用下列其中一種方法，在檔案系統上建立Watched資料夾：

* 設定Watched資料夾設定節點的屬性時，請在folderPath屬性中輸入父目錄的完整路徑，並附加要建立的Watched資料夾名稱，如下列範例所示： `C:/MyPDFs/MyWatchedFolder`
此 
`MyWatchedFolder`資料夾不存在，AEM Forms會嘗試在指定的路徑建立資料夾。

* 在設定Watched資料夾端點之前，先在檔案系統上建立資料夾，然後在folderPath屬性中提供完整路徑。 如需folderPath屬性的詳細資訊，請參閱 [Watched資料夾屬性](#watchedfolderproperties).

>[!NOTE]
>
>在叢集環境中，用來作為Watched資料夾的資料夾必須在檔案系統或網路上可存取、可寫入和共用。 叢集的每個應用程式伺服器執行個體都必須擁有相同共用資料夾的存取權。 在Windows上，在所有伺服器上建立對應的網路磁碟機，並在folderPath屬性中指定對應網路磁碟機的路徑。

## 建立Watched資料夾設定節點 {#create-watched-folder-configuration-node}

若要設定Watched資料夾，請建立Watched資料夾設定節點。 執行以下步驟來建立設定節點：

1. 以管理員身分登入CRX-DE Lite，並導覽至/etc/fd/watchfolder/config資料夾。

1. 建立型別的節點 `nt:unstructured`. 例如， watchedfolder

   >[!NOTE]
   >
   >Watched Folder節點名稱不能包含空格和特殊字元。

1. 將下列屬性新增至節點：

   * `folderPath`
   * `inputProcessorType`
   * `inputProcessorId`
   * `outputFilePattern`

   如需支援屬性的完整清單，請參閱 [Watched資料夾屬性](#watchedfolderproperties).

1. 按一下 **全部儲存**. 建立節點並儲存屬性後。 此 `input`， `result`， `failure`， `preserve`、和 `stage`資料夾是在 `folderPath` 屬性。

   掃描作業會以定義的時間間隔開始掃描Watched資料夾。

## Watched資料夾屬性 {#watchedfolderproperties}

您可以為Watched資料夾設定下列屬性。

* **folderPath （字串）**：在定義的時間間隔掃描的資料夾路徑。 對於叢集環境，資料夾必須位於共用位置，且所有伺服器都可完整存取伺服器。 這是強制屬性。
* **inputProcessorType （字串）**：要啟動的程式型別。 您可以指定工作流程、指令碼或服務。 這是強制屬性。
* **inputProcessorId （字串）**：inputProcessorId屬性的行為是根據inputProcessorType屬性指定的值。 這是強制屬性。 下列清單詳細說明了inputProcessorType屬性的所有可能值以及inputProcessorType屬性的對應必要條件：

   * 對於工作流程，請指定要執行的工作流程模型。 例如，/etc/workflow/models/&lt;workflow_name>/jcr：content/model
   * 對於指令碼，指定要執行的指令碼的JCR路徑。 例如， /etc/fd/watchfolder/test/testScript.ecma
   * 針對服務，指定用於找到OSGi服務的篩選器。 此服務註冊為com.adobe.aemfd.watchfolder.service.api.ContentProcessor Interface的實作。

* **runModes （字串）**：以逗號分隔的工作流程執行允許的執行模式清單。 以下是幾個範例：

   * 作者

   * 发布

   * 作者，发布

   * 發佈，作者

>[!NOTE]
>
>如果裝載Watched資料夾的伺服器沒有任何指定的執行模式，則無論伺服器上的執行模式為何，Watched資料夾一律會啟動。

* **outputFilePattern （字串）**：輸出檔案的模式。 您可以指定資料夾或檔案模式。 如果指定資料夾模式，則輸出檔案的名稱會如工作流程中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述。 [檔案和資料夾模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) 也可以指定輸出檔案的目錄結構。 這是強制屬性。

* **stageFileExpirationDuration （長，預設–1）**：已擷取以供處理的輸入檔案/資料夾應被視為已逾時並標籤為失敗之前，所等待的秒數。 只有當這個屬性的值是正數時，這個到期機制才會啟動。

>[!NOTE]
>
>即使使用此機制將輸入標籤為已逾時，它仍可能在背景中處理，但所花的時間比預期多。 如果輸入內容在逾時機制啟動之前被使用，處理甚至可能稍後繼續完成，輸出將被傾印到結果資料夾中。 如果內容在逾時之前未使用，處理很可能在稍後嘗試使用內容時失敗，而且此錯誤也會記錄到相同輸入的失敗資料夾中。 另一方面，如果因間歇性工作/工作流程誤觸發（這是到期機制所針對的情況）而從未啟動輸入的處理，則當然不會發生這兩個事件。 因此，對於失敗資料夾中因逾時而被標籤為失敗的任何專案(尋找形式為「檔案經過長時間後未處理，標籤為失敗！」的訊息。 在失敗記錄檔中)，建議您掃描結果資料夾（以及失敗資料夾本身，以尋找相同輸入的其他專案），以檢查先前所述的任何事件是否實際發生。

* **deleteExpiredStageFileOnlyWhenThrottled （布林值，預設為true）：** 到期機制是否應該只在監視資料夾已節流時啟動。 此機制與節流監視資料夾的關聯性較高，因為啟用節流時，少量以未處理狀態延遲的檔案（由於間歇性工作/工作流程錯誤引發）可能會阻塞整個批次的處理作業。 如果此屬性保持為true （預設值），則不會為未節流的Watch資料夾啟用到期機制。 如果屬性保留為false，則只要stageFileExpirationDuration屬性是正數，機制就會一律啟動。

* **pollInterval （長）**：掃描Watched資料夾以進行輸入的間隔（以秒為單位）。 除非啟用「限制」設定，否則「輪詢間隔」應比處理平均作業的時間長；否則，系統可能會變得超載。 默认值为 5。如需詳細資訊，請參閱「批次大小」的說明。 輪詢間隔的值必須大於或等於1。
* **excludeFilePattern （字串）**：分號(；)分隔的模式清單，Watched資料夾會使用這個清單來決定要掃描和擷取的檔案和資料夾。 不會掃描任何具有此模式的檔案或資料夾以進行處理。 當輸入是具有多個檔案的資料夾時，此設定會很有用。 資料夾的內容可以複製到一個資料夾中，其名稱由Watched資料夾擷取。 這可防止Watched資料夾在資料夾完全複製到輸入資料夾之前擷取資料夾進行處理。 預設值為null。
您可以使用 [檔案模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) 若要排除：

   * 具有特定副檔名的檔案；例如， &#42;.dat， &#42;.xml， .pdf， &#42;.&#42;
   * 具有特定名稱的檔案；例如，資料&#42; 會排除名為data1、data2等的檔案和資料夾。
   * 在名稱和副檔名中有複合運算式的檔案，如下列範例所示：

      * 資料[0-9][0-9][0-9].[dD][aA]&#39;連線埠&#39;
      * &#42;。[dD][Aa]&#39;連線埠&#39;
      * &#42;。[Xx][公厘][Ll]

如需檔案模式的詳細資訊，請參閱 [關於檔案模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

* **includeFilePattern （字串）**：分號(；)分隔的模式清單，Watched資料夾會使用這個清單來決定要掃描和擷取的資料夾和檔案。 例如，如果輸入IncludeFilePattern&#42;，所有符合輸入的檔案和資料夾&#42; 已選取。 這包括名為input1、input2等的檔案和資料夾。 預設值為 &#42; 和會指出所有檔案和資料夾。 您可以使用檔案模式來包含：

   * 具有特定副檔名的檔案；例如， &#42;.dat， &#42;.xml， .pdf， &#42;.&#42;
   * 具有特定名稱的檔案；例如，資料。&#42; 會包含名為data1、data2等的檔案和資料夾。

* 在名稱和副檔名中有複合運算式的檔案，如下列範例所示：

   * 資料[0-9][0-9][0-9].[dD][aA]&#39;連線埠&#39;

      * &#42;。[dD][Aa]&#39;連線埠&#39;
      * &#42;。[Xx][公厘][Ll]

如需檔案模式的詳細資訊，請參閱 [關於檔案模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)

* **waitTime （長）**：建立資料夾或檔案後，在掃描資料夾或檔案之前等待的時間（以毫秒為單位）。 例如，如果等待時間為3,600,000毫秒（一小時），且檔案是在一分鐘前建立的，則系統會在59分鐘或更長時間後擷取此檔案。 默认值为 0。此設定對於確保檔案或資料夾完全複製到輸入資料夾非常有用。 例如，如果您有大型檔案要處理，而檔案下載需要10分鐘，請將等待時間設定為10&#42;60 &#42;1000毫秒。 這可防止Watched資料夾在檔案不是十分鐘之前掃描檔案。
* **purgeDuration （長）**：結果資料夾中的檔案和資料夾早於此值時會遭清除。 此值以天為單位。 此設定對於確保結果資料夾未填滿非常有用。 值–1天表示從不刪除結果資料夾。 預設值為–1。
* **resultFolderName （字串）**：儲儲存存結果的資料夾。 如果結果未出現在此資料夾中，請檢查失敗資料夾。 唯讀檔案不會處理並儲存在失敗資料夾中。 此值可以是具有下列檔案模式的絕對或相對路徑：

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

   例如，如果是2009年7月17日晚上8點，而您指定C：/Test/WF0/failure/%Y/%M/%D/%H/，則結果資料夾是C：/Test/WF0/failure/2009/07/17/20

   如果路徑不是絕對路徑而是相對路徑，則會在Watched資料夾內建立資料夾。 預設值為result/%Y/%M/%D/，這是Watched資料夾內的Result資料夾。 如需檔案模式的詳細資訊，請參閱 [關於檔案模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

>[!NOTE]
>
>結果資料夾的大小越小，Watched資料夾的執行效能就越好。 例如，如果Watched資料夾的估計負載為每小時1000個檔案，請嘗試如result/%Y%M%D%H的模式，以便每小時建立新的子資料夾。 如果負載較小（例如，每天1000個檔案），您可以使用如result/%Y%M%D的模式。

* **failureFolderName （字串）**：儲存失敗檔案的資料夾。 此位置永遠是相對於Watched資料夾。 您可以使用檔案模式，如「結果資料夾」中所述。 唯讀檔案不會處理並儲存在失敗資料夾中。 預設值為failure/%Y/%M/%D/。
* **preserveFolderName （字串）：** 成功處理後儲存檔案的位置。 路徑可以是絕對、相對或Null目錄路徑。 您可以使用檔案模式，如「結果資料夾」中所述。 預設值為preserve/%Y/%M/%D/。
* **batchSize （長）**：每次掃描要擷取的檔案或資料夾數目。 用於防止系統過載；一次掃描太多檔案可能會導致當機。 默认值为 2。

   「輪詢間隔」和「批次大小」設定會決定Watched Folder在每次掃描中擷取多少檔案。 Watched資料夾使用Quartz執行緒集區來掃描輸入資料夾。 執行緒集區會與其他服務共用。 如果掃描間隔很小，執行緒會經常掃描輸入資料夾。 如果檔案經常被拖放到Watched資料夾中，則您應該將掃描間隔維持在較小的範圍內。 如果檔案不常被捨棄，請使用較大的掃描間隔，讓其他服務可以使用執行緒。

   如果捨棄了大量的檔案，請讓批次大小變大。 例如，如果Watched Folder端點啟動的服務每分鐘可以處理700個檔案，且使用者以相同速率將檔案放入輸入資料夾，則將「批次大小」設定為350，並將「輪詢間隔」設定為30秒，可協助Watched Folder發揮效能，而不會產生經常掃描Watched Folder的成本。

   當檔案被放入Watched資料夾時，它會列出輸入中的檔案，如果每秒都進行掃描，可能會降低效能。 增加掃描間隔可以改善效能。 如果捨棄的檔案量很小，請相應地調整「批次大小」和「輪詢間隔」。 例如，如果每秒丟棄10個檔案，請嘗試將pollInterval設定為1秒，並將Batch Size設定為10

* **throttleOn （布林值）**：選取此選項時，會限制AEM Forms在任何指定時間處理的Watched資料夾工作數目。 最大工作數量由「批次大小」值決定。 預設值為true。 (請參閱 [關於節流](../../forms/using/watched-folder-in-aem-forms.md#p-about-throttling-p).)

* **overwriteDuplicateFilename （布林值）**：設為True時，會覆寫結果資料夾和保留資料夾中的檔案。 設定為False時，名稱會使用具有數值索引尾碼的檔案和資料夾。 預設值為False。
* **preserveOnFailure （布林值）**：保留輸入檔案，以防無法對服務執行操作。 預設值為true。
* **inputFilePattern （字串）**：指定Watched資料夾的輸入檔案模式。 建立檔案的允許清單。
* **非同步（布林值）**：將呼叫型別識別為非同步或同步。 預設值為true （非同步）。 檔案處理是一項耗用資源的工作，請將非同步標幟的值保持為true以避免阻塞掃描工作的主要執行緒。 在叢集環境中，保持標幟為true對於啟用跨可用伺服器處理之檔案的負載平衡至關重要。 如果標幟為false，則掃描作業會嘗試在其自己的執行緒內依序對每個頂層檔案/資料夾執行處理。 若無特定原因（例如單一伺服器設定上的工作流程處理），請勿將標幟設為false 。

>[!NOTE]
>
>依設計，工作流程會非同步。 即使您將值設為false，工作流程也會以非同步模式啟動。

* **已啟用（布林值）**：停用及啟用Watched資料夾的掃描。 將enabled設為true，以開始掃描Watched資料夾。 預設值為true。
* **payloadMapperFilter：** 當資料夾設定為watched資料夾時，會在watched資料夾中建立資料夾結構。 此結構有資料夾來提供輸入、接收輸出（結果）、儲存失敗資料、保留資料供長期程式使用，以及儲存資料供不同階段使用。 Watched資料夾的資料夾結構可作為以Forms為中心的工作流程裝載。 裝載對應程式可讓您定義裝載的結構，該裝載使用Watched資料夾進行輸入、輸出和處理。 例如，如果您使用預設對應程式，它會將Watched資料夾的內容對應 [裝載]\輸入和 [裝載]\output資料夾。 提供兩種現成的裝載對應程式實作。 如果您沒有 [自訂實施](../../forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)，使用其中一種現成可用的實作：

   * **預設對應程式：** 使用預設的裝載對應程式，將watched資料夾的輸入和輸出內容保留在裝載中的個別輸入和輸出資料夾中。 此外，在工作流程的裝載路徑中，使用 [裝載]/input/和 [裝載]/output路徑以擷取和儲存內容。

   * **簡單的檔案型裝載對應程式：** 使用簡單檔案型裝載對應程式，將輸入和輸出內容直接保留在裝載資料夾中。 它不會建立任何額外的階層，例如預設對應程式。

### 自訂設定引數 {#custom-configuration-parameters}

除了上面列出的Watched資料夾組態屬性之外，您也可以指定自訂組態引數。 自訂引數會傳遞至檔案處理程式碼。 它可讓程式碼根據引數的值變更其行為。 若要指定引數，請執行下列動作：

1. 登入CRXDE-Lite並瀏覽至Watched Folder設定節點。
1. 新增屬性引數。&lt;property_name> 至Watched Folder設定節點。 屬性的型別只能是布林值、日期、小數、雙精度浮點數、長數字和字串。 您可以指定單一和多值屬性。

>[!NOTE]
>
>如果屬性的資料型別為Double，則在此類屬性的值中指定小數點。 對於資料型別為Double且值中未指定小數點的所有屬性，型別會轉換為Long。

這些屬性會以Map型別的不可變對應形式傳遞&lt;string object=&quot;&quot;> 至處理程式碼。 處理程式碼可以是ECMAScript、工作流程或服務。 為屬性提供的值在對應中作為索引鍵/值組提供。 索引鍵是屬性的名稱，值是屬性的值。 如需自訂組態引數的詳細資訊，請參閱下列影像：

![具有強制屬性、一些選擇性屬性、一些設定引數的監看資料夾設定節點範例](assets/custom-configuration-parameters.png)

具有強制屬性、一些選擇性屬性、一些設定引數的監看資料夾設定節點範例。

#### 工作流程的可变变量 {#mutable-variables-for-workflows}

您可以為工作流程型檔案處理方法建立可變變數。 這些變數可當作在工作流程步驟之間流動的資料的容器。 若要建立這類變數：

1. 登入CRXDE-Lite並瀏覽至Watched Folder設定節點。

1. 新增屬性workflow.var。&lt;variable_name> 至Watched Folder設定節點。

   屬性的型別只能是布林值、日期、小數、雙精度浮點數、長數字和字串。 也支援多值屬性。 對於多值屬性，工作流程步驟可用的值是指定型別的陣列。

   >[!NOTE]
   >
   >如果屬性的資料型別為Double，則在此類屬性的值中指定小數點。 對於資料型別為Double且值中未指定小數點的所有屬性，型別會轉換為Long。

>[!NOTE]
>
>JCR規格強制預設屬性值。 預設值可用於工作流程的步驟以進行處理。 因此，請指定適當的預設值。

![custom-configuration-parameters2](assets/custom-configuration-parameters2.png)

## 處理檔案的各種方法 {#variousmethodsforprocessingfiles}

您可以啟動工作流程、服務或指令碼，以處理監看資料夾中的檔案位置。

### 使用服務處理Watched資料夾的檔案   {#using-a-service-to-process-files-of-a-watched-folder-nbsp}

服務是自訂的 `com.adobe.aemfd.watchfolder.service.api.ContentProcessor` 介面。 它會向OSGi註冊以及一些自訂屬性。 實作的自訂屬性使其獨特，並有助於識別實作。

#### ContentProcessor介面的自訂實作 {#custom-implementation-of-the-contentprocessor-interface}

自訂實作接受處理內容（com.adobe.aemfd.watchfolder.service.api.ProcessorContext型別的物件）、從內容讀取輸入檔案和設定引數、處理輸入，以及將輸出新增回內容。 ProcessorContext具有下列API：

* **getWatchFolderId**：傳回監看資料夾的ID。
* **getInputMap**：傳回「對應」型別的對應。 對映的鍵是輸入檔案的檔案名稱以及包含檔案內容的檔案物件。 使用getinputMap API讀取輸入檔案。
* **getConfigParameters**：傳回Map型別的不可變對應。 對應包含Watched資料夾的設定引數。

* **setResult**： ContentProcessor實作會使用API將輸出檔案寫入結果資料夾。 您可以為setResult API的輸出檔案提供名稱。 API可能會根據指定的輸出資料夾/檔案模式，選擇使用或忽略提供的檔案。 如果指定資料夾模式，則輸出檔案的名稱會如工作流程中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述。

例如，下列程式碼是具有custom foo=bar屬性的ContentProcessor介面的自訂實作。

```java
@Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
@Service(value = {OutputWriter.class, ContentProcessor.class})
@Property(name = "foo", value = "bar")
public class OutputWriter implements ContentProcessor {
```

當 [設定Watched資料夾](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p)，如果您將inputProcessorId屬性指定為(foo=bar)，將inputProcessorType屬性指定為Service，則上述服務（自訂實作）將用於處理Watched資料夾的輸入檔案。

以下範例也是ContentProcessor介面的自訂實作。 在此範例中，服務接受輸入檔案，將檔案複製到暫存位置，然後傳回包含檔案內容的檔案物件。 檔案物件的內容會儲存到結果資料夾。 結果資料夾的實體路徑設定於 [Watched資料夾設定節點](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

```java
@Component(immediate = true)
@Service(value = ContentProcessor.class)
@Property(name = "serviceSelector", value = "testProcessor1")
public class TestContentProcessor1 implements ContentProcessor {
    @Override
    public void processInputs(ProcessorContext context) throws Exception {
        Map.Entry<String, Document> e = context.getInputMap().entrySet().iterator().next();
        File f = new File((String) context.getConfigParameters().get("tempDir"),
                context.getConfigParameters().get("outPrefix") + e.getKey());
        e.getValue().copyToFile(f);
        context.setResult(f.getName(), new Document(f, true));
    }
}
```

### 使用指令碼處理Watched資料夾的檔案 {#using-scripts-to-process-files-of-a-watched-folder}

指令碼是寫入到處理放置在Watched資料夾中的檔案的ECMAScript投訴自訂程式碼。 指令碼會以JCR節點表示。 除了標準ECMAScript變數（記錄、sling等）之外，指令碼還有變數processorContext。 變數的型別為ProcessorContext。 ProcessorContext具有下列API：

* **getWatchFolderId**：傳回監看資料夾的ID。
* **getInputMap**：傳回「對應」型別的對應。 對映的鍵是輸入檔案的檔案名稱以及包含檔案內容的檔案物件。 使用getinputMap API讀取輸入檔案。
* **getConfigParameters**：傳回Map型別的不可變對應。 對應包含Watched資料夾的設定引數。
* **setResult**： ContentProcessor實作會使用API將輸出檔案寫入結果資料夾。 您可以為setResult API的輸出檔案提供名稱。 API可能會根據指定的輸出資料夾/檔案模式，選擇使用或忽略提供的檔案。 如果指定資料夾模式，則輸出檔案的名稱會如工作流程中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述。

下列程式碼為ECMAScript範例。 它接受輸入檔案，將檔案複製到暫存位置，並傳回檔案物件與檔案內容。 檔案物件的內容會儲存到結果資料夾。 結果資料夾的實體路徑設定於 [Watched資料夾設定節點](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

>[!NOTE]
>
>輸出資料夾和檔案名稱首碼是根據Watched Folder組態引數來決定。

```java
var inputMap = processorContext.getInputMap();
var params = processorContext.getConfigParameters();
var entry = inputMap.entrySet().iterator().next();
var tempFile = new Packages.java.io.File(params.get("tempDir"), params.get("outPrefix") + entry.getKey());
entry.getValue().copyToFile(tempFile);
processorContext.setResult(tempFile.getName(), new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true));
```

#### 指令碼的位置和安全性考量 {#location-of-scripts-and-security-considerations}

依預設，會提供一個容器資料夾(/etc/fd/watchfolder/scripts)，客戶可以在其中放置其指令碼，而watch-folder架構使用的預設service-user具有從此位置讀取指令碼的必要許可權。

如果您計畫將指令碼放在自訂位置，則預設服務使用者可能沒有自訂位置的讀取許可權。 對於這種情況，請執行以下步驟，為自訂位置提供必要許可權：

1. 以程式設計方式或透過主控台https://&#39;建立系統使用者[伺服器]：[連線埠]&#39;/crx/explorer. 您也可以使用現有系統使用者。 請務必在此與系統使用者合作，而非與一般使用者合作。
1. 在儲存指令碼的自訂位置上，為新建立或現有系統使用者提供讀取許可權。 您可以有多個自訂位置。 至少為所有自訂位置提供讀取許可權。
1. 在Felix設定主控台(/system/console/configMgr)中，找到監視資料夾的服務使用者對應。 此對應類似於「對應： adobe-aemds-core-watch-folder=...」。
1. 按一下對應。 對於「adobe-aemds-core-watch-folder：scripts=fd-service」專案，請將fd-service變更為自訂系統使用者的ID。 单击“保存”。

現在，您可以使用已設定的自訂位置來儲存指令碼。

### 使用工作流程處理Watched資料夾的檔案 {#using-a-workflow-to-process-files-of-a-watched-folder}

工作流程可讓您自動化Experience Manager活動。 工作流程包含一系列以特定順序執行的步驟。 每個步驟都會執行不同的活動，例如啟動頁面或傳送電子郵件訊息。 工作流程可以與存放庫中的資產、使用者帳戶和Experience Manager服務互動。 因此，工作流程可能會協調複雜。

* 建立「工作流程」之前，請先考慮下列幾點：
* 步驟的輸出必須可用於所有後續步驟。
步驟必須能夠更新（甚至刪除）由先前步驟產生的現有輸出。
* 可變變數可用來在步驟之間流轉自訂動態資料。

執行以下步驟，使用工作流程處理檔案：

1. 建立實作 `com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextProcessor` 介面。 它類似於為服務建立的實作。

   >[!NOTE]
   >
   >您可以完全在ECMAScript中建立完整的實作。

1. 在Workflow的步驟中，找到型別為com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService的OSGi服務，並使用以下引數呼叫服務的execute()方法。

   * 您的WorkflowContextProcessor介面的自訂實作
   * 工作專案
   * workflowsession
   * 元数据

如果您使用Java程式設計語言來實作工作流程，AEM工作流程引擎會為workItem、workflowSession和中繼資料變數提供值。 這些變數會以引數的形式傳遞至自訂WorkflowProcess實作的execute()方法。

如果您使用ECMAScript來實作工作流程，AEM工作流程引擎會提供graniteWorkItem、graniteWorkflowSession和中繼資料變數的值。 這些變數會作為引數傳遞至WorkflowContextService.execute()方法。

processWorkflowContext()的引數是com.adobe.aemfd.watchfolder.workflow.api.WorkflowContext型別的物件。 WorkflowContext介面具有下列API，可促進上述工作流程特定考量事項：

* getWorkItem：傳回WorkItem變數值。 變數會傳遞至WorkflowContextService.execute()方法。
* getWorkflowSession：傳回WorkflowSession變數值。 變數會傳遞至WorkflowContextService.execute()方法。
* getMetadata：傳回中繼資料變數的值。 變數會傳遞至WorkflowContextService.execute()方法。
* getCommittedVariables：傳回代表先前步驟所設定變數的唯讀物件對應。 如果變數未在前面的任何步驟中修改，則會傳回在設定Watched資料夾時指定的預設值。
* getCommittedResults：傳回唯讀檔案對應。 對應代表先前步驟產生的輸出檔案。
* setVariable： WorkflowContextProcessor實作會使用變數來操作變數，這些變數代表在步驟之間流動的自訂動態資料。 變數的名稱和型別與期間指定的變數名稱相同 [設定Watched資料夾](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p). 若要變更變數的值，請使用非null值呼叫setVariable API。 若要移除變數，請使用null值呼叫setVariable()。

也可以使用下列ProcessorContext API：

* getWatchFolderId：傳回監看資料夾的ID。
* getInputMap：傳回Map型別的對應&lt;string document=&quot;&quot;>. 對映的鍵是輸入檔案的檔案名稱以及包含檔案內容的檔案物件。 使用getinputMap API讀取輸入檔案。
* getConfigParameters：傳回Map型別的不可變對應&lt;string object=&quot;&quot;>. 對應包含Watched資料夾的設定引數。
* setResult： ContentProcessor實作會使用API將輸出檔案寫入結果資料夾。 您可以為setResult API的輸出檔案提供名稱。 API可能會根據指定的輸出資料夾/檔案模式，選擇使用或忽略提供的檔案。 如果指定資料夾模式，則輸出檔案的名稱會如工作流程中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述

setResult API用於工作流程時的考量事項：

* 若要新增有助於整體工作流程輸出的輸出檔案，請使用先前步驟未用作輸出檔案名稱的檔案名稱來呼叫setResult API。
* 若要更新先前步驟產生的輸出，請使用先前步驟已使用的檔案名稱呼叫setResult API。
* 若要刪除上一步驟產生的輸出，請以上一個步驟已使用的檔案名稱呼叫setResult，並以空值作為內容。

>[!NOTE]
>
>在任何其他情況下呼叫具有null內容的setResult API會導致錯誤。

下列範例已實作為工作流程步驟。 在此範例中，ECMAscript會使用變數stepCount來追蹤在目前工作流程例項中呼叫步驟的次數。
輸出資料夾的名稱是目前步驟編號、原始檔案名稱和outPrefix引數中指定的前置詞的組合。

ECMAScript會取得工作流程內容服務的參考，並建立WorkflowContextProcessor介面的實作。 WorkflowContextProcessor實作接受輸入檔案、將檔案複製到暫存位置，並傳回代表所複製檔案的檔案。 根據布林值變數purgePrevious的值，目前步驟會刪除與目前工作流程例項中啟動步驟時相同的步驟上次產生的輸出。 最後，會叫用wfSvc.execute方法執行WorkflowContextProcessor實作。 輸出檔案的內容會儲存在Watched Folder設定節點中提及的實體路徑的結果資料夾中。

```javascript
log.error("Watch-folder workflow script called for step: " + graniteWorkItem.getNode().getTitle());
var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
// Custom WorkflowContextProcessor implementation which defines the processWorkflowContext() method purely in JS
var impl = { processWorkflowContext: function (wfContext) {
    var wfId = wfContext.getWatchFolderId();
    var inputMap = wfContext.getInputMap();
    var paramMap = wfContext.getConfigParameters();
    var preResults = wfContext.getCommittedResults();
    var preVars = wfContext.getCommittedVariables();
    log.info("WF ID: " + wfId); // workflowId of type String
    log.info("Inputs: " + inputMap); // Input map of type Map<String, Document>
    log.info("Params: " + paramMap); // Config params of type Map<String, Object>
    log.info("Old results: " + preResults);
    log.info("Old variables: " + preVars);
    var currStepNumber = new Packages.java.lang.Long(new Packages.java.lang.Long(preVars.get("stepCount")).longValue() + 1);
    log.info("Current step number: " + currStepNumber);
    wfContext.setVariable("stepCount", currStepNumber);
    var entry = inputMap.entrySet().iterator().next();
    var tempFile = new Packages.java.io.File(paramMap.get("tempDir"), paramMap.get("outPrefix") + "STEP-" + currStepNumber + "-" + entry.getKey());
    entry.getValue().copyToFile(tempFile);
    var fName = tempFile.getName();
    var outDoc = new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true);
    wfContext.setResult(tempFile.getName(), outDoc);
    var prevStepOutName = paramMap.get("outPrefix") + "STEP-" + (currStepNumber - 1) + "-" + entry.getKey();
    if (preResults.containsKey(prevStepOutName) && paramMap.get("purgePrevious").booleanValue()) {
        log.info("Purging previous step output " + prevStepOutName);
        wfContext.setResult(prevStepOutName, null);
    }
} }
wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
log.info("Exiting workflow script!")
```

### 建立裝載對應程式篩選器，將Watched資料夾的結構對應至工作流程的裝載 {#create-payload-mapper-filter-to-map-structure-of-a-watched-folder-to-the-payload-of-a-workflow}

當您建立watched資料夾時，它會在被監視的資料夾中建立資料夾結構。 資料夾結構有階段、結果、保留、輸入和失敗資料夾。 資料夾結構可作為工作流程的輸入裝載，並接受來自工作流程的輸出。 它也可以列出失敗點（如果有）。

如果有效負載的結構與watched資料夾的結構不同，您可以撰寫自訂指令碼，將watched資料夾的結構對應至有效負載。 此類指令碼稱為裝載對應程式篩選器。 AEM Forms提供立即可用的裝載對應程式篩選器，將watched資料夾的結構對應至裝載。

#### 建立自訂裝載對應程式篩選器 {#creating-a-custom-payload-mapper-filter}

1. 下載 [Adobe使用者端SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/).
1. 在Maven型專案的建置路徑中設定使用者端SDK。 若要開始使用，您可以下載並在您選擇的IDE中開啟以下maven型專案。
1. 編輯範例套件中可用的裝載對應程式篩選程式程式碼以符合您的需求。
1. 使用maven建立自訂裝載對應程式篩選器的套件。
1. 使用 [AEM套件組合主控台](https://localhost:4502/system/console/bundles) 以安裝套件組合。

   現在，自訂裝載對應程式篩選器列在AEM Watched資料夾UI中。 您可以將其用於工作流程。

   以下範常式式碼會針對相對於承載儲存的檔案，實作簡單的檔案型對應程式。 您可以使用它來開始。

   ```java
   package com.adobe.aemfd.watchfolder.workflow;
   import com.adobe.aemfd.docmanager.Document;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.PayloadMapper;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowExecutionContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowInitializationContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowVariable;
   import com.adobe.granite.workflow.exec.Workflow;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.ResourceResolver;
   import javax.jcr.Binary;
   import javax.jcr.Node;
   import java.util.Collection;
   import java.util.HashMap;
   import java.util.Map;
   @Component(immediate = true)
   @Service(value = PayloadMapper.class)
   public class SimpleFileBasedPayloadMapper implements PayloadMapper {
   @Override
   public Node createPayload(WorkflowInitializationContext wfInitCtxt, Node stagingFolder, String uniquePayloadName,
   Map<String, Binary> inputs, Collection<WorkflowVariable> variableDefs) throws Exception {
   Node dirNode = stagingFolder.addNode(uniquePayloadName, "sling:Folder");
   for (Map.Entry<String, Binary> bins: inputs.entrySet()) {
   Node fileNode = dirNode.addNode(bins.getKey(), "nt:file");
   Node resNode = fileNode.addNode ("jcr:content", "nt:resource");
   resNode.setProperty("jcr:data", bins.getValue());
   }
   return dirNode;
   }
   @Override
   public Map<String, Document> getInputs(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload, ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public void setOutput(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   String fileName, Binary contents, int outputMode) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getIntermediateOutputs(WorkflowInitializationContext wfInitCtxt,
   WorkflowExecutionContext wfExecCtxt, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getFinalOutputs(WorkflowInitializationContext wfInitCtxt, Workflow workflow, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   Map<String, Object> params = wfInitCtxt.getConfigParameters();
   Map<String, Document> result = new HashMap<String, Document>();
   for (Map.Entry<String, Object> me: params.entrySet()) {
   String key = me.getKey();
   if (key.startsWith("pm.outfile.")) {
   String fName = (String) me.getValue();
   Document d = new Document(payload.getPath() + "/" + fName, resourceResolver);
   result.put(fName, d);
   }
   }
   return result;
   }
   @Override
   public void setVariable(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   WorkflowVariable variable) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Object> getVariables(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   }
   ```

## 使用者如何與Watched資料夾互動 {#how-users-interact-with-a-watched-folder}

對於Watched資料夾端點，使用者可以透過複製輸入檔案或資料夾從其案頭拖曳到Watched資料夾來開始檔案處理作業。 檔案會依到達順序進行處理。

對於Watched資料夾端點，如果作業只需要一個輸入檔案，使用者可以將該檔案複製到Watched資料夾的根目錄。

如果作業包含多個輸入檔案，使用者必須在Watched資料夾階層之外建立包含所有必要檔案的資料夾。 這個新資料夾應該包含輸入檔案(以及選擇性包含的DDX檔案（如果處理序需要）)。 在建構工作資料夾後，使用者將其複製到Watched資料夾的輸入資料夾中。

>[!NOTE]
>
>確定應用程式伺服器已刪除Watched資料夾中檔案的存取權。 如果AEM Forms在掃描檔案後無法從輸入資料夾中刪除這些檔案，則關聯的程式將無限期啟動。

## 關於Watched資料夾的其他資訊 {#additional-information-about-the-watched-folders}

### 關於節流 {#about-throttling}

為監看資料夾端點啟用節流時，會限制在任何指定時間處理的Watched資料夾工作數目。 作業的最大數量由「批次大小」值決定，此值也可以在Watched資料夾端點中設定。 當達到節流限制時，不會輪詢Watched資料夾輸入目錄中的傳入檔案。 檔案也會保留在輸入目錄中，直到其他Watched Folder工作完成並嘗試輪詢為止。 對於同步處理，即使作業在單一執行緒中連續處理，在單一輪詢中處理的所有作業都會計入節流限制內。

>[!NOTE]
>
>節流不會隨叢集縮放。 啟用節流時，叢集作為一個整體不會在任何指定時間處理超過批次大小中指定的作業數。 此限制是整個叢集，並非叢集中的每個節點所特有。 例如，當批次大小為2時，單一節點處理兩個作業即可達到節流限制，而其中一個作業完成前，沒有其他節點會輪詢輸入目錄。

#### 節流如何運作 {#how-throttling-works}

Watched Folder會以每個pollInterval掃描輸入資料夾、擷取「批次大小」中指定的檔案數目，並叫用每個檔案的目標服務。 例如，如果「批次大小」為4，則每次掃描時，Watched Folder會挑選四個檔案、建立四個叫用請求，然後叫用目標服務。 在完成這些要求之前，如果叫用Watched Folder，就會再次啟動四個工作，無論前四個工作是否完成。

節流功能可防止Watched資料夾在先前工作未完成時叫用新工作。 Watched資料夾會偵測進行中的工作，並根據批次大小減去進行中的工作來處理新工作。 例如，在第二個叫用中，如果完成的工作數目只有三個，而一個工作仍在進行中，則Watched Folder只會叫用另外三個工作。

* Watched資料夾取決於Stage資料夾中存在的檔案數量，以找出有多少工作正在進行中。 如果Stage資料夾中的檔案仍未處理，Watched Folder就不會叫用任何其他工作。 例如，如果批次大小為四且有三個工作已停止，「監看資料夾」在後續的叫用中只會叫用一個工作。 有多個情況可能會導致Stage資料夾中的檔案保持未處理狀態。 當工作停止時，管理員可以在「程式管理」管理頁面上終止程式，以便Watched Folder將檔案移出Stage資料夾。
* 如果AEM Forms伺服器在Watched Folder叫用工作之前關閉，管理員可以將檔案移出stage資料夾。 如需詳細資訊，請參閱 [失敗點和復原](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).
* 如果AEM Forms伺服器正在執行，但工作管理員服務回撥時Watched Folder並未執行（當服務未依順序啟動時就會發生），管理員可以將檔案移出stage資料夾。 如需詳細資訊，請參閱 [失敗點和復原](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).

### 失敗點和復原失敗點和復原 {#failure-points-and-recoveryfailure-points-and-recovery}

在每個輪詢事件中，Watched Folder會鎖定輸入資料夾、將符合包含檔案模式的檔案移動到舞台資料夾，然後解除鎖定輸入資料夾。 需要鎖定，這樣兩個執行緒就不會擷取同一組檔案並處理它們兩次。 小pollInterval和大的批次大小會增加發生此情況的機率。 檔案移至stage資料夾後，輸入資料夾會解除鎖定，以便其他執行緒可以掃描該資料夾。 此步驟有助於提供高輸送量，因為其他執行緒可以在一個執行緒處理檔案時進行掃描。

檔案移至Stage資料夾後，系統會為每個檔案建立叫用請求，並叫用目標服務。 Watched Folder可能無法復原Stage資料夾中的檔案：

* 如果伺服器在Watched Folder建立啟動請求之前關閉，stage資料夾中的檔案會保留在stage資料夾中，且不會復原。

* 如果Watched Folder已順利為stage資料夾中的每個檔案建立叫用要求，且伺服器當機，則根據叫用型別有兩種行為：

   * **同步**：如果Watched資料夾設定為同步叫用服務，stage資料夾中的所有檔案在stage資料夾中仍維持未處理狀態。
   * **非同步**：在此情況下，Watched資料夾會仰賴Job Manager服務。 如果「工作管理員服務」回撥Watched資料夾，系統會根據叫用的結果，將stage資料夾中的檔案移至preserve或failure資料夾。 如果「工作管理員」服務沒有回撥Watched資料夾，檔案在Stage資料夾中仍會保持未處理狀態。 當「工作管理員」回撥時，Watched資料夾未執行，就會發生這種情況。

#### 復原stage資料夾中未處理的來源檔案 {#recover-unprocessed-source-files-in-the-stage-folder}

當Watched Folder無法處理階段資料夾中的來源檔案時，您可以復原未處理的檔案。

1. 重新啟動應用程式伺服器或節點。

1. 停止Watched資料夾處理新的輸入檔案。 如果您略過此步驟，將更難判斷哪些檔案在Stage資料夾中未處理。 若要防止Watched資料夾處理新的輸入檔案，請執行下列其中一項工作：

   * 將Watched資料夾的includeFilePattern屬性變更為不符合任何新輸入檔案的內容（例如，輸入NOMATCH）。
   * 暫停建立新輸入檔案的程式。

   等候AEM Forms復原並處理所有檔案。 大多數檔案應該會復原，任何新輸入檔案都會正確處理。 您等待Watched資料夾復原及處理檔案的時間長度將取決於要叫用的作業長度和要復原的檔案數目。

1. 判斷哪些檔案無法處理。 如果您已等待適當的時間且已完成上一步驟，但舞台資料夾中仍存在未處理的檔案，請前往下一個步驟。

   >[!NOTE]
   >
   >您可以檢視階段目錄中檔案的日期和時間戳記。 根據檔案數量和正常處理時間，您可以確定哪些檔案的年齡足以被視為卡住。

1. 將未處理的檔案從stage目錄複製到輸入目錄。

1. 如果您在步驟2中阻止Watched資料夾處理新的輸入檔案，請將「包含檔案模式」變更為先前的值，或重新啟用您停用的程式。

### 將Watched資料夾連結在一起 {#chain-watched-folders-together}

Watched資料夾可以鏈結在一起，因此一個Watched資料夾的結果檔案是下一個Watched資料夾的輸入檔案。 每個Watched資料夾都可以叫用不同的服務。 透過以這種方式設定Watched資料夾，可以叫用多項服務。 例如，一個Watched資料夾可以將PDF檔案轉換為Adobe PostScript®另一個Watched資料夾可以將PostScript檔案轉換為PDF/A格式。 若要這麼做，只要將您第一個端點定義的Watched資料夾的結果資料夾設定為指向您第二個端點定義的Watched資料夾的輸入資料夾。

第一次轉換的輸出會變成\path\result。 第二個轉換的輸入為\path\result，而第二個轉換的輸出會移至\path\result\result （或您在第二個轉換的「結果資料夾」方塊中定義的目錄）。

### 檔案和資料夾模式 {#file-and-folder-patterns}

管理員可以指定可以叫用服務的檔案型別。 可以為每個Watched資料夾建立多個檔案模式。 檔案模式可以是下列其中一個檔案屬性：

* 具有特定副檔名的檔案；例如， &#42;.dat， &#42;.xml， .pdf， &#42;.&#42;
* 具有特定名稱的檔案；例如，資料。&#42;
* 在名稱和副檔名中有複合運算式的檔案，如下列範例所示：

   * 資料[0-9][0-9][0-9].[dD][aA]&#39;連線埠&#39;
   * &#42;。[dD][Aa]&#39;連線埠&#39;
   * &#42;。[Xx][公厘][Ll]

* 管理員可以定義儲存結果的輸出資料夾的檔案模式。 對於輸出資料夾（結果、保留和失敗），管理員可以指定以下任何檔案模式：
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

例如，結果資料夾的路徑可能是C:\Adobe\AdobeLiveCycleES4\BarcodedForms\%y\%m\%d。

輸出引數對應也可以指定其他模式，例如：

* %F =來源檔案名稱
* %E =來源副檔名

如果輸出引數對應模式以「File.separator」（即路徑分隔符號）結尾，則會建立資料夾並將內容複製到該資料夾。 如果模式不是以「File.separator」結尾，則會以該名稱建立內容（結果檔案或資料夾）。

## 搭配Watched資料夾使用PDF產生器 {#using-pdf-generator-with-a-watched-folder}

您可以設定Watched資料夾，以啟動工作流程、服務或指令碼來處理輸入檔案。 在下一節中，我們將設定Watched資料夾以起始ECMAScript。 ECMAScript會使用PDF產生器將Microsoft Word (.docx)檔案轉換為PDF檔案。

執行以下步驟，使用PDF產生器設定Watched資料夾：

1. [建立ECMAScript](../../forms/using/watched-folder-in-aem-forms.md#p-create-an-ecmascript-p)
1. [建立工作流程](../../forms/using/watched-folder-in-aem-forms.md#p-create-a-workflow-p)
1. [設定Watched資料夾](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)

### 建立ECMAScript {#create-an-ecmascript}

ECMAScript會使用PDF產生器的createPDF API將Microsoft Word (.docx)檔案轉換為PDF檔案。 執行以下步驟來建立指令碼：

1. 在瀏覽器視窗中開啟CRXDE Lite。 URL為https://&#39;[伺服器]：[連線埠]&#39;/crx/de.

1. 導覽至/etc/workflow/scripts並建立名為PDFG的資料夾。

1. 在PDFG資料夾中，建立名為pdfg-openOffice-sample.ecma的檔案，並將下列程式碼新增至該檔案：

   ```javascript
   var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
   // Custom ContentProcessor implementation which defines the processInputs() method purely in JS
   var impl = { processWorkflowContext: function (wrkfContext) {
   
     //  var logger = Packages.org.slf4j.LoggerFactory.getLogger("cmb-mergeandprint-sample.ecma");
                   var inputMap=wrkfContext.getInputMap();
   
                   var distiller = sling.getService(com.adobe.pdfg.service.api.DistillerService);
                   var generatePDF = sling.getService(com.adobe.pdfg.service.api.GeneratePDFService);
                   var pdfgConfig = sling.getService(com.adobe.pdfg.service.api.PDFGConfigService);
       var result = new Packages.java.util.HashMap();
       var entry = inputMap.entrySet().iterator().next();
       var pdfgOut = generatePDF.createPDF(entry.getValue(), ".docx", "Standard OpenOffice", "Standard", "No Security", null, null);
                   var convertedDoc = pdfgOut.get("ConvertedDoc");
   //   logger.info("SuccessFully saved the document to Ouput Node");
       wrkfContext.setResult(entry.getKey().substring(0, entry.getKey().lastIndexOf('.'))+".pdf",convertedDoc); // Ownership flag set to true for auto temp-file deletion.
   
   } }
   
   wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
   ```

1. 儲存並關閉檔案。

### 建立工作流程 {#create-a-workflow}

1. 在瀏覽器視窗中開啟AEM Workflow UI。
   <https://[servername>]：&#39;port&#39;/workflow

1. 在「模型」檢視中，按一下 **新增**. 在新工作流程對話方塊中，指定 **標題**，然後按一下 **確定**.

   ![create-a-workflow-pdf](assets/create-a-workflow-pdf.png)

1. 選取新建立的工作流程並按一下 **編輯**. 工作流程會在新視窗中開啟。

1. 刪除預設的工作流程步驟。 將「流程步驟」從Sidekick拖放到「工作流程」。

   ![create-a-workflow-pdf2](assets/create-a-workflow-pdf2.png)

1. 以滑鼠右鍵按一下「處理步驟」並選取 **編輯**. 「步驟屬性」視窗即會出現。

1. 在「處理」標籤中，選取ECMAScript。 例如，在中建立的pdfg-openOffice-sample.ecma指令碼 [建立ECMAScript](#p-create-an-ecmascript-p). 啟用 **處理常式前進** 選項並按一下 **確定**.

   ![create-a-workflow3-pdf](assets/create-a-workflow3-pdf.png)

### 設定Watched資料夾 {#configure-the-watched-folder}

1. 在瀏覽器視窗中開啟CRXDE Lite。 https://&#39;[伺服器]：[連線埠]&#39;/crx/de/

1. 導覽至/etc/fd/watchfolder/config/資料夾，並建立nt：unstructured型別的節點。

   ![configure-the-watched-folder-pdf](assets/configure-the-watched-folder-pdf.png)

1. 將下列屬性新增至節點：

   * folderPath （字串）：在定義的時間間隔掃描的資料夾路徑。 資料夾必須位於共用位置，且所有伺服器都必須具備伺服器的完整存取權。
inputProcessorType （字串）：要啟動的程式型別。 在本教學課程中，指定工作流程。

   * inputProcessorId （字串）： inputProcessorId屬性的行為是根據為inputProcessorType屬性指定的值。 在此範例中，inputProcessorType屬性的值為workflow。 因此，針對inputProcessorId屬性指定PDFG工作流程的以下路徑： /etc/workflow/models/pdfg/jcr：content/model

   * outputFilePattern （字串）：輸出檔案的模式。 您可以指定資料夾或檔案模式。 如果指定資料夾模式，則輸出檔案的名稱會如工作流程中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述。
   除了上述的強制屬性以外，Watched資料夾也支援一些選擇性屬性。 如需選擇性屬性的完整清單和說明，請參閱 [Watched資料夾屬性](#watchedfolderproperties).

## 已知问题 {#watched-folder-known-issues}

在JEE上啟動AEM 6.5 Forms時，系統會在JBoss完全啟動且檔案無法處理之前開始處理檔案。 為避免此情況，請在啟動JBoss之前，清除所有Watched資料夾。
