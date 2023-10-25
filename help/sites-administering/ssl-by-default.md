---
title: 默认为SSL/TLS
seo-title: SSL/TLS By Default
description: 了解如何在AEM 6.5中使用默认的SSL功能。
seo-description: Learn how to use SSL by Default in AEM.
uuid: 2fbfd020-1d33-4b22-b963-c698e62f5bf6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: 68077369-0549-4c0f-901b-952e323013ea
docset: aem65
exl-id: 574e2fc2-6ebf-49b6-9b65-928237a8a34d
source-git-commit: e54c1d422f2bf676e8a7b0f50a101e495c869c96
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# 默认为SSL/TLS{#ssl-tls-by-default}

为了不断提高AEM的安全性，Adobe引入了一项默认称为SSL的功能。 其目的是鼓励使用HTTPS连接到AEM实例。

## 默认启用SSL/TLS {#enabling-ssl-tls-by-default}

您可以从AEM主屏幕单击相关的收件箱消息以开始默认配置SSL/TLS。 要访问收件箱，请按屏幕右上角的铃铛图标。 然后，单击 **查看全部**. 这将显示一个列表，其中包含以列表视图排序的所有警报。

在列表中，选择并打开 **配置HTTPS** 警报：

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>如果 **配置HTTPS** 收件箱中不存在警报，您可以通过转到 *<http://serveraddress:serverport/libs/granite/security/content/sslConfig.html?item=configuration%2fconfiguressl&_charset_=utf-8>*

名为的服务用户 **ssl服务** 已为此功能创建。 打开警报后，系统将引导您完成以下配置向导：

1. 首先，设置存储凭据。 这些是 **ssl服务** 系统用户的密钥存储，将包含HTTPS侦听器的私钥和信任存储。

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. 输入凭据后，单击 **下一个** （在页面的右上角）。 然后，为SSL/TLS连接上传关联的私钥和证书。

   ![chlimage_1-105](assets/chlimage_1-105.png)

   >[!NOTE]
   >
   >有关如何生成要用于向导的私钥和证书的信息，请参阅 [此过程](/help/sites-administering/ssl-by-default.md#generating-a-private-key-certificate-pair-to-use-with-the-wizard) 下。

1. 最后，指定HTTPS侦听器的HTTPS主机名和TCP端口。

   ![screen_shot_2018-07-25at31658pm](assets/screen_shot_2018-07-25at31658pm.png)

## 默认情况下，自动化SSL/TLS {#automating-ssl-tls-by-default}

默认情况下，有三种方法可自动化SSL/TLS。

### 通过HTTPPOST {#via-http-post}

第一种方法是发布到配置向导正在使用的SSLSetup服务器：

```shell
POST /libs/granite/security/post/sslSetup.html
```

您可以在POST中使用以下有效负载来自动进行配置：

```xml
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePassword"

test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePassword"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="privatekeyFile"; filename="server.der"
Content-Type: application/x-x509-ca-cert

------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="certificateFile"; filename="server.crt"
Content-Type: application/x-x509-ca-cert

------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="httpsPort"
8443
```

此servlet与任何slingPOSTservlet一样，将使用“200确定”或错误HTTP状态代码进行响应。 您可以在响应的HTML正文中找到有关状态的详细信息。

以下是成功响应和错误的示例。

**成功示例** （状态= 200）：

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>OK</title>
</head>
<body>
<h1>OK</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>200</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>SSL successfully configured</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>OK</dd>
<dt class='foundation-form-response-description'>Description</dt>
<dd>HTTPS has been configured on port 8443. The private key and
certificate were stored in the key store of the user ssl-service.
Please take note of the key store password you provided. You will need
it for any subsequent updating of the private key or certificate.</dd>
</dl>
<h2>Links</h2>
<ul class='foundation-form-response-links'>
<li><a class='foundation-form-response-redirect' href='/'>Done</a></li>
</ul>
</body>
</html>
```

**错误示例** （状态= 500）：

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>Error</title>
</head>
<body>
<h1>Error</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>500</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>The provided file is not a valid key, DER format expected</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>Error</dd>
</dl>
</body>
</html>
```

### 通过包 {#via-package}

或者，您可以通过上传已包含这些必需项目的包来自动化SSL/TLS设置：

* ssl服务用户的密钥库。 该文件位于 */home/users/system/security/ssl-service/keystore* 在存储库中。
* 此 `GraniteSslConnectorFactory` 配置

### 生成要用于向导的私钥/证书对 {#generating-a-private-key-certificate-pair-to-use-with-the-wizard}

下面您将找到一个示例，用于创建SSL/TLS向导可以使用的DER格式的自签名证书。 基于操作系统安装OpenSSL，打开OpenSSL命令提示符，并将目录更改为要生成私钥/证书的文件夹。

>[!NOTE]
>
>自签名证书的使用仅用于示例目的，不应在生产中使用。

1. 首先，创建私钥：

   ```shell
   openssl genrsa -aes256 -out localhostprivate.key 4096
   openssl rsa -in localhostprivate.key -out localhostprivate.key
   ```

1. 然后，使用私钥生成证书签名请求(CSR)：

   ```shell
   openssl req -sha256 -new -key localhostprivate.key -out localhost.csr -subj "/CN=localhost"
   ```

1. 生成SSL/TLS证书并使用私钥签名。 在此示例中，将从现在起一年后过期：

   ```shell
   openssl x509 -req -days 365 -in localhost.csr -signkey localhostprivate.key -out localhost.crt
   ```

将私钥转换为DER格式。 这是因为SSL向导要求密钥为DER格式：

```shell
openssl pkcs8 -topk8 -inform PEM -outform DER -in localhostprivate.key -out localhostprivate.der -nocrypt
```

最后，上传 **localhostprivate.der** 作为私钥和 **localhost.crt** 如本页开头描述的图形SSL/TLS向导步骤2中的SSL/TLS证书一样。

### 通过cURL更新SSL/TLS配置 {#updating-the-ssl-tls-configuration-via-curl}

>[!NOTE]
>
>请参阅 [在AEM中使用cURL](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/curl.html) 以集中显示AEM中有用的cURL命令列表。

您还可以使用cURL工具自动配置SSL/TLS。 为此，您可以将配置参数发布到此URL：

*https://&lt;serveraddress>：&lt;serverport>/libs/granite/security/post/sslSetup.html*

以下是可用于更改配置向导中各种设置的参数：

* `-F "keystorePassword=password"`  — 密钥库密码；

* `-F "keystorePasswordConfirm=password"`  — 确认密钥库密码；

* `-F "truststorePassword=password"`  — 信任库密码；

* `-F "truststorePasswordConfirm=password"`  — 确认信任库密码；

* `-F "privatekeyFile=@localhostprivate.der"`  — 指定私钥；

* `-F "certificateFile=@localhost.crt"`  — 指定证书；

* `-F "httpsHostname=host.example.com"` — 指定主机名；
* `-F "httpsPort=8443"` - HTTPS侦听器将处理的端口。

>[!NOTE]
>
>运行cURL以自动化SSL/TLS配置的最快方式来自DER和CRT文件所在的文件夹。 或者，您可以在 `privatekeyFile` 和certificateFile参数。
>
>您还需要进行身份验证才能执行更新，因此请确保将cURL命令附加到 `-u user:passeword` 参数。
>
>正确的cURL post命令应如下所示：

```shell
curl -u user:password -F "keystorePassword=password" -F "keystorePasswordConfirm=password" -F "truststorePassword=password" -F "truststorePasswordConfirm=password" -F "privatekeyFile=@localhostprivate.der" -F "certificateFile=@localhost.crt" -F "httpsHostname=host.example.com" -F "httpsPort=8443" https://host:port/libs/granite/security/post/sslSetup.html
```

#### 使用cURL的多个证书 {#multiple-certificates-using-curl}

您可以通过重复certificateFile参数，向servlet发送证书链，如下所示：

`-F "certificateFile=@root.crt" -F "certificateFile=@localhost.crt"..`

执行命令后，验证所有证书是否都进入密钥库。 查看 **密钥库** 条目来源：
[http://localhost:4502/libs/granite/security/content/v2/usereditor.html/home/users/system/security/ssl-service](http://localhost:4502/libs/granite/security/content/v2/usereditor.html/home/users/system/security/ssl-service)

### 启用TLS 1.3连接 {#enabling-tls-connection}

1. 转到Web控制台
1. 然后，导航到 **osgi** - **配置** - **AdobeGranite SSL连接器工厂**
1. 转到 **包含的密码套件** 字段并添加以下条目。 您可以通过按“**+**”按钮，在中添加每个按钮后：

   * `TLS_AES_256_GCM_SHA384`
   * `TLS_AES_128_GCM_SHA256`
   * `TLS_CHACHA20_POLY1305_SHA256`
   * `TLS_AES_128_CCM_SHA256`
   * `TLS_AES_128_CCM_8_SHA256`