---
title: 配置ContextHub
seo-title: 配置ContextHub
description: 了解如何配置Context Hub。
seo-description: 了解如何配置Context Hub。
uuid: f2988bb9-6878-42a2-bb51-c3f8683248c5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 780d1a2d-38f1-4115-a9bd-f466aa3774dd
translation-type: tm+mt
source-git-commit: e37ff1c9e657c580c607f2656adca01a2b39f81f

---


# 配置ContextHub {#configuring-contexthub}

ContextHub是一个用于存储、操作和呈现上下文数据的框架。 有关ContextHub的更多详细信息，请参阅开发 [人员文档](/help/sites-developing/contexthub.md)。 ContextHub替换 [了触屏UI中的Client Context](/help/sites-administering/client-context.md) 。

配置 [](/help/sites-developing/contexthub.md) ContextHub工具栏以控制它是否显示在“预览”模式中、创建ContextHub存储区以及使用触屏优化UI添加UI模块。

## 禁用ContextHub {#disabling-contexthub}

默认情况下，在AEM安装中启用ContextHub。 可以禁用ContextHub以阻止它加载js/css和初始化。 禁用ContextHub有两种选项：

* 编辑ContextHub的配置并选中禁用ContextHub **选项**

   1. 在边栏中，单击或点按工 **具>站点> ContextHub**
   1. 单击或点按默认的配 **置容器**
   1. 选择ContextHub配 **置** ，然后单击或点按编辑 **选定元素**
   1. 单击或点按 **禁用ContextHub** ，然后单击或点按保 **存**

或

* 使用CRXDE Lite将属性设 `disabled` 置 **为** true `/libs/settings/cloudsettings`

>[!NOTE]
>
>[由于AEM 6.4中的存储库重组，](/help/sites-deploying/repository-restructuring.md) contextHub配置的位置从更改 `/etc/cloudsettings` 为：
>
> * `/libs/settings/cloudsettings`
> * `/conf/global/settings/cloudsettings`
> * `/conf/<tenant>/settings/cloudsettings`


## 显示和隐藏ContextHub UI {#showing-and-hiding-the-contexthub-ui}

配置Adobe Granite ContextHub OSGi服务，以在页面上显示或隐 [藏ContextHub](/help/sites-authoring/ch-previewing.md) UI。 此服务的PID是 `com.adobe.granite.contexthub.impl.ContextHubImpl.`

要配置服务，您可以使用 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ，或在存储库 [中使用JCR节点](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository):

* **** Web控制台：要显示UI，请选择显示UI属性。 要隐藏UI，请清除隐藏UI属性。
* **** JCR节点：要显示UI，请将布尔属 `com.adobe.granite.contexthub.show_ui` 性设置为 `true`。 要隐藏UI，请将属性设置为 `false`。

显示ContextHub UI时，它仅显示在AEM作者实例的页面上。 UI不显示在发布实例的页面上。

## 添加ContextHub UI模式和模块 {#adding-contexthub-ui-modes-and-modules}

在“预览”模式下配置ContextHub工具栏中显示的UI模式和模块：

* UI模式：相关模块组
* 模块：用于显示来自商店的上下文数据并使作者能够操作上下文的构件

UI模式在工具栏左侧显示为一系列图标。 选择后，UI模式的模块将显示在右侧。

![chlimage_1-319](assets/chlimage_1-319.png)

图标是 [Coral UI图标库中的引用](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons)。

### 添加UI模式 {#adding-a-ui-mode}

添加UI模式以组相关的ContextHub模块。 在创建UI模式时，您提供标题和图标，它们显示在ContextHub工具栏中。

1. 在Experience manager边栏上，单击或点按工具>站点> Context Hub。
1. 单击或点按默认的配置容器。
1. 单击或点按Context Hub配置。
1. 单击或点按创建按钮，然后单击或点按Context Hub UI模式。

   ![chlimage_1-320](assets/chlimage_1-320.png)

1. 为以下属性提供值：

   * UI模式标题：标识UI模式的标题
   * 模式图标：例如 [](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) ，要使用的Coral UI图标的选择器 `coral-Icon--user`
   * 已启用：选择此选项可在ContextHub工具栏中显示UI模式

1. 单击或点按保存。

### 添加UI模块 {#adding-a-ui-module}

将ContextHub UI模块添加到UI模式，以便它显示在ContextHub工具栏中以预览页面内容。 添加UI模块时，您将创建向ContextHub注册的模块类型实例。 要添加UI模块，您必须知道关联模块类型的名称。

AEM提供基本UI模块类型以及多个示例UI模块类型，您可以在这些类型中作为UI模块的基础。 下表对每个选项进行了简要说明。 有关开发自定义UI模块的信息，请参 [阅创建ContextHub UI模块](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)。

UI模块属性包括详细信息配置，您可以在其中为模块特定的属性提供值。 您以JSON格式提供详细配置。 表中的“模块类型”列提供了指向每个UI模块类型所需的JSON代码信息的链接。

| 模块类型 | 描述 | 存储 |
|---|---|---|
| [contexthub.base](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) | 通用UI模块类型 | 在UI模块属性中配置 |
| [contexthub.browserinfo](/help/sites-developing/ch-samplemodules.md#contexthub-browserinfo-ui-module-type) | 显示有关浏览器的信息 | surferinfo |
| [contexthub.datetime](/help/sites-developing/ch-samplemodules.md#contexthub-datetime-ui-module-type) | 显示日期和时间信息 | datetime |
| [contexthub.device](/help/sites-developing/ch-samplemodules.md#contexthub-device-ui-module-type) | 显示客户端设备 | 模拟器 |
| [contexthub.location](/help/sites-developing/ch-samplemodules.md#contexthub-location-ui-module-type) | 显示客户端的经度和纬度，以及地图上的位置。 允许您更改位置。 | 地理位置 |
| [contexthub.screen-orientation](/help/sites-developing/ch-samplemodules.md#contexthub-screen-orientation-ui-module-type) | 显示设备的屏幕方向（横向或纵向） | 模拟器 |
| [contexthub.tagcloud](/help/sites-developing/ch-samplemodules.md#contexthub-tagcloud-ui-module-type) | 显示有关页面标记的统计信息 | tagcloud |
| [granite.profile](/help/sites-developing/ch-samplemodules.md#granite-profile-ui-module-type) | 显示当前用户的配置文件信息，包括authorizableID、displayName和familyName。 可以更改displayName和familyName的值。 | 配置文件 |

1. 在Experience manager边栏上，单击或点按工具>站点> ContextHub。
1. 单击或点按要向其添加UI模块的配置容器。
1. 单击或键入要向其添加UI模块的ContextHub配置。
1. 单击或点按要添加UI模块的UI模式。
1. 单击或点按创建按钮，然后单击或点按ContextHub UI模块（通用）。

   ![chlimage_1-321](assets/chlimage_1-321.png)

1. 为以下属性提供值：

   * UI模块标题：标识UI模块的标题
   * 模块类型：模块类型
   * 已启用：选择此项可在ContextHub工具栏中显示UI模块

1. （可选）要覆盖默认的存储配置，请输入JSON对象以配置UI模块。
1. 单击或点按保存。

## 创建ContextHub存储 {#creating-a-contexthub-store}

创建Context Hub存储库以保留用户数据并根据需要访问数据。 ContextHub存储基于注册的存储候选。 创建商店时，您需要注册商店候选者的storeType值。 (请参阅 [创建自定义商店候选](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)。)

### 详细的存储配置 {#detailed-store-configuration}

配置存储时，Detail Configuration属性允许您为特定于存储的属性提供值。 该值基于存储 `config` 器函数的参 `init` 数。 因此，是否需要提供此值以及值的格式取决于存储。

“详细配置”属性的值是JSON格 `config` 式的对象。

### 样例商店候选 {#sample-store-candidates}

AEM提供了以下样例存储候选，您可以基于这些候选存储。

| 存储类型 | 描述 |
|---|---|
| [aem.segmentation](/help/sites-developing/ch-samplestores.md#aem-segmentation-sample-store-candidate) | 存储已解析和未解析的ContextHub区段。 自动从ContextHub SegmentManager检索区段 |
| [aem.resolvedsegms](/help/sites-developing/ch-samplestores.md#aem-resolvedsegments-sample-store-candidate) | 存储当前解析的区段。 监听ContextHub SegmentManager服务以自动更新商店 |
| [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) | 存储浏览器位置的经度和纬度。 |
| [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) | 存储浏览器位置的当前日期、时间和季节 |
| [granite.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) | 为多个设备定义属性和功能，并检测当前客户端设备 |
| [contexthub.generic-jsonp](/help/sites-developing/ch-samplestores.md#contexthub-generic-jsonp-sample-store-candidate) | 从JSONP服务检索和存储数据 |
| [granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) | 存储当前用户的配置文件数据 |
| [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) | 存储有关客户端的信息，如设备信息、浏览器类型和窗口方向 |
| [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) | 存储页面标记和标记计数 |

1. 在Experience manager边栏上，单击或点按工具>站点> ContextHub。
1. 单击或点按默认配置容器。
1. 单击或点按Contexthub配置
1. 要添加商店，请单击或点按创建图标，然后单击或点按ContexHub商店配置。

   ![chlimage_1-322](assets/chlimage_1-322.png)

1. 为基本配置属性提供值，然后单击或点按下一步：

   * **** 配置标题：标识商店的标题
   * **** 商店类型：作为存储基础的存储候选项的storeType属性的值
   * **** 必需：选择
   * **** 已启用：选择以启用商店

1. （可选）要覆盖默认的存储配置，请在“详细配置(JSON)”框中输入JSON对象。
1. 单击或点按保存。

## 示例：使用JSONP服务 {#example-using-a-jsonp-service}

此示例说明如何配置存储并在UI模块中显示数据。 在此示例中，jsontest.com站点的MD5服务用作存储的数据源。 该服务返回给定字符串的MD5哈希代码，JSON格式。

配置contexthub.generic-jsonp存储，以便它存储服务调用的数据 `https://md5.jsontest.com/?text=%22text%20to%20md5%22`。 服务返回在UI模块中显示的以下数据：

```xml
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### 创建contexthub.generic-jsonp商店 {#creating-a-contexthub-generic-jsonp-store}

contexthub.generic-jsonp范例存储候选项允许您从JSONP服务或返回JSON数据的Web服务检索数据。 对于此存储候选项，请使用存储配置提供有关要使用的JSONP服务的详细信息。

Javascript [类的init函数](/help/sites-developing/contexthub-api.md#init-name-config) 定义一个对象，该对 `ContextHub.Store.JSONPStore``config` 象初始化此存储候选。 该对 `config` 象包含一 `service` 个对象，其中包含有关JSONP服务的详细信息。 要配置存储，您需要将 `service` JSON格式的对象作为“Detail Configuration”属性的值。

要保存jsontest.com站点的MD5服务中的数据，请使用以下属性 [创建ContextHub Store](/help/sites-administering/contexthub-config.md#creating-a-contexthub-store) 中的步骤：

* **** 配置标题：md5
* **** 商店类型：contexthub.generic-jsonp
* **** 必需：选择
* **** 已启用：选择
* **详细配置 (JSON):**

   ```xml
   {
    "service": {
    "jsonp": false,
    "timeout": 1000,
    "ttl": 1800000,
    "secure": false,
    "host": "md5.jsontest.com",
    "port": 80,
    "params":{
    "text":"text to md5"
        }
      }
    }
   ```

### 为md5数据添加UI模块 {#adding-a-ui-module-for-the-md-data}

将UI模块添加到ContextHub工具栏以显示存储在示例md5商店中的数据。 在此示例中，contexthub.base模块用于生成以下UI模块：

![chlimage_1-323](assets/chlimage_1-323.png)

使用添加UI模 [块中的步骤](/help/sites-administering/contexthub-config.md#adding-a-ui-module) ，将UI模块添加到现有UI模式，如示例Perona UI模式。 对于UI模块，请使用以下属性值：

* **** UI模块标题：MD5
* **** 模块类型：contexthub.base
* **详细配置 (JSON):**

   ```xml
   {
    "icon": "coral-Icon--data",
    "title": "MD5 Converstion",
    "storeMapping": { "md5": "md5" },
    "template": "<p> {{md5.original}}</p>;
                 <p>{{md5.md5}}</p>"
   }
   ```

## 调试ContextHub {#debugging-contexthub}

可以启用ContextHub的调试模式以允许进行疑难解答。 可通过ContextHub配置或通过CRXDE启用调试模式。

### 通过配置 {#via-the-configuration}

编辑ContextHub的配置并选中“调试”选 **项**

1. 在边栏中，单击或点按工 **具>站点> ContextHub**
1. 单击或点按默认的配 **置容器**
1. 选择ContextHub配 **置** ，然后单击或点按编辑 **选定元素**
1. 单击或点按调 **试** ，然后单击或点按保 **存**

### 通过CRXDE {#via-crxde}

使用CRXDE lite将属性设置 `debug` 为 **true** :

* `/conf/global/settings/cloudsettings` 或
* `/conf/<tenant>/settings/cloudsettings`

>[!NOTE]
>
>对于仍位于其旧版路径下的ContextHub配置，设置位置 `debug property` 为 `/libs/settings/cloudsettings/legacy/contexthub`。

### 静默模式 {#silent-mode}

“静默”模式禁止所有调试信息。 与常规调试选项不同，静默模式是全局设置，它优先于ContextHub配置级别上的任何调试设置。

这对于您的发布实例很有用，因为您根本不需要任何调试信息。 由于它是全局设置，因此它通过OSGi启用。

1. 打开 **Adobe Experience Manager Web Console配置** ，网址为 `http://<host>:<port>/system/console/configMgr`
1. 搜索 **Adobe Granite contextHub**
1. 单击配置 **Adobe Granite contextHub** ，以编辑其属性
1. 选中“静默模 **式”选项** ，然后单击“保 **存”**

## 升级后恢复ContextHub配置 {#recovering-contexthub-configurations-after-upgrading}

执行 [AEM升级后](/help/sites-deploying/upgrade.md) ,ContextHub配置将备份并存储在安全位置。 在升级过程中，将安装默认的ContextHub配置，替换现有配置。 需要备份才能保留您所做的任何更改或添加内容。

ContextHub配置存储在以下节点名 `contexthub` 称的文件夹中：

* `/conf/global/settings/cloudsettings`
* `/conf/<tenant>/settings/cloudsettings`

升级后，备份存储在名为： `contexthub`

`/conf/global/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx` 或
`/conf/<tenant>/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx`

节 `yyyymmdd` 点名称的部分是执行升级的日期。

要恢复ContextHub配置，请使用CRXDE lite将表示您的存储、UI模式和UI模块的节点从节点下复制到 `default-pre-upgrade_yyyymmdd_xxxxxx` 以下节点：

* `/conf/global/settings/cloudsettings` 或
* `/conf/<tenant>/settings/cloudsettings`