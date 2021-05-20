---
title: 为JBoss应用程序服务器配置SSL
seo-title: 为JBoss应用程序服务器配置SSL
description: 了解如何为JBoss应用程序服务器配置SSL。
seo-description: 了解如何为JBoss应用程序服务器配置SSL。
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
exl-id: 8eb4f691-a66b-498e-8114-307221f63718
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# 为JBoss应用程序服务器{#configuring-ssl-for-jboss-application-server}配置SSL

要在JBoss应用程序服务器上配置SSL，您需要SSL凭据进行身份验证。 您可以使用Java密钥工具创建凭据或请求，并从证书颁发机构(CA)导入凭据。 然后，必须在JBoss上启用SSL。

您可以使用包含创建密钥库所需的所有信息的单个命令来运行密钥工具。

在此过程中：

* `[appserver root]` 是运行AEM表单的应用程序服务器的主目录。
* `[type]` 文件夹名称会因您执行的安装类型而异。

## 创建SSL凭据{#create-an-ssl-credential}

1. 在命令提示符下，导航到&#x200B;*[JAVA HOME]*/bin ，然后键入以下命令以创建凭据和密钥库：

   `keytool -genkey -dname "CN=`*主* `, OU=`*机名* `, O=`*组名* `,L=`*称公司名* `, S=`** `, C=`称城市名称国家/地区代码 `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*&quot; key_* `-keystore`*passwordkeystor重命名* `.keystore`

   >[!NOTE]
   >
   >将`[JAVA_HOME]`替换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。 主机名是应用程序服务器的完全限定的域名。

1. 在提示输入密码时输入`keystore_password`。 密钥库和密钥的密码必须相同。

   >[!NOTE]
   >
   >在此步骤输入的`keystore_password` *可能与在步骤1中输入的密码(key_password)相同，也可能不同。*

1. 通过键入以下命令之一，将&#x200B;*keystorename*.keystore复制到`[appserver root]/server/[type]/conf`目录：

   * （Windows单服务器）`copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * （Windows服务器群集）复制`keystorename.keystore[appserver root]\domain\configuration`
   * （Linux单服务器）`cp keystorename.keystore [appserver root]/standalone/configuration`
   * （Linux服务器群集）`cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 通过键入以下命令导出证书文件：

   * （单台服务器）`keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * （服务器群集）`keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. 在提示输入密码时输入&#x200B;*keystore_password*。
1. 通过键入以下命令，将AEMForms_cert.cer文件复制到&#x200B;*[appserver root] \conf*&#x200B;目录中：

   * （Windows单服务器）`copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * （Windows服务器群集）`copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * （Linux单服务器）`cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * （Linux服务器群集）`cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 通过键入以下命令查看证书的内容：

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. 要提供对`[JAVA_HOME]\jre\lib\security`中缓存文件的写访问权限（如果需要），请执行以下任务：

   * (Windows)右键单击缓存文件并选择“属性”，然后取消选择“只读”属性。
   * (Linux)类型`chmod 777 cacerts`

1. 通过键入以下命令导入证书：

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_* `.cer -keystore`*certJAVA_HOME* `\jre\lib\security\cacerts`

1. 键入`changeit`作为密码。 此密码是Java安装的默认密码，系统管理员可能已更改此密码。
1. 提示输入`Trust this certificate? [no]`时，键入`yes`。 将显示确认“Certificate was added to keystore”（证书已添加到密钥库）。
1. 如果您通过Workbench中的SSL连接，请在Workbench计算机上安装证书。
1. 在文本编辑器中，打开以下文件进行编辑：

   * 单个服务器 — `[appserver root]`/standalone/configuration/lc_&lt;dbname/turnkey>.xml

   * 服务器群集 — `[appserver root]`/domain/configuration/host.xml

   * 服务器群集 — `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **对于单台服务器，** 在lc_&lt;dbaname>.xml文件中，在部分后面添加以 &lt;security-realms> 下内容：

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   在以下代码之后找到存在的`<server>`部分：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   将以下内容添加到上述代码后面存在的&lt;server>部分：

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **对于服务器群集，** 在所有节点 [的appserver根]\domain\configuration\host.xml中，在后面添加以下 &lt;security-realms> 部分：

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   在服务器群集的主节点上，在[appserver根]\domain\configuration\domain_&lt;dbname>.xml中，找到以下代码后面存在的&lt;server>部分：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   将以下内容添加到上述代码后面存在的&lt;server>部分：

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. 将`keystoreFile`属性和`keystorePass`属性的值更改为您在创建密钥库时指定的密钥库密码。
1. 重新启动应用程序服务器：

   * 对于统包安装：

      * 在Windows控制面板中，单击“管理工具”，然后单击“服务”。
      * 为Adobe Experience Manager表单选择JBoss。
      * 选择操作>停止。
      * 等待服务状态显示为已停止。
      * 选择操作>开始。
   * 对于Adobe预配置或手动配置的JBoss安装：

      * 在命令提示符下，导航到&#x200B;*`[appserver root]`*/bin。
      * 通过输入以下命令停止服务器：

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * 等待JBoss进程完全关闭（当JBoss进程将控制权返回到其启动的终端时）。
      * 输入以下命令以启动服务器：

         * (Windows)`run.bat -c <profile>`
         * (Linux)`./run.sh -c <profile>`



1. 要使用SSL访问管理控制台，请在Web浏览器中键入`https://[host name]:'port'/adminui`:

   JBoss的默认SSL端口为8443。 从此处访问AEM表单时，请指定此端口。

## 从CA {#request-a-credential-from-a-ca}请求凭据

1. 在命令提示符下，导航到&#x200B;*[JAVA HOME]*/bin ，然后键入以下命令以创建密钥库和密钥：

   `keytool -genkey -dname "CN=`*主* `, OU=`*机名* `, O=`*组名称* `, L=`*公司名称城市* `, S=`** `, C=`*名称州/省/自治区代码*&quot;  `-alias "AEMForms Cert"` `-keyalg RSA -keypass`- *key_* `-keystore`*passwordkeystor重命名* `.keystore`

   >[!NOTE]
   >
   >将&#x200B;*`[JAVA_HOME]`*&#x200B;替换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。

1. 键入以下命令以生成要发送到证书颁发机构的证书请求：

   `keytool -certreq -alias` &quot;AEMForms Cert&quot;  `-keystore`** `.keystore -file`*keystorenameAEMFormscertRequest.csr*

1. 在您的证书文件请求得到满足后，请完成下一个过程。

## 使用从CA获取的凭据启用SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. 在命令提示符下，导航到&#x200B;*`[JAVA HOME]`*/bin并键入以下命令以导入CSR已签名的CA的根证书：

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   如果根证书不在浏览器中，则还应将其导入此处。

   >[!NOTE]
   >
   >将&#x200B;*`[JAVA_HOME]`替换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。*

1. 在命令提示符下，导航到&#x200B;*`[JAVA HOME]`*/bin ，然后键入以下命令以将凭据导入密钥库：

   `keytool -import -trustcacerts -file`** `.crt -keystore`*CACertificateNamekeystorename* `.keystore`

   >[!NOTE]
   >
   >* 将`[JAVA_HOME]`替换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。
   >* 导入的CA签名证书将替换自签名的公共证书（如果存在）。


1. 完成创建SSL凭据的步骤13 - 18。
