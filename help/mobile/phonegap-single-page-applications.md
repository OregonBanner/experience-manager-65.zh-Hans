---
title: 单页应用程序
seo-title: 单页应用程序
description: 请阅读本页，了解单页应用程序，即创建与桌面或移动设备应用程序性能相同的应用程序。
seo-description: 请阅读本页，了解单页应用程序，即创建与桌面或移动设备应用程序性能相同的应用程序。
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 1%

---

# 单页应用程序{#single-page-applications}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

[单页应用程序](https://en.wikipedia.org/wiki/Single-page_application) (SPA)已达到临界质量，被广泛认为是使用Web技术构建无缝体验的最有效模式。通过遵循SPA模式，您可以创建一个与桌面或移动设备应用程序性能相同的应用程序，但由于该应用程序在开放Web标准中的基础，因此可以实现多种设备平台和外形规格。

一般而言，SPA比基于页面的传统网站显示的性能更高，因为它们通常只加载一次&#x200B;**的完整HTML页面（包括CSS、JS和支持字体内容），然后只加载每次应用程序中发生状态更改时所需的内容。**&#x200B;这种状态更改所需的内容可能因所选技术集而异，但通常包括用于替换现有“view”的单个HTML片段，以及执行一个JS代码块以连接新视图并执行任何可能需要的客户端模板渲染。 通过支持模板缓存机制，甚至在使用Adobe PhoneGap时脱机访问模板内容，可以进一步提高此状态更改的速度。

AEM 6.1支持通过AEM应用程序构建和管理SPA。 本文将介绍SPA的概念，以及它们如何利用[AngularJS](https://angularjs.org/)将您的品牌引入应用商店和Google Play。

## AEM应用程序中的SPA {#spa-in-aem-apps}

AEM应用程序中的单页应用程序框架支持AngularJS应用程序的高性能，同时使作者（或其他非技术人员）能够通过触屏优化拖放编辑器环境创建和管理应用程序内容，该环境传统上是用于管理网站的保留环境。 是否已使用AEM构建站点？ 您会发现，使用AEM应用程序重用内容、组件、工作流、资产和权限非常简单。

## AngularJS应用程序模块{#angularjs-application-module}

AEM应用程序可为您处理大部分AngularJS配置，包括将应用程序的顶级模块整合在一起。 默认情况下，此模块名为“AEMAngularApp”，可在/libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp上找到（并覆盖）负责生成此模块的脚本。

应用程序初始化的一部分涉及指定应用程序所依赖的AngularJS模块。 您的应用程序使用的模块列表由位于/libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp的脚本指定，并且您自己的应用程序的页面组件可以覆盖该列表，以提取应用程序需要的任何其他AngularJS模块。 例如，将上述脚本与Geometrixx实现(位于/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp)进行比较。

为支持在应用程序的不同状态之间导航，angular应用程序模块脚本会遍历顶级应用程序页面的所有子页面，以生成一组“路由”，并在Angular的$routeProvider服务上配置每个路径。 有关其在实践中的外观示例，请参阅由angular应用程序示例生成的Geometrixx Outdoors应用程序模块脚本：（链接需要本地实例）[http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

在查找生成的AEMAngularApp后，您会找到一系列指定的路由，如下所示：

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

上述示例特别说明了作为路径一部分传递参数的示例。 在此示例中，我们指示当请求满足指定模式(/content/phonegap/geometrixx-outdoors/en/home/products/:id)的路径时，应由home/products.template.html模板处理该路径，并使用“contentphonegemetrixxoutdoorsenhomeproducts”控制器。

templateUrl属性指定了在请求此路由时要加载的模板。 此模板将包含页面上包含的AEM组件中的HTML，以及连接应用程序客户端所需的任何AngularJS指令。 有关Geometrixx组件中AngularJS指令的示例，请查看轻扫轮播的template.jsp(/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp)的第45行。

## 页面控制器{#page-controllers}

用Angular自己的话来说，“控制器是一个JavaScript构造函数，用于扩大Angular范围。” ([source](https://docs.angularjs.org/guide/controller))AEM应用程序中的每个页面都自动连接到控制器，该控制器可以被任何指定`angular`的`frameworkType`的控制器增强。 以ng-text组件为例(/libs/mobileapps/components/angular/ng-text)，包括cq:template节点，该节点可确保每次将此组件添加到页面时，都包含此重要属性。

有关更复杂的控制器示例，请打开ng-template-page controller.jsp脚本(位于/apps/geometrixx-outdoors-app/components/angular/ng-template-page)。 特别值得关注的是它在执行时生成的javascript代码，该代码会按如下方式呈现：

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

在上例中，您会注意到，我们正在从`$routeParams`服务中获取一个参数，然后将其按摩到存储JSON数据的目录结构中。 通过以这种方式处理SKU `id`，我们能够提供单个产品模板，该模板可以呈现潜在数千个不同产品的产品数据。 这是一个扩展性更强的模型，它要求在（可能）庞大的产品数据库中为每个项目提供单独的路径。

此处还包含两个组件：ng-product使用它从上述`$http`调用中提取的数据来扩展范围。 此页面上还有一个ng图像，该图像反过来也通过从响应中检索的值来扩展范围。 借助Angular的`$http`服务，每个组件将耐心等待，直到请求完成并履行它创建的承诺。

## 后续步骤 {#the-next-steps}

了解单页应用程序后，请参阅[使用PhoneGap CLI开发应用程序](/help/mobile/phonegap-apps-pg-cli.md)。
