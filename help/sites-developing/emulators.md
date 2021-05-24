---
title: 模拟器
seo-title: 模拟器
description: AEM允许作者在模拟最终用户将在其中查看页面的环境的模拟器中查看页面
seo-description: AEM允许作者在模拟最终用户将在其中查看页面的环境的模拟器中查看页面
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# 模拟器{#emulators}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

Adobe Experience Manager(AEM)允许作者在模拟器中查看页面，该模拟器模拟最终用户将在其中查看页面的环境，例如在移动设备或电子邮件客户端中。

AEM模拟器框架：

* 在模拟的用户界面(UI)中提供内容创作，例如移动设备或电子邮件客户端（用于创作新闻稿）。
* 根据模拟的UI调整页面内容。
* 允许创建自定义模拟器。

>[!CAUTION]
>
>仅经典UI支持此功能。

## 模拟器特性{#emulators-characteristics}

模拟器：

* 基于ExtJS。
* 在页面DOM上运行。
* 其外观通过CSS进行管制。
* 支持插件（例如移动设备旋转插件）。
* 仅在作者上处于活动状态。
* 其基本组件位于`/libs/wcm/emulator/components/base`。

### 模拟器如何转换内容{#how-the-emulator-transforms-the-content}

模拟器的工作方式是将HTML主体内容封装到模拟器DIV中。 例如，以下html代码：

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

添加了两个div标记：

* id为`cq-emulator`的div将模拟器作为一个整体并

* id为`cq-emulator-content`的div，表示页面内容所在设备的视区/屏幕/内容区域。

还将新的CSS类分配给新的模拟器div:它们表示当前模拟器的名称。

模拟器的插件可以进一步扩展已分配CSS类的列表（如旋转插件的示例中），根据当前设备旋转插入“垂直”或“水平”类。

这样，可以通过具有与模拟器div的ID和CSS类相对应的CSS类来控制模拟器的完整外观。

>[!NOTE]
>
>建议项目HTML将主体内容包装在单个div中，就像上面的示例中一样。 如果正文内容包含多个标记，则结果可能无法预测。

### 移动设备模拟器{#mobile-emulators}

现有的移动设备模拟器：

* 位于/libs/wcm/mobile/components/emulators下。
* 可通过JSON Servlet在以下位置获取：

   http://localhost:4502/bin/wcm/mobile/emulators.json

当页面组件依赖于移动页面组件(`/libs/wcm/mobile/components/page`)时，模拟器功能将通过以下机制自动集成到页面中：

* 移动页面组件`head.jsp`包含设备组的关联模拟器初始组件（仅在创作模式下）和设备组的渲染CSS:

   `deviceGroup.drawHead(pageContext);`

* 方法`DeviceGroup.drawHead(pageContext)`包括模拟器的init组件，即调用模拟器组件的`init.html.jsp`。 如果模拟器组件没有自己的`init.html.jsp`并且依赖于移动设备基本模拟器(`wcm/mobile/components/emulators/base)`)，则将调用移动设备基本模拟器的init脚本(`/libs/wcm/mobile/components/emulators/base/init.html.jsp`)。

* 基于移动设备的模拟器的init脚本通过Javascript定义：

   * 为页面定义的所有模拟器的配置(emulatorConfigs)
   * 模拟器管理器通过以下方式在页面中集成了模拟器的功能：

      `emulatorMgr.launch(config)`;

      模拟器管理器由以下项定义：

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### 创建自定义移动设备模拟器{#creating-a-custom-mobile-emulator}

要创建自定义移动模拟器，请执行以下操作：

1. 在`/apps/myapp/components/emulators`下创建组件`myemulator`(节点类型：`cq:Component`)。

1. 将`sling:resourceSuperType`属性设置为`/libs/wcm/mobile/components/emulators/base`

1. 为模拟器外观定义类别为`cq.wcm.mobile.emulator`的CSS客户端库：name = `css`,node type = `cq:ClientLibrary`

   例如，您可以引用节点`/libs/wcm/mobile/components/emulators/iPhone/css`

1. 如果需要，请定义JS客户端库，例如定义特定插件：name = js，node type = cq:ClientLibrary

   例如，您可以引用节点`/libs/wcm/mobile/components/emulators/base/js`

1. 如果模拟器支持插件定义的特定功能（如触屏滚动），请在模拟器下方创建一个配置节点：name = `cq:emulatorConfig`,node type = `nt:unstructured`并添加用于定义插件的属性：

   * 名称= `canRotate`，类型= `Boolean`，值= `true`:以包含旋转功能。

   * 名称= `touchScrolling`，类型= `Boolean`，值= `true`:，以包含触控滚动功能。
   通过定义您自己的插件可添加更多功能。
