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
source-git-commit: e4d84b5c6f7d2bfcac942b0b685a8f1fd11274f0

---


# 为JBoss Application Server配置SSL {#configuring-ssl-for-jboss-application-server}

要在JBoss Application Server上配置SSL，您需要SSL凭据进行身份验证。 您可以使用Java密钥工具创建凭据或请求，并从证书颁发机构(CA)导入凭据。 然后，必须在JBoss上启用SSL。

您可以使用包含创建密钥库所需的所有信息的单个命令来运行keytool。

在此过程中：

* `[appserver root]` 是运行AEM表单的应用程序服务器的主目录。
* `[type]` 文件夹名称因您执行的安装类型而异。

## 创建SSL凭据 {#create-an-ssl-credential}

1. 在命令提示符下，导航到 *[JAVA HOME]*/bin并键入以下命令以创建凭据和密钥库：

   `keytool -genkey -dname "CN=`*主机名组名称&#x200B;*Group Name Name`, OU=`*Name* State NameState NameNameState Country Code `, O=`*Name *State Contury Code&quot; Key_passwordKeyStorenameRenameChad Ma Mad`,L=`*（主机名称：S）* PareSoneCreSun:PaunSCSSCrPaunCCC `, S=`**`, C=``-alias "AEMForms Cert"``-keyalg RSA -keypass`**`-keystore`**,CCCCSName,CSSCSS,Name，主机名称：Name,C，主机名称：Name,C,Name,C，主机名称：NameNameC,C,C,NameName,`.keystore`

   >[!NOTE]
   >
   >替 `[JAVA_HOME]` 换为安装JDK的目录，并将斜体文本替换为与您的环境相对应的值。 主机名是应用程序服务器的完全限定的域名。

1. 当提示输 `keystore_password` 入密码时，请输入。 密钥库的口令和密钥必须相同。

   >[!NOTE]
   >
   >在此 `keystore_password`*步骤中输入的口令可能与在步骤1中输入的口令相同(key_password)，也可能不同。*

1. 通过键 *入以下命令之一*，将keystorename `[appserver root]/server/[type]/conf` .keystore复制到该目录中：

   * （Windows单台服务器） `copy``keystorename.keystore[appserver root]\standalone\configuration`
   * （Windows服务器群集）副本 `keystorename.keystore[appserver root]\domain\configuration`
   * （Linux单服务器） `cp keystorename.keystore [appserver root]/standalone/configuration`
   * （Linux服务器群集） `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 通过键入以下命令导出证书文件：

   * （单台服务器） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * （服务器群集） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. 在提示输 *入密码时输入keystore_password* 。
1. 通过键入以下命令，将AEMForms_cert.cer文件复制到 *[appserver root]\conf *directory:

   * （Windows单台服务器） `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * （Windows服务器群集） `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * （Linux单服务器） `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * （Linux服务器群集） `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 视图证书的内容，方法是键入以下命令：

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. 要根据需要对中的cacerts文件提供写 `[JAVA_HOME]\jre\lib\security`访问权限，请执行以下任务:

   * (Windows)右键单击cacerts文件并选择“属性”，然后取消选择“只读”属性。
   * (Linux)类型 `chmod 777 cacerts`

1. 通过键入以下命令导入证书：

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_cert *`.cer -keystore`*JAVA_HOME*`\jre\lib\security\cacerts`

1. 键 `changeit` 入密码。 此密码是Java安装的默认密码，系统管理员可能已对其进行更改。
1. 当提示输入 `Trust this certificate? [no]`：时，键入 `yes`。 将显示确认“证书已添加到密钥库”。
1. 如果您通过Workbench的SSL连接，请在Workbench计算机上安装证书。
1. 在文本编辑器中，打开以下文件进行编辑：

   * 单台服务器- `[appserver root]`/standalone/configuration/lc_&lt;dbname/tunklying>.xml

   * 服务器群集- `[appserver root]`/domain/configuration/host.xml

   * 服务器群 `[appserver root]`集-/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **对于单台服务器** ，在lc_&lt;dbaname/tunkey>.xml文件中，在&lt;security-eards>部分后面添加以下内容：

   ```as3
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   找到以 `<server>` 下代码后面的部分：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   将以下内容添加到上述代码后面出现的&lt;server>部分：

   ```
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **对于服务器群集，** 在 [appserver]root \domain\configuration\host.xml中所有节点上，在&lt;security-experds>部分后添加以下内容：

   ```as3
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   在服务器群集的主节点上，在 [appserver]root&lt;dbname>.xml中，找到位于以下代码之后的&lt;server>部分：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   将以下内容添加到上述代码后面出现的&lt;server>部分：

   ```
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. 将属性和属 `keystoreFile` 性的值更改 `keystorePass` 为您在创建keystore时指定的keystore密码。
1. 重新启动应用程序服务器：

   * 对于整套安装：

      * 在Windows控制面板中，单击“管理工具”，然后单击“服务”。
      * 为Adobe Experience Manager表单选择JBoss。
      * 选择“操作”>“停止”。
      * 等待服务状态显示为已停止。
      * 选择“操作”>“开始”。
   * 对于Adobe预配置或手动配置的JBoss安装：

      * 在命令提示符下，导航到 *`[appserver root]`*/bin。
      * 通过输入以下命令停止服务器：

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * 等到JBoss进程完全关闭（当JBoss进程将控制返回到其启动时的终端时）。
      * 开始服务器，方法是输入以下命令：

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. 要使用SSL访问管理控制台，请在Web `https://[host name]:'port'/adminui` 浏览器中键入：

   JBoss的默认SSL端口为8443。 从此处，在访问AEM表单时指定此端口。

## 从CA请求凭据 {#request-a-credential-from-a-ca}

1. 在命令提示符下，导航到 *[JAVA HOME]*/bin并键入以下命令以创建密钥库和密钥：

   `keytool -genkey -dname "CN=`*主机名组名称&#x200B;*Group Name NameState NameNameState`, OU=`*State Name* State NameStateStateNameStateCountryPasswordRenamePasswordReJi `, O=`*-Jod *-Th Jon`, L=`*重命名-KeyKeyKey*`, S=`**`, C=`**`-alias "AEMForms Cert"``-keyalg RSA -keypass`**`-keystore`**ReKeyKeyKeyReKeyKey重命名KeyKeyKeyKeyKeyKey,KeyKeyKey,ReKeyReKeyPandPandRePastSePastPastPareKeyPastPastPastPardPastParePasdPashPassunstPassstPass`.keystore`

   >[!NOTE]
   >
   >替 *`[JAVA_HOME]`* 换为安装JDK的目录，并将斜体文本替换为与您的环境相对应的值。

1. 键入以下命令以生成要发送到证书颁发机构的证书请求：

   `keytool -certreq -alias` “AEMForms Cert”密 `-keystore`*钥重命名&#x200B;*`.keystore -file`*AEMFormscertRequest.csr*

1. 完成证书文件请求后，请完成下一步。

## 使用从CA获取的凭证启用SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. 在命令提示符下，导航到 *`[JAVA HOME]`*/bin并键入以下命令以导入CSR已与之签名的CA的根证书：

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   如果根证书不在浏览器中，也可将其导入浏览器。

   >[!NOTE]
   >
   >替 *`[JAVA_HOME]`换为安装JDK的目录，并将斜体文本替换为与您的环境相对应的值。*

1. 在命令提示符下，导航到 *`[JAVA HOME]`*/bin并键入以下命令以将凭据导入密钥库：

   `keytool -import -trustcacerts -file`*CACertificateName *`.crt -keystore`*关键字重命名*`.keystore`

   >[!NOTE]
   >
   >* 替 `[JAVA_HOME]` 换为安装JDK的目录，并将斜体文本替换为与您的环境相对应的值。
   >* 导入的CA签名证书将替换自签名的公共证书（如果存在）。


1. 完成创建SSL凭证的第13 - 18步。
