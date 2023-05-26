---
title: 使用AEM 6配置LDAP
description: 了解如何使用AEM配置LDAP。
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
exl-id: 2ebca4fb-20f7-499c-96a0-4018eaeddc1a
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 0%

---

# 使用AEM 6配置LDAP {#configuring-ldap-with-aem}

LDAP (此 **L** hightweight **D**&#x200B;目录 **A**&#x200B;访问 **P** rotocol)用于访问集中式目录服务。 它有助于减少管理用户帐户所需的工作量，因为多个应用程序可以访问用户帐户。 Active Directory就是这样的LDAP服务器。 LDAP通常用于实现单点登录，它允许用户在一次登录后访问多个应用程序。

用户帐户可以在LDAP服务器和存储库之间同步，LDAP帐户详细信息将保存在存储库中。 此功能允许将帐户分配给存储库组，以便分配所需的权限和权限。

存储库使用LDAP身份验证来验证此类用户，凭据将传递到LDAP服务器进行验证，在允许访问存储库之前需要验证。 为了提高性能，存储库可以缓存已成功验证的凭据，并且有过期超时，以确保在适当的时间段后进行重新验证。

从LDAP服务器中删除帐户后，将不再授予验证并拒绝对存储库的访问。 还可以清除保存在存储库中的LDAP帐户的详细信息。

此类帐户的使用对用户是透明的。 也就是说，他们发现，从LDAP创建的用户和组帐户与仅在存储库中创建的帐户之间没有区别。

在AEM 6中，LDAP支持随附了一个新实施，该实施需要与以前版本不同的配置类型。

所有LDAP配置现在都作为OSGi配置提供。 它们可以通过Web管理控制台进行配置，网址为：
`https://serveraddress:4502/system/console/configMgr`

要使LDAP与AEM配合使用，您必须创建三个OSGi配置：

1. LDAP身份提供程序(IDP)。
1. 同步处理程序。
1. 外部登录模块。

>[!NOTE]
>
>观看 [Oak的外部登录模块 — 使用LDAP及更高版本进行身份验证](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-oak-external-login-module-authenticating-with-ldap-and-beyond.html?lang=en) 以深入了解外部登录模块。
>
>要阅读有关使用Apache DS配置Experience Manager的示例，请参见 [正在配置Adobe Experience Manager 6.5以使用Apache Directory Service。](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/configuring-adobe-experience-manager-6-to-use-apache-directory/m-p/183805)

## 配置LDAP身份提供程序 {#configuring-the-ldap-identity-provider}

LDAP标识提供程序用于定义如何从LDAP服务器中检索用户。

它可以在管理控制台中的 **Apache Jackrabbit Oak LDAP身份提供程序** 名称。

以下配置选项可用于LDAP身份提供程序：

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
   <td>指示是否应使用SSL (LDAP)连接。</td>
  </tr>
  <tr>
   <td><strong>使用TLS</strong></td>
   <td>指示连接时是否应启动TLS。</td>
  </tr>
  <tr>
   <td><strong>禁用证书检查</strong></td>
   <td>指示是否应禁用服务器证书验证。</td>
  </tr>
  <tr>
   <td><strong>绑定DN</strong></td>
   <td>用于身份验证的用户的DN。 如果此字段留空，则执行匿名绑定。</td>
  </tr>
  <tr>
   <td><strong>绑定密码</strong></td>
   <td>用于验证的用户的密码</td>
  </tr>
  <tr>
   <td><strong>搜索超时</strong></td>
   <td>搜索超时前的时间</td>
  </tr>
  <tr>
   <td><strong>最大管理池活动</strong></td>
   <td>管理连接池的最大活动大小。</td>
  </tr>
  <tr>
   <td><strong>最大活动用户池</strong></td>
   <td>用户连接池的最大活动大小。</td>
  </tr>
  <tr>
   <td><strong>用户基础DN</strong></td>
   <td>用于用户搜索的DN</td>
  </tr>
  <tr>
   <td><strong>用户对象类</strong></td>
   <td>用户条目必须包含的对象类的列表。</td>
  </tr>
  <tr>
   <td><strong>用户ID属性</strong></td>
   <td>包含用户ID的属性的名称。</td>
  </tr>
  <tr>
   <td><strong>用户额外筛选器</strong></td>
   <td>搜索用户时要使用的额外LDAP过滤器。 最终筛选器的格式如下所示：'(&amp;(&lt;idattr&gt;=&lt;userid&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)' (user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>用户DN路径</strong></td>
   <td>控制是否应使用DN计算中间路径的一部分。</td>
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
   <td>包含组名称的属性的名称。</td>
  </tr>
  <tr>
   <td><strong>对额外过滤器进行分组</strong></td>
   <td>搜索组时要使用的额外LDAP过滤器。 最终筛选器的格式如下所示：'(&amp;(&lt;nameattr&gt;=&lt;groupname&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>组DN路径</strong></td>
   <td>控制是否应使用DN计算中间路径的一部分。</td>
  </tr>
  <tr>
   <td><strong>组成员属性</strong></td>
   <td>包含组的一个或多个成员的组属性。</td>
  </tr>
 </tbody>
</table>

## 配置同步处理程序 {#configuring-the-synchronization-handler}

同步处理程序定义身份提供程序用户和组如何与存储库同步。

它位于 **Apache Jackrabbit Oak默认同步处理程序** 名称。

以下配置选项可用于同步处理程序：

<table>
 <tbody>
  <tr>
   <td><strong>同步处理程序名称</strong></td>
   <td>同步配置的名称。</td>
  </tr>
  <tr>
   <td><strong>用户过期时间</strong></td>
   <td>同步用户过期之前的持续时间。</td>
  </tr>
  <tr>
   <td><strong>用户自动成员资格</strong></td>
   <td>同步用户自动添加到其中的组的列表。</td>
  </tr>
  <tr>
   <td><strong>用户属性映射</strong></td>
   <td>外部属性的列表映射定义。</td>
  </tr>
  <tr>
   <td><strong>用户路径前缀</strong></td>
   <td>创建用户时使用的路径前缀。</td>
  </tr>
  <tr>
   <td><strong>用户成员资格过期</strong></td>
   <td>成员资格过期的时间。<br /> </td>
  </tr>
  <tr>
   <td><strong>用户成员资格嵌套深度</strong></td>
   <td>同步成员关系时返回组嵌套的最大深度。 如果值为0，则实际上会禁用组成员资格查找。 值1仅添加用户的直接组。 仅当同步用户成员资格祖先时，同步各个组时，此值不起作用。</td>
  </tr>
  <tr>
   <td><strong>组过期时间</strong></td>
   <td>同步组过期之前的持续时间。</td>
  </tr>
  <tr>
   <td><strong>组自动成员资格</strong></td>
   <td>已同步组自动添加到其中的组的列表。</td>
  </tr>
  <tr>
   <td><strong>组属性映射</strong></td>
   <td>外部属性的列表映射定义。</td>
  </tr>
  <tr>
   <td><strong>组路径前缀</strong></td>
   <td>创建组时使用的路径前缀。</td>
  </tr>
 </tbody>
</table>

## 外部登录模块 {#the-external-login-module}

外部登录模块位于 **Apache Jackrabbit Oak外部登录模块** 在管理控制台下。

>[!NOTE]
>
>Apache Jackrabbit Oak外部登录模块实施Java™身份验证和授权服务(JAAS)规范。 请参阅 [官方OracleJava™安全参考指南](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) 了解更多信息。

其工作是定义要使用哪个身份提供程序和同步处理程序，从而有效地绑定这两个模块。

以下配置选项可用：

| **JAAS排名** | 指定此登录模块条目的排名（即排序顺序）。 这些条目按降序排序（即，值较高的排名配置排在首位）。 |
|---|---|
| **JAAS控制标志** | 指定LoginModule是REQUIRED、REQUISITE、SUFFIENT还是OPTIONAL的属性。 有关这些标记含义的更多详细信息，请参阅JAAS配置文档。 |
| **JAAS领域** | 注册LoginModule时所针对的领域名称（或应用程序名称）。 如果未提供领域名称，则使用Felix JAAS配置中配置的默认领域注册LoginModule。 |
| **身份提供程序名称** | 身份提供程序的名称。 |
| **同步处理程序名称** | 同步处理程序的名称。 |

>[!NOTE]
如果您打算在AEM实例中使用多个LDAP配置，则必须为每个配置创建单独的身份提供程序和同步处理程序。

## 通过SSL配置LDAP {#configure-ldap-over-ssl}

可以将AEM 6配置为通过SSL的LDAP进行身份验证，请执行以下步骤：

1. 查看 **使用SSL** 或 **使用TLS** 复选框。 [LDAP身份提供程序](#configuring-the-ldap-identity-provider).
1. 根据您的设置配置同步处理程序和外部登录模块。
1. 如果需要，请在Java™ VM中安装SSL证书。 可以使用keytool完成此安装：

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. 测试与LDAP服务器的连接。

### 创建SSL证书 {#creating-ssl-certificates}

在配置AEM以通过SSL通过LDAP进行身份验证时，可以使用自签名证书。 以下是生成用于AEM的证书的工作过程示例。

1. 确保您已安装并运行SSL库。 此过程使用OpenSSL作为示例。

1. 创建自定义的OpenSSL配置(cnf)文件。 可以通过复制默认**openssl.cnf**配置文件并对其进行自定义来完成此配置。 在UNIX®系统上，它位于 `/usr/lib/ssl/openssl.cnf`

1. 通过在终端中运行以下命令继续创建CA根密钥：

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. 接下来，创建自签名证书：

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. 要确保一切正常，请检查新生成的证书：

   `openssl x509 -noout -text -in root-ca.crt`

1. 确保证书配置(.cnf)文件中指定的所有文件夹都存在。 如果没有，请创建它们。
1. 通过运行创建随机种子，例如：

   `openssl rand -out private/.rand 8192`

1. 将创建的.pem文件移动到.cnf文件中配置的位置。

1. 最后，将证书添加到Java™密钥库中。

## 启用调试日志记录 {#enabling-debug-logging}

可以为LDAP身份提供程序和外部登录模块启用调试日志记录，以解决连接问题。

要启用调试日志记录，必须执行以下操作：

1. 转到Web管理控制台。
1. 查找“Apache Sling日志记录器配置”并使用以下选项创建两个日志记录器：

* 日志级别： Debug
* 日志文件logs/ldap.log
* 消息模式： {0，date，dd.MM.yyyy HH:mm:ss.SSS} &amp;ast；{4}&amp;ast； {2} {3} {5}
* 记录器：org.apache.jackrabbit.oak.security.authentication.ldap

* 日志级别： Debug
* 日志文件：logs/external.log
* 消息模式： {0，date，dd.MM.yyyy HH:mm:ss.SSS} &amp;ast；{4}&amp;ast； {2} {3} {5}
* 记录器：org.apache.jackrabbit.oak.spi.security.authentication.external

## 关于群组隶属的一句话 {#a-word-on-group-affiliation}

通过LDAP同步的用户可以属于AEM中的不同组。 这些组可以是作为同步过程的一部分添加到AEM的外部LDAP组。 但是，它们也可以是单独添加的组，而不是原始LDAP组关联方案的一部分。

通常，这些组由本地AEM管理员或任何其他身份提供程序添加。

如果从LDAP服务器上的组中删除某个用户，则同步时所做的更改将反映在AEM端。 但是，用户的所有其他未由LDAP添加的组关联仍保持不变。

AEM通过使用检测并处理从外部组中清除用户的操作， `rep:externalId` 属性。 此属性将自动添加到由同步处理程序同步的任何用户或组，并且包含有关原始身份提供者的信息。

请参阅有关的Apache Oak文档 [用户和组同步](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## 已知问题 {#known-issues}

如果您计划使用LDAP over SSL，请确保创建的证书不带Netscape注释选项。 如果启用此选项，身份验证将失败并出现SSL握手错误。
