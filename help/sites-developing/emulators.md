---
title: 模拟器
seo-title: 模拟器
description: AEM使作者能够在模拟器中查看页面，该模拟器模拟最终用户将在其中查看页面的环境
seo-description: AEM使作者能够在模拟器中查看页面，该模拟器模拟最终用户将在其中查看页面的环境
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 模拟器{#emulators}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

Adobe Experience Manager(AEM)使作者能够在模拟器中查看页面，该模拟器模拟最终用户将在其中查看页面的环境，例如在移动设备或电子邮件客户端中。

AEM模拟器框架：

* 在模拟用户界面(UI)（例如移动设备或电子邮件客户端）中提供内容创作（用于创作新闻稿）。
* 根据模拟的UI调整页面内容。
* 允许创建自定义模拟器。

>[!CAUTION]
>
>此功能仅在经典UI中受支持。

## 模拟器特性 {#emulators-characteristics}

模拟器：

* 基于ExtJS。
* 在页面DOM上操作。
* 其外观通过CSS进行调整。
* 支持插件（例如移动设备旋转插件）。
* 仅对作者处于活动状态。
* 其基本组件位于 `/libs/wcm/emulator/components/base`。

### 模拟器如何转换内容 {#how-the-emulator-transforms-the-content}

模拟器的工作方式是将HTML正文内容打包到模拟器DIV中。 例如，以下html代码：

```xml
<body>
<div id="wrapper" class="page mobilecontentpage ">
    <div class="topnav mobiletopnav">
    ...
    </div>
    ...
</div>
</body>
```

在模拟器启动后，将转换为以下html代码：

```xml
<body>
 <div id="cq-emulator-toolbar">
 ...
 </div>
 <div id="cq-emulator-wrapper">
  <div id="cq-emulator-device">
   <div class=" android vertical" id="cq-emulator">
    ...
    <div class=" android vertical" id="cq-emulator-content">
     ...
     <div id="wrapper" class="page mobilecontentpage">
     ...
     </div>
     ...
    </div>
   </div>
  </div>
 </div>
 ...
</body>
```

添加了两个div标签：

* id为整个模 `cq-emulator` 拟器的div以及

* div，其id表 `cq-emulator-content` 示页面内容所在设备的viewport/screen/content区域。

新的CSS类也分配给新的模拟器div:它们表示当前模拟器的名称。

模拟器的插件可以进一步扩展已分配的CSS类的列表，如旋转插件的示例所示，根据当前设备旋转插入“垂直”或“水平”类。

这样，通过使CSS类与模拟器div的ID和CSS类相对应，可以控制模拟器的完整外观。

>[!NOTE]
>
>建议项目HTML将正文内容包装在单个div中，如上例所示。 如果正文内容包含多个标记，则可能会产生不可预知的结果。

### 移动模拟器 {#mobile-emulators}

现有的移动模拟器：

* 位于/libs/wcm/mobile/components/emulators下。
* 可通过JSON servlet访问：

   http://localhost:4502/bin/wcm/mobile/emulators.json

当页面组件依赖移动页面组件( `/libs/wcm/mobile/components/page`)时，模拟器功能会通过以下机制自动集成到页面中：

* 移动页面组件 `head.jsp` 包括设备组的关联模拟器初始化组件（仅在创作模式下）和设备组的呈现CSS，具体通过：

   `deviceGroup.drawHead(pageContext);`

* 该方 `DeviceGroup.drawHead(pageContext)` 法包括模拟器的init组件，即调用模拟器 `init.html.jsp` 组件。 如果模拟器组件没有自己的模 `init.html.jsp` 拟器，并且依赖于移动基础模拟器( `wcm/mobile/components/emulators/base)`则调用移动基础模拟器的init脚本( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`))。

* 移动基本模拟器的init脚本通过Javascript定义：

   * 为页面定义的所有模拟器的配置(emulatorConfigs)
   * 模拟器管理器通过以下方式将模拟器的功能集成到页面中：

      `emulatorMgr.launch(config)`;

      模拟器管理器由以下几个部分定义：

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### 创建自定义移动模拟器 {#creating-a-custom-mobile-emulator}

要创建自定义移动模拟器，请执行以下操作：

1. 下面 `/apps/myapp/components/emulators` 创建组件 `myemulator` (节点类型： `cq:Component`)。

1. 将属 `sling:resourceSuperType` 性设置为 `/libs/wcm/mobile/components/emulators/base`

1. 为模拟器外观定义具有类 `cq.wcm.mobile.emulator` 别的CSS客户端库：name = `css`, node type = `cq:ClientLibrary`

   例如，您可以引用节点 `/libs/wcm/mobile/components/emulators/iPhone/css`

1. 如果需要，请定义JS客户端库，例如定义特定插件：name = js, node type = cq:ClientLibrary

   例如，您可以引用节点 `/libs/wcm/mobile/components/emulators/base/js`

1. 如果模拟器支持由插件定义的特定功能（如触屏滚动），请在模拟器下创建一个配置节点：name = `cq:emulatorConfig`, node type = `nt:unstructured` and add the property that defines plugin:

   * 名称= `canRotate`，类型= `Boolean`，值= `true`:以包含旋转功能。

   * 名称= `touchScrolling`，类型= `Boolean`，值= `true`:以包含触控滚动功能。
   通过定义您自己的插件可以添加更多功能。

