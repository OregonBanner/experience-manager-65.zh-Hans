---
title: AEM中的SPA入门——反应
seo-title: AEM中的SPA入门——反应
description: 本文展示了一个SPA应用程序示例，介绍了它的组合方式，并允许您使用React框架快速启动并运行自己的SPA。
seo-description: 本文展示了一个SPA应用程序示例，介绍了它的组合方式，并允许您使用React框架快速启动并运行自己的SPA。
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 1%

---


# AEM中的SPA入门——反应{#getting-started-with-spas-in-aem-react}

单页应用程序(SPA)可以为网站用户优惠引人入胜的体验。 开发人员希望能够使用SPA框架构建站点，作者希望在AEM内无缝编辑内容，使用SPA框架构建站点。

SPA创作功能优惠了用于支持AEM内SPA的全面解决方案。 本文介绍React框架上简化的SPA应用程序，并说明它的组合方式，使您能快速启动并运行自己的SPA。

>[!NOTE]
>
>本文基于React框架。 有关角度框架的相应文档，请参 [阅AEM中SPA快速入门——角度](/help/sites-developing/spa-getting-started-angular.md)。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染（如“反应”或“角度”）的项目，建议使用SPA编辑器。

## 简介 {#introduction}

本文概括了简单SPA的基本功能，以及使您的SPA运行所需的最低要求。

有关AEM中SPA的工作方式的详细信息，请参阅以下文档:

* [SPA简介和演练](/help/sites-developing/spa-walkthrough.md)
* [SPA创作简介](/help/sites-developing/spa-overview.md)
* [SPA Blueprint](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>为了能够在SPA中创作内容，内容必须存储在AEM中并由内容模型公开。
>
>如果AEM之外开发的SPA不遵守内容模型合同，则该SPA将不可授权。

此文档将介绍使用React框架创建的简化SPA的结构并说明其工作方式，以便您将此理解应用于您自己的SPA。

## 依赖关系、配置和构建 {#dependencies-configuration-and-building}

除了预期的React依赖关系外，示例SPA还可以利用其他库来提高SPA的创建效率。

### 依赖关系 {#dependencies}

文 `package.json` 件定义整个SPA包的要求。 此处列出了工作SPA的最低AEM依赖关系。

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

由于此示例基于React框架，因此在文件中必须有两个React-specific依赖 `package.json` 项：

```
react
 react-dom
```

利用 `aem-clientlib-generator` 该工具，可以在构建过程中自动创建客户端库。

`"aem-clientlib-generator": "^1.4.1",`

有关该功能的更多详细信 [息，请访问](https://github.com/wcm-io-frontend/aem-clientlib-generator)。

>[!CAUTION]
>
>所需的最低 `aem-clientlib-generator` 版本为1.4.1。

在文 `aem-clientlib-generator` 件中进行 `clientlib.config.js` 如下配置。

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

实际构建应用程序 [除了aem](https://webpack.js.org/) -clientlib-generator用于自动创建客户端库外，还利用Webpack进行转换。 因此，build命令将类似于：

`"build": "webpack && clientlib --verbose"`

构建后，包可以上传到AEM实例。

### AEM 项目原型 {#aem-project-archetype}

任何AEM项目都应利用 [AEM Project](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)Archetype，它支持使用React或Angular的SPA项目并利用SPA SDK。

## 应用程序结构 {#application-structure}

如前所述，包括依赖项和构建应用程序将留给您一个可上传到AEM实例的工作SPA包。

本文档的下一节将介绍AEM中SPA的结构、驱动应用程序的重要文件以及它们如何协同工作。

以简化的图像组件为例，但应用程序的所有组件都基于相同的概念。

### index.js {#index-js}

进入SPA的入口点当然是此处显示的 `index.js` 文件经过简化以集中处理重要内容。

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

其主要功能 `index.js` 是利用该功 `ReactDOM.render` 能确定在DOM中插入应用程序的位置。

这是此函数的标准使用，并非此示例应用程序所特有的。

#### 静态实例化 {#static-instantiation}

当使用组件模板（如JSX）静态实例化组件时，必须将值从模型传递到组件的属性。

### App.js {#app-js}

通过呈现应用程 `index.js` 序 `App.js`调用，此处以简化版本显示以专注于重要内容。

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` 主要用于包装构成应用程序的根组件。 任何应用程序的入口点都是页面。

### Page.js {#page-js}

通过呈现页面， `App.js` 以简 `Page.js` 化版本列出的调用。

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

在此示例中 `AppPage` ，类 `Page`扩展，它包含随后可以使用的内部内容方法。

收 `Page` 集页面模型的JSON表示形式并处理内容以包装／装饰页面的每个元素。 有关此项的更 `Page` 多详细信息，请参 [阅文档SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501)。

### Image.js {#image-js}

呈现页面后，可以呈现 `Image.js` 如下组件。

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

AEM中SPA的核心思想是将SPA组件映射到AEM组件，并在内容被修改时更新组件（反之亦然）。 有关此通 [信模型的摘要](/help/sites-developing/spa-overview.md) ，请参阅文档SPA编辑器概述。

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

该方 `MapTo` 法将SPA组件映射到AEM组件。 它支持使用单个字符串或字符串数组。

`ImageEditConfig` 是一个配置对象，它通过为编辑器提供生成占位符所需的元数据来帮助启用组件的创作功能

如果没有内容，则标签将作为占位符提供以表示空内容。

#### 动态传递的属性 {#dynamically-passed-properties}

来自模型的数据将作为组件的属性动态传递。

## 导出可编辑内容 {#exporting-editable-content}

您可以导出组件并使其保持可编辑性。

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

该 `MapTo` 函数返回 `Component` 一个合成的结果，该合成扩展了所提供的类名 `PageClass` 和属性，这些属性支持创作。 此组件可以导出，以后在应用程序的标记中实例化。

当使用或函 `MapTo` 数导 `withModel` 出时，该组件会与一个组件打包，该组件 `Page``ModelProvider` 提供标准组件对页面模型最新版本的访问或该页面模型中的精确位置。

有关详细信息，请参 [阅SPA Blueprint文档](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743)。

>[!NOTE]
>
>默认情况下，使用函数时将收到组件的整个模 `withModel` 型。

## 在SPA组件之间共享信息 {#sharing-information-between-spa-components}

单页应用程序中的组件需要定期共享信息。 有几种推荐的方法可以这样做，其复杂程度按顺序增加如下所示。

* **选项1:** 将逻辑集中化并广播到必要的组件，例如，使用React Context。
* **选项2:** 使用状态库（如Redux）共享组件状态。
* **选项3:** 通过自定义和扩展容器组件来利用对象层次结构。

## 后续步骤 {#next-steps}

有关创建您自己的SPA的分步指南，请参 [阅AEM SPA编辑器入门- WKND事件教程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

有关如何组织您自己为AEM开发SPA的更多信息，请参阅为AEM开 [发SPA一文](/help/sites-developing/spa-architecture.md)。

有关动态模型到组件映射以及它在AEM中的SPA中的工作方式的更多详细信息，请参 [阅SPA的动态模型到组件映射文章](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

如果您希望在AEM中为除React或Angular之外的框架实施SPA，或只是希望深入了解AEM的SDK的工作方式，请参阅 [SPA Blueprint文章](/help/sites-developing/spa-blueprint.md) 。
