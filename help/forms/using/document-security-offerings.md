---
title: Document Security方案
seo-title: Document security offerings
description: 瞭解AEM Document Security的各種工具和功能
seo-description: Learn about various tools and features of AEM Document Security
uuid: 24e3275c-cd44-47c0-a6a0-e4cfb1bced8a
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 91e85e86-2361-4d1d-aa73-c3cce46ab1f1
docset: aem65
feature: Document Security
exl-id: d00ae232-b018-44e5-b04b-376d4cd9c6eb
source-git-commit: 18c180a491af10b41393ad841f2fa74d02ec9cd9
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 0%

---

# Document Security方案{#document-security-offerings}

Adobe Experience Manager Forms document security可確保只有授權的使用者才能使用您的檔案。 使用Document Security，您可以安全地散發以支援格式儲存的任何資訊。 支援的檔案格式包括Adobe可攜式檔案格式(PDF)以及Microsoft Word、Excel和PowerPoint檔案。

您可以使用原則來保護檔案。 您在原則中指定的機密性設定可決定收件者如何使用您套用原則的檔案。 例如，您可以指定收件者是否可以列印或複製文字、編輯文字，或將簽名和註解新增至受保護檔案。

原則儲存在Document Security伺服器上；您可以透過使用者端應用程式將這些原則套用至檔案。 將原則套用至檔案時，原則中指定的機密性設定會保護檔案所包含的資訊。 您可以將受原則保護的檔案分發給受原則授權的收件者。

下圖顯示AEM Forms Document Security的典型架構：

![Document Security — 建議的架構](do-not-localize/document_security_architecture.png)

## Document Security使用者端 {#document-security-clients}

Document Security提供各種使用者端來保護檔案、檢視和編輯受保護的檔案，以及索引器以啟用對受保護檔案的全文搜尋。 您可以根據您的需求和使用者端功能來選擇使用者端。

Document Security Server是Document Security執行交易的中央元件，例如使用者驗證、政策的即時管理和機密性應用。 伺服器還提供原則、稽核記錄及其他相關資訊的中央存放庫。

Document Security伺服器提供網頁型介面（網頁），可建立原則、管理受原則保護的檔案，以及監控與受原則保護檔案相關聯的事件。 管理員也可以設定全域選項，例如受邀使用者的使用者驗證、稽核和傳訊，以及管理受邀的使用者帳戶。

伺服器包含在AEM Forms Document Security附加元件產品中。 您可以聯絡AEM Forms [銷售團隊](https://www.adobe.com/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&amp;s_iid=70114000002JHs3AAG) 以購買Document Security附加元件。

### Protect檔案 {#protect-documents}

AEM Forms Document Security提供多種工具來套用安全性原則。 您可以根據需求和規格選擇工具。

![document-security-offers](assets/document-security-offerings.png)

您可以使用Document Security SDK、Adobe Acrobat、Microsoft Office適用的Document Security Extension或Portable Protection Library來套用及追蹤安全性原則：

* **Document Security SDK：** SDK是功能豐富的使用者端。 您可以使用Document Security SDK來存取檔案伺服器功能、開啟受原則保護的檔案，以及開發自訂擴充功能、外掛程式或應用程式。 例如，您可以開發擴充功能以保護自訂檔案格式，或將SDK與資料遺失預防(DLP)解決方案整合。 使用Document Security SDK開發的擴充功能、應用程式和外掛程式會將檔案傳送至指定的AEM Forms伺服器，而原則會套用至伺服器。 另請注意，AEM Forms document security client SDK (CSDK)無法取消保護使用可攜式保護程式庫(PPL)保護的檔案，反之亦然。

   Document Security SDK適用於Java和C++。 Java SDK包含在AEM Forms Document Security產品中，並安裝在在JEE上部署AEM Forms時。 您可以聯絡 [AEM支援團隊](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html) 以取得C++ SDK。 C++ SDK可透過Microsoft Visual Studio 2013進行編譯。 您可以造訪 [Document Security API檔案](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) 網站以瞭解及使用SDK的功能。

* **Adobe Acrobat：** 您可以使用Adobe Acrobat將安全性原則套用至PDF使用常見案頭應用程式(例如Microsoft Office、網頁瀏覽器或任何支援PDF格式列印的應用程式)建立的檔案。

   您可以購買並下載Adobe Acrobat，網址為 [Adobe網站](https://acrobat.adobe.com/us/en/free-trial-download.html). Adobe Acrobat文章 [設定PDF的安全性原則](https://helpx.adobe.com/acrobat/using/setting-security-policies-pdfs.html) 提供有關在Adobe Acrobat中建立和套用原則的詳細資訊。

* **Microsoft Office適用的Document Security Extension**：您可以使用Microsoft Office適用的Document Security Extension，從Microsoft Office程式中將預先定義的原則套用至Microsoft Office檔案。 此擴充功能可確保只有授權人員才能使用受原則保護的Microsoft Word、Excel和PowerPoint檔案。 只有已安裝外掛程式的授權使用者才能使用受原則保護的檔案。

   Document Security Extension可作為Microsoft Office外掛程式使用。 您可以聯絡 [AEM支援團隊](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) 以取得擴充功能。 稍後您可以造訪 [Microsoft Office適用的Document Security Extension](https://helpx.adobe.com/aem-forms/aem-document-security/download-installer.html) 說明以瞭解安裝、設定和使用擴充功能。

* **可攜式保護程式庫：** Portable Protection Library (PPL)會在本機保護檔案，不會將檔案傳送至AEM Forms伺服器。 只有安全性認證和原則詳細資料會透過網路傳遞。 PPL也可讓您將原則擷取存取許可權製為僅供登入的使用者存取。 您可以根據登入AEM使用者之使用者的內容擷取原則。

   除了上述功能，Proportable Protection Library還具備Document Security SDK的所有功能。 您可以使用Document Security SDK來存取檔案伺服器功能、開啟受原則保護的檔案，以及開發自訂擴充功能、外掛程式或應用程式。 另請注意，portable protection library (PPL)無法取消保護使用AEM Forms document security client SDK (CSDK)保護的檔案，反之亦然。

   Portable Protection Library提供32位元和64位元版本的Java和C++語言。 它也可作為OSGi上AEM Forms的OSGi套件組合提供。 C++ PPL可以使用Microsoft Visual Studio 2013編譯。 如果您已獲得授權AEM Forms Document Security附加元件，您可以聯絡 [AEM Forms檔案安全性](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html) 支援團隊以取得可攜式保護程式庫。 稍後，您可以使用Portable Protection Library Help （隨附於程式庫）來設定及使用Portable Protection Library。

### 檢視或編輯受保護的檔案 {#view-or-edit-protected-documents}

* 對象 **PDF檔案**，您可以使用Adobe Acrobat DC、Acrobat Reader和Acrobat Reader Mobile檢視受保護的PDF檔案。 大部分的使用者已在裝置上安裝Acrobat Reader，因此他們不需要取得或學習其他軟體即可檢視受保護的檔案。 您也可以從下載Acrobat Reader [Acrobat Reader下載網站](https://get.adobe.com/reader/).

* 對象 **Microsoft Office檔案**，您需要使用Microsoft Office適用的Microsoft Office和AEM Forms Document Security Extension。 Document Security Extension可作為Microsoft Office外掛程式使用。 您可以從Adobe網站下載擴充功能。

### 受保護檔案索引 {#index-protected-documents}

Microsoft Windows全文檢索搜尋引擎(SharePoint Index server)和Adobe Experience Manager (AEM)可以對常用的檔案格式(例如純文字檔、Microsoft Office檔案和PDF檔案)執行全文檢索。 您可以使用Document Security索引子來啟用全文檢索搜尋引擎，以搜尋受保護的PDF檔案：

* **iFilter索引子：** 您可以使用iFilter索引子來索引受保護的PDF檔案，並啟用Microsoft Windows全文檢索搜尋引擎(案頭索引服務和SharePoint Indexserver)來搜尋受保護的PDF檔案。 如需詳細資訊，請參閱 [受保護檔案的AEM SharePoint IFilter](assets/sharepoint-ifilter-doc-security.pdf).

* **AEM Forms檔案安全性索引器：** 您可以使用AEM Forms Document Security Indexer為受保護的PDF檔案編制索引，並讓Adobe Experience Manager搜尋受保護的PDF檔案。 索引器是AEM Forms Document Security產品的一部分。 這些包含在AEM Forms on JEE安裝程式中。
