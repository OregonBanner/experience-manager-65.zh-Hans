---
title: 单页应用程序
seo-title: 单页应用程序
description: 可查看本页以了解有关单页应用程序的信息，即，您可以创建与桌面或移动应用程序性能相同的应用程序。
seo-description: 可查看本页以了解有关单页应用程序的信息，即，您可以创建与桌面或移动应用程序性能相同的应用程序。
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 0%

---


# 单页应用程序{#single-page-applications}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

[单页应用程序](https://en.wikipedia.org/wiki/Single-page_application) (SPA)已达到临界质量，被广泛认为是利用Web技术构建无缝体验的最有效模式。通过遵循SPA模式，您可以创建一个与桌面或移动应用程序性能相同的应用程序，但由于它在开放Web标准中的基础，它可以到达多种设备平台和外形规格。

一般而言，SPA比基于页面的传统网站表现更出色，因为它们通常只加载一次&#x200B;**完整的HTML页面（包括CSS、JS和支持字体内容），然后仅加载每次应用程序中发生状态更改时所需的内容。**&#x200B;此状态更改的必要性可能因所选技术集而异，但通常包括一个HTML片段以替换现有的“视图”，以及执行一组JS代码以连接新视图并执行任何可能需要的客户端模板渲染。 通过支持模板缓存机制，甚至在使用Adobe PhoneGap时脱机访问模板内容，可以进一步提高此状态更改的速度。

AEM 6.1支持通过AEM应用程序构建和管理SPA。 本文将介绍SPA背后的概念以及它们如何利用[AngularJS](https://angularjs.org/)将您的品牌引入App Store和Google Play。

## SPA AEM应用程序{#spa-in-aem-apps}中的

AEM Apps中的单页应用程序框架支持AngularJS应用程序的高性能，同时允许作者（或其他非技术人员）通过触控优化拖放编辑器环境创建和管理应用程序内容，该编辑器通常为管理网站而保留。 已经有一个使用AEM构建的站点？ 您会发现，使用AEM App可以轻松地重复利用您的内容、组件、工作流、资产和权限。

## AngularJS应用程序模块{#angularjs-application-module}

AEM应用程序为您处理大部分AngularJS配置，包括将应用程序的顶级模块整合在一起。 默认情况下，此模块名为“AEMAngularApp”，负责生成该模块的脚本可在/libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp上找到（并覆盖）。

应用程序初始化的一部分涉及指定应用程序所依赖的AngularJS模块。 应用程序使用的模块列表由位于/libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp的脚本指定，并可由您自己的应用程序的页面组件覆盖，以拉入您的应用程序需要的任何其他AngularJS模块。 例如，将上述脚本与Geometrixx实现(位于/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp)进行比较。

为了支持在应用程序中的不同状态之间进行导航，角度式应用程序模块脚本会迭代您顶级应用程序页面的所有子页面以生成一组“路由”，并在Angular的$routeProvider服务上配置每条路径。 有关实际操作情况的示例，请查看由Geometrixx Outdoors应用程序范例生成的角度式应用程序模块脚本：（链接需要本地实例）[http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

深入到生成的AEMAngularApp，您将找到一系列指定的路由：

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

以上示例特别说明了将参数作为路径的一部分进行传递的示例。 在此示例中，我们指示当请求满足指定模式(/content/phonegap/geometrixx-outdoors/en/home/products/:id)的路径时，它应由home/products.template.html模板处理，并使用“contentphonegapgeometrixxoutdoorshomeproducts”控制器。

templateUrl属性指定了请求此路由时要加载的模板。 此模板将包含页面中包含的AEM组件的HTML，以及连接应用程序客户端所需的任何AngularJS指令。 有关Geometrixx组件中AngularJS指令的示例，请查看轻扫——轮盘的template.jsp(/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp)的第45行。

## 页面控制器{#page-controllers}

在Angular自己的单词中，“控制器是用于扩展角范围的JavaScript构造函数。” ([source](https://docs.angularjs.org/guide/controller))AEM应用程序中的每页都自动连接到控制器，该控制器可由指定`angular`的`frameworkType`的任何控制器进行增强。 以ng-text组件为例(/libs/mobileapps/components/angular/ng-text)，它包括cq:template节点，它确保每次将此组件添加到页面时都包含这个重要属性。

有关更复杂的控制器示例，请打开ng-template-page controller.jsp脚本（位于/apps/geometrixx-outdoors-app/components/angular/ng-template-page）。 其中特别感兴趣的是执行时生成的javascript代码，其呈现如下：

```xml
// Controller for page 'products'
.controller('contentphonegapgeometrixxoutdoorsenhomeproducts', ['$scope', '$http', '$routeParams',
    function($scope, $http, $routeParams) {
        var sku = $routeParams.id;
        var productPath = '/' + sku.substring(0, 2) + '/' + sku.substring(0, 4) + '/' + sku;
        var data = $http.get('home/products' + productPath + '.angular.json' + cacheKiller);

        /* ng-product component controller (path: content-par/ng-product) */
        data.then(function(response) {
            $scope.contentparngproduct = response.data["content-par/ng-product"].items;
        });

        /* ng-image component controller (path: content-par/ng-product/ng-image) */
        data.then(function(response) {
            $scope.contentparngproductngimage = response.data["content-par/ng-product/ng-image"].items;
        });
    }
])
```

在上例中，您将注意到我们从`$routeParams`服务中选取一个参数，然后将其按摩到存储JSON数据的目录结构中。 通过以这种方式处理sku `id`，我们能够提供单个产品模板，该模板可以呈现可能数千个不同产品的产品数据。 这是一个可扩展性更强的模型，它要求在（可能）庞大的产品数据库中的每个项目都使用单独的路由。

此处还有两个组件：ng-product通过它从上述`$http`调用中提取的数据扩大范围。 此页上还有一个ng图像，该图像反过来又用它从响应中检索的值来扩大范围。 凭借Angular的`$http`服务，每个组件都将耐心等待，直到请求完成，并实现它所创造的承诺。

## 后续步骤 {#the-next-steps}

了解单页应用程序后，请参阅[使用PhoneGap CLI](/help/mobile/phonegap-apps-pg-cli.md)开发应用程序。
