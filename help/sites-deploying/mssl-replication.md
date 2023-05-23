---
title: 使用雙向SSL復寫
seo-title: Replicating Using Mutual SSL
description: 瞭解如何設定AEM，讓製作執行個體上的復寫代理程式使用雙向SSL (MSSL)來與發佈執行個體連線。 使用MSSL時，發佈執行個體上的復寫代理程式和HTTP服務會使用憑證來相互驗證。
seo-description: Learn how to configure AEM so that a replication agent on the author instance uses mutual SSL (MSSL) to connect with the publish instance. Using MSSL, the replication agent and the HTTP service on the publish instance use certificates to authenticate each other.
uuid: f4bc5e61-a58c-4fd2-9a24-b31e0c032c15
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 8bc307d9-fa5c-44c0-bff9-2d68d32a253b
feature: Configuring
exl-id: 0a8d7831-d076-45cf-835c-8063ee13d6ba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 3%

---

# 使用雙向SSL復寫{#replicating-using-mutual-ssl}

設定AEM，讓製作執行個體上的復寫代理程式使用雙向SSL (MSSL)來與發佈執行個體連線。 使用MSSL時，發佈執行個體上的復寫代理程式和HTTP服務會使用憑證來相互驗證。

設定MSSL進行復寫需要執行下列步驟：

1. 建立或取得製作和發佈執行個體的私密金鑰和憑證。
1. 在製作和發佈執行個體上安裝金鑰和憑證：

   * 作者：作者的私密金鑰和發佈者的憑證。
   * 發佈：發佈的私密金鑰和作者的憑證。 憑證與透過復寫代理程式驗證的使用者帳戶相關聯。

1. 在發佈執行個體上設定Jetty型HTTP服務。
1. 設定復寫代理程式的傳輸和SSL屬性。

![chlimage_1-64](assets/chlimage_1-64.png)

您必須判斷執行復寫的使用者帳戶。 在發佈執行個體上安裝信任的作者憑證時，該憑證會與此使用者帳戶相關聯。

## 取得或建立MSSL的認證 {#obtaining-or-creating-credentials-for-mssl}

您需要製作和發佈執行個體的私密金鑰和公開憑證：

* 私密金鑰必須包含在pkcs#12或JKS格式中。
* 憑證必須包含在pkcs#12或JKS格式中。 此外，「CER」格式中包含的憑證也可以新增到Granite Truststore。
* 憑證可以由可辨識的CA自我簽署或簽署。

### JKS格式 {#jks-format}

產生JKS格式的私密金鑰和憑證。 私密金鑰儲存在KeyStore檔案中，而憑證儲存在TrustStore檔案中。 使用 [Java `keytool`](https://docs.oracle.com/javase/7/docs/technotes/tools/solaris/keytool.html) 以建立兩者。

使用Java執行以下步驟 `keytool` 若要建立私密金鑰和認證：

1. 在KeyStore中產生私密與公開金鑰組。
1. 建立或取得憑證：

   * 自行簽署：從KeyStore匯出憑證。
   * CA簽署：產生憑證要求並將其傳送至CA。

1. 將憑證匯入TrustStore。

使用以下程式，為作者和發佈執行個體建立私密金鑰和自簽憑證。 請相應地使用不同的命令選項值。

1. 開啟命令列視窗或終端機。 若要建立私人 — 公開金鑰組，請使用下表中的選項值輸入以下命令：

   ```shell
   keytool -genkeypair -keyalg RSA -validity 3650 -alias alias -keystore keystorename.keystore  -keypass key_password -storepass  store_password -dname "CN=Host Name, OU=Group Name, O=Company Name,L=City Name, S=State, C=Country_ Code"
   ```

   | 选项 | 创作 | 发布 |
   |---|---|---|
   | -alias | 作者 | 发布 |
   | -keystore | author.keystore | publish.keystore |

1. 若要匯出憑證，請使用下表中的選項值輸入以下命令：

   ```shell
   keytool -exportcert -alias alias -file cert_file -storetype jks -keystore keystore -storepass store_password
   ```

   | 选项 | 创作 | 发布 |
   |---|---|---|
   | -alias | 作者 | 发布 |
   | -file | author.cer | publish.cer |
   | -keystore | author.keystore | publish.keystore |

### pkcs#12格式 {#pkcs-format}

產生pkcs#12格式的私密金鑰和憑證。 使用 [openSSL](https://www.openssl.org/) 以產生這些變數。 使用以下程式來產生私密金鑰和憑證要求。 若要取得憑證，請使用您的私密金鑰（自我簽署憑證）簽署要求，或傳送要求給CA。 然後，產生包含私密金鑰和憑證的pkcs#12封存。

1. 開啟命令列視窗或終端機。 若要建立私密金鑰，請使用下表中的選項值輸入以下命令：

   ```shell
   openssl genrsa -out keyname.key 2048
   ```

   | 选项 | 创作 | 发布 |
   |---|---|---|
   | -out | author.key | publish.key |

1. 若要產生憑證要求，請使用下表中的選項值，輸入下列命令：

   ```shell
   openssl req -new -key keyname.key -out key_request.csr
   ```

   | 选项 | 创作 | 发布 |
   |---|---|---|
   | -key | author.key | publish.key |
   | -out | author_request.csr | publish_request.csr |

   請簽署憑證要求或傳送要求給CA。

1. 若要簽署憑證要求，請使用下表中的選項值，輸入下列命令：

   ```shell
   openssl x509 -req -days 3650 -in key_request.csr -signkey keyname.key -out certificate.cer
   ```

   | 选项 | 创作 | 发布 |
   |---|---|---|
   | -signkey | author.key | publish.key |
   | -中的 | author_request.csr | publish_request.csr |
   | -out | author.cer | publish.cer |

1. 若要將您的私密金鑰和簽署的憑證新增至pkcs#12檔案，請使用下表中的選項值輸入以下命令：

   ```shell
   openssl pkcs12 -keypbe PBE-SHA1-3DES -certpbe PBE-SHA1-3DES -export -in certificate.cer -inkey keyname.key -out pkcs12_archive.pfx -name "alias"
   ```

   | 选项 | 创作 | 发布 |
   |---|---|---|
   | -inkey | author.key | publish.key |
   | -out | author.pfx | publish.pfx |
   | -中的 | author.cer | publish.cer |
   | -name | 作者 | 发布 |

## 在作者上安裝私密金鑰和TrustStore {#install-the-private-key-and-truststore-on-author}

在作者執行個體上安裝下列專案：

* 作者執行個體的私密金鑰。
* 發佈執行個體的憑證。

若要執行下列程式，您必須以作者執行個體的管理員身分登入。

### 安裝作者私密金鑰 {#install-the-author-private-key}

1. 開啟作者執行個體的「使用者管理」頁面。 ([http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html))
1. 若要開啟使用者帳戶的屬性，請按一下或點選您的使用者名稱。
1. 如果「帳戶設定」區域中出現「建立KeyStore」連結，請按一下連結。 設定密碼，然後按一下「確定」。
1. 在「帳戶設定」區域中，按一下「管理金鑰存放區」。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 按一下「從金鑰庫檔案新增私密金鑰」。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 按一下「選取金鑰庫檔案」，然後瀏覽並選取author.keystore檔案或author.pfx檔案（如果使用pkcs#12），然後按一下「開啟」。
1. 輸入金鑰存放區的別名和密碼。 輸入私密金鑰的別名和密碼，然後按一下送出。
1. 關閉[KeyStore管理]對話方塊。

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 安裝發佈憑證 {#install-the-publish-certificate}

1. 開啟作者執行個體的「使用者管理」頁面。 ([http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html))
1. 若要開啟使用者帳戶的屬性，請按一下或點選您的使用者名稱。
1. 如果[Create TrustStore]連結出現在[Account Settings]區域中，請按一下該連結，為TrustStore建立密碼，然後按一下[OK]。
1. 在「帳戶設定」區域中，按一下「管理TrustStore」。
1. 按一下「從CER檔案新增憑證」。

   ![chlimage_1-68](assets/chlimage_1-68.png)

1. 清除將憑證對應至使用者選項。 按一下「選取憑證檔案」，選取「publish.cer」，然後按一下「開啟」。
1. 關閉[TrustStore管理]對話方塊。

   ![chlimage_1-69](assets/chlimage_1-69.png)

## 在發佈時安裝私密金鑰和TrustStore {#install-private-key-and-truststore-on-publish}

在發佈執行個體上安裝下列專案：

* 發佈執行個體的私密金鑰。
* 作者執行個體的憑證。 將憑證與用來執行復寫請求的使用者建立關聯。

若要執行下列程式，您必須以發佈執行個體的管理員身分登入。

### 安裝發佈私密金鑰 {#install-the-publish-private-key}

1. 開啟發佈執行個體的「使用者管理」頁面。 ([http://localhost:4503/libs/granite/security/content/useradmin.html](http://localhost:4503/libs/granite/security/content/useradmin.html))
1. 若要開啟使用者帳戶的屬性，請按一下或點選您的使用者名稱。
1. 如果「帳戶設定」區域中出現「建立KeyStore」連結，請按一下連結。 設定密碼，然後按一下「確定」。
1. 在「帳戶設定」區域中，按一下「管理金鑰存放區」。
1. 按一下「從金鑰庫檔案新增私密金鑰」。
1. 按一下「選取金鑰庫檔案」，然後瀏覽並選取publish.keystore檔案或publish.pfx檔案（如果使用pkcs#12），然後按一下「開啟」。
1. 輸入金鑰存放區的別名和密碼。 輸入私密金鑰的別名和密碼，然後按一下送出。
1. 關閉[KeyStore管理]對話方塊。

### 安裝作者憑證 {#install-the-author-certificate}

1. 開啟發佈執行個體的「使用者管理」頁面。 ([http://localhost:4503/libs/granite/security/content/useradmin.html](http://localhost:4503/libs/granite/security/content/useradmin.html))
1. 找到您用來執行復寫請求的使用者帳戶，然後按一下或點選使用者名稱。
1. 如果[Create TrustStore]連結出現在[Account Settings]區域中，請按一下該連結，為TrustStore建立密碼，然後按一下[OK]。
1. 在「帳戶設定」區域中，按一下「管理TrustStore」。
1. 按一下「從CER檔案新增憑證」。
1. 請確定已選取將憑證對應至使用者選項。 按一下「選取憑證檔案」，選取「author.cer」，然後按一下「開啟」。
1. 按一下提交，然後關閉「信任庫管理」對話方塊。

## 在發佈上設定HTTP服務 {#configure-the-http-service-on-publish}

在發佈執行個體上設定Apache Felix Jetty型HTTP服務的屬性，以便在存取Granite Keystore時使用HTTPS。 服務的PID為 `org.apache.felix.http`.

下表列出您在設定是否使用Web主控台時需要設定的OSGi屬性。

| Web主控台上的屬性名稱 | OSGi 属性名称 | 价值 |
|---|---|---|
| 啟用HTTPS | org.apache.felix.https.enable | true |
| 啟用HTTPS以使用Granite KeyStore | org.apache.felix.https.use.granite.keystore | true |
| HTTPS 端口 | org.osgi.service.http.port.secure | 8443 （或其他需要的連線埠） |
| 使用者端憑證 | org.apache.felix.https.clientcertificate | 「需要使用者端憑證」 |

## 在作者上設定復寫代理 {#configure-the-replication-agent-on-author}

在製作執行個體上設定復寫代理程式，以便在連線至發佈執行個體時使用HTTPS通訊協定。 如需設定復寫代理的完整資訊，請參閱 [設定您的復寫代理](/help/sites-deploying/replication.md#configuring-your-replication-agents).

若要啟用MSSL，請根據下表在「傳輸」標籤上設定屬性：

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>价值</th>
  </tr>
  <tr>
   <td>URI</td>
   <td><p>https://server_name:SSL_port/bin/receive?sling:authRequestLogin=1</p> <p>例如：</p> <p>http://localhost:8443/bin/receive?sling:authRequestLogin=1</p> </td>
  </tr>
  <tr>
   <td>用户</td>
   <td>無值</td>
  </tr>
  <tr>
   <td>密码</td>
   <td>無值</td>
  </tr>
  <tr>
   <td>SSL</td>
   <td>客户端身份验证</td>
  </tr>
 </tbody>
</table>

![chlimage_1-70](assets/chlimage_1-70.png)

設定復寫代理程式之後，請測試連線以判斷MSSL設定是否正確。

```xml
29.08.2014 14:02:46 - Create new HttpClient for Default Agent
29.08.2014 14:02:46 - * HTTP Version: 1.1
29.08.2014 14:02:46 - * Using Client Auth SSL configuration *
29.08.2014 14:02:46 - adding header: Action:Test
29.08.2014 14:02:46 - adding header: Path:/content
29.08.2014 14:02:46 - adding header: Handle:/content
29.08.2014 14:02:46 - deserialize content for delivery
29.08.2014 14:02:46 - No message body: Content ReplicationContent.VOID is empty
29.08.2014 14:02:46 - Sending POST request to http://localhost:8443/bin/receive?sling:authRequestLogin=1
29.08.2014 14:02:46 - sent. Response: 200 OK
29.08.2014 14:02:46 - ------------------------------------------------
29.08.2014 14:02:46 - Sending message to localhost:8443
29.08.2014 14:02:46 - >> POST /bin/receive HTTP/1.0
29.08.2014 14:02:46 - >> Action: Test
29.08.2014 14:02:46 - >> Path: /content
29.08.2014 14:02:46 - >> Handle: /content
29.08.2014 14:02:46 - >> Referer: about:blank
29.08.2014 14:02:46 - >> Content-Length: 0
29.08.2014 14:02:46 - >> Content-Type: application/octet-stream
29.08.2014 14:02:46 - --
29.08.2014 14:02:46 - << HTTP/1.1 200 OK
29.08.2014 14:02:46 - << Connection: Keep-Alive
29.08.2014 14:02:46 - << Server: Day-Servlet-Engine/4.1.64
29.08.2014 14:02:46 - << Content-Type: text/plain;charset=utf-8
29.08.2014 14:02:46 - << Content-Length: 26
29.08.2014 14:02:46 - << Date: Fri, 29 Aug 2014 18:02:46 GMT
29.08.2014 14:02:46 - << Set-Cookie: login-token=3529326c-1500-4888-a4a3-93d299726f28%3ac8be86c6-04bb-4d18-80d6-91278e08d720_98797d969258a669%3acrx.default; Path=/; HttpOnly; Secure
29.08.2014 14:02:46 - << Set-Cookie: cq-authoring-mode=CLASSIC; Path=/; Secure
29.08.2014 14:02:46 - <<
29.08.2014 14:02:46 - << R
29.08.2014 14:02:46 - << eplicationAction TEST ok.
29.08.2014 14:02:46 - Message sent.
29.08.2014 14:02:46 - ------------------------------------------------
29.08.2014 14:02:46 - Replication (TEST) of /content successful.
Replication test succeeded
```
