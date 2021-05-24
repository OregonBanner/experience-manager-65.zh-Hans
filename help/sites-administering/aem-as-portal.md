---
title: AEM门户和Portlet
seo-title: AEM门户和Portlet
description: 了解AEM中的门户和门户。
seo-description: 了解AEM中的门户和门户。
uuid: 7f9e316d-277e-4a1e-b6f3-cd89addc897b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 99528fda-5c8c-4034-bcbe-a4cea42f694b
docset: aem65
exl-id: b5f3d3a6-39c0-4aa5-8562-3cc6fa2b9e46
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '6097'
ht-degree: 0%

---

# AEM门户和Portlet{#aem-portals-and-portlets}

本文档将介绍以下内容：

* AEM Portal架构
* 管理和配置AEM作为门户
* 将AEM用作门户
* 在portlet（例如Web服务器）中安装、配置和显示AEM内容

## AEM Portal Architecture {#aem-portal-architecture}

AEM门户架构包括门户和portlet的定义。

### 什么是门户？{#what-is-a-portal}

门户是一个Web应用程序，它提供个性化、单点登录、来自不同来源的内容集成，并托管信息系统的表示层。

您可以在AEM中运行符合JSR 286的portlet。 Portlet组件允许您在页面上嵌入Portlet。 请参阅[管理AEM内容Portlet](#administeringthecqcontentportlet)。

### 什么是portlet?{#what-is-a-portlet}

Portlet是部署在容器内的Web组件，用于生成动态内容。 Portlet接口被打包并部署为Portlet容器内的.war文件。 如果您将AEM作为门户运行，则需要Portlet的.war文件来运行Portlet。

要将AEM内容配置为显示在门户中，请参阅[在portlet](#installingconfiguringandusingcqinaportlet)中安装、配置和使用AEM 。

### AEM Portal Director {#aem-portal-director}

>[!CAUTION]
>
>从AEM 6.4起，已弃用AEM Portal Director。请参阅[已弃用和已删除的功能](https://helpx.adobe.com/experience-manager/6-4/release-notes/deprecated-removed-features.html)。

## 管理AEM内容Portlet {#administering-the-aem-content-portlet}

通过AEM内容portlet，您可以在门户中显示AEM内容。 Portlet在`/crx-quickstart/opt/portal`上可用，并可以通过各种方式进行自定义。 例如，您可以通过部署您自己的身份验证服务来生成AEM覆盖默认行为所需的身份验证信息，从而自定义SSO/身份验证处理。 插件使用定义的API，通过该API，您可以根据API构建插件，以添加自己的功能。 该插件可以部署到正在运行的portlet中。 要正常运行，需要配置AEM创作和发布实例以及内容路径，才能在启动时显示。

某些配置可以通过portlet首选项进行更改，而其他配置则通过OSGi服务配置进行更改。 使用&#x200B;**config**&#x200B;文件或OSGi Web控制台更改这些配置。

### Portlet首选项{#portlet-preferences}

可以在部署Portlet Web应用程序之前，在Portlet服务器中或通过编辑&#x200B;**WEB-INF/portlet.xml**&#x200B;文件来配置Portlet首选项。 默认情况下，portlet.xml文件如下所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<portlet-app xmlns="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd /opt/SUNWps/dtd/portlet.xsd"
             version="1.0">
   <portlet>
      <portlet-name>RSSWeatherPortlet</portlet-name>
      <portlet-class>org.jboss.portlet.weather.WeatherPortlet</portlet-class>
      <init-param>
         <name>default_zipcode</name>
         <value>05673</value>
      </init-param>
      <init-param>
         <name>RSS_XSL</name>
         <value>/WEB-INF/Rss.xsl</value>
      </init-param>
      <init-param>
         <name>base_url</name>
         <value>https://xml.weather.yahoo.com/forecastrss?p=</value>
      </init-param>
      <expiration-cache>180</expiration-cache>
      <supports>
         <mime-type>text/html</mime-type>
         <portlet-mode>VIEW</portlet-mode>
         <portlet-mode>EDIT</portlet-mode>
      </supports>
      <portlet-info>
         <title>Weather Portlet</title>
      </portlet-info>
      <portlet-preferences>
         <preference>
            <name>expires</name>
            <value>180</value>
         </preference>
         <preference>
            <name>RssXml</name>
            <value>https://xml.weather.yahoo.com/forecastrss?p=33145</value>
            <read-only>false</read-only>
         </preference>
      </portlet-preferences>
   </portlet>
</portlet-app>
```

Portlet可以使用以下首选项进行配置：

<table>
 <tbody>
  <tr>
   <td>startPath</td>
   <td><p>这是portlet的开始路径：它定义最初显示的内容。</p> <p><strong>重要信息</strong>:如果portlet配置为连接到AEM创作实例和发布在与<strong> /</strong>不同的上下文路径上运行的实例，则您需要在这些AEM实例的Html库管理器配置（例如，通过Felix Webconsole）或编辑中启用强制 <strong></strong> CQUrlInfo，并且不会显示首选项对话框。</p> </td>
  </tr>
  <tr>
   <td>htmlSelector</td>
   <td>附加到每个URL的选择器。 默认情况下，这是<strong>portlet</strong>，因此对html页面的所有请求都使用以<strong>.portlet.html结尾的url。</strong> 这允许在AEM中使用自定义脚本来渲染portlet。</td>
  </tr>
  <tr>
   <td>addCssToPortalHeader</td>
   <td><p>默认情况下，AEM的HTML页面中包含的css文件将包含在Portlet中。 禁用此选项将排除默认的css文件。</p> <p>如果启用了此选项，则CSS文件会添加到html页面的标题中，或嵌入到html页面中，具体取决于门户的行为。</p> </td>
  </tr>
  <tr>
   <td>includeToolbar</td>
   <td>默认情况下，工具栏会呈现在内容portlet内以用于管理功能。 禁用此选项后，不会呈现任何工具栏。</td>
  </tr>
  <tr>
   <td>urlParameterNames</td>
   <td><p>替代URL参数名称的列表，该名称可能包含要为Portlet显示的新内容URL。 该列表按从上到下的顺序处理，将使用包含值的第一个参数。 如果未找到URL，则使用默认的URL参数。 提供的URL将按原样使用，无需进行任何进一步修改。</p> <p>此设置是按已部署的Portlet进行的 — 它还可以在OSGi配置中为“Day Portal Director Portlet Bridge”全局配置一些URL参数。</p> </td>
  </tr>
  <tr>
   <td>preferenceDialog</td>
   <td>AEM中首选项对话框的路径 — 如果留空，将使用内置首选项对话框。 默认为/libs/portal/content/prefs.html。</td>
  </tr>
  <tr>
   <td>initialRedirect</td>
   <td>默认情况下，Portlet在第一次调用时对整个门户页面执行Javascript重定向。 这是为了支持现代门户服务器的拖放方案。 在生产中，很少需要此重定向，因此可以关闭此重定向，并将此首选项设置为<em>false</em>。</td>
  </tr>
 </tbody>
</table>

#### OSGi Web控制台{#osgi-web-console}

假设门户服务器在主机localhost上运行，端口8080，并且AEM portlet Web应用程序在Web应用程序上下文&#x200B;*cqportlet*&#x200B;中挂载，则Web控制台的URL为`https://localhost:8080/cqportlet/cqbridge/system/console`。 默认的用户和密码为&#x200B;**admin**。

打开&#x200B;**Configurations**&#x200B;选项卡，然后选择&#x200B;**Portal Directory CQ Server Configuration**。 在此，您可以指定作者和发布实例的基本URL。 [配置Portlet](#configuring-the-portlet)中介绍了此过程。

>[!NOTE]
>
>OSGi Web控制台仅用于在开发（或测试）期间更改配置。 确保阻止向生产系统的控制台发出请求。

### 提供配置{#providing-configurations}

为了支持自动部署和配置配置配置，AEM内容portlet具有内置配置支持，该配置支持尝试从提供给portlet应用程序的类路径中读取配置。

启动时，会读取系统属性&#x200B;**com.day.cq.portet.config**&#x200B;以检测当前环境。 通常，此属性的值类似于&#x200B;**dev**、**prod**、**test**&#x200B;等。 如果未设置环境，则不会读取任何配置。

如果设置了环境，则会在类路径* ***com/day/cq/portlet/{env}.config**&#x200B;中搜索配置文件，其中&#x200B;**env**&#x200B;被替换为环境的实际值。 此文件应列出此环境的所有配置文件。 这些文件会相对于配置文件的位置进行搜索。 例如，如果文件包含行`my.service.xml,` ，则会从位于`com/day/cq/portlet/my.service.config.`的类路径中读取此文件。文件名由服务的持久性ID组成，后跟&#x200B;**.config**。 在上一个示例中，持久性ID为&#x200B;**my.service**。 配置文件的格式是Apache Sling OSGi安装程序使用的格式。

这意味着，对于每个环境，都需要添加相应的配置文件。 需要在所有这些文件中输入应用于所有环境的配置 — 如果只适用于单个环境，则只需在该文件中输入。 此机制可确保完全控制在哪个环境中读取哪个配置。

可以使用不同的系统属性来检测环境。 指定系统属性&#x200B;**com.day.cq.portet.configproperty**，其中包含要使用的系统属性的名称，而不是&#x200B;**com.day.cq.portet.config**。

#### 缓存和缓存失效{#caching-and-caching-invalidation}

Portlet在其默认配置中，将从AEM WCM收到的响应缓存到用户特定的缓存中。 当发布实例的内容发生更改时，缓存需要失效。 为此，在AEM WCM中，必须在创作实例上配置复制代理。 也可以手动刷新缓存。 本节将介绍这两个过程。

Portlet可以使用其自己的缓存进行配置，以便Portlet中的内容显示而无需访问AEM。 该门户在/libs/portal/director中以内容形式提供。 要访问内容，请启动AEM实例，然后使用CRXDE Lite或Webdav从该位置下载文件。

您可以在运行时部署此包，也可以在部署前将其添加到Portlet Web应用程序的`WEB-INF/lib/resources/bundles`中。

部署缓存后，Portlet会缓存发布实例中的内容。 使用AEM的调度程序刷新，Portlet缓存可以失效。 要配置Portlet以使用其自己的缓存，请执行以下操作：

1. 在作者中配置以门户服务器为目标的复制代理。
1. 假定门户服务器在主机&#x200B;**localhost**、**port 8080 **上运行，并且AEM portlet Web应用程序在上下文&#x200B;**cqportlet**&#x200B;中挂载，则用于刷新缓存的url为`https://localhost:8080/cqportlet/cqbridge/cqpcache?Path=$(path)`。 使用GET作为方法。
   **注意：** 您可以发送名为Path **的http标头，而不是使用请求**&#x200B;参数。

#### 通过复制代理{#flushing-the-cache-via-replication-agent}刷新缓存

与正常的调度程序失效一样，复制代理也可以配置为定向门户的AEM portlet缓存。 配置复制代理后，每次常规页面激活都会刷新门户缓存。

如果运行AEM Portlet的多个门户节点，则需要为每个节点创建一个代理，如此过程中所述。

要为门户配置复制代理，请执行以下操作：

1. 登录到创作实例。
1. 在网站选项卡中，单击&#x200B;*工具*&#x200B;选项卡。
1. 单击&#x200B;**新建页面……复制代理**&#x200B;中的&#x200B;**新……**&#x200B;菜单。

   ![screen_shot_2012-02-15at40647pm](assets/screen_shot_2012-02-15at40647pm.png)

1. 在&#x200B;*模板*&#x200B;中，选择&#x200B;*复制代理*，然后输入代理的名称。 单击&#x200B;*创建*。

   ![screen_shot_2012-02-15at40817pm](assets/screen_shot_2012-02-15at40817pm.png)

1. 双击您刚刚创建的复制代理。 由于尚未配置，因此显示为无效。

   ![screen_shot_2012-02-15at41001pm](assets/screen_shot_2012-02-15at41001pm.png)

1. 单击&#x200B;**编辑。**
1. 在&#x200B;**设置**&#x200B;选项卡中，选中&#x200B;**已启用**&#x200B;复选框，选择&#x200B;**调度程序刷新**&#x200B;作为序列化类型，然后输入重试超时(例如，60000)。

   ![screen_shot_2012-02-15at42101pm](assets/screen_shot_2012-02-15at42101pm.png)

1. 单击&#x200B;**Transport**&#x200B;选项卡。
1. 在&#x200B;**URI**&#x200B;字段中，输入Portlet的刷新URI(URL)。 URI的格式如下：

   ```xml
   https://<wps-host>:<port>/<wps-context>/<cq5-portlet-context>/cqbridge/cqpcache
   ```

   ![screen_shot_2012-02-15at42322pm](assets/screen_shot_2012-02-15at42322pm.png)

1. 单击&#x200B;**Extended**&#x200B;选项卡。

   ![screen_shot_2012-02-15at42515pm](assets/screen_shot_2012-02-15at42515pm.png)

1. 在&#x200B;**HTTP方法**&#x200B;字段中，键入&#x200B;**GET**。
1. 在&#x200B;**HTTP标头**&#x200B;字段中，单击&#x200B;**+**&#x200B;以添加新条目并键入&#x200B;**路径：{path}**。
1. 如有必要，单击&#x200B;**Proxy**&#x200B;选项卡，并向代理输入代理信息。
1. 单击&#x200B;**确定**&#x200B;以保存更改。
1. 要测试连接，请单击&#x200B;**Test Connection**&#x200B;链接。 出现日志消息，指示复制测试是否成功。 例如：

   ![screen_shot_2012-02-15at42639pm](assets/screen_shot_2012-02-15at42639pm.png)

#### 手动刷新Portlet缓存{#manually-flushing-the-portlet-cache}

您可以通过访问为复制代理配置的相同URL来手动刷新Portlet缓存。 有关URL的形式，请参阅[刷新缓存](#flushing-the-cache-via-replication-agent) 。 此外，需要使用URL参数Path=&lt;path>扩展URL，以指示要刷新的内容。

例如：

`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=*` 刷新完整缓存。`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=/content/mypage/xyz` 从缓 `/content/mypage/xyz` 存中刷新。

### 门户安全{#portal-security}

入口是驱动认证机制。 您可以与技术用户、门户用户、组等登录AEM。 Portlet无权访问门户中用户的密码，因此，如果Portlet不知道要成功登录用户的所有凭据，则必须使用SSO解决方案。 在这种情况下， AEM Portlet会将所有必需的信息转发给AEM，而又会将此信息转发给基础AEM存储库。 此行为可插拔，并可进行自定义。

### 发布时的身份验证{#authentication-on-publish}

本节介绍Portlet在与基础AEM WCM实例通信时可使用的身份验证模式。

默认情况下，不会向AEM的发布实例发送用户信息；内容始终显示为匿名用户。 如果应从AEM传递用户特定信息，或者如果需要对发布进行用户身份验证，则必须启用此设置。

#### 访问Portlet的身份验证配置{#accessing-the-portlet-s-authentication-configuration}

Portlet在AEM WCM实例中使用的身份验证配置选项在Web控制台中可用（OSGi配置）。

>[!NOTE]
>
>使用AEM时，可以通过多种方法来管理OSGi服务（控制台或存储库节点）的配置设置。
>
>有关完整的详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md) 。

要访问Portlet的身份验证配置，请执行以下操作：

1. 通过以下URL访问Web控制台：

   `https://localhost:8080/cqportlet/cqbridge/system/console`

   例如，在其默认配置中：

   `https://wps-host:10040/wps/PA_CQ5_Portlet/cqbridge/system/console`

1. 登录到Web控制台。 默认凭据为`admin/admin`。
1. 在控制台中，选择&#x200B;**Configuration**。
1. 在&#x200B;**配置**&#x200B;菜单中，选择要配置的特定服务。 服务由OSGi框架中的Portlet提供。

   | 服务名称 | 描述 |
   |---|---|
   | Day Portal Director Authenticator | 配置用于AEM WCM实例的身份验证模式。 根据所选的模式，可以指定技术用户或SSO Cookie的名称。 此外，还可以启用AEM WCM发布实例的身份验证。 |
   | Day Portal Director文件缓存 | 配置Portlet如何缓存其从AEM WCM实例收到的响应的参数。 |
   | Day Portal Director HTTP客户端服务 | 配置portlet如何通过HTTP连接到基础AEM WCM实例。 例如，您可以指定代理服务器。 |
   | Day Portal Director区域设置处理程序 | 配置Portlet支持的区域设置。 对AEM WCM实例的请求基于用户区域设置；例如，用户语言*德语*将请求`/content/geometrixx/de/`.... |
   | 日门户Director权限管理器 | 根据当前登录的用户配置Portlet是否应测试“网站”选项卡。 |
   | Day Portal Director工具栏渲染器 | 自定义Portlet工具栏的呈现。 |

1. 此外，您还可以配置Web控制台和日志记录服务。 例如，您可以通过单击Apache Felix OSGi管理控制台链接来更改Web控制台的管理员凭据。

#### 技术用户模式{#technical-user-mode}

在默认模式下，Portlet为AEM WCM创作实例发出的所有请求都将使用同一技术用户进行身份验证，而不考虑当前的门户用户。 默认情况下，“技术用户”模式处于启用状态。 在OSGi管理控制台的相应配置屏幕中启用/禁用此模式：

如果启用了&#x200B;**在Publish**&#x200B;上进行身份验证，则指定的技术用户必须存在于AEM WCM创作实例和发布实例中。 确保为用户授予足够的访问权限，以便进行创作工作。

#### 单点登录 {#sso}

Portlet支持开箱即用的AEM SSO。 验证器服务可以配置为使用SSO，并将格式为&#x200B;**Basic**&#x200B;的当前门户用户作为名为`cqpsso`的Cookie传输到AEM。 AEM应配置为对路径/使用SSO身份验证处理程序。 此处还需要配置Cookie名称。

需要相应地配置AEM存储库的`crx-quickstart/repository/repository.xml`:

```xml
<LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
  ...
  <param name="trust_credentials_attribute" value="TrustedInfo"/>
  <param name="anonymous_principal" value="anonymous"/>
</LoginModule>
```

#### SSO身份验证模式{#sso-authentication-mode}

Portlet可以使用单点登录(SSO)方案来验证AEM WCM。 在此模式下，当前登录到门户的用户将以SSO Cookie的形式转发到AEM WCM。 如果使用SSO模式，则对AEM Portlet具有访问权限的所有门户用户都必须知晓基础AEM WCM实例，通常以AEM WCM连接到LDAP的形式，或通过事先手动创建用户的方式。 此外，在portlet中启用SSO之前，基础AEM WCM创作实例（以及发布实例，如果&#x200B;**在发布时进行身份验证**）需要配置为接受基于SSO的请求。

要配置Portlet以使用SSO身份验证模式，请完成以下步骤（在以下各节中有详细描述）：

* 启用AEM WCM的存储库以接受可信凭据。
* 在AEM WCM中启用SSO身份验证。
* 在AEM Portlet中启用SSO身份验证。

#### 使AEM WCM的存储库接受可信凭据{#enabling-aem-wcm-s-repository-to-accept-trusted-credentials}

在为AEM WCM启用SSO之前，需要将基础存储库配置为接受AEM WCM提供的可信凭据。 要实现此目的，请配置AEM repository.xml。

1. 在安装了AEM WCM的文件系统中，打开以下文件：

   `//crx-quickstart/repository/repository.xml`

1. 在XML文件中，找到&#x200B;**LoginModule**&#x200B;的条目，并将trust_credentials_attribute添加到其配置中：

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
     <param name="anonymous_principal" value="anonymous"/>
   </LoginModule>
   ```

1. 重新启动AEM WCM以使更改生效。

#### 在AEM WCM {#enabling-sso-authentication-in-the-aem-wcm}中启用SSO身份验证

要在AEM WCM中启用SSO，请访问AEM WCM的Apache Felix Web管理控制台(OSGi)中的相关配置条目：

1. 通过位于https://&lt;AEM-host>:&lt;port>/system/console的URI访问控制台。
1. 在“配置”菜单中，选择SSO身份验证处理程序。 在此示例中，SSO处理程序根据AEM Portlet提供的Cookie接受所有路径的SSO请求。 您的配置可能会有所不同。

   | 路径 | / | 为所有请求启用SSO处理程序 |
   |---|---|---|
   | Cookie名称 | cqpsso | Portlet在Portlet的OSGi控制台中配置的Cookie的名称。 |

1. 单击&#x200B;**Save**&#x200B;以启用SSO。 SSO现在是主要的身份验证方案。

对于AEM WCM收到的每个请求，首先尝试基于SSO的身份验证。 失败时，将执行回退到通常的基本身份验证方案。 因此，与AEM WCM（不使用单点登录）的正常连接仍然可能。

#### 在AEM Portlet {#enabling-sso-authentication-in-a-aem-portlet}中启用SSO身份验证

为了使基础AEM WCM实例接受SSO请求，必须将portlet的身份验证模式从&#x200B;**Technical**&#x200B;切换到&#x200B;**SSO**。

要在AEM Portlet中启用SSO身份验证，请执行以下操作：

1. 通过位于https://&lt;aem-host>:&lt;port>/system/console的URI访问控制台。
1. 在“配置”菜单中，从可用配置列表中选择Day Portal Director Authenticator 。
1. 在模式中，选择SSO。 将其他参数保留为其默认值。

   ![chlimage_1-133](assets/chlimage_1-135.png)

1. 单击“保存”为Portlet启用SSO。

   出于测试目的，在AEM WCM中以管理员权限创建同一用户后，可以使用门户的管理用户访问portlet。

执行此过程后，请求将使用SSO进行身份验证。 HTTP通信中的典型代码片段显示存在以下特定于SSO和Portlet的标头：

```xml
C-12-#001898 -> [GET /mynet/en/_jcr_content/par/textimage/image.img.png HTTP/1.1 ]
C-12-#001963 -> [cq5:locale: en ]
C-12-#001979 -> [cq5:used-locale: en ]
C-12-#002000 -> [cq5:locales: en,en_US ]
C-12-#002023 -> [cqp:user: wpadmin ]
C-12-#002042 -> [cqp:portal: IBM WebSphere Portal/6.1 ]
C-12-#002080 -> [cqp:windowid: 7_CGAH47L000CE302V2KFNOG0084 ]
C-12-#002124 -> [cqp:windowstate: normal ]
C-12-#002149 -> [cqp:portletmode: view ]
C-12-#002172 -> [User-Agent: Jakarta Commons-HttpClient/3.1 ]
C-12-#002216 -> [Host: 10.0.0.68:4502 ]
C-12-#002238 -> [Cookie: $Version=0; cqpsso=Basic+d3BhZG1pbg%3D%3D ]
C-12-#002289 -> [ ]
```

### 启用PIN身份验证{#enabling-pin-authentication}

如果您没有使用AEM内容portlet的默认内联编辑功能，但希望门户外部的创作和管理部分直接在AEM创作实例中使用，则应该启用PIN身份验证。 您还需要更改管理按钮的配置。

要打开网站管理页面或从portlet编辑页面，AEM内容portlet使用新的pin身份验证。 默认情况下，PIN身份验证处于禁用状态，因此必须在AEM中进行以下配置更改：

1. 通过在repository.xml文件中添加可信信息，在AEM中启用可信身份验证：

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
   </LoginModule>
   ```

1. 在OSGi配置控制台中，默认位于https://localhost:4502/system/console/configMgr ，从下拉菜单中选择&#x200B;**CQ PIN身份验证处理程序**。
1. 编辑&#x200B;**URL根路径**&#x200B;参数，以仅包含单个值&#x200B;**/**。

### 权限 {#privileges}

Portlet的某些功能受权限保护。 当前用户需要具有此权限才能访问此函数。 预定义了以下权限：

* &quot;toolbar&quot; :这是查看/使用Portlet中的工具栏的一般权限。
* &quot;prefs&quot; :如果用户具有此权限，则允许用户查看/更改Portlet的首选项。
* &quot;cq-author:edit&quot; :使用此权限，允许用户调用内容的编辑视图。
* &quot;cq-author:preview&quot; :使用此权限，用户可以查看预览。
* &quot;cq-author:siteadmin&quot; :通过此权限，允许用户在AEM中打开siteadmin。

管理权限的最佳方法是使用门户角色并为这些权限分配角色。 这可以通过OSGi配置来完成。 可以为“Day Portal Director权限管理器”配置每个权限的一组角色。 如果用户具有其中一个角色，则用户具有相应的权限。

此外，还可以根据每个portlet实例库的访问来定义此角色。 Portlet的“首选项”对话框包含用于上述每种权限的输入字段。 对于每个权限，可以配置以逗号分隔的portlet角色列表。 如果配置了值，则它将覆盖“Day Portal Director Privilege Manager”服务中的全局配置，并且在角色未合并时可能需要从此全局设置中添加相同的角色！ 如果未指定任何值，则使用全局配置。

### 自定义AEM Portlet应用程序{#customizing-the-aem-portlet-application}

提供的AEM portlet应用程序会像AEM一样在Web应用程序内启动OSGi容器。 此架构让您能够利用OSGi的所有优势：

* 易于更新和扩展
* 在门户服务器不进行任何交互的情况下提供Portlet的热更新
* 易于自定义portlet

### 工具栏按钮{#toolbar-buttons}

工具栏及其按钮是可配置的，并可进行自定义。 您可以在工具栏中添加自己的按钮，或定义在哪种模式下显示的按钮。 每个按钮都是可通过OSGi配置配置的OSGi服务。

OSGi Web控制台在&#x200B;**Configuration**&#x200B;选项卡上列出了所有按钮配置。 对于每个按钮，您可以定义此按钮在哪种模式下显示。 例如，您可以通过删除所有模式来禁用按钮。

默认情况下， AEM内容portlet使用内联编辑功能。 但是，如果您希望切换到AEM创作实例进行编辑，请启用&#x200B;**SiteAdmin Button**&#x200B;和&#x200B;**ContentFinder Button**，但禁用&#x200B;**Edit Button**。 在这种情况下，请确保在AEM中正确配置PIN身份验证。

可以通过Portlet的Felix Web控制台安装包来自定义Portlet的工具栏布局，该包包含预定义位置的自定义CSS/HTML。

#### 束结构{#bundle-structure}

以下是包结构示例：

```xml
$ jar tvf target/toolbarlayout-0.0.1-SNAPSHOT.jar | awk '{print $8}'
META-INF/
META-INF/MANIFEST.MF
/com/day/cq/portlet/toolbar/layout/
/com/day/cq/portlet/toolbar/layout/author.gif
/com/day/cq/portlet/toolbar/layout/back.gif
/com/day/cq/portlet/toolbar/layout/button.html
/com/day/cq/portlet/toolbar/layout/edit.gif
/com/day/cq/portlet/toolbar/layout/manage.html
/com/day/cq/portlet/toolbar/layout/publish.html
/com/day/cq/portlet/toolbar/layout/refresh.gif
/com/day/cq/portlet/toolbar/layout/siteadmin.gif
/com/day/cq/portlet/toolbar/layout/toolbar.css
```

META-INF文件夹包含OSGi将其标识为包所需的MANIFEST.MF文件。 显示如下：

```xml
Manifest-Version: 1.0
Built-By: djaeggi
Created-By: Apache Maven Bundle Plugin
Import-Package: com.day.cq.portlet.toolbar.layout
Bnd-LastModified: 1234178347159
Export-Package: com.day.cq.portlet.toolbar.layout
Bundle-Version: 0.0.1.SNAPSHOT
Bundle-Name: Company CQ5 Portal Director Portlet Toolbar Layout
Bundle-Description: This bundle provides a custom layout for the CQ5 P
 ortal Director Portlet Toolbar.
Build-Jdk: 1.5.0_16
Bundle-ManifestVersion: 2
Bundle-SymbolicName: com.day.cq.portlet.company.toolbarlayout
Tool: Bnd-0.0.255
```

HTML/CSS/images位于/com/day/cq/portlet/toolbar/layout文件夹内这一事实是Portlet强制要求的，不能更改。 同样，MANIFEST.MF中的Import-Package和Export-Package标头也必须称为/com/day/cq/portlet/toolbar/layout。 Bundle-SymbolicName必须是唯一且完全限定的包名称。

您可以使用Maven之类的工具来构建该文件，也可以手动创建此类jar文件，并设置相关标头，如此部分所示。

#### Portlet工具栏视图{#portlet-toolbar-views}

Portlet的工具栏基本上有两种视图状态。 每个视图和关联的按钮都可以使用相应的HTML文件进行自定义。

#### 发布视图{#publish-view}

发布视图只有一个按钮，可将工具栏切换到管理视图。 发布视图由[上一个包](/help/sites-deploying/configuring-osgi.md#bundles)中的publish.html文件表示。 在HTML中，您可以使用以下占位符，在呈现时，这些占位符将由Portlet替换为相应的内容：

#### 发布视图占位符{#publish-view-placeholders}

| 占位符字符串 | 描述 |
|---|---|
| {buttonManage} | 占位符由&#x200B;**Manage**&#x200B;按钮替换，该按钮将portlet状态切换到管理状态。 |

#### 管理视图{#manage-view}

“管理”视图包含四个按钮：“编辑”、“网站”选项卡、“刷新”和“返回”。 管理视图由[上一个包](/help/sites-deploying/configuring-osgi.md#bundles)中的manage.html文件表示。 在HTML中，您可以使用以下占位符，在呈现时，这些占位符将由Portlet替换为相应的内容：

#### 管理视图占位符{#manage-view-placeholders}

| 占位符字符串 | 描述 |
|---|---|
| {buttonEdit} | 占位符由&#x200B;**Edit**&#x200B;按钮替换，该按钮会在AEM编辑模式下使用当前页面打开一个新窗口。 |
| {buttonWebsites选项卡} | 占位符，替换为打开AEM WCM的“网站”选项卡的按钮。 |
| {buttonRefresh} | 刷新当前视图。 |
| {buttonBack} | 将portlet切换回发布视图。 |

#### 按钮 {#buttons}

按钮在显示的任何视图上，都使用在button.html中定义的相同通用HTML。

在HTML中，您可以使用以下占位符，在呈现时，这些占位符将由Portlet替换为相应的内容：

#### 管理和发布视图按钮{#manage-and-publish-view-buttons}

| 占位符字符串 | 描述 |
|---|---|
| {name} | 按钮的名称，例如**作者、后退、刷新**等。 |
| {id} | 按钮的CSS ID。 |
| {url} | 按钮目标的URL。 |
| {文本} | 按钮的标签。 |
| {onclick} | Javascript **onclick**&#x200B;函数（包含{url}）。 |

button.html文件的示例：

```xml
<div class="cqp_button">

 <a href="#" onclick="{onclick}">

 <img src="/wps/PA_CQ5_Portlet/cqbridge/static/{id}.gif" alt="{text}"
title="{text}"/>

 </a>
</div>
```

#### 安装自定义布局{#installing-a-custom-layout}

要安装自定义布局，请访问Portlet的OSGI Web控制台**包**部分并上载包。

#### 包 {#packages}

如果您需要上传或创建安装软件包，请参阅AEM文档中的包管理器以了解详细说明。

### 链接处理{#link-handling}

所有链接都将被重写，以便在Portal上下文中工作。 默认情况下，会使用带有呈现参数的链接。 可以将门户Director HTML重写器配置为改用操作链接。

您还可以定义要查询的其他请求参数以查看要显示的内容路径。 例如，如果存在从外部到特定内容的链接，则此功能非常有用。

此外，还可以为门户Director HTML重写器配置一个为链接重写定义的排除的正则表达式列表。 例如，如果您具有与外部系统的相对链接，则应将其添加到此排除列表。

### 本地化 {#localization}

AEM内容portlet具有内置的本地化功能，可确保AEM中的内容使用正确的语言。

可分两步完成此操作：

1. 门户目录区域设置检测器通过从门户获取区域设置来检测门户用户的区域设置。 必须在AEM中为此服务配置可用语言的列表。
1. 门户Director区域设置处理程序处理当前请求的本地化。 它采用所请求内容的路径，例如`/content/geometrixx/en/company.html`，并根据配置，使用用户的实际区域设置重写&#x200B;**en**。

门户Director区域设置处理程序可以配置用于检查区域设置信息的路径 — 通常包括`/content`下的所有内容以及路径中区域设置信息的位置。 默认情况下，区域设置处理程序遵循在AEM中构建多语言站点的重新通用化。

如果您的站点没有用于处理路径中区域设置信息的严格规则，则可以使用您自己的实施替换区域设置处理程序。

### 可选OSGi服务{#optional-osgi-services}

可以实施可选的OSGi服务来自定义Portlet的各个部分。 每个服务都对应一个Java接口。 此接口可以通过包实施和部署到Portlet中。

<table>
 <tbody>
  <tr>
   <td>RequestTracker</td>
   <td>每当Portlet显示内容时，请求跟踪器都会收到通知。 这样，您就可以跟踪portlet的调用。</td>
  </tr>
  <tr>
   <td>InvocationContextListener</td>
   <td>在对portlet的每个请求的开始和结束时调用的侦听器。 监听器可用于更改或添加当前请求的信息。<br /> </td>
  </tr>
  <tr>
   <td>ErrorHandler</td>
   <td>呈现阶段错误的自定义错误处理程序。</td>
  </tr>
  <tr>
   <td>HttpProcessor</td>
   <td>此服务可用于向AEM的每次http调用添加信息。</td>
  </tr>
  <tr>
   <td>PortletAction</td>
   <td>向portlet添加自己的操作 — 此操作可通过portlet操作链接调用。</td>
  </tr>
  <tr>
   <td>PortletDecoratorService</td>
   <td>此服务可用于装饰portlet的内容。</td>
  </tr>
  <tr>
   <td>ResourceProvider</td>
   <td>添加您自己的资源提供程序，以通过Portlet资源链接将某些资源交付到客户端。</td>
  </tr>
  <tr>
   <td>TextMapper</td>
   <td>允许您后处理HTML、CSS和Javascript文件。</td>
  </tr>
  <tr>
   <td>工具栏按钮</td>
   <td>在工具栏中添加您自己的按钮。</td>
  </tr>
  <tr>
   <td>UrlMapper</td>
   <td>添加服务以应用自定义url映射或重写。</td>
  </tr>
  <tr>
   <td>UserInfoProvider</td>
   <td>添加您自己的用户信息。 此服务可用于从门户获取信息到portlet。</td>
  </tr>
 </tbody>
</table>

#### 替换默认服务{#replacing-default-services}

以下服务在内容portlet中具有默认实施（具有相应的Java界面）。 要进行自定义，需要将包含新服务实施的包部署到Portlet应用程序中。

在实施此类服务时，请确保将服务的&#x200B;**service.ranking**&#x200B;属性设置为正值。 默认实施使用排名** 0**,Portlet使用排名最高的服务。

| **名称** | **描述** | **默认行为** |
|---|---|---|
| 身份验证器 | 向AEM提供身份验证信息 | 使用可配置的技术用户进行创作和发布。 或者，也可以使用单点登录。 |
| HTMLRewriter | 重写链接、图像等 | 将AEM链接重写到门户链接，可通过UrlMapper和TextMapper扩展 |
| HttpClientService | 处理所有http连接 | 标准实施 |
| LocaleHandler | 处理区域设置信息 | 根据区域设置，重写指向内容的链接。 |
| LocaleDetector | 检测用户的区域设置。 | 使用门户提供的区域设置。 |
| 权限管理器 | 检查用户权限 | 检查在允许用户编辑内容时对创作实例的访问权限 |
| ToolbarRenderer | 呈现工具栏 | 添加工具栏功能 |

### Portlet事件{#portlet-events}

portlet API(JSR-286)指定portlet事件。 AEM内容portlet具有集成的桥，它将AEM portlet事件作为OSGi事件分发为portlet事件 — 这使处理portlet事件变得可插拔。

如果要处理特定事件，请在部署描述符中声明这些事件作为接收事件（或通过门户服务器配置它），并实施声明EventHandler接口的OSGi服务（请参阅OSGi EventAdmin规范）。

每当发生portlet事件时，都会调用您的处理程序发送特定的OSGi事件。 处理程序获取所有上下文信息，并可相应地更新Portlet的状态或发送新事件。 基本上，在句柄方法内部可以使用portlet事件阶段的所有功能。

## 将AEM用作门户{#using-aem-as-a-portal}

使用Portlet组件将Portlet窗口添加到AEM页面。 安装到应用程序服务器的共享库使Portlet组件能够检测已部署的Portlet应用程序。

要将AEM用作门户，请执行以下任务：

1. 安装Portlet组件和共享库。
1. 将Portlet组件添加到Sidekick。
1. 配置和部署Web应用程序，该应用程序包含要在门户组件中显示的Portlet。
1. 将Portlet组件添加到页面并选择要显示的Portlet。

>[!NOTE]
>
>只有将AEM部署为Web应用程序时，才能使用portlet组件。 ([请参阅使用应用程序服务器安装AEM](/help/sites-deploying/application-server-install.md)。)

### 安装Portlet组件{#installing-the-portlet-component}

AEM快速入门JAR文件包含Portlet组件文件。 要获取文件(cq-portlet-components.zip)，您可以执行快速入门，或解压缩内容。

1. 执行或提取快速入门JAR文件的内容，并相应地找到cq-portlet-components.zip文件：

   * 执行快速启动：crx-quickstart/opt/portal
   * 提取快速入门内容：静态/选择/门户

1. 打开部署到应用程序服务器的CQ5创作实例的包管理器。 (https://*appserverhost*:*port*/cq5author/crx/packmgr)

1. 使用包管理器[上载并安装](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) cq-portlets-components.zip包。

   该包将cq-portlet-director-sharedlibs-x.x.x.jar安装在存储库的/libs/portal/director文件夹中。

1. 将cq-portlet-director-sharedlibs-x.x.x.jar复制到硬盘。 使用任何方式获取文件，例如FileVault或WebDAV客户端。
1. 将cq-portlet-director-sharedlibs.x.x.x.jar文件移动到应用程序服务器的共享库文件夹中，以便类可用于部署的portlet应用程序。

### 将Portlet组件添加到Sidekick {#adding-the-portlet-component-to-sidekick}

将portlet组件添加到段落系统，以便作者可以使用它。

1. 在Sidekick中，单击标尺图标以进入设计模式。
1. 在第一段上方的`Design of par`标题旁边，单击&#x200B;**编辑**。

1. 在&#x200B;**General**&#x200B;组件类别中，选中Portlet组件旁边的复选框，然后单击“确定”。

![chlimage_1-25](assets/chlimage_1-25.jpeg)

### 配置和部署Portlet应用程序{#configuring-and-deploying-your-portlet-applications}

将portlet部署到应用程序服务器Web容器，以便它们可用于门户组件。 在部署Portlet应用程序之前，您需要配置该应用程序，以便它加载AEM Portal容器Servlet。 此配置使Portlet组件能够访问Portlet。

1. 提取Portlet应用程序WAR文件的内容。

   **提示：** jar xf nameofapp *.war命*&#x200B;令会提取文件。

1. 在文本编辑器中打开web.xml文件。
1. 在Web应用程序元素中添加以下Servlet配置：

   ```xml
   <servlet>
           <servlet-name>slingportal</servlet-name>
           <servlet-class>org.apache.sling.portal.container.api.ContainerServlet</servlet-class>
           <load-on-startup>1</load-on-startup>
   </servlet>
   <servlet-mapping>
           <servlet-name>slingportal</servlet-name>
           <url-pattern>/SlingPortletInvoker</url-pattern>
   </servlet-mapping>
   ```

1. 保存web.xml文件并重新打包WAR文件。

   **提示：** 命 `jar cvf nameofapp.war *` 令将当前目录的内容添加到nameofapp.war文件中。

1. 将Portlet应用程序部署到应用程序服务器。 有关信息，请参阅应用程序服务器相关文档。

### 将portlet添加到您的AEM页{#adding-portlets-to-your-aem-page}

使用Portal组件将Portlet窗口添加到网页。 使用组件属性指定要显示的portlet。

1. 在网页上，将&#x200B;**Portlet**&#x200B;组件从Sidekick中的“常规”组拖到该页。

   >[!NOTE]
   >
   >将组件拖到页面后，重新加载页面以确保其正常工作。

1. 双击组件以打开Portlet属性。
1. 在&#x200B;**Portlet实体**&#x200B;下拉菜单中，从列表中选择Portlet。
1. 根据您是否要查看Portlet的标题栏，选择或清除**隐藏标题栏**复选框。
1. 在&#x200B;**Portlet窗口**&#x200B;字段中，根据需要输入唯一的Portlet窗口ID。

   >[!NOTE]
   >
   >如果您计划在同一页面上多次使用同一Portlet，请为每个Portlet指定不同的窗口ID。

1. 单击&#x200B;**确定**。Portlet显示在您的AEM页面上。

   ![chlimage_1-136](assets/chlimage_1-136.png)

## 在Portlet {#installing-configuring-and-using-aem-in-a-portlet}中安装、配置和使用AEM

要访问AEM WCM提供的内容，需要为门户服务器安装AEM Portal Director Portlet。 为此，请使用本节中提供的步骤来安装、配置Portlet并将其添加到门户页面。

默认情况下，Portlet会连接到localhost:4503处的发布实例，并连接到localhost:4502处的创作实例。 这些值可以在部署Portlet期间进行更改。 门户控制器在/libs/portal/directory下的存储库中以内容形式提供。 您需要先下载应用程序战争文件，然后再使用它。

### 下载战争文件{#downloading-the-war-file}

1. 使用Webdav或CRXDE Lite，导航到/libs/portal/director。

1. 下载&#x200B;*cq-portlet-webapp.war*。

>[!NOTE]
>
>这些过程尽可能地通用，但以Websphere门户为例；请注意，其他Web门户的程序各不相同。 尽管所有Web门户的步骤基本相同，但您需要为特定Web门户重新调整这些步骤的用途。

#### 安装Portlet {#installing-the-portlet}

要安装Portlet，请执行以下操作：

1. 使用管理员权限登录到门户。
1. 导航到Web门户的Portlet管理部分。
1. 单击“安装”并浏览到您下载的AEM portlet应用程序(cq-portlet-webapp.war)，然后输入有关portlet的其他重要信息。

   对于其他基本Portlet信息，您可以接受默认值或更改值。 如果接受默认值，则Portlet可在https://&lt;wps-host>:&lt;port>/wps/PA_CQ5_Portlet中找到。 Portlet提供的OSGi管理控制台位于https://&lt;wps-host>:&lt;port>/wps/ PA_CQ5_Portlet/cqbridge/system/console（默认用户名/密码为admin/admin）。

1. 通过选中该选项或复选框并保存您的更改，确保Portlet应用程序自动启动。 您会看到一条消息，指示安装成功。

#### 配置Portlet {#configuring-the-portlet}

安装Portlet后，您需要对其进行配置，以便它知道基础AEM实例（创作和发布）的URL。 您还可以配置其他选项。

要配置Portlet，请执行以下操作：

1. 在应用程序服务器的门户管理窗口中，导航到Portlet管理，其中列出了所有Portlet，然后选择AEM Portal Director Portlet。
1. 根据需要配置portlet。 例如，您可能需要更改创作和发布实例的URL以及开始路径的URL。 [Portlet首选项](/help/sites-administering/aem-as-portal.md#portlet-preferences)中介绍了默认配置。

   >[!NOTE]
   >
   >如果portlet配置为连接到AEM创作实例和发布实例，这些实例在与** /**不同的上下文路径上运行，则您需要在这些AEM实例的Html库管理器配置中启用强制&#x200B;**CQUrlInfo**（例如，通过Felix Webconsole）或编辑将不起作用，并且将不显示首选项对话框。

1. 在应用程序服务器中保存配置更改。

1. 导航到Portlet的OSGI管理控制台。 默认位置为`https://<wps-host>:<port>/wps/PA_CQ5_Portlet/cqbridge/system/console/configMgr`。 默认用户名/密码为&#x200B;**admin/admin**。

1. 选择&#x200B;**Day Portal Director CQ服务器配置**&#x200B;配置并编辑以下值：

   * **作者基本URL**:AEM创作实例的基本URL。
   * **发布基本URL**:AEM发布实例的基本URL。
   * **作者用作发布**:创作实例是否用作发布实例（用于开发）？

   ![chlimage_1-137](assets/chlimage_1-137.png)

1. 单击&#x200B;**保存**。现在，您可以将portlet添加到门户页面并使用门户。

### 内容URL {#content-urls}

当从AEM请求内容时，Portlet使用当前显示模式（发布或创作）和当前路径来组合完整的URL。 如果使用默认值，则第一个url为`https://localhost:4503/content/geometrixx/en.portlet.html`。 `htmlSelector`的值会自动添加到扩展之前的URL中。

如果Portlet切换到帮助模式并选择了`appendHelpViewModeAsSelector` ，则还会附加`help`选择器，例如`https://localhost:4503/content/geometrixx/en.portlet.html.help`。 如果最大化了Portlet窗口并选择了`appendMaxWindowStateAsSelector` ，则还会附加选择器，例如`https://localhost:4503/content/geometrixx/en.portlet.max.help`。

选择器可以在AEM中评估，而不同的模板可用于不同的选择器。

### 在AEM {#using-a-content-url-map-in-aem}中使用内容Url映射

通常，开始路径直接指向AEM中的内容。 但是，如果要在AEM中而不是portlet首选项中维护起始路径，则可以将起始路径指向AEM中的内容映射，如`/var/portlets`。 在这种情况下，在AEM中运行的脚本可以使用portlet中提交的信息来确定哪个url是起始URL。 它应会发出到正确URL的重定向。

#### 将Portlet添加到门户页面{#adding-the-portlet-to-the-portal-page}

要将Portlet添加到门户页面，请执行以下操作：

1. 确保您位于应用程序服务器的管理窗口中，并导航到管理页面的位置。 （例如，在WebSphere 6.1中，单击&#x200B;**管理页面**）。
1. 选择Portlet的名称，然后选择现有页面或创建新页面。
1. 编辑页面布局。
1. 选择Portlet并将其添加到容器。
1. 保存更改。

#### 使用Portlet {#using-the-portlet}

要访问您添加到Portlet的页面，请执行以下操作：

1. 在Portlet的个性化菜单中，将Portlet配置为在Portal中配置。
1. 打开配置（Portlet显示在Portlet配置中配置的发布开始URL），并根据需要进行编辑，然后保存它们。
