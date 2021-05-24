---
title: 使用AEM 6配置LDAP
seo-title: 使用AEM 6配置LDAP
description: 了解如何使用AEM配置LDAP。
seo-description: 了解如何使用AEM配置LDAP。
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
exl-id: 2ebca4fb-20f7-499c-96a0-4018eaeddc1a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 0%

---

# 使用AEM 6 {#configuring-ldap-with-aem}配置LDAP

LDAP（**L** 8个&#x200B;**D**&#x200B;目录&#x200B;**A**&#x200B;访问&#x200B;**P**&#x200B;协议）用于访问集中的目录服务。 这有助于减少管理用户帐户所需的工作量，因为多个应用程序都可以访问这些帐户。 其中一个LDAP服务器是Active Directory。 LDAP通常用于实现单点登录，该单点登录允许用户在登录一次后访问多个应用程序。

用户帐户可以在LDAP服务器和存储库之间同步，LDAP帐户详细信息将保存在存储库中。 这允许将帐户分配给存储库组以分配所需的权限和权限。

存储库使用LDAP身份验证来验证此类用户，并将凭据传递到LDAP服务器以进行验证，验证是允许访问存储库之前需要的。 为了提高性能，存储库可以缓存已成功验证的凭据，并设置到期超时，以确保在适当的时间段后进行重新验证。

从LDAP服务器验证中删除帐户后，将不再授予该帐户的验证权限，从而拒绝对存储库的访问。 也可以清除存储库中保存的LDAP帐户的详细信息。

此类帐户的使用对用户而言是透明的，他们发现从LDAP创建的用户和组帐户与仅在存储库中创建的用户和组帐户之间没有区别。

在AEM 6中，LDAP支持随附一个新实施，该实施需要与以前版本不同的配置类型。

现在，所有LDAP配置均可用作OSGi配置。 这些配置文件可通过Web管理控制台(位于：
`https://serveraddress:4502/system/console/configMgr`

要让LDAP与AEM配合使用，您需要创建三个OSGi配置：

1. LDAP身份提供程序(IDP)。
1. 同步处理程序。
1. 外部登录模块。

>[!NOTE]
>
>观看[Oak的外部登录模块 — 使用LDAP和Beyond](https://docs.adobe.com/content/ddc/en/gems/oak-s-external-login-module---authenticating-with-ldap-and-beyon.html#)进行身份验证，以深入了解外部登录模块。
>
>要阅读有关使用Apache DS配置Experience Manager的示例，请参阅[配置Adobe Experience Manager 6.5以使用Apache Directory Service。](https://helpx.adobe.com/experience-manager/using/configuring-aem64-apache-directory-service.html)

## 配置LDAP标识提供程序{#configuring-the-ldap-identity-provider}

LDAP标识提供程序用于定义如何从LDAP服务器中检索用户。

它可在管理控制台的&#x200B;**Apache Jackrabbit Oak LDAP标识提供程序**&#x200B;名称下找到。

LDAP标识提供程序可使用以下配置选项：

<table>
 <tbody>
  <tr>
   <td><strong>LDAP提供程序名称</strong></td>
   <td>此LDAP提供程序配置的名称。</td>
  </tr>
  <tr>
   <td><strong>LDAP服务器主机名</strong><br /> </td>
   <td>LDAP服务器的主机名</td>
  </tr>
  <tr>
   <td><strong>LDAP服务器端口</strong></td>
   <td>LDAP服务器的端口</td>
  </tr>
  <tr>
   <td><strong>使用SSL</strong></td>
   <td>指示是否应使用SSL(LDAP)连接。</td>
  </tr>
  <tr>
   <td><strong>使用TLS</strong></td>
   <td>指示是否应在连接上启动TLS。</td>
  </tr>
  <tr>
   <td><strong>禁用证书检查</strong></td>
   <td>指示是否应禁用服务器证书验证。</td>
  </tr>
  <tr>
   <td><strong>绑定DN</strong></td>
   <td>用户进行身份验证的DN。 如果留空，则将执行匿名绑定。</td>
  </tr>
  <tr>
   <td><strong>绑定密码</strong></td>
   <td>用于身份验证的用户密码</td>
  </tr>
  <tr>
   <td><strong>搜索超时</strong></td>
   <td>搜索超时的时间</td>
  </tr>
  <tr>
   <td><strong>管理池最大活动数</strong></td>
   <td>管理员连接池的最大活动大小。</td>
  </tr>
  <tr>
   <td><strong>最大活动用户池数</strong></td>
   <td>用户连接池的最大活动大小。</td>
  </tr>
  <tr>
   <td><strong>用户基DN</strong></td>
   <td>用户搜索的DN</td>
  </tr>
  <tr>
   <td><strong>用户对象类</strong></td>
   <td>用户条目必须包含的对象类列表。</td>
  </tr>
  <tr>
   <td><strong>用户ID属性</strong></td>
   <td>包含用户ID的属性的名称。</td>
  </tr>
  <tr>
   <td><strong>用户额外过滤器</strong></td>
   <td>在搜索用户时要使用的额外LDAP筛选器。 最终过滤器的格式如下：'(&amp;(&lt;idAttr&gt;=&lt;userId&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)'(user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>用户DN路径</strong></td>
   <td>控制是否应使用DN来计算中间路径的一部分。</td>
  </tr>
  <tr>
   <td><strong>组基本DN</strong></td>
   <td>组搜索的基本DN。</td>
  </tr>
  <tr>
   <td><strong>组对象类</strong></td>
   <td>组条目必须包含的对象类列表。</td>
  </tr>
  <tr>
   <td><strong>组名称属性</strong></td>
   <td>包含群组名称的属性的名称。</td>
  </tr>
  <tr>
   <td><strong>组附加过滤器</strong></td>
   <td>在搜索组时要使用的额外LDAP筛选器。 最终过滤器的格式如下：'(&amp;(&lt;nameAttr&gt;=&lt;groupName&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>组DN路径</strong></td>
   <td>控制是否应使用DN来计算中间路径的一部分。</td>
  </tr>
  <tr>
   <td><strong>组成员属性</strong></td>
   <td>包含组成员的组属性。</td>
  </tr>
 </tbody>
</table>

## 配置同步处理程序{#configuring-the-synchronization-handler}

同步处理程序将定义如何将身份提供程序用户和组与存储库同步。

它位于管理控制台中的&#x200B;**Apache Jackrabbit Oak默认同步处理程序**&#x200B;名称下。

同步处理程序可使用以下配置选项：

<table>
 <tbody>
  <tr>
   <td><strong>同步处理程序名称</strong></td>
   <td>同步配置的名称。</td>
  </tr>
  <tr>
   <td><strong>用户过期时间</strong></td>
   <td>同步的用户过期前的持续时间。</td>
  </tr>
  <tr>
   <td><strong>用户自动成员资格</strong></td>
   <td>已同步用户自动添加到的组列表。</td>
  </tr>
  <tr>
   <td><strong>用户属性映射</strong></td>
   <td>外部属性的本地属性的列表映射定义。</td>
  </tr>
  <tr>
   <td><strong>用户路径前缀</strong></td>
   <td>创建新用户时使用的路径前缀。</td>
  </tr>
  <tr>
   <td><strong>用户成员资格过期</strong></td>
   <td>成员资格过期的时间。<br /> </td>
  </tr>
  <tr>
   <td><strong>用户成员身份嵌套深度</strong></td>
   <td>返回同步成员关系时组嵌套的最大深度。 值为0会有效禁用组成员身份查找。 值1只会添加用户的直接组。 仅当同步用户成员资格祖先时，此值才会在同步单个组时不起作用。</td>
  </tr>
  <tr>
   <td><strong>组过期时间</strong></td>
   <td>同步的组过期前的持续时间。</td>
  </tr>
  <tr>
   <td><strong>组自动成员资格</strong></td>
   <td>已同步组自动添加到的组列表。</td>
  </tr>
  <tr>
   <td><strong>组属性映射</strong></td>
   <td>外部属性的本地属性的列表映射定义。</td>
  </tr>
  <tr>
   <td><strong>组路径前缀</strong></td>
   <td>创建新组时使用的路径前缀。</td>
  </tr>
 </tbody>
</table>

## 外部登录模块{#the-external-login-module}

外部登录模块位于管理控制台下的&#x200B;**Apache Jackrabbit Oak外部登录模块**&#x200B;下。

>[!NOTE]
>
>Apache Jackrabbit Oak外部登录模块实施Java身份验证和授权服务(JAAS)规范。 有关详细信息，请参阅[官方OracleJava安全参考指南](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html)。

其工作是定义要使用的身份提供程序和同步处理程序，从而有效地绑定这两个模块。

以下配置选项可用：

| **JAAS排名** | 指定此登录模块条目的排名（即排序顺序）。 条目按降序排序（即排名配置的值越高）。 |
|---|---|
| **JAAS控制标志** | 属性指定LoginModule是否为必需、必需、充分或可选。有关这些标志含义的更多详细信息，请参阅JAAS配置文档。 |
| **JAAS Realm** | 注册LoginModule的领域名称（或应用程序名称）。 如果未提供领域名称，则LoginModule将按照Felix JAAS配置中配置的默认领域进行注册。 |
| **身份提供程序名称** | 标识提供程序的名称。 |
| **同步处理程序名称** | 同步处理程序的名称。 |

>[!NOTE]
>
>如果您计划与AEM实例一起使用多个LDAP配置，则需要为每个配置创建单独的身份提供程序和同步处理程序。

## 通过SSL {#configure-ldap-over-ssl}配置LDAP

AEM 6可以按照以下过程配置为通过SSL通过LDAP进行身份验证：

1. 选中&#x200B;**配置[LDAP标识提供程序](#configuring-the-ldap-identity-provider)时使用SSL**&#x200B;或&#x200B;**使用TLS**&#x200B;复选框。
1. 根据您的设置配置同步处理程序和外部登录模块。
1. 如有需要，请在Java VM中安装SSL证书。 可以使用键工具完成此操作：

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. 测试与LDAP服务器的连接。

### 创建SSL证书{#creating-ssl-certificates}

在配置AEM以通过SSL通过LDAP进行身份验证时，可以使用自签名证书。 以下是生成用于AEM的证书的工作过程示例。

1. 确保已安装并运行SSL库。 此过程将以OpenSSL为例。

1. 创建自定义的OpenSSL配置(cnf)文件。 可通过复制默认的**openssl.cnf **配置文件并对其进行自定义来完成此操作。 在UNIX系统上，它通常位于`/usr/lib/ssl/openssl.cnf`

1. 在终端中运行以下命令以继续创建CA根密钥：

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. 接下来，创建一个新的自签名证书：

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. Inspect新生成的证书可确保一切顺序：

   `openssl x509 -noout -text -in root-ca.crt`

1. 确保证书配置(.cnf)文件中指定的所有文件夹都存在。 如果没有，请创建它们。
1. 通过运行(例如：

   `openssl rand -out private/.rand 8192`

1. 将创建的.pem文件移动到.cnf文件中配置的位置。

1. 最后，将证书添加到Java KeyStore。

## 启用调试日志记录{#enabling-debug-logging}

可以为LDAP身份提供程序和外部登录模块启用调试日志记录，以解决连接问题。

要启用调试日志记录，您需要：

1. 转到Web管理控制台。
1. 查找“Apache Sling日志记录器配置”，并创建两个具有以下选项的日志记录器：

* 日志级别：调试
* 日志文件logs/ldap.log
* 消息模式：{0,date，dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast;{2} {3} {5}
* 记录器：org.apache.jackrabbit.oak.security.ldap

* 日志级别：调试
* 日志文件：logs/external.log
* 消息模式：{0,date，dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast;{2} {3} {5}
* 记录器：org.apache.jackrabbit.oak.spi.security.authentication.external

## 关于群从属关系的一个词{#a-word-on-group-affiliation}

通过LDAP同步的用户可能属于AEM中的不同组。 这些组可以是将作为同步过程的一部分添加到AEM的外部LDAP组，但也可以是单独添加的组，而不是原始LDAP组从属关系方案的一部分。

在大多数情况下，这些组可以是由本地AEM管理员或任何其他身份提供程序添加的组。

如果从LDAP服务器上的组中删除了用户，则同步时所做的更改也会反映在AEM端。 但是，LDAP中未添加的用户的所有其他组从属关系都将保留。

AEM通过使用`rep:externalId`属性来检测并处理从外部组清除用户的情况。 此属性将自动添加到由同步处理程序同步的任何用户或组，并包含有关原始身份提供程序的信息。

有关更多信息，请参阅[用户和组同步](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html)上的Apache Oak文档。

## 已知问题 {#known-issues}

如果您计划通过SSL使用LDAP，请确保创建您正在使用的证书时没有使用Netscape注释选项。 如果启用此选项，身份验证将失败，并出现SSL握手错误。
