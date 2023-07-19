---
title: 开箱即用的应用程序处理程序
seo-title: Out of the Box App Handlers
description: 按照本页中的说明，了解带AEM的Adobe PhoneGap Enterprise的现成处理程序。
seo-description: Follow this page to learn about the out-of-the-box handlers for Adobe PhoneGap Enterprise with AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 0%

---

# 开箱即用的应用程序处理程序{#out-of-the-box-app-handlers}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

请参阅以下有关开发内容同步处理程序的准则：

* 必须实施处理程序 *com.day.cq.contentsync.handler.ContentUpdateHandler* （直接或扩展具有的类）
* 处理程序可以扩展 *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 如果处理程序更新了ContentSync缓存，则只能报告true。 错误地报告true将允许AEM创建更新。
* 仅当内容实际更改时，处理程序才应更新缓存。 如果不需要白色，请不要写入缓存，并避免创建不必要的更新。

## 开箱即用的处理程序 {#out-of-the-box-handlers}

下面列出了现成的应用程序处理程序：

**mobileapppages** 渲染应用程序页面。

* ***类型 — 字符串*** - mobileapppages
* ***path — 字符串***  — 页面路径
* ***扩展 — 字符串***  — 应在请求中使用的扩展。 对于页面，这种情况几乎总是 *html*，但其他功能仍然可用。

* ***选择器 — 字符串***  — 可选的选择器，以点分隔。 常见示例包括 *触控* 用于呈现页面的移动设备版本。

* ***deep — 布尔值***  — 可选的布尔属性，用于确定是否也应包含子页面。 默认值为 *对。*

* ***includeImages — 布尔值***  — 可选的布尔属性，用于确定是否应包含图像。 默认值为 *true*.

   * 默认情况下，只考虑包含资源类型为foundation/components/image的图像组件。

* ***includeVideos — 布尔值***  — 可选的布尔属性确定是否应包含视频。 默认值为 *true*.

* ***includeModifiedPagesOnly — 布尔值***  — 如果为false或忽略，则渲染所有页面并检查渲染中的更新。 如果为true，则根据对页面lastModified的更改进行差值。
* ***+重写（节点）***
  ***- relativeParentPath — 字符串***  — 写入所有其他相对路径的路径。

>[!NOTE]
>
>受此处理程序影响的图像和视频组件的资源类型是通过配置 *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*MobilePagesUpdateHandler OSGi服务*.

**mobilepageassets** 收集应用程序页面资产。

**mobilecontentlisting** 列出ContentSync zip文件的内容。 设备上的客户端js使用此项来执行AEM应用程序所需的初始文件复制。

应将此处理程序添加到任何AEM Apps ContentSync配置中。

* ***类型 — 字符串 — mobilecontentlisting***
* ***路径***  — 字符串 — 保留为空，必须存在才能被视为有效的处理程序，但路径被推断为当前的ContentSync缓存。 此值将被忽略。
* ***targetRootDirectory* -**字符串 — 作为此处理程序内容更新的目标根添加到路径的前缀。
* ***订购 — 长* -**ContentSync执行此处理程序的顺序。 此数字应设置为高于所有其他处理程序，例如100。 它应在传统内容处理程序之后运行。

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

**mobilecontentpackageslisting** 列出给定应用程序中的AEM内容包以及向其发出更新请求的serverURL。 这用于设备上的客户端js请求内容更新

该处理程序应用于AEM App Shell ContentSync配置（具有pge-type=app-instance的节点）

* ***类型 — 字符串 — mobilecontentpackageslisting***
* ***路径&#x200B;**-**字符串***  — 应用程序Shell的路径（具有page-type=app-instance的节点）。
* ***targetRootDirectory — 字符串***  — 作为此处理程序内容更新的目标根添加到路径的前缀。
* ***订购 — 长* -**ContentSync执行此处理程序的顺序。 此数字应设置为高于所有其他处理程序，例如100。 它应在传统内容处理程序之后运行。

>[!NOTE]
>
>以下代码块不是准确的实施，应用作参考示例：

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

**widgetconfig** 包含一个更新的config.xml，它将通过命令中心所做的任何编辑与提供的config.xml合并。 如果未包含此处理程序，则通过管理界面更改的任何应用程序详细信息将不会包含在缓存中。

此处理程序应在AEM App Shell ContentSync配置（pge-type=的节点）上使用[app-instance])。

* ***类型 — 字符串* - **widgetconfig
* ***路径&#x200B;**-**字符串***  — 任何应用程序shell子节点的路径（pge-type=的节点）[app-instance])。
* ***targetRootDirectory — 字符串***  — 作为此处理程序内容更新的目标根添加到路径的前缀。
* ***targetIconDirectory — 字符串***  — 用于放置应用程序图标的目录

**mobileADBMobileConfigJSON** 如果配置了AMS cloudservice，请包含ADBMobileConfig.JSON文件。

在编译时使用此插件配置AMS插件以提供分析支持。

该处理程序应用于AEM App Shell ContentSync配置（具有pge-type=app-instance的节点）

* ***类型 — 字符串*** - mobileADBMobileConfigJSON
* ***path — 字符串***  — 应用程序shell的路径（具有pge-type=app-instance的节点或扩展/libs/mobileapps/core/components/instance的RT）
* ***targetRootDirectory — 字符串***  — 作为此处理程序内容更新的目标根添加到路径的前缀

**notificationsconfig** 提取设备上所需的通知配置。 这些属性提取自与应用程序关联的相应推送服务云服务配置。

将提取云服务jcr：content节点中的非AEM属性并将其添加到 **pge-notifications-config.json** 要包含在应用程序内容的www根目录中的JSON文件。

AEM属性是使用“cq”、“sling”或“jcr”进行命名空间的属性。 可以使用content-sync配置节点上的“excludeProperties”属性排除其他属性。

* ***类型 — 字符串*** - notificationsconfig
* ***excludeProperties — 字符串[]***  — 要排除的属性

**contentsyncconfigcontent** 从现有ContentSync配置收集内容。

* ***类型 — 字符串*** - contentsynconfigcontent
* ***path — 字符串***  — 指向以下项之一的路径：

   * 其他ContentSync配置
   * 到内容包（将使用其phonegap-exportTemplate属性来查找其ContentSync配置）
   * 移动资源（在该资源下可找到app-content，如果这些内容包的page-includeInBuild属性为true，则将使用phonegap-exportTemplate查找其ContentSync配置）

* ***autoCreateFirstUpdateBeforeImport — 布尔值***  — 如果为true，则创建初始 **更新** 如果已经不存在，则在导入之前的目标配置中

* ***autoFillBeforeImport — 布尔值***  — 如果为true，则在导入之前更新/填充目标配置
* ***configSuffix — 字符串***  — 一个字符串，可附加到app-content的“phonegap-exportTemplate”属性上指示的路径。 这可用于区分不同的导出模板。 例如，此属性可设置为 **“ — dev”** 以表明 *&quot;/../../../appconfig-dev&quot;* 应该使用(而不是 *&quot;/../../../appconfig&quot;*)。

**应用程序资产** 包含与应用程序实例关联的所有资产。 此处理程序将包括在指定路径下找到的任何资产，以及由应用程序实例的appAssetPath属性引用的任何资产。

* ***类型 — 字符串***  — 应用程序资产

* ***路径&#x200B;**-**字符串***  — 应用程序实例下存储应用程序资产的位置的路径

**mobileappoffers** 为个性化用例引入了一个新的内容同步处理程序，用于呈现目标内容。 “mobileappoffers”处理程序知道如何呈现由内容作者创建的关联目标选件。 mobileappoffers处理程序扩展了抽象页面更新处理程序，因此许多属性是相似的。 mobileappoffers处理程序的详细信息具有以下属性。

mobileappsoffers处理程序扩展mobileappspages处理程序并添加以下属性：

* ***locationRoot — 字符串***  — 指定移动应用程序的位置
* ***includePageTypes — 字符串***  — 默认为支持cq/personalization/components/teaserpage和cq/personalization/components/offerproxy
* ***选择器 — 字符串***  — 应设置为tandt
* ***path — 字符串*** — 营销活动品牌的路径

**mobileappconfig** mobileappconfig内容同步处理程序提供了一种将JSON数据插入MobileAppsConfig.json的方法。 要注册提供程序类，开发人员将使用提供程序列表添加其MobileAppsInfoProvider类。 该处理程序将对MobileAppsInfoProviders列表进行迭代，并允许提供程序将数据插入生成的json文件中。 此处理程序支持的属性列表包括：

* ***路径&#x200B;**-**字符串***  — 指向pge-type=app-instance的应用程序实例节点或扩展/libs/mobileapps/core/components/instance的RT的路径
* ***提供程序 — 字符串*** `[]`  — 完全限定的MobileAppsInfoProviders列表
* ***targetRootDirectory — 字符串***  — 将MobileAppsConfig.json文件写入到的目录。
* **文件名 — 字符串**  — 要将JSON写入到的文件的可选名称，默认为MobileAppsConfig.json

可能有多个mobileappconfig处理程序分别配置了写入不同JSON文件的唯一提供程序集。

### 测试内容同步处理程序 {#testing-content-sync-handlers}

**检查完整性的步骤** 清除缓存

* 清除缓存
* 运行处理程序（缓存已更新）
* 再次运行您的处理程序（不应更新缓存）

**调试步骤**

* 运行配置
* 在设备上导出配置或查看
* 如果渲染失败，则检查是否缺失 *样式/资产/库* 或检查是否存在错误的路径 *样式/资产/库*

**日志记录** 通过包上的OSGI记录器配置启用ContentSync调试日志记录 `com.day.cq.contentsync` 这将允许您跟踪哪些处理程序已运行，以及他们是否更新了缓存并报告更新了缓存。

## 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM为Adobe PhoneGap Enterprise创作](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>要开始使用AEM Mobile应用程序开发，请单击 [此处](/help/mobile/getting-started-aem-mobile.md).
