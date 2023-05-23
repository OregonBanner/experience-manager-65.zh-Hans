---
title: 安裝維護作業
seo-title: Install workbench
description: 安裝維護作業。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
role: Admin
exl-id: d530dbb9-f95e-4329-9665-37faf8f7931b
source-git-commit: 18cfefb794382b5314b18a62645f1fba28d314a2
workflow-type: tm+mt
source-wordcount: '2232'
ht-degree: 0%

---

# 安裝Workbench {#install-workbench}

本檔案提供安裝和設定AEM Forms Workbench的說明。 安裝程式也會安裝Forms Designer。

## 誰應該閱讀此檔案？ {#who-should-read-this-doc}

本檔案適用於負責安裝、設定、管理或部署Workbench的管理員或開發人員。 此外，也包含設定您的系統以支援已升級AEM Forms程式的資訊。 所提供的資訊假設任何閱讀本檔案的人都很熟悉Microsoft® Windows®作業系統。

## 附加信息 {#additional-information}

此表格中的資源可協助您進一步瞭解並開始使用AEM Forms。
<table>
 <tbody>
  <tr>
   <td><p><strong>有关信息</strong></p> </td>
   <td><p><strong>请参阅</strong></p> </td>
  </tr>
  <tr>
   <td><p>Workbench的程式資訊</p> </td>
   <td><p><a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Workbench說明</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>有關AEM Forms的一般資訊，以及它如何與其他Adobe產品整合</p> </td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/getting-started/introduction-aem-forms.html?lang=en">AEM Forms概觀</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>AEM Forms的所有可用檔案</p> </td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/getting-started/introduction-aem-forms.html?lang=en">AEM Forms檔案</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>此產品版本的修補程式更新、技術說明和其他資訊</p> </td>
   <td><p>聯絡Adobe企業支援</a><br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM Forms已棄用Flex工作區。 它適用於AEM Forms版本。

## 安裝之前 {#before-you-install}

### Workbench安裝概述 {#workbench-installation-overview}

Workbench是整合式開發環境(IDE)，開發人員和表單作者可使用它來建立自動化的業務流程和表單。 它也用於管理流程和表單使用的資源和服務。

下圖說明Workbench安裝，包括：
* 使用Workbench進行程式設計
* 使用設計工具的表單設計

>[!NOTE]
>
>AEM Forms伺服器需要單獨的安裝程式。 如需詳細資訊，請參閱AEM Forms on JEE安裝檔案。

![default-render-form](assets/installing-workbench.png)

## 系統必備條件 {#system-prerequisites}

本節概述硬體與軟體需求，以及支援的平台。

### 最低硬體與軟體需求 {#minimum-hardware-software-requirements}

**Workbench**
建議最低需求如下：安裝所需的磁碟空間：
* 680 MB （僅適用於Workbench）。
* 2.15 GB的磁碟機，完整安裝Workbench、Designer和範例元件。
* 臨時安裝目錄為400 MB — 使用者\temp目錄為200 MB，Windows臨時目錄為200 MB。

>[!NOTE]
>
>如果所有這些位置都位於單一磁碟機上，安裝期間必須有1.5 GB的可用空間。 安裝完成時，會刪除複製到暫存目錄的檔案。

* 硬體需求：Intel® Pentium® 4或AMD®同等處理器，1 GHz處理器。
* Java™ Runtime Environment (JRE) 7.0更新51或更新版本至7.0。
* 最低1024 X 768畫素或更高的熒幕解析度（含16位元色彩或更高）。
* TCP/IPv4或TCP/IPv6網路連線至AEM Forms伺服器。
* 安裝Visual C++可轉散發執行階段套件2012 32位元。
* 安裝Visual C++可轉散發執行階段套件2013 32位元。

>[!NOTE]
>
>您必須具有管理許可權才能安裝Workbench。 如果您使用非管理員帳戶進行安裝，安裝程式會提示您輸入適當帳戶的認證。

### 支援的平台 {#supported-platforms}

若要檢視Workbench支援平台的完整清單，請前往 [AEM Forms支援的平台](https://www.adobe.com/go/learn_aemforms_supportedplatforms_65).

## 設計工具安裝注意事項 {#designer-installation-considerations}

依預設，Workbench安裝會包含對應的英文版Designer。 如果Workbench安裝應用程式在您的電腦上偵測到現有的Designer版本，安裝可能會終止，而且您必須先移除目前的Designer版本，才能繼續。
下表列出您在安裝Workbench時可能會遇到的可能設計師安裝案例，以及您必須執行的任何動作。

<table>
 <tbody>
  <tr>
   <td><p><strong>目前安裝的設計工具版本</strong></p> </td>
   <td><p><strong>必要動作</strong></p> </td>
  </tr>
  <tr>
   <td><p>Acrobat Pro或Acrobat Pro Extended （包含設計工具）</p> </td>
   <td><p>无。<br /> 
Workbench安裝會偵測到電腦上隨Acrobat Pro或Acrobat Pro Extended一起安裝的Designer執行個體。<br />
不同版本的Designer可以共存於同一個系統中，例如Workbench 6.4的Designer 6.4.x和Workbench 6.5的Designer 6.5.0.x。不需要解除安裝與Acrobat 10 Pro或Acrobat 10 Pro Extended （含）以上版本一起安裝的Designer版本。
<br /></p> </td>
  </tr>
  <tr>
   <td><p>Designer （獨立）</p> </td>
   <td><p>无。<br />Workbench隨附的Designer版本僅限英文。 <br />Workbench安裝程式不會重新安裝新版的Designer。 而是會修補隨Workbench安裝程式提供的更新版本。 這也允許您在Workbench中使用本地化版本的Designer。<br /> </p> </td>
  </tr>
 </tbody>
</table>

### 若要在Windows 10上解除安裝Designer （獨立式） {#uninstall-designer-standalone-windows10}

1. 前往 **「控制面板」>「程式」>「程式和功能」**
1. 在「目前安裝的程式」清單中，選取 **Adobe設計工具**.
1. 按一下 **解除安裝** 然後按一下 **是**.

## 安裝Workbench {#installing-workbench}

本章說明如何安裝Workbench。

### 安裝及執行Workbench {#installing-and-running-workbench}

在安裝Workbench之前，您必須確定您的環境包含執行它所需的軟體和硬體(請參閱區段： **安裝之前**)。

**若要安裝及執行Workbench，請執行下列動作：**

1. 執行下列工作之一：
   * 瀏覽至安裝媒體上的\workbench目錄，然後按兩下run_windows_installer.bat檔案。
   * 將Workbench下載並解壓縮至您的檔案系統。 下載後，瀏覽至\workbench目錄，然後按兩下run_windows_installer.bat檔案。

   >[!IMPORTANT]
   >
   >Workbench安裝程式只會從本機磁碟機執行。 無法從遠端站台執行。

   >[!NOTE]
   >
   >如果您遇到「無法建立Java™虛擬機器器」錯誤，請以值 — Xmx512M建立名為_JAVA_OPTIONS的環境變數並執行安裝程式。

1. 在「簡介」畫面上，按一下「下一步」。
1. 閱讀「產品授權合約」，選取「我接受授權合約的條款」，然後按一下「下一步」。
1. （選擇性）如果您需要此工具來建立和修改表單，請選取「安裝Adobe設計工具」。

   >[!NOTE]
   您可以保留取消選取此選項，繼續使用隨Acrobat 10安裝的Designer。

1. 接受列出的預設目錄，或按一下「選擇」並瀏覽至您要安裝Workbench的目錄，然後按一下「下一步」。

   >[!NOTE]
   安裝目錄路徑不應包含# （井號）和$ （美元）字元。

1. 檢閱安裝前摘要，然後按一下安裝。 安裝程式會顯示安裝進度。
1. 檢閱安裝摘要。 選取「啟動AEM Forms Workbench」以啟動Workbench，然後按一下「下一步」。
1. 檢閱發行說明，然後按一下完成。
1. 您的電腦現在已安裝下列專案：
   * **Workbench**：若要從「開始」功能表執行Workbench，請選取「所有程式> AEM Forms > Workbench」 （如果您選擇將捷徑資料夾儲存在此處）。 如需詳細資訊，請參閱 <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">使用Workbench</a> 說明檔案。
   * **設計工具**：您可以從Workbench內部存取Designer。 如需詳細資訊，請參閱中的快速入門主題。 <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf">Designer說明</a>.
   * **AEM FORMS SDK**：如需使用SDK的詳細資訊，請參閱 <a href="https://helpx.adobe.com/pdf/aem-forms/6-3/programming-with-aem-forms.pdf">使用AEM Forms程式設計</a>.

## 升級程式 {#upgrading-processes}

JEE上的AEM Forms程式可使用升級精靈升級到AEM Forms應用程式。 如需詳細資訊，請參閱Workbench說明中的升級舊版人工因素檔案。

### 設定並登入伺服器 {#configuring-and-logging-server}

若要使用Workbench，您必須執行AEM Forms的執行個體（通常在個別的電腦上）。 您必須有使用者名稱和密碼才能登入AEM Forms，以及關於伺服器位置的詳細資訊。

>[!NOTE]
如果您已將AEM Forms設定為使用EMC Documentum®或IBM® FileNet存放庫提供者，而您想要登入存放庫(AEM Forms管理主控台中設定為預設的存放庫除外)，請提供使用者名稱username@Repository。

### 設定逾時設定 {#configuring-timeout-settings}

根據預設，Workbench會在兩小時後逾時，無論活動或非活動狀態為何。 若要編輯逾時設定，請參閱&lt;設定使用者管理>設定進階系統屬性> <a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/configure-user-management/configure-advanced-system-attributes.html">管理主控台說明</a>.

### 設定Workbench以透過HTTPS連線 {#configuring-workbench-to-connect-over-HTTPS}

若要透過HTTPS將Workbench連線至AEM Forms伺服器，您必須確保會將核發公開金鑰的憑證授權單位(CA)辨識為Workbench所信任。 如果無法辨識憑證來自信任的來源，您必須更新 [Workbench_HOME]/workbench/jre/lib/security目錄。

>[!NOTE]
[Workbench_HOME] 代表您安裝Workbench的目錄。 預設位置為C:\Program Files (x86)\Adobe Experience Manager Forms Workbench。

請確定您使用憑證中指定的名稱來連線到HTTPS。 此名稱通常是完整的主機名稱。

**更新cacert檔案的方式**：
1. 確保您有安全通訊端層(SSL)憑證的復本。 請連絡設定SSL伺服器的管理員，或使用網頁瀏覽器匯出憑證。

   >[!NOTE]
   若要匯出憑證，請開啟網頁瀏覽器並登入管理主控台，在瀏覽器中安裝憑證，然後從瀏覽器將憑證匯出至暫存位置(或直接匯出至 [Workbench_HOME]/workbench/jre/lib/security directory)。

1. 將憑證複製到 [Workbench_HOME]/workbench/jre/lib/security目錄。

1. 開啟命令提示字元視窗，瀏覽至 [Workbench_HOME]/workbench/jre/bin，然後輸入以下命令：
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`其中：
   * `changeit` 是cacerts金鑰存放區的預設密碼。
   * certname是您在步驟1中選取的憑證。
   * 範例是您為憑證選擇的別名。 此值可以變更。

1. 當提示信任憑證時，鍵入Yes並按Enter鍵。 Keytool會繼續將快取記憶體檔案匯入 [Workbench_HOME]/workbench/jre/lib/security目錄。

1. 關閉並重新啟動Workbench以套用變更。

### 為動態產生的範本設定快取設定 {#configuring-cache-settings-for-dynamically-generated-templates}

如果您的應用程式透過自動更新XFA內容來即時產生唯一範本，則應考慮快取操作的以下方面。 實際上，每個交易都使用新的唯一範本。

當表單產生器或輸出搜尋或更新特定表單範本的快取專案時，它會使用數個索引鍵值來找出將存取的特定快取專案。

* **範本檔案名稱**：用作快取表單主要唯一識別碼的範本的位置和檔案名稱。
* **時間戳記**：範本檔案包含用於判斷表單上次更新時間的時間戳記。
* **範本UUID**：設計工具會在每個範本中插入表單及其版本的唯一識別碼(UUID)。 每次更新表單時，都會更新內嵌的UUID。 例如，XDP範本可能顯示下列內容：

   `<?xml version="1.0" encoding="UTF-8"?>`
   `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=https://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="https://www.xfa.org/schema/xfa-template/2.6/">`

* **演算選項**：在演算後的表單快取中，快取內容會分別儲存於每組不重複演算選項。


Forms服務會參照檔案名稱或存放庫位置接收範本，或依據記憶體中XML物件的值接收。
* **透過參考傳遞的範本**：使用內容根和表單名稱。 如果使用此方法傳遞每個請求中具有不同檔案名稱的不重複範本，磁碟快取會無限成長，且永遠不會重複使用。 為避免此問題，應使用相同的檔案名稱傳遞唯一範本，以確保為所有請求更新相同的快取。
* **按值傳遞的範本**：使用範本位元組，與使用inDataDoc引數的資料一併傳遞。 如果使用此方法傳遞具有不同UUID的不重複範本，磁碟快取會無限成長，且永遠不會被重複使用。 為避免發生此情況，應從所有範本中移除UUID屬性，以確保未建立範本的快取。 或者，傳遞相同的非Null UUID可讓您建立快取物件，但會確保隨著每個請求更新相同的快取。

為避免快取無限成長，請考慮以下因素，以使用新的AEM Forms API （即renderHTMLForm2和renderPDFForm2）呈現動態產生的範本。

使用新API時，範本會以檔案物件形式傳遞，在Forms服務中根據其是否被鈍化處理。

對於以UUID和內容根目錄作為快取索引鍵的鈍化檔案，請考慮以下方面：
* 系統不會為沒有UUID的被動化輸入範本建立快取。
* 如果傳遞了多個具有相同UUID和內容根的被動化輸入範本，則會覆寫相同的快取。

對於檔案名稱和內容根目錄作為快取索引鍵的非被動化檔案，請考慮以下方面：
* 對於非被動式輸入範本，快取取決於產生檔案的內容根目錄和檔案名稱。
相同的快取只會用於具有相同內容根目錄和範本檔案名稱的請求。
下列最佳實務可確保將動態產生的範本傳遞至Forms服務時，快取不會無止境地增大：
   * 在所有動態產生的範本中移除UUID或傳遞相同的UUID。
   * 從範本位元組或磁碟上的相同檔案名稱產生檔案。

### 解除安裝Workbench {#uninstalling-workbench}

使用[控制檯]中的[新增或移除程式]功能來啟動解除安裝程式。 Workbench和Designer應用程式有不同的解除安裝程式。

## 設定AEM Forms XDC編輯器 {#configuring-aem-forms-xdc-editor}

使用XDC編輯器，網路印表機管理員可以建立和修改XML Forms架構裝置組態(XDC)檔案。 XDC檔案說明印表機的功能，例如印表機語言或紙張大小與紙匣位置之間的關聯性。

在網路印表機管理員使用XDC編輯器之前，請重新定位範例XDC檔案，並參閱使用XDC編輯器建立裝置設定檔。

**取得範例XDC檔案的方式**：
1. 在AEM Forms伺服器上，找到XDC資料夾，位置為 [AEM Forms根目錄]\sdk\samples\Output\IVS.
1. 將此資料夾的內容複製到可從Workbench或Eclipse系統存取的目錄中。

**取得XDC編輯器說明的方式**：
1. 前往AEM Forms檔案網站。
1. 按一下 **開發** 索引標籤並導覽至使用XDC編輯器建立裝置設定檔。 下載xdc_editor_help_web.zip檔案，並按照Readme檔案中提供的指示來安裝說明檔案。
