---
title: 使用AEM 6設定LDAP
description: 瞭解如何使用AEM設定LDAP。
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
exl-id: 2ebca4fb-20f7-499c-96a0-4018eaeddc1a
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 0%

---

# 使用AEM 6設定LDAP {#configuring-ldap-with-aem}

LDAP (此 **L** hightweight **D**&#x200B;目錄 **A**&#x200B;存取 **P** rotocol)用來存取集中式目錄服務。 它有助於減少管理使用者帳戶所需的工作量，因為使用者帳戶可由多個應用程式存取。 Active Directory就是這類LDAP伺服器。 LDAP通常用於實現單一登入，可讓使用者在登入一次後存取多個應用程式。

使用者帳戶可以在LDAP伺服器和存放庫之間同步，而LDAP帳戶詳細資訊會儲存在存放庫中。 此功能允許將帳戶指派給存放庫群組，以配置所需的許可權和許可權。

存放庫會使用LDAP驗證來驗證這類使用者，並將認證傳遞給LDAP伺服器進行驗證，在允許存取存放庫之前需要驗證。 為了改善效能，存放庫可以快取已成功驗證的認證，並且設有到期逾時，以確保在適當的時間段後進行重新驗證。

從LDAP伺服器移除帳戶時，不再授與驗證並拒絕存取存放庫。 儲存於儲存庫中的LDAP帳戶詳細資訊也可以清除。

這類帳戶的使用對使用者而言是透明的。 也就是說，他們發現從LDAP建立的使用者和群組帳戶，與只在存放庫中建立的帳戶之間沒有差異。

在AEM 6中，LDAP支援隨附的新實作需要與舊版不同的設定型別。

所有LDAP設定現在都可作為OSGi設定使用。 這些設定可透過Web管理主控台進行設定，網址為：
`https://serveraddress:4502/system/console/configMgr`

若要讓LDAP與AEM搭配使用，您必須建立三個OSGi設定：

1. LDAP身分提供者(IDP)。
1. 同步處理常式。
1. 外部登入模組。

>[!NOTE]
>
>觀看 [Oak的外部登入模組 — 使用LDAP及以外進行驗證](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-oak-external-login-module-authenticating-with-ldap-and-beyond.html?lang=en) 以深入探究外部登入模組。
>
>若要閱讀使用Apache DS設定Experience Manager的範例，請參閱 [設定Adobe Experience Manager 6.5以使用Apache Directory Service。](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/configuring-adobe-experience-manager-6-to-use-apache-directory/m-p/183805)

## 設定LDAP識別提供者 {#configuring-the-ldap-identity-provider}

LDAP身分提供者用於定義如何從LDAP伺服器擷取使用者。

您可以在管理主控台的 **Apache Jackrabbit Oak LDAP身分提供者** 名稱。

下列組態選項適用於LDAP識別提供者：

<table>
 <tbody>
  <tr>
   <td><strong>LDAP提供者名稱</strong></td>
   <td>此LDAP提供者設定的名稱。</td>
  </tr>
  <tr>
   <td><strong>ldap伺服器主機名稱</strong><br /> </td>
   <td>LDAP伺服器的主機名稱</td>
  </tr>
  <tr>
   <td><strong>LDAP伺服器連線埠</strong></td>
   <td>LDAP伺服器的連線埠</td>
  </tr>
  <tr>
   <td><strong>使用SSL</strong></td>
   <td>指出是否應該使用SSL (LDAP)連線。</td>
  </tr>
  <tr>
   <td><strong>使用TLS</strong></td>
   <td>指出是否應該在連線上啟動TLS。</td>
  </tr>
  <tr>
   <td><strong>停用憑證檢查</strong></td>
   <td>指出是否應該停用伺服器憑證驗證。</td>
  </tr>
  <tr>
   <td><strong>繫結DN</strong></td>
   <td>用於驗證的使用者DN。 如果此欄位留空，則會執行匿名繫結。</td>
  </tr>
  <tr>
   <td><strong>繫結密碼</strong></td>
   <td>用於驗證的使用者密碼</td>
  </tr>
  <tr>
   <td><strong>搜尋逾時</strong></td>
   <td>搜尋逾時前的時間</td>
  </tr>
  <tr>
   <td><strong>管理集區最大使用中</strong></td>
   <td>管理連線集區的作用中大小上限。</td>
  </tr>
  <tr>
   <td><strong>使用者集區最大使用中</strong></td>
   <td>使用者連線集區的作用中大小上限。</td>
  </tr>
  <tr>
   <td><strong>使用者基本DN</strong></td>
   <td>使用者搜尋的DN</td>
  </tr>
  <tr>
   <td><strong>使用者物件類別</strong></td>
   <td>使用者專案必須包含的物件類別清單。</td>
  </tr>
  <tr>
   <td><strong>使用者ID屬性</strong></td>
   <td>包含使用者ID的屬性名稱。</td>
  </tr>
  <tr>
   <td><strong>使用者額外篩選器</strong></td>
   <td>搜尋使用者時要使用的額外LDAP篩選器。 最終篩選的格式如下： '(&amp;(&lt;idattr&gt;=&lt;userid&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)' (user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>使用者DN路徑</strong></td>
   <td>控制是否應該使用DN來計算部分中繼路徑。</td>
  </tr>
  <tr>
   <td><strong>群組基本DN</strong></td>
   <td>群組搜尋的基礎DN。</td>
  </tr>
  <tr>
   <td><strong>群組物件類別</strong></td>
   <td>群組專案必須包含的物件類別清單。</td>
  </tr>
  <tr>
   <td><strong>群組名稱屬性</strong></td>
   <td>包含群組名稱的屬性名稱。</td>
  </tr>
  <tr>
   <td><strong>群組額外篩選器</strong></td>
   <td>搜尋群組時要使用的額外LDAP篩選器。 最終篩選的格式如下： '(&amp;(&lt;nameattr&gt;=&lt;groupname&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>群組DN路徑</strong></td>
   <td>控制是否應該使用DN來計算部分中繼路徑。</td>
  </tr>
  <tr>
   <td><strong>群組成員屬性</strong></td>
   <td>包含一或多個群組成員的群組屬性。</td>
  </tr>
 </tbody>
</table>

## 設定同步處理常式 {#configuring-the-synchronization-handler}

同步處理常式會定義身分提供者使用者和群組如何與存放庫同步。

它位在 **Apache Jackrabbit Oak預設同步處理常式** 管理主控台中的名稱。

同步處理常式可使用下列組態選項：

<table>
 <tbody>
  <tr>
   <td><strong>同步處理常式名稱</strong></td>
   <td>同步設定的名稱。</td>
  </tr>
  <tr>
   <td><strong>使用者到期時間</strong></td>
   <td>同步使用者過期之前的持續時間。</td>
  </tr>
  <tr>
   <td><strong>使用者自動成員資格</strong></td>
   <td>同步的使用者自動新增到的群組清單。</td>
  </tr>
  <tr>
   <td><strong>使用者屬性對應</strong></td>
   <td>來自外部屬性的本機屬性的清單對應定義。</td>
  </tr>
  <tr>
   <td><strong>使用者路徑首碼</strong></td>
   <td>建立使用者時使用的路徑前置詞。</td>
  </tr>
  <tr>
   <td><strong>使用者成員資格到期</strong></td>
   <td>成員資格到期的時間。<br /> </td>
  </tr>
  <tr>
   <td><strong>使用者會籍巢狀深度</strong></td>
   <td>同步成員關係時，傳回群組巢狀的最大深度。 值為0會有效停用群組成員資格查閱。 值1隻會新增使用者的直接群組。 只有在同步使用者成員資格祖先時，同步個別群組時，這個值才無效。</td>
  </tr>
  <tr>
   <td><strong>群組到期時間</strong></td>
   <td>同步群組過期前的持續時間。</td>
  </tr>
  <tr>
   <td><strong>群組自動成員資格</strong></td>
   <td>同步群組自動新增到的群組清單。</td>
  </tr>
  <tr>
   <td><strong>群組屬性對應</strong></td>
   <td>來自外部屬性的本機屬性的清單對應定義。</td>
  </tr>
  <tr>
   <td><strong>群組路徑前置詞</strong></td>
   <td>建立群組時使用的路徑前置詞。</td>
  </tr>
 </tbody>
</table>

## 外部登入模組 {#the-external-login-module}

外部登入模組位於 **Apache Jackrabbit Oak外部登入模組** 在「管理主控台」下。

>[!NOTE]
>
>Apache Jackrabbit Oak外部登入模組實作Java™驗證和授權服務(JAAS)規格。 請參閱 [官方OracleJava™安全性參考指南](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) 以取得詳細資訊。

其工作是定義要使用的身分提供者和同步處理常式，有效地繫結兩個模組。

下列組態選項可供使用：

| **jaas排名** | 指定此登入模組專案的排名（即排序順序）。 專案會以遞減順序排序（也就是說，較高的值排名設定會排在首位）。 |
|---|---|
| **JAAS控制旗標** | 指定LoginModule為REQUIRED、REQUISITE、SUFFIENT或OPTIONAL的屬性。 如需這些標幟涵義的詳細資訊，請參閱JAAS設定檔案。 |
| **JAAS領域** | LoginModule登入時所依據的領域名稱（或應用程式名稱）。 如果未提供領域名稱，則LoginModule會以Felix JAAS組態中設定的預設領域註冊。 |
| **身分提供者名稱** | 身分提供者的名稱。 |
| **同步處理常式名稱** | 同步處理常式的名稱。 |

>[!NOTE]
如果您打算讓AEM執行個體擁有多個LDAP組態，則必須為每個組態建立個別的身分識別提供者與同步處理程式。

## 透過SSL設定LDAP {#configure-ldap-over-ssl}

AEM 6可以設定為透過SSL使用LDAP進行驗證，其程式如下：

1. 檢查 **使用SSL** 或 **使用TLS** 核取方塊 [LDAP身分提供者](#configuring-the-ldap-identity-provider).
1. 根據您的設定，設定同步處理常式和外部登入模組。
1. 視需要在Java™ VM中安裝SSL憑證。 您可以使用keytool完成此安裝：

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. 測試與LDAP伺服器的連線。

### 建立SSL憑證 {#creating-ssl-certificates}

設定AEM透過SSL以LDAP驗證時，可以使用自我簽署憑證。 以下是產生憑證以與AEM搭配使用的工作程式範例。

1. 請確定您已安裝並運作SSL程式庫。 此程式使用OpenSSL作為範例。

1. 建立自訂的OpenSSL設定(cnf)檔案。 此設定可透過複製預設**openssl.cnf**設定檔案並自訂它來完成。 在UNIX®系統上，它位於 `/usr/lib/ssl/openssl.cnf`

1. 在終端機中執行下列命令，繼續建立CA根金鑰：

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. 接下來，建立自我簽署憑證：

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. 若要確定一切正常，請檢查新產生的憑證：

   `openssl x509 -noout -text -in root-ca.crt`

1. 請確定憑證設定(.cnf)檔案中指定的所有資料夾都存在。 如果沒有，請建立它們。
1. 建立隨機種子，例如透過執行：

   `openssl rand -out private/.rand 8192`

1. 將建立的.pem檔案移動到.cnf檔案中設定的位置。

1. 最後，將憑證新增至Java™金鑰存放區。

## 啟用偵錯記錄 {#enabling-debug-logging}

LDAP身分提供者和外部登入模組都可以啟用偵錯記錄，以疑難排解連線問題。

若要啟用偵錯記錄，您必須執行下列動作：

1. 前往「Web管理主控台」。
1. 找到「Apache Sling記錄器設定」並使用以下選項建立兩個記錄器：

* 記錄層級：偵錯
* 記錄檔logs/ldap.log
* 訊息模式： {0，date，dd.MM.yyyy HH:mm:ss.SSS} &amp;ast；{4}&amp;ast； {2} {3} {5}
* 記錄器： org.apache.jackrabbit.oak.security.authentication.ldap

* 記錄層級：偵錯
* 記錄檔：logs/external.log
* 訊息模式： {0，date，dd.MM.yyyy HH:mm:ss.SSS} &amp;ast；{4}&amp;ast； {2} {3} {5}
* 記錄器： org.apache.jackrabbit.oak.spi.security.authentication.external

## 關於群組從屬關係的一句話 {#a-word-on-group-affiliation}

透過LDAP同步的使用者可以屬於AEM中的不同群組。 這些群組可以是外部LDAP群組，這些群組會作為同步程式的一部分新增到AEM。 但是，它們也可以是單獨新增的群組，而不是原始LDAP群組從屬關係方案的一部分。

通常，這些群組是由本機AEM管理員或任何其他身分提供者所新增。

如果從LDAP伺服器上的群組移除使用者，則同步處理時變更會反映在AEM端。 但是，使用者未由LDAP新增的所有其他群組關聯仍會保留在原處。

AEM會使用，偵測並處理使用者從外部群組中清除作業。 `rep:externalId` 屬性。 此屬性會自動新增至同步處理常式同步的任何使用者或群組，且包含原始身分提供者的相關資訊。

請參閱Apache Oak檔案於 [使用者和群組同步](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## 已知问题 {#known-issues}

如果您打算使用LDAP over SSL，請確定您使用的憑證是在沒有Netscape註解選項的情況下建立的。 如果啟用此選項，驗證會失敗並出現SSL交握錯誤。
