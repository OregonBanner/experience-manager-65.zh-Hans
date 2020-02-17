---
title: 内容同步的移动设备
seo-title: 内容同步的移动设备
description: 可查看本页以了解有关使用AEM实现Adobe PhoneGap Enterprise内容同步的信息。
seo-description: 可查看本页以了解有关使用AEM实现Adobe PhoneGap Enterprise内容同步的信息。
uuid: c3a82171-e070-4e32-b1ef-26e65ae23d99
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 923fc031-1a06-4a9d-94da-a2a4e82c54ee
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 内容同步的移动设备{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>本文档是《AEM Mobile [](/help/mobile/getting-started-aem-mobile.md) Guide入门指南》（AEM Mobile参考的推荐起点）的一部分。

使用内容同步打包内容，以将其用于本机移动应用程序。 在AEM中创作的页面可用作应用程序内容，即使设备处于脱机状态也是如此。 此外，由于AEM页面基于Web标准，因此它们可以跨平台工作，使您能将它们嵌入到任何本机包装器中。 此战略可减少开发工作，并使您能轻松更新应用程序内容。

>[!NOTE]
>
>您使用AEM工具创建的PhoneGap应用程序已配置为通过内容同步将AEM页面用作内容。

内容同步框架创建包含Web内容的存档文件。 内容可以是简单页面、图像和PDF文件或整个Web应用程序中的任何内容。 内容同步API允许从移动应用程序或构建进程访问归档文件，以便检索内容并将其包含在应用程序中。

以下步骤序列说明了内容同步的典型用例：

1. AEM开发人员创建一个内容同步配置，用于指定要包含的内容。
1. 内容同步框架可收集和缓存内容。
1. 在移动设备上，启动移动应用程序并从服务器请求内容，该内容以ZIP文件形式传送。
1. 客户端将ZIP内容解包到本地文件系统。 ZIP文件中的文件夹结构模拟客户端（例如浏览器）通常从服务器请求的路径。
1. 客户端在嵌入式浏览器中打开内容或以其他方式使用它。
1. 稍后，客户端从服务器请求更新的内容。 内容同步框架提供增量更新以减少下载大小和时间，这对于移动设备很重要，因为带宽或数据量有限。

>[!NOTE]
>
>要获取有关开发内容同步处理程序的指南的更多信息，请参阅开箱即用的应用程序处理程序，请参 [阅开发内容同步处理程序](/help/mobile/contentsync-app-handlers.md)。

## 配置内容同步内容 {#configuring-the-content-sync-content}

创建内容同步配置以指定交付给客户端的ZIP文件的内容。 您可以创建任意数量的内容同步配置。 每个配置都有一个用于标识的名称。

要创建内容同步配置，请向存储库 `cq:ContentSyncConfig` 添加一个节点，并将属 `sling:resourceType` 性设置为 `contentsync/config`。 该节 `cq:ContentSyncConfig` 点可以位于存储库中的任意位置，但AEM发布实例上的用户必须可以访问该节点。 因此，您应在下面添加节点 `/content`。

要指定内容同步ZIP文件的内容，请将子节点添加到cq:ContentSyncConfig节点。 每个子节点的以下属性标识要包含的内容项以及添加该项时如何处理该项：

* `path`:内容的位置。
* `type`:用于处理内容的配置类型的名称。 有几种类型可用，并在配置类型中加以说明。

请参阅内容同步配置示例。

在创建内容同步配置后，该配置会显示在内容同步控制台中。

>[!NOTE]
>
>内容同步框架不会检查内容同步包中是否包含资产的依赖关系和与设计相关的文件。 确保在ZIP文件中包含所有必需的文件。

### 配置对内容同步下载的访问 {#configuring-access-to-content-sync-downloads}

指定可从内容同步下载的用户或用户组。 您可以配置可从所有内容同步缓存下载的默认用户或用户组，还可以覆盖默认用户或用户组，并配置对特定内容同步配置的访问权限。

安装AEM后，默认情况下，管理员组的成员可以从内容同步进行下载。

### 设置内容同步下载的默认访问权限 {#setting-the-default-access-for-content-sync-downloads}

Day CQ Content Sync manager服务控制对内容同步的访问。 配置此服务以指定默认情况下可从内容同步下载的用户或用户组。

如果您使 [用Web控制台配置服务](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)，请键入用户或组的名称作为“备用缓存可授权”属性的值。

如果要在存 [储库中配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)，请使用以下有关服务的信息：

* PID:com.day.cq.contentsync.impl.ContentSyncManagerImpl
* 属性名称：contentsync.fallback.authorizable

#### 覆盖内容同步缓存的下载访问 {#overriding-download-access-for-a-content-sync-cache}

要为特定内容同步配置下载访问权限，请向节点添加以下属 `cq:ContentSyncConfig` 性：

* 名称：可授权
* 类型：字符串
* 值：可下载的用户或用户组的名称。

例如，您的应用程序允许用户直接从内容同步安装更新。 要使所有用户能够下载更新，请将authorizable属性的值设置为 `everyone`。

如果节 `cq:ContentSyncConfig` 点没有可授权属性，则为Day CQ内容同步管理器服务的“备份缓存可授权”属性配置的默认用户或用户组将决定哪些用户可以下载。

### 配置用户以更新内容同步缓存 {#configuring-the-user-for-updating-a-content-sync-cache}

当用户执行内容同步缓存的更新时，特定用户帐户将代表用户执行该操作。 默认情况下，匿名用户会更新所有内容同步缓存。

您可以覆盖默认用户并指定更新特定内容同步缓存的用户或用户组。

要覆盖默认用户，请通过向cq:ContentSyncConfig节点添加以下属性来指定为特定内容同步配置执行更新的用户或用户组：

* 名称：updateuser
* 类型：字符串
* 值：可执行更新的用户或用户组的名称。

如果cq:ContentSyncConfig节点没有更新用户属性，则默认的匿名用户会更新缓存。

### 配置类型 {#configuration-types}

处理范围从渲染简单的JSON到完全渲染页面（包括其引用的资产）。 本节列出了可用的配置类型及其特定参数：

**复制** -只需复制文件和文件夹。

* **path** —— 如果路径指向单个文件，则仅复制文件。 如果它指向一个文件夹（其中包括页面节点），则将复制下面的所有文件和文件夹。

**内容** ，使用标准Sling请求处理来渲染内容。

* **path** —— 应输出的资源路径。
* **extension** —— 请求中应使用的扩展。 常见示例 *有html* 和 *json*，但任何其他扩展都可能。

* **选择器** -可选选择器，以点分隔。 常见示例 *包括* touch *for rendering mobile versions of a page, or infinity* for JSON output。

**clientlib** 将Javascript或CSS客户端库打包。

* **path** —— 客户端库的根路径。
* **extension** —— 客户端库的类型。 此时应将其设置为 *js**或* css。

* **includeFolders** - type是一组字符串，它允许用户指定要在客户端库中扫描以获取文件（如自定义字体）的其他文件夹。

**资产**

收集资产的原始演绎版。

* **path** - /content/dam下的资产文件夹的路径。
* **演绎版** -类型是字符串的数组，用户可以通过它指定要使用的演绎版而不是默认图像。 以下列表汇总了一些现成的演绎版，但您也可以使用由工作流创建的任何演绎版：

   * *原始*
   * *cq5dam.thumbnail.48.48.png*
   * *cq5dam.thumbnail.319.319.png*
   * *cq5dam.thumbnail.140.100.png*
   * *cq5dam.web.1280.1280.png*

**图像** ：收集图像。

* **path** —— 图像资源的路径。

图像类型用于在zip文件中包含We.Retail徽标。

**pages** Render AEM pages and collect referenced assets.

* **path** —— 页面路径。
* **extension** —— 请求中应使用的扩展。 对于页面，这几乎总是 *html*，但其他内容仍然可能。

* **选择器** -可选选择器，以点分隔。 常见示例 *包括触控* ，用于呈现页面的移动版本。

* **deep** —— 可选的布尔属性，用于确定是否也应包括子页面。 The default value is *true.*

* **includeImages** —— 确定是否应包括图像的可选布尔属性。 The default value is *true*.
默认情况下，仅考虑包含资源类型为foundation/components/image的图像组件。 您可以通过在Web控制台中配置 **Day CQ WCM页面更新处理程序来添加更多资源类型** 。

**rewrite** 重写节点定义如何在导出的页面中重写链接。 重写的链接可以指向包含在zip文件中的文件或指向服务器上的资源。

该 `rewrite` 节点需要位于该节点下 `page` 方。

节 `rewrite` 点可以具有以下一个或多个属性：

* `clientlibs`:重写clientlibs路径。

* `images`:重写图像路径。
* `links`:重写链接路径。

每个属性都可以具有以下值之一：

* `REWRITE_RELATIVE`:将路径重写为文件系统中。html页文件的相对位置。

* `REWRITE_EXTERNAL`:使用AEM [Externalizer服务，通过指向服务器上的资源来重写路径](/help/sites-developing/externalizer.md)。

AEM服务名 **为PathRewriterTransformerFactory** ，允许您配置要重写的特定html属性。 该服务可以在Web控制台中配置，并且该节点的每个属性都有一个 `rewrite` 配置： `clientlibs`和 `images``links`。

此功能已在AEM 5.5中添加。

### 内容同步配置示例 {#example-content-sync-configuration}

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

**等等。设计、默认等。移动** ，配置的前两个条目应该比较明显。 由于我们将包含许多移动页面，因此需要/etc/designs下的相关设计文件。 由于不需要额外处理，复制就足够了。

**events.plist** 此条目有点特殊。 如导言中所述，应用程序应提供具有事件位置标记的地图视图。 我们将以PLIST格式作为单独的文件提供必要的位置信息。 为了使其正常工作，索引页上使用的事件列表组件有一个名为plist.jsp的脚本。 当使用。plist扩展名请求组件的资源时，将执行此脚本。 与通常一样，组件路径在path属性中给出，并且类型设置为内容，因为我们希望利用Sling请求处理。

**events.touch.html** 接下来是应用程序中将显示的实际页面。 路径属性设置为活动的根页面。 该页面下的所有活动页面也将包含在内，因为deep属性默认为true。 我们使用页面作为配置类型，以便包含任何可能从页面上的图像或下载组件引用的图像或其他文件。 此外，设置触摸选择器还为我们提供了移动版本的页面。 功能包中的配置包含更多此类条目，但为了简单起见，这些条目被遗漏了。

**徽标** “徽标”配置类型迄今未提及，它不是任何内置类型。 但是，内容同步框架可在一定程度上扩展，这是其示例，下一节将介绍该示例。

**manifest** 通常，希望在zip文件中包含某种元数据，例如内容的开始页。 但是，硬编码此类信息会妨碍您稍后轻松更改它。 内容同步框架通过在配置中查找清单节点支持此用例，清单节点只能通过名称进行标识，不需要配置类型。 在该特定节点上定义的每个属性都会添加到一个文件中，该文件也称为清单，并位于zip文件的根中。

在示例中，活动列表页面应为初始页面。 此信息在indexPage属性 **中提供** ，因此可以随时轻松更改。 第二个属性定义 *events.plist文件的路径* 。 正如我们稍后看到的，客户端应用程序现在可以读取清单并根据清单进行操作。

设置配置后，内容即可通过浏览器或任何其他HTTP客户端下载，或者如果您正在为iOS进行开发，则可以使用专用的WAppKitSync客户端库。 下载位置由配置的路径和 *.zip* 扩展组成，例如，使用本地AEM实例时： *https://localhost:4502/content/weretail_go.zip*

### 内容同步控制台 {#the-content-sync-console}

内容同步控制台列出了存储库中的所有内容同步配置(所有类型的节点 `cq:ContentSyncConfig`)，并且对于每个配置，您都可以执行以下操作：

* 更新缓存。
* 清除缓存。
* 下载完整的zip文件。
* 下载一个介于现在和特定日期和时间之间的diff zip。

它可用于开发和疑难解答。

可以通过以下方式访问控制台：

`https://localhost:4502/libs/cq/contentsync/content/console.html`

它如下所示：

![chlimage_1](assets/chlimage_1.png)

### 扩展内容同步框架 {#extending-the-content-sync-framework}

虽然配置选项的数量已经相当广泛，但可能不涵盖特定用例的所有要求。 本节介绍内容同步框架的扩展点以及如何创建自定义配置类型。

对于每个配置类型，都有一个 *内容更新处理程序*，它是为该特定类型注册的OSGi组件工厂。 这些处理函数收集内容、处理它并将它添加到由内容同步框架维护的缓存中。 实现以下接口或抽象基类：

* `com.day.cq.contentsync.handler.ContentUpdateHandler` -所有更新处理程序都需要实现的接口
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` -一个抽象类，它使用Sling简化了资源呈现

将您的类注册为OSGi组件工厂，并将它部署到捆绑包中的OSGi容器中。 这可以使用Maven SCR插 [件使用JavaDoc标记](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html) 或注释来完成。 以下示例显示了JavaDoc版本：

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

请注意，工 *厂定义* ，包含公用接口和以斜杠分隔的自定义类型。 此策略使内容同步框架能够查找和创建自定义类的实例，因为它识别配置条目中的自定义类型。 下一节给出了自定义更新处理程序的具体示例。

>[!CAUTION]
>
>在AbstractSlingResourceUpdateHandler基类的基础上构建时，必须添加 *inherit定义* 。 否则，OSGi容器将不设置在基类中声明的必需引用。

### 实现自定义更新处理程序 {#implementing-a-custom-update-handler}

当然，每个We.Retail mobile页面都在左上角包含一个Logo，我们希望将它包含在zip文件中。 但是，对于缓存优化，AEM不引用图像文件在存储库中的实际位置，这会阻止我们仅使用复制配 **置类型** 。 我们需要做的是提供我们自己的 **Logo** 配置类型，使图像可在AEM请求的位置使用。 以下代码列表显示了徽标更新处理程序的完整实现：

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

该 `LogoUpdateHandler` 类实现接 `ContentUpdateHandler` 口的方 `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` 法，该方法采用许多参数：

* 提 `ConfigEntry` 供对为其调用此处理函数的配置条目及其属性的访问权限的实例。
* 指示 `lastUpdated` 内容同步上次更新其缓存的时间的时间戳。 在该时间戳之后未修改的内容不应由处理程序更新。
* 指定 `configCacheRoot` 缓存的根路径的参数。 所有更新的文件必须存储在此路径下方，才能添加到zip文件中。
* 应用于所有缓存相关存储库操作的管理会话。
* 一种用户会话，可用于在特定用户的上下文中更新内容并因此提供一种个性化内容。

要实现自定义处理函数，请首先根据配置条目中提供的资源创建Image类的实例。 这基本上与我们页面上实际的徽标组件操作相同。 它确保图像的目标路径与从页面引用的路径相同。

接下来，检查自上次更新以来是否修改了资源。 自定义实现应避免对缓存进行不必要的更新，并在没有发生任何变化时返回false。 如果修改了资源，则将图像复制到与缓存根目录相对的预期目标位置。 最后， `true` 返回以向框架指示已更新缓存。

## 使用客户端上的内容 {#using-the-content-on-the-client}

要在内容同步提供的移动应用程序中使用内容，您需要通过HTTP或HTTPS连接请求内容。 因此，可以提取检索到的内容（打包成ZIP文件）并将其存储在移动设备上的本地。 请注意，内容不仅指数据，还指逻辑，即完整的Web应用；从而使得移动用户即使在没有网络连接的情况下也能够执行检索到的网络应用程序和相应的数据。

内容同步以智能方式交付内容：只传送自上次成功数据同步以来的数据更改，从而缩短数据传输所需的时间。 自1970年1月1日起，在首次运行应用程序时请求数据更改，随后只请求自上次成功同步以来更改的数据。 AEM利用iOS的客户端通信框架简化数据通信和传输，因此启用基于iOS的Web应用程序需要最少量的本机代码。

所有传输的数据都可以提取到同一目录结构中，在提取数据时不需要任何其他步骤（例如依赖性检查）。 对于iOS，所有数据都存储在iOS应用程序的“文档”文件夹内的子文件夹中。

基于iOS的AEM mobile应用程序的典型执行路径：

* 用户在iOS设备上启动应用程序。
* 应用程序尝试连接到AEM后端并请求自上次运行以来的数据更改。
* 服务器检索相关数据并将其压缩到文件中。
* 数据将返回到将其提取到文档文件夹中的客户端设备。
* UIWebView组件启动／刷新。

如果无法建立连接，将显示以前下载的数据。

### 抢先一步 {#getting-ahead}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM为Adobe PhoneGap Enterprise进行创作](/help/mobile/phonegap.md)
* [通过AEM管理Adobe phoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)

