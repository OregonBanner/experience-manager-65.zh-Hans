---
title: 移动应用程序的页面模板
seo-title: 移动应用程序的页面模板
description: 可查看本页以了解有关页面模板的更多信息。 您为应用程序创建的页面组件基于/libs/mobileapps/components/angular/ng-page组件。
seo-description: 可查看本页以了解有关页面模板的更多信息。 您为应用程序创建的页面组件基于/libs/mobileapps/components/angular/ng-page组件。
uuid: c53901c9-5974-4c6b-ac61-1c094a93c9d6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: cfc7ad16-965e-4075-bc4d-5630abeaba55
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 移动应用程序的页面模板 {#page-templates-for-mobile-apps}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

## 移动应用程序的页面模板 {#page-templates-for-mobile-apps-1}

您为应用程序创建的页面组件基于/libs/mobileapps/components/angular/ng-page组件(在本地服[务器上的CRXDE Lite中打开](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page))。 此组件包含以下JSP脚本，您的组件会继承或覆盖这些脚本：

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

使用属性确定应用程序的名 `applicationName` 称，并通过pageContext公开它。

包括head.jsp和body.jsp。

### head.jsp {#head-jsp}

写出应用 `<head>` 程序页面的元素。

如果要覆盖应用程序的viewport meta属性，则此属性是您覆盖的文件。

根据最佳实践，应用程序在头中包括客户端库的css部分，而JS包含在closing &lt;元 `body>` 素。

### body.jsp {#body-jsp}

根据是否检测到wcmMode，角度页面的主体呈现方式不同(!= WCMMode.DISABLED)，以确定页面是打开以进行创作还是作为已发布页面。

**创作模式**

在创作模式中，每个单独的页面都会单独呈现。 Angular不处理页面之间的路由选择，ng-view也不用于加载包含页面组件的部分模板。 相反，页面模板的内容(template.jsp)通过标记包含在服务器端 `cq:include` 上。

此策略支持创作功能（如在段落系统中添加和编辑组件、Sidekick、设计模式等）函数。 依赖客户端渲染的页面（如应用程序的页面）在AEM创作模式下表现不佳。

请注意，template.jsp包含在包含指 `div` 令的元素中 `ng-controller` 。 这种结构使得DOM内容能够与控制器相链接。 因此，尽管在客户端呈现自己的页面会失败，但各个组件仍可正常工作（请参阅下面组件部分）。

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**发布模式**

在发布模式（例如，当使用内容同步导出应用程序时）中，所有页面都将变为单个页面应用程序(SPA)。 (要了解SPA，请使用Angular教程，具体而言就是 [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07)。)

SPA中只有一个HTML页面(包含元素的页 `<html>` 面)。 此页面称为“布局模板”。 在角度术语中，它是“...一个模板，它对于我们应用程序中的所有视图都是通用的。” 将此页面视为“顶级应用程序页面”。 按照惯例，顶级应用程序页面是您 `cq:Page` 的应用程序最靠近根节点的节点（而不是重定向）。

由于应用程序的实际URI在发布模式下没有更改，因此对此页面中外部资产的引用必须使用相对路径。 因此，提供了一个特殊的图像组件，它在渲染用于导出的图像时考虑此顶级页面。

作为SPA，此布局模板页面只生成一个带有ng-view指令的div元素。

```xml
 <div ng-view ng-class="transition"></div>
```

Angular route服务使用此元素显示应用程序中每页的内容，包括当前页面（包含在template.jsp中）的可创作内容。

body.jsp文件包含header.jsp和footer.jsp，这两个文件为空。 如果要在每个页面上提供静态内容，则可以在应用程序中覆盖这些脚本。

最后，在&lt;body>元素的底部包含javascript clientlib，其中包括两个在服务器上生成的特殊JS文件： *&lt;page name>*.angular-app-module.js和 *&lt;page name>*.angular-app-controllers.js。

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

此脚本定义应用程序的角度模块。 此脚本的输出链接到模板组件的其余部分通过ng-page.jsp中的元素生成的标记， `html` 该元素包含以下属性：

```xml
ng-app="<c:out value='${applicationName}'/>"
```

此属性指示Angular，表示此DOM元素的内容应链接到以下模块。 此模块将视图（在AEM中，这些视图将是cq:Page资源）与相应的控制器链接起来。

此模块还定义一个名为的顶级控制器，该控 `AppController` 制器将变量公开到 `wcmMode` 该范围，并配置从中获取内容同步更新负载的URI。

最后，此模块迭代每个子页面（包括自身）并呈现每个页面的路由片段的内容（通过angular-route-fragment.js选择器和扩展），包括它作为Angular的\$routeProvider的配置条目。 换句话说，\$routeProvider告知应用程序请求给定路径时要呈现的内容。

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

此脚本生成一个JavaScript片段，该片段必须采用以下形式：

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

此代码向$routeProvider(在angular-app-module.js.jsp中定义)指示“/&lt;path>”将由位于的资源处理，并由 `templateUrl``controller` （我们将转到下一个）连接。

如有必要，您可以覆盖此脚本以处理更复杂的路径，包括那些带有变量的路径。 在随AEM一起安装的/apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp脚本中可以看到以下示例：

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

在Angular中，控制器在\$scope中连接变量，将它们暴露给视图。 angular-app-controllers.js.jsp脚本遵循angular-app-module.js.jsp所示的模式，即它迭代每个子页面（包括自身）并输出每页定义的控制器片段(通过controller.js.jsp)。 它定义的模块将被调用 `cqAppControllers` ，并且必须作为顶级应用程序模块的依赖关系列出，以使页面控制器可用。

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

请注意，该 `data` 变量被指定为由角度方法返回的承 `$http.get` 诺。 如果需要，本页中包含的每个组件都可以使某些。json内容可用（通过其angular.json.jsp脚本），并在解析时对此请求的内容执行操作。 移动设备上的请求非常快，因为它只访问文件系统。

要使组件以这种方式成为控制器的一部分，它应扩展/libs/mobileapps/components/angular/ng-component组件并包含该属 `frameworkType: angular` 性。

### template.jsp {#template-jsp}

petmale.jsp首先在body.jsp部分引入，它只包含页面的parsys。 在发布模式中，此内容被直接引用（在&lt;page-path>.template.html），并通过在\$routeProvider上配置的templateUrl加载到SPA中。

此脚本中的parsys可以配置为接受任何类型的组件。 但是，在处理为传统网站（而非SPA）构建的组件时，必须小心。 例如，基础图像组件仅在顶级应用程序页面上正常工作，因为它不设计为引用应用程序内的资源。

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

此脚本只输出顶级Angular应用程序模块的Angular依赖项。 它由angular-app-module.js.jsp引用。

### header.jsp {#header-jsp}

将静态内容放在应用程序顶部的脚本。 此内容由顶级页面包含，位于ng-view的范围之外。

### footer.jsp {#footer-jsp}

用于在应用程序底部放置静态内容的脚本。 此内容由顶级页面包含，位于ng-view的范围之外。

### js_clientlibs.jsp {#js-clientlibs-jsp}

覆盖此脚本以包含您的JavaScript客户端。

### css_clientlibs.jsp {#css-clientlibs-jsp}

覆盖此脚本以包含您的CSS客户端库。

## 应用程序组件 {#app-components}

应用程序组件不仅必须处理AEM实例（发布或作者），而且当应用程序内容通过内容同步导出到文件系统时也必须处理。 因此，该组件必须包含以下特征：

* 必须相对引用PhoneGap应用程序中的所有资源、模板和脚本。
* 如果AEM实例在创作或发布模式下操作，则对链接的处理会有所不同。

### 相对资产 {#relative-assets}

PhoneGap应用程序中任何给定资产的URI不仅在每个平台上不同，而且在每个应用程序安装时都是唯一的。 例如，请注意iOS模拟器中运行的应用程序的以下URI:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

请在路径中记下GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39;。

作为PhoneGap开发人员，您关注的内容位于www目录下。 要访问应用程序资产，请使用相对路径。

要复合此问题，PhoneGap应用程序使用单页应用程序(SPA)模式，以便基本URI（不包括哈希）不会更改。 因此，您引用的每个资产、模板或脚 **本都必须相对于顶级页面。** 顶级页面通过和初始化角度路由和控 `*<name>*.angular-app-module.js` 制器 `*<name>*.angular-app-controllers.js`。 此页应是距存储库根目录最近的页面，*不*扩展sling:redirect。

有几种帮助方法可用于处理相对路径：

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

要查看其用法的示例，请打开位于/libs/mobileapps/components/angular的mobileapps源。

### 链接 {#links}

链接必须使用该函 `ng-click="go('/path')"` 数来支持所有WCM模式。 此函数取决于范围变量的值以正确确定链接操作：

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

当 `$scope.wcmMode == true` 我们以通常的方式处理每个导航事件时，结果是URL的路径和／或页面部分发生更改。

或者，如 `$scope.wcmMode == false`果每个导航事件导致URL的哈希部分发生更改，该哈希部分由Angular的ngRoute模块在内部解析。

### 组件脚本详细信息 {#component-script-details}

![chlimage_1-36](assets/chlimage_1-36.png)

#### ng-component.jsp {#ng-component-jsp}

此脚本在检测到“编辑”模式时显示组件内容或合适的占位符。

#### template.jsp {#template-jsp-1}

template.jsp脚本可呈现组件的标记。 如果相关组件是由从AEM提取的JSON数据驱动的(如“ng-text”:/libs/mobileapps/components/angular/ng-text/template.jsp)，则此脚本将负责将标记与由页面的控制器范围公开的数据连接起来。

但是，性能要求有时要求不执行客户端模板（aka数据绑定）。 在这种情况下，只需在服务器端渲染组件的标记，该标记便包含在页面模板内容中。

#### insperative.jsp {#overhead-jsp}

在由JSON数据驱动的组件中（如“ng-text”）:/libs/mobileapps/components/angular/ng-text)，开销。jsp可用于从template.jsp中删除所有Java代码。 然后，它会从template.jsp中引用，并且它在请求中公开的任何变量都可供使用。 此策略鼓励逻辑与表示分离，并限制从现有组件派生新组件时必须复制和粘贴的代码量。

#### controller.js.jsp {#controller-js-jsp-1}

如AEM页面模板中所述，每个组件都可以输出一个JavaScript片段以使用承诺公开的JSON内 `data` 容。 按照角度约定，控制器仅应用于为范围分配变量。

#### angular.json.jsp {#angular-json-jsp}

此脚本作为片段包含在页面范围的“&lt;page-name>.angular.json”文件中，该文件为扩展ng-page的每个页面导出。 在此文件中，组件开发人员可以公开组件所需的任何JSON结构。 在“ng-text”示例中，此结构只包括组件的文本内容以及指示组件是否包含富文本的标志。

Geometrixx Outdoors应用程序产品组件是一个更复杂的示例(/apps/geometrixx-outdoors-app/components/angular/ng-product):

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

## CLI资产下载的内容 {#contents-of-the-cli-assets-download}

从“应用程序”控制台下载CLI资源，以针对特定平台优化这些资源，然后使用PhoneGap命令行集成(CLI)API构建应用程序。 保存到本地文件系统的ZIP文件的内容具有以下结构：

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

这是一个隐藏目录，根据您当前的操作系统设置，您可能看不到该目录。 如果您计划修改包含该目录的应用程序挂钩，则应配置操作系统，以使此目录可见。

#### .cordova/hooks/ {#cordova-hooks}

此目录包含 [CLI挂钩](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/)。 挂接目录中的文件夹包含node.js脚本，这些脚本在构建过程中的精确点执行。

#### .cordova/hooks/after_platform_add/ {#cordova-hooks-after-platform-add}

after-platform_add目录包含该文 `copy_AMS_Conifg.js` 件。 此脚本复制配置文件以支持Adobe Mobile services分析的集合。

#### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

准备后目录包含该文 `copy_resource_files.js` 件。 此脚本将许多图标和初始屏幕图像复制到平台特定的位置。

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

before_platform_add目录包含该文 `install_plugins.js` 件。 此脚本迭代Cordova插件标识符列表，安装它检测到的尚未可用的插件标识符。

此策略不要求您每次执行Maven命令时都将插件捆绑并安 `content-package:install` 装到AEM。 将文件签入SCM系统的替代策略需要重复捆绑和安装活动。

#### .cordova/hooks/Other Hooks {#cordova-hooks-other-hooks}

根据需要包括其他挂钩。 以下挂钩可用（由Phonegap范例hello world应用程序提供）:

* after_build
* before_build
* after_compile
* before_compile
* after_docs
* before_docs
* after_emulate
* before_emulate
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

在您对项目执行命令之前， `phonegap run <platform>` 此目录为空。 当前， `<platform>` 可以是 `ios` 或 `android`。

为特定平台构建应用程序后，将创建相应的目录并包含特定于平台的应用程序代码。

#### plugins/ {#plugins}

执行命令后，插件目录将由文件中列 `.cordova/hooks/before_platform_add/install_plugins.js` 出的每个插件填 `phonegap run <platform>` 充。 该目录最初为空。

#### www/ {#www}

www目录包含实现应用程序外观和行为的所有Web内容（HTML、JS和CSS文件）。 除下述例外情况外，此内容源自AEM，并通过内容同步导出到其静态表单中。

#### www/config.xml {#www-config-xml}

PhoneGap [文档将此文件称为](https://docs.phonegap.com) “全局配置文件”。 config.xml包含许多应用程序属性，如应用程序名称、应用程序“preferences”（例如，iOS web视图是否允许溢流滚动）以及仅由PhoneGap内部版本使用的插 *件依赖* 。

config.xml文件是AEM中的静态文件，它按原样通过内容同步导出。

#### www/index.html {#www-index-html}

index.html文件将重定向到应用程序的起始页。

config.xml文件包含元 `content` 素：

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

在 [PhoneGap文档中](https://docs.phonegap.com)，此元素描述为“可选&lt;content>元素在顶级Web资产目录中定义应用程序的起始页。 默认值是index.html，它通常显示在项目的顶级www目录中。”

如果index.html文件不存在，PhoneGap构建将失败。 因此，会包含此文件。

#### www/res {#www-res}

res目录包含初始屏幕图像和图标。 该脚 `copy_resource_files.js` 本在构建阶段将文件复制到其特定于平台 `after_prepare` 的位置。

#### www/etc {#www-etc}

根据惯例，在AEM中， /etc节点包含静态clientlib内容。 etc目录包含Topcoat、AngularJS和Geometrixx ng-clientlibsall库。

#### www/apps {#www-apps}

应用程序目录包含与初始页面相关的代码。 AEM应用程序的初始化页面的独特特征是，它在不进行用户交互的情况下初始化应用程序。 因此，应用程序的clientlib内容（CSS和JS）最小，可以最大化性能。

#### www/content {#www-content}

内容目录包含应用程序的其余Web内容。 内容可以包括（但不限于）以下文件：

* HTML页面内容，直接在AEM中创作
* 与AEM组件关联的图像资产
* 服务器端脚本生成的JavaScript内容
* 描述页面或组件内容的JSON文件

#### www/package.json {#www-package-json}

package.json文件是一个清单文件，其中列出了完整内容同 **步下载** 包含的文件。 此文件还包含生成内容同步有效负荷的时间戳(`lastModified`)。 从AEM请求部分更新应用程序时，将使用此属性。

#### www/package-update.json {#www-package-update-json}

如果此有效负荷是整个应用程序的下载，则此清单包含文件的精确列表 `package.json`。

但是，如果此有效负荷是部分更新， `package-update.json` 则仅包含此特定有效负荷中包含的文件。
