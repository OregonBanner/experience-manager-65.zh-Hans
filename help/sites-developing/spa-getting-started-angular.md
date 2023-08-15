---
title: AEM中的SPA快速入门 — Angular
seo-title: Getting Started with SPAs in AEM - Angular
description: 本文介绍了一个SPA应用程序示例，说明它是如何组合在一起的，并使您能够使用Angular框架快速启动和运行自己的SPA。
seo-description: This article presents a sample SPA application, explains how it is put together, and lets you get up-and-running with your own SPA quickly using the Angular framework.
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
exl-id: 9528d92b-0989-4e2d-83be-ba6c07c845e2
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 6%

---

# AEM中的SPA快速入门 — Angular{#getting-started-with-spas-in-aem-angular}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用SPA框架构建站点，而创作者希望能够在AEM中顺畅地为使用SPA框架构建的站点编辑内容。

SPA创作功能提供了一个全面的解决方案，用于在AEM中支持SPA。 本文在Angular框架上提供了一个简化的SPA应用程序，并说明它是如何进行组合，使您能够快速启动和运行自己的SPA。

>[!NOTE]
>
>本文基于Angular框架。 有关React框架的相应文档，请参阅 [AEM中的SPA快速入门 — React](/help/sites-developing/spa-getting-started-react.md).

>[!NOTE]
>
>SPA编辑器是推荐的解决方案，适用于需要基于SPA Framework的客户端渲染(例如React或Angular)的项目。

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

本文档将逐步介绍简化SPA的结构，并说明其工作方式，以便您将此理解应用于自己的SPA。

## 依赖项、配置和构建 {#dependencies-configuration-and-building}

除了预期的Angular依赖关系之外，示例SPA还可以利用其他库来更有效地创建SPA。

### 依赖项 {#dependencies}

此 `package.json` 文件定义整个SPA包的要求。 此处列出了最低必需的AEM依赖项。

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
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
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
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

实际构建应用程序时会利用 [网络包](https://webpack.js.org/) 用于转换，并且使用aem-clientlib-generator自动创建客户端库。 因此，构建命令将类似于：

`"build": "ng build --build-optimizer=false && clientlib",`

构建后，可以将包上传到AEM实例。

### AEM 项目原型 {#aem-project-archetype}

任何 AEM 项目都应使用 [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用 React 或 Angular 的 SPA 项目并利用 SPA SDK。

## 应用程序结构 {#application-structure}

如前所述，包括依赖项和构建应用程序将为您提供一个有效的SPA包，您可以将该包上传到您的AEM实例。

本文档的下一部分将介绍如何构建AEM中的SPA、驱动应用程序的重要文件以及它们如何协同工作。

以简化的图像组件为例，但应用程序的所有组件都基于相同的概念。

### app.module.ts {#app-module-ts}

SPA的入口点为 `app.module.ts` 此处显示的文件被简化为重点介绍重要内容。

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/aem-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

此 `app.module.ts` file是应用程序的起点，包含初始项目配置和使用 `AppComponent` 以引导应用程序。

#### 静态实例化 {#static-instantiation}

使用组件模板静态实例化组件时，必须将值从模型传递到组件的属性。 模型中的值作为属性进行传递，以便以后作为组件属性使用。

### app.component.ts {#app-component-ts}

一次 `app.module.ts` bootstraps `AppComponent`，然后它可以初始化应用程序，此处以简化版的形式显示了应用程序，以便重点关注重要内容。

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

通过处理页面， `app.component.ts` 调用 `main-content.component.ts` 此处以简化版本列出。

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

此 `MainComponent` 摄取页面模型的JSON表示形式并处理内容以包装/装饰页面的每个元素。 有关更多详情，请参阅 `Page` 可以在文档中找到 [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### image.component.ts {#image-component-ts}

此 `Page` 由组件组成。 摄取JSON后， `Page` 可以处理这些组件，例如 `image.component.ts` 如下所示。

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

AEM中SPA的核心思想是：将SPA组件映射到AEM组件，并在内容被修改时更新组件（反之亦然）。 查看文档 [SPA编辑器概述](/help/sites-developing/spa-overview.md) 以获取该通信模型的摘要。

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

此 `MapTo` 方法将SPA组件映射到AEM组件。 它支持使用单个字符串或字符串数组。

`ImageEditConfig` 是一个配置对象，它通过为编辑器提供生成占位符所需的元数据来帮助启用组件的创作功能

如果没有内容，则会提供标签作为占位符来表示空内容。

#### 动态传递的属性 {#dynamically-passed-properties}

来自模型的数据将作为组件的属性动态传递。

### image.component.html {#image-component-html}

最后，可以在中呈现图像 `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## 在SPA组件之间共享信息 {#sharing-information-between-spa-components}

单页应用程序中的组件经常需要共享信息。 有几种推荐的方法可以做到这一点，按复杂性递增的顺序如下所示。

* **选项1：** 例如，通过使用util类作为纯面向对象的解决方案，将逻辑集中并广播到必要的组件。
* **选项2：** 使用状态库（如NgRx）共享组件状态。
* **选项3：** 通过自定义和扩展容器组件来利用对象层次结构。

## 后续步骤 {#next-steps}

有关创建您自己的SPA的分步指南，请参阅 [AEM SPA编辑器快速入门 — WKND事件教程](https://helpx.adobe.com/cn/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

有关如何组织自己来开发SPA for AEM的更多信息，请参阅文章 [开发SPA for AEM](/help/sites-developing/spa-architecture.md).

有关动态模型到组件映射及其如何在AEM中的SPA中工作的更多详细信息，请参阅文章 [SPA的动态模型到组件映射](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

如果您希望在AEM中为React或Angular以外的框架实施SPA，或者只是希望深入了解SPA SDK for AEM的工作原理，请参阅 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 文章。
