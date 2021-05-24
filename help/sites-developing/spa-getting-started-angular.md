---
title: AEM SPA快速入门 — Angular
seo-title: AEM SPA快速入门 — Angular
description: 本文提供了一个SPA应用程序示例，介绍了它的组合方式，并允许您使用Angular框架快速启动并运行自己的SPA。
seo-description: 本文提供了一个SPA应用程序示例，介绍了它的组合方式，并允许您使用Angular框架快速启动并运行自己的SPA。
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
exl-id: 9528d92b-0989-4e2d-83be-ba6c07c845e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 2%

---

# AEM中的SPA快速入门 — Angular{#getting-started-with-spas-in-aem-angular}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用SPA框架构建站点，而作者则希望在AEM中无缝编辑使用SPA框架构建的站点的内容。

SPA创作功能提供了一个全面的解决方案，可在AEM中支持SPA。 本文介绍了Angular框架上的一个简化的SPA应用程序，并说明了它的组合方式，使您能够快速启动并运行自己的SPA。

>[!NOTE]
>
>本文基于Angular框架。 有关React框架的相应文档，请参阅[AEM中的SPA快速入门 — React](/help/sites-developing/spa-getting-started-react.md)。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染(例如，React或Angular)的项目，推荐使用SPA编辑器解决方案。

## 简介 {#introduction}

本文概述了简单SPA的基本功能以及运行运行所需了解的最低值。

有关SPA在AEM中工作方式的更多详细信息，请参阅以下文档：

* [SPA简介和演练](/help/sites-developing/spa-walkthrough.md)
* [SPA创作简介](/help/sites-developing/spa-overview.md)
* [SPA Blueprint](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>为了能够在SPA中创作内容，内容必须存储在AEM中并由内容模型公开。
>
>如果在AEM之外开发的SPA不遵守内容模型合同，则该将不可授权。

本文档将介绍简化的SPA的结构并说明其工作方式，以便您能够将此理解应用于您自己的SPA。

## 依赖关系、配置和构建{#dependencies-configuration-and-building}

除了预期的Angular依赖关系之外，示例SPA还可以利用其他库来更高效地创建SPA。

### 依赖关系 {#dependencies}

`package.json`文件定义了整个SPA包的要求。 此处列出了所需的最低AEM依赖项。

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

利用`aem-clientlib-generator`可在构建过程中自动创建客户端库。

`"aem-clientlib-generator": "^1.4.1",`

有关该报表包的更多详细信息，请在GitHub上找到[此处](https://github.com/wcm-io-frontend/aem-clientlib-generator)。

>[!CAUTION]
>
>所需`aem-clientlib-generator`的最低版本为1.4.1。

`aem-clientlib-generator`在`clientlib.config.js`文件中进行配置，如下所示。

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

实际构建应用程序时，除了使用aem-clientlib-generator自动创建客户端库外，还会利用[Webpack](https://webpack.js.org/)进行转换。 因此，build命令将类似于：

`"build": "ng build --build-optimizer=false && clientlib",`

生成后，可将包上传到AEM实例。

### AEM 项目原型 {#aem-project-archetype}

任何AEM项目都应使用[AEM项目原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用React或Angular的SPA项目并利用SPA SDK。

## 应用程序结构{#application-structure}

如前所述，包括依赖项和构建应用程序时，您将获得一个可上传到AEM实例的工作SPA包。

本文档的下一部分将介绍AEM中SPA的结构方式、驱动应用程序的重要文件以及它们如何协同工作。

以简化的图像组件为例，但应用程序的所有组件都基于相同的概念。

### app.module.ts {#app-module-ts}

SPA的入口点是此处显示的`app.module.ts`文件，该文件经过简化，可集中显示重要内容。

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

`app.module.ts`文件是应用程序的起点，包含初始项目配置，并使用`AppComponent`引导应用程序。

#### 静态实例化{#static-instantiation}

使用组件模板静态实例化组件时，必须将值从模型传递到组件的属性。 模型中的值将作为属性传递，以便稍后作为组件属性提供。

### app.component.ts {#app-component-ts}

在`app.module.ts`引导`AppComponent`后，它便可以初始化应用程序，该应用程序将以简化版本显示在此处，以重点关注重要内容。

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

通过处理页面，`app.component.ts`将调用此处以简化版本列出的`main-content.component.ts`。

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

`MainComponent`将摄取页面模型的JSON表示形式，并处理内容以包装/装饰页面的每个元素。 有关`Page`的更多详细信息，请参阅文档[SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501)。

### image.component.ts {#image-component-ts}

`Page`由组件组成。 摄取JSON后，`Page`可以处理这些组件，如`image.component.ts`，如下所示。

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

AEM中SPA的核心思想是将SPA组件映射到AEM组件，并在修改内容时更新组件（反之亦然）。 有关此通信模型的摘要，请参阅文档[SPA Editor概述](/help/sites-developing/spa-overview.md)。

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

`MapTo`方法可将SPA组件映射到AEM组件。 它支持使用单个字符串或字符串数组。

`ImageEditConfig` 是一个配置对象，通过为编辑器提供生成占位符所需的元数据来有助于启用组件的创作功能

如果没有内容，则将提供标签作为占位符来表示空内容。

#### 动态传递的属性{#dynamically-passed-properties}

来自模型的数据将作为组件的属性动态传递。

### image.component.html {#image-component-html}

最后，可以在`image.component.html`中呈现图像。

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## 在SPA组件{#sharing-information-between-spa-components}之间共享信息

单页应用程序中的组件需要定期共享信息。 有几种推荐的方法可以执行此操作，如下所示，它们的复杂性会越来越高。

* **选项1:** 将逻辑集中并广播到必要的组件，例如，将util类用作纯面向对象的解决方案。
* **选项2:** 使用状态库（如NgRx）共享组件状态。
* **选项3:** 通过自定义和扩展容器组件来利用对象层次结构。

## 后续步骤{#next-steps}

有关创建您自己的SPA的分步指南，请参阅[AEM SPA编辑器入门 — WKND事件教程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

有关如何组织您自己开发SPA for AEM的更多信息，请参阅文章[开发SPA for AEM](/help/sites-developing/spa-architecture.md)。

有关动态模型到组件映射以及它如何在AEM的SPA中工作的更多详细信息，请参阅文章[Dynamic Model to Component Mapping for SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

如果您希望在AEM中为React或Angular以外的框架实施SPA，或者只想深入了解SPA SDK for AEM的工作方式，请参阅[SPA Blueprint](/help/sites-developing/spa-blueprint.md)文章。
