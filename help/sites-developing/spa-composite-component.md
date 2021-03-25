---
title: 在SPA中组合组件
description: 了解如何创建您自己的复合组件，这些组件由其他组件组成，可与AEM单页应用程序(SPA)编辑器一起使用。
translation-type: tm+mt
source-git-commit: 431bed450ed5b0239d9191dcf061f01e64b8981a
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---


# SPA {#composite-components-in-spas}中的复合组件

通过将多个基本组件组合到单个组件中，复合组件充分利用了AEM组件的模块化特性。 常用的复合组件用例是卡组件，由图像和文本组件的组合构成。

当在AEM单页应用程序(SPA)编辑器框架中正确实现复合组件时，内容作者可以像拖放任何其他组件一样拖放这些组件，但仍然能够单独编辑组成复合组件的每个组件。

本文演示如何向单页应用程序添加复合组件以与AEM SPA Editor无缝协作。

## 用例 {#use-case}

本文将以典型卡组件为例进行说明。 卡是许多数字体验的常用UI元素，通常由图像和关联文本或题注组成。 作者希望能够拖放整张卡，但能够单独编辑卡的图像并自定义相关文本。

## 前提条件 {#prerequisites}

支持复合组件用例的以下模型需要以下先决条件。

* 您的AEM开发实例正在带有示例项目的端口4502上本地运行。
* 在AEM中启用了可编辑的正常外部React应用程序[。](spa-edit-external.md)
* React应用程序使用RemotePage组件加载到AEM编辑器[中。](spa-remote-page.md)

## 将复合组件添加到SPA {#adding-composite-components}

根据AEM中的SPA实施，有三种不同的实现组件模型。

* [您的AEM项目中不存在该组件。](#component-does-not-exist)
* [该组件存在于您的AEM项目中，但其必需内容不存在。](#content-does-not-exist)
* [组件及其必需内容都存在于您的AEM项目中。](#both-exist)

以下部分以卡组件为例说明了如何实现每种情况。

### 您的AEM项目中不存在该组件。{#component-does-not-exist}

开始，方法是创建将构成复合组件的组件，即图像及其文本的组件。

1. 在您的AEM项目中创建文本组件。
1. 在组件的`editConfig`节点中，从项目添加相应的`resourceType`。

   ```text
    resourceType: 'wknd-spa/components/text' 
   ```

1. 使用`withMappable`帮助程序可启用组件编辑。

   ```text
   export const AEMText = withMappable(Text, TextEditConfig); 
   ```

文本组件将类似于以下内容。

```javascript
import React from 'react';
import { withMappable } from '@adobe/aem-react-editable-components';

export const TextEditConfig = {
  emptyLabel: 'Text',
  isEmpty: function(props) {
    return !props || !props.text || props.text.trim().length < 1;
  },
  resourceType: 'wknd-spa/components/text'
};

export const Text = ({ cqPath, richText, text }) => {
  const richTextContent = () => (
    <div className="aem_text"
      id={cqPath.substr(cqPath.lastIndexOf('/') + 1)}
      data-rte-editelement
      dangerouslySetInnerHTML={{__html: text}} />
  );
  return richText ? richTextContent() : (
     <div className="aem_text">{text}</div>
  );
};

export const AEMText = withMappable(Text, TextEditConfig);
```

如果以类似方式创建图像组件，则可以将它与`AEMText`组件合并为新卡组件，并将图像和文本组件用作子组件。

```javascript
import React from 'react';
import { AEMText } from './AEMText';
import { AEMImage } from './AEMImage';

export const AEMCard = ({ pagePath, itemPath}) => (
  <div>
    <AEMText
       pagePath={pagePath}
       itemPath={`text`} />
    <AEMImage
       pagePath={pagePath}
       itemPath={`image`} />
   </div>
);
```

现在，此生成的复合组件可放置在应用程序中的任意位置，并将在SPA编辑器中为文本和图像组件添加占位符。 在下面的示例中，卡组件将添加到标题下方的主组件中。

```javascript
function Home() {
  return (
    <div className="Home">
      <h2>Current Adventures</h2>
      <AEMCard
        pagePath='/content/wknd-spa/home' />
    </div>
  );
}
```

这将在编辑器中显示文本和图像的空占位符。 使用编辑器输入这些值时，这些值将存储在指定的页面路径（即`/content/wknd-spa/home`）的根级别上，其名称在`itemPath`中指定。

![在编辑器中合成卡组件](assets/composite-card.png)

### 该组件存在于您的AEM项目中，但其必需内容不存在。{#content-does-not-exist}

在这种情况下，卡组件已在包含标题和图像节点的AEM项目中创建。 子节点（文本和图像）具有相应的资源类型。

![卡组件的节点结构](assets/composite-node-structure.png)

然后，您可以将其添加到SPA并检索其内容。

1. 在SPA中为此创建相应组件。 确保将子组件映射到SPA项目中相应的AEM资源类型。 在此示例中，我们使用与上例中详细的[相同的`AEMText`和`AEMImage`组件。](#component-does-not-exist)

   ```javascript
   import React from 'react';
   import { Container, withMappable, MapTo } from '@adobe/aem-react-editable-components';
   import { Text, TextEditConfig } from './AEMText';
   import Image, { ImageEditConfig } from './AEMImage';
   
   export const AEMCard = withMappable(Container, {
     resourceType: 'wknd-spa/components/imagecard'
   });
   
   MapTo('wknd-spa/components/text')(Text, TextEditConfig);
   MapTo('wknd-spa/components/image')(Image, ImageEditConfig);
   ```

1. 由于`imagecard`组件没有内容，因此请将卡添加到页面。 在SPA中包含AEM的现有容器。
   * 如果AEM项目中已有容器，则我们可以将此组件包含在SPA中，然后从AEM将组件添加到容器。
   * 确保将卡组件映射到SPA中的相应资源类型。

   ```javascript
   <ResponsiveGrid
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid' />
   ```

1. 将创建的`wknd-spa/components/imagecard`组件添加到页面模板中容器组件[的允许组件。](/help/sites-authoring/templates.md)

现在，可以在AEM编辑器中将`imagecard`组件直接添加到容器。

![在编辑器中合成卡](assets/composite-card.gif)

### 组件及其必需内容都存在于您的AEM项目中。{#both-exist}

如果内容存在于AEM中，则可以通过提供内容的路径直接将其包含在SPA中。

```javascript
<AEMCard
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid/imagecard' />
```

![节点结构中的复合路径](assets/composite-path.png)

`AEMCard`组件与上一个用例中定义的[相同。](#content-does-not-exist) 在此，AEM项目中上述位置中定义的内容将包含在SPA中。
