---
title: 通过内容同步移动设备
seo-title: Mobile with Content Sync
description: 关注本页，了解Content Sync for Adobe PhoneGap Enterprise with AEM。
seo-description: Follow this page to learn about Content Sync for Adobe PhoneGap Enterprise with AEM.
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
source-wordcount: '2971'
ht-degree: 0%

---

# 通过内容同步移动设备{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

>[!NOTE]
>
>本文档是 [AEM Mobile快速入门](/help/mobile/getting-started-aem-mobile.md) 指南，建议的AEM Mobile参考起点。

使用Content Sync将内容打包，以便在本机移动设备应用程序中使用这些内容。 在AEM中创作的页面可用作应用程序内容，即使设备处于离线状态也是如此。 此外，由于AEM页面基于Web标准，因此它们可跨平台工作，使您能够将其嵌入任何本机包装器中。 此策略可减少开发工作量，并让您能够轻松更新应用程序内容。

>[!NOTE]
>
>您使用AEM工具创建的PhoneGap应用程序已配置为通过Content Sync将AEM页面用作内容。

内容同步框架会创建一个包含Web内容的存档文件。 内容可以是简单页面、图像和PDF文件或整个Web应用程序中的任何内容。 内容同步API提供了从移动应用程序或构建过程访问存档文件的权限，以便可以检索内容并将其包含在应用程序中。

以下步骤序列说明了Content Sync的典型用例：

1. AEM开发人员创建一个内容同步配置，用于指定要包含的内容。
1. 内容同步框架收集和缓存内容。
1. 在移动设备上，启动移动应用程序并从服务器请求内容（以ZIP文件形式交付）。
1. 客户端将ZIP内容解压缩到本地文件系统。 ZIP文件中的文件夹结构模拟客户端（如浏览器）通常从服务器请求的路径。
1. 客户端在嵌入式浏览器中打开内容，或以其他方式使用内容。
1. 稍后，客户端从服务器请求更新内容。 内容同步框架提供增量更新以减少下载大小和时间，由于带宽或数据量有限，这对于移动设备可能非常重要。

>[!NOTE]
>
>要获取有关开发内容同步处理程序的准则的更多信息，请参阅开箱即用的应用程序处理程序，请参阅 [开发内容同步处理程序](/help/mobile/contentsync-app-handlers.md).

## 配置内容同步内容 {#configuring-the-content-sync-content}

创建内容同步配置以指定传送到客户端的ZIP文件的内容。 您可以创建任意数量的内容同步配置。 每个配置都有一个名称用于标识。

要创建内容同步配置，请添加 `cq:ContentSyncConfig` 节点到存储库，使用 `sling:resourceType` 属性设置为 `contentsync/config`. 此 `cq:ContentSyncConfig` 节点可以位于存储库中的任意位置，但是AEM发布实例上的用户必须能够访问该节点。 因此，您应该添加以下节点 `/content`.

要指定内容同步ZIP文件的内容，请将子节点添加到cq：ContentSyncConfig节点。 每个子节点的以下属性标识要包含的内容项，以及在添加该内容项时如何对其进行处理：

* `path`：内容的位置。
* `type`：用于处理内容的配置类型的名称。 提供了几种类型，在配置类型中对此进行了介绍。

请参阅示例内容同步配置。

创建内容同步配置后，该配置将显示在内容同步控制台中。

>[!NOTE]
>
>内容同步框架不检查资产和相关设计文件的依赖项是否包含在内容同步包中。 确保在ZIP文件中包含所有必需的文件。

### 配置对内容同步下载的访问权限 {#configuring-access-to-content-sync-downloads}

指定可从内容同步下载的用户或组。 您可以配置可以从所有内容同步缓存下载的默认用户或组，也可以覆盖默认用户或组并配置特定内容同步配置的访问权限。

安装AEM后，管理员组的成员可以默认从Content Sync下载。

### 设置内容同步下载的默认访问权限 {#setting-the-default-access-for-content-sync-downloads}

Day CQ内容同步管理器服务控制对内容同步的访问。 配置此服务以指定默认情况下可从Content Sync下载的用户或组。

如果您是 [使用Web控制台配置服务](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)，键入用户或组的名称作为后备缓存可授权属性的值。

如果您是 [在存储库中配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)中，使用以下有关服务的信息：

* PID： com.day.cq.contentsync.impl.ContentSyncManagerImpl
* 属性名称： contentsync.fallback.authorizable

#### 覆盖内容同步缓存的下载访问权限 {#overriding-download-access-for-a-content-sync-cache}

要配置特定内容同步配置的下载访问权限，请将以下属性添加到 `cq:ContentSyncConfig` 节点：

* 名称：可授权
* 类型：字符串
* 值：可下载的用户或组的名称。

例如，您的应用程序允许用户直接从Content Sync安装更新。 要允许所有用户下载更新，请将可授权属性的值设置为 `everyone`.

如果 `cq:ContentSyncConfig` 节点没有可授权属性，为Day CQ Content Sync Manager服务的Fallback Cache Authorizable属性配置的默认用户或组决定了谁可以下载。

### 配置用户以更新内容同步缓存 {#configuring-the-user-for-updating-a-content-sync-cache}

当用户对内容同步缓存执行更新时，特定用户帐户代表用户执行该操作。 默认情况下，匿名用户会更新所有Content Sync缓存。

您可以覆盖默认用户，并指定更新特定内容同步缓存的用户或组。

要覆盖默认用户，请指定用户或组，通过将以下属性添加到cq：ContentSyncConfig节点来为特定内容同步配置执行更新：

* 名称： updateuser
* 类型：字符串
* 值：可执行更新的用户或组的名称。

如果cq：ContentSyncConfig节点没有updateuser属性，则默认匿名用户将更新缓存。

### 配置类型 {#configuration-types}

处理范围从呈现简单的JSON到完全呈现页面（包括其引用的资产）。 此部分列出了可用的配置类型及其特定参数：

**复制** 只需复制文件和文件夹。

* **路径**  — 如果路径指向单个文件，则仅复制该文件。 如果它指向一个文件夹（这包含页面节点），则会复制下面的所有文件和文件夹。

**内容** 使用标准Sling请求处理呈现内容。

* **路径**  — 应输出的资源的路径。
* **扩展**  — 应在请求中使用的扩展。 常见示例包括 *html* 和 *json*，但任何其他扩展都是可能的。

* **选择器**  — 可选的选择器，以点分隔。 常见示例包括 *触控* 用于呈现页面的移动版本或 *无限* 用于JSON输出。

**clientlib** 打包Javascript或CSS客户端库。

* **路径**  — 客户端库的根路径。
* **扩展**  — 客户端库的类型。 此参数应设置为 *js* 或 *css* 此刻。

* **includeFolders**  — 类型是一个字符串数组，它允许用户指定要在客户端库中扫描的其他文件夹以获取文件（如自定义字体）。

**资产**

收集资源的原始演绎版。

* **路径** - /content/dam下的资源文件夹的路径。
* **演绎版**  — 类型是一个字符串数组，允许用户指定要使用的演绎版，而不是默认图像。 以下列表汇总了一些现成的演绎版，但您也可以使用工作流创建的任何演绎版：

   * *原始*
   * *cq5dam.thumbnail.48.48.png*
   * *cq5dam.thumbnail.319.319.png*
   * *cq5dam.thumbnail.140.100.png*
   * *cq5dam.web.1280.1280.png*

**图像** 收集图像。

* **路径**  — 图像资源的路径。

图像类型用于在zip文件中包含We.Retail徽标。

**页面** 渲染AEM页面并收集引用的资源。

* **路径**  — 页面的路径。
* **扩展**  — 应在请求中使用的扩展。 对于页面，这种情况几乎总是 *html*，但其他功能仍然可用。

* **选择器**  — 可选的选择器，以点分隔。 常见示例包括 *触控* 用于呈现页面的移动设备版本。

* **深**  — 可选的布尔属性，用于确定是否也应包含子页面。 默认值为 *对。*

* **includeImages**  — 可选的布尔属性，用于确定是否应包含图像。 默认值为 *true*.
默认情况下，只考虑包含资源类型为foundation/components/image的图像组件。 您可以通过配置 **Day CQ WCM页面更新处理程序** 在Web控制台中。

**重写** rewrite节点定义如何在导出的页面中重写链接。 重写的链接可以指向zip文件中包含的文件或服务器上的资源。

此 `rewrite` 节点需要位于 `page` 节点。

此 `rewrite` 节点可以具有以下一个或多个属性：

* `clientlibs`：重写clientlibs路径。

* `images`：重写图像路径。
* `links`：重写链接路径。

每个属性可以具有以下值之一：

* `REWRITE_RELATIVE`：使用相对于文件系统上的页面.html文件的位置重写路径。

* `REWRITE_EXTERNAL`：通过使用AEM指向服务器上的资源来重写路径 [Externalizer服务](/help/sites-developing/externalizer.md).

AEM服务调用了 **PathRewriterTransformerFactory** 用于配置将重写的特定html属性。 该服务可以在Web控制台中配置，并且每个属性的配置都为 `rewrite` 节点： `clientlibs`， `images` 和 `links`.

AEM 5.5中添加了此功能。

### 示例内容同步配置 {#example-content-sync-configuration}

以下列表显示了内容同步的示例配置。

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

**etc.designs.default和etc.designs.mobile** 配置的前两个条目应该非常明显。 由于我们将包含多个移动页面，因此我们需要/etc/designs下的相关设计文件。 由于不需要额外的处理，因此只需复制即可。

**events.plist** 这个条目有点特别。 如简介中所述，应用程序应提供包含事件位置标记的地图视图。 我们将以PLIST格式作为单独的文件提供所需的位置信息。 要使此功能正常工作，在索引页面上使用的事件列表组件具有一个名为plist.jsp的脚本。 当使用.plist扩展名请求组件的资源时，将执行此脚本。 与往常一样，组件路径在path属性中给出，并且类型设置为content，因为我们希望利用Sling请求处理。

**events.touch.html** 接下来是将在应用程序中显示的实际页面。 path属性设置为事件的根页面。 该页面下的所有事件页面也将包含在内，因为deep属性默认为true。 我们将页面用作配置类型，以便包含可能从页面上的图像或下载组件引用的任何图像或其他文件。 此外，设置触摸选择器可为我们提供页面的移动设备版本。 功能包中的配置包含更多此类条目，但为了简单起见，此处省略了这些条目。

**徽标** 到目前为止，尚未提及徽标配置类型，并且它不属于任何内置类型。 但是，内容同步框架在某种程度上是可扩展的，本例将在下一节中介绍。

**清单** 通常需要在zip文件中包含某种类型的元数据，例如内容的起始页。 但是，对这些信息进行硬编码会妨碍您以后轻松更改这些信息。 内容同步框架支持此用例，方法是查找配置中的清单节点，该节点仅由名称标识，不需要配置类型。 在该特定节点上定义的每个属性都会添加到文件中，该文件也称为manifest ，驻留在zip文件的根中。

在本例中，事件列表页面应该是初始页面。 此信息请参见 **indexPage** 属性，因此可以随时轻松更改。 第二个属性定义 *events.plist* 文件。 正如我们稍后将看到的，客户端应用程序现在可以读取清单并根据清单执行操作。

一旦设置好配置，就可以通过浏览器或任何其他HTTP客户端下载内容，或者，如果您正在为iOS开发，则可以使用专用的WAppKitSync客户端库。 下载位置由配置的路径和 *.zip* 扩展(例如，使用本地AEM实例时)： *https://localhost:4502/content/weretail_go.zip*

### 内容同步控制台 {#the-content-sync-console}

内容同步控制台列出存储库中的所有内容同步配置（类型为的所有节点） `cq:ContentSyncConfig`)并为每个配置执行以下操作：

* 更新缓存。
* 清除缓存。
* 下载完整的zip文件。
* 下载现在与特定日期和时间的邮政编码差异。

这对于开发和故障排除非常有用。

可在以下位置访问该控制台：

`https://localhost:4502/libs/cq/contentsync/content/console.html`

它看起来如下所示：

![chlimage_1](assets/chlimage_1.png)

### 扩展内容同步框架 {#extending-the-content-sync-framework}

尽管配置选项的数量已经相当庞大，但可能并不涵盖特定用例的所有要求。 此部分介绍Content Sync框架的扩展点以及如何创建自定义配置类型。

对于每个配置类型，都有一个 *内容更新处理程序*，是为特定类型注册的OSGi组件工厂。 这些处理程序收集和处理内容，并将其添加到由内容同步框架维护的缓存中。 实现以下接口或抽象基类：

* `com.day.cq.contentsync.handler.ContentUpdateHandler`  — 所有更新处理程序都需要实施的接口
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler`  — 一个抽象类，使用Sling简化了资源的渲染

将类注册为OSGi组件工厂，并将其部署在捆绑包中的OSGi容器中。 这可以使用以下代码来完成 [Maven SCR插件](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html) 使用JavaDoc标记或注释。 以下示例显示了JavaDoc版本：

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

请注意 *工厂* definition包含公共接口和用斜杠分隔的自定义类型。 此策略使内容同步框架能够查找并创建自定义类的实例，因为它可以识别配置条目中的自定义类型。 下一部分提供了自定义更新处理程序的具体示例。

>[!CAUTION]
>
>在AbstractSlingResourceUpdateHandler基类上构建时，必须添加 *inherit* 定义。 否则，OSGi容器不会设置基类中声明的必需引用。

### 实施自定义更新处理程序 {#implementing-a-custom-update-handler}

每个We.Retail Mobile页面的左上角都有一个徽标，当然，我们要将该徽标包含在zip文件中。 但是，对于缓存优化，AEM不会引用图像文件在存储库中的实际位置，这会阻止我们仅使用 **复制** 配置类型。 相反，我们需要做的是提供我们自己的 **徽标** 使图像在AEM请求的位置可用的配置类型。 以下代码列表显示了徽标更新处理程序的完整实施：

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

此 `LogoUpdateHandler` 类实现 `ContentUpdateHandler` 界面 `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` 方法，它采用多个参数：

* A `ConfigEntry` 提供对配置条目（该处理程序针对此条目而调用）及其属性的访问权限的实例。
* A `lastUpdated` 时间戳，指示内容同步上次更新其缓存的时间。 处理程序不应更新在该时间戳之后未修改的内容。
* A `configCacheRoot` 参数，指定缓存的根路径。 所有更新的文件都必须存储在此路径下方，才能添加到zip文件中。
* 应用于所有与缓存相关的存储库操作的管理会话。
* 用户会话，可用于更新特定用户上下文中的内容，从而提供个性化内容。

要实施自定义处理程序，请首先基于配置条目中给定的资源创建Image类的实例。 这基本上与我们页面上实际的徽标组件执行的操作相同。 它确保图像的目标路径与页面中引用的路径相同。

接下来，检查自上次更新以来是否修改了资源。 自定义实施应避免对缓存进行不必要的更新，如果未做任何更改，则返回false。 如果修改了资源，请将映像复制到相对于缓存根目录的预期目标位置。 最后， `true` 返回以向框架指示缓存已更新。

## 使用客户端上的内容 {#using-the-content-on-the-client}

要在内容同步提供的移动应用程序中使用内容，您需要通过HTTP或HTTPS连接请求内容。 因此，检索的内容（打包在ZIP文件中）可以被提取并存储在移动设备本地。 请注意，内容不仅涉及数据，还涉及逻辑，即完整的Web应用程序；从而使移动用户即使没有网络连接也能执行检索到的Web应用程序和相应的数据。

内容同步以智能方式交付内容：仅交付自上次成功数据同步后发生的数据更改，从而减少数据传输所需的时间。 在首次运行应用程序时，从1970年1月1日起请求更改数据，而随后只请求自上次成功同步以来更改的数据。 AEM利用iOS的客户端通信框架来简化数据通信和传输，从而只需少量本机代码即可启用基于iOS的Web应用程序。

所有传输的数据都可提取到相同的目录结构中，提取数据时不需要额外的步骤（例如依赖关系检查）。 对于iOS，所有数据都存储在iOS应用程序的Documents文件夹的子文件夹中。

基于iOS的AEM Mobile应用程序的典型执行路径：

* 用户在iOS设备上启动应用程序。
* 应用程序尝试连接到AEM后端，并请求自上次运行以来的数据更改。
* 服务器检索有问题的数据并将这些数据压缩到一个文件中。
* 数据将返回到客户端设备，并提取到文档文件夹中。
* UIWebView组件启动/刷新。

如果无法建立连接，将显示以前下载的数据。

### 快速入门 {#getting-ahead}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM为Adobe PhoneGap Enterprise创作](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)
