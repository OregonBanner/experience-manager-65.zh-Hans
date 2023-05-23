---
title: 安裝和設定檔案服務
seo-title: Installing and configuring document services
description: 安裝AEM Forms檔案服務，以建立、彙編、散佈、封存PDF檔案、新增數位簽名以限制對檔案的存取，以及解碼條碼Forms。
seo-description: Install AEM Forms document services to create, assemble, distribute, archive PDF documents, add digital signatures to limit access to documents, and decode barcoded forms.
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
role: Admin
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
source-git-commit: 420b7f83939aef548501b4676ddca1ec9fc2aa03
workflow-type: tm+mt
source-wordcount: '5530'
ht-degree: 2%

---


# 安裝和設定檔案服務 {#installing-and-configuring-document-services}

AEM Forms提供了一組OSGi服務來完成不同的檔案層級操作，例如，建立、彙編、散發和封存PDF檔案的服務，新增數位簽名以限制對檔案的存取以及解碼條碼Forms的服務。 AEM Forms附加元件套件包含這些服務。 這些服務統稱為檔案服務。 可用檔案服務及其主要功能的清單如下：

* **組合器服務：** 可讓您組合、重新排列和增加PDF和XDP檔案，並取得有關PDF檔案的資訊。 它還有助於將PDF檔案轉換和驗證為PDF/A標準，將PDF forms、XML表單和PDF forms轉換為PDF/A-1b、PDF/A-2b和PDFA/A-3b。 如需詳細資訊，請參閱 [組合器服務](/help/forms/using/assembler-service.md).

* **ConvertPDF服務：** 可讓您將PDF檔案轉換為PostScript或影像檔案(JPEG、JPEG2000、PNG和TIFF)。 如需詳細資訊，請參閱 [ConvertPDF服務](/help/forms/using/using-convertpdf-service.md).

* **條碼式Forms服務：** 可讓您從條碼的電子影像擷取資料。 此服務接受包含一或多個條碼作為輸入的TIFF和PDF檔案，並擷取條碼資料。 如需詳細資訊，請參閱 [條碼式Forms服務](/help/forms/using/using-barcoded-forms-service.md).

* **DocAssurance服務：** 可讓您加密和解密檔案、透過其他使用許可權來擴充Adobe Reader的功能，以及將數位簽名新增至您的檔案。 Doc Assurance服務包含三種服務：簽名、加密和讀取器延伸。 如需詳細資訊，請參閱 [DocAssurance服務](/help/forms/using/overview-aem-document-services.md).

* **加密服務：** 可讓您加密和解密檔案。 檔案加密後，其內容會變得無法讀取。 授權的使用者可以解密檔案以取得其內容的存取權。 如需詳細資訊，請參閱 [加密服務](/help/forms/using/overview-aem-document-services.md#encryption-service).

* **Forms服務：** 可讓您建立互動式資料擷取使用者端應用程式，以驗證、處理、轉換及傳遞通常在Forms Designer中建立的表單。 Forms服務會轉譯您為PDF檔案所開發的任何表單設計。 如需詳細資訊，請參閱 [Forms服務](/help/forms/using/forms-service.md).

* **輸出服務：** 可讓您建立不同格式的檔案，包括PDF、雷射印表機格式和標籤印表機格式。 雷射印表機格式為PostScript和印表機控制語言(PCL)。 如需詳細資訊，請參閱 [輸出服務](/help/forms/using/output-service.md).

* **PDF產生器服務：** PDF產生器服務提供API，將原生檔案格式轉換為PDF。 它也會將PDF轉換為其他檔案格式，並最佳化PDF檔案的大小。 如需詳細資訊，請參閱 [PDF產生器服務](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Reader擴充功能服務：** 透過擴充具有額外使用許可權的Adobe Reader功能，讓您的組織輕鬆共用互動式PDF檔案。 此服務會啟動使用Adobe Reader開啟PDF檔案時無法使用的功能，例如新增註釋至檔案、填寫表單和儲存檔案。 如需詳細資訊，請參閱 [Reader延伸服務](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **簽章服務：** 可讓您在AEM伺服器上處理數位簽名和檔案。 例如，簽章服務通常用於下列情況：

   * AEM伺服器會在表單傳送給使用者以使用Acrobat或Adobe Reader開啟之前驗證表單。
   * AEM伺服器會使用Acrobat或Adobe Reader驗證已新增至表單的簽名。
   * AEM伺服器代表公證人簽署表格。

   簽章服務會存取儲存在信任存放區中的憑證和認證。 如需詳細資訊，請參閱 [簽章服務](/help/forms/using/aem-document-services-programmatically.md).

AEM Forms是功能強大的企業級平台，而document services只是AEM Forms的其中一項功能。 如需完整的功能清單，請參閱 [AEM Forms簡介](/help/forms/using/introduction-aem-forms.md).

## 部署拓撲 {#deployment-topology}

AEM Forms附加元件套件是部署至AEM的應用程式。 一般而言，您只需要一個AEM例項（製作或發佈）即可執行AEM Forms檔案服務。 建議使用下列拓撲來執行AEM Forms檔案服務。 如需有關拓撲的詳細資訊，請參閱 [AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md).

![AEM Forms的架構和部署拓撲](do-not-localize/document-services.png)

>[!NOTE]
>
>雖然AEM Forms可讓您從單一伺服器設定並執行所有功能，但您應執行容量規劃、負載平衡，並為生產環境中的特定功能設定專用伺服器。 例如，若環境使用PDF產生器服務每天轉換數千頁頁面，並使用多個調適型表單來擷取資料，請為PDF產生器服務和調適型表單功能設定個別的AEM Forms伺服器。 它有助於提供最佳效能，並獨立擴充伺服器。

## 系统要求 {#system-requirements}

開始安裝及設定AEM Forms檔案服務前，請確定：

* 硬體與軟體基礎架構已準備就緒。 如需支援的硬體和軟體詳細清單，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md).

* AEM執行個體的安裝路徑未包含空格。
* AEM執行個體已啟動且正在執行。 在AEM術語中，「例項」是在伺服器上以製作或發佈模式執行的AEM的副本。 一般而言，您只需要一個AEM例項（製作或發佈）即可執行AEM Forms檔案服務：

   * **作者**：AEM執行個體，用來建立、上傳和編輯內容以及管理網站。 一旦內容準備好上線，就會將其復寫到發佈執行個體。
   * **發佈**：透過網際網路或內部網路，向公眾提供已發佈內容的AEM例項。

* 符合記憶體需求。 AEM Forms附加元件套件需要：

   * 15 GB的暫存空間，適用於Microsoft® Windows安裝。
   * UNIX安裝需要6 GB的暫存空間。

* 已安裝在Microsoft®Windows和Linux®上執行PDF產生器轉換所需的使用者端軟體：

   * **Microsoft® Windows**：安裝 [Microsoft® Office](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p) 或 [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux®**：安裝 [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* 在Microsoft® Windows上，PDF產生器支援WebKit、Acrobat WebCapture和PhantomJS轉換路由，以將HTML檔案轉換為PDF檔案。
>* 在UNIX作業系統上，PDF產生器支援WebKit和PhantomJS轉換路由，將HTML檔案轉換為PDF檔案。
>


### UNIX作業系統的額外需求 {#extrarequirements}

如果您使用UNIX作業系統，請從個別作業系統的安裝媒體安裝下列32位元套件：
<table>
 <tbody>
  <tr>
   <td>
    <ul>
     <li>外傳</li>
    </ul> </td>
   <td>
    <ul>
     <li>libxcb</li>
    </ul> </td>
   <td>
    <ul>
     <li>自由文字</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXau</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libSM</li>
    </ul> </td>
   <td>
    <ul>
     <li>zlib</li>
    </ul> </td>
   <td>
    <ul>
     <li>libICE</li>
    </ul> </td>
   <td>
    <ul>
     <li>libuuid</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>glibc</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXext</li>
    </ul> </td>
   <td>
    <ul>
     <li>nss-softokn-freebl</li>
    </ul> </td>
   <td>
    <ul>
     <li>fontconfig</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libX11</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrender</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrandr</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXinerama</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

* **(僅限PDF產生器**)安裝32位元版本的libcurl、libcrypto和libssl程式庫，並建立下列symlink。 符號連結指向個別程式庫的最新版本：

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(僅限PDF產生器)** PDF產生器服務支援WebKit和PhantomJS路由，以將HTML檔案轉換為PDF檔案。 若要啟用PhantomJS路由的轉換，請安裝下列列出的64位元程式庫。 一般來說，這些程式庫已經安裝。 如果缺少任何程式庫，請手動安裝：

   * linux-gate.so.1
   * libz.so.1
   * libfontconfig.so.1
   * libfreetype.so.6
   * libdl.so.2
   * librt.so.1
   * libpthread.so.0
   * libstdc++.so.6
   * libm.so.6
   * libgcc_s.so.1
   * libc.so.6
   * ld-linux.so.2
   * libexpat.so.1

## 安裝前設定 {#preinstallationconfigurations}

安裝前組態區段中列出的組態僅適用於PDF產生器服務。 如果您未設定PDF產生器服務，可以略過安裝前設定區段。

### 安裝Adobe Acrobat和第三方應用程式 {#install-adobe-acrobat-and-third-party-applications}

如果您要使用PDF產生器服務將原生檔案格式(例如Microsoft® Word、Microsoft®Excel、Microsoft®PowerPoint、OpenOffice、WordPerfect X7和Adobe Acrobat)轉換為PDF檔案，請確定這些應用程式已安裝在AEM Forms伺服器上。

>[!NOTE]
>
>* 如果您的AEM Forms伺服器處於離線或安全的環境，且無法透過網際網路啟動Adobe Acrobat，請參閱 [離線啟用](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en) 以取得啟用此類Adobe Acrobat例項的指示。
>* Adobe Acrobat、Microsoft®Word、Excel和Powerpoint僅適用於Microsoft® Windows。 如果您使用UNIX作業系統，請安裝OpenOffice，將RTF文字檔和支援的Microsoft® Office檔案轉換為PDF檔案。
>* 為所有設定要使用PDF產生器服務的使用者關閉安裝Adobe Acrobat和協力廠商軟體後顯示的所有對話方塊。
>* 至少啟動一次所有已安裝的軟體。 關閉所有設定為使用PDF產生器服務之使用者的所有對話方塊。
>* [檢查Adobe Acrobat序號的到期日](https://helpx.adobe.com/enterprise/kb/volume-license-expiration-check.html) 並設定更新授權的日期，或 [移轉您的序號](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) 根據到期日。


安裝Acrobat後，請開啟Microsoft® Word。 於 **Acrobat** 標籤，按一下 **建立PDF** 並將電腦上可用的.doc或.docx檔案轉換為PDF檔案。 如果轉換成功，AEM Forms即可搭配PDF產生器服務使用Acrobat。

### 設定環境變數 {#setup-environment-variables}

設定32位元和64位元Java Development Kit、協力廠商應用程式和Adobe Acrobat的環境變數。 環境變數應包含用來啟動對應應用程式的可執行檔的絕對路徑，例如，下表列出一些應用程式的環境變數：

<table>
 <tbody>
  <tr>
   <td><p><strong>应用程序</strong></p> </td>
   <td><p><strong>環境變數</strong></p> </td>
   <td><p><strong>示例</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>JDK （64位元）</strong></p> </td>
   <td><p>JAVA_HOME</p> </td>
   <td><p>C:\Program Files\Java\jdk1.8.0_74</p> </td>
  </tr>
  <tr>
   <td><p><strong>Adobe Acrobat</strong></p> </td>
   <td><p>Acrobat_PATH</p> </td>
   <td><p>C:\Program檔案(x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td>
  </tr>
  <tr>
   <td><p><strong>筆記本</strong></p> </td>
   <td><p>Notepad_PATH</p> </td>
   <td><p>C:\WINDOWS\notepad.exe<br /> <strong></strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>OpenOffice</strong></p> </td>
   <td><p>OpenOffice_PATH</p> </td>
   <td><p>C:\Program檔案(x86)\OpenOffice.org4</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 所有環境變數和各自的路徑都會區分大小寫。
>* JAVA_HOME、JAVA_HOME_32和Acrobat_PATH （僅限Windows）是強制環境變數。
>* 環境變數OpenOffice_PATH設定為安裝資料夾，而不是可執行檔的路徑。
>* 請勿為Microsoft® Office應用程式（例如Word、PowerPoint、Excel和Project）或AutoCAD設定環境變數。 如果這些應用程式安裝在伺服器上，則產生PDF服務會自動啟動這些應用程式。
>* 在UNIX平台上，以/root安裝OpenOffice。 如果OpenOffice未安裝為root，則PDF產生器服務無法將OpenOffice檔案轉換為PDF檔案。 如果您需要以非root使用者的身分安裝及執行OpenOffice，請為非root使用者提供sudo許可權。
>* 如果您在以UNIX為基礎的平台上使用OpenOffice，請執行以下命令來設定路徑變數：
>
>  `export OpenOffice_PATH=/opt/openoffice.org4`

### (僅適用於IBM® WebSphere®)設定IBM® SSL通訊端提供者 {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

執行以下步驟來設定IBM® SSL通訊端提供者：

1. 建立java.security檔案的復本。 檔案的預設位置為 `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. 開啟複製的java.security檔案以進行編輯。
1. 變更預設的SSL通訊端工廠以使用JSSE2工廠，而非預設的IBM® WebSphere®工廠：

   **預設內容：**

   ```shell
   #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   #WebSphere socket factories (in cryptosf.jar)
   ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

   **修改的內容：**

   ```shell
   ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   
   #WebSphere socket factories (in cryptosf.jar)
   #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

1. 若要讓AEM Forms伺服器使用更新後的java.security檔案，請在啟動AEM Forms伺服器時新增下列java引數：

   `-Djava.security.properties= [path of newly created Java.security file].`

### （僅限Windows）設定Microsoft® Office的檔案封鎖設定 {#configure-the-file-block-settings-for-microsoft-office}

變更Microsoft® Office信任中心設定，以啟用PDF產生器服務，轉換使用舊版Microsoft® Office建立的檔案。

1. 開啟Microsoft® Office應用程式。 例如，Microsoft® Word。 導覽至 **[!UICONTROL 檔案]**> **[!UICONTROL 選項]**. 「選項」對話方塊隨即顯示。

1. 按一下 **[!UICONTROL 信任中心]**，然後按一下 **[!UICONTROL 信任中心設定]**.
1. 在 **[!UICONTROL 信任中心設定]**，按一下 **[!UICONTROL 檔案區塊設定]**.
1. 在 **[!UICONTROL 檔案型別]** 清單，取消選取 **[!UICONTROL 開啟]** 應允許PDF產生器服務轉換為PDF檔案的檔案型別。

### （僅限Windows）授予Replace a process level token許可權 {#grant-the-replace-a-process-level-token-privilege}

用來啟動應用程式伺服器的使用者帳戶需要 **取代程式層級權杖** 許可權。 本機系統帳戶具有 **取代程式層級權杖** 預設許可權。 對於以Local Administrators群組的使用者執行的伺服器，必須明確授與許可權。 執行以下步驟來授與許可權：

1. 開啟Microsoft® Windows的群組原則編輯器。 若要開啟群組原則編輯器，請按一下 **[!UICONTROL 開始]**，型別 **gpedit.msc** ，然後按一下 **[!UICONTROL 群組原則編輯器]**.
1. 導覽至 **[!UICONTROL 本機電腦原則]** > **[!UICONTROL 電腦設定]** > **[!UICONTROL Windows設定]** > **[!UICONTROL 安全性設定]** > **[!UICONTROL 本機原則]** > **[!UICONTROL 使用者許可權指派]** 並編輯 **[!UICONTROL 取代程式層級權杖]** 原則並包含管理員群組。
1. 將使用者新增至「取代程式層級權杖」專案。

### （僅限Windows）為非管理員啟用PDF產生器服務 {#enable-the-pdf-generator-service-for-non-administrators}

您可以讓非管理員使用者使用PDF產生器服務。 通常只有具有管理許可權的使用者才能使用服務：

1. 建立環境變數PDFG_NON_ADMIN_ENABLED。
1. 將環境變數的值設定為TRUE。
1. 重新啟動AEM Forms執行個體。

### （僅限Windows）停用使用者帳戶控制(UAC) {#disable-user-account-control-uac}

1. 若要存取系統組態公用程式，請前往 **[!UICONTROL 開始>執行]** 然後輸入 **[!UICONTROL MSCONFIG]**.
1. 按一下 **[!UICONTROL 工具]** Tab鍵並向下捲動並選取 **[!UICONTROL 變更UAC設定]**. 按一下 **[!UICONTROL Launch]** 在新視窗中執行指令。
1. 將滑桿調整至永不通知層級。 完成後，關閉命令視窗並關閉「系統組態」視窗。
1. 確認UAC的登入設定設為0 （零）。 執行以下步驟以進行驗證：

   1. Microsoft®建議您在修改登入之前先備份登入。 如需詳細步驟，請參閱 [如何在Windows中備份及還原登入](https://support.microsoft.com/en-us/help/322756).
   1. 開啟Microsoft® Windows登入編輯器。 若要開啟登入編輯程式，請前往「開始>執行」，輸入regedit，然後按一下「確定」。
   1. 导航到 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`。請確定EnableLUA的值設為0 （零）。
   1. 確保值 **EnableLUA** 設為0 （零）。 如果值不是0，請將值變更為0。 关闭注册表编辑器。

1. 重新啟動電腦。

### （僅限Windows）停用錯誤報告服務 {#disable-error-reporting-service}

在Windows Server上使用PDF產生器服務將檔案轉換為PDF時，Windows Server偶爾會報告可執行檔遇到問題且必須關閉。 但是，它不會影響PDF轉換，因為它會在背景中繼續。

若要避免收到錯誤，您可以停用Windows錯誤報告。 如需停用錯誤報告的詳細資訊，請參閱 [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### （僅限Windows）設定HTML以PDF轉換 {#configure-html-to-pdf-conversion}

PDF產生器服務提供將HTML檔案轉換為PDF檔案的WebKit、WebCapture和PhantomJS路由或方法。 在Windows上，若要啟用WebKit和Acrobat WebCapture路由的轉換，請將Unicode字型複製到%windir%\fonts目錄。

>[!NOTE]
>
>每當您將新字型安裝至字型資料夾時，請重新啟動AEM Forms例項。

### （僅限UNIX平台）額外的HTML至PDF轉換設定  {#extra-configurations-for-html-to-pdf-conversion}

在UNIX平台上，PDF產生器服務支援WebKit和PhantomJS路由，將HTML檔案轉換為PDF檔案。 若要啟用HTML至PDF轉換，請執行以下適用於您偏好的轉換路由的設定：

### （僅限UNIX平台）啟用Unicode字型支援（僅限WebKit） {#enable-support-for-unicode-fonts-webkit-only}

根據您的系統將Unicode字型複製到下列任何目錄：

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType (Solaris™)

>[!NOTE]
>
>* 在Red Hat® Enterprise Linux® 6.x和更新版本上，Courier字型無法使用。 若要安裝Courier字型，請下載font-ibm-type1-1.0.3.zip封存。 在/usr/share/fonts解壓縮封存。 從/usr/share/X11/fonts建立符號連結至/usr/share/fonts。
>* 刪除Html2PdfSvc/bin和/usr/share/fonts目錄中的所有.lst字型快取檔案。
>* 確定目錄/usr/lib/X11/fonts和/usr/share/fonts存在。 如果目錄不存在，則使用ln命令建立從/usr/share/X11/fonts到/usr/lib/X11/fonts的符號連結，以及從/usr/share/fonts到/usr/share/X11/fonts的另一個符號連結。 也請確定在/usr/lib/X11/fonts中可以使用快遞。
>* 請確定/usr/share/fonts或/usr/share/X11/fonts目錄中的所有字型（Unicode和非Unicode）都可用。
>* 當您以非根使用者身分執行PDF產生器服務時，請為非根使用者提供所有字型目錄的讀寫存取權。
>* 每當您將新字型安裝至字型資料夾時，請重新啟動AEM Forms例項。
>


## 安裝AEM Forms附加元件套件 {#install-aem-forms-add-on-package}

AEM Forms附加元件套件是部署至AEM的應用程式。 此套件包含AEM Forms Document Services和其他AEM Forms功能。 執行以下步驟來安裝套裝軟體：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 區段：
   1. 選取 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 下拉式清單。
   2. 選取套件的版本和型別。 您也可以使用 **[!UICONTROL 搜尋下載]** 篩選結果的選項。
1. 點選適用於您的作業系統的套件名稱，然後選取 **[!UICONTROL 接受EULA條款]**，然後點選 **[!UICONTROL 下載]**.
1. 打开[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 選取套件並按一下 **[!UICONTROL 安裝]**.

   您也可以透過下列連結下載套件： [AEM Forms發行版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 文章。

1. 安裝套件後，系統會提示您重新啟動AEM執行個體。 **請勿立即停止伺服器。** 在停止AEM Forms伺服器之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在 `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log檔案且記錄穩定。

## 安裝後設定 {#post-installation-configurations}

### 設定RSA/BouncyCastle程式庫的開機委派  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. 停止AEM執行個體。 導覽至 [AEM安裝目錄]\crx-quickstart\conf\資料夾。 開啟sling.properties檔案以進行編輯。

   如果您使用 `[AEM installation directory]\crx-quickstart\bin\start.bat` 若要啟動AEM執行個體，請編輯位於的sling.properties `[AEM_root]\crx-quickstart\`.

1. 將下列屬性新增至sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. (僅限AIX®)將以下屬性新增到sling.properties檔案：

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. 儲存並關閉檔案。

### 設定Font Manager服務  {#configuring-the-font-manager-service}

1. 登入 [AEM Configuration Manager](http://localhost:4502/system/console/configMgr) 作為管理員。
1. 找到並開啟 **[!UICONTROL CQ-DAM-Handler-Gibson字型管理員]** 服務。 指定System Fonts、System Server Fonts和Customer Fonts目錄的Adobe。 单击“**[!UICONTROL 保存]**”。

   >[!NOTE]
   >
   >您使用Adobe以外各方所提供字型的權利受這些各方所提供之授權合約所規範，且不受您使用Adobe軟體的授權所涵蓋。 Adobe建議您先檢閱並確保符合所有適用的非Adobe授權合約，然後再搭配Adobe軟體使用非Adobe字型，尤其是有關在伺服器環境中使用字型的問題。
   >將新字型安裝至字型資料夾時，請重新啟動AEM Forms例項。

### 設定本機使用者帳戶以執行PDF產生器服務  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

需要本機使用者帳戶才能執行PDF產生器服務。 如需建立本機使用者的步驟，請參閱 [在Windows中建立使用者帳戶](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) 或在UNIX平台中建立使用者帳戶。

1. 開啟 [AEM FormsPDF產生器設定](http://localhost:4502/libs/fd/pdfg/config/ui.html) 頁面。

1. 在 **[!UICONTROL 使用者帳戶]** 標籤，提供本機使用者帳戶的認證，然後按一下 **[!UICONTROL 提交]**. 如果Microsoft® Windows提示，請允許使用者存取。 成功新增後，設定的使用者會顯示在 **[!UICONTROL 您的使用者帳戶]** 中的區段 **[!UICONTROL 使用者帳戶]** 標籤。

### 設定逾時設定 {#configure-the-time-out-settings}

1. 在 [AEM設定管理員](http://localhost:4502/system/console/configMgr)，找到並開啟 **[!UICONTROL Jacorb ORB提供者]** 服務。

   將下列專案新增至 **[!UICONTROL 自訂屬性.name]** 欄位並按一下 **[!UICONTROL 儲存]**. 它會將擱置中的回覆逾時（也稱為CORBA使用者端逾時）設定為600秒。

   `jacorb.connection.client.pending_reply_timeout=600000`

1. 登入AEM編寫執行個體並導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 設定PDF產生器]**. 預設URL為 <http://localhost:4502/libs/fd/pdfg/config/ui.html>.

   開啟 **[!UICONTROL 一般設定]** 標籤並修改下列欄位對您環境的值：

<table>
 <tbody>
  <tr>
   <td>字段</td>
   <td>描述</td>
   <td>默认值</td>
  </tr>
  <tr>
   <td>服务器转换超时</td>
   <td>PDFG轉換會在伺服器轉換逾時中定義的秒數內保持作用中</td>
   <td>270秒<br /> </td>
  </tr>
  <tr>
   <td>PDFG 清理扫描秒数</td>
   <td>執行轉換後作業所需的秒數。<br /> </td>
   <td>3600 秒</td>
  </tr>
  <tr>
   <td>作业盗取秒数</td>
   <td>允許PDF產生器服務執行轉換的持續時間。 請確定作業過期秒數的值大於PDFG清除掃描秒數的值。</td>
   <td>7200 秒</td>
  </tr>
 </tbody>
</table>

### （僅限Windows）為PDF產生器服務設定Acrobat {#configure-acrobat-for-the-pdf-generator-service}

在Microsoft® Windows上，PDF產生器服務會使用Adobe Acrobat將支援的檔案格式轉換為PDF檔案。 執行以下步驟，為PDF產生器服務設定Adobe Acrobat：

1. 開啟Acrobat並選取 **[!UICONTROL 編輯]**> **[!UICONTROL 偏好設定]**> **[!UICONTROL 更新程式]**. 在檢查更新中，取消選取 **[!UICONTROL 自動安裝更新]**，然後按一下 **[!UICONTROL 確定]**. 關閉Acrobat。
1. 連按兩下您系統上的PDF檔案。 當Acrobat首次啟動時，會出現登入、歡迎畫面和EULA的對話方塊。 為所有設定為使用PDF產生器的使用者關閉這些對話方塊。
1. 執行PDF產生器公用程式批次檔案，為PDF產生器服務設定Acrobat：

   1. 開啟 [AEM封裝管理員](http://localhost:4502/crx/packmgr/index.jsp) 並下載 `adobe-aemfd-pdfg-common-pkg-[version].zip` 封裝管理員中的檔案。
   1. 將下載的.zip檔案解壓縮。 以管理許可權開啟命令提示字元。
   1. 導覽至 `[extracted-zip-file]\jcr_root\etc\packages\day\cq60\fd\adobe-aemds-common-pkg-[version]\jcr_root\etc\packages\day\cq60\fd\`
   1. 解壓縮 `adobe-aemfd-pdfg-common-pkg-[version]`.
   1. 導覽至 `[downloaded-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]` 目錄。 執行以下批次檔案：

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat已設定為搭配PDF產生器服務執行。

1. 執行 [系統整備工具(SRT)](#SRT) 驗證Acrobat安裝。

### （僅限Windows）設定HTML至PDF轉換的主要路由 {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

PDF產生器服務提供將HTML檔案轉換為PDF檔案的多種途徑：Webkit、Acrobat WebCapture （僅限Windows）和PhantomJS。 Adobe建議使用PhantomJS路由，因為它有能力處理動態內容，並且不依賴32位元程式庫、32位元JDK，或不需要額外字型。 此外，PhantomJS路由不需要sudo或root存取權即可執行轉換。

HTML至PDF轉換的預設主要路徑為Webkit。 若要變更轉換路線，請執行下列動作：

1. 在AEM作者執行個體上，導覽至 **[!UICONTROL 工具]**> **[!UICONTROL Forms]**> **[!UICONTROL 設定PDF產生器]**.

1. 在 **[!UICONTROL 一般設定]** 索引標籤中，選取偏好的轉換路線 **[!UICONTROL HTML至PDF轉換的主要路線]** 下拉式清單。

### 初始化全域信任存放區 {#intialize-global-trust-store}

使用「信任存放區管理」，您可以匯入、編輯和刪除您信任在伺服器上的憑證，以驗證數位簽名和憑證驗證。 您可以匯入和匯出任意數量的憑證。 匯入憑證後，您可以編輯信任設定和信任存放區型別。 執行以下步驟來初始化信任存放區：

1. 以管理員身分登入AEM Forms執行個體。
1. 前往  **[!UICONTROL 工具]** >  **[!UICONTROL 安全性]** >  **[!UICONTROL 信任存放區]**.
1. 按一下  **[!UICONTROL 建立信任存放區]**. 設定密碼並點選 **[!UICONTROL 儲存]**.

### 設定Reader延伸與加密服務的憑證 {#set-up-certificates-for-reader-extension-and-encryption-service}

DocAssurance服務可套用使用許可權至PDF檔案。 若要套用使用許可權至PDF檔案，請設定憑證。

在設定憑證之前，請確定您擁有：

* 憑證檔案(.pfx)。

* 憑證隨附的私密金鑰密碼。

* 私钥别名. 您可以執行Java keytool指令來檢視「私密金鑰別名」：
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* 金鑰存放區檔案密碼。 如果您使用Adobe的Reader延伸憑證，Keystore檔案密碼一律與私密金鑰密碼相同。

執行以下步驟來設定憑證：

1. 以管理員身分登入AEM作者執行個體。 前往 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**.
1. 按一下 **[!UICONTROL 名稱]** 使用者帳戶的欄位。 此 **[!UICONTROL 編輯使用者設定]** 頁面隨即開啟。 在AEM Author執行個體上，憑證位於KeyStore中。 如果您先前尚未建立KeyStore，請按一下 **[!UICONTROL 建立KeyStore]** 並設定KeyStore的新密碼。 如果伺服器已包含KeyStore，請略過此步驟。  如果您使用Adobe的Reader延伸憑證，Keystore檔案密碼一律與私密金鑰密碼相同。
1. 於 **[!UICONTROL 編輯使用者設定]** 頁面，選取 **[!UICONTROL 金鑰存放區]** 標籤。 展開 **[!UICONTROL 從金鑰庫檔案新增私密金鑰]** 選項並提供別名。 別名可用來執行Reader擴充功能作業。
1. 若要上傳憑證檔案，請按一下 **[!UICONTROL 選取金鑰庫檔案]** 並上傳 &lt;filename>.pfx檔案。

   新增 **[!UICONTROL 金鑰庫密碼]**， **[!UICONTROL 私密金鑰密碼]**、和 **[!UICONTROL 私密金鑰別名]** 與對應欄位之憑證相關聯的內容區段。 按一下 **[!UICONTROL 提交]**.

   >[!NOTE]
   >
   >在生產環境中，將評估認證替換為生產認證。 在更新過期的認證或評估認證之前，請務必刪除舊的Reader擴充功能認證。

1. 按一下 **[!UICONTROL 儲存並關閉]** 於 **[!UICONTROL 編輯使用者設定]** 頁面。

### 啟用AES-256 {#enable-aes}

若要對PDF檔案使用AES 256加密，請取得並安裝Java Cryptography Extension (JCE) Unlimited Strength Jurishment Policy檔案。 取代jre/lib/security資料夾中的local_policy.jar和US_export_policy.jar檔案。 例如，如果您使用Sun JDK，請將下載的檔案複製到 `[JAVA_HOME]/jre/lib/security` 資料夾。

Assembler服務取決於Reader擴充功能服務、簽名服務、Forms服務和輸出服務。 執行以下步驟，確認必要的服務已啟動且正在執行：

1. 登入URL `https://'[server]:[port]'/system/console/bundles` 作為管理員。
1. 搜尋下列服務，並確定服務已啟動且正在執行：

<table>
 <tbody>
  <tr>
   <th>服务名称</th>
   <th>包名称</th>
  </tr>
  <tr>
   <td>签名服务</td>
   <td>adobe-aemfd-signatures</td>
  </tr>
  <tr>
   <td>Reader 扩展服务</td>
   <td>com.adobe.aemfd.adobe-aemfd-readerextensions<br /> </td>
  </tr>
  <tr>
   <td>表单服务</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector<br /> </td>
  </tr>
  <tr>
   <td>输出服务</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector</td>
  </tr>
 </tbody>
</table>

## 已知問題和疑難排解 {#known-issues-and-troubleshooting}

* 如果壓縮的輸入檔案包含檔案名稱中含有雙位元組字元的HTML檔案，則PDF轉換的HTML會失敗。 為避免此問題，命名HTML檔案時請勿使用雙位元組字元。

* 在基於UNIX的作業系統上，執行下列操作來尋找任何遺漏的程式庫：

1. 导航到 `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`。

1. 執行以下命令，列出PhantomJS需要HTML到PDF轉換的所有程式庫。

   `ldd phantomjs`

   執行以下命令以列出遺失的程式庫。

   `ldd phantomjs | grep not`

1. 手動安裝遺失的程式庫。

## 系統整備工具(SRT) {#SRT}

此 [系統整備工具](#srt-configuration) 檢查電腦是否已正確設定為執行PDF產生器轉換。 工具會在指定的路徑產生報表。 若要執行工具：

1. 開啟命令提示。 導覽至 `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools` 資料夾。

1. 從命令提示字元執行下列命令：

   `java -jar forms-srt-[version].jar [Path_of_reports_folder] en`

   該命令會產生報告，也會建立srt_config.yaml檔案。 您可以使用它來設定SRT工具的選項。 可選擇性設定SRT工具的選項。

   >[!NOTE]
   >
   >* 如果「系統整備工具」報告指出pdfgen.api檔案在Acrobat外掛程式資料夾中無法使用，請從 `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]\plugins\x86_win32` 目錄到 `[Acrobat_root]\Acrobat\plug_ins` 目錄。


1. 导航到 `[Path_of_reports_folder]`。開啟SystemReadinessTool.html檔案。 驗證報告並修正上述問題。

### 設定SRT工具的選項 {#srt-configuration}

您可以使用srt_config.yaml檔案來設定SRT工具的各種設定。 檔案的格式為：

```shell
   # =================================================================
   # SRT Configuration
   # =================================================================
   #Note - follow correct format to avoid parsing failures
   #e.g. <param name>:<space><param value> 
   #locale: (mandatory field)Locale to be used for SRT. Supported locales [en/fr/de/ja].
   locale: en
   
   #aemTempDir: AEM Temp direcotry
   aemTempDir:
   
   #users: provide PDFG converting users list
   #users:
   # - user1
   # - user2
   users:
   
   #profile: select profile to run specific checks. Choose from [LCM], more will be added soon 
   profile:
   
   #outputDir: directory where output files will be saved
   outputDir:
```

* **地區設定：** 此為必要引數。 它支援英文(en)、德文(de)、法文(fr)和日文(ja)。 預設值為en。 對於在OSGi上的AEM Forms上執行的PDF產生器服務沒有影響。
* **aemTempDir：** 此為選用引數。 它會指定Adobe Experience Manager的暫存位置。
* **使用者：** 此為選用引數。 您可以指定使用者來檢查使用者是否具有執行PDF產生器所需的目錄許可權和讀取/寫入存取權。 如果未指定使用者，則會略過使用者特定檢查，並在報表中顯示為失敗。
* **outputdir：** 指定儲存SRT報表的位置。 預設位置是SRT工具的目前工作目錄。

## 疑难解答

如果在修復SRT工具報告的所有問題後仍遇到問題，請執行以下檢查：

執行以下檢查之前，請確定 [系統整備工具](#SRT) 不會回報任何錯誤。

+++ Adobe Acrobat

* 僅確認 [支援的版本](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) 已安裝Microsoft® Office （32位元）和Adobe Acrobat，且已取消開啟對話方塊。
* 請確定Adobe Acrobat更新服務已停用。
* 確保 [Acrobat_for_PDFG_Configuration.bat](#configure-acrobat-for-the-pdf-generator-service) 批次檔案是以管理員許可權執行。
* 確認已在PDF設定UI中新增PDF產生器使用者。
* 確保 [取代程式層級權杖](#grant-the-replace-a-process-level-token-privilege) 已為PDF產生器使用者新增許可權。
* 確認已為Microsoft Office應用程式啟用Acrobat PDFMaker Office COM增益集。

+++

+++OpenOffice

**Microsoft® Windows**

* 請確定32位元 [支援的版本 ](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) 已安裝Microsoft Office，且已取消開啟所有應用程式的對話方塊。
* 確認已在PDF設定UI中新增PDF產生器使用者。
* 確保PDF產生器使用者是管理員群組的成員，並且 [取代程式層級權杖](#grant-the-replace-a-process-level-token-privilege) 已為使用者設定許可權。
* 確定已在PDF產生器UI中設定使用者，並執行下列動作：
   1. 使用PDF產生器使用者登入Microsoft® Windows。
   1. 開啟Microsoft® Office或OpenOffice應用程式並取消所有對話方塊。
   1. 將AdobePDF設為預設印表機。
   1. 將Acrobat設為PDF檔案的預設程式。
   1. 使用Microsoft Office應用程式中的選項「檔案>列印」和Acrobat功能區來執行手動轉換，並取消所有對話方塊。
   1. 結束與轉換相關的所有程式，例如winword.exe、powerpoint.exe和excel.exe。
   1. 重新啟動AEM Forms伺服器。

**Linux®**

* 安裝 [支援的版本](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) OpenOffice的。 AEM Forms支援32位元和64位元版本。 安裝之後，請開啟所有OpenOffice應用程式、取消所有對話視窗，然後關閉應用程式。 重新開啟應用程式，並確保開啟OpenOffice應用程式時不會顯示任何對話方塊。

* 建立環境變數 `OpenOffice_PATH` 並將它設定為指向OpenOffice安裝設定於 [主控台](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/) 或dt （裝置樹狀結構）設定檔。
* 如果安裝OpenOffice時發生問題，請確定 [32位元程式庫](#extrarequirements) 提供OpenOffice安裝的必要專案。

+++

+++HTML至PDF轉換問題

* 請確定已在PDF產生器設定UI中新增字型目錄。

**Linux和Solaris （PhantomJS轉換路由）**

* 確保可用於基於Webkit的HTMLToPDF轉換的32位元資料庫(libicudata.so.42)和可用於基於PhantomJS的HTMLToPDF轉換的64位元（libicudata.so.42資料庫）。

* 執行以下命令以列出phantomjs的缺少程式庫：

   ```
   ldd phantomjs | grep not
   ```

* 請確定JAVA_HOME_32環境變數指向正確的位置。

**Linux®和Solaris™ （WebKit轉換路由）**

* 確定目錄 `/usr/lib/X11/fonts` 和 `/usr/share/fonts` 存在。 如果目錄不存在，請從建立符號連結 `/usr/share/X11/fonts` 至 `/usr/lib/X11/fonts` 和另一個符號連結 `/usr/share/fonts` 至 `/usr/share/X11/fonts`.

   ```
   ln -s /usr/share/fonts /usr/share/X11/fonts
   
   ln -s /usr/share/X11/fonts /usr/lib/X11/fonts
   ```

* 請確定IBM字型複製於usr/share/fonts之下。
* 確定電腦上有Ghost弱點修正Glibc。 使用您的預設封裝管理員以更新至最新版本的glibc。 其中包括Ghost漏洞修正。
* 確保系統上已安裝最新版的32位元lib curl、libcrypto和libssl程式庫。 同時建立符號連結 `/usr/lib/libcurl.so` (或適用於AIX®的libcurl.a)、 `/usr/lib/libcrypto.so` (或適用於AIX®的libcrypto.a)和 `/usr/lib/libssl.so` (或libssl.a (適用於AIX®))指向個別程式庫的最新版本（32位元）。

* 針對IBM® SSL通訊端提供者執行以下步驟：
   1. 複製java.security檔案來源 `<WAS_Installed_JAVA>\jre\lib\security` 至您AEM Forms伺服器上的任何位置。 預設位置為預設位置為= `<WAS_Installed>\Appserver\java_[version]\jre\lib\security`.

   1. 編輯複製位置的java.security檔案，並變更預設的SSL通訊端工廠與JSSE2工廠(使用JSSE2工廠而非WebSphere®)。

      變更下列預設JSSE通訊端工廠：

      ```
      #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

      替换为

      ```
      ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

+++

+++ 無法新增PDF產生器(PDFG)使用者

* 請確定Windows上已安裝Microsoft® Visual C++ 2012 x86和Microsoft® Visual C++ 2013 x86 （32位元）可轉散發套件。

+++

+++自動化測試失敗

* 對於Microsoft® Office和OpenOffice，請手動執行至少一個轉換（以每位使用者的身分），以確保轉換期間不會彈出任何對話方塊。 如果出現任何對話方塊，則會將其關閉。 自動轉換期間不應出現這類對話方塊。

* 在OSGi環境的AEM Forms上執行自動化之前，請確定測試套件已安裝且作用中。

+++

+++多個使用者轉換失敗

* 驗證伺服器記錄以檢查特定使用者的轉換是否失敗。（程式總管可以幫助您檢查不同使用者的執行程式）

* 請確定為PDF產生器設定的使用者擁有本機管理員許可權。

* 確保PDF產生器使用者對LC臨時和PDFG臨時使用者具有讀取、寫入和執行許可權。

* 對於Microsoft® Office和OpenOffice，請手動執行至少一個轉換（以每位使用者的身分），以確保轉換期間不會彈出任何對話方塊。 如果出現任何對話方塊，則會將其關閉。 自動轉換期間不應出現這類對話方塊。

* 執行範例轉換。

+++

+++安裝在AEM Forms伺服器上的Adobe Acrobat授權到期

* 如果您已有Adobe Acrobat的授權，且該授權已過期， [下載最新版Adobe Application Manager](https://helpx.adobe.com/in/creative-suite/kb/aam-troubleshoot-download-install.html)，並移轉您的序號。 早於 [正在移轉您的序號](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number).

   * 使用以下命令產生prov.xml，並使用prov.xml檔案（而非中提供的命令）重新序列化現有的安裝 [正在移轉您的序號](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) 數字文章。

          ```
          
          adobe_prtk —tool=VolumeSerialize —generate —serial=&lt;serialnum> [—leid=&lt;leid>] [—regsuppress=ss] [—eulasuppress] [—locales=xx_XX格式或ALL格式的有限語言環境清單>] [—provfile=&lt;absolute path=&quot;&quot; to=&quot;&quot; prov.xml=&quot;&quot;>]
          
          ```
      
   * 磁碟區序列化套件（使用prov.xml檔案和新的序列重新序列化現有的安裝）：以管理員身分從PRTK安裝資料夾執行下列命令，序列化並啟動使用者端機器上部署的套件：

          ```
          adobe_prtk —tool=VolumeSerialize —provfile=C:\prov.xml -stream
          
          ```
      
* 若為大型安裝，請使用 [AcrobatCustomization Wizard](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/index.html) 以移除舊版Reader和Acrobat。 自訂安裝程式，並將其部署至貴組織的所有電腦。

+++

+++ AEM Forms伺服器處於離線或安全的環境中，且無法透過網際網路啟動Acrobat。

* 您可以在Adobe產品首次上市後的7天內上線，完成線上啟用和註冊，或使用具備網際網路功能的裝置和產品的序號來完成此程式。 如需詳細指示，請參閱 [離線啟用](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en).

+++

+++ 無法在Windows Server上將Word或Excel檔案轉換為PDF

當使用者嘗試在Microsoft Windows Server上將Word或Excel檔案轉換為PDF時，會遇到以下錯誤：

*來自主要轉換器的錯誤訊息：ALC-PDG-015-003 — 系統無法開啟輸入檔案。 請再次提交您的檔案或連絡您的系統管理員。*

若要解決問題，請參閱 [無法在Windows Server上將Word或Excel檔案轉換為PDF](/help/forms/using/disable-uac-for-pdfgconfiguration.md).


## 后续步骤 {#next-steps}

您有一個運作中的AEM Forms檔案服務環境。 您可以透過以下方式使用檔案服務：

* [OSGi上的表單中心工作流程](/help/forms/using/aem-forms-workflow.md)
* [观察文件夹](/help/forms/using/watched-folder-in-aem-forms.md)
* [檔案服務API](/help/forms/using/aem-document-services-programmatically.md)
