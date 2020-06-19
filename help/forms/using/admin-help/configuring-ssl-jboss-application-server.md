---
title: 为JBoss Application Server配置SSL
seo-title: 为JBoss Application Server配置SSL
description: 了解如何为JBoss Application Server配置SSL。
seo-description: 了解如何为JBoss Application Server配置SSL。
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---


# 为JBoss Application Server配置SSL {#configuring-ssl-for-jboss-application-server}

要在JBoss应用程序服务器上配置SSL，您需要SSL凭据进行身份验证。 您可以使用Java密钥工具创建凭据或请求，并从证书颁发机构(CA)导入凭据。 然后，必须在JBoss上启用SSL。

您可以使用包含创建密钥库所需的所有信息的单个命令运行keytool。

在此过程中：

* `[appserver root]` 是运行AEM表单的应用程序服务器的主目录。
* `[type]` 文件夹名称会因您执行的安装类型而异。

## 创建SSL凭据 {#create-an-ssl-credential}

1. 在命令提示符下，导 *[航到JAVA]* HOME/bin并键入以下命令以创建凭据和密钥库：

   `keytool -genkey -dname "CN=`*主机名组&#x200B;*名称`, OU=`** 公司名称 `, O=`*城市名称国&#x200B;*家／地区`,L=`*国家／地区NameState Key_password*`, S=`**`, C=``-alias "AEMForms Cert"``-keyalg RSA -keypass`**`-keystore`*Code ”主密钥重命名&#x200B;*`.keystore`

   >[!NOTE]
   >
   >替 `[JAVA_HOME]` 换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。 主机名是应用程序服务器的完全限定的域名。

1. 在提示 `keystore_password` 输入密码时输入。 密钥库和密钥的密码必须相同。

   >[!NOTE]
   >
   >此 `keystore_password` 步 *骤中输入的密码可能与您在步骤1中输入的密码相同，也可能不同。*

1. 通过键 *入以*&#x200B;下命令之 `[appserver root]/server/[type]/conf` 一，将keystorename.keystore复制到目录：

   * (Windows Single Server) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * （Windows服务器群集）副本 `keystorename.keystore[appserver root]\domain\configuration`
   * （Linux单服务器） `cp keystorename.keystore [appserver root]/standalone/configuration`
   * （Linux服务器群集） `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 通过键入以下命令导出证书文件：

   * （单台服务器） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * （服务器群集） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. 当提示 *输入密码* 时，输入keystore_password。
1. 通过键入以下命令，将AEMForms_cert.cer文 *[件复制到appserver]root *\conf目录：

   * (Windows Single Server) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * （Windows服务器群集） `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * （Linux单服务器） `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * （Linux服务器群集） `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 通过键入以下命令视图证书的内容：

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. 要在中提供对cacerts文件的写入访 `[JAVA_HOME]\jre\lib\security`问权限（如果需要），请执行以下任务:

   * (Windows)右键单击缓存文件并选择“属性”，然后取消选择“只读”属性。
   * (Linux)类型 `chmod 777 cacerts`

1. 通过键入以下命令导入证书：

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_cert *`.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. 键入 `changeit` 作为密码。 此密码是Java安装的默认密码，系统管理员可能已对其进行更改。
1. 当提示输入 `Trust this certificate? [no]`以下内容时，键 `yes`入。 将显示确认“已将证书添加到密钥库”。
1. 如果通过SSL从Workbench连接，请在Workbench计算机上安装证书。
1. 在文本编辑器中，打开以下文件进行编辑：

   * 单台服 `[appserver root]`务器-/standalone/configuration/lc_&lt;dbname/turnkey>.xml

   * 服务器群集- `[appserver root]`/domain/configuration/host.xml

   * 服务器群 `[appserver root]`集-/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **对于单台服务器** ，在lc_&lt;dbaname/tunkey>.xml文件中，在&lt;security-inderds>部分后添加以下内容：

   ```as3
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   找到以 `<server>` 下代码之后出现的部分：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   将以下代码添加到以上代码之后出现的&lt;server>部分：

   ```
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **对于服务器群集** ，在 [appserver]root \domain\configuration\host.xml所有节点上，在&lt;security-indersms>部分后添加以下内容：

   ```as3
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   在服务器群集的主节点上，在 [appserver]root中\domain\configuration\domain_&lt;dbname>.xml找到以下代码之后出现的&lt;server>部分：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   将以下代码添加到以上代码之后出现的&lt;server>部分：

   ```
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. 将属性和属 `keystoreFile` 性的值更 `keystorePass` 改为创建密钥库时指定的密钥库密码。
1. 重新启动应用程序服务器：

   * 对于整套安装：

      * 在Windows控制面板中，单击“管理工具”，然后单击“服务”。
      * 为Adobe Experience Manager表单选择JBoss。
      * 选择“操作”>“停止”。
      * 等待服务状态显示为已停止。
      * 选择“操作”>“开始”。
   * 对于Adobe预配置或手动配置的JBoss安装：

      * 在命令提示符下，导航 *`[appserver root]`*&#x200B;到/bin。
      * 输入以下命令停止服务器：

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * 等到JBoss进程完全关闭（当JBoss进程将控制返回到其启动时的终端时）。
      * 通过输入以下命令开始服务器：

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. 要使用SSL访问管理控制台，请在 `https://[host name]:'port'/adminui` Web浏览器中键入：

   JBoss的默认SSL端口为8443。 从此处访问AEM表单时指定此端口。

## 从CA请求凭据 {#request-a-credential-from-a-ca}

1. 在命令提示符下，导 *[航到JAVA]* HOME/bin并键入以下命令以创建密钥库和密钥：

   `keytool -genkey -dname "CN=`*主机名组名&#x200B;*称组`, OU=`*名称* 城市名称 `, O=`*城市名称&#x200B;*StateState State国家／地区`, L=`**`, S=`**`, C=`**`-alias "AEMForms Cert"``-keyalg RSA -keypass`**`-keystore`*名称“公司密钥重命名密钥密码密钥密码&#x200B;*`.keystore`

   >[!NOTE]
   >
   >替 *`[JAVA_HOME]`* 换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。

1. 键入以下命令以生成要发送到证书颁发机构的证书请求：

   `keytool -certreq -alias` &quot;AEMForms Cert&quot; `-keystore`*keystorename *`.keystore -file`*AEMFormscertRequest.csr*

1. 完成证书文件请求后，请完成下一步。

## 使用从CA获取的凭据启用SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. 在命令提示符下，导 *`[JAVA HOME]`*&#x200B;航到/bin并键入以下命令以导入CSR已与其签名的CA的根证书：

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   如果根证书不在浏览器中，也可将其导入此处。

   >[!NOTE]
   >
   >替 *`[JAVA_HOME]`换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。*

1. 在命令提示符下，导 *`[JAVA HOME]`*&#x200B;航到/bin并键入以下命令以将凭据导入密钥库：

   `keytool -import -trustcacerts -file`*CACertificateName *键`.crt -keystore`*目录重命名* `.keystore`

   >[!NOTE]
   >
   >* 替 `[JAVA_HOME]` 换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。
   >* 导入的CA签名证书将替换自签名的公共证书（如果存在）。


1. 完成创建SSL凭据的步骤13 - 18。
