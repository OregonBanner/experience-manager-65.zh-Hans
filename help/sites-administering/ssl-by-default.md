---
title: 默认情况下为SSL
seo-title: 默认情况下为SSL
description: 了解如何在AEM中默认使用SSL。
seo-description: 了解如何在AEM中默认使用SSL。
uuid: 2fbfd020-1d33-4b22-b963-c698e62f5bf6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: 68077369-0549-4c0f-901b-952e323013ea
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---


# 默认情况下，SSL{#ssl-by-default}

为了不断提高AEM的安全性，Adobe引入了一个称为“默认SSL”的功能。 其目的是鼓励使用HTTPS连接到AEM实例。

## 默认情况下启用SSL {#enabling-ssl-by-default}

您可以通过单击AEM主屏幕中的相关收件箱消息来开始默认配置SSL。 要进入收件箱，请按屏幕右上角的铃图标。 然后，单击&#x200B;**视图All**。 这将显示在列表视图中排序的所有警报的列表。

在列表中，选择并打开&#x200B;**配置HTTPS**&#x200B;警报：

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>如果收件箱中不存在&#x200B;**配置HTTPS**&#x200B;警报，您可以通过转到&#x200B;*<http://serveraddress:serverport/libs/granite/security/content/sslConfig.html?item=configuration%2fconfiguressl&_charset_=utf-8>*&#x200B;直接导航到HTTPS向导

已为此功能创建名为&#x200B;**ssl-service**&#x200B;的服务用户。 打开警报后，将引导您完成以下配置向导：

1. 首先，设置存储凭据。 这些是&#x200B;**ssl-service**&#x200B;系统用户密钥存储的凭据，将包含HTTPS监听器的私钥和信任存储。

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. 输入凭据后，单击页面右上角的&#x200B;**下一步**。 然后，上传SSL连接的相关私钥和证书。

   ![chlimage_1-106](assets/chlimage_1-105.png)

   >[!NOTE]
   >
   >有关如何生成私钥和用于向导的证书的信息，请参见下面的[此过程](/help/sites-administering/ssl-by-default.md#generating-a-private-key-certificate-pair-to-use-with-the-wizard)。

1. 最后，指定HTTPS监听器的HTTPS主机名和TCP端口。

   ![screen_shot_2018-07-25at31658pm](assets/screen_shot_2018-07-25at31658pm.png)

## 默认情况下自动执行SSL {#automating-ssl-by-default}

默认情况下，有三种方法可自动执行SSL。

### 通过HTTPPOST{#via-http-post}

第一种方法包括发布到配置向导正在使用的SSLSetup服务器：

```shell
POST /libs/granite/security/post/sslSetup.html
```

您可以在POST中使用以下有效负荷自动配置：

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

Servlet与任何slingPOSTservlet一样，将以200 OK或错误HTTP状态代码做出响应。 您可以在响应的HTML正文中查找有关状态的详细信息。

以下是成功响应和错误的示例。

**成功示例** (status = 200):

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

**错误示例** (status = 500):

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

### 通过包{#via-package}

或者，您也可以通过上传已包含这些必需项的包来自动设置SSL:

* ssl服务用户的密钥库。 它位于存储库的&#x200B;*/home/users/system/security/ssl-service/keystore*&#x200B;下。
* `GraniteSslConnectorFactory`配置

### 生成要与向导{#generating-a-private-key-certificate-pair-to-use-with-the-wizard}一起使用的私钥／证书对

在下面，您将找到一个示例，用于创建SSL向导可使用的DER格式的自签名证书。

>[!NOTE]
>
>自签名证书的使用仅用于示例目的，不应用于生产。

1. 首先，创建私钥：

   ```shell
   openssl genrsa -aes256 -out localhostprivate.key 4096
   openssl rsa -in localhostprivate.key -out localhostprivate.key
   ```

1. 然后，使用私钥生成证书签名请求(CSR):

   ```shell
   openssl req -sha256 -new -key localhostprivate.key -out localhost.csr -subj '/CN=localhost'
   ```

1. 生成SSL证书并使用私钥对其进行签名。 在此示例中，将从现在起一年过期：

   ```shell
   openssl x509 -req -days 365 -in localhost.csr -signkey localhostprivate.key -out localhost.crt
   ```

将私钥转换为DER格式。 这是因为SSL向导要求密钥采用DER格式：

```shell
openssl pkcs8 -topk8 -inform PEM -outform DER -in localhostprivate.key -out localhostprivate.der -nocrypt
```

最后，在本页开头所述的图形SSL向导的步骤2中，将&#x200B;**localhostprivate.der**&#x200B;作为私钥上传，将&#x200B;**localhost.crt**&#x200B;作为SSL证书上传。

### 通过cURL {#updating-the-ssl-configuration-via-curl}更新SSL配置

>[!NOTE]
>
>有关AEM中有用的cURL命令的集中列表，请参阅[将cURL与AEM](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/curl.html)一起使用。

您还可以使用cURL工具自动进行SSL配置。 您可以通过将配置参数发布到此URL来执行此操作：

*https://&lt;serveraddress>:&lt;serverport>/libs/granite/security/post/sslSetup.html*

下面是在配置向导中更改各种设置时可以使用的参数：

* `-F "keystorePassword=password"` -密钥库密码；

* `-F "keystorePasswordConfirm=password"` -确认密钥库密码；

* `-F "truststorePassword=password"` -信任商店密码；

* `-F "truststorePasswordConfirm=password"` -确认信任商店密码；

* `-F "privatekeyFile=@localhostprivate.der"` -指定私钥；

* `-F "certificateFile=@localhost.crt"` -指定证书；

* `-F "httpsHostname=host.example.com"`-指定主机名；
* `-F "httpsPort=8443"` - HTTPS监听器将使用的端口。

>[!NOTE]
>
>运行cURL以自动进行SSL配置的最快方式来自DER和CRT文件所在的文件夹。 或者，也可以在`privatekeyFile`和certificateFile参数中指定完整路径。
>
>您还需要通过身份验证才能执行更新，因此请确保在cURL命令后面附加`-u user:passeword`参数。
>
>正确的cURL post命令应当如下：

```shell
curl -u user:password -F "keystorePassword=password" -F "keystorePasswordConfirm=password" -F "truststorePassword=password" -F "truststorePasswordConfirm=password" -F "privatekeyFile=@localhostprivate.der" -F "certificateFile=@localhost.crt" -F "httpsHostname=host.example.com" -F "httpsPort=8443" https://host:port/libs/granite/security/post/sslSetup.html
```

#### 使用cURL {#multiple-certificates-using-curl}的多个证书

可以通过重复certificateFile参数，将证书链发送给servlet，如下所示：

`-F "certificateFile=@root.crt" -F "certificateFile=@localhost.crt"..`

执行命令后，请验证所有证书是否都已发送到密钥库。 从以下位置检查密钥库：
[http://localhost:4502/libs/granite/security/content/userEditor.html/home/users/system/security/ssl-service](http://localhost:4502/libs/granite/security/content/userEditor.html/home/users/system/security/ssl-service)
