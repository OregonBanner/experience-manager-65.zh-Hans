---
title: AEM中的SPA快速入门 — React
description: 本文介绍了一个SPA应用程序示例，说明它是如何组合在一起的，并使您能够使用React框架快速启动和运行自己的SPA。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 552649e7-6054-4ae8-b570-5ba7230e6f19
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 4%

---

# AEM中的SPA快速入门 — React{#getting-started-with-spas-in-aem-react}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用SPA框架构建站点，而创作者希望能够在AEM中顺畅地为使用SPA框架构建的站点编辑内容。

SPA创作功能提供了一个全面的解决方案，用于在AEM中支持SPA。 本文在React框架上提供了一个简化的SPA应用程序，说明了其组合方式，允许您快速启动并运行自己的SPA。

>[!NOTE]
>
>本文基于React框架。 有关Angular框架的相应文档，请参阅 [AEM中的SPA快速入门 — Angular](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>SPA编辑器是推荐的解决方案，适用于需要基于SPA框架的客户端渲染(例如React或Angular)的项目。

## 简介 {#introduction}

本文总结了简单的SPA的基本功能以及运行它所需了解的最少信息。

有关SPA如何在AEM中工作的更多详细信息，请参阅以下文档：

* [SPA 简介和演练](/help/sites-developing/spa-walkthrough.md)
* [SPA创作简介](/help/sites-developing/spa-overview.md)
* [SPA Blueprint](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>为了能够在SPA中创作内容，内容必须存储在AEM中并由内容模型公开。
>
>如果不遵守内容模型合同，则在AEM之外开发的SPA将无法创作。

本文档将介绍使用React框架创建的简化SPA的结构，并说明其工作方式，以使您可将此理解应用于您自己的SPA。

## 依赖项、配置和构建 {#dependencies-configuration-and-building}

除了预期的React依赖项之外，示例SPA还可以使用其他库来更有效地创建SPA。

### 依赖项 {#dependencies}

此 `package.json` 文件定义整个SPA包的要求。 此处列出了正在工作的AEM的最小SPA依赖项。

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

由于此示例基于React框架，因此中存在两个特定于React的依赖项，它们是 `package.json` 文件：

```
react
 react-dom
```

此 `aem-clientlib-generator` 用于在构建过程中自动创建客户端库。

`"aem-clientlib-generator": "^1.4.1",`

可以找到有关它的更多详细信息 [在此处GitHub上](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>的最低版本 `aem-clientlib-generator` 要求为1.4.1。

此 `aem-clientlib-generator` 在中配置 `clientlib.config.js` 文件如下所示。

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### 正在生成 {#building}

实际构建应用程序使用 [网络包](https://webpack.js.org/) 用于转换，并且使用aem-clientlib-generator自动创建客户端库。 因此，构建命令将类似于：

`"build": "webpack && clientlib --verbose"`

构建后，可以将包上传到AEM实例。

### AEM 项目原型 {#aem-project-archetype}

任何 AEM 项目都应使用 [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用 React 或 Angular 的 SPA 项目并利用 SPA SDK。

## 应用程序结构 {#application-structure}

如前所述，包括依赖项和构建应用程序将为您提供一个有效的SPA包，您可以将该包上传到您的AEM实例。

本文档的下一部分将介绍AEM中SPA的结构方式、驱动应用程序的重要文件以及它们如何协同工作。

以简化的图像组件为例，但应用程序的所有组件都基于相同的概念。

### index.js {#index-js}

SPA的入口点为 `index.js` 此处显示的文件被简化为重点介绍重要内容。

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

的主要功能 `index.js` 就是使用 `ReactDOM.render` 函数来确定在DOM中插入应用程序的位置。

这是此函数的标准用法，并非特定于此示例应用程序。

#### 静态实例化 {#static-instantiation}

使用组件模板（例如，JSX）静态实例化组件时，必须将值从模型传递到组件的属性。

### App.js {#app-js}

通过呈现应用程序， `index.js` 调用 `App.js`，此处以简化版的形式显示，重点介绍重要内容。

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` 主要用于封装构成应用程序的根组件。 任何应用程序的入口点是页面。

### Page.js {#page-js}

通过呈现页面， `App.js` 调用 `Page.js` 此处以简化版本列出。

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

在此示例中， `AppPage` 类扩展 `Page`，其中包含随后可以使用的内部内容方法。

此 `Page` 摄取页面模型的JSON表示形式并处理内容以包装/装饰页面的每个元素。 有关更多详情，请参阅 `Page` 可以在文档中找到 [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### Image.js {#image-js}

在呈现页面时，组件(例如 `Image.js` 如下所示，可以渲染。

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

AEM中SPA的核心思想是：将SPA组件映射到AEM组件，并在内容被修改时更新组件（反之亦然）。 查看文档 [SPA编辑器概述](/help/sites-developing/spa-overview.md) 以获取该通信模型的摘要。

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

此 `MapTo` 方法将SPA组件映射到AEM组件。 它支持使用单个字符串或字符串数组。

`ImageEditConfig` 是一个配置对象，它通过为编辑器提供生成占位符所需的元数据来帮助启用组件的创作功能

如果没有内容，则会提供标签作为占位符来表示空内容。

#### 动态传递的属性 {#dynamically-passed-properties}

来自模型的数据将作为组件的属性动态传递。

## 导出可编辑内容 {#exporting-editable-content}

您可以导出组件并使其保持可编辑状态。

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

此 `MapTo` 函数返回 `Component` 这是延伸了所提供的结构的结果 `PageClass` 类名和属性启用创作。 此组件可导出以供稍后在应用程序的标记中实例化。

使用导出时 `MapTo` 或 `withModel` 函数， `Page` 组件，用 `ModelProvider` 组件，通过此组件可让标准组件访问最新版本的页面模型或该页面模型中的精确位置。

欲知更多信息，请参见 [SPA Blueprint文档](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>缺省情况下，使用时接收元件的整个模型 `withModel` 函数。

## 在SPA组件之间共享信息 {#sharing-information-between-spa-components}

单页应用程序中的组件经常需要共享信息。 有几种推荐的方法可以做到这一点，按复杂性递增的顺序如下所示。

* **选项1：** 例如，通过使用React Context将逻辑集中并广播到必要的组件。
* **选项2：** 使用状态库（如Redux）共享组件状态。
* **选项3：** 通过自定义和扩展容器组件来利用对象层次结构。

## 后续步骤 {#next-steps}

有关创建您自己的SPA的分步指南，请参阅 [AEM SPA编辑器快速入门 — WKND事件教程](https://helpx.adobe.com/cn/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

有关如何组织自己来开发SPA for AEM的更多信息，请参阅文章 [开发SPA for AEM](/help/sites-developing/spa-architecture.md).

有关动态模型到组件映射及其如何在AEM中的SPA中工作的更多详细信息，请参阅文章 [SPA的动态模型到组件映射](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

如果您希望在AEM中为React或Angular以外的框架实施SPA，或者只是希望深入了解SPA SDK for AEM的工作原理，请参阅 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 文章。
