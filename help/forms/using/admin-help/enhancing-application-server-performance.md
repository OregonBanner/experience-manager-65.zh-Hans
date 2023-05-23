---
title: 增強應用程式伺服器效能
seo-title: Enhancing application server performance
description: 本檔案說明您可以設定的選用設定，以改善AEM表單應用程式伺服器的效能。
seo-description: This document describes optional settings that you can configure to improve the performance of your AEM forms application server.
uuid: 88d2f96a-3b59-410d-8160-20581d27acad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fad65765-d56d-4a9f-82d5-bcceb1758953
exl-id: 6e2f3d4c-2ead-45b3-98e7-32cacc7e2985
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 0%

---

# 增強應用程式伺服器效能{#enhancing-application-server-performance}

本內容說明您可以設定的選用設定，以改善AEM表單應用程式伺服器的效能。

## 設定應用程式伺服器資料來源 {#configuring-application-server-data-sources}

AEM forms使用AEM forms存放庫作為其資料來源。 AEM表單存放庫會儲存應用程式資產，並且在執行階段，服務可以在完成自動化業務流程的過程中從存放庫擷取資產。

根據您正在執行的AEM表單模組數目以及同時存取應用程式的使用者數目，存取資料來源可能相當重要。 可使用連線集區來最佳化資料來源存取。 *連線集區* 是一種技術，用來避免每次應用程式或伺服器物件需要存取資料庫時，建立新資料庫連線的額外負荷。 連線集區通常用於Web應用程式和企業應用程式，通常由應用程式伺服器處理，但不限於應用程式伺服器。

請務必正確設定連線集區引數，以免連線用盡，進而導致應用程式效能降低。

若要正確設定連線集區設定，應用程式伺服器管理員必須在當天的尖峰時段監視連線集區。 監控可確保應用程式和使用者隨時都能使用足夠的連線。 大部分的應用程式伺服器都包含監控工具。

您可以使用「WebLogic伺服器管理主控台」來監視網域中每個JDBC資料來源執行處理的各種統計資料。 如需詳細資訊，請參閱您的WebLogic檔案。

當應用程式伺服器管理員決定正確的連線集區設定時，該人員必須將此資訊傳達給資料庫管理員。 資料庫管理員需要此資訊，因為資料庫連線數目等於資料來源之連線集區中的連線數目。 然後，完成以下步驟來設定應用程式伺服器和資料來源型別的連線集區設定。

### 設定WebLogic的連線集區設定，以供Oracle和MySQL使用 {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. 在「領域結構」下，按一下「服務」>「JDBC」>「資料來源」，然後在右窗格中按一下「IDP_DS」。
1. 在下一個畫面中，按一下「組態>連線集區」標籤，然後在下列方塊中輸入值：

   * 初始容量
   * 最大容量
   * 容量增加
   * 陳述式快取大小

1. 按一下儲存，然後按一下啟用變更。
1. 重新啟動WebLogic管理的伺服器。

### 為SQLServer設定WebLogic的連線集區設定 {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. 在「變更中心」下，按一下「鎖定與編輯」。
1. 在「網域結構」下，按一下「服務」>「JDBC」>「資料來源」，然後在右窗格中按一下「EDC_DS」。
1. 在下一個畫面中，按一下「組態>連線集區」標籤，然後在下列方塊中輸入值：

   * 初始容量
   * 最大容量
   * 容量增加
   * 陳述式快取大小

1. 按一下儲存，然後按一下啟用變更。
1. 重新啟動WebLogic管理的伺服器。

### 為DB2的WebSphere設定連線集區設定 {#configure-connection-pool-settings-for-websphere-for-db2}

1. 在導覽樹狀結構中，按一下「資源」>「JDBC」>「JDBC提供者」。 在右窗格中，按一下您建立的資料來源：DB2 Universal JDBC Driver Provider或LiveCycle- db2 - IDP_DS。
1. 在「其他屬性」下，按一下「資料來源」，然後選取IDP_DS。
1. 在下一個畫面的「其他屬性」下，按一下「連線集區屬性」，然後在「最大連線數」方塊和「最小連線數」方塊中輸入值。
1. 按一下「確定」或「套用」，然後按一下「直接儲存至主組態」。

### 設定WebSphere的連線集區設定以進行Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. 在導覽樹狀結構中，按一下「資源」>「JDBC」>「JDBC提供者」。 在右窗格中，按一下您建立的OracleJDBC驅動程式資料來源。
1. 在「其他屬性」下，按一下「資料來源」，然後選取IDP_DS。
1. 在下一個畫面的「其他屬性」下，按一下「連線集區屬性」，然後在「最大連線數」方塊和「最小連線數」方塊中輸入值。
1. 按一下「確定」或「套用」，然後按一下「直接儲存至主組態」。

### 設定WebSphere for SqlServer的連線集區設定值 {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. 在導覽樹狀結構中，按一下「資源」>「JDBC」>「JDBC提供者」，然後在右窗格中，按一下您建立的「使用者定義的JDBC驅動程式」資料來源。
1. 在「其他屬性」下，按一下「資料來源」，然後選取IDP_DS。
1. 在下一個畫面的「其他屬性」下，按一下「連線集區屬性」，然後在「最大連線數」方塊和「最小連線數」方塊中輸入值：
1. 按一下「確定」或「套用」，然後按一下「直接儲存至主組態」。

## 最佳化內嵌檔案及對JVM記憶體的影響 {#optimizing-inline-documents-and-impact-on-jvm-memory}

如果您通常要處理相對較小大小的檔案，您可以改善與檔案傳輸速度和儲存空間相關的效能。 若要這麼做，請實作下列AEM Forms產品設定：

* 增加AEM表單的預設檔案最大內嵌大小，使其大於大多數檔案的大小。
* 若要處理大型檔案，請指定位於高速磁碟系統或RAM磁碟上的儲存目錄。

內嵌大小上限和儲存目錄(AEM表單暫存檔目錄和GDS目錄)是在管理主控台中設定的。

### 檔案大小和最大內嵌大小 {#document-size-and-maximum-inline-size}

當由AEM表單傳送以進行處理的檔案小於或等於預設檔案最大內嵌大小，檔案會儲存在伺服器內嵌，且會序列化為Adobe檔案物件。 內嵌儲存檔案可帶來顯著的效能優勢。 不過，如果您使用表單工作流程，內容也可能儲存在資料庫中以供追蹤。 因此，增加最大內嵌大小可能會影響資料庫大小。

大於最大內嵌大小的檔案會儲存在本機檔案系統中。 傳輸到伺服器或從伺服器傳輸的Adobe檔案物件只是指向該檔案的指標。

當檔案內容內聯（即小於最大內聯大小）時，內容會作為檔案序列化承載的一部分儲存在資料庫中。 因此，增加最大內嵌大小可能會影響資料庫大小。

**變更內嵌大小上限**

1. 在管理控制檯中，按一下「設定>核心系統設定>設定」。
1. 在「預設檔案最大內嵌大小」方塊中輸入值，然後按一下「確定」。

   >[!NOTE]
   >
   >對於JEE環境上的AEM Forms和JEE環境中包含的OSGi套件組合上的AEM Forms AEM Forms，檔案最大內嵌大小屬性的值必須相同。 此步驟僅針對JEE環境上的AEM Forms更新值，而非JEE環境上的AEM Forms (包含OSGi套件的AEM Forms)。

1. 使用下列系統屬性重新啟動應用程式伺服器：

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >上述系統屬性會覆寫針對JEE環境上的AEM Forms和JEE環境上的OSGi套件組合中包含的AEM FormsAEM Forms所設定的Document Max Inline Size屬性值。

>[!NOTE]
>
>預設內嵌大小上限為65536位元組。

### JVM棧積大小上限 {#jvm-maximum-heap-size}

增加最大內嵌大小需要更多記憶體來儲存序列化檔案。 因此，通常還需要增加JVM棧積大小上限。

處理許多檔案的過載系統可快速讓JVM棧積記憶體達到飽和。 若要避免OutOfMemoryError，請將JVM棧積大小上限增加一個量，該量等於內嵌檔案大小乘以通常在任何指定時間執行的檔案數目。

JVM棧積大小上限增加= （內嵌檔案大小） x （已處理的平均檔案數）。

**正在計算JVM棧積大小上限**

在此範例中，目前的JVM最大棧積設定為512 MB，最大內嵌大小為64 KB。 伺服器必須針對同時執行10個作業的案例進行設定，每個作業都有9個輸入檔案和1個結果檔案（每個作業共有10個檔案和100個檔案同時處理）。 所有檔案的大小都在512 KB以下。

若要內嵌儲存所有檔案，請將內嵌大小上限設定為至少512 KB。

使用以下方程式計算JVM棧積大小上限所需的增加：

(512 KB) x (100) = 51200 KB或50 MB

JVM棧積大小上限必須增加50 MB，總容量才能達到562 MB。

**考慮棧積片段**

將內嵌檔案的大小設定為較大的值，會增加容易產生棧積片段的系統發生OutOfMemoryError的風險。 若要內嵌儲存檔案，JVM棧積記憶體必須有足夠的連續空間。 某些作業系統、JVM和垃圾收集演演算法容易產生棧積片段。 片段會減少連續棧積空間的數量，即使總可用空間足夠，也可能導致OutOfMemoryError。

例如，先前在應用程式伺服器上的操作導致JVM棧積處於分散狀態，而且垃圾回收程式無法充分壓縮棧積，以重新獲得較大的可用空間區塊。 即使已調整JVM棧集大小上限來增加內嵌大小，也可能發生OutOfMemoryError。

若要說明棧積碎片，內嵌檔案大小不可設定為大於棧積總大小的0.1%。 例如，512 MB的JVM最大棧積大小可以支援最大內嵌大小512 MB x 0.001 = 0.512 MB或512 KB。

## WebSphere Application Server增強功能 {#websphere-application-server-enhancements}

本節說明WebSphere Application Server環境的特定設定值。

### 增加配置給JVM的最大記憶體 {#increasing-the-maximum-memory-allocated-to-the-jvm}

如果您正在執行Configuration Manager或嘗試使用命令列公用程式產生Enterprise JavaBeans (EJB)建置程式碼 *ejbdeploy* 且發生OutOfMemory錯誤，請增加配置給JVM的記憶體數量。

1. 在中編輯ejbdeploy指令碼 *[appserver根目錄]*/deploytool/itp/目錄：

   * (Windows) `ejbdeploy.bat`
   * （Linux和UNIX） `ejbdeploy.sh`

1. 尋找 `-Xmx256M` 引數並將其變更為較高的值，例如 `-Xmx1024M`.
1. 保存文件。
1. 執行 `ejbdeploy` 命令或使用Configuration Manager重新部署。

## 透過LDAP改善Windows Server 2003效能 {#improving-windows-server-2003-performance-with-ldap}

此內容說明Microsoft Windows Server 2003作業系統環境的特定設定。

在搜尋連線上使用連線集區最多可減少50%所需的連線埠數量。 這是因為該連線一律會針對指定網域使用相同的認證，而且上下文和相關物件會明確關閉。

### 設定您的Windows Server以進行連線集區 {#configure-your-windows-server-for-connection-pooling}

1. 按一下[開始] > [執行]以啟動登入編輯程式，並在[開啟]方塊中輸入 `regedit` 並按一下「確定」。
1. 移至登入機碼 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. 在登入編輯器的右窗格中，找到TcpTimedWaitDelay值名稱。 如果名稱未出現，請從選單列中選取「編輯」>「新增」>「DWORD值」以新增名稱。
1. 在「名稱」方塊中，輸入 `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >如果您沒有看到閃爍的游標和 `New Value #` 在方塊內，在右側面板內按一下滑鼠右鍵，選取「重新命名」，然後在「名稱」方塊中輸入 `TcpTimedWaitDelay`*.*

1. 對值名稱MaxUserPort、MaxHashTableSize和MaxFreeTcbs重複步驟4。
1. 在右窗格內連按兩下以設定TcpTimedWaitDelay值。 在「基底」下，選取「小數」，然後在「值」方塊中鍵入 `30`.
1. 在右窗格內連按兩下以設定MaxUserPort值。 在「基底」下，選取「小數」，然後在「值」方塊中鍵入 `65534`.
1. 在右窗格內連按兩下以設定MaxHashTableSize值。 在「基底」下，選取「小數」，然後在「值」方塊中鍵入 `65536`.
1. 在右窗格內連按兩下以設定MaxFreeTcbs值。 在「基底」下，選取「小數」，然後在「值」方塊中鍵入 `16000`.

>[!NOTE]
>
>如果您使用登入編輯器或使用其他方法不正確地修改登入，可能會發生嚴重問題。 這些問題可能需要您重新安裝作業系統。 自行修改登入。
