---
title: 設定使用者端和伺服器選項
seo-title: Configuring client and server optionsn
description: 瞭解如何設定各種使用者端和伺服器選項，例如伺服器組態設定、Document Security角色和事件稽核。
seo-description: Learn how you can configure the various client and server options, such as server configuration settings, document security roles, and event auditing.
uuid: 1f9f9886-726e-4fad-9ff8-0ff11eef653e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0f069fbc-10c2-403e-9419-5e9920035d75
feature: Document Security
exl-id: fe132f13-5f9a-4c86-a385-0a0026c812e2
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '10242'
ht-degree: 0%

---

# 設定Document Security伺服器 {#configure-the-document-security-server}

1. 在管理控制檯中，按一下「服務> Document Security >設定>伺服器設定」。
1. 設定設定，然後按一下「確定」。

## 伺服器組態設定 {#server-configuration-settings}

**基本URL：** 基礎Document Security URL，包含伺服器名稱和連線埠。 附加至基底的資訊會建立連線URL。 例如，會附加/edc/Main.do以存取網頁。 使用者也會透過此URL回應外部使用者註冊邀請。

如果您使用IPv6，請輸入基礎URL作為電腦名稱或DNS名稱。 如果您使用數值IP位址，Acrobat將無法開啟受原則保護的檔案。 此外，請為伺服器使用HTTP安全(HTTPS) URL。

>[!NOTE]
>
>基礎URL內嵌在受原則保護的檔案中。 使用者端應用程式會使用基本URL來連線回伺服器。 安全檔案將繼續包含基本URL，即使稍後變更亦然。 如果您變更基本URL，則需要更新所有連線使用者端的設定資訊。

**預設離線租期：** 使用者可離線使用受保護檔案的預設時間長度。 此設定會決定當您建立原則時，自動離線租期設定的初始值。 （請參閱建立和編輯原則）。 當租期到期時，收件者必須再次同步化檔案才能繼續使用。

有關離線租賃和同步化如何運作的討論，請參閱 [設定離線租賃和同步化的入門課程](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html).

**預設離線同步處理期間：** 任何檔案在最初受到保護後可離線使用的最長時間。

**使用者端工作階段逾時：** 如果透過使用者端應用程式登入的使用者沒有與Document Security互動，則Document Security中斷連線的時間長度（以分鐘為單位）。

**允許匿名使用者存取：** 選取此選項可啟用建立共用和個人原則的功能，以允許匿名使用者開啟受原則保護的檔案。 （沒有帳戶的使用者可以存取檔案，但他們無法登入Document Security或使用其他受原則保護的檔案。）

**停用對版本7使用者端的存取：** 指定使用者是否可以使用Acrobat或Reader 7.0連線至伺服器。 選取此選項時，使用者必須使用Acrobat或Reader 8.0和更新版本，才能在PDF檔案上完成檔案安全性操作。 如果原則要求Acrobat或Reader 8.0及更高版本在開啟受原則保護的檔案時必須在認證模式下執行，您應停用對Acrobat或Reader7的存取權。 （請參閱指定使用者和群組的檔案許可權。）

**允許每個檔案的離線存取** 選取此選項可指定每個檔案的離線存取。 如果啟用此設定，則使用者將只能離線存取使用者已線上上至少開啟一次的檔案。

**允許使用者名稱密碼驗證：** 選取此選項可讓使用者端應用程式在連線至伺服器時使用使用者名稱/密碼驗證。

**允許Kerberos驗證：** 選取此選項可讓使用者端應用程式在連線至伺服器時使用Kerberos驗證。

**允許使用者端憑證驗證：** 選取此選項可讓使用者端應用程式在連線至伺服器時使用憑證驗證。

**允許延伸驗證** 選取以啟用延伸驗證，然後輸入延伸驗證登陸URL。

選取此選項可讓使用者端應用程式使用延伸驗證。 延伸驗證可提供自訂的驗證程式，以及在AEM Forms伺服器上設定的不同驗證選項。 例如，使用者現在可以從Acrobat和Reader使用者端體驗以SAML為基礎的驗證，而不是AEM表單使用者名稱/密碼。 根據預設，登陸URL包含 *localhost* 作為伺服器名稱。 以完整的主機名稱取代伺服器名稱。 如果尚未啟用延伸驗證，登陸URL中的主機名稱會自動從基本URL填入。 另請參閱 [新增延伸驗證提供者](configuring-client-server-options.md#add-the-extended-authentication-provider).

***注意&#x200B;**：Apple Mac OS X搭配Adobe Acrobat 11.0.6版及更新版本支援延伸驗證。*

**延伸驗證的偏好HTML控制寬度** 指定延伸驗證對話方塊的寬度，此對話方塊會在Acrobat中開啟，用來輸入使用者認證。

**延伸驗證的偏好HTML控制高度** 指定在Acrobat中開啟用來輸入使用者認證的延伸驗證對話方塊的高度。

***注意&#x200B;**：此對話方塊的寬度和高度限制如下：*
寬度：最小值= 400，最大值= 900

高度：最小值= 450；最大值= 800

**啟用使用者端認證快取：** 選取此選項可允許使用者快取其認證（使用者名稱和密碼）。 快取使用者的認證時，使用者不必在每次開啟檔案或按一下Adobe Acrobat中「管理安全性原則」頁面上的「重新整理」按鈕時輸入認證。 您可以指定使用者必須再次提供其認證的天數。 將天數設為0，可無限期快取認證。

## 設定Document Security使用者和管理員 {#configuring-document-security-users-and-administrators}

### 指派檔案安全性角色給管理員 {#assigning-document-security-roles-to-administrators}

您的AEM表單環境包含一或多個具有適當許可權可建立使用者和群組的管理員使用者。 如果您的組織正在使用Document Security，則必須至少指派一位管理員來管理受邀和本機使用者。

管理員也必須具有管理控制檯使用者角色，才能存取管理控制檯。 (請參閱 [建立和設定角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

### 設定可見的使用者和群組 {#configuring-visible-users-and-groups}

若要在原則使用者搜尋期間檢視所選網域中的使用者與群組，超級管理員或原則集管理員必須選取網域（在「使用者管理」中建立），並將網域新增至每個原則集的可見使用者與群組清單。

可見的使用者和群組清單對原則集協調者可見，並用來限制一般使用者選擇要新增到原則的使用者或群組時，可以瀏覽的網域。 如果未執行此工作，原則集協調器將無法找到任何使用者或群組來新增至原則。 任何指定的原則集可以有一個以上的原則集協調器。

1. 使用Document Security安裝並設定AEM表單環境後，請在「使用者管理」中設定所有適當的網域。 <!-- Fix broken link (See Setting up and managing domains) -->

   ***注意&#x200B;**：建立網域必須先完成，才能建立任何原則。*

1. 在管理控制檯中，按一下「服務>檔案管理>原則」，然後按一下「原則集」標籤。
1. 選取「全域原則集」，然後按一下「可見的使用者和群組」標籤。
1. 按一下「新增網域」 ，然後視需要新增現有網域。
1. 導覽至「服務> Document Security >設定>我的原則」 ，然後按一下「可見的使用者和群組」標籤。
1. 按一下「新增網域」 ，然後視需要新增現有網域。

## 新增延伸驗證提供者 {#add-the-extended-authentication-provider}

AEM forms提供您可針對環境自訂的設定範例。 執行下列步驟：

>[!NOTE]
>
>Apple Mac OS X搭配Adobe Acrobat 11.0.6版及更新版本支援延伸驗證。

1. 取得部署該檔案的範例WAR。 請參閱適合您應用程式伺服器的安裝指南。
1. 確保表單伺服器具有完整名稱（而非IP位址）做為基礎URL，且它是HTTPS URL。 另請參閱 [伺服器組態設定](configuring-client-server-options.md#server-configuration-settings).
1. 從「伺服器組態」頁面啟用「延伸驗證」。 另請參閱 [伺服器組態設定](configuring-client-server-options.md#server-configuration-settings).
1. 在「使用者管理」設定檔中新增必要的SSO重新導向URL。 另請參閱 [新增延伸驗證的SSO重新導向URL](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication).

### 新增延伸驗證的SSO重新導向URL {#add-sso-redirect-urls-for-extended-authentication}

啟用延伸驗證後，使用者在Acrobat XI或Reader XI中開啟受原則保護的檔案時，會收到驗證對話方塊。 此對話方塊會載入您在Document Security伺服器設定上指定為延伸驗證登陸URL的HTML頁面。 另請參閱 [伺服器組態設定](configuring-client-server-options.md#server-configuration-settings).

>[!NOTE]
>
>Apple Mac OS X搭配Adobe Acrobat 11.0.6版及更新版本支援延伸驗證。

1. 在管理控制檯中，按一下「設定」>「使用者管理」>「組態」>「匯入和匯出組態檔」。
1. 按一下「匯出」 ，然後將組態檔儲存至您的磁碟。
1. 在編輯器中開啟檔案，並找到AllowedUrls節點。
1. 在 `AllowedUrls` 節點，新增下列行： `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. 儲存檔案，然後從「手動組態」頁面匯入更新的檔案：在管理控制檯中，按一下「設定」>「使用者管理」>「組態」>「匯入和匯出組態檔」。

## 設定離線安全性 {#configuring-offline-security}

document security提供離線使用受原則保護檔案的功能，而不需要透過網際網路或網路連線。 此功能需要原則允許離線存取，如所述 [指定使用者和群組的檔案許可權](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). 在離線使用具有此類原則的檔案之前，收件者必須線上上時開啟檔案，並在出現提示時按一下[是]，以啟用離線存取。 收件者可能也會被要求驗證其身分。 然後，收件者便可以在原則指定的離線租期期間離線使用檔案。

離線租期結束時，收件者必須透過線上開啟檔案，或使用Acrobat或Acrobat Reader DC擴充功能表命令來同步，以再次與Document Security同步。 (請參閱 *Acrobat說明* 或適當的 *Acrobat Reader DC擴充功能說明*.)

因為允許離線存取的檔案需要在離線儲存檔案的電腦上快取關鍵資料，所以如果未經授權的使用者可以取得關鍵資料，則檔案可能會受到危害。 為了補償這種可能性，我們提供了排程和手動金鑰變換選項，您可以設定這些選項，以防止未經授權的人使用金鑰存取檔案。

### 設定預設離線租期 {#set-a-default-offline-lease-period}

受原則保護檔案的收件者可在原則指定的天數內將檔案離線。 最初將檔案與Document Security同步化後，收件者可以離線使用檔案，直到離線租期到期為止。 當租期到期時，收件者必須將檔案上線並登入以與Document Security同步，才能繼續使用檔案。

您可以設定預設的離線租期。 任何人建立或編輯原則時，租期可以從預設值變更。

1. 在Document Security頁面上，按一下「組態」>「伺服器組態」。
1. 在「預設離線租賃期間」方塊中，輸入離線租賃期間的天數。
1. 单击确定。

### 管理關鍵變換影像 {#manage-key-rollovers}

Document Security使用加密演演算法和授權來保護檔案。 當加密檔案時，Document Security會產生並管理稱為的解密金鑰。 *DocKey* 傳遞給使用者端應用程式。 如果保護檔案的原則允許離線存取，則稱為的離線金鑰 *主體金鑰* 也會針對具有檔案離線存取權的每個使用者產生。

>[!NOTE]
>
>如果主要金鑰不存在，則Document Security會產生一個主要金鑰來保護檔案。

若要離線開啟受原則保護的檔案，使用者的電腦必須具備適當的主體金鑰。 當使用者與Document Security同步時，電腦會取得主要金鑰（線上上開啟受保護的檔案）。 如果此主體金鑰遭到破壞，使用者離線存取的任何檔案也可能遭到破壞。

減少離線檔案威脅的一種方法是避免允許離線存取特別敏感的檔案。 另一種方法是定期捲動主要金鑰。 當Document Security將金鑰捲動時，任何現有的金鑰都無法再存取受原則保護的檔案。 例如，如果犯罪者從被盜的筆記型電腦取得主要金鑰，則該金鑰無法用於存取變換後受到保護的檔案。 如果您懷疑特定主要金鑰已遭破壞，可以手動將游標移到金鑰上。

不過，您也需要注意，金鑰變換會影響所有主要金鑰，而不僅僅是一項。 它也會降低系統的擴充性，因為使用者端必須儲存更多金鑰才能進行離線存取。 預設金鑰變換頻率是20天。 建議不要將此值設定在14天以下，因為可能會阻止人員檢視離線檔案，而且系統效能可能會受到影響。

在下列範例中，Key1是兩個主要金鑰中較舊的金鑰，而Key2是較新的金鑰。 當您第一次按一下「立即變換金鑰」按鈕時，Key1會變成無效，並產生較新的有效主體金鑰(Key3)。 當使用者與Document Security同步時（通常透過線上開啟受保護的檔案的方式），他們將取得金鑰3。 但是，使用者在達到原則中指定的最大離線租期之前，不會強制與Document Security同步。 在第一次金鑰變換後，保持離線狀態的使用者仍可開啟離線檔案，包括受金鑰3保護的檔案，直到他們達到最大離線租期為止。 當您再次按一下「立即變換金鑰」按鈕時，Key2會變成無效，而會建立Key4。 在兩個金鑰變換期間保持離線狀態的使用者無法開啟受金鑰3或金鑰4保護的檔案，直到他們與Document Security同步為止。

**變更金鑰變換頻率**

為了機密性，當您使用離線檔案時，Document Security會提供自動金鑰變換選項，預設頻率期間為20天。 您可以變更變換頻率；但是，請避免將值設定在14天以下，因為可能會阻止人員檢視離線檔案，而且系統效能可能會受到影響。

1. 在Document Security頁面上，按一下「組態」>「金鑰管理」。
1. 在「索引鍵滑鼠指向效果頻率」方塊中，輸入滑鼠指向效果期間的天數。
1. 单击确定。

**手動捲動主要金鑰**

若要維護離線檔案的機密性，您可以手動將滑鼠移到主要金鑰。 您可能會發現有必要手動捲動金鑰（例如，如果有人從快取該金鑰的電腦取得該金鑰，以啟用檔案的離線存取時）而危及該金鑰。

>[!NOTE]
>
>避免經常使用手動變換，因為這會使所有主要金鑰變換，而不僅僅是一個金鑰，並且可能會暫時阻止使用者離線檢視新檔案。

使用者端電腦上先前存在的金鑰失效之前，必須經過兩次主要金鑰的捲動。 具有無效主體金鑰的使用者端電腦必須與Document Security服務重新同步以取得新的主體金鑰。

1. 在Document Security頁面上，按一下「組態」>「金鑰管理」。
1. 按一下「立即變換金鑰」，然後按一下「確定」。
1. 等候約10分鐘。 下列記錄訊息會顯示在伺服器記錄檔中： `Done RightsManagement key rollover for`*N* `principals`. 位置 *N* 是document security系統中的使用者人數。
1. 按一下「立即變換金鑰」，然後按一下「確定」。
1. 等候約10分鐘。

## 設定事件稽核和隱私設定 {#configuring-event-auditing-and-privacy-settings}

Document Security可稽核和記錄與受原則保護檔案、原則、管理員和伺服器互動相關的事件資訊。 您可以設定事件稽核，也可以指定要稽核的事件型別。 若要稽核特定檔案的事件，也必須啟用原則上的稽核選項。

啟用稽核後，您可以在「事件」頁面上檢視稽核事件的詳細資訊。 document security使用者還可以檢視與他們使用或建立的受原則保護檔案特別相關的事件。

您可以選取下列型別的事件進行稽核：

* 受原則保護的檔案事件，例如授權或未經授權的使用者嘗試開啟檔案
* 原則事件，例如建立、變更、刪除、啟用和停用原則
* 使用者事件，例如外部使用者邀請和註冊、啟用和停用的使用者帳戶、使用者密碼的變更以及設定檔更新
* AEM forms事件，例如，版本不相符、無法使用的目錄伺服器和授權提供者，以及伺服器設定變更

### 啟用或停用事件稽核 {#enable-or-disable-event-auditing}

您可以啟用和停用與伺服器、受原則保護的檔案、原則、原則集和使用者相關的事件稽核。 啟用事件稽核時，您可以選擇稽核所有可能的事件，也可以選取要稽核的特定事件。

啟用伺服器稽核時，您可以在「事件」頁面上檢視稽核的事件。

1. 在管理控制檯中，按一下「服務> Document Security >設定>稽核和隱私設定」。
1. 若要設定伺服器稽核，請在[啟用伺服器稽核]下，選取[是]或[否]。
1. 如果您選取「是」，請在每個事件類別下執行下列其中一項動作，以選取要稽核的選項：

   * 若要稽核類別中的所有事件，請選取全部。
   * 若只要稽核某些事件，請取消選取全部，然後選取您要稽核之事件旁的核取方塊。

      (請參閱 [事件稽核選項](configuring-client-server-options.md#event-auditing-options).)

1. 单击确定。

>[!NOTE]
>
>使用網頁時，請避免使用瀏覽器按鈕（例如「上一步」按鈕、「重新整理」按鈕以及「上一步」或「前進」箭頭），因為此動作可能會導致不必要的資料擷取和資料顯示問題。

### 啟用或停用隱私權通知 {#enable-or-disable-privacy-notification}

您可以啟用和停用隱私權通知訊息。 當您啟用隱私權通知時，當收件者嘗試開啟受原則保護的檔案時，會顯示一則訊息。 通知會通知使用者正在稽核檔案使用情況。 您也可以指定使用者可用於檢視您的隱私權原則頁面（如果有）的URL。

1. 在管理控制檯中，按一下「服務> Document Security >設定>稽核和隱私設定」。
1. 若要設定隱私權通知，請在「啟用隱私權通知」下方選取「是」或「否」。

   如果附加至檔案的原則允許匿名使用者存取，且「啟用隱私權通知」設定為「否」，則不會提示使用者登入，且不會顯示隱私權通知訊息。

   如果附加到檔案的原則不允許匿名使用者存取，使用者將會看到隱私權通知訊息。

1. 如果適用，請在「隱私權URL」方塊中，輸入隱私權原則頁面的URL。 如果「隱私權URL」方塊留空，則會顯示adobe.com的隱私權頁面。
1. 单击确定。

>[!NOTE]
>
>停用隱私權通知並不會停用檔案使用稽核。 透過延伸使用追蹤支援的開箱即用稽核動作和自訂動作仍可收集使用者行為資訊。

### 匯入自訂稽核事件型別 {#import-a-custom-audit-event-type}

如果您使用已啟用Document Security的應用程式，該應用程式支援其他事件的稽核，例如特定檔案型別的事件，則Adobe合作夥伴可為您提供自訂稽核事件，供您匯入至Document Security中。 只有在Adobe合作夥伴向您提供自訂事件型別時，才使用此功能。

1. 在管理控制檯中，按一下「服務> Document Security >設定>事件管理」。
1. 按一下「瀏覽」前往要匯入的XML檔案，然後按一下「匯入」。
1. 如果發現相同的事件程式碼和名稱空間組合，匯入會覆寫伺服器上現有的自訂稽核事件型別。
1. 单击确定。

### 刪除自訂稽核事件型別 {#delete-a-custom-audit-event-type}

1. 在管理控制檯中，按一下「服務> Document Security >設定>事件管理」。
1. 選取要刪除的自訂稽核事件型別旁的核取方塊，然後按一下刪除。
1. 单击确定。

### 匯出稽核事件 {#export-audit-events}

您可以將稽核事件匯出至檔案以供封存。

1. 在管理控制檯中，按一下「服務> Document Security >設定>事件管理」。
1. 視需要編輯「匯出稽核事件」下的設定。 您可以指定：

   * 要匯出的稽核事件最小年齡
   * 單一檔案中可包含的最大稽核事件數。 伺服器會根據此值產生一或多個檔案。
   * 將在其中建立檔案的資料夾。 此資料夾位於表單伺服器上。 如果資料夾路徑是相對的，則它是相對於應用程式伺服器根目錄的。
   * 用於稽核事件檔案的檔案首碼
   * 檔案的格式，可以是與Microsoft Excel相容的逗號分隔值(CSV)檔案，也可以是XML檔案。

1. 按一下「匯出」。 如果要取消匯出，請按一下「取消匯出」。 如果其他使用者已排程匯出，則在該匯出完成之前，「取消匯出」按鈕不可用。 如果其他使用者已排程匯出，則取消匯出按鈕不可用。 若要檢查排定的匯出或刪除是否已開始或完成，請按一下[重新整理]。

### 刪除稽核事件 {#delete-audit-events}

您可以刪除早於指定天數的稽核事件。

1. 在管理控制檯中，按一下「服務> Document Security >設定>事件管理」。
1. 在「刪除稽核事件」下，指定「刪除早於下列時間的稽核事件」方塊中的天數。
1. 单击删除。按一下「匯出」。 如果要取消刪除，請按一下「取消刪除」。 如果其他使用者已排程刪除，則在該匯出完成之前，「取消刪除」按鈕不可用。 如果其他使用者已排程匯出，則取消刪除按鈕不可用。 若要檢查排定的刪除是否已開始或完成，請按一下重新整理。

### 事件稽核選項 {#event-auditing-options}

您可以啟用和停用事件稽核，並指定要稽核的事件型別。

**檔案事件**

**檢視檔案：** 收件者檢視受原則保護的檔案。

**關閉檔案：** 收件者關閉受原則保護的檔案。

**列印低解析度** 收件者列印受原則保護的檔案，並指定低解析度選項。

**列印高解析度：** 收件者列印受原則保護的檔案，並指定高解析度選項。

**新增註解至檔案：** 收件者將註解新增至PDF檔案。

**撤銷檔案：** 使用者或管理員撤銷對受原則保護檔案的存取權。

**取消撤銷檔案：** 使用者或管理員恢復對受原則保護檔案的存取權。

**表單填寫：** 收件者會在可填寫表單的PDF檔案中輸入資訊。

**已移除原則：** 發行者從檔案中移除一項原則，以撤銷安全性保護。

**變更檔案撤銷URL：** 來自API層級的呼叫會變更指定的撤銷URL，以存取取代已撤銷檔案的新檔案。

**修改檔案：** 收件者變更受原則保護檔案的內容。

**簽署檔案：** 收件者簽署檔案。

**保護新檔案：** 使用者套用原則來保護檔案。

**切換檔案原則：** 使用者或管理員會切換附加至檔案的原則。

**將檔案發佈為：** 在伺服器上註冊的documentName和授權與現有檔案相同的新檔案，且檔案沒有父子關係。 此事件可使用AEM Forms SDK觸發。

**重複檔案：** 在伺服器上註冊的documentName和授權與現有檔案相同的新檔案，且檔案具有父子關係。 此事件可使用AEM Forms SDK觸發。

**原則事件**

**建立的原則：** 使用者或管理員會建立原則。

**啟用的原則：** 管理員讓原則可供使用。

**已變更的原則：** 使用者或管理員變更原則。

**已停用原則：** 管理員讓原則無法使用。

**已刪除原則：** 使用者或管理員刪除原則。

**變更原則擁有者：** 來自API層級的呼叫會變更原則所有者。

**使用者事件**

**已刪除的使用者：** 管理員會刪除使用者帳戶。

**註冊受邀使用者：** 外部使用者向Document Security註冊。

**成功登入：** 管理員或使用者成功登入嘗試。

**受邀使用者：** Document Security邀請使用者註冊。

**已啟動的使用者：** 外部使用者透過啟用電子郵件中的URL來啟用其帳戶，或管理員啟用帳戶。

**變更密碼：** 邀請的使用者變更其密碼，或管理員為本機使用者重設密碼。

**登入失敗：** 管理員或使用者的登入嘗試失敗。

**已停用的使用者：** 管理員會停用本機使用者帳戶。

**設定檔更新：** 受邀使用者變更其名稱、組織名稱和密碼。

**帳戶已鎖定：** 管理員會鎖定帳戶。

**原則集事件**

**建立的原則集：** 管理員或原則集協調者會建立原則集。

**已刪除的原則集：** 管理員或原則集協調者會刪除原則集。

**修改的原則集：** 管理員或原則集協調器會變更原則集。

**系統事件**

**目錄同步處理完成：** 無法從「事件」頁面取得此資訊。 目前的目錄同步處理資訊（包括目前的同步處理狀態和上次同步處理的時間）會顯示在「網域管理」頁面上。 若要存取管理控制檯中的「網域管理」頁面，請按一下「設定>使用者管理>網域管理」。

**使用者端啟用離線存取：** 使用者已啟用對檔案的離線存取，而這些檔案是透過使用者電腦上的伺服器所保護。

**已同步的使用者端** 使用者端應用程式必須與伺服器同步化資訊，以允許離線存取。

**版本不相符：** 與嘗試連線至伺服器的伺服器不相容的AEM Forms SDK版本。

**目錄同步處理資訊：** 無法從「事件」頁面取得此資訊。 目前的目錄同步處理資訊（包括目前的同步處理狀態和上次同步處理的時間）會顯示在「網域管理」頁面上。 若要存取管理控制檯中的「網域管理」頁面，請按一下「設定>使用者管理>網域管理」。

**伺服器組態變更：** 透過網頁或手動匯入config.xml檔案來完成伺服器設定的變更。 這包括變更基本URL、工作階段逾時、登入鎖定、目錄設定、金鑰變換、外部註冊的SMTP伺服器設定、浮水印設定、顯示選項等。

## 設定延伸使用追蹤 {#configuring-extended-usage-tracking}

Document Security可以追蹤可能在受保護檔案上執行的各種自訂事件。 您可以在全域層級或原則層級啟用Document Security伺服器的事件追蹤。 然後您可以設定JavaScript來擷取在受保護的PDF檔案中執行的特定動作，例如按一下按鈕或儲存檔案。 此使用資料會以索引鍵值配對的XML檔案傳送，供您進一步分析。 存取受保護檔案的一般使用者可以允許或拒絕來自使用者端應用程式的此類追蹤。

如果在全域層級啟用追蹤，您可以在原則層級覆寫此設定，並為特定原則停用它。 如果在全域層級停用追蹤，則無法進行原則層級覆寫。 當事件計數達到25個或檔案關閉時，追蹤的事件清單會自動推送到伺服器。 您也可以根據需求設定指令碼，明確推送事件清單。 您可以存取Document Security物件屬性和方法來自訂事件追蹤。

啟用追蹤後，所有後續建立的原則都會預設開啟追蹤。 在伺服器上啟用追蹤之前建立的原則將需要手動更新。

### 啟用或停用延伸使用量追蹤 {#enable-or-disable-extended-usage-tracking}

開始之前，請確定伺服器稽核已啟用。 另請參閱 [設定事件稽核和隱私設定](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) 以取得稽核的詳細資訊。

1. 在管理控制檯中，按一下「服務> Document Security >設定>稽核和隱私設定」。
1. 若要設定擴充使用量追蹤，請在「啟用追蹤」下選取「是」或「否」。
1. 若要設定選取登入頁面上的「允許收集詳細使用資料」核取方塊，請在「啟用追蹤」預設值下，選取「是」或「否」。

若要檢視追蹤的事件，您可以使用「事件」頁面上的「檔案事件」篩選器。 使用JavaScript追蹤的事件會標示為「詳細使用情況追蹤」。 請參閱 [監視事件](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) 以取得事件的詳細資訊。

## 設定Document Security顯示設定 {#configure-document-security-display-settings}

1. 在管理控制檯中，按一下「服務> Document Security >設定>顯示選項」。
1. 設定設定，然後按一下「確定」。

### 顯示設定 {#display-settings}

**要針對搜尋結果顯示的列：** 執行搜尋時出現在頁面上的列數。

**使用者端登入對話方塊的自訂**

這些設定可控制當使用者透過使用者端應用程式登入Document Security時，在登入提示中顯示的文字。

**歡迎文字：** 歡迎訊息文字，例如「請使用您的使用者名稱和密碼登入」。 歡迎訊息文字應包含有關如何登入Document Security以及如何聯絡管理員或您組織中的其他指定支援人員以尋求協助的資訊。 例如，如果外部使用者忘記密碼，或需要註冊或登入程式的協助，則可能需要聯絡管理員。 歡迎文字的最大長度為512個字元。

**使用者名稱文字：** 使用者名稱方塊的文字標籤。

**密碼文字：** 密碼方塊的文字標籤。

**使用者端憑證驗證對話方塊的自訂**

這些設定控制憑證驗證對話方塊中顯示的文字。

**選擇驗證型別文字：** 顯示用來指示使用者選取驗證型別的文字。

**選擇憑證文字：** 顯示的文字，用來指示使用者選取憑證型別。

**無法取得憑證錯誤文字：** 所選憑證不可用時，最多可顯示512個字元的訊息。

**自訂使用者端憑證顯示**

**僅顯示信任的認證發行者：** 選取此選項時，使用者端應用程式僅會向使用者提供AEM表單設定為可信任的認證發行者憑證（請參閱管理憑證和認證）。 未選取此選項時，會向使用者顯示使用者系統上所有憑證的清單。

## 設定動態浮水印 {#configure-dynamic-watermarks}

您可以使用Document Security來設定動態浮水印選項的預設設定，以便在建立原則時套用。 A *浮水印* 是疊加在檔案中文字上的影像。 此變數對於追蹤檔案內容很有用，且有助於識別內容的非法使用。

動態浮水印可包含由已定義變數（例如使用者ID和日期以及自訂文字）組成的文字，或PDF中的RTF內容。 您可以使用數個元素來設定浮水印，每個元素都有自己的位置和格式。

浮水印不可編輯，因此是確保檔案內容機密性的更安全方法。 動態浮水印也可確保浮水印顯示足夠的使用者特定資訊，以作為進一步分發檔案的威懾力。

當收件者檢視或列印檔案時，原則指定的浮水印會出現在受原則保護的檔案中。 與永久浮水印不同，動態浮水印永遠不會儲存在檔案中，這提供了在內聯網環境中部署檔案時所需的靈活性，以確保檢視應用程式顯示特定使用者的身份。 此外，如果檔案有多個使用者，使用動態浮水印表示您可以使用一個檔案，而不是多個版本，每個版本都有不同的浮水印。 出現的浮水印反映了目前使用者的身份。

請注意，動態浮水印與使用者可直接新增至Acrobat中的檔案的浮水印不同。 結果是在受原則保護的檔案中可以有兩個浮水印。

### 建立浮水印時的注意事項 {#considerations-when-creating-watermarks}

您可以使用數個浮水印元素來建立動態浮水印，並將每個元素指定為文字或PDF。 您最多可以在浮水印中包含五個元素。

如果您選擇文字型浮水印，您可以在含有多個文字專案的浮水印內指定數個元素，並指定每個元素的位置。 為這些元素指派有意義的名稱，例如頁首、頁尾等。

例如，如果您想在頁首、頁尾、邊界和整個檔案中指定不同的文字做為浮水印，您可以建立數個浮水印元素並指定其位置。 如果您希望使用者的使用者ID和目前存取檔案的日期顯示在頁首中、右邊界的原則名稱，以及自訂文字「CONFIDENTIAL」在檔案中對角顯示，您可以定義以文字為型別的個別浮水印元素，並指定其格式和位置。 將浮水印套用至檔案時，浮水印中的所有元素會以它們加入浮水印的順序同時套用至檔案。

通常，您可以使用PDF式浮水印來包含圖形內容（例如商標或特殊符號），例如版權或註冊商標。

您可以修改Document Security組態檔，以變更浮水印元素數量和PDF檔案大小的限制。 另請參閱 [變更浮水印設定引數](configuring-client-server-options.md#change-the-watermark-configuration-parameters).

設定浮水印時，請牢記以下事項：

* 您無法使用受密碼保護的PDF檔案作為浮水印元素。 不過，如果您建立的浮水印包含其他不受密碼保護的元素，則會套用這些元素作為浮水印的一部分。
* 您可以變更要用作浮水印元素的PDF檔案大小上限。 不過，在離線同步處理套用這類浮水印的檔案期間，用作浮水印的大型PDF檔案會降低效能。 另請參閱 [變更浮水印設定引數](configuring-client-server-options.md#change-the-watermark-configuration-parameters).
* 只有所選PDF的第一頁會用作浮水印。 確保您要顯示為浮水印的資訊可在第一頁本身使用。
* 即使您可以指定PDF檔案的縮放比例，如果您打算在頁首、頁尾或邊界中將其用作浮水印，請考慮頁面大小和PDF版面。
* 指定字型名稱時，請正確輸入名稱。 AEM forms會取代您指定的字型（如果開啟檔案的使用者端電腦中不存在此字型）。
* 如果您選取文字作為浮水印內容，將縮放比例選項指定為「符合頁面」時，無法用於寬度不相似的頁面。
* 當您指定浮水印元素的位置時，請確定只有一個元素具有相同的位置。 如果兩個浮水印元素具有相同的位置（例如置中），它們會以加入浮水印的順序在檔案上顯示重疊。
* 指定字型大小和文字時，請確定文字的長度在頁面中完全可見。 文字內容會捲動到新的行中，因此您想要在邊界出現的浮水印內容可能會與頁面上的內容區域重疊。 但是，如果檔案在Acrobat 9中開啟，則單行以外的文字會被截斷。

### 動態浮水印的限制 {#limitations-of-dynamic-watermarks}

某些使用者端應用程式可能不支援動態浮水印。 請參閱適當的Acrobat Reader DC擴充功能說明。 此外，對於支援動態浮水印的Acrobat版本，請記得下列事項：

* 您無法使用受密碼保護的PDF檔案作為浮水印元素。
* 10版之前的Acrobat和Adobe Reader不支援下列浮水印功能：

   * PDF浮水印
   * 浮水印中有多個元素(文字/PDF)
   * 進階選項，例如頁面範圍或顯示選項
   * 文字格式選項，例如指定的字型、字型名稱和顏色。 不過，舊版Acrobat和Reader會以預設字型和顏色顯示文字內容。

* Acrobat 9.0及舊版： Acrobat 9.0及舊版不支援動態浮水印中的原則名稱。 如果Acrobat 9.0開啟含有動態浮水印的受原則保護檔案，其中包含原則名稱和其他動態資料，則浮水印顯示時不會包含原則名稱。 如果動態浮水印僅包含原則名稱，Acrobat會顯示錯誤訊息

### 新增動態浮水印範本 {#add-a-dynamic-watermark-template}

您可以建立動態浮水印範本。 這些範本仍可作為管理員或使用者建立之原則的設定選項。

>[!NOTE]
>
>匯出組態檔時，動態浮水印組態資訊不會與其他組態資訊一起擷取。

1. 在管理控制檯中，按一下「服務> Document Security >設定>浮水印」。
1. 按一下「新增」。
1. 在「名稱」方塊中，鍵入新浮水印的名稱。

   ***注意&#x200B;**：您無法在浮水印或浮水印元素的名稱或說明中使用某些特殊字元。 請參閱下列限制清單： [編輯原則的考量](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies).*

1. 在「名稱」下方的加號旁，為浮水印元素輸入有意義的名稱（例如「標題」），並新增說明，然後展開加號以顯示選項。
1. 在「來源」下，選取「文字」或「PDF」型別的浮水印。
1. 如果您選取「文字」，請執行下列動作：

   * 選取要包含的浮水印型別。 如果您選取「自訂文字」，請在鄰接方塊中輸入要針對浮水印顯示的文字。 請記住將顯示為浮水印的文字長度。
   * 為浮水印文字的文字內容指定文字格式屬性，例如字型名稱、字型大小、前景色和背景色。 將前景色和背景色指定為十六進位值。

      ***注意&#x200B;**：如果您選取「縮放比例」選項為「符合頁面」，則無法編輯font size屬性。*

1. 如果您已選取PDF豐富浮水印選項，請按一下 **瀏覽** 在「選取浮水印PDF」旁邊，選取您要用作浮水印的PDF檔案。

   ***注意&#x200B;**：請勿使用受密碼保護的PDF檔案。 如果您指定受密碼保護的PDF作為浮水印元素，則不會套用浮水印。*

1. 在「用作背景」下，選取「是」或「否」。

   **注意**：目前，無論此設定為何，浮水印都會出現在前景中。

1. 若要控制浮水印在檔案上的顯示位置，請設定「垂直對齊」和「水準對齊」選項。
1. 選取「符合頁面」或選取%，然後在方塊中輸入百分比。 值必須是整數，而非分數。 若要設定浮水印大小，您可以使用頁面百分比的值，或設定浮水印以符合頁面大小。
1. 在「旋轉」方塊中，輸入旋轉浮水印的角度。 範圍為–180到180。 使用負值可逆時針旋轉浮水印。 值必須是整數，而非分數。
1. 在「不透明度」方塊中，輸入百分比。 請使用整數，而非分數。
1. 在「進階選項」下，設定下列專案：

   **頁面範圍選項**

   設定應顯示浮水印的頁面範圍。 輸入起始頁為1，結束頁為–1，讓所有頁面都標示有浮水印。

   **顯示選項**

   選取您要讓浮水印出現的位置。 依預設，浮水印會同時出現在軟復本（線上）和硬復本（列印）上。

1. 按一下 **新增** 如有必要，可在「浮水印元素」下方新增更多浮水印元素。
1. 单击确定。

### 編輯動態浮水印範本 {#edit-a-dynamic-watermark-template}

1. 在管理控制檯中，按一下「服務> Document Security >設定>浮水印」。
1. 按一下清單中適當的浮水印。
1. 在「編輯浮水印」頁面上，視需要變更設定。
1. 单击确定。

### 刪除動態浮水印範本 {#delete-a-dynamic-watermark-template}

當您刪除動態浮水印時，將無法再將它新增到新原則中。 不過，浮水印會保留在目前使用它的現有原則上，而且原則目前保護的檔案會繼續顯示動態浮水印，直到您或使用者編輯包含已刪除浮水印的原則為止。 編輯原則後，不再套用浮水印。 會出現一則訊息，指示原則上的現有浮水印已刪除，使用者可以選擇另一個來取代它。

1. 在管理控制檯中，按一下「服務> Document Security >設定>浮水印」。
1. 選取適當浮水印旁的核取方塊，然後按一下「刪除」。
1. 单击确定。

## 設定受邀使用者註冊 {#configuring-invited-user-registration}

您組織外部的使用者可以註冊Document Security。 註冊並啟用其帳戶的受邀使用者可以使用其電子郵件地址和註冊時建立的密碼來登入Document Security。 已註冊的受邀使用者可以使用他們有權使用的受原則保護檔案。

當受邀使用者啟動時，他們會成為本機使用者。 您可以使用「受邀使用者」和「本機使用者」區域來設定和管理本機使用者。 (請參閱 [管理受邀和本機使用者帳戶](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts).)

根據您為受邀使用者啟用的功能，他們也可以使用這些Document Security功能：

* 套用原則至檔案
* 建立原則
* 將受邀使用者新增至原則

當發生下列事件時，Document Security會自動產生註冊邀請電子郵件，除非使用者已在來源LDAP目錄中或先前已被邀請註冊：

* 現有使用者將受邀使用者新增至原則
* 管理員會在「受邀使用者註冊」頁面上新增受邀使用者帳戶

註冊電子郵件包含「註冊」頁面的連結，以及有關如何註冊的資訊。 受邀使用者註冊後，Document Security會發出一封包含啟動頁面連結的啟動電子郵件。 啟用後，帳戶會維持有效，直到您停用或刪除帳戶為止。

如果您啟用內建註冊，您只需指定一次SMTP伺服器、註冊電子郵件詳細資訊、存取權及重設密碼電子郵件資訊。 啟用內建註冊之前，請確保您已在「使用者管理」中建立本機網域，並已將「Document Security邀請使用者」角色指派給組織中的適當使用者和群組。 (請參閱 [新增本機網域](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) 和 [建立和設定角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).) 如果您未使用內建註冊，則必須使用AEM Forms SDK建立自己的使用者註冊系統。 請參閱以下主題中「為AEM表單開發SPI」的說明： [使用AEM表單程式設計](/help/forms/developing/introducing-java-api-soap-quick.md). 如果您未使用內建註冊選項，建議您在啟動電子郵件及使用者端登入畫面上設定訊息，以通知使用者如何連絡管理員以取得新密碼或其他資訊。

**啟用並設定受邀使用者註冊**

依預設，受邀使用者註冊程式會停用。 您可以視需要啟用和停用受邀使用者註冊以獲得Document Security。

1. 在管理控制檯中，按一下「服務> Document Security >設定>受邀使用者註冊」。
1. 選取「啟用受邀使用者註冊」。
1. （可選）視需要更新受邀使用者註冊設定：

   * [排除或包含外部使用者或群組](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [伺服器和註冊帳戶引數](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [註冊邀請電子郵件設定](configuring-client-server-options.md#registration-invitation-email-settings)
   * [啟用電子郵件設定](configuring-client-server-options.md#activation-email-settings)
   * [設定密碼重設電子郵件](configuring-client-server-options.md#configure-a-password-reset-email)

1. （選擇性）在內建註冊下，選取是以啟用此選項。 如果您未啟用內建註冊，則必須設定您自己的使用者註冊系統。
1. 单击确定。

### 排除或包含外部使用者或群組 {#exclude-or-include-an-external-user-or-group}

您可以限制某些外部使用者或使用者群組使用Document Security註冊。 此選項很實用，例如可允許存取特定使用者群組，但排除屬於該群組的特定個人。

下列設定位於「受邀使用者註冊」頁面的「電子郵件限制篩選」區域。

**排除：** 輸入要排除的使用者或群組的電子郵件地址。 若要排除多個使用者或群組，請在新行中輸入每個電子郵件地址。 若要排除屬於特定網域的所有使用者，請輸入萬用字元和網域名稱。 例如，若要排除example.com網域中的所有使用者，請輸入&amp;ast；.example.com。

**包含：** 輸入要包含的使用者或群組的電子郵件地址。 若要包含多個使用者或群組，請在新行中輸入每個電子郵件地址。 若要包含屬於特定網域的所有使用者，請輸入萬用字元和網域名稱。 例如，若要在example.com網域中包含所有使用者，請輸入&amp;ast；.example.com。

### 伺服器和註冊帳戶引數 {#server-and-registration-account-parameters}

下列設定位於「受邀使用者註冊」頁面的「一般設定」區域中。

**SMTP主機：** SMTP伺服器的主機名稱。 SMTP伺服器會管理外寄電子郵件通知，以註冊及啟用受邀使用者帳戶。

如果您的SMTP主機需要，請在[SMTP伺服器帳戶名稱]和[SMTP伺服器帳戶密碼]方塊中輸入所需的資訊，以連線到SMTP伺服器。 有些組織不強制此要求。 如果您需要資訊，請洽詢系統管理員。

**SMTP伺服器通訊端類別名稱：** SMTP伺服器的通訊端類別名稱。 例如，javax.net.ssl.SSLSocketFactory。

**電子郵件內容型別：** 接受的MIME型別，例如text/plain或text/html。

**電子郵件編碼：** 傳送電子郵件訊息時使用的編碼格式。 您可以指定任何編碼，例如UTF-8表示Unicode，或ISO-8859-1表示Latin。 預設值為UTF-8。

**重新導向電子郵件地址：** 當您為此設定指定電子郵件地址時，任何新的邀請都會傳送至提供的地址。 此設定可用於測試目的。

**使用本機網域：** 選取適當的網域。 在新安裝時，請確定您是使用使用者管理建立網域。 如果是升級，則會在升級期間建立外部使用者網域，且可以使用。

**對SMTP伺服器使用SSL：** 選取此選項以啟用SMTP伺服器的SSL。

**在註冊頁面上顯示登入連結：** 在註冊頁面上顯示受邀使用者的登入連結。

**為SMTP伺服器啟用傳輸層安全性(TLS)的方式**

1. 開啟管理主控台。

   管理主控台的預設位置為 `https://<server>:<port>/adminui`.

1. 導覽至「首頁>服務> Document Security >設定>受邀使用者註冊」。
1. 在「受邀使用者註冊」中，指定所有組態設定，然後按一下「確定」。

   >[!NOTE]
   >
   >如果您使用Microsoft Office 365做為SMTP伺服器來傳送使用者註冊邀請，請使用下列設定：
   >
   >**SMTP主機：** smtp.office365.com
   >**連線埠：** 587

1. 接下來，您需要更新config.xml。 另請參閱 [啟用傳輸層安全性(TLS) SMTP的設定](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>如果您對「受邀使用者註冊」選項進行任何變更，則會覆寫config.xml檔案並停用TLS。 如果您覆寫變更，您必須執行上述步驟以重新啟用「受邀使用者註冊」的TLS支援。

### 註冊邀請電子郵件設定 {#registration-invitation-email-settings}

當您建立新的受邀使用者帳戶，或現有使用者新增先前未註冊或被邀請註冊原則的外部收件者時，Document Security會自動發出註冊邀請電子郵件。 電子郵件包含收件者可用來存取註冊頁面及輸入個人帳戶資訊（包括使用者名稱和密碼）的連結。 密碼可以是八個字元的任意組合。

當收件者啟用帳戶時，使用者會成為本機使用者。

下列設定位於「受邀使用者註冊」頁面的「邀請電子郵件設定」區域中。

**從：** 用來傳送邀請電子郵件的電子郵件地址。 寄件者電子郵件地址的預設格式為postmaster@[your_installation_domain].com.

**主旨：** 邀請電子郵件訊息的預設主旨。

**逾時：** 如果外部使用者未註冊，則註冊邀請到期的天數。 預設值為30天。

**訊息：** 邀請使用者註冊的訊息內文中顯示的文字。

### 啟用電子郵件設定 {#activation-email-settings}

受邀使用者註冊後，Document Security會傳送一封啟用電子郵件。 啟用電子郵件包含帳戶啟用頁面的連結，使用者可在其中啟用其帳戶。 帳戶啟動後，使用者可以使用他們的電子郵件地址和註冊時建立的密碼來登入Document Security。

當收件者啟用使用者帳戶時，使用者會成為本機使用者。

下列設定位於「受邀使用者註冊」頁面的「啟動電子郵件設定」區域中。

>[!NOTE]
>
>也建議您在登入畫面上設定訊息，以建議外部使用者如何聯絡其管理員以取得新密碼或其他資訊。

**從：** 傳送啟動電子郵件的電子郵件地址。 此電子郵件地址會從註冊人的電子郵件主機接收失敗的傳遞通知，也會收到收件者為回覆註冊電子郵件而傳送的任何訊息。 寄件者電子郵件地址的預設格式為postmaster@[your_installation_domain].com.

**主旨：** 啟用電子郵件訊息的預設主旨。

**逾時：** 如果使用者未啟用帳戶，則啟用邀請到期的天數。 預設值為30天。

**訊息：** 顯示在訊息內文的文字，此訊息指出收件者的使用者帳戶需要啟動。 您可能也想要包含如何連絡管理員以取得新密碼等資訊。

### 設定密碼重設電子郵件 {#configure-a-password-reset-email}

如果您必須重設受邀使用者的密碼，則會產生確認電子郵件，邀請使用者選擇新密碼。 無法判斷使用者的密碼；如果使用者忘記密碼，您必須重設密碼。

下列設定位於「受邀使用者註冊」頁面的「重設密碼電子郵件」區域中。

**從：** 傳送密碼重設電子郵件的電子郵件地址。 寄件者電子郵件地址的預設格式為postmaster@[your_installation_domain].com.

**主旨：** 重設電子郵件的預設主旨。

**訊息：** 顯示在訊息內文中的文字，此訊息指出收件者的外部使用者密碼已重設。

## 啟用使用者和群組來建立原則 {#enable-users-and-groups-to-create-policies}

「組態」頁面有一個連至「我的原則」頁面的連結，您可以在其中指定哪些一般使用者可以建立我的原則，以及搜尋結果中會顯示哪些使用者和群組。 「我的原則」頁面有兩個頁簽：

**「建立原則」標籤：** 使用來設定使用者許可權，以建立自訂原則。

**可見的使用者和群組索引標籤：** 用來控制可在使用者搜尋結果中看到的使用者和群組。 超級使用者或原則集管理員必須選取並在「使用者管理」中建立的網域，並將網域新增至每個原則集的可見使用者與群組。 原則集協調器可以看見此清單，並用來限制原則集協調器在選擇要新增到原則的使用者時，可以瀏覽哪些網域。

在授予使用者建立自訂原則的許可權之前，請考慮您希望個別使用者擁有多少存取權或控制權。 此外，請考量您希望使用者與群組在搜尋時顯示於何種程度。

### 指定可以建立原則的使用者和群組 {#specify-users-and-groups-who-can-create-policies}

以管理員身分，指定哪些使用者和群組可以建立自訂原則。 此許可權可在使用者和群組層級設定。 搜尋功能會在「使用者管理」資料庫中搜尋使用者和群組。

1. 在管理控制檯中，按一下「服務> Document Security >設定>我的原則」。
1. 在「我的原則」頁面上，按一下「建立原則」標籤，然後按一下「新增使用者和群組」。
1. 在「尋找」方塊中，輸入您要搜尋的使用者或群組的使用者名稱或電子郵件地址。 如果您沒有此資訊，請將此方塊留空。 您也可以輸入部分名稱或電子郵件地址，例如只知道使用者名稱的前兩個字母時。
1. 在「使用」清單中，選取搜尋引數「名稱」或「電子郵件」。
1. 在「型別」清單中，選取「群組」或「使用者」來縮小搜尋範圍。
1. 在「在」清單中，選取要搜尋的網域。 如果您不知道使用者或群組的網域，請選取「所有網域」。
1. 在「顯示」清單中，指定每頁要顯示的搜尋結果數目，然後按一下「尋找」。
1. 若要新增「我的原則」使用者和群組，請選取每個要新增的使用者和群組的核取方塊。
1. 按一下「新增」，然後按一下「確定」。

您選取的使用者和群組現在擁有建立自訂原則的許可權。

### 移除使用者或群組的建立自訂原則許可權 {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. 在Document Security頁面上，按一下「設定」>「我的原則」。
1. 在「我的原則」頁面上，按一下「建立原則」頁簽。 將顯示具有建立自訂原則許可權的使用者和群組。
1. 選取要從此許可權中移除的使用者和群組旁的核取方塊。
1. 按一下「刪除」，然後按一下「確定」。

### 指定搜尋中可見的使用者和群組 {#specify-users-and-groups-that-are-visible-in-searches}

當使用者管理其自訂原則時，他們可以搜尋要新增到其原則中的使用者和群組。 您必須指定在這些搜尋中顯示使用者和群組的網域。

1. 在Document Security頁面上，按一下「設定」>「我的原則」。
1. 在「我的原則」頁面上，按一下「可見的使用者和群組」標籤。
1. 若要讓網域中的使用者和群組可見，請按一下「新增網域」、選取網域，然後按一下「新增」。 若要移除網域，請選取網域名稱旁的核取方塊，然後按一下刪除。

## 手動編輯Document Security {#manually-editing-the-document-security-configuration-file}

您可以匯入和匯出儲存在Document Security資料庫中的組態資訊。 例如，從中繼環境移至生產環境時，您可能想要備份組態資訊的復本，或者您可能想要編輯編輯此檔案時只能設定的進階選項。

您可以使用組態檔進行下列變更：

[建立和編輯原則時顯示CATIA許可權](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[指定離線同步處理的逾時期間](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[拒絕特定應用程式的檔案安全性服務](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[變更浮水印設定引數](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[停用外部連結](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>匯入組態檔案會根據檔案中的資訊重新配置系統。 動態浮水印設定和自訂事件資訊則屬例外，這些資訊不會與匯出的設定檔案一起儲存。 您必須在新系統中手動設定此資訊。 只有熟悉Document Security和XML的系統管理員或專業服務顧問才能修改組態檔的內容，例如重新設定損毀的設定，或調整特定企業部署案例的引數。

**匯出組態檔**

1. 在管理控制檯中，按一下「服務> document security 11 >設定>手動設定」。
1. 按一下「匯出」並將組態檔案儲存在其他位置。 預設檔案名稱為config.xml。
1. 单击确定。
1. 在變更組態檔之前，請先製作備份復本，以備您需要回覆時使用。

**匯入組態檔**

1. 在管理控制檯中，按一下「服務> document security 11 >設定>手動設定」。
1. 按一下「瀏覽」以前往組態檔，然後按一下「匯入」。 您無法直接在「檔案名稱」方塊中輸入路徑。
1. 单击确定。

### 指定離線同步處理的逾時期間 {#specify-a-timeout-period-for-offline-synchronization}

Document Security可讓使用者在未連線至Document Security伺服器時，開啟並使用受保護檔案。 使用者的使用者端應用程式必須定期與伺服器同步，以確保檔案可離線使用。 使用者第一次開啟受保護的檔案時，系統會詢問其電腦是否應該獲授權執行定期的使用者端同步處理。

根據預設，當使用者連線到Document Security伺服器時，同步處理會視需要每四小時自動執行一次。 如果檔案的離線期間在使用者離線時到期，則使用者必須重新連線至伺服器，讓使用者端應用程式與伺服器同步。

在Document Security組態檔中，您可以指定自動背景同步化的預設頻率。 除非使用者端明確設定自己的逾時值，否則此設定會作為預設逾時期間使用者端應用程式。

1. 匯出Document Security組態檔。 (請參閱 [手動編輯Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在編輯器中開啟設定檔案，並找到 `PolicyServer` 節點。 在該節點下，找到 `ServerSettings` 節點。
1. 在 `ServerSettings` 節點，新增以下專案，然後儲存檔案：

   `<entry key="BackgroundSyncFrequency" value="`*時間* `"/>`

   位置 *時間* 是自動背景同步之間的秒數。 如果您將此值傳送至 `0`，一律會進行同步。 預設值為 `14400` 秒（每四小時）。

1. 匯入組態檔。 (請參閱 [手動編輯Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 拒絕特定應用程式的檔案安全性服務 {#denying-document-security-services-for-specific-applications}

您可以設定Document Security，拒絕對符合特定條件的應用程式提供服務。 條件可指定單一屬性（例如平台名稱），也可以指定多組屬性。 此功能可協助您控制Document Security必須處理的請求。 以下是此功能的一些應用程式：

* **收入保障：** 您可能想要拒絕存取任何不支援收入慣例的使用者端應用程式。
* **應用程式相容性：** 某些應用程式可能與您的Document Security伺服器的原則或行為不相容。

當使用者端應用程式嘗試與Document Security建立連結時，會提供應用程式、版本和平台資訊。 Document Security會將此資訊與從Document Security設定檔中取得的「拒絕」設定進行比較。

[拒絕]設定可包含幾組拒絕條件。 如果任一組的所有屬性相符，則拒絕請求應用程式存取Document Security服務。

阻斷服務功能要求使用者端應用程式使用Document Security C++使用者端SDK 8.2版或更新版本。 下列Adobe產品在要求Document Security服務時提供產品資訊：

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard和更新版本
* Adobe Reader 9.0和更新版本
* Microsoft Office 8.2及更新版本的Acrobat Reader DC擴充功能

使用者端應用程式會使用Document Security C++使用者端SDK的使用者端API，向Document Security請求服務。 使用者端API請求包含平台和SDK版本資訊（預先編譯至使用者端API）以及從使用者端應用程式取得的產品資訊。

使用者端應用程式或外掛程式會在執行回呼函式時提供產品資訊。 應用程式提供下列資訊：

* Integrator名稱
* Integrator版本
* 應用程式系列
* 應用程式名稱
* 應用程式版本

如果有任何資訊不適用，使用者端應用程式會將對應的欄位留空。

有幾種Adobe應用程式在請求Document Security服務時包含產品資訊，包括Acrobat、Adobe Reader和Microsoft Office的Acrobat Reader DC擴充功能。

**Acrobat和Adobe Reader**

Acrobat或Adobe Reader向Document Security請求服務時，會提供下列產品資訊：

* **Integrator：** Adobe Systems公司
* **Integrator版本：** 1.0
* **應用程式系列：** Acrobat
* **應用程式名稱：** Acrobat
* **應用程式版本：** 9.0.0

**Microsoft Office適用的Acrobat Reader DC擴充功能**

Microsoft Office的Acrobat Reader DC擴充功能是搭配Microsoft Office產品Microsoft Word、Microsoft Excel和Microsoft PowerPoint使用的外掛程式。 當它請求服務時，會提供下列資訊：

* **Integrator：** Adobe Systems Incorporated
* **Integrator版本：** 8.2
* **應用程式系列：** Microsoft Office適用的Acrobat Reader DC擴充功能
* **應用程式名稱：** Microsoft Word、Microsoft Excel或Microsoft PowerPoint
* **應用程式版本：** 2003或2007

**設定Document Security以拒絕特定應用程式的服務**

1. 匯出Document Security組態檔。 (請參閱 [手動編輯Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在編輯器中開啟設定檔案，並找到 `PolicyServer` 節點。 新增 `ClientVersionRules` 節點，作為 `PolicyServer` 節點（如果節點不存在）：

   ```xml
    <node name="ClientVersionRules">
        <map>
            <entry key="infoURL" value="URL"/>
        </map>
        <node name="Denials">
            <map/>
            <node name="MyEntryName">
                <map>
                    <entry key="SDKPlatforms" value="platforms"/>
                    <entry key="SDKVersions" value="versions"/>
                    <entry key="AppFamilies" value="families"/>
                    <entry key="AppNames" value="names"/>
                    <entry key="AppVersions" value="versions"/>
                    <entry key="Integrators" value="integrators"/>
                    <entry key="IntegratorVersions" value="versions"/>
                </map>
            </node>
            <node name="MyOtherEntryName"
                <map>
                    [...]
                </map>
            </node>
            [...]
        </node>
    </node>
   ```

   其中：

   `SDKPlatforms` 指定主控使用者端應用程式的平台。 可能的值包括：

   * Microsoft Windows
   * APPLE OS X
   * Sun Solaris
   * HP-UX

   `SDKVersions` 指定使用者端應用程式使用的Document Security C++使用者端API版本。 例如：`"8.2"`。

   `APPFamilies` 由使用者端API定義。

   `AppName`指定使用者端應用程式的名稱。 使用逗號作為名稱分隔符號。 若要在名稱中包含逗號，請以反斜線(\)字元逸出逗號。 例如， *「Adobe Systems\， Inc.」*.

   `AppVersions` 指定使用者端應用程式的版本。

   `Integrators` 指定開發外掛程式或整合式應用程式的公司或群組名稱。

   `IntegratorVersions` 是外掛程式或整合式應用程式的版本。

1. 對於每一組其他拒絕資料，請新增另一個 *MyEntryName* 元素。
1. 儲存組態檔。
1. 匯入組態檔。 (請參閱 [手動編輯Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

**示例**

在此範例中，所有Windows使用者端均被拒絕存取。

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://www.dont.use/windows.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="SDKPlatforms" value="Microsoft Windows"/>
             </map>
         </node>
     </node>
 </node>
```

在此範例中，「我的應用程式3.0版」和「我的其他應用程式2.0版」被拒絕存取。 無論拒絕的原因為何，都會使用相同的拒絕資訊URL。

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://get.a.new/version.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="FirstDenialSettings">
             <map>
                 <entry key="AppNames" value="My Application"/>
                 <entry key="AppVersions" value="3.0"/>
             </map>
         </node>
         <node name="SecondDenialSettings">
             <map>
                 <entry key="AppNames" value="My Other Application"/>
                 <entry key="AppVersions" value="2.0"/>
             </map>
         </node>
     </node>
 </node>
```

在此範例中，Microsoft PowerPoint 2007或Microsoft PowerPoint 2010安裝適用於Microsoft Office的Acrobat Reader DC擴充功能的所有請求都會遭到拒絕。

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://get.a.new/version.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="AppFamilies" value=
     "document security Extension for Microsoft Office"/>
                 <entry key="AppNames" value= "Microsoft PowerPoint"/>
                 <entry key="AppVersions" value="2007,2010"/>
             </map>
         </node>
     </node>
 </node
```

### 變更浮水印設定引數 {#change-the-watermark-configuration-parameters}

根據預設，您最多可以在浮水印中指定五個元素。 此外，您要用作浮水印的PDF檔案最大檔案大小限製為100KB。 您可以在config.xml檔案中變更這些引數。

***注意&#x200B;**：您應謹慎變更這些引數。*

1. 匯出Document Security組態檔。 (請參閱 [手動編輯Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在編輯器中開啟設定檔案，並找到 `ServerSettings` 節點。
1. 在 `ServerSettings` 節點，新增下列專案，然後儲存檔案： `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   第一個專案， *檔案大小上限* 是PDF浮水印元素允許的最大檔案大小(KB)。 預設為100KB。

   第二個專案， *最大元素* 是浮水印中允許的最大元素數量。 預設值為5。

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. 匯入組態檔。 (請參閱 [手動編輯Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 停用外部連結 {#disabling-external-links}

許多Document Security使用者無權存取外部連結，例如 **www.adobe.com** 當他們使用Right Management使用者介面：

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`。

下列對config.xml的變更會停用來自Right Management使用者介面的所有外部連結。

1. 匯出Document Security組態檔。 (請參閱 [手動編輯Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在編輯器中開啟設定檔案，並找到 `DisplaySettings` 節點。
1. 若要停用所有外部連結，請在 `DisplaySettings` 節點，新增以下專案，然後儲存檔案： `<entry key="ExternalLinksAllowed" value="false"/>`

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. 匯入組態檔。 (請參閱 [手動編輯Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 啟用傳輸層安全性(TLS) SMTP的設定 {#configuration-to-enable-smtp-for-transport-layer-security-tls}

下列對config.xml的變更，會啟用「受邀使用者註冊」功能的TLS支援。

1. 匯出Document Security組態檔。 (請參閱 [手動編輯Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在編輯器中開啟設定檔案，並找到 `DisplaySettings` 節點。
1. 找到下列節點： `<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. 設定 `SmtpUseTls` 中的索引鍵 `ExternalUser` 節點至 **true**.
1. 設定 `SmtpUseSsl` 中的索引鍵 `ExternalUser` 節點至 **false**.
1. 儲存 `config.xml`.
1. 匯入組態檔。 (請參閱 [手動編輯Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 停用Document Security檔案的SOAP端點 {#disable-soap-endpoints-for-document-security-documents}

下列對config.xml的變更，以停用Document Security檔案的SOAP端點。

1. 匯出Document Security組態檔。 (請參閱 [手動編輯Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在編輯器中開啟設定檔案，並找出以下節點： `<node name="DRM">`

   ```xml
   <node name="DRM">
   ```

1. 在DRM節點中，找到 `entry` 節點：

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. 若要停用Document Security檔案的SOAP端點，請將value屬性設定為 **false**.

   ```xml
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. 儲存 `config.xml`.
1. 匯入組態檔。 (請參閱 [手動編輯Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 提高檔案安全性伺服器的擴充性 {#increasingscalability}

根據預設，當同步檔案供離線使用時，連同目前檔案的資訊，document security使用者端會擷取使用者有權存取的所有其他檔案的原則、浮水印、授權和撤銷更新資訊。 如果這些更新和資訊未與客戶同步，則以離線模式開啟的檔案仍可能以舊的原則、浮水印和撤銷資訊開啟。

您可以限制傳送給使用者端的資訊，以增加Document Security伺服器的可擴充性。 減少傳送至使用者端的資訊量可改善擴充性、縮短回應時間，並提升伺服器效能。 執行以下步驟以提高擴充性：

1. 匯出Document Security組態檔。 (請參閱 [手動編輯Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在編輯器中開啟組態檔，並找到ServerSettings節點。
1. 在ServerSettings節點中，設定 `DisableGlobalOfflineSynchronizationData`屬性至 `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   若設為true，則Document Security伺服器僅傳送目前檔案的資訊，而其餘檔案（使用者可存取的其他檔案）的資訊則不會傳送給使用者端。

   >[!NOTE]
   >
   >根據預設， `DisableGlobalOfflineSynchronizationData`金鑰已設為 `false`.

1. 儲存並匯入組態檔。 (請參閱 [手動編輯Document Security](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
