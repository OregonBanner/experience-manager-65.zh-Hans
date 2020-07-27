---
title: 为WebLogic服务器配置SSL
seo-title: 为WebLogic服务器配置SSL
description: 了解如何创建用于WebLogic服务器的SSL凭据，以及如何为WebLogic服务器配置SSL。
seo-description: 了解如何创建用于WebLogic服务器的SSL凭据，以及如何为WebLogic服务器配置SSL。
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---


# 为WebLogic服务器配置SSL {#configuring-ssl-for-weblogic-server}

要在WebLogic服务器上配置SSL，您需要SSL凭据进行身份验证。 您可以使用Java密钥工具执行以下任务来创建凭据：

* 创建公钥／私钥对，将公钥包含在作为单元素证书链存储的X.509 v1自签名证书中，然后将证书链和私钥存储在新密钥库中。 此密钥库是应用程序服务器的自定义标识密钥库。
* 提取证书并将其插入新密钥库。 此密钥库是应用程序服务器的自定义信任密钥库。

然后，配置WebLogic，使其使用您创建的自定义标识密钥库和自定义信任密钥库。 另外，禁用WebLogic主机名验证功能，因为用于创建密钥库文件的可分辨名称不包含承载WebLogic的计算机的名称。

## 创建用于WebLogic服务器的SSL凭据 {#creating-an-ssl-credential-for-use-on-weblogic-server}

keytool命令通常位于Java jre/bin目录中，并且必须包括多个选项和选项值，这些选项和选项值列在下表中。

<table>
 <thead>
  <tr>
   <th><p>Keytool选项</p></th>
   <th><p>描述</p></th>
   <th><p>选项值</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>-alias</p></td>
   <td><p>密钥库的别名。</p></td>
   <td>
    <ul>
     <li><p>自定义标识密钥库： <code>ads-credentials</code></p></li>
     <li><p>自定义信任密钥库： <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>用于生成密钥对的算法。</p></td>
   <td><p>RSA</p><p>根据公司的策略，您可以使用不同的算法。</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>密钥库文件的位置和名称。</p><p>该位置可以包含文件的绝对路径。 或者，它可以相对于输入keytool命令的命令提示符的当前目录。</p></td>
   <td>
    <ul>
     <li><p>自定义标识密钥库： <code>[</code><i>appserverdomain]</i><code>/adobe/</code><i>[服务器名称]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>自定义信任密钥库： <code>[</code><i>appserverdomain]</i><code>/adobe/</code><i>[服务器名称]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>证书文件的位置和名称。</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-validity</p></td>
   <td><p>认为证书有效的天数。</p></td>
   <td><p>3650</p><p>您可以根据公司的策略使用不同的值。</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>保护密钥库内容的密码。 </p></td>
   <td>
    <ul>
     <li><p>自定义标识密钥库： 密钥库密码必须与为管理控制台的信任存储组件指定的SSL凭据密码相对应。</p></li>
     <li><p>自定义信任密钥库： 使用与用于自定义身份密钥库的口令相同的口令。</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>保护密钥对的私钥的密码。</p></td>
   <td><p>使用与选项所用的口令相 <code>-storepass</code> 同的口令。 密钥密码必须至少为6个字符。</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>标识密钥库所有者的可分辨名称。</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> 是拥有密钥库的用户的标识。</p></li>
     <li><p><code><i>[Group Name]</i></code> 是密钥库所有者所属的公司组的标识。</p></li>
     <li><p><code><i>[Company Name]</i></code> 是您组织的名称。</p></li>
     <li><p><code><i>[City Name]</i></code> 是您的组织所在的城市。</p></li>
     <li><p><code><i>[State or province]</i></code> 是您的组织所在的州或省。</p></li>
     <li><p><code><i>[Country Code]</i></code> 是贵组织所在国家／地区的双字母代码。</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

有关使用keytool命令的详细信息，请参阅JDK文档中的keytool.html文件。

## 创建自定义标识和信任密钥库 {#create-the-custom-identity-and-trust-keystores}

1. 在命令提示符下，导 *[航到appserverdomain]*/adobe/*[server name]*。
1. 输入以下命令：

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >替 `[JAVA_HOME]`*换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   名为“ads-credentials.jks”的自定义标识密钥库文件在appserverdomain [/adobe/server name目]录中创[建] 出来。

1. 输入以下命令，从ads-credentials密钥库提取证书：

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**password**

   >[!NOTE]
   >
   >替 `[JAVA_HOME]` 换为安装JDK的目录，并将_ `store`**替换为自定义&#x200B;*`password`标识密钥库的口令。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   名为“ads-ca.cer”的证书文件在appserverdomain [/adobe]/server name目&#x200B;[*录中创建*] 。

1. 将ads-ca.cer文件复制到需要与应用程序服务器进行安全通信的任何主机。
1. 通过输入以下命令将证书插入新密钥库文件（自定义信任密钥库）:

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >替换 `[JAVA_HOME]` 为安装JDK的目录，并用您自 `store`*己的密码替&#x200B;*换_和`password`_`key`**`password`*。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

名为“ads-ca.jks”的自定义信任密钥库文件在appserverdomain []/adobe/&#39;server&#39;目录中创建。

配置WebLogic，以使其使用您创建的自定义标识密钥库和自定义信任密钥库。 另外，禁用WebLogic主机名验证功能，因为用于创建密钥库文件的可分辨名称不包括承载WebLogic服务器的计算机的名称。

## 将WebLogic配置为使用SSL {#configure-weblogic-to-use-ssl}

1. 开始WebLogic服务器管理控制台， `https://`*[方法是&#x200B;]*`:7001/console`在Web浏览器的URL行中键入主机名。
1. 在“环境”下的“域配置”中， **选择“服务器”>“服务器”>“配置”>“常规**”。
1. 在“常规”下，在“配置”中 **，确保选择“启** 用监听端口 **”** 和“启用SSL监听端口”。 如果未启用，请执行以下操作：

   1. 在“更改中心”下，单 **击“锁定并编辑** ”以修改选择和值。
   1. 选中“ **启用监听端口** ”和 **“启用SSL监听端口** ”复选框。

1. 如果此服务器是受控服务器，请将“侦听端口”更改为未使用的端口值（如8001），将“SSL侦听端口”更改为未使用的端口值（如8002）。 在独立服务器上，默认SSL端口为7002。
1. 单击“ **释放配置**”。
1. 在“环境”下，在“域配置”中， **单击“服务&#x200B;[*器”>“托管服务器*]”>“配置”>“常规”**。
1. 在“常规”下的“配置”中，选择“ **密钥存储**”。
1. 在“更改中心”下，单 **击“锁定并编辑** ”以修改选择和值。
1. 单 **击** “更改”以将密钥库列表作为下拉列表，然后选择“自 **定义标识和自定义信任”**。
1. 在“标识”下，指定以下值：

   **自定义标识密钥库**: *[appserverdomain]*/adobe/*[server name]*/ads-credentials.jks，其中*[appserverdomain] *是实际路径， *[服务器名称]* 是应用服务器的名称。

   **自定义标识密钥库类型**: JKS

   **自定义标识密钥库密码**: *mypassword* （自定义标识密钥库密码）

1. 在“信任”下，指定以下值：

   **自定义信任密钥库文件名**: `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`，其中 `*[appserverdomain]*` 是实际路径

   **自定义信任密钥库类型**: JKS

   **自定义信任密钥库密码短语**: *mypassword* （自定义信任密钥密码）

1. 在“常规”下的“配置”中，选 **择SSL**。
1. 默认情况下，为“标识和信任位置”选择“密钥库”。 否则，将其更改为密钥库。
1. 在“标识”下，指定以下值：

   **私钥别名**: ads-credentials

   **密码**: *mypassword*

1. 单击“ **释放配置**”。

## 禁用主机名验证功能 {#disable-the-hostname-verification-feature}

1. 在“配置”选项卡上，单击“SSL”。
1. 在“高级”下，从“主机名验证”列表中选择“无”。

   如果未禁用主机名验证，则公用名称(CN)必须包含服务器主机名。

1. 在“更改中心”下，单击“锁定并编辑”以修改选择和值。
1. 重新启动应用程序服务器。

