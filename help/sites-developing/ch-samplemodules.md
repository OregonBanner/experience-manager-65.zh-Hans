---
title: 示例ContextHub UI模块类型
seo-title: 示例ContextHub UI模块类型
description: ContextHub提供了几个可在解决方案中使用的示例UI模块
seo-description: ContextHub提供了几个可在解决方案中使用的示例UI模块
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 0%

---


# 示例ContextHub UI模块类型 {#sample-contexthub-ui-module-types}

ContextHub提供了几个可在解决方案中使用的示例UI模块。 提供了以下信息：

* UI模块的主要功能。
* 在何处可以找到源代码，以便您打开它进行学习。
* 如何配置UI模块。

有关将UI模块添加到ContextHub的信息，请 [参阅添加UI模块](ch-configuring.md#adding-a-ui-module)。 有关开发UI模块的信息，请参 [阅创建ContextHub UI模块类型](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)。

## contexthub.base UI模块类型 {#contexthub-base-ui-module-type}

contexthub.base UI模块类型是所有其他UI模块类型的基本类型。 因此，它提供用于呈现存储数据的通用功能。

提供以下功能：

* **标题和图标：** 指定UI模块的标题和图标。 该图标可以使用URL或从Coral UI图标库中引用。
* **存储数据：** 标识要从中检索数据的一个或多个存储。
* **内容：** 指定在UI模块中显示的内容（如ContextHub工具栏中显示的内容）。
* **跨距内容：** 指定单击或点按UI模块时在弹出窗口中显示的内容。
* **全屏模式：** 控制是否允许全屏模式。

源代码位于/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js。

### 配置 {#configuration}

使用JSON格式的Javascript对象配置contexthub.base UI模块。 包含以下任意属性以配置UI模块功能：

* **图像：** 要显示为图标的图像的URL。
* **图标：** Coral UI图 [标类的名称](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) 。 如果为图标和图像属性指定值，则会使用图像。

* **标题：** UI模块的标题。 当指针暂停在UI模块图标上时，将显示标题。
* **全屏：** 一个布尔值，它指示UI模块是否支持全屏模式。 使用 `true` 支持全屏模式 `false` 并防止全屏模式。

* **模板：** 一个 [Handlebars](https://handlebarsjs.com/) 模板，它指定要在ContextHub工具栏中呈现的内容。 最多使用两个 `<p>` 标记。

* **storeMapping:** 密钥／存储映射。 使用Handlebar模板中的键访问关联的ContextHub存储数据。
* **列表:** 在单击UI模块时，要在弹出窗口中显示为列表的项目数组。 如果包括此项目，则不要包括popoverTemplate。 该值是具有以下键的对象的数组：

   * 标题：此项目要显示的文本
   * 图像：（可选）应显示在左侧的图像的URL
   * 图标：（可选）应显示在左侧的CUI图标类；如果指定了图像，则忽略
   * 选定：（可选）一个布尔值，它指定是否应将此项显示为选定项（true=已选定）。 默认情况下，选定项目使用粗体显示。 使用属 `listType` 性配置其他外观（请参见下文）。

* **listType:** 用于弹出列表项的样式。 请使用以下值之一：

   * 选中标记
   * 复选框
   * 无线电

* **弹出窗口模板：** 一个Handlebars模板，它指定在单击UI模块时在弹出窗口中呈现的内容。 如果包含此项目，则不要包含该 `list` 项目。

### 示例 {#example}

以下示例将contexthub.base UI模块配置为显示contexthub. [emulators存储中的信息](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) 。 该 `template` 项目演示如何使用项目建立的密钥从商店获取 `storeMapping` 数据。

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

contexthub.browserinfo UI模块显示有关客户端Web浏览器和操作系统的信息。 根据contexthub.surferinfo存储候选项，从 [surferinfo存储获](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) 取信息。

![chlimage_1-77](assets/chlimage_1-77a.png)

UI模块的源代码位于/libs/granite/contexthub/components/modules/browserinfo。 尽管contexthub.browserinfo扩展了contexthub.base UI模块，但它不会覆盖或提供其他功能。 该实现为呈现浏览器信息提供了默认配置。

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

contexthub.datetime UI模块显示存储在名为datetime的存储中的日期和时间，该存储基于 [contexthub.datetime存储候](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) 选项。

![chlimage_1-78](assets/chlimage_1-78a.png)

该模块提供一个弹出窗格，允许您更改商店中的日期和时间。

contexthub.datetime UI模块的源位于/libs/granite/contexthub/components/modules/datetime。

### 配置 {#configuration-2}

contexthub.datetime UI模块的实例不需要Detail Configuration的值。 以下JSON文本表示模块的默认配置。

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

contexthub.location UI模块显示客户端的经度和纬度。 该模块提供一个弹出窗口，其中显示一个Google地图，您可以单击该地图来更改当前位置。 该模块从名为geolocation的ContextHub存储中获取信息，该Geolocation基 [于contexthub.geolocation存储候](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) 选项。

![chlimage_1-80](assets/chlimage_1-80a.png)

UI模块的源位于/etc/cloudsettings/default/contexthub/geolocation。

### 配置 {#configuration-4}

contexthub.location UI模块的实例不需要详细信息配置的值。 以下JSON文本表示模块的默认配置。

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

contexthub.screen-orientation UI模块显示客户端的当前屏幕方向。 虽然模块默认处于禁用状态，但该模块会提供一个弹出窗口，允许您选择方向。 该模块从名为emulators的ContextHub存储中获取信息，该模拟器基于 [granite.emulators存储候](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) 选项。

![chlimage_1-81](assets/chlimage_1-81a.png)

UI模块的源位于/libs/granite/contexthub/components/modules/screen-orientation。

### 配置 {#configuration-5}

contexthub.screen-orientation UI模块的实例不需要“详细配置”值。 以下JSON文本表示模块的默认配置。 请注意， `clickable` 默认情况下 `false` 该属性。 如果覆盖要设置为的默认配 `clickable` 置， `true`则单击模块会显示一个弹出窗口，您可以从中选择方向。

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

contexthub.tagcloud UI模块显示有关标记的信息。 在工具栏中，UI模块显示标记数。 弹出窗口会显示用于添加新标记的标记云和文本框。 UI模块从名为tagcloud的ContextHub存储中获取基于contexthub.tagcloud存储候 [选项的信息](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) 。

![chlimage_1-82](assets/chlimage_1-82a.png)

UI模块的源位于/libs/granite/contexthub/components/modules/tagcloud。

### 配置 {#configuration-6}

contexthub.tagcloud UI模块的实例不需要详细信息配置的值。 以下JSON文本表示模块的默认配置。

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

## granite.用户档案UI模块类型 {#granite-profile-ui-module-type}

granite.用户档案ContextHub UI模块显示当前用户的显示名称。 弹出窗口显示用户的登录名，并允许您更改显示名称的值。 UI模块从名为用户档案的ContextHub存储中获取基于granite. [用户档案存储候选](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) 的信息。

![chlimage_1-83](assets/chlimage_1-83a.png)

UI模块的源位置为/libs/granite/contexthub/components/modules/用户档案。

### 配置 {#configuration-7}

用户档案UI模块的实例不需要详细信息配置的值。 以下JSON文本表示模块的默认配置。

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
