---
title: 具有内容同步的移动设备
seo-title: 具有内容同步的移动设备
description: 可查看本页以了解有关将Adobe PhoneGap企业版与AEM进行内容同步的信息。
seo-description: 可查看本页以了解有关将Adobe PhoneGap企业版与AEM进行内容同步的信息。
uuid: c3a82171-e070-4e32-b1ef-26e65ae23d99
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 923fc031-1a06-4a9d-94da-a2a4e82c54ee
docset: aem65
exl-id: 2cadd9c5-4335-48d0-8d1c-941fca717409
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2989'
ht-degree: 0%

---

# 内容同步的移动设备{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

>[!NOTE]
>
>本文档是[AEM Mobile快速入门](/help/mobile/getting-started-aem-mobile.md)指南的一部分，该指南是AEM Mobile参考的推荐起点。

使用内容同步来打包内容，以便将其用在本机移动设备应用程序中。 在AEM中创作的页面可用作应用程序内容，即使设备处于离线状态也是如此。 此外，由于AEM页面基于Web标准，因此它们可以跨平台工作，从而可以将它们嵌入到任何本机包装器中。 此策略可减少开发工作，并让您能够轻松更新应用程序内容。

>[!NOTE]
>
>使用AEM工具创建的PhoneGap应用程序已配置为通过内容同步将AEM页面用作内容。

内容同步框架会创建一个包含Web内容的存档文件。 内容可以是简单页面、图像和PDF文件或整个Web应用程序中的任何内容。 内容同步API允许从移动设备应用程序或构建流程中访问存档文件，以便能够检索内容并将其包含在应用程序中。

以下步骤顺序说明了内容同步的典型用例：

1. AEM开发人员创建内容同步配置，以指定要包含的内容。
1. 内容同步框架会收集和缓存内容。
1. 在移动设备上，启动移动应用程序并从服务器请求内容，该内容以ZIP文件形式交付。
1. 客户端将ZIP内容解包到本地文件系统。 ZIP文件中的文件夹结构模拟客户端（例如浏览器）通常从服务器请求的路径。
1. 客户端在嵌入式浏览器中打开内容，或以其他方式使用内容。
1. 之后，客户端从服务器请求更新内容。 内容同步框架提供了增量更新以减小下载大小和时间，由于带宽或数据卷有限，这对于移动设备可能非常重要。

>[!NOTE]
>
>要获取有关开发内容同步处理程序的准则的更多信息，请参阅开箱即用的应用程序处理程序，请参阅[开发内容同步处理程序](/help/mobile/contentsync-app-handlers.md)。

## 配置内容同步内容{#configuring-the-content-sync-content}

创建内容同步配置，以指定要交付给客户端的ZIP文件的内容。 您可以创建任意数量的内容同步配置。 每个配置都有一个用于标识的名称。

要创建内容同步配置，请向存储库添加`cq:ContentSyncConfig`节点，并将`sling:resourceType`属性设置为`contentsync/config`。 `cq:ContentSyncConfig`节点可以位于存储库中的任意位置，但AEM发布实例上的用户必须可以访问该节点。 因此，您应将节点添加到`/content`下。

要指定内容同步ZIP文件的内容，请将子节点添加到cq:ContentSyncConfig节点。 每个子节点的以下属性标识要包含的内容项目以及添加该内容项目时如何处理该内容项目：

* `path`:内容的位置。
* `type`:用于处理内容的配置类型的名称。有几种类型可用，有关这些类型的说明，请参见配置类型。

请参阅示例内容同步配置。

创建内容同步配置后，该配置会显示在内容同步控制台中。

>[!NOTE]
>
>内容同步框架不会检查内容同步包中是否包含资产和与设计相关的文件的依赖项。 确保在ZIP文件中包含所有必需的文件。

### 配置对内容同步下载的访问{#configuring-access-to-content-sync-downloads}

指定可从内容同步下载的用户或组。 您可以配置默认用户或组，以从所有内容同步缓存中下载该用户或组，并且可以覆盖默认用户或组，并配置对特定内容同步配置的访问权限。

安装AEM后，管理员组的成员默认可以从内容同步下载。

### 设置内容同步下载的默认访问权限{#setting-the-default-access-for-content-sync-downloads}

Day CQ内容同步管理器服务控制对内容同步的访问。 配置此服务以指定默认可从内容同步下载的用户或组。

如果您使用Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)配置服务，请键入用户或组的名称作为回退缓存可授权属性的值。[

如果您正在存储库](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)中配置[，请使用以下有关服务的信息：

* PID:com.day.cq.contentsync.impl.ContentSyncManagerImpl
* 属性名称：contentsync.fallback.authorizable

#### 覆盖内容同步缓存{#overriding-download-access-for-a-content-sync-cache}的下载访问

要为特定的内容同步配置配置下载访问权限，请将以下属性添加到`cq:ContentSyncConfig`节点：

* 名称：可授权
* 类型：字符串
* 值：可下载的用户或组的名称。

例如，您的应用程序允许用户直接从内容同步安装更新。 要使所有用户能够下载更新，请将可授权属性的值设置为`everyone`。

如果`cq:ContentSyncConfig`节点没有可授权属性，则为Day CQ内容同步管理器服务的回退缓存可授权属性配置的默认用户或组将确定可以下载的内容。

### 配置用户以更新内容同步缓存{#configuring-the-user-for-updating-a-content-sync-cache}

当用户对内容同步缓存执行更新时，特定用户帐户代表用户执行该操作。 默认情况下，匿名用户会更新所有内容同步缓存。

您可以覆盖默认用户并指定更新特定内容同步缓存的用户或组。

要覆盖默认用户，请通过向cq:ContentSyncConfig节点添加以下属性来指定执行特定内容同步配置更新的用户或组：

* 名称：updateuser
* 类型：字符串
* 值：可执行更新的用户或组的名称。

如果cq:ContentSyncConfig节点没有updateuser属性，则默认匿名用户会更新缓存。

### 配置类型{#configuration-types}

处理过程可能包括渲染简单的JSON，以及完全渲染页面（包括其引用的资产）。 本节列出了可用的配置类型及其特定参数：

**** 复制只需复制文件和文件夹。

* **路径**  — 如果路径指向单个文件，则仅复制文件。如果指向文件夹（其中包括页面节点），则将复制下面的所有文件和文件夹。

**** contentRender content（使用标准Sling请求处理）。

* **path**  — 应输出的资源路径。
* **扩展**  — 应在请求中使用的扩展。常见示例包括&#x200B;*html*&#x200B;和&#x200B;*json*，但其他任何扩展都可能。

* **选择器**  — 以点分隔的可选选择器。常见示例包括用于呈现页面移动版本的&#x200B;*touch*&#x200B;或用于JSON输出的&#x200B;*infinity*。

**** clientlib包Javascript或CSS客户端库。

* **路径**  — 客户端库根的路径。
* **扩展**  — 客户端库的类型。此时应将此参数设置为&#x200B;*js*&#x200B;或&#x200B;*css*。

* **includeFolders**  - Type是一个字符串数组，它允许用户指定其他文件夹以在客户端库中扫描以获取文件（如自定义字体）。

**资产**

收集资产的原始演绎版。

* **路径**  - /content/dam下资产文件夹的路径。
* **演绎版**  — 类型是一个字符串数组，它允许用户指定要使用的演绎版，而不是默认图像。以下列表汇总了一些现成的演绎版，但您也可以使用工作流创建的任何演绎版：

   * *原始*
   * *cq5dam.thumbnail.48.48.png*
   * *cq5dam.thumbnail.319.319.png*
   * *cq5dam.thumbnail.140.100.png*
   * *cq5dam.web.1280.1280.png*

**** 图像收集图像。

* **路径**  — 图像资源的路径。

图像类型用于在zip文件中包含We.Retail徽标。

**** 页面渲染AEM页面并收集引用的资产。

* **路径**  — 页面路径。
* **扩展**  — 应在请求中使用的扩展。对于页面，这几乎总是&#x200B;*html*，但其他内容仍然可用。

* **选择器**  — 以点分隔的可选选择器。常见示例包括&#x200B;*touch*，用于呈现页面的移动版本。

* **deep**  — 确定是否应包含子页面的可选布尔属性。默认值为&#x200B;*true。*

* **includeImages**  — 确定是否应包含图像的可选布尔属性。默认值为&#x200B;*true*。
默认情况下，仅考虑包含资源类型为foundation/components/image的图像组件。 您可以通过在Web控制台中配置**Day CQ WCM Pages Update Handler**&#x200B;来添加更多资源类型。

**** rewriteRewrite节点定义链接在导出的页面中的重写方式。重写的链接可以指向zip文件中包含的文件，也可以指向服务器上的资源。

`rewrite`节点需要位于`page`节点的下方。

`rewrite`节点可以具有以下一个或多个属性：

* `clientlibs`:重写clientlibs路径。

* `images`:重写图像路径。
* `links`:重写链接路径。

每个属性可以具有以下值之一：

* `REWRITE_RELATIVE`:用相对于文件系统上的page .html文件的位置重写路径。

* `REWRITE_EXTERNAL`:使用AEM Externalizer服务 [，通过指向服务器上的资源来重写](/help/sites-developing/externalizer.md)路径。

名为&#x200B;**PathRewriterTransformerFactory**&#x200B;的AEM服务允许您配置要重写的特定html属性。 该服务可以在Web控制台中进行配置，并且为`rewrite`节点的每个属性配置：`clientlibs`、`images`和`links`。

此功能已在AEM 5.5中添加。

### 内容同步配置示例{#example-content-sync-configuration}

下面列出了内容同步的示例配置。

```java
+ weretail_go [cq:ContentSyncConfig]
  - sling:resourceType = "contentsync/config"

  + etc.designs.default [nt:unstructured]
    - path = "/etc/designs/default"
    - type = "copy"

  + etc.designs.mobile [nt:unstructured]
    - path = "/etc/designs/mobile"
    - type = "copy"

  + events.plist [nt:unstructured]
    - path = "/content/weretail_mobile/en/events/jcr:content/par/events"
    - type = "content"
    - extension = "plist"

  + events.touch.html [nt:unstructured]
    - path = "/content/weretail_mobile/en/events"
    - type = "pages"
    - extension = "html"
    - selector = "touch"

  + logo [nt:unstructured]
    - path = "/etc/designs/mobile/jcr:content/mobilecontentpage/logo"
    - type = "logo"

  + manifest [nt:unstructured]
    - indexPage = "/content/weretail_mobile/en/events.touch.html"
    - metadataPlist = "/content/weretail_mobile/en/events/_jcr_content/par/events.plist"

  + ...
```

**等。default等。** mobile配置的前两个条目应该比较明显。由于我们将包含许多移动页面，因此需要/etc/designs下的相关设计文件。 由于不需要额外处理，因此复制就足够了。

**events.** plist此条目有点特殊。如导言中所述，应用程序应提供包含事件位置标记的地图视图。 我们将以PLIST格式作为单独的文件提供必要的位置信息。 要使其正常工作，在索引页上使用的事件列表组件具有一个名为plist.jsp的脚本。 当使用.plist扩展名请求组件的资源时，将执行此脚本。 与往常一样，组件路径在path属性中给定，类型设置为内容，因为我们希望利用Sling请求处理。

**events.touch.html** Next显示应用程序中将显示的实际页面。路径属性将设置为事件的根页面。 该页面下的所有事件页面也将包含在内，因为深层属性默认为true。 我们将页面用作配置类型，以便包含可能从页面上的图像或下载组件引用的任何图像或其他文件。 此外，设置触屏选择器还为我们提供了页面的移动版本。 功能包中的配置包含更多此类条目，但为方便起见，此处未列出这些条目。

**** 徽标迄今为止尚未提及徽标配置类型，它不是内置类型。但是，内容同步框架在一定程度上是可扩展的，这是一个示例，将在下一节中介绍。

**** manifestZip文件中通常希望包含某种类型的元数据，例如内容的开始页面。但是，对此类信息进行硬编码会阻止您稍后轻松更改该信息。 内容同步框架通过在配置中查找清单节点来支持此用例，清单节点仅通过名称进行标识，不需要配置类型。 在该特定节点上定义的每个属性都会添加到文件中，该文件也称为清单，并位于zip文件的根中。

在示例中，事件列表页面应为初始页面。 此信息在&#x200B;**indexPage**&#x200B;属性中提供，因此可以随时轻松更改。 第二个属性定义&#x200B;*events.plist*&#x200B;文件的路径。 正如我们稍后将看到的，客户端应用程序现在可以读取清单并根据清单执行操作。

设置配置后，可以使用浏览器或任何其他HTTP客户端下载内容，或者，如果您正在为iOS进行开发，则可以使用专用的WAppKitSync客户端库。 下载位置由配置的路径和&#x200B;*.zip*&#x200B;扩展组成，例如，使用本地AEM实例时：*https://localhost:4502/content/weretail_go.zip*

### 内容同步控制台{#the-content-sync-console}

“内容同步”控制台列出了存储库中的所有内容同步配置（所有`cq:ContentSyncConfig`类型的节点），并且对于每个配置，您可以执行以下操作：

* 更新缓存。
* 清除缓存。
* 下载完整的zip文件。
* 下载现在与特定日期和时间之间的差异zip文件。

它可用于开发和疑难解答。

控制台可从以下位置访问：

`https://localhost:4502/libs/cq/contentsync/content/console.html`

如下所示：

![chlimage_1](assets/chlimage_1.png)

### 扩展内容同步框架{#extending-the-content-sync-framework}

尽管配置选项的数量已经非常多，但它可能并不涵盖特定用例的所有要求。 本节介绍内容同步框架的扩展点以及如何创建自定义配置类型。

对于每个配置类型，都有一个&#x200B;*内容更新处理程序*，它是为该特定类型注册的OSGi组件工厂。 这些处理程序会收集内容、处理内容并将其添加到由内容同步框架维护的缓存中。 实现以下接口或抽象基类：

* `com.day.cq.contentsync.handler.ContentUpdateHandler`  — 所有更新处理程序都需要实施的接口
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler`  — 使用Sling简化资源渲染的抽象类

将类注册为OSGi组件工厂，并将其部署在包中的OSGi容器中。 可以使用[Maven SCR插件](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html)使用JavaDoc标记或注释来完成此操作。 以下示例显示JavaDoc版本：

```java
/*
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/customtype"
 */
public class CustomTypeUpdateHandler implements ContentUpdateHandler {
    // add your code here
}

/*
 * @scr.component metatype="no" inherit="true"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/othertype"
 */
public class OtherTypeUpdateHandler extends AbstractSlingResourceUpdateHandler {
    // add your code here
}
```

请注意，*factory*&#x200B;定义包含通用接口和以斜杠分隔的自定义类型。 此策略使内容同步框架能够查找和创建自定义类的实例，因为它识别配置条目中的自定义类型。 下一节提供了自定义更新处理程序的具体示例。

>[!CAUTION]
>
>在基于AbstractSlingResourceUpdateHandler基类构建时，必须添加&#x200B;*inherit*&#x200B;定义。 否则，OSGi容器将不会设置在基类中声明的必需引用。

### 实施自定义更新处理程序{#implementing-a-custom-update-handler}

当然，每个We.Retail Mobile页面的左上角都包含一个要包含在zip文件中的徽标。 但是，为了优化缓存， AEM不会引用图像文件在存储库中的实际位置，这会阻止我们仅使用&#x200B;**copy**&#x200B;配置类型。 我们需要做的是提供我们自己的&#x200B;**logo**&#x200B;配置类型，以便在AEM请求的位置提供图像。 以下代码列表显示了徽标更新处理程序的完整实施：

#### LogoUpdateHandler.java {#logoupdatehandler-java}

```java
package com.day.cq.wcm.apps.weretail.impl;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.day.cq.commons.jcr.JcrUtil;
import com.day.cq.contentsync.config.ConfigEntry;
import com.day.cq.contentsync.handler.ContentUpdateHandler;
import com.day.cq.wcm.foundation.Image;
import com.day.text.Text;

/**
 * The <code>LogoUpdateHandler</code> is used to update the content sync cache
 * with a page logo added using a logo component.
 *
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/logo"
 */
public class LogoUpdateHandler implements ContentUpdateHandler {

    private static final Logger log = LoggerFactory.getLogger(LogoUpdateHandler.class);

    /** @scr.reference policy="static" */
    protected JcrResourceResolverFactory resolverFactory;

    public boolean updateCacheEntry(ConfigEntry configEntry, Long lastUpdated, String configCacheRoot, Session admin, Session session) {
        ResourceResolver resolver = resolverFactory.getResourceResolver(admin);
        Resource resource = resolver.getResource(configEntry.getContentPath());

        Image img = new Image(resource);
        img.setItemName(Image.NN_FILE, "image");
        img.setItemName(Image.PN_REFERENCE, "imageReference");
        img.setSelector("img");

        try {
            if(img.getLastModified() == null || lastUpdated < img.getLastModified().getTime().getTime()) {
                String src = img.getSrc();
                String parentPath = configCacheRoot + Text.getRelativeParent(src, 1);

                Node parent = JcrUtil.createPath(parentPath, "sling:Folder", admin);
                Node image = resolver.getResource(resource.getPath() + "/image").adaptTo(Node.class);
                JcrUtil.copy(image, parent, Text.getName(src));

                admin.save();

                return true;
            }
        } catch (RepositoryException e) {
            log.error("Unexpected error while updating logo: ", e);
        }

        return false;
    }
}
```

`LogoUpdateHandler`类实现`ContentUpdateHandler`接口的`updateCacheEntry(ConfigEntry, Long, String, Session, Session)`方法，该方法采用多个参数：

* `ConfigEntry`实例，用于提供对配置条目及其属性的访问，该配置条目被调用了此处理程序。
* `lastUpdated`时间戳，指示内容同步上次更新其缓存的时间。 处理程序不应更新在该时间戳后未修改的内容。
* 指定缓存根路径的`configCacheRoot`参数。 所有更新的文件都必须存储在此路径下方，才能添加到zip文件中。
* 应用于所有缓存相关存储库操作的管理会话。
* 一种用户会话，可用于在特定用户的上下文中更新内容，从而提供一种个性化内容。

要实施自定义处理程序，请首先根据配置条目中给定的资源创建Image类的实例。 这基本上与我们页面上实际的徽标组件执行的操作过程相同。 它可确保图像的目标路径与从页面引用的路径相同。

接下来，检查自上次更新后是否修改了资源。 自定义实施应避免对缓存进行不必要的更新，并在没有发生任何更改时返回false。 如果资源已修改，请将图像复制到与缓存根目录相关的预期目标位置。 最后，返回`true` ，以向框架指示缓存已更新。

## 在客户端{#using-the-content-on-the-client}上使用内容

要在内容同步提供的移动设备应用程序中使用内容，您需要通过HTTP或HTTPS连接请求内容。 因此，可以提取检索到的内容（打包成ZIP文件）并将其存储在移动设备上的本地。 请注意，内容不仅指数据，还指逻辑，即完整的Web应用程序；从而使得移动用户即使在没有网络连接的情况下也能执行检索到的web应用和相应的数据。

内容同步以智能方式交付内容：只传送自上次成功数据同步以来的数据更改，从而减少数据传输所需的时间。 自1970年1月1日起，在首次运行应用程序时请求数据更改，随后只请求自上次成功同步以来更改的数据。 AEM利用iOS的客户端通信框架来简化数据通信和传输，从而需要最少量的本机代码来启用基于iOS的web应用程序。

所有传输的数据都可以提取到同一目录结构中，因此在提取数据时无需执行其他步骤（如依赖性检查）。 对于iOS，所有数据都存储在iOS应用程序Documents文件夹的子文件夹中。

基于iOS的AEM Mobile应用程序的典型执行路径：

* 用户在iOS设备上启动应用程序。
* 应用程序会尝试连接到AEM后端，并请求自上次运行以来的数据更改。
* 服务器会检索相关数据，并将其压缩到文件中。
* 数据将返回到客户端设备，并将其提取到文档文件夹中。
* UIWebView组件启动/刷新。

如果无法建立连接，则会显示之前下载的数据。

### 提前{#getting-ahead}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM创作Adobe PhoneGap企业版](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)
