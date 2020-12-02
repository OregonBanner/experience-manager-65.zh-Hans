---
title: 内容同步的移动设备
seo-title: 内容同步的移动设备
description: 可查看本页以了解有关内容同步的信息。 在AEM中创作的页面可用作应用程序内容，即使设备处于脱机状态也是如此。 此外，由于AEM页面基于Web标准，因此它们可以跨平台工作，使您能够将它们嵌入到任何本机包装器中。 此战略可减少开发工作，并使您能轻松更新应用程序内容。
seo-description: 可查看本页以了解有关内容同步的信息。 在AEM中创作的页面可用作应用程序内容，即使设备处于脱机状态也是如此。 此外，由于AEM页面基于Web标准，因此它们可以跨平台工作，使您能够将它们嵌入到任何本机包装器中。 此战略可减少开发工作，并使您能轻松更新应用程序内容。
uuid: 11f74cc5-99a5-4186-9b60-b19351305432
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 8fb70ca4-86fc-477d-9773-35b84d5e85a8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '3057'
ht-degree: 0%

---


# 具有内容同步的移动设备{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

使用内容同步来打包内容，以将其用于本机移动应用程序。 在AEM中创作的页面可用作应用程序内容，即使设备处于脱机状态也是如此。 此外，由于AEM页面基于Web标准，因此它们可以跨平台工作，使您能够将它们嵌入到任何本机包装器中。 此战略可减少开发工作，并使您能轻松更新应用程序内容。

内容同步框架创建包含Web内容的存档文件。 内容可以是简单页面、图像和PDF文件或整个Web 应用程序中的任何内容。 内容同步API允许从移动应用程序访问归档文件或构建进程，以便检索内容并将其包含在应用程序中。

以下步骤序列说明了内容同步的典型用例：

1. AEM开发人员创建指定要包含的内容的内容同步配置。
1. 内容同步框架会收集和缓存内容。
1. 在移动设备上，启动移动应用程序并请求来自服务器的内容，该内容以ZIP文件形式提供。
1. 客户端将ZIP内容解包到本地文件系统。 ZIP文件中的文件夹结构模拟客户端（例如浏览器）通常从服务器请求的路径。
1. 客户端在嵌入式浏览器中打开内容或以其他方式使用内容。
1. 稍后，客户端从服务器请求更新的内容。 内容同步框架提供增量更新以减少下载大小和时间，这对移动设备很重要，因为带宽或数据量有限。

## 开发内容同步处理程序{#developing-the-content-sync-handlers}

开发内容同步处理程序的一些准则如下：

* 处理函数必须实现&#x200B;*com.day.cq.contentsync.handler.ContentUpdateHandler*（直接或扩展具有该功能的类）
* 处理函数可以扩展&#x200B;*com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 只有更新ContentSync缓存时，处理函数才能报告为true。 假报告为true时，AEM将在更新未实际发生时创建更新。
* 仅当内容实际发生更改时，处理程序才应更新缓存。 如果不需要白色，请勿写入缓存。 这会导致创建不必要的更新。

>[!NOTE]
>
>通过包&#x200B;*com.day.cq.contentsync*&#x200B;上的OSGI记录器配置启用&#x200B;*ContentSync调试日志记录*。 这允许跟踪运行了哪些处理程序以及它们是否更新了缓存并报告了更新缓存。

## 配置内容同步内容{#configuring-the-content-sync-content}

创建内容同步配置以指定交付给客户端的ZIP文件的内容。 您可以创建任意数量的内容同步配置。 每个配置都有一个用于标识的名称。

要创建内容同步配置，请向存储库添加`cq:ContentSyncConfig`节点，并将`sling:resourceType`属性设置为`contentsync/config`。 `cq:ContentSyncConfig`节点可以位于存储库中的任意位置，但AEM发布实例上的用户必须可以访问该节点。 因此，您应在`/content`下添加节点。

要指定内容同步ZIP文件的内容，请向cq:ContentSyncConfig节点添加子节点。 每个子节点的以下属性标识要包含的内容项目以及添加该内容项目时如何处理它：

* `path`:内容的位置。
* `type`:用于处理内容的配置类型的名称。有几种类型可用，有关说明，请参见&#x200B;*配置类型*。

有关详细信息，请参阅&#x200B;*内容同步配置示例*。

创建内容同步配置后，该配置会显示在内容同步控制台中。

>[!NOTE]
>
>内容同步框架不会检查内容同步包中是否包含资产和设计相关文件的依赖关系。 确保在ZIP文件中包含所有必需的文件。

### 配置对内容同步下载的访问{#configuring-access-to-content-sync-downloads}

指定可从内容同步下载的用户或用户组。 您可以配置可从所有内容同步缓存下载的默认用户或组，还可以覆盖默认用户或组，并配置对特定内容同步配置的访问权限。

安装AEM后，默认情况下，管理员组的成员可以从内容同步进行下载。

#### 设置内容同步下载的默认访问权限{#setting-the-default-access-for-content-sync-downloads}

CQ内容同步管理器服务控制对内容同步的访问。 配置此服务以指定默认情况下可从内容同步下载的用户或用户组。

如果[使用Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)配置服务，请键入用户或组的名称作为“回退缓存可授权”属性的值。

如果您正在存储库](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)中进行[配置，请使用以下有关服务的信息：

* PID:com.day.cq.contensync.impl.ContentSyncManagerImpl
* 属性名称：contentsync.fallback.authorizable

#### 覆盖内容同步缓存的下载访问{#overriding-download-access-for-a-content-sync-cache}

要为特定内容同步配置配置下载访问权限，请向`cq:ContentSyncConfig`节点添加以下属性：

* 名称：授权
* 类型：字符串
* 值：可下载的用户或用户组的名称。

例如，您的应用程序允许用户直接从内容同步安装更新。 要使所有用户下载更新，请将可授权属性的值设置为`everyone`。

如果`cq:ContentSyncConfig`节点没有可授权属性，则为Day CQ内容同步管理器服务的“备用缓存可授权”属性配置的默认用户或组将决定哪些用户可以下载。

### 配置用户以更新内容同步缓存{#configuring-the-user-for-updating-a-content-sync-cache}

当用户执行内容同步缓存的更新时，特定用户帐户将代表用户执行该操作。 默认情况下，匿名用户会更新所有内容同步缓存。

您可以覆盖默认用户并指定更新特定内容同步缓存的用户或用户组。

要覆盖默认用户，请通过向cq:ContentSyncConfig节点添加以下属性，指定为特定内容同步配置执行更新的用户或用户组：

* 名称: `updateuser`
* 类型: `String`
* 值：可执行更新的用户或组的名称。

如果`cq:ContentSyncConfig`节点没有`updateuser`属性，则默认的`anonymous`用户将更新缓存。

### 配置类型{#configuration-types}

处理过程包括呈现简单JSON到完全呈现页面（包括其引用的资产）。 本节列表了可用的配置类型及其特定参数：

**复制** 只需复制文件和文件夹。

* **path**  —— 如果路径指向单个文件，则只复制该文件。如果它指向文件夹（包括页面节点），则将复制下面的所有文件和文件夹。

**内** 容使用标准Sling请 [求处理呈现内容](/help/sites-developing/the-basics.md#sling-request-processing)。

* **path**  —— 应输出的资源的路径。
* **extension**  —— 请求中应使用的扩展。常见示例有&#x200B;*html*&#x200B;和&#x200B;*json*，但可能有任何其他扩展。

* **选择** 器——可选选择器，以点分隔。常见示例包括：用于呈现移动版本的页面的&#x200B;*touch*&#x200B;或用于JSON输出的&#x200B;*infinity*。

**clientlib** 打包Javascript或CSS客户端库。

* **path**  —— 客户端库的根路径。
* **extension**  —— 客户端库的类型。此时应将其设置为&#x200B;*js*&#x200B;或&#x200B;*css*。

**资产**

收集资产的原始演绎版。

* **path**  - /content/dam下的资产文件夹的路径。

**图** 像收集图像。

* **path**  —— 图像资源的路径。

图像类型用于在zip文件中包含We Retail徽标。

**页面** 渲染AEM页面并收集引用的资产。

* **path**  —— 页面的路径。
* **extension**  —— 请求中应使用的扩展。对于页面，这几乎始终为&#x200B;*html*，但其他页面仍有可能。

* **选择** 器——可选选择器，以点分隔。常见示例包括用于呈现移动版本页面的&#x200B;*touch*。

* **deep**  —— 可选布尔属性，用于确定是否也应包括子页面。默认值为&#x200B;*true。*

* **includeImages**  —— 可选布尔属性，用于确定是否应包括图像。默认值为&#x200B;*true*。

   默认情况下，仅考虑包含资源类型为foundation/components/image的图像组件。 您可以通过在Web控制台中配置&#x200B;**Day CQ WCM页面更新处理程序**&#x200B;来添加更多资源类型。

**重** 写重写节点定义如何在导出的页面中重写链接。重写的链接可以指向包含在zip文件中的文件，也可以指向服务器上的资源。

`rewrite`节点必须位于`page`节点下。

`rewrite`节点可以具有以下一个或多个属性：

* `clientlibs`:重写clientlibs路径。

* `images`:重写图像路径。
* `links`:重写链接路径。

每个属性都可以具有以下值之一：

* `REWRITE_RELATIVE`:在文件系统上用。html页文件的相对位置重写路径。

* `REWRITE_EXTERNAL`:使用AEM Externalizer服务，通过指向服务器上的资源重写 [路径](/help/sites-developing/externalizer.md)。

名为&#x200B;**PathRewriterTransformerFactory**&#x200B;的AEM服务允许您配置要重写的特定html属性。 该服务可以在Web控制台中进行配置，并且`rewrite`节点的每个属性都有配置：`clientlibs`、`images`和`links`。

此功能在AEM 5.5中添加。

### 内容同步配置示例{#example-content-sync-configuration}

以下列表显示了内容同步的配置示例。

```xml
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

**等等。designs.default等。** mobile配置的前两个条目应该相当明显。由于我们将包含许多移动页面，因此需要/etc/designs下的相关设计文件。 由于不需要额外处理，复制就足够了。

**事件.** plist此条目有点特殊。如导言中所述，应用程序应提供具有事件位置标记的地图视图。 我们将以PLIST格式作为单独的文件提供必要的位置信息。 为了使其正常工作，在索引页上使用的事件列表组件有一个名为plist.jsp的脚本。 当使用。plist扩展请求组件的资源时，将执行此脚本。 像往常一样，组件路径在path属性中给定，并且类型设置为内容，因为我们希望利用[Sling请求处理](/help/sites-developing/the-basics.md#sling-request-processing)。

**事件.touch.html** 下一步是应用程序中将显示的实际页面。路径属性设置为事件的根页面。 该页面下的所有事件页也将包含在内，因为deep属性默认为true。 我们将页面用作配置类型，以便包含可能从页面上的图像或下载组件引用的任何图像或其他文件。 此外，设置触摸选择器还为我们提供了移动版本的页面。 功能包中的配置包含更多此类条目，但为了简单起见，这些条目被遗漏了。

**标** 志迄今为止尚未提到标志配置类型，它不是任何内置类型。但是，内容同步框架可在某种程度上扩展，而这是其示例，下一节将介绍该示例。

**清** 单通常希望在zip文件中包含某种元数据，例如内容的开始页。但是，硬编码此类信息会阻止您稍后轻松更改它。 内容同步框架通过在配置中查找清单节点支持此用例，清单节点只由名称标识，不需要配置类型。 在该特定节点上定义的每个属性都会添加到一个文件中，该文件也称为清单，并驻留在zip文件的根中。

在示例中，事件列表页面应为初始页面。 此信息在&#x200B;**indexPage**&#x200B;属性中提供，因此可以随时轻松更改。 第二个属性定义&#x200B;*事件.plist*&#x200B;文件的路径。 正如我们稍后将看到的，客户端应用程序现在可以读取清单并根据清单进行操作。

配置一经设置，内容便可通过浏览器或任何其他HTTP客户端下载，或者如果您正在为iOS进行开发，则可以使用专用的WAppKitSync客户端库。 下载位置由配置的路径和&#x200B;*.zip*&#x200B;扩展组成，例如，当使用本地AEM实例时：*http://localhost:4502/content/weretail_go.zip*

### 内容同步控制台{#the-content-sync-console}

内容同步控制台列表存储库中的所有内容同步配置（`cq:ContentSyncConfig`类型的所有节点），并且对于每个配置，您都可以执行以下操作：

* 更新缓存。
* 清除缓存。
* 下载完整的zip文件。
* 下载现在与特定日期和时间之间的差异zip。

它可用于开发和故障排除。

控制台可从以下位置访问：

`http://localhost:4502/libs/cq/contentsync/content/console.html`

如下所示：

![chlimage_1-50](assets/chlimage_1-50.png)

### 扩展内容同步框架{#extending-the-content-sync-framework}

虽然配置选项的数量已经相当多，但可能不涵盖特定用例的所有要求。 本节介绍内容同步框架的扩展点以及如何创建自定义配置类型。

对于每个配置类型，都有一个&#x200B;*内容更新处理程序*，它是为该特定类型注册的OSGi组件工厂。 这些处理函数收集内容、处理它并将它添加到由内容同步框架维护的缓存中。 实现以下接口或抽象基类：

* `com.day.cq.contentsync.handler.ContentUpdateHandler` -所有更新处理程序都需要实现的接口
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` -一个抽象类，它使用Sling简化资源呈现

将您的类注册为OSGi组件工厂，并将它部署到OSGi容器中并打包。 使用[Maven SCR插件](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html)可以使用JavaDoc标记或注释完成此操作。 以下示例显示JavaDoc版本：

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

请注意，*factory*&#x200B;定义包含通用接口和以斜杠分隔的自定义类型。 此策略使内容同步框架能够查找和创建自定义类的实例，因为它可以识别配置条目中的自定义类型。 下一节给出了自定义更新处理程序的具体示例。

>[!CAUTION]
>
>在AbstractSlingResourceUpdateHandler基类的基础上构建时，必须添加&#x200B;*inherit*&#x200B;定义。 否则，OSGi容器将不设置在基类中声明的必需引用。

### 实现自定义更新处理程序{#implementing-a-custom-update-handler}

当然，每个We.Retail Mobile页面的左上角都包含一个要包含在zip文件中的徽标。 但是，对于缓存优化，AEM不引用图像文件在存储库中的实际位置，这会阻止我们简单地使用&#x200B;**copy**&#x200B;配置类型。 我们需要做的是提供我们自己的&#x200B;**徽标**&#x200B;配置类型，使映像在AEM请求的位置可用。 以下代码列表显示了徽标更新处理程序的完整实现：

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

* 一个`ConfigEntry`实例，它提供对配置项及其属性的访问，该配置项被调用。
* `lastUpdated`时间戳，指示内容同步上次更新其缓存的时间。 处理程序不应更新在该时间戳后未修改的内容。
* 一个`configCacheRoot`参数，它指定缓存的根路径。 所有更新的文件必须存储在此路径下才能添加到zip文件。
* 应用于所有缓存相关存储库操作的管理会话。
* 一种用户会话，可用于在特定用户的上下文中更新内容，从而提供一种个性化内容。

要实现自定义处理函数，请首先根据配置条目中提供的资源创建Image类的实例。 这基本上与我们页面上的实际徽标组件操作过程相同。 它确保图像的目标路径与从页面引用的路径相同。

接下来，检查自上次更新以来是否修改了资源。 自定义实现应避免对缓存进行不必要的更新，并在没有更改时返回false。 如果修改了资源，则将图像复制到与缓存根目录相关的预期目标位置。 最后，返回`true`以向框架指示已更新缓存。

## 使用客户端{#using-the-content-on-the-client}上的内容

要在内容同步提供的移动应用程序中使用内容，您需要通过HTTP或HTTPS连接请求内容。 因此，可以提取检索到的内容（打包成ZIP文件）并在本地存储在移动设备上。 请注意，内容不仅指数据，还指逻辑，即完整的Web应用程序；因此，即使没有网络连接，移动用户也能够执行检索到的web应用和相应数据。

内容同步以智能方式交付内容：只传送自上次成功数据同步以来的数据更改，从而减少数据传输所需的时间。 自1970年1月1日起，在首次运行应用程序时请求数据更改，随后只请求自上次成功同步以来更改的数据。 AEM利用iOS的客户端通信框架简化数据通信和传输，以便启用基于iOS的Web应用程序需要最少量的本机代码。

所有传输的数据都可以提取到同一目录结构中，在提取数据时不需要任何其他步骤（例如依赖性检查）。 对于iOS，所有数据都存储在iOS应用程序的文档文件夹内的子文件夹中。

基于iOS的AEM Mobile应用程序的典型执行路径：

* iOS设备上的用户开始应用程序。
* 应用程序尝试连接到AEM后端并请求自上次运行以来的数据更改。
* 服务器检索相关数据并将其压缩到文件中。
* 数据将返回至将其提取到文档文件夹的客户端设备。
* UIWebView组件开始/刷新。

如果无法建立连接，将显示以前下载的数据。

### 其他资源 {#additional-resources}

要了解管理员和作者的角色和职责，请参阅以下资源：

* [为AEM Mobile On-demand Services创作AEM内容](/help/mobile/mobile-apps-ondemand.md)
* [管理内容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)

