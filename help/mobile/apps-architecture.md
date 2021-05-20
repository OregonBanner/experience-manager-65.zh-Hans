---
title: 移动设备应用程序的页面模板
seo-title: 移动设备应用程序的页面模板
description: 可查看本页以了解有关页面模板的更多信息。 您为应用程序创建的页面组件基于/libs/mobileapps/components/angular/ng-page组件。
seo-description: 可查看本页以了解有关页面模板的更多信息。 您为应用程序创建的页面组件基于/libs/mobileapps/components/angular/ng-page组件。
uuid: c53901c9-5974-4c6b-ac61-1c094a93c9d6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: cfc7ad16-965e-4075-bc4d-5630abeaba55
exl-id: 397def36-45b2-47a7-b103-99ca22b6dae1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2698'
ht-degree: 0%

---

# 移动设备应用程序的页面模板{#page-templates-for-mobile-apps}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

## 移动设备应用程序的页面模板{#page-templates-for-mobile-apps-1}

您为应用程序创建的页面组件基于/libs/mobileapps/components/angular/ng-page组件([在本地服务器上以CRXDE Lite打开](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page))。 此组件包含以下JSP脚本，您的组件会继承或覆盖这些脚本：

* ng-page.jsp
* head.jsp
* body.jsp
* angular-app-module.js.jsp
* angular-route-fragment.js.jsp
* angular-app-controllers.js.jsp
* controller.js.jsp
* template.jsp
* angular-module-list.js.jsp
* header.jsp
* footer.jsp
* js_clientlibs.jsp
* css_clientlibs.jsp

### ng-page.jsp {#ng-page-jsp}

使用`applicationName`属性确定应用程序的名称，并通过pageContext公开该名称。

包括head.jsp和body.jsp。

### head.jsp {#head-jsp}

写出应用程序页面的`<head>`元素。

如果要覆盖应用程序的视区元属性，则是您覆盖的文件。

按照最佳实践，应用程序将客户端库的css部分包含在标头中，而JS包含在结束`body>`元素中。

### body.jsp {#body-jsp}

angular页面的主体呈现方式不同，具体取决于是否检测到wcmMode(!= WCMMode.DISABLED)来确定页面是打开进行创作，还是作为已发布的页面打开。

**创作模式**

在创作模式下，每个页面会单独呈现。 Angular不处理页面之间的路由，也不使用ng-view来加载包含页面组件的部分模板。 而是通过`cq:include`标记在服务器端包含页面模板(template.jsp)的内容。

此策略支持创作功能（例如在段落系统中添加和编辑组件、Sidekick、设计模式等） 功能。 依赖客户端渲染的页面（例如应用程序的页面）在AEM创作模式下表现不佳。

请注意，template.jsp包含封装在包含`ng-controller`指令的`div`元素中。 此结构允许将DOM内容与控制器链接。 因此，尽管在客户端呈现自身的页面失败，但是执行此操作的各个组件仍可正常使用（请参阅下面“组件”部分）。

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**发布模式**

在发布模式下（例如，当使用内容同步导出应用程序时），所有页面都将变为单页应用程序(SPA)。 (要了解SPA，请使用Angular教程，特别是[https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07)。)

SPA中只有一个HTML页面（一个包含`<html>`元素的页面）。 此页面称为“布局模板”。 在Angular术语中，它是“……一个模板，它适用于应用程序中的所有视图。” 将此页面视为“顶级应用程序页面”。 按照惯例，顶级应用程序页面是应用程序的`cq:Page`节点，该节点离根节点最近（而不是重定向）。

由于应用程序的实际URI在发布模式下不会更改，因此从此页面对外部资产的引用必须使用相对路径。 因此，提供了特殊的图像组件，在渲染要导出的图像时，该组件会考虑此顶级页面。

作为SPA，此布局模板页面只会生成一个包含ng-view指令的div元素。

```xml
 <div ng-view ng-class="transition"></div>
```

angular路由服务使用此元素来显示应用程序中每个页面的内容，包括当前页面（包含在template.jsp中）的可创作内容。

body.jsp文件包含header.jsp和footer.jsp，它们为空。 如果要在每个页面上提供静态内容，则可以在应用程序中覆盖这些脚本。

最后，Javascript clientlibs包含在&lt;body>元素的底部，其中包括服务器上生成的两个特殊JS文件：*&lt;页面名称>*.angular-app-module.js和&#x200B;*&lt;页面名称>*.angular-app-controllers.js。

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

此脚本定义应用程序的Angular模块。 此脚本的输出链接到模板组件的其余部分通过ng-page.jsp中的`html`元素生成的标记，该元素包含以下属性：

```xml
ng-app="<c:out value='${applicationName}'/>"
```

此属性指示Angular此DOM元素的内容应链接到以下模块。 此模块将视图(在AEM中，这些视图将是cq:Page资源)与相应的控制器链接起来。

此模块还定义一个名为`AppController`的顶级控制器，该控制器将`wcmMode`变量公开到作用域，并配置从中获取内容同步更新负载的URI。

最后，此模块遍历每个子页面（包括其本身）并呈现每个页面的路由片段的内容(通过angular-route-fragment.js选择器和扩展)，包括作为Angular\$routeProvider的配置条目。 换言之， \$routeProvider会告知应用程序在请求给定路径时要呈现的内容。

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

此脚本会生成一个必须采用以下形式的JavaScript片段：

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

此代码指示$routeProvider(在angular-app-module.js.jsp中定义)“/&lt;path>”将由`templateUrl`的资源处理，并由`controller`连接（我们将在下一步中连接）。

如有必要，您可以覆盖此脚本以处理更复杂的路径，包括包含变量的路径。 例如，在随AEM一起安装的/apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp脚本中可以看到此示例：

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

在Angular中，控制器在\$范围中连接变量，将它们公开给视图。 angular-app-controllers.js.jsp脚本遵循angular-app-module.js.jsp所示的模式，即它遍历每个子页面（包括其自身）并输出每个页面定义的控制器片段(通过controller.js.jsp)。 它定义的模块称为`cqAppControllers`，必须作为顶级应用程序模块的依赖项列出，以使页面控制器可用。

### controller.js.jsp {#controller-js-jsp}

controller.js.jsp脚本为每个页面生成控制器片段。 此控制器片段采用以下形式：

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

请注意，为`data`变量分配了Angular`$http.get`方法返回的promise。 如果需要，本页中包含的每个组件都可以使某些.json内容可用(通过其angular.json.jsp脚本)，并在解析此请求时对其内容执行操作。 在移动设备上，请求的速度非常快，因为它只是访问文件系统。

要使组件以这种方式成为控制器的一部分，它应该扩展/libs/mobileapps/components/angular/ng-component组件并包含`frameworkType: angular`属性。

### template.jsp {#template-jsp}

template.jsp首先在body.jsp部分中引入，它只包含页面的parsys。 在发布模式下，此内容会直接引用（在&lt;page-path>.template.html），并通过在\$routeProvider中配置的templateUrl加载到SPA中。

此脚本中的parsys可配置为接受任何类型的组件。 但是，在处理为传统网站(而不是SPA)构建的组件时，必须谨慎。 例如，基础图像组件仅在顶级应用程序页面上正常运行，因为它不是设计为引用应用程序内的资产。

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

此脚本只会输出顶级Angular应用程序模块的Angular依赖项。 angular-app-module.js.jsp引用了该变量。

### header.jsp {#header-jsp}

用于在应用程序顶部放置静态内容的脚本。 此内容由顶级页面（在ng-view范围之外）包含。

### footer.jsp {#footer-jsp}

用于在应用程序底部放置静态内容的脚本。 此内容由顶级页面（在ng-view范围之外）包含。

### js_clientlibs.jsp {#js-clientlibs-jsp}

覆盖此脚本以包含您的JavaScript clientlib。

### css_clientlibs.jsp {#css-clientlibs-jsp}

覆盖此脚本以包含您的CSS客户端库。

## 应用程序组件{#app-components}

应用程序组件不仅必须在AEM实例（发布或创作）上工作，而且当应用程序内容通过内容同步导出到文件系统时也必须工作。 因此，该组件必须包括以下特征：

* PhoneGap应用程序中的所有资产、模板和脚本都必须相对引用。
* 如果AEM实例在创作或发布模式下运行，则对链接的处理会有所不同。

### 相对资产{#relative-assets}

PhoneGap应用程序中任何给定资产的URI不仅会按平台而有所不同，而且在应用程序的每次安装中都是唯一的。 例如，请注意在iOS模拟器中运行的应用程序的以下URI:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

请注意路径中的GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39;。

作为PhoneGap开发人员，您关注的内容位于www目录下方。 要访问应用程序资产，请使用相对路径。

要解决此问题，您的PhoneGap应用程序使用单页应用程序(SPA)模式，以便基本URI（不包括哈希）永不更改。 因此，您引用&#x200B;**的每个资产、模板或脚本都必须相对于您的顶级页面。** 顶级页通过和初始化Angular路由和 `*<name>*.angular-app-module.js` 控 `*<name>*.angular-app-controllers.js`制器。此页面应是距存储库根目录最近的*不*扩展sling:redirect页面。

有几种帮助程序方法可用于处理相对路径：

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

要查看其使用示例，请打开位于/libs/mobileapps/components/angular的mobileapps源。

### 链接 {#links}

链接必须使用`ng-click="go('/path')"`函数来支持所有WCM模式。 此函数取决于作用域变量的值，以正确确定链接操作：

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

当`$scope.wcmMode == true`时，我们会按常规方式处理每个导航事件，这样会导致URL的路径和/或页面部分发生更改。

或者，如果`$scope.wcmMode == false`，则每个导航事件都会导致URL的哈希部分发生更改，该哈希部分由Angular的ngRoute模块在内部解析。

### 组件脚本详细信息{#component-script-details}

![chlimage_1-36](assets/chlimage_1-36.png)

#### ng-component.jsp {#ng-component-jsp}

在检测到编辑模式时，此脚本会显示组件内容或合适的占位符。

#### template.jsp {#template-jsp-1}

template.jsp脚本呈现组件的标记。 如果相关组件是由从AEM提取的JSON数据（例如“ng-text”）驱动的：/libs/mobileapps/components/angular/ng-text/template.jsp)，则此脚本将负责将标记与由页面的控制器范围公开的数据连接起来。

但是，性能要求有时要求不执行客户端模板（即数据绑定）。 在这种情况下，只需在服务器端渲染组件的标记，即可将其包含在页面模板内容中。

#### 开销.jsp {#overhead-jsp}

在由JSON数据驱动的组件（例如“ng-text”）中：/libs/mobileapps/components/angular/ng-text)，开销.jsp可用于从template.jsp中删除所有Java代码。 然后，该变量会从template.jsp中引用，并且该变量在请求中公开的任何变量都可供使用。 此策略鼓励将逻辑与呈现分离，并限制从现有组件派生新组件时必须复制和粘贴的代码量。

#### controller.js.jsp {#controller-js-jsp-1}

如AEM页面模板中所述，每个组件都可以输出一个JavaScript片段来使用`data` promise公开的JSON内容。 遵循Angular惯例，控制器应仅用于将变量分配给范围。

#### angular.json.jsp {#angular-json-jsp}

此脚本作为片段包含在页面范围的“&lt;page-name>.angular.json”文件中，该文件将针对扩展ng-page的每个页面导出。 在此文件中，组件开发人员可以公开组件所需的任何JSON结构。 在“ng-text”示例中，此结构仅包含组件的文本内容以及指示组件是否包含富文本的标记。

Geometrixx户外应用程序产品组件是一个更复杂的示例(/apps/geometrixx-outdoors-app/components/angular/ng-product):

```xml
{
    "content-par/ng-product": {
        "items": [{
            "name": "Cajamara",
            "description": "Bike",
            "summaryHTML": "",
            "price": "$610.00",
            "SKU": "eqsmcj",
            "numberOfLikes": "0",
            "numberOfComments": "0"
        }]
    },
    "content-par/ng-product/ng-image": {
        "items": [{
            "hasContent": true,
            "imgSrc": "home/products/eq/eqsm/eqsmcj/jcr_content/content-par/ng-product/ng-image.img.jpg/1377771306985.jpg",
            "description": "",
            "alt": "Cajamara",
            "title": "Cajamara",
            "hasLink": false,
            "linkPath": "",
            "attributes": [{
                "attributeName": "class",
                "attributeValue": "cq-dd-image"
            }]
        }]
    }
}
```

## CLI资产下载{#contents-of-the-cli-assets-download}的内容

从应用程序控制台下载CLI资产，以针对特定平台优化资产，然后使用PhoneGap命令行集成(CLI)API构建应用程序。 保存到本地文件系统的ZIP文件的内容具有以下结构：

```xml
.cordova/
  |- hooks/
     |- after_prepare/
     |- before_platform_add/
     |- Other Hooks
plugins/
www/
  |- config.xml
  |- index.html
  |- res/
  |- etc/
  |- apps/
  |- content/
  |- package.json
  |- package-update.json
```

### .cordova {#cordova}

这是一个隐藏目录，您可能看不到它，具体取决于您当前的操作系统设置。 如果您计划修改包含的应用程序挂接，则应配置操作系统，以便此目录可见。

#### .cordova/hooks/ {#cordova-hooks}

此目录包含[CLI挂接](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/)。 挂接目录中的文件夹包含node.js脚本，这些脚本在生成过程中的确切时间点执行。

#### .cordova/hooks/after_platform_add/ {#cordova-hooks-after-platform-add}

after-platform_add目录包含`copy_AMS_Conifg.js`文件。 此脚本会复制一个配置文件，以支持AdobeMobile Services分析的收集。

#### .cordova/hooks/after prepare/ {#cordova-hooks-after-prepare}

after-prepare目录包含`copy_resource_files.js`文件。 此脚本将大量图标和启动屏幕图像复制到特定于平台的位置。

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

before_platform_add目录包含`install_plugins.js`文件。 此脚本通过Cordova插件标识符列表进行迭代，并安装它检测到的标识符尚不可用。

此策略不要求每次执行Maven `content-package:install`命令时都将插件捆绑并安装到AEM中。 将文件签入SCM系统的替代策略需要重复捆绑和安装活动。

#### .cordova/hooks/Other Hooks {#cordova-hooks-other-hooks}

根据需要包括其他挂钩。 可用的挂钩如下（由Phonegap hello world应用程序示例提供）：

* after_build
* before_build
* after_compile
* before_compile
* after_docs
* before_docs
* after_imulate
* before_umalut
* after_platform_add
* before_platform_add
* after_platform_ls
* before_platform_ls
* after_platform_rm
* before_platform_rm
* after_plugin_add
* before_plugin_add
* after_plugin_ls
* before_plugin_ls
* after_plugin_rm
* before_plugin_rm
* after_prepare
* before_prepare
* after_run
* before_run

#### platforms/ {#platforms}

在对项目执行`phonegap run <platform>`命令之前，此目录为空。 目前，`<platform>`可以是`ios`或`android`。

为特定平台构建应用程序后，将创建相应的目录，并包含特定于平台的应用程序代码。

#### plugins/ {#plugins}

执行`phonegap run <platform>`命令后，插件目录将由`.cordova/hooks/before_platform_add/install_plugins.js`文件中列出的每个插件填充。 目录最初为空。

#### www/ {#www}

www目录包含实施应用程序外观和行为的所有Web内容（HTML、JS和CSS文件）。 除下面所述的例外情况外，此内容源自AEM，并通过内容同步导出为其静态形式。

#### www/config.xml {#www-config-xml}

[PhoneGap文档](https://docs.phonegap.com)将此文件称为“全局配置文件”。 config.xml包含许多应用程序属性，如应用程序名称、应用程序“首选项”（例如iOS Web视图是否允许覆盖滚动）以及&#x200B;*仅*&#x200B;由PhoneGap内部版本使用的插件依赖项。

config.xml文件是AEM中的静态文件，可通过内容同步按原样导出。

#### www/index.html {#www-index-html}

index.html文件将重定向到应用程序的起始页。

config.xml文件包含`content`元素：

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

在[PhoneGap文档](https://docs.phonegap.com)中，此元素被描述为“可选&lt;content>元素在顶级Web资产目录中定义应用程序的起始页。 默认值为index.html，它通常显示在项目的顶级www目录中。”

如果不存在index.html文件，则PhoneGap生成失败。 因此，会包含此文件。

#### www/res {#www-res}

res目录包含启动屏幕图像和图标。 在`after_prepare`生成阶段， `copy_resource_files.js`脚本会将文件复制到其特定于平台的位置。

#### www/etc {#www-etc}

按照惯例，在AEM中，/etc节点包含静态clientlib内容。 etc目录包含Topcoat、AngularJS和Geometrixxng-clientlibsall库。

#### www/apps {#www-apps}

应用程序目录包含与启动页面相关的代码。 AEM应用程序的启动页面的独特之处在于，它在不进行用户交互的情况下初始化应用程序。 因此，应用程序的clientlib内容（CSS和JS）是最小的，可最大程度地提高性能。

#### www/content {#www-content}

内容目录包含应用程序的其余Web内容。 内容可以包括（但不限于）以下文件：

* 直接在AEM中创作的HTML页面内容
* 与AEM组件关联的图像资产
* 服务器端脚本生成的JavaScript内容
* 描述页面或组件内容的JSON文件

#### www/package.json {#www-package-json}

package.json文件是一个清单文件，其中列出了&#x200B;**full**&#x200B;内容同步下载包含的文件。 此文件还包含生成内容同步有效负载的时间戳(`lastModified`)。 当从AEM请求部分更新应用程序时，会使用此属性。

#### www/package-update.json {#www-package-update-json}

如果此负载是整个应用程序的下载，则此清单包含`package.json`文件的确切列表。

但是，如果此负载是部分更新，则`package-update.json`只包含此特定负载中包含的文件。
