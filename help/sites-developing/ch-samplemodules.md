---
title: 示例ContextHub UI模块类型
seo-title: Sample ContextHub UI Module Types
description: ContextHub提供了几个可在解决方案中使用的示例UI模块
seo-description: ContextHub provides several sample UI modules that you can use in your solutions
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: df28180f-7af4-437d-8e91-bfd305f73113
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 0%

---

# 示例ContextHub UI模块类型 {#sample-contexthub-ui-module-types}

ContextHub提供了几个可在解决方案中使用的示例UI模块。 提供了以下信息：

* UI模块的主要功能。
* 在何处查找源代码，以便可以打开它进行学习。
* 如何配置UI模块。

有关将UI模块添加到ContextHub的信息，请参阅 [添加UI模块](ch-configuring.md#adding-a-ui-module). 有关开发UI模块的信息，请参阅 [创建ContextHub UI模块类型](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

## contexthub.base UI模块类型 {#contexthub-base-ui-module-type}

contexthub.base UI模块类型是所有其他UI模块类型的基类型。 因此，它提供了用于呈现存储数据的通用功能。

可以使用以下功能：

* **标题和图标：** 指定UI模块的标题和一个图标。 可以使用URL或Coral UI图标库引用该图标。
* **存储数据：** 标识要从中检索数据的一个或多个存储。
* **内容：** 指定UI模块中显示的内容，该内容显示在ContextHub工具栏中。
* **弹出框内容：** 指定单击或点按UI模块时弹出框中显示的内容。
* **全屏模式：** 控制是否允许全屏模式。

源代码位于/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js。

### 配置 {#configuration}

使用JSON格式的JavaScript对象配置contexthub.base UI模块。 包括以下任意属性以配置UI模块功能：

* **图像：** 显示为图标的图像的URL。
* **图标：** 的名称 [Coral UI图标](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) 类。 如果同时为图标和图像属性指定值，则会使用图像。

* **标题：** UI模块的标题。 当指针悬停在UI模块图标上时，将显示标题。
* **全屏：** 一个布尔值，指示UI模块是否支持全屏模式。 使用 `true` 支持全屏和 `false` 以防止使用全屏模式。

* **模板：** A [Handlebars](https://handlebarsjs.com/) 指定要在ContextHub工具栏中渲染的内容的模板。 最多使用两个 `<p>` 标记之间。

* **storeMapping：** 密钥/存储映射。 使用手柄栏模板中的键访问关联的ContextHub存储数据。
* **列表：** 在单击UI模块时作为弹出框中的列表显示的项目数组。 如果包含此项目，请不要包含poverTemplate。 该值是一个包含以下键的对象数组：

   * 标题：为此项目显示的文本
   * 图像： （可选）应在左侧显示的图像的URL
   * 图标： （可选）应在左侧显示的CUI图标类；如果指定了图像，则忽略此类别
   * selected： （可选）一个布尔值，它指定此项目是否应显示为已选中（true=已选中）。 默认情况下，选定的项目使用粗体字体显示。 使用 `listType` 属性以配置其他外观（见下文）。

* **listType：** 用于弹出框列表项的样式。 使用以下值之一：

   * 复选标记
   * 复选框
   * 无线电

* **poverTemplate：** 一个Handlebars模板，它指定在单击UI模块时要在弹出框中渲染的内容。 如果您包含此项目，请不要包含 `list` 个项目。

### 示例 {#example}

以下示例将contexthub.base UI模块配置为显示来自 [contexthub.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) 商店。 此 `template` 项目演示了如何使用键 `storeMapping` 项目已建立。

```xml
{
   "icon": "coral-Icon--move",
    "title": "Screen Resolution",
    "storeMapping": {
      "emulator": "emulators"
    },
    "template": "<p>{{{ i18n \"Resolution\"}}}</p><p>{{{emulator.currentDevice.width}}} x {{{emulator.currentDevice.height}}}</p>"
}
```

![chlimage_1-76](assets/chlimage_1-76a.png)

## contexthub.browserinfo UI模块类型 {#contexthub-browserinfo-ui-module-type}

contexthub.browserinfo UI模块显示有关客户端Web浏览器和操作系统的信息。 信息是从surferinfo商店获得的，根据 [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) 商店候选者。

![chlimage_1-77](assets/chlimage_1-77a.png)

UI模块的源代码位于/libs/granite/contexthub/components/modules/browserinfo。 尽管contexthub.browserinfo扩展了contexthub.base UI模块，但它不会覆盖或提供其他函数。 该实施提供了用于呈现浏览器信息的默认配置。

### 配置 {#configuration-1}

contexthub.browserinfo UI模块的实例不需要详细信息配置的值。 以下JSON文本表示模块的默认配置。

```xml
{
   "icon":"coral-Icon--globe",
   "title":"Browser/OS Information",
   "storeMapping":{"surferinfo":"surferinfo"},
   "template":"<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p><p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>"
}
```

## contexthub.datetime UI模块类型 {#contexthub-datetime-ui-module-type}

contexthub.datetime UI模块显示存储在名为datetime的存储区中的日期和时间，该存储区基于 [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) 商店候选者。

![chlimage_1-78](assets/chlimage_1-78a.png)

模块提供了一个弹出窗体，通过该窗体可以更改存储中的日期和时间。

contexthub.datetime UI模块的源位于/libs/granite/contexthub/components/modules/datetime。

### 配置 {#configuration-2}

Contexthub.datetime UI模块的实例不需要详细信息配置的值。 以下JSON文本表示模块的默认配置。

```xml
{
   "icon":"coral-Icon--clock",
   "title":"DATE&TIME",
   "clickable":true,
   "storeMapping":{"d":"datetime"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Date&Time\"}}</p><p class=\"contexthub-module-line2\">{{d.formatted.locale.date}} {{d.formatted.locale.time}}</p>",
   "popoverTemplate":"<div class=\"datetime center\"><div class=\"coral-DatePicker-calendar\" data-init=\"datepicker\"><input class=\"coral-Textfield\" type=\"datetime\" value=\"{{d.formatted.iso}}\"><button class=\"coral-Button coral-Button--secondary coral-Button--square\" title=\"{{i18n \"Datetime picker\"}}\"><i class=\"coral-Icon coral-Icon--calendar coral-Icon--sizeS\"></i></button></div></div>"
}
```

## contexthub.location UI模块类型 {#contexthub-location-ui-module-type}

contexthub.location UI模块显示客户端的经度和纬度。 该模块提供了一个弹出窗口，用于显示Google地图，单击该地图可更改当前位置。 模块从名为geolocation的ContextHub存储中获取信息，该存储基于 [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) 商店候选者。

![chlimage_1-80](assets/chlimage_1-80a.png)

UI模块的源位于/etc/cloudsettings/default/contexthub/geolocation。

### 配置 {#configuration-4}

Contexthub.location UI模块的实例不需要详细信息配置的值。 以下JSON文本表示模块的默认配置。

```xml
{
 "icon":"coral-Icon--compass",
 "title":"Location",
 "clickable":true,
 "editable":{"key":"/geolocation","disabled":[],"hidden":["/geolocation/generatedThumbnail","/geolocation/city","/geolocation/country"]},
 "fullscreen":true,
 "storeMapping":{"g":"geolocation"},
 "template":"<p>{{i18n \"Location\"}}</p><p>{{g.address.postalCode}} {{g.address.city}}{{#if g.address.city}}{{#if g.address.region}},{{/if}}{{/if}} {{g.address.region}}</p>",
 "list":[
  {"title":"Basel, Switzerland",
  "data":{"longitude":7.58929,"latitude":47.554746,"city":"Basel","country":"Switzerland"}},
  {"title":"Melbourne, Australia",
  "data":{"longitude":144.96328,"latitude":-37.814107,"city":"Melbourne","country":"Australia"}},
  {"title":"Beijing, China",
  "data":{"longitude":116.407526,"latitude":39.90403,"city":"Beijing","country":"China"}},
  {"title":"New York, NY, USA",
  "data":{"longitude":-74.005973,"latitude":40.714353,"city":"New York","country":"United States"}},
  {"title":"Paris, France",
  "data":{"longitude":2.352222,"latitude":48.856614,"city":"Paris","country":"France"}},
  {"title":"Rio de Janeiro, Brazil",
  "data":{"longitude":-43.20071,"latitude":-22.913395,"city":"Rio","country":"Brazil"}},
  {"title":"San Jose, CA, USA",
  "data":{"longitude":-121.894955,"latitude":37.339386,"city":"San Jose","country":"United States"}},
  {"title":"Tokyo, Japan",
  "data":{"longitude":139.691706,"latitude":35.689487,"city":"Shinjuku","country":"Japan"}}
 ],
 "listType":"checkmark"
}
```

## contexthub.screen-orientation UI模块类型 {#contexthub-screen-orientation-ui-module-type}

contexthub.screen-orientation UI模块显示客户端的当前屏幕方向。 尽管默认情况下处于禁用状态，但模块会提供一个弹出窗口，允许您选择方向。 模块从名为emulator的ContextHub存储中获取信息，该存储基于 [granite.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) 商店候选者。

![chlimage_1-81](assets/chlimage_1-81a.png)

UI模块的源位于/libs/granite/contexthub/components/modules/screen-orientation。

### 配置 {#configuration-5}

contexthub.screen-orientation UI模块的实例不需要“详细信息配置”的值。 以下JSON文本表示模块的默认配置。 请注意 `clickable` 属性为 `false` 默认情况下。 如果您覆盖要设置的默认配置 `clickable` 到 `true`，单击模块将显示一个弹出窗口，您可以在其中选择方向。

```xml
{
   "icon":"coral-Icon--rotateRight",
   "title":"Screen Orientation",
   "clickable":false,
   "storeMapping":{"emulator":"emulators"},
   "template":"<p>{{{ i18n \"Screen Orientation\" }}}</p><p>{{{ emulator.currentDevice.orientation }}}",
   "listReference":"/emulators/orientations",
   "listType":"checkmark"
}
```

## contexthub.tagcloud UI模块类型 {#contexthub-tagcloud-ui-module-type}

contexthub.tagcloud UI模块显示有关标记的信息。 在工具栏上，UI模块显示标记数量。 弹出窗口将显示一个tagcloud和一个用于添加新标记的文本框。 UI模块从名为tagcloud且基于 [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) 商店候选者。

![chlimage_1-82](assets/chlimage_1-82a.png)

UI模块的源位于/libs/granite/contexthub/components/modules/tagcloud。

### 配置 {#configuration-6}

Contexthub.tagcloud UI模块的实例不需要详细信息配置的值。 以下JSON文本表示模块的默认配置。

```xml
{
   "icon":"coral-Icon--tag",
   "title":"TagCloud",
   "clickable":true,
   "storeMapping":{"t":"tagcloud"},
   "maxTags":20,
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"TagCloud\"}}</p><p class=\"contexthub-module-line2\">{{stats.total}} {{i18n \"Tags\"}}</p>",
   "popoverTemplate":"<div class=\"contexthub-popover-content center\"><p class=\"stats\">{{stats.total}} {{i18n \"Tags\"}} | {{stats.hits}} {{i18n \"Hits\"}} | {{i18n \"Last tag\"}}: {{#if stats.recent}}{{stats.recent}}{{else}}{{i18n \"Unknown\"}}{{/if}}</p><p class=\"tagcloud\">{{#each tags}}<span class=\"tag{{this.weight}}\">{{this.name}}</span> {{/each}}</p><div class=\"coral-InputGroup\"><input type=\"text\" class=\"coral-InputGroup-input coral-Textfield tag-name\" placeholder=\"{{i18n \"Add a namespace:my/tag\"}}\" pattern=\"^[A-Za-z0-9_\\-]+(:[A-Za-z0-9_\\-\\/]+)?$\" title=\"{{i18n \"namespace:my/tag\"}}\"><span class=\"coral-InputGroup-button\"><button class=\"coral-Button coral-Button--secondary coral-Button--square contexthub-new-tag\" type=\"button\" title=\"{{i18n \"increment\"}}\"><i class=\"coral-Icon coral-Icon--sizeS coral-Icon--add\"></i></button></span></div></div>"
}
```

## granite.profile UI模块类型 {#granite-profile-ui-module-type}

granite.profile ContextHub UI模块显示当前用户的显示名称。 弹出窗口将显示用户的登录名，并允许您更改显示名的值。 UI模块从名为profile的ContextHub存储中获取信息，该配置文件基于 [granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) 商店候选者。

![chlimage_1-83](assets/chlimage_1-83a.png)

UI模块的源位于/libs/granite/contexthub/components/modules/profile。

### 配置 {#configuration-7}

grantie.profile UI模块的实例不需要详细信息配置的值。 以下JSON文本表示模块的默认配置。

```xml
{
   "icon":"coral-Icon--user",
   "title":"Profile",
   "clickable":true,
   "editable":{
      "key":"/profile",
      "disabled":["/profile/authorizableId"],
      "hidden":["/profile/avatar","/profile/path"]},
   "storeMapping":{"p":"profile"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Persona\"}}</p><p class=\"contexthub-module-line2\">{{p.displayName}}</p>",
   "listType":"checkmark"
}
```
