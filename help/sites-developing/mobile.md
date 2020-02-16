---
title: 创建适用于移动设备的站点
seo-title: 创建适用于移动设备的站点
description: 创建移动站点与创建标准站点类似，因为它还涉及创建模板和组件
seo-description: 创建移动站点与创建标准站点类似，因为它还涉及创建模板和组件
uuid: 6b19042c-03f1-4e33-970e-475f9fb8c5fb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 0aabfb0a-ef9c-4b06-b698-61cad101c3c1
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# 创建适用于移动设备的站点{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

创建移动站点与创建标准站点类似，因为它还涉及创建模板和组件。 有关创建模板和组件的更多详细信息，请参阅以下页面：模 [板](/help/sites-developing/templates.md)、组 [件](/help/sites-developing/components.md)[和AEM Sites开发入门](/help/sites-developing/getting-started.md)。 主要区别在于在站点中启用AEM内置移动功能。 通过创建依赖移动页面组件的模板来实现。

您还应考虑使用响 [应式设计](/help/sites-developing/responsive.md)，创建一个适合多种屏幕尺寸的站点。

要开始使用，您可以查看AEM中 **提供的We.Retail mobile演示站点** 。

要创建移动站点，请按如下步骤继续：

1. 创建页面组件：

   * 将属性设 `sling:resourceSuperType` 置为这 `wcm/mobile/components/page`样，组件就依赖于移动页面组件。

   * 使用项 `body.jsp` 目特定逻辑创建。

1. 创建页面模板：

   * 将属性 `sling:resourceType` 设置为新创建的页面组件。
   * 设置属 `allowedPaths` 性。

1. 为站点创建设计页面。
1. 在节点下创建站点根页 `/content` 面：

   * 设置属 `cq:allowedTemplates` 性。
   * 设置属 `cq:designPath` 性。

1. 在站点根页面的页面属性中，在“移动”选项卡中设置设 **备组** 。
1. 使用新模板创建站点页面。

移动页面组件( `/libs/wcm/mobile/components/page`):

* 将“移 **动** ”选项卡添加到页面属性对话框。
* 通过它 `head.jsp``drawHead()` ，它从请求中检索当前移动设备组，如果找到设备组，则使用该组的方法包括设备组的关联模拟器初始组件（仅在创作模式下）和设备组的呈现CSS。

>[!NOTE]
>
>移动站点的根页面必须位于节点层次结构的第1级，建议位于/content节点下。

## 使用多站点管理器创建移动站点 {#creating-a-mobile-site-with-the-multi-site-manager}

使用多站点管理器(MSM)从标准站点创建移动Live Copy。 标准站点会自动转换为移动站点：移动站点具有移动站点的所有功能（例如，在模拟器中编辑），并且可以与标准站点同步管理。 请参阅“多站 [点管理器”页面中为不同渠道](/help/sites-administering/msm.md) 创建Live Copy一节。

## 服务器端移动API {#server-side-mobile-api}

包含移动类的Java包包括：

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) —— 定义MobileConstants。
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) —— 定义Device、DeviceGroup和DeviceGroupList。
* [com.day.cq.wcm.mobile.api.device.capability](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) —— 定义DeviceCapability。
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) —— 定义WurflQueryEngine。
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) —— 定义MobileUtil，它提供围绕WCM Mobile的各种实用程序方法。

### 移动组件 {#mobile-components}

We. **Retail移动演示站点使用** ，下面列出了以下移动组件 `/libs/foundation/components`:

<table>
 <tbody>
  <tr>
   <td>名称</td>
   <td>组</td>
   <td>特征</td>
  </tr>
  <tr>
   <td>mobilefooter</td>
   <td>隐藏</td>
   <td>- footer</td>
  </tr>
  <tr>
   <td>mobileimage</td>
   <td>移动设备</td>
   <td>-基于图像基础组件<br /> -如果设备能够<br /> </td>
  </tr>
  <tr>
   <td>mobilelist</td>
   <td>移动设备</td>
   <td>-基于列表基础组件<br /> - listitem_teaser.jsp在设备可以<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>隐藏</td>
   <td>-基于徽标基础组件<br /> -如果设备可以<br /> </td>
  </tr>
  <tr>
   <td>mobilereference</td>
   <td>移动设备</td>
   <td><p>-类似于引用基础组件</p> <p>-将textimage组件映射到mobiletextimage 1，将图像组件映射到mobileimage 1</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>移动设备</td>
   <td>-基于文本时间基础组件<br /> -如果设备可以</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>隐藏</td>
   <td><p>-基于topnav基础组件</p> <p>-仅渲染文本</p> </td>
  </tr>
 </tbody>
</table>

#### 创建移动组件 {#creating-a-mobile-component}

AEM Mobile框架允许开发对发出请求的设备敏感的组件。 以下代码示例演示如何在组件jsp中使用AEM Mobile API，特别是如何：

* 从请求中获取设备：
   `Device device = slingRequest.adaptTo(Device.class);`

* 获取设备组：
   `DeviceGroup deviceGroup = device.getDeviceGroup();`

* 获取设备组功能：
   `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* 获取设备属性（WURFL数据库中的原始功能键／值）:
   `Map<String,String> deviceAttributes = device.getAttributes();`

* 获取设备用户代理：
   `String userAgent = device.getUserAgent();`

* 从当前页面获取设备组列表（作者为站点分配的设备组）:
   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* 检查设备组是否支持图像
   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
或者
   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>在jsp中，可 `slingRequest` 以通过标记 `<sling:defineObjects>` 和标 `currentPage` 记使用 `<cq:defineObjects>` 。

### 模拟器 {#emulators}

基于模拟器的创作为作者提供了创建适用于移动客户端的内容页面的方法。 移动内容创作遵循与就地所见即所得编辑相同的原则。 为了使作者能够感知移动设备上的页面外观，使用设备模拟器编辑移动内容页面。

移动设备模拟器基于通用模拟器框架。 有关详细信息，请参阅“模拟 [器](/help/sites-developing/emulators.md) ”页。

设备模拟器在页面上显示移动设备，而通常的编辑（parsys、组件）发生在设备的屏幕中。 设备模拟器取决于为站点配置的设备组。 可以为设备组分配多个模拟器。 然后，所有模拟器都可在内容页面上使用。 默认情况下，将显示分配给分配给站点的第一个设备组的第一个模拟器。 模拟器可以通过页面顶部的模拟器轮盘或通过Sidekick的编辑按钮进行切换。

**创建模拟器**

要创建模拟器，请参阅通用模拟器页 [面中的“创建自定义移动模拟器](/help/sites-developing/emulators.md) ”部分。

**移动模拟器的主要特性**

* 设备组由以下多个模拟器之一组成：设备组配置页面，例如/etc/mobile/groups/touch，包含节 `emulators` 点下的属 `jcr:content` 性。
注意：虽然同一模拟器可能属于多个设备组，但是这并不合理。

* 通过设备组的配置对话框， `emulators` 该属性会使用所需模拟器的路径进行设置。 For example: `/libs/wcm/mobile/components/emulators/iPhone4`.

* 模拟器组件(例如，( `/libs/wcm/mobile/components/emulators/iPhone4`)扩展基本移动模拟器组件( `/libs/wcm/mobile/components/emulators/base`)。

* 在配置设备组时，可以选择扩展基本移动模拟器的每个组件。 因此，可以轻松创建或扩展自定义模拟器。
* 在编辑模式下的请求时，模拟器实现用于呈现页面。
* 当页面的模板依赖于移动页面组件时，模拟器功能会自动集成到页面中(通过移 `head.jsp` 动页面组件)。

### 设备组 {#device-groups}

移动设备组根据设备功能提供移动设备的分段。 设备组提供了在创作实例上基于模拟器进行创作以及在发布实例上正确呈现内容所需的信息：作者将内容添加到移动页面并发布后，可以在发布实例上请求该页面。 在该视图中，内容页面将使用一个已配置的设备组呈现，而不是模拟器编辑视图。 根据移动设备检测来选择设 [备组](#devicedetection)。 然后，匹配设备组提供必要的样式信息。

设备组定义为下面的内容页 `/etc/mobile/devices` 面，并使用 **移动设备组模板** 。 设备组模板用作内容页面形式的设备组定义的配置模板。 其主要特点是：

* 位置: `/libs/wcm/mobile/templates/devicegroup`
* 允许的路径： `/etc/mobile/groups/*`
* 页面组件： `wcm/mobile/components/devicegroup`

#### 将设备组分配给站点 {#assigning-device-groups-to-your-site}

在创建移动站点时，您需要将设备组分配到站点。 AEM根据设备的HTML和JavaScript渲染功能提供三个设备组：

* **功能** ，适用于Sony Ericsson W800等功能设备，支持基本HTML，但不支持图像和JavaScript。
* **智能电话** ，适用于Blackberry等设备，支持基本HTML和图像，但不支持JavaScript。

* **触屏** ，适用于iPad等设备，并完全支持HTML、图像、JavaScript和设备旋转。

由于模拟器可以与设备组关联(请参阅创建设备组 [](#creating-a-device-group))，因此将设备组分配给站点使作者能够在与设备组关联的模拟器之间进行选择以编辑页面。

要将设备组分配给站点，请执行以下操作：

1. 在您的浏览器中，转到 **Siteadmin** 控制台。
1. 在网站下打开移动站点的根 **页面**。
1. 打开页面属性。
1. Select the **Mobile** tab:

   * 定义设备组。
   * 单击&#x200B;**确定**。

>[!NOTE]
>
>为站点定义设备组后，站点的所有页面都会继承这些设备组。

#### 设备组筛选器 {#device-group-filters}

设备组过滤器定义基于功能的标准以确定设备是否属于该组。 创建设备组时，您可以选择用于评估设备的过滤器。

在AEM从设备接收HTTP请求的运行时，与组关联的每个过滤器都会将设备功能与特定条件进行比较。 当设备具有过滤器所需的所有功能时，设备将被视为属于该组。 功能从WURFL™数据库检索。

设备组可以使用零个或多个过滤器进行功能检测。 此外，过滤器可以与多个设备组一起使用。 AEM提供了一个默认筛选器，用于确定设备是否具有为组选择的功能：

* CSS
* JPG和PNG图像
* JavaScript
* 设备旋转

如果设备组不使用过滤器，则为该组配置的选定功能是设备唯一需要的功能。

有关详细信息，请参阅 [创建设备组过滤器](/help/sites-developing/groupfilters.md)。

#### 创建设备组 {#creating-a-device-group}

当AEM安装的组不符合您的要求时，创建一个设备组。

1. In your browser, go to the **Tools** console.
1. 在“工具”>“移动 **设备** ” **>“设备** 组”下创建新页面 ****。 在创建 **页面对话框中** :

   * 输入 **标题**`Special Phones`。

   * 输 **入名** 称 `special`。

   * 选择移 **动设备组模板**。
   * 单击&#x200B;**创建**。

1. 在CRXDE中，添加一个 **static.css** 文件，其中包含节点下设备组的样 `/etc/mobile/groups/special` 式。

1. 打开“ **特殊电话** ”页。
1. 要配置设备组，请单击“设置”旁 **的** “编辑 **”按钮**。
在“常规 **”选项卡** :

   * **标题**:移动设备组的名称。
   * **说明**:组的说明。
   * **用户代理**:与设备匹配的用户代理字符串。 它是可选的，可以是正则表达式。 示例: `BlackBerryZ10`
   * **功能**:定义组是否可以处理图像、CSS、JavaScript或设备旋转。
   * **最小屏幕宽**&#x200B;度和&#x200B;**高度**
   * **禁用模拟器**:以在内容编辑过程中启用／禁用模拟器。
   在“模拟 **器** ”选项卡上：

   * **模拟器**:选择分配给此设备组的模拟器。
   在“过滤 **器** ”选项卡上：

   * 要添加过滤器，请单击添加项目，然后从下拉列表中选择一个过滤器。
   * 过滤器将按其显示顺序计算。 当设备不满足过滤器的条件时，不会评估列表上的后续过滤器。



1. 单击“确定”。

移动设备组配置对话框如下所示：

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### 每个设备组的自定义CSS {#custom-css-per-device-group}

如前所述，可以将自定义CSS与设备组页面关联，这与设计页面的CSS非常相似。此CSS用于影响创作和发布时页面内容的设备组特定呈现。然后自动包括此CSS:

* 在此设备组使用的每个模拟器的创作实例的页面上。
* 在发布实例的页面中，如果请求的用户代理与此特定设备组中的移动设备匹配。

## 服务器端设备检测 {#server-side-device-detection}

使用过滤器和设备规范库确定执行HTTP请求的设备的功能。

### 开发设备组过滤器 {#develop-device-group-filters}

创建设备组过滤器以定义一组设备功能要求。 根据需要创建任意数量的过滤器，以针对所需的设备功能组。

设计滤镜，以便使用它们的组合来定义功能组。 通常，不同设备组的功能存在重叠。 因此，您可以对多个设备组定义使用某些过滤器。

创建过滤器后，可在组配置中使用它。

有关信息，请转到“创建 [设备组过滤器”](/help/sites-developing/groupfilters.md)。

### 使用WURFL™数据库 {#using-the-wurfl-database}

AEM使用截断版本的 [WURFL](https://wurfl.sourceforge.net/)™数据库根据设备的用户代理查询设备功能，如屏幕分辨率或javascript支持。

WURFL™数据库的XML代码通过解析文 `/var/mobile/devicespecs` 件来表示为下面的节点。向节点的扩展是在第一次启动包 `wurfl.xml``/libs/wcm/mobile/devicespecs/wurfl.xml.``cq-mobile-core` 时进行的。

设备功能存储为节点属性，节点表示设备型号。 您可以使用查询检索设备或用户代理的功能。

随着WURFL™数据库的不断发展，您可能需要自定义或替换它。 要更新移动设备数据库，您有以下选项：

* 如果您拥有允许此用途的许可证，请将文件替换为最新版本。 请参阅安装其他WURFL数据库。
* 使用AEM中提供的版本并配置一个与用户代理字符串匹配并指向现有WURFL™设备的regexp。 请参 [阅添加基于regexp的用户代理匹配](#adding-a-regexp-based-user-agent-matching)。

#### 测试用户代理到WURFL™功能的映射 {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

当设备访问您的移动站点时，AEM会检测设备，根据其功能将其映射到设备组，并发送与设备组对应的页面视图。 匹配的设备组提供必要的样式信息。 可以在“移动用户——代理测试”页上测试映射：

`https://localhost:4502/etc/mobile/useragent-test.html`

#### 安装其他WURFL™数据库 {#installing-a-different-wurfl-database}

随AEM一起安装的截断的WURFL™数据库是2011年8月30日之前的版本。 如果您的WURFL版本在2011年8月30日之后发布，请确保您的使用符合您的许可。

安装WURFL™数据库：

1. 在CRXDE lite中，创建以下文件夹： `/apps/wcm/mobile/devicespecs`
1. 将WURFL™文件复制到该文件夹。
1. 将文件重命名为 `wurfl.xml`。

AEM会自动分析文 `wurfl.xml` 件并更新以下节点 `/var/mobile/devicespecs`。

>[!NOTE]
>
>启用完整的WURFL™数据库后，可能需要几分钟才能进行解析和激活。 您可以查看日志以获取进度信息。

#### 添加基于regexp的用户代理匹配 {#adding-a-regexp-based-user-agent-matching}

在/apps/wcm/mobile/deviceceps/wurfl/regexp下添加一个用户代理作为正则表达式，以指向现有WURFL™设备类型。

1. 在 **CRXDE Lite中**，在/apps/wcm/mobile/deviceceps/regexp下创建一个节点，如apple_ipad_ver1。
1. 将以下属性添加到节点：

   * **regexp**:定义用户代理的正则表达式，例如：.*Mozilla。*iPad.*AppleWebKit。*Safari.*
   * **deviceId**:wurfl.xml中定义的设备ID，例如：apple_ipad_ver1

上述配置使用户代理与提供的正则表达式匹配的设备映射到apple_ipad_ver1 WURFL™设备ID（如果存在）。

## 客户端设备检测 {#client-side-device-detection}

本节介绍如何使用AEM的设备客户端检测来优化页面渲染或为客户端提供替代网站版本。

AEM支持基于的设备客户端检测 `BrowserMap`。 `BrowserMap` 在AEM中作为客户端库提供 `/etc/clientlibs/browsermap`。

`BrowserMap` 为您提供三个战略，您可以使用这些战略向客户提供替代网站，其顺序如下：

1. [替代链接](#providing-alternate-links)
1. [设备组特定URL](#definingdevicegroupspecificurl)
1. [基于选择器的URL](#defining-selector-based-urls)

>[!NOTE]
>
>有关客户端库集成的详细信息，请阅读 [使用客户端HTML库一节](/help/sites-developing/clientlibs.md) 。

### 提供替代链接 {#providing-alternate-links}

OSGi服 `PageVariantsProvider` 务能够为属于同一家族的站点生成替代链接。 为了配置要由服务考虑的站点，必须 `cq:siteVariant` 从站点的根节点 `jcr:content` 向该节点添加节点。

节 `cq:siteVariant` 点需要具有以下属性：

* `cq:childNodesMapTo` -确定子节点将映射到的链接元素的属性；建议以这样的方式组织网站的内容，以便根节点的子节点代表全局网站语言变体的根(例如， `/content/mysite/en`, `/content/mysite/de`在此情况下， `cq:childNodesMapTo` 价值应为 `hreflang`;
* `cq:variantDomain` -指示将 `Externalizer` 用于生成页面变体绝对URL的域；如果未设置此值，则将使用相对链接生成页面变体；
* `cq:variantFamily` -指示此站点属于哪个网站系列；同一网站的多个特定设备表示应属于同一系列；
* `media` -存储链接元素媒体属性的值；建议使用注册的名称 `BrowserMap``DeviceGroups`，以便库可 `BrowserMap` 以自动将客户端转发到网站的正确变体。

#### PageVariantsProvider和Externalizer {#pagevariantsprovider-and-externalizer}

当节点的属 `cq:variantDomain` 性值不为空 `cq:siteVariant` 时，服务将使用此值生成绝对链接 `PageVariantsProvider` ，作为服务的配置域 `Externalizer` 。 确保配置服务以 `Externalizer` 反映您的设置。

>[!NOTE]
>
>When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

### 定义设备组特定URL {#defining-a-device-group-specific-url}

如果不想使用替代链接，则可以为每个链接配置全局URL `DeviceGroup`。 我们建议创建您自己的客户端库，它嵌入客 `browsermap.standard` 户端库，但重新定义设备组。

BrowserMap的设计方式是，通过从自定义客户端库中为对象创建和添加同名的新设备组，可以覆盖设备组定义。 `BrowserMap`

>[!NOTE]
>
>有关详细信息，请阅读自定 [义的BrowserMap](#creatingacustomisedbrowsermap) 部分。

### 定义基于选择器的URL {#defining-selector-based-urls}

如果之前没有使用任何机制来指示替代站点 `BrowserMap`，则将使用名称的选择器将添加到 `DeviceGroups``URL`s中，在这种情况下，您应提供自己的Servlet来处理请求。

例如，将由BrowserMap标 `www.example.com/index.html` 识的设备 `smartphone` 浏览转发到 `www.example.com/index.smartphone.html.`

### 在页面上使用BrowserMap {#using-browsermap-on-your-pages}

要在页面中使用标准BrowserMap客户端库，您必须在页面的部 `/libs/wcm/core/browsermap/browsermap.jsp` 分中使 `cq:include`用标记来包含该文 `head` 件。

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

除了在文 `BrowserMap` 件中添加客户端库之 `JSP` 外，您还必须将设置为的“字符串”属 `cq:deviceIdentificationMode` 性添加到网站 `client-side``jcr:content` 根目录下的节点。

### 覆盖BrowserMap的默认行为 {#overriding-browsermap-s-default-behaviour}

如果要通过覆盖或添 `BrowserMap` 加更多探测器来自定义 `DeviceGroups` ，则应创建您自己的客户端库，在其中嵌入客 `browsermap.standard`户端库。

此外，您必须手动调用代 `BrowserMap.forwardRequest()` 码中的方 `JavaScript` 法。

>[!NOTE]
>
>有关客户端库集成的详细信息，请阅读 [使用客户端HTML库一节](/help/sites-developing/clientlibs.md) 。

在您创建自定义客户端库 `BrowserMap` 后，我们建议采用以下方法：

1. 在应用程 `browsermap.jsp` 序中创建文件

   ```xml
   <%@include file="/libs/foundation/global.jsp" %>
   <%@ taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
   <%@ page import="
       com.day.cq.wcm.api.variants.PageVariant,
       com.day.cq.wcm.api.variants.PageVariantsProvider,
       com.day.cq.wcm.api.devicedetection.DeviceIdentificationMode,
       com.day.cq.wcm.api.WCMMode"
   %>
   <%
       final PageVariantsProvider p = sling.getService(PageVariantsProvider.class);
       if(p == null) {
           throw new IllegalStateException("Missing PageVariantsProvider service");
       }
       for(PageVariant v : p.getVariants(currentPage, slingRequest)) {
           final String curVar = v.getAttributes().get("data-current-variant");
           String media = v.getAttributes().get("media");
           if (media != null) {
               media = media.replaceAll(" ", "");
           }
   %>
       <link
           rel="alternate"
           data-cq-role="site.variant"
           title="<%= xssAPI.encodeForHTMLAttr(v.getTitle()) %>"
           hreflang="<%= xssAPI.encodeForHTMLAttr(v.getAttributes().get("hreflang")) %>"
           media="<%= xssAPI.encodeForHTMLAttr(media) %>"
           href="<%= xssAPI.getValidHref(v.getURL()) %>"
           <% if(curVar != null) { %> data-current-variant="<%= curVar %>"<% } %>
       />
   <%
       }
       Boolean browserMapEnabled = true;
       final DeviceIdentificationMode dim = sling.getService(DeviceIdentificationMode.class);
       String[] selectors  = slingRequest.getRequestPathInfo().getSelectors();
       boolean isPortletRequest = false;
       for (int i = 0; i < selectors.length; i++) {
           if ("portlet".equals(selectors[i])) {
               isPortletRequest = true;
               break;
           }
       }
       if (isPortletRequest) {
           log.debug("Request was made by a portlet container - BrowserMap will not be embedded");
       } else {
           final WCMMode wcmMode = WCMMode.fromRequest(slingRequest);
           boolean shouldIncludeClientLib = false;
           if (WCMMode.EDIT != wcmMode && WCMMode.PREVIEW != wcmMode && WCMMode.DESIGN != wcmMode) {
               if (dim != null) {
                   final String mode = dim.getDeviceIdentificationModeForPage(currentPage);
                   shouldIncludeClientLib = DeviceIdentificationMode.CLIENT_SIDE.equals(mode);
                   if (shouldIncludeClientLib) {
                       browserMapEnabled = (Boolean) request.getAttribute("browsermap.enabled");
                       if (browserMapEnabled == null) {
                           browserMapEnabled = true;
                       }
                   }
               }
           }
   %>
           <c:if test="<%= !browserMapEnabled %>">
               <meta name="browsermap.enabled" content="false">
           </c:if>
           <c:if test="<%= shouldIncludeClientLib %>">
               <meta name="viewport" content="width=device-width, initial-scale=1.0">
               <cq:includeClientLib categories="browsermap.custom"/>
           </c:if>
   <%
       }
   %>
   ```

1. 将文件 `broswermap.jsp` 包含在头部部分。

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### 从某些页面中排除BrowserMap {#excluding-browsermap-from-certain-pages}

如果要从不需要客户端检测的某些页面中排除BrowserMap库，可以添加请求属性：

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

这将使脚本 `/libs/wcm/core/browsermap/browsermap.jsp` 向页面添加元标签，使其不 `BrowserMap` 执行任何检测：

```xml
<meta name="browsermap.enabled" content="false">
```

### 测试网站的特定版本 {#testing-a-specific-version-of-a-web-site}

通常，BrowserMap脚本会始终将访问者重定向到最合适的网站版本，通常会根据需要将访问者重定向到桌面或移动站点。

您可以通过向URL添加参数来强制使用任何请求的设备以测试网站的 `device` 特定版本。 以下URL将呈现Geometrixx Outdoors网站的移动版本。

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>该参 `wcmmode` 数设置为 `disabled` 以模拟发布实例的行为。

过渡设备值存储在cookie中，因此您无需为每个设备添加参数即可浏览 `device` 您的网站 `URL`。

因此，您需要调用设置为 `URL` 的同 `device` 一调用 `browser` ，才能返回桌面版网站。

>[!NOTE]
>
>BrowserMap将覆盖的设备值存储在名为的cookie中 `BMAP_device`。 删除此Cookie将确保CQ将根据您的当前设备（例如桌面或移动设备）提供相应版本的网站。

## 移动请求处理 {#mobile-request-processing}

AEM将处理由属于触控设备组的移动设备发出的请求，如下所示：

1. iPad向AEM发布实例发送请求，例如 `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM确定所请求页面的站点是否为移动站点(通过检查第一级页面是否扩展 `/content/geometrixx_mobile` 了移动页面组件)。 如果是：
1. AEM根据请求标头中的用户代理查找设备功能。
1. AEM将设备功能映射到设备组，并将其设 `touch` 置为设备组选择器。
1. AEM将请求重定向到 `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM将响应发送到iPad:

   * `products.touch.html` 以平易近人的方式呈现。
   * 渲染组件使用选择器来调整演示文稿。
   * AEM会自动将移动选择器添加到页面中的所有内部链接。

### 统计数据 {#statistics}

您可以获取有关移动设备向AEM服务器发出的请求数的一些统计信息。 可以细分请求数：

* 每个设备组和设备
* 每年，月和日

要查看统计信息，请执行以下操作：

1. 转到“工 **具** ”控制台。
1. 打开“工 **具** ”>“移动设备 **”下** 的“设备统 **计信息”页**&#x200B;面。
1. 单击链接可查看特定年份、月份或日的统计数据。

“统 **计信息** ”页如下所示：

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>“统 **计信息** ”页面是在移动设备首次访问AEM时创建的，并且被检测到。 在此之前，它不可用。

如果需要在统计信息中生成条目，可以按如下步骤继续：

1. 使用移动设备或模拟器(例如，https://chrispederick.com/work/user-agent-switcher/在Firefox上下载)。
1. 通过禁用创作模式在创作实例上请求移动页面，例如：
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

“统 **计信息** ”页现在可用。

### 支持“发送链接至朋友”链接的页面缓存 {#supporting-page-caching-for-send-link-to-a-friend-links}

移动页面通常可在Dispatcher上访问，因为为设备组呈现的页面在页面URL中由设备组选择器进行区分，例如 `/content/mobilepage.touch.html`。 不缓存对移动页面的请求（没有选择器），就像在这种情况下，设备检测操作并最终重定向到匹配的设备组（或“不匹配”）。 通过设备组选择器呈现的移动页面由链接重写器处理，该链接重写器重写页面内的所有链接以同时包含设备组选择器，从而防止对已经限定的页面上的每次点击重新执行设备检测。

因此，您可能会遇到以下情况：

用户Alice被重定向到 `coolpage.feature.html`设备组，并将该URL发送给朋友Bob,Bob使用位于设备组中的其他客户端访问 `touch` 它。

如果 `coolpage.feature.html` 从前端缓存中提供，则AEM没有机会分析请求以发现移动选择器与新的用户代理不匹配，而Bob得到的表示错误。

要解决此问题，您可以在页面上包含一个简单的选择UI，在该UI中，最终用户可以覆盖由AEM选择的设备组。 在上例中，如果最终用户认为其设备已足够用于此，则页面上的链接（或图标） `coolpage.touch.html` 允许他们切换到该页面。
