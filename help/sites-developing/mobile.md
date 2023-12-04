---
title: 为移动设备创建站点
description: 创建移动站点与创建标准站点类似，因为它还包括创建模板和组件
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
exl-id: 21b2037a-685a-441d-aecd-865884253e03
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '3720'
ht-degree: 0%

---

# 为移动设备创建站点{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

创建移动站点与创建标准站点类似，因为它还包括创建模板和组件。 有关创建模板和组件的更多详细信息，请参阅以下页面： [模板](/help/sites-developing/templates.md)， [组件](/help/sites-developing/components.md)、和 [AEM Sites开发入门](/help/sites-developing/getting-started.md). 主要区别在于在站点内启用Adobe Experience Manager (AEM)内置的移动功能。 这是通过创建依赖于移动页面组件的模板来实现的。

考虑使用 [响应式设计](/help/sites-developing/responsive.md)，创建适合多种屏幕大小的单个站点。

要开始配置，您可以查看 **We.Retail移动演示网站** 在AEM中可用。

要创建移动站点，请按照以下步骤操作：

1. 创建页面组件：

   * 设置 `sling:resourceSuperType` 属性至 `wcm/mobile/components/page`
这样，组件就可以依赖移动设备页面组件。

   * 创建 `body.jsp` 使用项目特定的逻辑。

1. 创建页面模板：

   * 设置 `sling:resourceType` 属性到新创建的页面组件。
   * 设置 `allowedPaths` 属性。

1. 为站点创建设计页面。
1. 在下创建站点根页面 `/content` 节点：

   * 设置 `cq:allowedTemplates` 属性。
   * 设置 `cq:designPath` 属性。

1. 在站点根页面的页面属性中，将设备组设置为 **移动设备** 选项卡。
1. 使用新模板创建网站页面。

移动设备页面组件( `/libs/wcm/mobile/components/page`)：

* 添加 **移动设备** 选项卡，转到页面属性对话框。
* 通过其 `head.jsp`，它会从请求中检索当前移动设备组，如果找到了某个设备组，则会使用该组的 `drawHead()` 方法，用于包含设备组的关联仿真器init组件（仅在创作模式下）和设备组的渲染CSS。

>[!NOTE]
>
>移动站点的根页面需要位于节点层次结构的1级，并且建议位于/content节点下方。

## 使用多站点管理器创建移动站点 {#creating-a-mobile-site-with-the-multi-site-manager}

使用多站点管理器(MSM)从标准站点创建移动Live Copy。 标准站点自动转换为移动站点：移动站点具有移动站点的所有功能（例如，在模拟器中编辑），并且可以与标准站点同步管理。 请参阅一节 [为不同渠道创建Live Copy](/help/sites-administering/msm.md) 在“多站点管理器”页面中。

## 服务器端Mobile API {#server-side-mobile-api}

包含移动类的Java™包包括：

* [com.day.cq.wcm.mobile.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html)  — 定义MobileConstants。
* [com.day.cq.wcm.mobile.api.device](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html)  — 定义Device、DeviceGroup和DeviceGroupList。
* [com.day.cq.wcm.mobile.api.device.capability](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html)  — 定义DeviceCapability
* [com.day.cq.wcm.mobile.api.wurfl](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/workflow/api/package-summary.html)  — 定义WurlQueryEngine。
* [com.day.cq.wcm.mobile.core](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/core/package-summary.html)  — 定义了MobileUtil，它提供了围绕WCM Mobile旋转的各种实用工具方法。

### 移动设备组件 {#mobile-components}

此 **We.Retail移动演示网站** 使用以下位于下面的移动设备组件 `/libs/foundation/components`：

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
   <td> — 页脚</td>
  </tr>
  <tr>
   <td>mobileimage</td>
   <td>移动设备</td>
   <td> — 基于图像基础组件<br />  — 如果设备能够呈现图像<br /> </td>
  </tr>
  <tr>
   <td>mobilelist</td>
   <td>移动设备</td>
   <td> — 基于list foundation组件<br /> - listitem_teaser.jsp在设备可以运行时呈现图像<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>隐藏</td>
   <td> — 基于徽标基础组件<br />  — 如果设备能够呈现图像<br /> </td>
  </tr>
  <tr>
   <td>mobilereference</td>
   <td>移动设备</td>
   <td><p> — 与reference foundation组件类似</p> <p> — 将文本时间组件映射到mobiletextimage组件，将图像组件映射到mobileimage组件</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>移动设备</td>
   <td> — 基于textimage foundation组件<br />  — 如果设备能够呈现图像</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>隐藏</td>
   <td><p> — 基于topnav foundation组件</p> <p> — 仅渲染文本</p> </td>
  </tr>
 </tbody>
</table>

#### 创建移动组件 {#creating-a-mobile-component}

AEM移动框架允许开发对发出请求的设备敏感的组件。 以下代码示例说明了如何在组件jsp中使用AEM移动设备API，特别是如何：

* 从请求中获取设备：
  `Device device = slingRequest.adaptTo(Device.class);`

* 获取设备组：
  `DeviceGroup deviceGroup = device.getDeviceGroup();`

* 获取设备组功能：
  `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* 获取设备属性（原始功能键/值来自WURFL数据库）：
  `Map<String,String> deviceAttributes = device.getAttributes();`

* 获取设备用户代理：
  `String userAgent = device.getUserAgent();`

* 从当前页面获取设备组列表（作者分配给站点的设备组）：
  `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* 检查设备组是否支持映像
  `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...或者
  `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>在jsp中， `slingRequest` 可通过 `<sling:defineObjects>` 标记和 `currentPage` 通过 `<cq:defineObjects>` 标记之前。

### 模拟器 {#emulators}

基于模拟器的创作为作者提供了创建针对移动客户端的内容页面的方法。 移动设备内容创作遵循与就地WYSIWYG编辑相同的原则。 为了使作者能够感知移动设备上的页面外观，可使用设备模拟器编辑移动设备内容页面。

移动设备模拟器基于通用模拟器框架。 有关更多详细信息，请参阅 [模拟器](/help/sites-developing/emulators.md).

设备仿真器在页面上显示移动设备，而常规的编辑（parsys、组件）会在设备的屏幕内进行。 设备模拟器取决于为该站点配置的设备组。 可以为一个设备组分配多个模拟器。 随后，所有模拟器都将显示在内容页面上。 默认情况下，将显示分配给分配给站点的第一个设备组的第一个模拟器。 模拟器可通过页面顶部的模拟器轮播或Sidekick的编辑按钮进行切换。

**创建模拟器**

要创建模拟器，请参见 [创建自定义移动模拟器](/help/sites-developing/emulators.md) 在通用的“模拟器”页面中。

**移动仿真器的主要特性**

* 设备组由一个或多个模拟器组成：设备组配置页面（例如，/etc/mobile/groups/touch）包含 `emulators` 属性位于 `jcr:content` 节点。
注意：虽然同一模拟器可能属于多个设备组，但这并没有多大意义。

* 通过设备组的配置对话框， `emulators` 属性通过所需模拟器的路径进行设置。 例如：`/libs/wcm/mobile/components/emulators/iPhone4`。

* 模拟器组件(例如， `/libs/wcm/mobile/components/emulators/iPhone4`)扩展基本移动模拟器组件( `/libs/wcm/mobile/components/emulators/base`)。

* 在配置设备组时，每个扩展基本移动仿真器的组件都可以选择。 因此，可以轻松创建或扩展自定义模拟器。
* 在编辑模式的请求时，使用模拟器实施来呈现页面。
* 当页面的模板依赖于移动页面组件时，模拟器功能会自动集成在页面中(通过 `head.jsp` （属于移动设备页面组件）。

### 设备组 {#device-groups}

移动设备组根据设备功能对移动设备进行分段。 设备组提供创作实例上基于模拟器的创作以及在发布实例上正确呈现内容所需的信息：一旦作者将内容添加到移动页面并进行发布，就可以在发布实例上请求页面。 在这里，使用其中一个配置的设备组呈现内容页面，而不是模拟器编辑视图。 设备组的选择基于 [移动设备检测](#devicedetection). 然后，匹配的设备组会提供所需的样式信息。

设备组在下方定义为内容页面 `/etc/mobile/devices` 并使用 **移动设备组** 模板。 设备组模板可用作内容页面形式的设备组定义的配置模板。 其主要特点是：

* 位置： `/libs/wcm/mobile/templates/devicegroup`
* 允许的路径： `/etc/mobile/groups/*`
* 页面组件： `wcm/mobile/components/devicegroup`

#### 将设备组分配给您的站点 {#assigning-device-groups-to-your-site}

创建移动网站时，需要为网站分配设备组。 根据设备的HTML和JavaScript渲染功能，AEM提供了三个设备组：

* **功能** 手机，适用于Sony Ericsson W800等功能设备，支持基础HTML，但不支持图像和JavaScript。
* **Smart** 手机，适用于像BlackBerry®这样的设备，它支持基本HTML和图像，但不支持JavaScript。

* **触控** 手机，适用于像iPad这样的设备，完全支持HTML、图像、JavaScript和设备旋转。

由于模拟器可以与设备组相关联（请参阅部分） [创建设备组](#creating-a-device-group))，将设备组分配到站点后，作者可以在与设备组关联的模拟器之间进行选择，以编辑页面。

要为站点分配设备组，请执行以下操作：

1. 在浏览器中，转到 **Siteadmin** 控制台。
1. 在下面打开您的移动站点的根页面 **网站**.
1. 打开页面属性。
1. 选择 **移动设备** 选项卡：

   * 定义设备组。
   * 单击&#x200B;**确定**。

>[!NOTE]
>
>为网站定义设备组后，网站的所有页面都会继承这些设备组。

#### 设备组筛选器 {#device-group-filters}

设备组筛选器定义了基于功能的标准，用于确定设备是否属于组。 在创建设备组时，可以选择用于评估设备的过滤器。

在运行时，当AEM收到来自设备的HTTP请求时，与组关联的每个过滤器都会将设备功能与特定条件进行比较。 如果设备具有过滤器所需的所有功能，则将其视为属于该组。 从WURFL™数据库中检索功能。

设备组可以使用零个或多个过滤器进行功能检测。 此外，过滤器也可以与多个设备组一起使用。 AEM提供了一个默认筛选器，用于确定设备是否具有为组选择的功能：

* CSS
* JPG和PNG图像
* JavaScript
* 设备旋转

如果设备组不使用过滤器，则为该组配置的选定功能是设备唯一需要的功能。

有关更多信息，请参阅 [创建设备组筛选器](/help/sites-developing/groupfilters.md).

#### 创建设备组 {#creating-a-device-group}

当AEM安装的组不符合您的要求时，请创建一个设备组。

1. 在浏览器中，转到 **工具** 控制台。
1. 在下方创建页面 **工具** > **移动设备** > **设备组**. 在 **创建页面** 对话框：

   * 作为 **标题**，输入 `Special Phones`.

   * 作为 **名称**，输入 `special`.

   * 选择 **移动设备组模板**.
   * 单击&#x200B;**创建**。

1. 在CRXDE中，添加 **static.css** 包含设备组以下样式的文件 `/etc/mobile/groups/special` 节点。

1. 打开 **特殊电话** 页面。
1. 要配置设备组，请单击 **编辑** 按钮旁边 **设置**.
在 **常规** 选项卡：

   * **标题**：移动设备组的名称。
   * **描述**：组的描述。
   * **User-Agent**：设备匹配的用户代理字符串。 它是可选的，也可以是正则表达式。 示例： `BlackBerryZ10`
   * **功能**：定义组是否可以处理图像、CSS、JavaScript或设备旋转。
   * **最小屏幕宽度**&#x200B;和&#x200B;**高度**
   * **禁用模拟器**：在内容编辑期间启用/禁用模拟器。

   在 **模拟器** 选项卡：

   * **模拟器**：选择分配给此设备组的模拟器。

   在 **过滤器** 选项卡：

   * 要添加筛选器，请单击添加项，然后从下拉列表中选择一个筛选器。
   * 过滤器会按照其显示顺序进行评估。 当设备不符合过滤器的条件时，不评估列表中的后续过滤器。

1. 单击“确定”。

移动设备组配置对话框如下所示：

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### 每个设备组的自定义CSS {#custom-css-per-device-group}

如前所述，可以将自定义CSS与设备组页面关联，就像设计页面的CSS一样。 此CSS用于影响创作和发布时特定于设备组的页面内容渲染。 然后，将自动包含此CSS：

* 在创作实例的页面中，对于此设备组使用的每个模拟器。
* 在发布实例的页面中，如果请求的用户代理与此特定设备组中的移动设备匹配。

## 服务器端设备检测 {#server-side-device-detection}

使用筛选器和设备规范库来确定执行HTTP请求的设备的功能。

### 开发设备组筛选器 {#develop-device-group-filters}

创建设备组筛选器以定义一组设备功能要求。 根据需要创建任意数量的过滤器，以定位所需的设备功能组。

设计您的过滤器，以便您可以使用这些过滤器的组合来定义功能组。 通常，不同设备组的功能会重叠。 因此，您可以使用具有多个设备组定义的某些筛选器。

创建筛选器后，您可以在组配置中使用它。

有关信息，请访问 [创建设备组筛选器](/help/sites-developing/groupfilters.md).

### 使用WURFL™数据库 {#using-the-wurfl-database}

AEM使用截断版本的 [WURFL](https://wurfl.sourceforge.net/)™数据库根据设备的用户代理查询设备功能，如屏幕分辨率或JavaScript支持。

WURFL™数据库的XML代码表示为以下节点 `/var/mobile/devicespecs` 通过解析 `wurfl.xml`文件位于 `/libs/wcm/mobile/devicespecs/wurfl.xml.` 在第一次执行扩展时，将展开到节点。 `cq-mobile-core` 捆绑包已启动。

设备功能作为节点属性存储，节点表示设备型号。 您可以使用查询检索设备或用户代理的功能。

随着WURFL™数据库的不断发展，您可能需要对其进行自定义或替换。 要更新移动设备数据库，您可以使用以下选项：

* 如果您拥有允许此使用的许可证，请使用最新版本替换文件。 请参阅安装其他WURFL数据库。
* 使用AEM中可用的版本，并配置一个与User-Agent字符串匹配并指向现有WURFL™设备的正则表达式。 请参阅 [添加基于正则表达式的用户代理匹配](#adding-a-regexp-based-user-agent-matching).

#### 测试用户代理到WURFL™功能的映射 {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

当设备访问您的移动网站时，AEM会检测该设备，根据其功能将其映射到设备组，并发送与设备组对应的页面视图。 匹配的设备组提供了必要的样式信息。 可以在Mobile User-Agent的“测试”页上测试映射：

`https://localhost:4502/etc/mobile/useragent-test.html`

#### 安装其他WURFL™数据库 {#installing-a-different-wurfl-database}

与AEM一起安装的截断的WURFL™数据库是2011年8月30日之前的版本。 如果您的WURFL版本是在2011年8月30日之后发布的，请确保您的使用符合您的许可证。

安装WURFL™数据库：

1. 在CRXDE Lite中，创建以下文件夹： `/apps/wcm/mobile/devicespecs`
1. 将WURFL™文件复制到文件夹中。
1. 将文件重命名为 `wurfl.xml`.

AEM自动解析 `wurfl.xml` 文件并更新以下节点 `/var/mobile/devicespecs`.

>[!NOTE]
>
>启用完整的WURFL™数据库后，解析和激活可能需要几分钟的时间。 您可以查看日志以了解进度信息。

#### 添加基于正则表达式的用户代理匹配 {#adding-a-regexp-based-user-agent-matching}

在/apps/wcm/mobile/devicespecs/wurfl/regexp下添加用户代理作为正则表达式，以指向现有的WURFL™设备类型。

1. 在 **CRXDE Lite**，在/apps/wcm/mobile/devicespecs/regexp下创建一个节点，例如， `apple_ipad_ver1`.
1. 将以下属性添加到节点：

   * **regexp**：定义用户代理的正则表达式，例如。&#42;莫兹拉。&#42;iPad。&#42;AppleWebKit。&#42;Safari&#42;
   * **deviceId**：wurfl.xml中定义的设备ID，例如， `apple_ipad_ver1`

上述配置导致用户代理与提供的正则表达式匹配的设备映射到apple_ipad_ver1 WURFL™设备ID（如果存在）。

## 客户端设备检测 {#client-side-device-detection}

本节介绍如何使用AEM的设备客户端检测来优化页面渲染或向客户端提供替代网站版本。

AEM支持基于设备客户端检测 `BrowserMap`. `BrowserMap` 在AEM中作为客户端库提供，位于 `/etc/clientlibs/browsermap`.

`BrowserMap` 为您提供三种策略，您可以使用这两种策略向客户提供备用网站，其应用顺序如下：

1. [备用链接](#providing-alternate-links)
1. [设备组特定URL](#definingdevicegroupspecificurl)
1. [基于选择器的URL](#defining-selector-based-urls)

>[!NOTE]
>
有关客户端库集成的详细信息，请参阅 [使用客户端HTML库](/help/sites-developing/clientlibs.md).

### 提供备用链接 {#providing-alternate-links}

此 `PageVariantsProvider` OSGi服务能够为属于同一系列的网站生成备用链接。 要配置服务要考虑的站点，请 `cq:siteVariant` 节点必须添加到 `jcr:content` 站点的根目录中的节点。

此 `cq:siteVariant` 节点必须具有以下属性：

* `cq:childNodesMapTo`  — 确定子节点将映射到的链接元素的属性；建议以这种方式组织网站的内容，以便根节点的子节点表示全局网站的语言变体的根(例如， `/content/mysite/en`， `/content/mysite/de`)，在这种情况下，的 `cq:childNodesMapTo` 应为 `hreflang`；
* `cq:variantDomain`  — 指示内容 `Externalizer` 域用于生成页面变体绝对URL；如果未设置此值，则使用相对链接生成页面变体；
* `cq:variantFamily`  — 指示此网站属于哪个网站系列；同一网站的多个特定于设备的表示应属于同一系列；
* `media`  — 存储链接元素的媒体属性的值；建议使用 `BrowserMap` 已注册 `DeviceGroups`，以便 `BrowserMap` 库可以自动将客户端转发到网站的正确变体。

#### PageVariantsProvider和Externalizer {#pagevariantsprovider-and-externalizer}

当 `cq:variantDomain` 属性 `cq:siteVariant` 节点不为空， `PageVariantsProvider` 服务使用此值作为的已配置域来生成绝对链接 `Externalizer` 服务。 确保配置 `Externalizer` 服务以反映您的设置。

>[!NOTE]
>
使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解更多详细信息和建议的做法。

### 定义特定于设备组的URL {#defining-a-device-group-specific-url}

如果您不想使用备用链接，则可以为每个链接配置全局URL `DeviceGroup`. Adobe建议创建自己的客户端库，其中嵌入 `browsermap.standard` 客户端库，但重新定义了设备组。

BrowserMap的设计方式允许通过创建具有相同名称的设备组并将其添加到来覆盖设备组定义 `BrowserMap` 自定义客户端库中的对象。

>[!NOTE]
>
有关更多详细信息，请参阅 [自定义的BrowserMap](#creatingacustomisedbrowsermap).

### 定义基于选择器的URL {#defining-selector-based-urls}

如果以前没有采用任何机制来指示替代站点 `BrowserMap`，然后将使用 `DeviceGroups` 将被添加到 `URL`s，在这种情况下，您应该提供自己的将处理请求的servlet。

例如，设备浏览 `www.example.com/index.html` 标识为 `smartphone` 通过BrowserMap转发到 `www.example.com/index.smartphone.html.`

### 在页面上使用浏览器地图 {#using-browsermap-on-your-pages}

要在页面中使用标准BrowserMap客户端库，您必须包含 `/libs/wcm/core/browsermap/browsermap.jsp` 文件使用 `cq:include`标记的位置 `head` 部分。

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

除了添加 `BrowserMap` 您的中的客户端库 `JSP` 文件，您还必须添加 `cq:deviceIdentificationMode` 字符串属性设置为 `client-side` 到 `jcr:content` 节点。

### 覆盖BrowserMap的默认行为 {#overriding-browsermap-s-default-behaviour}

如果要自定义 `BrowserMap`  — 透过覆写 `DeviceGroups` 或添加更多探测器 — 然后您应该创建自己的客户端库，并在其中嵌入 `browsermap.standard`客户端库。

此外，您必须手动调用 `BrowserMap.forwardRequest()` 中的方法 `JavaScript` 代码。

>[!NOTE]
>
有关客户端库集成的详细信息，请参阅 [使用客户端HTML库](/help/sites-developing/clientlibs.md).

创建您的自定义设置后 `BrowserMap` 客户端库，Adobe建议采用以下方法：

1. 创建 `browsermap.jsp` 文件中的文件

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

1. 包括 `broswermap.jsp` 你头部的档案。

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### 从某些页面中排除浏览器地图 {#excluding-browsermap-from-certain-pages}

如果您希望从某些不需要客户端检测的页面中排除BrowserMap库，则可以添加请求属性：

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

这将使 `/libs/wcm/core/browsermap/browsermap.jsp` 用于向将生成的页面添加meta标记的脚本 `BrowserMap` 不执行任何检测：

```xml
<meta name="browsermap.enabled" content="false">
```

### 测试网站的特定版本 {#testing-a-specific-version-of-a-web-site}

通常，BrowserMap脚本始终将访客重定向到网站的最佳版本，通常会在需要时将访客重定向到桌面或移动网站。

您可以通过添加 `device` 参数到您的URL。 以下URL呈现Geometrixx Outdoors网站的移动版本。

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
此 `wcmmode` 参数设置为 `disabled` 以模拟发布实例的行为。

覆盖的设备值存储在Cookie中，因此您可以浏览网站而不添加 `device` 参数到 `URL`.

因此，您需要调用相同的 `URL` 使用 `device` 设置为 `browser` 以返回到网站的桌面版本。

>[!NOTE]
>
BrowserMap将覆盖设备值存储在名为的Cookie中 `BMAP_device`. 删除此Cookie可确保CQ将根据您当前的设备（例如，桌面或移动设备）提供相应版本的网站。

## 移动请求处理 {#mobile-request-processing}

AEM会按如下方式处理由属于触控设备组的移动设备发出的请求：

1. iPad向AEM发布实例发送请求，例如， `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM确定所请求页面的网站是否为移动网站(通过检查第一级页面是否 `/content/geometrixx_mobile` 扩展了移动设备页面组件)。 如果是：
1. AEM会根据请求标头中的User-Agent查找设备功能。
1. AEM将设备功能映射到设备组并设置 `touch` 作为设备组选择器。
1. AEM将请求重定向到 `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM将响应发送到iPad：

   * `products.touch.html` 以常规方式呈现并是可缓存的。
   * 渲染组件使用选择器来调整表示法。
   * AEM会自动将移动设备选择器添加到页面中的所有内部链接。

### 统计数据 {#statistics}

您可以获取有关移动设备向AEM服务器发出的请求数的一些统计信息。 请求数可以细分：

* 每个设备组和设备
* 每年、月、日

要查看统计信息，请执行以下操作：

1. 转到 **工具** 控制台。
1. 打开 **设备统计数据** 页面如下 **工具** > **移动设备**.
1. 单击该链接可查看特定年、月或日的统计信息。

此 **统计数据** 页面如下所示：

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
此 **统计数据** 在移动设备首次访问AEM并检测到该移动设备时创建页面。 在此之前，该函数不可用。

如果需要在统计信息中生成一个条目，可以按如下方式继续操作：

1. 使用移动设备或模拟器(例如，Firefox上的https://chrispederick.com/work/user-agent-switcher/)。
1. 通过禁用创作模式在创作实例上请求移动页面，例如：
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

此 **统计数据** 页面现已可用。

### 支持“将链接发送到朋友”链接的页面缓存 {#supporting-page-caching-for-send-link-to-a-friend-links}

移动设备页面可在Dispatcher上缓存，因为为设备组呈现的页面在页面URL中被设备组选择器区分开，例如， `/content/mobilepage.touch.html`. 绝不会缓存对没有选择器的移动页面的请求，因为在这种情况下，设备检测会运行，并且最终重定向到匹配的设备组（或就此而言的“不匹配”）。 使用设备组选择器呈现的移动页面由链接重写器处理，该链接重写器重写页面内的所有链接以同时包含设备组选择器，从而防止对已经限定的页面的每次点击重新执行设备检测。

因此，您可能会遇到以下情况：

用户Alice被重定向到 `coolpage.feature.html`，并将该URL发送给朋友Bob，后者通过位于网站上的 `touch` 设备组。

如果 `coolpage.feature.html` 从前端缓存中提供，AEM没有机会分析请求以找出移动设备选择器与新的用户代理不匹配，并且Bob获得错误的表示形式。

要解决此问题，您可以在页面上包括一个简单的选择UI，最终用户可以在其中覆盖AEM选择的设备组。 在上例中，页面上的链接（或图标）允许最终用户切换到 `coolpage.touch.html` 如果他们认为他们的设备足够好。
