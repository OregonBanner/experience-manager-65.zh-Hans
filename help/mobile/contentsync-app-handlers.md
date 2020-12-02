---
title: 开箱即用的应用程序处理程序
seo-title: 开箱即用的应用程序处理程序
description: 可查看本页，了解包含AEM的Adobe PhoneGap企业的现成处理程序。
seo-description: 可查看本页，了解包含AEM的Adobe PhoneGap企业的现成处理程序。
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---


# 开箱即用的应用程序处理程序{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

请参阅以下内容同步处理程序开发指南：

* 处理函数必须实现&#x200B;*com.day.cq.contentsync.handler.ContentUpdateHandler*（直接或扩展具有该功能的类）
* 处理函数可以扩展&#x200B;*com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 仅当处理程序更新了ContentSync缓存时，它们必须报告为true。 假报告true将允许AEM创建更新。
* 仅当内容实际发生更改时，处理程序才应更新缓存。 如果不需要白色，请不要写到缓存中，并避免不必要的更新创建。

## 开箱即用的处理程序{#out-of-the-box-handlers}

以下列表现成的应用程序处理程序：

**mobileappages** 呈现应用程序页面。

* ***type - String***  - mobileappages
* ***path —— 字符串*** -页面的路径
* ***extension —— 字符串*** -应在请求中使用的扩展。对于页面，这几乎始终为&#x200B;*html*，但其他页面仍有可能。

* ***选择器*** -字符串——可选选择器，以点分隔。常见示例包括用于呈现移动版本页面的&#x200B;*touch*。

* ***deep - Boolean***  —— 可选布尔属性，用于确定是否也应包括子页面。默认值为&#x200B;*true。*

* ***includeImages - Boolean***  —— 可选布尔属性，用于确定是否应包括图像。默认值为&#x200B;*true*。

   * 默认情况下，仅考虑包含资源类型为foundation/components/image的图像组件。

* ***includeVideos - Boolean***  —— 可选布尔属性确定视频是否应包括。默认值为&#x200B;*true*。

* ***includeModifiedPagesOnly - Boolean***  —— 如果为false或省略，则渲染所有页面并检查渲染中的更新。如果为true，则基本差异取决于对页面lastModified的更改。
* ***+重写（节点）***
   ***- relativeParentPath - String***  —— 写入相对于的所有其他路径的路径。

>[!NOTE]
>
>通过配置&#x200B;*com.adobe.cq.mobile.platform.impl.contentsync.handler*&#x200B;的属性，可设置受此处理函数影响的图像和视频组件的资源类型。*MobilePagesUpdateHandler OSGi服务*。

**mobile** ageassets收集应用程序页面资产。

**** mobilecontentlisting列出ContentSync zip的内容。设备上的客户端js使用它执行AEM应用程序所需的初始文件复制。

此处理函数应添加到任何AEM Apps ContentSync配置。

* ***type —— 字符串- mobilecontenlisting***
* ***path***  —— 字符串——保持为空，必须显示为有效的处理函数，但路径被推断为当前ContentSync缓存。将忽略此值。
* ***targetRootDirectory* -**String —— 添加到路径的前缀，作为此处理函数的内容更新的目标根。
* ***顺序- ContentSync* 执&#x200B;**行此处理函数的长顺序。此数字应设置为高于所有其他句柄（如100）。 它应在传统内容处理程序之后运行。

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

**** mobilecontentpackageslisting列出给定应用程序中的AEM内容包以及向其发出更新请求的serverURL。这是使用设备上的客户端js请求内容更新

此处理函数应用于AEM App Shell ContentSync配置（pge-type=app-instance的节点）

* ***type —— 字符串- mobilecontentpackageslisting***
* ***path **-**String*** -应用程序Shell的路径（pge-type=app-instance的节点）。
* ***targetRootDirectory - String***  —— 添加到路径的前缀，作为此处理函数内容更新的目标根。
* ***顺序- Content* Sync **执行此处理函数的长顺序。此数字应设置为高于所有其他句柄（如100）。 它应在传统内容处理程序之后运行。

>[!NOTE]
>
>以下代码块不是确切的实现，应当用作参考示例：

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

**** widgetconfig包含已更新的config.xml，它将通过命令中心所做的任何编辑与提供的config.xml合并。如果此处理函数未包含通过“管理”界面更改的任何应用程序详细信息，则缓存中将不包含这些详细信息。

此处理函数应用于AEM App Shell ContentSync配置（pge-type=[app-instance]的节点）。

* ***类型——字符串* - **widgetconfig
* ***path **- String**-指向任何应用程序shell子节点(pge-type=*** app-instance的节点[])的路径。
* ***targetRootDirectory - String***  —— 添加到路径的前缀，作为此处理函数内容更新的目标根。
* ***targetIconDirectory - String***  —— 放置应用程序图标的目录

**如** 果配置了AMS云服务，请包含ADBMobileConfig.JSON文件。

此插件在编译时用于配置AMS插件以获得分析支持。

此处理函数应用于AEM App Shell ContentSync配置（pge-type=app-instance的节点）

* ***type - String***  - mobileADBMobileConfigJSON
* ***path —— 字符串*** -应用程序Shell的路径（pge-type=app-instance的节点或扩展/libs/mobileapps/core/components/instance的RT）
* ***targetRootDirectory - String***  —— 添加到路径的前缀，作为此处理函数的内容更新的目标根

**通** 知config提取设备上所需的通知配置。属性从与应用程序关联的相应推送服务云服务配置中提取。

云服务的jcr:content节点中的非AEM属性被提取并添加到&#x200B;**pge-notifications-config.json** JSON文件中，以包含在应用程序内容的www root中。

AEM属性是名称间隔为“cq”、“sling”或“jcr”的属性。 其他属性可能会使用content-sync配置节点上的“excludeProperties”属性排除。

* ***type —— 字符串*** -通知config
* ***excludeProperties —— 字符串[]*** -要排除的属性

**content** syncconfigcontent从现有ContentSync配置收集内容。

* ***类型——字符串*** -内容syncconfigcontent
* ***path —— 字符串*** -指向以下任一路径：

   * 另一个ContentSync配置
   * 到内容包（将使用其phonegap-exportTemplate属性查找其ContentSync配置）
   * 到移动资源（将在该资源下找到app-content&#39;s；如果这些内容包具有pge-includeInBuild属性，则phonegap-exportTemplate将用于查找其ContentSync配置）

* ***autoCreateFirstUpdateBeforeImport - Boolean*** -如果为true，请在目标配置中创建 **** 初始更新，然后导入（如果不存在）

* ***autoFillBeforeImport - Boolean***  —— 如果为true，请在导入之前更新／填充目标配置
* ***configSuffix —— 字符串*** -要附加到app-content的“phonegap-exportTemplate”属性上指示的路径的字符串。这可用于区分不同的导出模板。 例如，此属性可设置为&#x200B;**&quot;-dev&quot;**&#x200B;以指示应使用&#x200B;*&quot;/../../../../appconfig-dev&quot;*（与&#x200B;*&quot;/.../../appconfig&quot;*&#x200B;相对）。

**app-assets包** 括与应用程序实例关联的所有资产。此处理函数将包括在指定路径下找到的任何资产以及应用程序实例的appAssetPath属性引用的任何资产。

* ***类型——字符串*** -应用程序资产

* ***path **- String***** -应用程序实例下存储应用程序资源的位置的路径

**移** 动apporfers为个性化用例引入了一个新的内容同步处理程序，用于呈现目标内容。“mobileapporfers”处理程序知道如何呈现由内容作者创建的关联目标优惠。 mobileapporfers处理函数扩展了抽象页面更新处理函数，因此许多属性都是相似的。 mobileapporpers处理程序的详细信息具有以下属性。

mobileappsoffers处理函数扩展mobileappspages处理函数并添加以下属性：

* ***locationRoot - String***  —— 指定移动应用程序的位置
* ***includePageTypes —— 字符串*** -默认支持cq/personalization/components/teaserpage和cq/personalization/components/offerproxy
* ***选择器*** -字符串——应设置为tandt
* ***path —— 字符串***-活动品牌的路径

**mobileappconfig** mobileappconfig内容同步处理程序提供了一种将JSON数据注入MobileAppsConfig.json的方法。要注册提供者类，开发者将使用提供者的列表添加其MobileAppsInfoProvider类。 该处理函数将遍历MobileAppsInfoProviders的列表，并允许提供者将数据注入到生成的json文件中。 此处理函数支持的属性列表为：

* ***path **-**String*** -使用pge-type=app-instance的应用程序实例节点或扩展/libs/mobileapps/core/components/instance的RT的路径
* ***提供者*** `[]` -字符串——完全限定的MobileAppsInfoProviders的列表
* ***targetRootDirectory - String***  —— 将MobileAppsConfig.json文件写入的目录。
* **fileName - String**  —— 要将JSON写入的文件的可选名称，默认为MobileAppsConfig.json

可以为多个mobileappconfig处理函数配置一组唯一的提供程序，这些提供程序写入不同的JSON文件。

### 测试内容同步处理程序{#testing-content-sync-handlers}

**检查完整性清除缓** 存的步骤

* 清除缓存
* 运行处理程序（已更新缓存）
* 再次运行处理程序（不应更新缓存）

**调试步骤**

* 运行配置
* 在设备上导出配置或查看
* 如果渲染失败，请检查是否缺少&#x200B;*样式／资产/libs*，或检查到&#x200B;*样式／资产/libs*&#x200B;的错误路径

**记** 录通过OSGI记录器配置在包上启用ContentSync调试 `com.day.cq.contentsync` 日志记录这将允许您跟踪运行了哪些处理程序以及它们是否更新了缓存并报告了更新缓存。

## 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM为Adobe PhoneGap企业进行创作](/help/mobile/phonegap.md)
* [通过AEM为Adobe PhoneGap企业管理内容](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>要开始使用AEM Mobile应用程序开发，请单击[此处](/help/mobile/getting-started-aem-mobile.md)。

