---
title: 开箱即用的应用程序处理程序
seo-title: 开箱即用的应用程序处理程序
description: 可查看本页以了解适用于AEM的Adobe PhoneGap Enterprise的现成处理程序。
seo-description: 可查看本页以了解适用于AEM的Adobe PhoneGap Enterprise的现成处理程序。
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 开箱即用的应用程序处理程序{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

请参阅以下内容同步处理程序开发指南：

* 处理函数必 *须实现com.day.cq.contentsync.handler.ContentUpdateHandler* （直接或扩展需要实现的类）
* 处理函数可 *以扩展com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 仅当处理函数更新了ContentSync缓存时，它们必须报告为true。 错误报告为true将允许AEM创建更新。
* 仅当内容实际发生更改时，处理程序才应更新缓存。 如果不需要白色，请勿写入缓存，并避免创建不必要的更新。

## 开箱即用的处理程序 {#out-of-the-box-handlers}

以下列出了现成的应用程序处理程序：

**mobileappages** 呈现应用程序页面。

* ***type - String*** - mobileappages
* ***path —— 字符串*** -页面路径
* ***extension - String*** —— 请求中应使用的扩展。 对于页面，这几乎总是 *html*，但其他内容仍然可能。

* ***选择器——字符串*** -以点分隔的可选选择器。 常见示例 *包括触控* ，用于呈现页面的移动版本。

* ***deep - Boolean*** —— 确定是否也应包括子页面的可选布尔属性。 The default value is *true.*

* ***includeImages - Boolean*** —— 确定是否应包括图像的可选布尔属性。 The default value is *true*.

   * 默认情况下，仅考虑包含资源类型为foundation/components/image的图像组件。

* ***includeVideos - Boolean*** —— 可选的布尔属性确定视频是否应包括在内。 The default value is *true*.

* ***includeModifiedPagesOnly - Boolean*** —— 如果为false或省略，则渲染所有页面并检查渲染中的更新。 如果为true，则基数会因页面lastModified的更改而有所不同。
* ***+重写（节点）***
   ***- relativeParentPath - String*** —— 写入所有其他相对路径的路径。

>[!NOTE]
>
>通过配置com.adobe.cq.mobile.platform.impl.contentsync.handler的属性，可以设置受此处理函数影响的图像和视频组件的资源类型 **。*MobilePagesUpdateHandler OSGi服务*。

**mobilepageassets** 收集应用程序页面资产。

**mobilecontentlisting** 列出ContentSync zip的内容。 设备上的客户端js使用它执行AEM应用程序所需的初始文件复制。

此处理函数应添加到任何AEM应用程序ContentSync配置。

* ***type - String - mobilecontenlisting***
* ***path*** - String - keep empty，必须显示为有效的处理函数，但路径被推断为当前ContentSync缓存。 将忽略此值。
* ***targetRootDirectory ***- String —— 添加到路径的前缀，作为此处理函数内容更新的目标根目录。
* ***order - Long *- Order for ContentSync **to extute this handler. 此数字应设置为高于所有其他处理函数（如100）。 它应在传统内容处理程序之后运行。

```xml
{
  "files": [
    "config.xml",
    "res/screens/ios/screen-ipad-portrait-2x.png",
    "res/screens/ios/screen-ipad-landscape.png",
    "res/screens/ios/screen-iphone-portrait-2x.png",
    "res/screens/ios/screen-iphone-landscape.png",
    "res/screens/ios/screen-iphone-portrait.png",
    "apps/weretail-app/components/splash-page/clientlibs.css",
    ...
    "pge-content-packages.json"
  ],
  "count": 382,
  "lastModified": 1422902754733
}
```

**mobilecontentpackageslist** 列出给定应用程序中的AEM内容包以及向其发出更新请求的serverURL。 这是使用设备上的客户端js请求内容更新

此处理函数应用于AEM App Shell ContentSync配置（pge-type=app-instance的节点）

* ***type - String - mobilecontentpackageslisting***
* ***path **-**String*** —— 应用程序Shell的路径（pge-type=app-instance的节点）。
* ***targetRootDirectory - String*** —— 添加到路径的前缀，作为此处理函数的内容更新的目标根目录。
* ***order - Long *- Order **for ContentSync to execute this handler. 此数字应设置为高于所有其他处理函数（如100）。 它应在传统内容处理程序之后运行。

>[!NOTE]
>
>以下代码块不是确切的实现，应用作参考示例：

```xml
{
  "content": [
    {
      "name": "en",
      "title": "We Retail Mobile App - English",
      "type": "CONTENT",
      "path": "/content/phonegap/weretail-outdoors/en",
      "updatePath": "/content/phonegap/weretail/en/jcr:content/pge-app/app-config"
    },
    {
      "name": "shell",
      "title": "We Retail Mobile App",
      "type": "INSTANCE",
      "path": "/content/phonegap/weretail-outdoors/shell",
      "updatePath": "/content/phonegap/weretail/shell/jcr:content/pge-app/app-config"
    }
  ],
  "serverURL": "http://localhost:4503/"
}
```

**widgetconfig** 包含更新的config.xml，它将通过命令中心所做的任何编辑与提供的config.xml合并。 如果此处理函数未包含通过“管理”界面更改的任何应用程序详细信息，则缓存中将不包含这些详细信息。

此处理函数应用于AEM App Shell ContentSync配置(pge-type=[app-instance的节点])。

* ***type —— 字符串* - **widgetconfig
* ***path **-**String*** —— 指向任何应用程序Shell子节点的路径(pge-type=[app-instance]的节点)。
* ***targetRootDirectory - String*** —— 添加到路径的前缀，作为此处理函数的内容更新的目标根目录。
* ***targetIconDirectory - String*** —— 放置应用程序图标的目录

**mobileADBMobileConfigJSON** 如果配置了AMS云服务，则包括ADBMobileConfig.JSON文件。

它在编译时用于配置AMS插件以获得分析支持。

此处理函数应用于AEM App Shell ContentSync配置（pge-type=app-instance的节点）

* ***type - String*** - mobileADBMobileConfigJSON
* ***path —— 字符串*** -应用程序Shell的路径（pge-type=app-instance的节点或扩展/libs/mobileapps/core/components/instance的RT）
* ***targetRootDirectory - String*** —— 添加到路径的前缀，作为此处理函数的内容更新的目标根目录

**通知配置** 提取设备上所需的通知配置。 这些属性从与应用程序相关联的各个推送服务云服务配置中提取。

将提取云服务的jcr:content节点中的非AEM属性并将其添加到 **pge-notifications-config.json** JSON文件，以包含在应用程序内容的wwwroot中。

AEM属性是名称间隔为“cq”、“sling”或“jcr”的属性。 其他属性可能会使用content-sync配置节点上的“excludeProperties”属性来排除。

* ***type —— 字符串*** -通知config
* ***excludeProperties - String[]*** —— 要排除的属性

**contentsyncconfigcontent** 从现有ContentSync配置收集内容。

* ***type - String*** - contentsyncconfigcontent
* ***path - String*** —— 指向以下任一路径：

   * 另一ContentSync配置
   * 到内容包（将使用其phonegap-exportTemplate属性查找其ContentSync配置）
   * 到移动资源（将在该资源下找到app-content的，如果这些内容包具有pge-includeInBuild属性，则phonegap-exportTemplate将用于查找其ContentSync配置）

* ***autoCreateFirstUpdateBeforeImport - Boolean*** —— 如果为true，请在导入之前在目标配置中创建初始 **更新** （如果一次不存在）

* ***autoFillBeforeImport - Boolean*** —— 如果为true，请在导入之前更新／填充目标配置
* ***configSuffix —— 字符串*** -要附加到app-content的“phonegap-exportTemplate”属性上指示的路径的字符串。 这可用于区分不同的导出模板。 例如，此属性可设置为 **&quot;-dev&quot;** ，以指示应使用 *&quot;/../../appconfig-dev&quot;***（与&quot;/.../../../appconfig&quot;相对）。

**app-assets** 包括与应用程序实例关联的所有资产。 此处理函数将包括在指定路径下找到的任何资产以及应用程序实例的appAssetPath属性引用的任何资产。

* ***type - String*** - app-assets

* ***path **-**String*** —— 应用程序实例下存储应用程序资源的位置的路径

**mobileapporfers** 为个性化用例引入了一个新的内容同步处理程序，用于呈现目标内容。 “mobileapporfers”处理函数知道如何呈现由内容作者创建的关联目标选件。 mobileapporfers处理程序扩展了抽象页面更新处理程序，因此许多属性都类似。 mobileapporfers处理程序的详细信息具有以下属性。

mobileappsoffers处理函数扩展mobileappspages处理函数并添加以下属性：

* ***locationRoot - String*** —— 指定手机应用程序的位置
* ***includePageTypes - String*** —— 默认支持cq/personalization/components/teaserpage和cq/personalization/components/offerproxy
* ***选择器*** -字符串——应设置为
* ***path —— 字符串***-指向营销活动品牌的路径

**mobileappconfig** mobileappconfig内容同步处理程序提供了一种将JSON数据注入MobileAppsConfig.json的方法。 要注册提供者类，开发人员将其MobileAppsInfoProvider类添加到提供者列表中。 该处理函数将迭代MobileAppsInfoProviders列表，并允许提供者将数据注入到生成的json文件中。 此处理函数支持的属性列表包括：

* ***path **-**String*** —— 指向pge-type=app-instance的应用程序实例节点或扩展/libs/mobileapps/core/components/instance的RT的路径
* ***提供者——字符串*** - `[]` 完全限定的MobileAppsInfoProviders列表
* ***targetRootDirectory - String*** —— 将MobileAppsConfig.json文件写入的目录。
* **fileName - String** —— 要将JSON写入的文件的可选名称，默认为MobileAppsConfig.json

可以配置多个mobileappconfig处理函数，每个函数都配置有一组写入不同JSON文件的唯一提供者。

### 测试内容同步处理程序 {#testing-content-sync-handlers}

**检查完整性清除缓存的步骤** （英文）

* 清除缓存
* 运行处理程序（已更新缓存）
* 再次运行处理函数（不应更新缓存）

**调试步骤**

* 运行配置
* 在设备上导出配置或查看
* 如果渲染失败，请检查 *是否缺少样式／资源/lib* ，或检查样式／资源/lib *的不良路径*

**记录**`com.day.cq.contentsync` 通过OSGI记录器配置在包上启用ContentSync调试记录此操作允许您跟踪运行了哪些处理程序以及它们是否更新了缓存并报告了更新缓存。

## 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM为Adobe PhoneGap Enterprise进行创作](/help/mobile/phonegap.md)
* [通过AEM管理Adobe phoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>要开始使用AEM mobile应用程序开发，请单击 [此处](/help/mobile/getting-started-aem-mobile.md)。

