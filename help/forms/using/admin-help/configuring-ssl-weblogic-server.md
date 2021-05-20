---
title: 为WebLogic服务器配置SSL
seo-title: 为WebLogic服务器配置SSL
description: 了解如何创建SSL凭据以在WebLogic服务器上使用，以及如何为WebLogic服务器配置SSL。
seo-description: 了解如何创建SSL凭据以在WebLogic服务器上使用，以及如何为WebLogic服务器配置SSL。
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---


# 为WebLogic服务器{#configuring-ssl-for-weblogic-server}配置SSL

要在WebLogic服务器上配置SSL，您需要SSL凭据进行身份验证。 您可以使用Java密钥工具执行以下任务以创建凭据：

* 创建公钥/私钥对，将公钥封装在X.509 v1自签名证书中（存储为单元证书链），然后将证书链和私钥存储在新密钥库中。 此密钥库是应用程序服务器的自定义身份密钥库。
* 提取证书并将其插入到新密钥库中。 此密钥库是应用程序服务器的自定义信任密钥库。

然后，配置WebLogic，以便它使用您创建的自定义身份密钥库和自定义信任密钥库。 此外，禁用WebLogic主机名验证功能，因为用于创建密钥库文件的可分辨名称不包含托管WebLogic的计算机的名称。

## 创建SSL凭据以在WebLogic服务器{#creating-an-ssl-credential-for-use-on-weblogic-server}上使用

keytool命令通常位于Java jre/bin目录中，并且必须包括几个选项和选项值，这些选项和选项值列在下表中。

<table>
 <thead>
  <tr>
   <th><p>键工具选项</p></th>
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
     <li><p>自定义身份密钥库： <code>ads-credentials</code></p></li>
     <li><p>自定义信任密钥库： <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>用于生成键对的算法。</p></td>
   <td><p>RSA</p><p>您可以使用不同的算法，具体取决于您公司的策略。</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>密钥库文件的位置和名称。</p><p>位置可以包含文件的绝对路径。 或者，它可以相对于输入keytool命令的命令提示符的当前目录。</p></td>
   <td>
    <ul>
     <li><p>自定义身份密钥库：<code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[服务器名称]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>自定义信任密钥库：<code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[服务器名称]</i><code>/ads-ca.jks</code></p></li>
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
   <td><p>3650</p><p>您可以使用不同的值，具体取决于您公司的策略。</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>用于保护密钥库内容的密码。 </p></td>
   <td>
    <ul>
     <li><p>自定义身份密钥库：密钥库密码必须与为管理控制台的信任存储组件指定的SSL凭据密码相对应。</p></li>
     <li><p>自定义信任密钥库：使用与用于自定义身份密钥库的密码相同。</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>用于保护密钥对的私钥的密码。</p></td>
   <td><p>使用与<code>-storepass</code>选项所用的密码相同。 密钥密码必须至少为6个字符。</p></td>
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
     <li><p><code><i>[Country Code]</i></code> 是贵组织所在国家/地区的双字母代码。</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

有关使用keytool命令的更多信息，请参阅JDK文档中包含的keytool.html文件。

## 创建自定义标识和信任密钥库{#create-the-custom-identity-and-trust-keystores}

1. 在命令提示符下，导航到&#x200B;*[appserverdomain]*/adobe/*[服务器名称]*。
1. 输入以下命令：

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >将&#x200B;`[JAVA_HOME]`*替换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   在[appserverdomain]/adobe/[服务器名称]目录中创建名为“ads-credentials.jks”的自定义身份密钥存储文件。

1. 通过输入以下命令，从ads-credentials密钥库中提取证书：

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**password**

   >[!NOTE]
   >
   >将`[JAVA_HOME]`替换为安装JDK的目录，并将&#x200B;`store`*_* `password`*替换为自定义身份密钥库的密码。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   名为“ads-ca.cer”的证书文件创建在[appserverdomain]/adobe/[*服务器名称*]&#x200B;目录中。

1. 将ads-ca.cer文件复制到需要与应用程序服务器进行安全通信的任何主机计算机。
1. 通过输入以下命令将证书插入新密钥库文件（自定义信任密钥库）：

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >将`[JAVA_HOME]`替换为安装JDK的目录，并将&#x200B;`store`*_* `password`和&#x200B;`key`*_* `password` *替换为您自己的密码。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

在[appserverdomain]/adobe/&#39;server&#39;目录中创建名为“ads-ca.jks”的自定义信任密钥库文件。

配置WebLogic，以便它使用您创建的自定义身份密钥库和自定义信任密钥库。 此外，禁用WebLogic主机名验证功能，因为用于创建密钥库文件的可分辨名称不包含承载WebLogic服务器的计算机的名称。

## 配置WebLogic以使用SSL {#configure-weblogic-to-use-ssl}

1. 在Web浏览器的URL行中键入`https://`*[主机名&#x200B;]*`:7001/console`以启动WebLogic服务器管理控制台。
1. 在“环境”下的“域配置”中，选择&#x200B;**服务器> &#39;服务器&#39; >配置>常规**。
1. 在“常规”下，在“配置”中，确保选中了&#x200B;**已启用监听端口**&#x200B;和&#x200B;**已启用SSL监听端口**。 如果未启用，请执行以下操作：

   1. 在“更改中心”下，单击&#x200B;**锁定并编辑**&#x200B;以修改选择和值。
   1. 选中&#x200B;**Listen Port Enabled**&#x200B;和&#x200B;**SSL Listen Port Enabled**&#x200B;复选框。

1. 如果此服务器是受管服务器，请将“侦听端口”更改为未使用的端口值（如8001），将SSL侦听端口更改为未使用的端口值（如8002）。 在独立服务器上，默认的SSL端口为7002。
1. 单击&#x200B;**Release Configuration**。
1. 在“环境”下的“域配置”中，单击&#x200B;**服务器> [*托管服务器*] >配置>常规**。
1. 在常规下的配置中，选择&#x200B;**密钥库**。
1. 在“更改中心”下，单击&#x200B;**锁定并编辑**&#x200B;以修改选择和值。
1. 单击&#x200B;**Change**&#x200B;以将密钥库列表作为下拉列表获取，然后选择&#x200B;**Custom Identity And Custom Trust**。
1. 在标识下，指定以下值：

   **自定义身份密钥库**: *[appserverdomain]*/adobe/*[服务器名称]*/ads-credentials.jks，其中*[appserverdomain] *是实际路径，而 *[服务]* 器名称是应用程序服务器的名称。

   **自定义身份密钥库类型**:JKS

   **自定义身份密钥库密码**: *mypassword* （自定义身份密钥库密码）

1. 在信任下，指定以下值：

   **自定义信任密钥库文件名**: `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`，其中 `*[appserverdomain]*` 是实际路径

   **自定义信任密钥库类型**:JKS

   **自定义信任密钥库密码短语**: *mypassword* （自定义信任密钥密码）

1. 在常规下的配置中，选择&#x200B;**SSL**。
1. 默认情况下，为“身份”和“信任”位置选择KeyStore。 如果没有，请将其更改为KeyStore。
1. 在标识下，指定以下值：

   **私钥别名**:ads-credentials

   **密码**: *mypassword*

1. 单击&#x200B;**Release Configuration**。

## 禁用主机名验证功能{#disable-the-hostname-verification-feature}

1. 在“配置”选项卡上，单击SSL。
1. 在高级下，从主机名验证列表中选择无。

   如果未禁用主机名验证，则通用名称(CN)必须包含服务器主机名。

1. 在“更改中心”(Change Center)下，单击“锁定并编辑”(Lock &amp; Edit)以修改选择和值。
1. 重新启动应用程序服务器。

