---
title: 开箱即用的应用程序处理程序
seo-title: Out of the Box App Handlers
description: 可查看本页以了解有关使用AEM的Adobe PhoneGap Enterprise的现成处理程序。
seo-description: Follow this page to learn about the out-of-the-box handlers for Adobe PhoneGap Enterprise with AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---

# 开箱即用的应用程序处理程序{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

请参阅以下有关开发内容同步处理程序的准则：

* 处理程序必须实施 *com.day.cq.contentsync.handler.ContentUpdateHandler* （直接或扩展的类）
* 处理程序可以扩展 *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 仅当处理程序更新了ContentSync缓存时，它们必须报告true。 错误报告为true会允许AEM创建更新。
* 仅当内容实际发生更改时，处理程序才应更新缓存。 如果不需要白色，请勿写入缓存，并避免不必要的更新创建。

## 开箱即用处理程序 {#out-of-the-box-handlers}

下面列出了现成的应用程序处理程序：

**mobileappages** 呈现应用程序页面。

* ***类型 — 字符串*** - mobileappages
* ***路径 — 字符串***  — 页面路径
* ***扩展 — 字符串***  — 请求中应使用的扩展。 对于页面，这几乎总是 *html*&#x200B;但其他仍有可能。

* ***选择器 — 字符串***  — 可选选择器，以圆点分隔。 常见示例包括 *触控* ，用于渲染页面的移动版本。

* ***deep — 布尔值***  — 确定是否应包含子页面的可选布尔属性。 默认值为 *真的。*

* ***includeImages — 布尔值***  — 确定是否应包含图像的可选布尔属性。 默认值为 *true*.

   * 默认情况下，仅考虑包含资源类型为foundation/components/image的图像组件。

* ***includeVideos — 布尔值***  — 可选布尔属性，用于确定是否应包含视频。 默认值为 *true*.

* ***includeModifiedPagesOnly — 布尔值***  — 如果为false或忽略，则渲染所有页面并检查渲染中的更新。 如果为true，则根据对页面lastModified的更改而有所不同。
* ***+重写（节点）***
   ***- relativeParentPath — 字符串***  — 相对于写入所有其他路径的路径。

>[!NOTE]
>
>通过配置 *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*MobilePagesUpdateHandler OSGi服务*.

**mobilepageassets** 收集应用程序页面资产。

**mobilecontentlisting** 列出ContentSync zip的内容。 设备上的客户端js会使用此功能来执行AEM应用程序所需的初始文件副本。

此处理程序应添加到任何AEM应用程序ContentSync配置中。

* ***type - String - mobilecontentlisting***
* ***路径***  — 字符串 — 保持为空，必须显示为有效的处理程序，但路径一定为当前ContentSync缓存。 此值将被忽略。
* ***targetRootDirectory* -**字符串 — 作为此处理程序的内容更新目标根添加到路径的前缀。
* ***顺序 — 长* -**ContentSync执行此处理程序的顺序。 此数字应设置为高于所有其他处理程序（如100）。 它应在传统内容处理程序之后运行。

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

**mobilecontentpackagelisting** 列出给定应用程序中的AEM内容包以及要向其发出更新请求的serverURL。 设备上的客户端js使用此参数来请求内容更新

处理程序应用于AEM App Shell ContentSync配置（具有pge-type=app-instance的节点）

* ***type - String - mobilecontentpackageslisting***
* ***路径&#x200B;**-**字符串***  — 应用程序Shell的路径（具有pge-type=app-instance的节点）。
* ***targetRootDirectory — 字符串***  — 作为此处理程序内容更新的目标根添加到路径的前缀。
* ***顺序 — 长* -**ContentSync执行此处理程序的顺序。 此数字应设置为高于所有其他处理程序（如100）。 它应在传统内容处理程序之后运行。

>[!NOTE]
>
>以下代码块不是确切的实施，应该用作引用示例：

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

**widgetconfig** 包含更新的config.xml，可将通过命令中心所做的任何编辑与提供的config.xml合并。 如果此处理程序未包含通过管理界面更改的任何应用程序详细信息，则缓存中将不会包含这些详细信息。

此处理程序应用于AEM App Shell ContentSync配置（具有pge-type=的节点）[应用程序实例])。

* ***类型 — 字符串* - **widgetconfig
* ***路径&#x200B;**-**字符串***  — 任何应用程序Shell子节点的路径（具有pge-type=的节点）[应用程序实例])。
* ***targetRootDirectory — 字符串***  — 作为此处理程序内容更新的目标根添加到路径的前缀。
* ***targetIconDirectory — 字符串***  — 用于放置应用程序图标的目录

**mobileADBMobileConfigJSON** 如果配置了AMS云服务，请包含ADBMobileConfig.JSON文件。

在编译时使用此插件来配置AMS插件以支持分析。

处理程序应用于AEM App Shell ContentSync配置（具有pge-type=app-instance的节点）

* ***类型 — 字符串*** - mobileADBMobileConfigJSON
* ***路径 — 字符串***  — 应用程序Shell的路径（具有pge-type=app-instance的节点或扩展/libs/mobileapps/core/components/instance的RT）
* ***targetRootDirectory — 字符串***  — 作为此处理程序的内容更新的目标根添加到路径的前缀

**notificationsconfig** 提取设备上所需的通知配置。 这些属性是从与应用程序关联的相应推送服务云服务配置中提取的。

将提取云服务的jcr:content节点中的非AEM属性，并将其添加到 **pge-notifications-config.json** JSON文件，以包含在应用程序内容的www根中。

AEM属性是指具有“cq”、“sling”或“jcr”命名空间的属性。 可以使用content-sync配置节点上的“excludeProperties”属性排除其他属性。

* ***类型 — 字符串*** - notificationsconfig
* ***excludeProperties — 字符串[]***  — 要排除的属性

**contentsyncconfigcontent** 从现有ContentSync配置收集内容。

* ***类型 — 字符串*** - contentsyncconfigcontent
* ***路径 — 字符串***  — 路径之一：

   * 另一个ContentSync配置
   * 到内容包（将使用其phonegap-exportTemplate属性查找其ContentSync配置）
   * 移动资源（该资源下将找到app-content的，如果这些内容包具有pge-includeInBuild属性（为true），则将使用phonegap-exportTemplate查找其ContentSync配置）

* ***autoCreateFirstUpdateBeforeImport — 布尔值***  — 如果为true，则创建初始 **更新** （如果不存在）

* ***autoFillBeforeImport — 布尔值***  — 如果为true，则在导入之前更新/填充target配置
* ***configSuffix — 字符串***  — 一个字符串，附加到app-content的“phonegap-exportTemplate”属性中指示的路径。 这可用于区分不同的导出模板。 例如，此属性可设置为 **&quot;-dev&quot;** 表示 *&quot;/../../../appconfig-dev&quot;* 的 *&quot;/../../../appconfig&quot;*)。

**app-assets** 包括与应用程序实例关联的所有资产。 此处理程序将包含在指定路径下找到的任何资产，以及应用程序实例的appAssetPath属性引用的任何资产。

* ***类型 — 字符串***  — 应用程序资产

* ***路径&#x200B;**-**字符串***  — 应用程序实例下存储应用程序资产的位置的路径

**mobileappoffers** 为个性化用例引入了新的内容同步处理程序，以渲染目标内容。 “mobileappoffers”处理程序知道如何渲染由内容作者创建的关联目标选件。 mobileappoffers处理程序扩展抽象页面更新处理程序，因此许多属性都相似。 mobileappopers处理程序的详细信息具有以下属性。

mobileappsoffers处理程序扩展mobileappspages处理程序并添加以下属性：

* ***locationRoot — 字符串***  — 指定移动应用程序的位置
* ***includePageTypes — 字符串***  — 默认支持cq/personalization/components/teaserpage和cq/personalization/components/offerproxy
* ***选择器 — 字符串***  — 应设置为tandt
* ***路径 — 字符串*** — 营销活动品牌的路径

**mobileappconfig** mobileappconfig内容同步处理程序提供了一种将JSON数据注入MobileAppsConfig.json的方法。 要注册提供程序类，开发人员将在提供程序列表中添加其MobileAppsInfoProvider类。 处理程序将迭代到MobileAppsInfoProviders列表上，并允许提供程序将数据注入到生成的json文件中。 此处理程序支持的属性列表包括：

* ***路径&#x200B;**-**字符串***  — 使用pge-type=app-instance的应用程序实例节点或扩展/libs/mobileapps/core/components/instance的RT的路径
* ***提供程序 — 字符串*** `[]`  — 完全符合条件的MobileAppsInfoProviders列表
* ***targetRootDirectory — 字符串***  — 将MobileAppsConfig.json文件写入的目录。
* **fileName — 字符串**  — 将JSON写入的文件的可选名称，默认为MobileAppsConfig.json

可以为多个mobileappconfig处理程序分别配置一组唯一的提供程序，这些提供程序写入不同的JSON文件。

### 测试内容同步处理程序 {#testing-content-sync-handlers}

**检查完整性的步骤** 清除缓存

* 清除缓存
* 运行处理程序（缓存已更新）
* 再次运行处理程序（不应更新缓存）

**调试步骤**

* 运行配置
* 导出配置或在设备上查看
* 如果渲染失败检查是否缺失 *样式/资产/lib* 或检查到的错误路径 *样式/资产/lib*

**记录** 通过包上的OSGI日志记录器配置启用ContentSync调试日志记录 `com.day.cq.contentsync` 这将允许您跟踪运行的处理程序以及它们是否更新了缓存并报告了更新缓存。

## 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM创作Adobe PhoneGap企业版](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>要开始开发AEM Mobile应用程序，请单击 [此处](/help/mobile/getting-started-aem-mobile.md).
