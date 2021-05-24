---
title: ContextHub存储候选示例
seo-title: ContextHub存储候选示例
description: ContextHub提供了多个可在解决方案中使用的示例存储候选项
seo-description: ContextHub提供了多个可在解决方案中使用的示例存储候选项
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: d8d9a799-3e30-442a-843b-d4d7ba70c557
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# ContextHub存储候选项示例{#sample-contexthub-store-candidates}

ContextHub提供了多个可在解决方案中使用的示例存储候选项。 为每个示例提供了以下信息：

* 在何处查找源代码，以便您能够将其打开以用于学习目的。
* 如何配置从应用商店创建的商店。
* 存储数据的结构方式，以便您能够访问它。

>[!WARNING]
>
>示例存储候选项将作为参考配置提供，以帮助您为项目构建自己的专用配置，因此不应直接使用。

## aem.segmentation样本存储候选项{#aem-segmentation-sample-store-candidate}

存储已解析和未解析的ContextHub区段。 自动从ContextHub SegmentManager中检索区段。

### 源位置{#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### 基本实施{#base-implementation-segmentation}

aem.segmentation存储候选项扩展[`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)。

### 配置 {#configuration-segmentation}

创建aem.segmentation存储区时，您无需提供详细配置。 默认配置指定ContextHub区段定义的位置。

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## contexthub.geolocation示例存储候选项{#contexthub-geolocation-sample-store-candidate}

ContextHub.geolocation示例存储候选项使用Google Map获取和存储有关客户端位置的信息。

### 源位置{#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### 基本实施{#base-implementation-geolocation}

contexthub.geolocation存储候选项扩展[`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)。

### 配置 {#configuration-geolocation}

默认配置指定有关Google服务以及初始纬度和经度坐标的信息。

```xml
{
        "service": {
            "jsonp": false,
            "timeout": 1000,
            "ttl": 1800000,
            "secure": false,
            "host": "maps.googleapis.com",
            "port": 80,
            "path": "/maps/api/geocode/json"
        },

        "eventDeferring": 16,

        "html5coordinatesDiscoveryAPI": {
            "timeout": 30000,
            "ttl": 900000,
            "highAccuracy": false
        },

        "initialValues": {
            "latitude": 37.331375,
            "longitude": -121.893992
        }
    }
```

### 数据项{#data-items-geolocation}

存储使用与以下示例类似的数据树：

```xml
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>Chrome 50.x中引入的安全策略要求所有与地理位置相关的调用都必须通过安全连接进行。 因此，如果AEM也通过https运行，则AEM会强制将https用于地理位置API调用。 否则，使用http以符合同一源的策略。 有关Chrome中更改的更多详细信息，请参阅[此Google博客文章](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only)。

## contexthub.surferinfo示例存储候选项{#contexthub-surferinfo-sample-store-candidate}

存储有关当前客户端环境的信息，如设备、窗口、浏览器、日期和时间。

### 源位置{#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### 基本实施{#base-implementation-surferinfo}

contexthub.datetime存储候选项扩展[`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)。

### 配置 {#configuration-surferinfo}

默认配置继承自`ContextHub.Store.PersistedStore`。

### 数据项{#data-items-surferinfo}

使用此存储候选项的存储具有与以下示例类似的数据树：

```xml
{
   "display":{
      "resolution":{
         "width":1440,
         "height":900
      },
      "devicePixelRatio":1,
      "colorDepth":24,
      "nrOfColors":16777216,
      "pixelsPerInch":96,
      "orientation":{
         "mode":"landscape",
         "direction":"normal"
      }
   },
   "window":{
      "dimension":{
         "width":1395,
         "height":652
      },
      "percentageUsage":0.7
   },
   "browser":{
      "version":"39.0",
      "family":"Firefox",
      "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:39.0) Gecko/20100101 Firefox/39.0"
   },
   "device":{
      "category":"Desktop",
      "type":"Desktop",
      "model":"PC",
      "version":""
   },
   "isMobile":true,
   "os":{
      "name":"Mac OS X",
      "version":"10"
   },
   "year":2015,
   "month":7,
   "day":22,
   "hour":14,
   "minutes":1
}
```

## granite.emulators存储候选项示例{#granite-emulators-sample-store-candidate}

granite.emulators示例存储候选存储有关客户端设备的信息。

### 源位置{#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### 基本实施{#base-implementation-emulators}

contexthub.geolocation存储候选项扩展[`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)。

### 配置 {#configuration-emulators}

默认配置包括一个名为`defaultEmulators`的阵列，其中包含有关不同设备的信息。 创建商店时，请按照需要在Detail Configuration属性中提供不同的设备配置文件，其格式如下例所示：

```xml
{
   "defaultEmulators":[
        {
            "id": "iphone-6",
            "title": "iPhone 6",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 750,
            "height": 1334,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 2
        },
        {
            "id": "iphone-6-plus",
            "title": "iPhone 6 Plus",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        },
        {
            "id": "galaxy-s4",
            "title": "Samsung Galaxy S4",
            "type": "mobile",
            "platform": "Android",
            "platformVersion": "4.4.2 KitKat",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        }
    ]
}
```

### 数据项{#data-items-emulators}

存储数据树类似于以下示例：

```xml
{
   "devices":[
      {"id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
      },
      {"id":"ipad-3",
      "title":"iPad 3 / 4 / Air",
      "type":"tablet",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":1536,
      "height":2048,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"iphone-6",
      "title":"iPhone 6",
      "type":"mobile",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":750,
      "height":1334,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"galaxy-s4",
      "title":"Samsung Galaxy S4",
      "type":"mobile",
      "platform":"Android",
      "platformVersion":"4.4.2 KitKat",
      "width":1080,
      "height":1920,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":3
      }
   ],
   "currentDeviceId":"native",
   "orientations":[
      {"id":"landscape",
      "title":"Landscape"
      },
      {"id":"portrait",
       "title":"Portrait"
      }
   ],
   "currentDevice":{
      "id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
   }
}
```

## granite.profile存储候选项示例{#granite-profile-sample-store-candidate}

存储有关当前用户的信息。

### 源位置{#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### 基本实施{#base-implementation-profile}

contexthub.datetime存储候选项扩展[`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)。

### 配置 {#configuration-profile}

使用以下默认配置。 您不应更改此配置。

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"${contexthub:/store/profile/path}.infinity.json"
   },
   "initialValues":{"path":"/home/users/a/anonymous"}
}
```

### 数据项{#data-items-profile}

使用此存储候选项的存储具有与以下示例类似的数据树：

```xml
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
