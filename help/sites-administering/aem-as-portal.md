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
translation-type: tm+mt
source-git-commit: b97452eb42275d889a82eb9364b5daf7075fcc41
workflow-type: tm+mt
source-wordcount: '6097'
ht-degree: 0%

---


# AEM门户和Portlet{#aem-portals-and-portlets}

本文档将介绍以下内容：

* AEM门户架构
* 将AEM管理和配置为门户
* 将AEM用作门户
* 在portlet中安装、配置和显示AEM内容（例如，Web服务器）

## AEM门户体系架构{#aem-portal-architecture}

AEM门户体系结构包括门户和portlet的定义。

### 什么是门户？{#what-is-a-portal}

门户是一个Web应用程序，它提供个性化、单一登录、来自不同来源的内容集成，并托管信息系统的表示层。

您可以在AEM中运行符合JSR 286规范的portlet。 portlet组件允许您在页面上嵌入portlet。 请参阅[管理AEM Content Portlet](#administeringthecqcontentportlet)。

### 什么是portlet?{#what-is-a-portlet}

Portlet是部署在容器内的Web组件，用于生成动态内容。 portlet接口被打包并部署为portlet容器内的。war文件。 如果您以门户的身份运行AEM，则需要portlet的。war文件来运行portlet。

要将AEM内容配置为显示在门户中，请参阅[在portlet](#installingconfiguringandusingcqinaportlet)中安装、配置和使用AEM。

### AEM门户Director{#aem-portal-director}

>[!CAUTION]
>
>AEM PortalDirector从AEM 6.4起已弃用。请参阅[已弃用和已删除功能](https://helpx.adobe.com/experience-manager/6-4/release-notes/deprecated-removed-features.html)。

## 管理AEM内容Portlet {#administering-the-aem-content-portlet}

AEM内容portlet允许您在门户中显示AEM内容。 portlet在`/crx-quickstart/opt/portal`上可用，并可以通过各种方式进行自定义。 例如，您可以通过部署您自己的身份验证服务来为AEM生成所需的身份验证信息以覆盖默认行为，来自定义SSO/身份验证处理。 插件使用定义的API，它允许您根据API构建插件来添加您自己的功能。 插件可部署到正在运行的portlet中。 要正常工作，它需要AEM作者配置和发布实例以及要在启动时显示的内容路径。

某些配置可以通过portlet首选项进行更改，而其他配置则可以通过OSGi服务配置进行更改。 您可以使用&#x200B;**config**&#x200B;文件或OSGi Web控制台更改这些配置。

### Portlet首选项{#portlet-preferences}

可以在部署时在门户服务器中配置门户首选项，或在部署portlet Web应用程序之前编辑&#x200B;**WEB-INF/portlet.xml**&#x200B;文件。 默认情况下，portlet.xml文件如下所示：

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
   <td><p>这是portlet的开始路径：它定义最初显示的内容。</p> <p><strong>重要说明</strong>:如果portlet配置为连接到AEM作者并发布在与／不同的上下文路径上运行的实例<strong> ,</strong>则需要在这些AEM实例的Html库管理器配置中启用强制 <strong></strong> CQUrlInfo（例如，通过Felix Webconsole），否则编辑将无法工作，并且不会显示首选项对话框。</p> </td>
  </tr>
  <tr>
   <td>htmlSelector</td>
   <td>附加到每个url的选择器。 默认情况下，它为<strong>portlet</strong>，因此对html页的所有请求都使用以<strong>.portlet.html结尾的url。</strong> 这允许在AEM中使用自定义脚本进行portlet渲染。</td>
  </tr>
  <tr>
   <td>addCssToPortalHeader</td>
   <td><p>默认情况下，AEM的HTML页面中包含的css文件会包含在portlet中。 禁用此选项将排除默认的css文件。</p> <p>如果启用此选项，则CSS文件将添加到html页面的标题中，或嵌入到html页面中，具体取决于门户的行为。</p> </td>
  </tr>
  <tr>
   <td>includeToolbar</td>
   <td>默认情况下，在内容portlet中显示一个工具栏以用于管理功能。 通过禁用此选项，不会呈现任何工具栏。</td>
  </tr>
  <tr>
   <td>urlParameterNames</td>
   <td><p>替代URL参数名称的列表，可能包含要为portlet显示的新内容URL。 从上到下处理列表，使用包含值的第一个参数。 如果未找到URL，则使用默认URL参数。 按原样使用提供的URL，无需进一步修改。</p> <p>此设置是按部署的portlet进行的——还用于在“Day PortalDirectorportlet Bridge”的OSGi配置中全局配置一些url参数。</p> </td>
  </tr>
  <tr>
   <td>preferenceDialog</td>
   <td>AEM中首选项对话框的路径——如果留空，将使用内置首选项对话框。 默认为/libs/portal/content/prefs.html。</td>
  </tr>
  <tr>
   <td>initialRedirect</td>
   <td>默认情况下，portlet在第一次调用时执行整个门户页面的javascript重定向。 这支持现代门户服务器的拖放方案。 在生产中，很少需要此重定向，因此可以关闭此首选项，将此首选项设置为<em>false</em>。</td>
  </tr>
 </tbody>
</table>

#### OSGi Web控制台{#osgi-web-console}

假定门户服务器运行于主机localhost上，端口8080，并且AEM portlet Web应用程序已装入Web应用程序上下文&#x200B;*cqportlet*&#x200B;中，则Web控制台的URL为`https://localhost:8080/cqportlet/cqbridge/system/console`。 默认用户和密码为&#x200B;**admin**。

打开&#x200B;**Configurations**&#x200B;选项卡，选择&#x200B;**Portal Directory CQ Server Configuration**。 在此处，您指定作者和发布实例的基本URL。 此过程在[配置Portlet](#configuring-the-portlet)中有介绍。

>[!NOTE]
>
>OSGi Web控制台仅用于在开发（或测试）过程中更改配置。 确保阻止对生产系统控制台的请求。

### 提供配置{#providing-configurations}

为了支持自动部署和配置配置设置，AEM content portlet内置了配置支持功能，它尝试从提供到portlet应用程序的类路径中读取配置。

启动时，读取系统属性&#x200B;**com.day.cq.portet.config**&#x200B;以检测当前环境。 通常，此属性的值类似于&#x200B;**dev**、**prod**、**test**&#x200B;等。 如果未设置环境，则不会读取配置。

如果设置了环境，则在类路径中搜索配置文件：* ***com/day/cq/portlet/{env}.config**，其中&#x200B;**env**&#x200B;替换为环境的实际值。 此文件应列表此环境的所有配置文件。 这些文件会相对于配置文件的位置进行搜索。 例如，如果文件包含行`my.service.xml,`，则从位于`com/day/cq/portlet/my.service.config.`的类路径中读取此文件。文件的名称由服务的持久性ID组成，后跟&#x200B;**.config**。 在上一个示例中，持久性ID为&#x200B;**my.service**。 配置文件的格式是Apache Sling OSGi安装程序使用的格式。

这意味着，对于每个环境，都需要添加相应的配置文件。 应应用于所有环境的配置需要输入到所有这些文件中——如果仅用于单个环境，则只需在该文件中输入。 此机制确保完全控制读取哪个配置的环境。

可以使用不同的系统属性来检测环境。 指定系统属性&#x200B;**com.day.cq.portet.configproperty**，其中包含要使用的系统属性名称，而不是&#x200B;**com.day.cq.portet.config**。

#### 缓存和缓存失效{#caching-and-caching-invalidation}

portlet在其默认配置中将其从AEM WCM收到的响应缓存到用户特定的缓存中。 当发布实例的内容发生更改时，缓存需要失效。 为此，在AEM WCM中，必须在创作实例上配置复制代理。 也可以手动刷新缓存。 本节将介绍这两个过程。

portlet可以配置其自己的缓存，以便portlet中的内容显示而不需要访问AEM。 门户在/libs/portal/director中以内容形式提供。 要访问内容，请开始AEM实例，然后使用CRXDE Lite或Webdav从该位置下载文件。

您可以在运行时部署此捆绑包，也可以在部署前将其添加到portlet Web应用程序的`WEB-INF/lib/resources/bundles`。

部署缓存后，portlet缓存来自发布实例的内容。 使用AEM的调度程序刷新可以使portlet缓存失效。 要配置portlet以使用其自己的缓存，请执行以下操作：

1. 在作者中配置一个目标门户服务器的复制代理。
1. 假定门户服务器运行于主机&#x200B;**localhost**、**port 8080 **，并且AEM portlet Web应用程序安装在上下文&#x200B;**cqportlet**&#x200B;中，用于刷新缓存的url为`https://localhost:8080/cqportlet/cqbridge/cqpcache?Path=$(path)`。 使用GET作为方法。
   **注意：** 您可以发送名为Path的http头，而不是使用请求 **参数**。

#### 通过复制代理{#flushing-the-cache-via-replication-agent}刷新缓存

与正常的调度程序失效一样，复制代理也可以配置为目标门户的AEM portlet缓存。 配置复制代理后，每个常规页面激活都会刷新门户缓存。

如果运行AEM portlet的多个门户节点，您需要为每个节点创建一个代理，如本过程所述。

为门户配置复制代理：

1. 登录到创作实例。
1. 在“网站”选项卡中，单击&#x200B;*“工具”*&#x200B;选项卡。
1. 单击&#x200B;**新建页面……复制代理**&#x200B;中的&#x200B;**新……**&#x200B;菜单。

   ![screen_shot_2012-02-15at40647pm](assets/screen_shot_2012-02-15at40647pm.png)

1. 在&#x200B;*模板*&#x200B;中，选择&#x200B;*复制代理*，然后输入代理的名称。 单击&#x200B;*创建*。

   ![screen_shot_2012-02-15at40817pm](assets/screen_shot_2012-02-15at40817pm.png)

1. 多次-单击您刚刚创建的复制代理。 它显示为无效，因为尚未配置它。

   ![screen_shot_2012-02-15at41001pm](assets/screen_shot_2012-02-15at41001pm.png)

1. 单击&#x200B;**编辑。**
1. 在&#x200B;**设置**&#x200B;选项卡中，选中&#x200B;**已启用**&#x200B;复选框，选择&#x200B;**调度程序刷新**&#x200B;作为序列化类型，然后输入重试超时（例如，60000）。

   ![screen_shot_2012-02-15at42101pm](assets/screen_shot_2012-02-15at42101pm.png)

1. 单击&#x200B;**传输**&#x200B;选项卡。
1. 在&#x200B;**URI**&#x200B;字段中，输入portlet的刷新URI(URL)。 URI的形式如下：

   ```xml
   https://<wps-host>:<port>/<wps-context>/<cq5-portlet-context>/cqbridge/cqpcache
   ```

   ![screen_shot_2012-02-15at42322下午](assets/screen_shot_2012-02-15at42322pm.png)

1. 单击&#x200B;**Extended**&#x200B;选项卡。

   ![screen_shot_2012-02-15at42515pm](assets/screen_shot_2012-02-15at42515pm.png)

1. 在&#x200B;**HTTP方法**&#x200B;字段中，键入&#x200B;**GET**。
1. 在&#x200B;**HTTP头**&#x200B;字段中，单击&#x200B;**+**&#x200B;以添加新条目并键入&#x200B;**路径：{path}**。
1. 如有必要，单击&#x200B;**Proxy**&#x200B;选项卡，然后为代理输入代理信息。
1. 单击&#x200B;**确定**&#x200B;以保存更改。
1. 要测试连接，请单击&#x200B;**测试连接**&#x200B;链接。 将显示一条日志消息，指示复制测试是否成功。 例如：

   ![screen_shot_2012-02-15at42639pm](assets/screen_shot_2012-02-15at42639pm.png)

#### 手动刷新Portlet缓存{#manually-flushing-the-portlet-cache}

您可以通过访问为复制代理配置的同一URL手动刷新portlet缓存。 有关URL的形式，请参阅[刷新缓存](#flushing-the-cache-via-replication-agent)。 此外，URL需要用URL参数Path=&lt;path>进行扩展，以指示要刷新的内容。

例如：

`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=*` 刷新完整缓存。`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=/content/mypage/xyz` 从缓 `/content/mypage/xyz` 存中刷新。

### 门户安全{#portal-security}

入口是驱动认证机制。 您可以与技术用户、门户用户、组等登录AEM。 Portlet无权访问门户中用户的口令，因此，如果Portlet不知道成功登录用户的所有凭据，则必须使用SSO解决方案。 在这种情况下，AEM portlet将所有必需信息转发给AEM，后者将这些信息转发给基础AEM存储库。 此行为可插拔，并可进行自定义。

### 发布时的身份验证{#authentication-on-publish}

本节介绍portlet在与基础AEM WCM实例通信时可用的身份验证模式。

默认情况下，不向AEM的发布实例发送任何用户信息；内容始终以匿名用户的身份显示。 如果用户特定信息应从AEM提供，或者如果需要用户发布身份验证，则必须启用此功能。

#### 访问Portlet的身份验证配置{#accessing-the-portlet-s-authentication-configuration}

portlet在AEM WCM实例中使用的身份验证配置选项在Web控制台（OSGi配置）中可用。

>[!NOTE]
>
>使用AEM时，有几种方法可以管理OSGi服务（控制台或存储库节点）的配置设置。
>
>有关完整的详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)。

要访问portlet的身份验证配置：

1. 通过以下URL访问Web控制台：

   `https://localhost:8080/cqportlet/cqbridge/system/console`

   例如，在其默认配置中：

   `https://wps-host:10040/wps/PA_CQ5_Portlet/cqbridge/system/console`

1. 登录到Web控制台。 默认凭据为`admin/admin`。
1. 在控制台中，选择&#x200B;**配置**。
1. 在&#x200B;**配置**&#x200B;菜单中，选择要配置的特定服务。 服务由OSGi框架中的portlet提供。

   | 服务名称 | 描述 |
   |---|---|
   | 日门户Director身份验证器 | 配置用于AEM WCM实例的身份验证模式。 根据所选模式，可以指定技术用户或SSO Cookie的名称。 此外，还可以启用AEM WCM发布实例的身份验证。 |
   | 日门户Director文件缓存 | 配置portlet缓存其从AEM WCM实例接收的响应方式的参数。 |
   | 日门户DirectorHTTP客户端服务 | 配置portlet如何通过HTTP连接到基础AEM WCM实例。 例如，可以指定代理服务器。 |
   | 日门户Director区域设置处理程序 | 配置portlet支持的语言环境。 对AEM WCM实例的请求基于用户区域设置；例如，用户语言*德语*将请求`/content/geometrixx/de/`.... |
   | 日门户Director特权经理 | 根据当前登录的用户配置portlet是否应测试“网站”选项卡。 |
   | 日门户Director工具栏渲染器 | 自定义portlet工具栏的呈现。 |

1. 此外，您还可以配置Web控制台和日志记录服务。 例如，您可以通过单击Apache Felix OSGi管理控制台链接来更改Web控制台的管理员凭据。

#### 技术用户模式{#technical-user-mode}

在默认模式下，portlet为AEM WCM作者实例发出的所有请求都将使用同一技术用户进行身份验证，而不管当前门户用户如何。 技术用户模式默认处于启用状态。 在OSGi管理控制台中的相应配置屏幕中启用／禁用此模式：

如果启用了&#x200B;**在发布上进行身份验证**，则指定的技术用户必须存在于AEM WCM作者实例和发布实例中。 请务必为用户授予足够的访问权限，以便进行创作。

#### SSO {#sso}

Portlet支持SSO(即装即用的AEM)。 身份验证器服务可以配置为使用SSO并将格式为&#x200B;**Basic**&#x200B;的当前门户用户作为名为`cqpsso`的cookie传输到AEM。 应将AEM配置为使用路径／的SSO身份验证处理程序。 此处也需要配置Cookie名称。

AEM存储库的`crx-quickstart/repository/repository.xml`需要相应地进行配置：

```xml
<LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
  ...
  <param name="trust_credentials_attribute" value="TrustedInfo"/>
  <param name="anonymous_principal" value="anonymous"/>
</LoginModule>
```

#### SSO身份验证模式{#sso-authentication-mode}

portlet可以使用单点登录(SSO)方案验证AEM WCM的身份。 在此模式下，当前登录到门户的用户以SSO cookie的形式转发到AEM WCM。 如果使用SSO模式，则对AEM portlet具有访问权限的所有门户用户都必须知道底层AEM WCM实例，最常采用AEM WCM连接到LDAP的形式，或事先手动创建用户的方式。 此外，在portlet中启用SSO之前，需要将基础AEM WCM作者实例（如果启用了&#x200B;**在Publish上进行身份验证**，则还需要将发布实例）配置为接受基于SSO的请求。

要配置portlet以使用SSO身份验证模式，请完成以下步骤（在以下各节中有详细说明）:

* 使AEM WCM的存储库接受受信任凭据。
* 在AEM WCM中启用SSO身份验证。
* 在AEM portlet中启用SSO身份验证。

#### 使AEM WCM的存储库接受受信任凭据{#enabling-aem-wcm-s-repository-to-accept-trusted-credentials}

在为AEM WCM启用SSO之前，需要将基础存储库配置为接受AEM WCM提供的受信任凭据。 为此，请配置AEM repository.xml。

1. 在安装AEM WCM的文件系统中，打开以下文件：

   `//crx-quickstart/repository/repository.xml`

1. 在XML文件中，找到&#x200B;**LoginModule**&#x200B;的条目，并将trust_credentials属性添加到其配置中：

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
1. 在“配置”菜单中，选择“SSO身份验证处理程序”。 在此示例中，SSO处理函数根据AEM portlet提供的cookie接受所有路径的SSO请求。 您的配置可能会有所不同。

   | 路径 | / | 为所有请求启用SSO处理程序 |
   |---|---|---|
   | Cookie名称 | cqpsso | portlet在portlet的OSGi控制台中配置的cookie的名称。 |

1. 单击&#x200B;**保存**&#x200B;以启用SSO。 SSO现在是主身份验证方案。

对于AEM WCM收到的每个请求，首先尝试基于SSO的身份验证。 失败时，执行回退到通常的基本身份验证方案。 因此，与AEM WCM的正常连接（无SSO）仍可能存在。

#### 在AEM Portlet {#enabling-sso-authentication-in-a-aem-portlet}中启用SSO身份验证

为了使基础AEM WCM实例接受SSO请求，必须将portlet的身份验证模式从&#x200B;**Technical**&#x200B;切换为&#x200B;**SSO**。

要在AEM portlet中启用SSO身份验证：

1. 通过位于https://&lt;aem-host>:&lt;port>/system/console的URI访问控制台。
1. 在“配置”菜单中，从可用配置的列表中选择Day PortalDirector身份验证器。
1. 在模式中，选择SSO。 保留其他参数的默认值。

   ![chlimage_1-133](assets/chlimage_1-135.png)

1. 单击“保存”以为portlet启用SSO。

   出于测试目的，在AEM WCM中以管理员权限创建同一用户后，使用门户的管理用户访问portlet。

执行此过程后，请求将使用SSO进行身份验证。 HTTP通信中的典型代码片断显示存在以下特定于SSO和Portlet的标头：

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

如果您没有使用AEM content portlet的默认内联编辑功能，但希望portlet的创作和管理部分直接在AEM作者实例中位于门户外部，则应启用PIN身份验证。 您还需要更改管理按钮的配置。

要打开网站管理页面或从portlet编辑页面，AEM内容portlet使用新的pin身份验证。 默认情况下，禁用PIN身份验证，因此，必须在AEM中进行以下配置更改：

1. 通过在repository.xml文件中添加受信任信息，在AEM中启用受信任身份验证：

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
   </LoginModule>
   ```

1. 在OSGi配置控制台(默认位置为https://localhost:4502/system/console/configMgr)中，从下拉菜单中选择&#x200B;**CQ PIN身份验证处理程序**。
1. 编辑&#x200B;**URL根路径**&#x200B;参数，只包含单个值&#x200B;**/**。

### 权限 {#privileges}

portlet的某些功能受权限保护。 当前用户需要具有此权限才能访问此函数。 预定义了以下权限：

* “工具栏”:这是查看／使用Portlet中的工具栏的一般权限。
* &quot;prefs&quot; :如果用户具有此权限，则允许用户查看／更改portlet的首选项。
* &quot;cq-author:edit&quot;:使用此权限，用户可以调用内容的编辑视图。
* &quot;cq-author:预览&quot;:使用此权限，用户可以查看预览。
* &quot;cq-author:siteadmin&quot;:通过此权限，用户可以在AEM中打开siteadmin。

管理权限的最佳方法是使用门户角色并为这些权限分配角色。 这可以通过OSGi配置完成。 “日门户Director权限管理器”可配置为每个权限的一组角色。 如果用户具有其中一个角色，则用户具有相应的权限。

此外，还可以根据每个portlet实例库的访问来定义此角色。 portlet的首选项对话框包含上述每个权限的输入字段。 对于每个权限，可以配置以逗号分隔的portlet角色列表。 如果配置了值，则这将覆盖“Day PortalDirector权限管理器”服务中的全局配置，并且可能需要从此全局设置添加相同的角色，因为角色未合并！ 如果未指定值，则使用全局配置。

### 自定义AEM portlet应用程序{#customizing-the-aem-portlet-application}

提供的AEM portlet应用程序像AEM一样在Web应用程序中开始OSGi容器。 此架构允许您利用OSGi的所有优势：

* 易于更新和扩展
* 无需门户服务器进行任何交互即可提供门户的热更新
* 易于自定义portlet

### 工具栏按钮{#toolbar-buttons}

工具栏及其按钮是可配置的，并且可以进行自定义。 您可以向工具栏添加您自己的按钮，或定义在哪种模式下显示哪些按钮。 每个按钮都是可通过OSGi配置配置的OSGi服务。

OSGi Web控制台列表&#x200B;**Configuration**&#x200B;选项卡上的所有按钮配置。 对于每个按钮，您可以定义显示此按钮的模式。 这允许您通过删除所有模式（例如）来禁用按钮。

默认情况下，AEM内容portlet使用内联编辑功能。 但是，如果您希望切换到AEM作者实例进行编辑，请启用&#x200B;**SiteAdmin Button**&#x200B;和&#x200B;**ContentFinder Button**，但禁用&#x200B;**Edit Button**。 在这种情况下，请确保在AEM中正确配置PIN身份验证。

可以通过portlet的Felix Web控制台安装捆绑包来自定义portlet的工具栏布局，该控制台包含在预定义位置的自定义CSS/HTML。

#### 捆绑结构{#bundle-structure}

以下是一个示例捆绑结构：

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

META-INF文件夹包含OSGi要求的MANIFEST.MF文件，以将其标识为捆绑包。 显示如下：

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

HTML/CSS/图像位于/com/day/cq/portlet/toolbar/layout文件夹内的事实由portlet规定，不能更改。 同样，MANIFEST.MF中的导入包和导出包头也必须被称为/com/day/cq/portlet/toolbar/layout。 Bundle-SymbolicName必须是唯一且完全限定的包名称。

您可以使用手动或手动创建此类jar文件的工具（如本节所示）来构建它。

#### Portlet工具栏视图{#portlet-toolbar-views}

portlet的工具栏基本上有两种视图状态。 每个视图和关联按钮都可以用相应的HTML文件进行自定义。

#### 发布视图{#publish-view}

发布视图只有一个按钮，可将工具栏切换到管理视图。 发布视图由[上一个bundle](/help/sites-deploying/configuring-osgi.md#bundles)中的publish.html文件表示。 在HTML中，您可以使用以下占位符，在呈现时，portlet将替换为相应的内容：

#### 发布视图占位符{#publish-view-placeholders}

| 占位符字符串 | 描述 |
|---|---|
| {buttonManage} | 占位符由&#x200B;**管理**&#x200B;按钮替换，该按钮将portlet状态切换到管理状态。 |

#### 管理视图{#manage-view}

管理视图有四个按钮：“编辑”、“网站”选项卡、“刷新”和“返回”。 管理视图由[上一个包](/help/sites-deploying/configuring-osgi.md#bundles)中的manage.html文件表示。 在HTML中，您可以使用以下占位符，在呈现时，portlet将替换为相应的内容：

#### 管理视图占位符{#manage-view-placeholders}

| 占位符字符串 | 描述 |
|---|---|
| {buttonEdit} | 占位符由&#x200B;**编辑**&#x200B;按钮替换，该按钮在AEM编辑模式下打开一个具有当前页面的新窗口。 |
| {buttonWebsites选项卡} | 占位符，替换为打开AEM WCM的“网站”选项卡的按钮。 |
| {buttonRefresh} | 刷新当前视图。 |
| {buttonBack} | 将portlet切换回发布视图。 |

#### 按钮 {#buttons}

按钮在出现的视图上使用在button.html中定义的相同的通用HTML。

在HTML中，您可以使用以下占位符，在呈现时，portlet将替换为相应的内容：

#### 管理和发布视图按钮{#manage-and-publish-view-buttons}

| 占位符字符串 | 描述 |
|---|---|
| {name} | 按钮的名称，例如，**作者、返回、刷新**等。 |
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

要安装自定义布局，请访问portlet的OSGI Web控制台**Bundles **部分并上传该包。

#### 包 {#packages}

如果您需要上传或创建安装的包，请参阅AEM文档中的包管理器以获取详细说明。

### 链路处理{#link-handling}

所有链接都将重写，以在门户上下文中工作。 默认情况下，使用带有渲染参数的链接。 可以将门户DirectorHTML重写器配置为改用操作链接。

您还可以定义要查询的其他请求参数以查看要显示的内容路径。 这很有用，例如，如果有从外部到特定内容的链接。

此外，门户DirectorHTML重写程序可配置一列表定义为不包括链接重写的常规表达式。 例如，如果您有到外部系统的相对链接，则应将这些链接添加到此排除列表。

### 本地化 {#localization}

AEM内容portlet具有内置的本地化功能，可确保AEM中的内容使用正确的语言。

此操作分两步完成：

1. 门户目录区域设置检测器通过从门户获取区域设置来检测门户用户的区域设置。 此服务必须配置AEM中可用语言的列表。
1. 门户Director区域设置处理程序处理当前请求的本地化。 它采用所请求内容的路径，例如`/content/geometrixx/en/company.html`，并且根据配置，它使用用户的实际区域设置重写&#x200B;**en**。

门户Director区域设置处理程序可以配置用于检查区域设置信息的路径——通常，这包括`/content`下的所有内容以及路径中区域设置信息的位置。 默认情况下，区域设置处理函数遵循在AEM中重新公认组织多语言站点。

如果您的站点没有处理路径中区域设置信息的严格规则，则可以将区域设置处理程序替换为您自己的实现。

### 可选OSGi服务{#optional-osgi-services}

可实现可选的OSGi服务以自定义portlet的各个部分。 每个服务对应一个Java接口。 此接口可以通过portlet中的捆绑实现和部署。

<table>
 <tbody>
  <tr>
   <td>RequestTracker</td>
   <td>每当portlet显示内容时，请求跟踪器都会收到通知。 这允许您跟踪portlet的调用。</td>
  </tr>
  <tr>
   <td>InvocationContextListener</td>
   <td>在对portlet的每个请求的开始和结束时调用的监听器。 监听器可用于更改或添加当前请求的信息。<br /> </td>
  </tr>
  <tr>
   <td>ErrorHandler</td>
   <td>渲染阶段错误的自定义错误处理程序。</td>
  </tr>
  <tr>
   <td>HttpProcessor</td>
   <td>此服务可用于向AEM的每个http调用添加信息。</td>
  </tr>
  <tr>
   <td>PortletAction</td>
   <td>向portlet添加自己的操作——可以通过portlet操作链接调用此操作。</td>
  </tr>
  <tr>
   <td>PortletDecoratorService</td>
   <td>此服务可用于装饰portlet的内容。</td>
  </tr>
  <tr>
   <td>资源提供程序</td>
   <td>添加您自己的资源提供者，以便通过指向客户端的portlet资源链接来传送某些资源。</td>
  </tr>
  <tr>
   <td>TextMapper</td>
   <td>允许您发布处理HTML、CSS和Javascript文件。</td>
  </tr>
  <tr>
   <td>工具栏按钮</td>
   <td>将您自己的按钮添加到工具栏。</td>
  </tr>
  <tr>
   <td>UrlMapper</td>
   <td>添加服务以应用自定义url映射或重写。</td>
  </tr>
  <tr>
   <td>用户信息提供者</td>
   <td>添加您自己的用户信息。 此服务可用于从门户获取信息到portlet。</td>
  </tr>
 </tbody>
</table>

#### 替换默认服务{#replacing-default-services}

以下服务在内容portlet中具有默认实现（带有相应的Java接口）。 要进行自定义，需要将包含新服务实现的捆绑包部署到portlet应用程序中。

实施此类服务时，请确保将服务的&#x200B;**service.ranking**&#x200B;属性设置为正值。 默认实现使用排名** 0**,portlet使用排名最高的服务。

| **名称** | **描述** | **默认行为** |
|---|---|---|
| 身份验证器 | 向AEM提供身份验证信息 | 使用可配置的技术用户进行创作和发布。 或者可以使用SSO。 |
| HTMLRewriter | 重写链接、图像等。 | 重写AEM链接到门户链接，可以通过UrlMapper和TextMapper扩展 |
| HttpClientService | 处理所有http连接 | 标准实施 |
| LocaleHandler | 处理区域设置信息 | 重写指向与区域设置相关的内容的链接。 |
| LocaleDetector | 检测用户的区域设置。 | 使用门户提供的区域设置。 |
| PrivilegeManager | 检查用户权限 | 如果允许用户编辑内容，则检查对作者实例的访问权限 |
| 工具栏渲染器 | 呈现工具栏 | 添加工具栏功能 |

### Portlet事件{#portlet-events}

portlet API(JSR-286)指定portlet事件。 AEM内容portlet具有集成桥，将AEM portlet的portlet事件作为OSGi事件分发——这使portlet事件的处理变得可插拔。

如果要处理特定事件，请在部署描述符中将这些事件声明为接收（或通过门户服务器配置它），并实现声明EventHandler接口的OSGi服务（请参阅OSGi EventAdmin规范）。

每当出现portlet事件时，都会调用处理程序发送特定OSGi事件。 处理程序获取所有上下文信息，并可以相应地更新portlet的状态或发送新事件。 基本上，在句柄方法中，可以使用portlet事件阶段的所有功能。

## 将AEM用作门户{#using-aem-as-a-portal}

使用Portlet组件将portlet窗口添加到AEM页面。 安装到应用程序服务器的共享库使Portlet组件能够检测已部署的Portlet应用程序。

要将AEM用作门户，请执行以下任务:

1. 安装Portlet组件和共享库。
1. 将Portlet组件添加到Sidekick。
1. 配置和部署Web应用程序，该应用程序包含要显示在门户组件中的portlet。
1. 将Portlet组件添加到页面并选择要显示的Portlet。

>[!NOTE]
>
>仅当AEM部署为Web应用程序时，才可使用portlet组件。 ([请参阅安装AEM和应用程序服务器](/help/sites-deploying/application-server-install.md)。)

### 安装portlet组件{#installing-the-portlet-component}

AEM Quickstart JAR文件包含portlet组件文件。 要获取文件(cq-portlet-components.zip)，您可以执行快速启动或提取内容。

1. 执行或解压Quickstart JAR文件的内容，并相应地找到cq-portlet-components.zip文件：

   * 执行快速启动：crx-quickstart/opt/portal
   * 提取快速入门内容：静态／选择／门户

1. 打开部署到应用程序服务器的CQ5作者实例的包管理器。 (https://*appserverhost*:*port*/cq5author/crx/packmgr)

1. 使用包管理器来[上传并安装](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) cq-portlet-components.zip包。

   该包将cq-portlet-director-sharedlibs-x.x.x.jar安装在存储库的/libs/portal/director文件夹中。

1. 将cq-portlet-director-sharedlibs-x.x.x.jar复制到硬盘。 使用任何方式获取文件，例如FileVault或WebDAV客户端。
1. 将cq-portlet-director-sharedlibs.x.x.x.jar文件移到应用程序服务器的共享库文件夹，以便类可用于部署的portlet应用程序。

### 将Portlet组件添加到Sidekick {#adding-the-portlet-component-to-sidekick}

将portlet组件添加到段落系统，以便作者可以使用它。

1. 在Sidekick中，单击标尺图标以进入设计模式。
1. 在第一个段落上方的`Design of par`标题旁，单击&#x200B;**编辑**。

1. 在&#x200B;**常规**&#x200B;组件类别中，选中Portlet组件旁边的复选框，然后单击确定。

![chlimage_1-25](assets/chlimage_1-25.jpeg)

### 配置和部署Portlet应用程序{#configuring-and-deploying-your-portlet-applications}

将Portlet部署到应用程序服务器Web容器，以便它们可用于Portal组件。 在部署portlet应用程序之前，您需要配置应用程序，以便它加载AEM portal容器servlet。 此配置使Portlet组件能够访问Portlet。

1. 提取portlet应用程序WAR文件的内容。

   **提示：** jar xf nameofapp **.war命令提取文件。

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

   **提示：** 该 `jar cvf nameofapp.war *` 命令将当前目录的内容添加到app.war文件的名称中。

1. 将portlet应用程序部署到应用程序服务器。 有关信息，请参阅应用程序服务器的相关文档。

### 将portlet添加到AEM页面{#adding-portlets-to-your-aem-page}

使用门户组件向网页添加portlet窗口。 使用组件属性指定要显示的portlet。

1. 在网页上，将&#x200B;**Portlet**&#x200B;组件从Sidekick中的“常规”组拖动到该页面。

   >[!NOTE]
   >
   >将组件拖到页面后，请重新加载页面以确保其正常工作。

1. 多次-单击组件以打开Portlet属性。
1. 在&#x200B;**Portlet实体**&#x200B;下拉菜单中，从列表中选择portlet。
1. 根据您是否要查看portlet的标题栏，选择或清除“隐藏标题栏”复选框。
1. 在&#x200B;**Portlet窗口**&#x200B;字段中，根据需要输入唯一的Portlet窗口ID。

   >[!NOTE]
   >
   >如果您计划在同一页面上多次使用同一portlet，请为每个portlet提供一个不同的窗口ID。

1. 单击&#x200B;**确定**。portlet显示在AEM页面上。

   ![chlimage_1-136](assets/chlimage_1-136.png)

## 在Portlet {#installing-configuring-and-using-aem-in-a-portlet}中安装、配置和使用AEM

要访问AEM WCM提供的内容，门户服务器需要与AEM门户DirectorPortlet一起安装。 要执行此操作，请使用本节中提供的步骤，安装、配置Portlet并将其添加到门户页面。

默认情况下，portlet连接到localhost:4503处的发布实例和localhost:4502处的作者实例。 这些值可以在部署portlet时进行更改。 门户控制器在/libs/portal/directory下作为存储库中的内容可用。 您需要先下载应用程序war文件，然后再使用它。

### 下载war文件{#downloading-the-war-file}

1. 使用Webdav或CRXDE Lite，导航到/libs/portal/director。

1. 下载&#x200B;*cq-portlet-webapp.war*。

>[!NOTE]
>
>这些过程以Websphere门户为例，尽管它们尽可能通用；请注意，其他Web门户的程序会有所不同。 尽管所有Web门户的步骤基本相同，但您需要为特定Web门户重新设定这些步骤的用途。

#### 安装portlet {#installing-the-portlet}

安装Portlet:

1. 以管理员权限登录到门户。
1. 导航到Web门户的Portlet Management部分。
1. 单击“安装”并浏览至您下载的AEM portlet应用程序(cq-portlet-webapp.war)，然后输入有关portlet的其他重要信息。

   对于其他基本portlet信息，您可以接受默认值或更改值。 如果您接受默认值，则portlet可在https://&lt;wps-host>:&lt;port>/wps/PA_CQ5_Portlet中找到。 portlet提供的OSGi管理控制台位于https://&lt;wps-host>:&lt;port>/wps/ PA_CQ5_Portlet/cqbridge/system/console（默认用户名／密码为admin/admin）。

1. 通过选中该选项或复选框，确保portlet应用程序自动开始，并保存您所做的更改。 您会看到一条消息，表明您的安装成功。

#### 配置Portlet {#configuring-the-portlet}

安装portlet后，您需要对其进行配置，以便它知道基础AEM实例（作者和发布）的URL。 您还可以配置其他选项。

要配置Portlet，请执行以下操作：

1. 在应用程序服务器的门户管理窗口中，导航到portlet管理，其中列出了所有portlet，然后选择AEM PortalDirectorportlet。
1. 根据需要配置portlet。 例如，您可能需要更改创作和发布实例的URL以及开始路径的URL。 [Portlet首选项](/help/sites-administering/aem-as-portal.md#portlet-preferences)中介绍了默认配置。

   >[!NOTE]
   >
   >如果portlet配置为连接到AEM作者并发布在不同于**/**的上下文路径上运行的实例，您需要在这些AEM实例的Html库管理器配置中启用强制&#x200B;**CQUrlInfo**（例如，通过Felix Webconsole）或编辑将无法工作，并且不显示首选项对话框。

1. 在应用程序服务器中保存配置更改。

1. 导航到portlet的OSGI管理控制台。 默认位置为`https://<wps-host>:<port>/wps/PA_CQ5_Portlet/cqbridge/system/console/configMgr`。 默认用户名／密码为&#x200B;**admin/admin**。

1. 选择&#x200B;**Day PortalDirectorCQ服务器配置**&#x200B;配置并编辑以下值：

   * **作者基本URL**:AEM作者实例的基本URL。
   * **发布基本URL**:AEM发布实例的基本URL。
   * **作者用作发布**:作者实例是否用作发布实例（用于开发）?

   ![chlimage_1-137](assets/chlimage_1-137.png)

1. 单击&#x200B;**保存**。您现在可以将portlet添加到门户页面并使用门户。

### 内容URL {#content-urls}

当从AEM请求内容时，portlet将使用当前显示模式（发布或作者）和当前路径来组合完整的URL。 对于默认值，第一个url为`https://localhost:4503/content/geometrixx/en.portlet.html`。 `htmlSelector`的值会自动添加到扩展前的URL中。

如果portlet切换到帮助模式并选择`appendHelpViewModeAsSelector`，则还会附加`help`选择器，例如`https://localhost:4503/content/geometrixx/en.portlet.html.help`。 如果portlet窗口最大化，并且选择`appendMaxWindowStateAsSelector`，则选择器也会附加，例如`https://localhost:4503/content/geometrixx/en.portlet.max.help`。

选择器可以在AEM中进行评估，不同的选择器可以使用不同的模板。

### 在AEM {#using-a-content-url-map-in-aem}中使用内容Url映射

通常，开始路径直接指向AEM中的内容。 但是，如果要在AEM而不是portlet首选项中保持开始路径，可以将开始路径指向AEM中的内容映射，如`/var/portlets`。 在这种情况下，在AEM中运行的脚本可以使用portlet中提交的信息来确定哪个url是开始URL。 它应发出指向正确URL的重定向。

#### 将Portlet添加到门户页面{#adding-the-portlet-to-the-portal-page}

要将portlet添加到门户页面，请执行以下操作：

1. 请确保您位于应用程序服务器的管理窗口中，并导航到管理页面的位置。 （例如，在WebSphere 6.1中，单击&#x200B;**管理页面**）。
1. 选择portlet的名称，然后选择现有页面或创建新页面。
1. 编辑页面布局。
1. 选择portlet并将其添加到容器。
1. 保存更改。

#### 使用Portlet {#using-the-portlet}

要访问您添加到portlet的页面：

1. 在portlet的个性化菜单中，将portlet配置为在门户中配置。
1. 打开配置(Portlet显示在Portlet配置中配置的发布开始URL)并根据需要进行编辑，然后保存它们。

