---
title: 为WebLogic Server配置SSL
seo-title: Configuring SSL for WebLogic Server
description: 了解如何创建在WebLogic服务器上使用的SSL凭据以及如何为WebLogic服务器配置SSL。
seo-description: Learn how to create an SSL credential for use on WebLogic server and how to configure SSL for WebLogic Server.
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 1%

---


# 为WebLogic Server配置SSL {#configuring-ssl-for-weblogic-server}

要在WebLogic Server上配置SSL，您需要用于身份验证的SSL凭据。 可以使用Java keytool执行以下任务来创建凭据：

* 创建公钥/私钥对，将公钥包装在X.509 v1自签名证书中（该证书存储为单元素证书链），然后将证书链和私钥存储到新的密钥库中。 此密钥库是应用程序服务器的自定义身份密钥库。
* 提取证书并将其插入新的密钥库中。 此密钥库是应用程序服务器的自定义信任密钥库。

然后，配置WebLogic，使其使用您创建的自定义身份密钥库和自定义信任密钥库。 另外，禁用WebLogic主机名验证功能，因为用于创建密钥库文件的可分辨名称不包含承载WebLogic的计算机的名称。

## 创建用于WebLogic Server的SSL凭据 {#creating-an-ssl-credential-for-use-on-weblogic-server}

keytool命令通常位于Java jre/bin目录中，并且必须包含下表列出的多个选项和选项值。

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
   <td><p> — 别名</p></td>
   <td><p>密钥库的别名。</p></td>
   <td>
    <ul>
     <li><p>自定义身份密钥库： <code>ads-credentials</code></p></li>
     <li><p>自定义信任密钥库： <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>用于生成密钥对的算法。</p></td>
   <td><p>RSA</p><p>您可以使用不同的算法，具体取决于公司的策略。</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>密钥库文件的位置和名称。</p><p>该位置可以包含文件的绝对路径。 或者，它可以相对于命令提示符（输入keytool命令）的当前目录。</p></td>
   <td>
    <ul>
     <li><p>自定义身份密钥库： <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[服务器名称]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>自定义信任密钥库： <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[服务器名称]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>证书文件的位置和名称。</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-validity</p></td>
   <td><p>证书被视为有效的天数。</p></td>
   <td><p>3650</p><p>您可以使用其他值，具体取决于贵公司的策略。</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>保护密钥库内容的密码。 </p></td>
   <td>
    <ul>
     <li><p>自定义身份密钥库：密钥库密码必须与为Administration Console的Trust Store组件指定的SSL凭据密码相对应。</p></li>
     <li><p>自定义信任密钥库：使用与自定义身份密钥库相同的密码。</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>保护密钥对私钥的密码。</p></td>
   <td><p>使用您用于 <code>-storepass</code> 选项。 密钥密码必须至少为6个字符。</p></td>
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
     <li><p><code><i>[State or province]</i></code> 是您的组织所在的省/市/自治区。</p></li>
     <li><p><code><i>[Country Code]</i></code> 是组织所在国家/地区的双字母代码。</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

有关使用keytool命令的更多信息，请参阅作为JDK文档一部分的keytool.html文件。

## 创建自定义标识和信任密钥库 {#create-the-custom-identity-and-trust-keystores}

1. 在命令提示符下，导航至 *[appserverdomain]*/adobe/*[服务器名称]*.
1. 输入以下命令：

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >替换 `[JAVA_HOME]`*替换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   名为“ads-credentials.jks”的自定义身份密钥库文件是在 [appserverdomain]/adobe/[服务器名称] 目录。

1. 通过输入以下命令从ads-credentials密钥库中提取证书：

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**密码**

   >[!NOTE]
   >
   >替换 `[JAVA_HOME]` 替换为安装JDK的目录，并将 `store`*_* `password`*包含自定义身份密钥库的密码。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   在中创建名为“ads-ca.cer”的证书文件 [appserverdomain]/adobe/[*服务器名称*] 目录。

1. 将ads-ca.cer文件复制到需要与应用程序服务器安全通信的任何主机计算机上。
1. 通过输入以下命令，将证书插入到新的密钥库文件（自定义信任密钥库）中：

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >替换 `[JAVA_HOME]` 替换为安装JDK的目录，并将 `store`*_* `password` 和 `key`*_* `password` *使用您自己的密码。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

名为“ads-ca.jks”的自定义信任密钥库文件是在 [appserverdomain]/adobe/&#39;server&#39;目录。

配置WebLogic，使其使用您创建的自定义身份密钥库和自定义信任密钥库。 另外，禁用WebLogic主机名验证功能，因为用于创建密钥库文件的可分辨名称不包含承载WebLogic Server的计算机的名称。

## 配置WebLogic以使用SSL {#configure-weblogic-to-use-ssl}

1. 通过键入以下内容启动WebLogic服务器管理控制台 `https://`*[主机名&#x200B;]*`:7001/console` 在Web浏览器的URL行中。
1. 在环境下的域配置中，选择 **“服务器”>“服务器”>“配置”>“常规”**.
1. 在“常规”下的“配置”中，确保 **侦听端口已启用** 和 **已启用SSL侦听端口** 已选中。 如果未启用，请执行以下操作：

   1. 在更改中心下，单击 **锁定并编辑** 修改选项和值。
   1. 查看 **侦听端口已启用** 和 **已启用SSL侦听端口** 复选框。

1. 如果此服务器是受控服务器，请将“监听端口”更改为未使用的端口值（如8001），并将“SSL监听端口”更改为未使用的端口值（如8002）。 在独立服务器上，默认SSL端口为7002。
1. 单击 **发行配置**.
1. 在环境下的域配置中，单击 **服务器> [*受控服务器*] >配置>常规**.
1. 在“常规”下的“配置”中，选择 **密钥库**.
1. 在更改中心下，单击 **锁定并编辑** 修改选项和值。
1. 单击 **更改** 要以下拉列表的形式获取密钥库列表，请选择 **自定义身份和自定义信任**.
1. 在“标识”下，指定以下值：

   **自定义身份密钥库**： *[appserverdomain]*/adobe/*[服务器名称]*/ads-credentials.jks，其中*[appserverdomain] *是实际路径和 *[服务器名称]* 是应用程序服务器的名称。

   **自定义身份密钥库类型**：JKS

   **自定义身份密钥库密码短语**： *我的密码* （自定义身份密钥库密码）

1. 在“信任”下，指定以下值：

   **自定义信任密钥库文件名**： `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`，其中 `*[appserverdomain]*` 是实际路径

   **自定义信任密钥库类型**：JKS

   **自定义信任密钥库密码短语**： *我的密码* （自定义信任密钥密码）

1. 在“常规”下的“配置”中，选择 **SSL**.
1. 默认情况下，为“标识和信任位置”选择Keystore。 如果不能，请将其更改为keystore。
1. 在“标识”下，指定以下值：

   **私钥别名**：ads-credentials

   **密码短语**： *我的密码*

1. 单击 **发行配置**.

## 禁用主机名验证功能 {#disable-the-hostname-verification-feature}

1. 在配置选项卡上，单击SSL。
1. 在“高级”下，从“主机名验证”列表中选择“无”。

   如果未禁用主机名验证，则公用名(CN)必须包含服务器主机名。

1. 在“更改中心”下，单击“锁定和编辑”以修改选项和值。
1. 重新启动应用程序服务器。

