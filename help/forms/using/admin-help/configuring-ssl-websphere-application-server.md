---
title: 為WebSphere Application Server設定SSL
seo-title: Configuring SSL for WebSphere Application Server
description: 瞭解如何設定WebSphere Application Server的SSL。
seo-description: Learn how to configure SSL for WebSphere Application Server.
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
exl-id: b0786b52-879e-4a24-9cc9-bd9dcb2473cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 0%

---

# 為WebSphere Application Server設定SSL {#configuring-ssl-for-websphere-application-server}

本節包含使用IBM WebSphere Application Server設定SSL的下列步驟。

## 在WebSphere上建立本機使用者帳戶 {#creating-a-local-user-account-on-websphere}

若要啟用SSL，WebSphere需要存取本機作業系統使用者登入中具有系統管理許可權的使用者帳戶：

* (Windows)建立新的Windows使用者，使其隸屬於Administrators群組，並擁有作為作業系統一部分的許可權。 (請參閱 [為WebSphere建立Windows使用者](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).)
* (Linux、UNIX)使用者可以是root使用者或其他具有root許可權的使用者。 當您在WebSphere上啟用SSL時，請使用此使用者的伺服器識別碼和密碼。

### 為WebSphere建立Linux或UNIX使用者 {#create-a-linux-or-unix-user-for-websphere}

1. 以root使用者身分登入。
1. 在命令提示字元中輸入下列命令以建立使用者：

   * （Linux和Sun Solaris） `useradd`
   * (IBM AIX) `mkuser`

1. 輸入以設定新使用者的密碼 `passwd` 在命令提示字元中。
1. （Linux和Solaris）輸入以建立陰影密碼檔案 `pwconv` （沒有引數）。

   >[!NOTE]
   >
   >（Linux和Solaris）若要讓WebSphere Application Server本機作業系統安全性登入正常運作，陰影密碼檔案必須存在。 陰影密碼檔案通常命名為 **/etc/shadow** 和是根據/etc/passwd檔案。 如果陰影密碼檔案不存在，則在啟用全域安全性並將使用者登入設定為本機作業系統之後會發生錯誤。

1. 在文字編輯器中從/etc目錄開啟群組檔案。
1. 將您在步驟2中建立的使用者新增至 `root` 群組。
1. 儲存並關閉檔案。
1. （啟用SSL的UNIX）以root使用者身分啟動和停止WebSphere。

### 為WebSphere建立Windows使用者 {#create-a-windows-user-for-websphere}

1. 使用系統管理員使用者帳戶登入Windows。
1. 選取 **「開始」 > 「控制檯」 > 「管理工具」 > 「電腦管理」 > 「本機使用者和群組」**.
1. 以滑鼠右鍵按一下「使用者」並選取 **新使用者**.
1. 在適當的方塊中輸入使用者名稱和密碼，並在其他方塊中輸入您需要的任何其他資訊。
1. 取消選取 **使用者必須在下次登入時變更密碼**，按一下 **建立**，然後按一下 **關閉**.
1. 按一下 **使用者**，以滑鼠右鍵按一下您剛建立的使用者並選取 **屬性**.
1. 按一下 **成員隸屬於** 標籤，然後按一下 **新增**.
1. 在「輸入要選取的物件名稱」方塊中，鍵入 `Administrators`，按一下「檢查名稱」以確保群組名稱正確。
1. 按一下 **確定** 然後按一下 **確定** 再來一次。
1. 選取 **「開始」 > 「控制面板」 > 「管理工具」 > 「本機安全性原則」 > 「本機原則」**.
1. 按一下「使用者許可權指派」，然後以滑鼠右鍵按一下「作為作業系統的一部分」，並選取「屬性」。
1. 按一下 **新增使用者或群組**.
1. 在「輸入要選取的物件名稱」方塊中，輸入您在步驟4中建立的使用者名稱，然後按一下 **檢查名稱** 以確保名稱正確，然後按一下 **確定**.
1. 按一下 **確定** 關閉Act As A Operating System屬性對話方塊的一部分。

### 設定WebSphere以使用新建立的使用者作為管理員 {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. 請確定WebSphere正在執行。
1. 在WebSphere管理主控台中，選取 **安全性>全域安全性**.
1. 在「管理安全性」下，選取 **管理使用者角色**.
1. 按一下「新增」並執行下列動作：

   1. 型別 **&amp;ast；** ，然後按一下「搜尋」。
   1. 按一下 **管理員** 在「角色」底下。
   1. 將新建立的使用者新增至對應至角色，並將其對應至管理員。

1. 按一下 **確定** 並儲存您的變更。
1. 重新啟動WebSphere設定檔。

## 啟用管理安全性 {#enable-administrative-security}

1. 在WebSphere管理主控台中，選取 **安全性>全域安全性**.
1. 按一下 **安全性設定精靈**.
1. 確定 **啟用應用程式安全性** 核取方塊已啟用。 单击&#x200B;**下一步**。
1. 選取 **同盟存放庫** 並按一下 **下一個**.
1. 指定您要設定的認證，然後按一下 **下一個**.
1. 按一下 **完成**.
1. 重新啟動WebSphere設定檔。

   WebSphere將開始使用預設金鑰存放區和信任存放區。

## 啟用SSL （自訂金鑰和信任庫） {#enable-ssl-custom-key-and-truststore}

信任存放區和金鑰存放區可以使用ikeyman公用程式或Admin Console來建立。 若要讓ikeyman正常運作，請確保WebSphere安裝路徑不包含括弧。

1. 在WebSphere管理主控台中，選取 **安全性> SSL憑證和金鑰管理**.
1. 按一下 **金鑰存放區和憑證** 在「相關專案」下。
1. 在 **金鑰存放區使用情形** 下拉式清單，確認 **SSL金鑰存放區** 「 」已選取。 按一下 **新增**.
1. 輸入邏輯名稱和說明。
1. 指定您要建立金鑰存放區的路徑。 如果您已透過ikeyman建立金鑰存放區，請指定金鑰存放區檔案的路徑。
1. 指定並確認密碼。
1. 選擇金鑰庫型別並按一下 **套用**.
1. 儲存主組態。
1. 按一下 **個人憑證**.
1. 如果您已新增使用ikeyman建立的金鑰存放區，則會顯示您的憑證。 否則，您需要透過執行以下步驟來新增自我簽署憑證：

   1. 選取 **建立>自我簽署憑證**.
   1. 在憑證表單上指定適當的值。 請確定您保留別名與通用名稱做為電腦的完整網域名稱。
   1. 按一下 **套用**.

1. 重複步驟2到10以建立信任存放區。

## 將自訂金鑰存放區和信任存放區套用至伺服器 {#apply-custom-keystore-and-truststore-to-the-server}

1. 在WebSphere管理主控台中，選取 **安全性> SSL憑證和金鑰管理**.
1. 按一下 **管理端點安全性設定**. 本機拓撲對應隨即開啟。
1. 在輸入下，選取節點的直接子項。
1. 在「相關專案」下，選取 **SSL設定**.
1. 選取 **NodeDefaultSSLSetting**.
1. 從信任庫名稱和金鑰庫名稱下拉式清單中，選取您建立的自訂信任庫和金鑰庫。
1. 按一下 **套用**.
1. 儲存主組態。
1. 重新啟動WebSphere設定檔。

   您的設定檔現在會在自訂SSL設定和您的憑證上執行。

## 啟用AEM表單原生支援 {#enabling-support-for-aem-forms-natives}

1. 在WebSphere管理主控台中，選取 **安全性>全域安全性**.
1. 在驗證區段中，展開 **RMI/IIOP安全性** 並按一下 **CSIv2傳入通訊**.
1. 確定 **支援SSL** 在「傳輸」下拉式清單中選取。
1. 重新啟動WebSphere設定檔。

## 設定WebSphere以轉換以https開頭的URL {#configuring-websphere-to-convert-urls-that-begins-with-https}

若要轉換以https開頭的URL，請將該URL的簽署者憑證新增至WebSphere伺服器。

**為啟用https的網站建立簽署者憑證**

1. 請確定WebSphere正在執行。
1. 在WebSphere管理主控台中，瀏覽至簽署者憑證，然後按一下「安全性> SSL憑證和金鑰管理>金鑰存放區和憑證> NodeDefaultTrustStore >簽署者憑證」。
1. 按一下從連線埠擷取，然後執行下列工作：

   * 在「主機」方塊中，輸入URL。 例如，輸入 `www.paypal.com`.
   * 在「連線埠」方塊中，輸入 `443`. 此連線埠是預設的SSL連線埠。
   * 在「別名」方塊中，鍵入別名。

1. 按一下「擷取簽署者資訊」，然後確認已擷取資訊。
1. 按一下套用，然後按一下儲存。

從已新增憑證的網站進行HTML至PDF轉換後，現在可在產生PDF服務中運作。

>[!NOTE]
>
>應用程式若要從WebSphere內部連線到SSL網站，需要簽署者憑證。 Java Secure Socket Extensions (JSSE)會用它來驗證連線的遠端端在SSL交握期間傳送的憑證。

## 設定動態連線埠 {#configuring-dynamic-ports}

啟用全域安全性時，IBM WebSphere不允許對ORB.init()進行多次呼叫。 如需永久限制的相關資訊，請參閱https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704。

執行以下步驟，將連線埠設定為動態並解決問題：

1. 在WebSphere管理主控台中，選取 **伺服器** > **伺服器型別** > **WebSphere應用程式伺服器**.
1. 在偏好設定區段中，選取您的伺服器。
1. 在 **設定** 標籤，底下 **通訊** 區段，展開 **連線埠**，然後按一下 **詳細資料**.
1. 按一下下列連線埠名稱，變更 **連線埠號碼** 設為0，然後按一下 **確定**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## 設定sling.properties檔案 {#configure-the-sling-properties-file}

1. 開啟 `[aem-forms_root]`\crx-repository\launchpad\sling.properties檔案進行編輯。
1. 找到 `sling.bootdelegation.ibm` 屬性和新增 `com.ibm.websphere.ssl.*`至其值欄位。 更新後的欄位如下所示：

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. 保存文件并重新启动服务器。
