---
title: SPA 中的复合组件
description: 了解如何创建自己的复合组件，这些组件由使用AEM单页应用程序(SPA)编辑器的其他组件组成。
exl-id: 02b6c698-d169-467a-9168-9fa6181bed6c
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---

# SPA 中的复合组件 {#composite-components-in-spas}

复合组件通过将多个基础组件组合到一个组件中，来使用AEM组件的模块化特性。 常见的复合组件用例是卡组件，由图像和文本组件组合而成。

在AEM单页应用程序(SPA)编辑器框架中正确实施复合组件后，内容作者可以像拖放任何其他组件一样拖放此类组件，但仍然能够单独编辑构成复合组件的每个组件。

本文演示了如何将复合组件添加到单页应用程序，以便与AEM SPA编辑器无缝地配合使用。

## 用例 {#use-case}

本文将以典型卡组件作为示例用例。 信息卡是许多数字体验的公用UI元素，通常由图像和相关文本或标题组成。 作者希望能够拖放整个卡片，但能够单独编辑卡片的图像并自定义关联的文本。

## 前提条件 {#prerequisites}

以下支持复合组件用例的模型需要以下先决条件。

* 您的AEM开发实例正在带有示例项目的端口4502上本地运行。
* 您有一个正常工作的外部React应用程序 [已启用以便在AEM中编辑。](spa-edit-external.md)
* 在AEM编辑器中加载React应用程序 [使用RemotePage组件。](spa-remote-page.md)

## 将复合组件添加到SPA {#adding-composite-components}

实施复合组件有三种不同的模型，具体取决于AEM中的SPA实施。

* [您的AEM项目中不存在该组件。](#component-does-not-exist)
* [您的AEM项目中存在该组件，但其必需的内容不存在。](#content-does-not-exist)
* [AEM项目中同时存在该组件及其必需内容。](#both-exist)

以下部分提供了使用卡组件作为示例来实施每个用例的示例。

### 您的AEM项目中不存在该组件。 {#component-does-not-exist}

首先，创建将构成复合组件的组件，即图像及其文本的组件。

1. 在AEM项目中创建文本组件。
1. 添加相应的 `resourceType` 从组件的项目 `editConfig` 节点。

   ```text
    resourceType: 'wknd-spa/components/text' 
   ```

1. 使用 `withMappable` 帮助程序启用组件的编辑。

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

如果以类似方式创建图像组件，则可以将其与 `AEMText` 组件放入新的卡组件，并将图像和文本组件用作子组件。

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

生成的复合组件现在可以放置在应用程序中的任意位置，并且将在SPA编辑器中为文本和图像组件添加占位符。 在以下示例中，信息卡组件被添加到标题下的主页组件。

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

这将在编辑器中显示文本和图像的空占位符。 使用编辑器输入这些字段的值时，它们存储在指定的页面路径(即 `/content/wknd-spa/home`  在根级别使用 `itemPath`.

![编辑器中的复合卡组件](assets/composite-card.png)

### 您的AEM项目中存在该组件，但其必需的内容不存在。 {#content-does-not-exist}

在这种情况下，卡组件已在包含标题和图像节点的AEM项目中创建了。 子节点（文本和图像）具有相应的资源类型。

![卡组件的节点结构](assets/composite-node-structure.png)

然后，您可以将其添加到SPA并检索其内容。

1. 在SPA中为此创建对应的组件。 确保子组件映射到SPA项目中的相应AEM资源类型。 在此示例中，我们使用相同的 `AEMText` 和 `AEMImage` 详细组件 [在上一个案例中。](#component-does-not-exist)

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

1. 因为没有内容 `imagecard` 组件中，将卡添加到页面中。 在SPA中包含来自AEM的现有容器。
   * 如果AEM项目中已有容器，我们可以改为将此容器包含在SPA中，并改为从AEM将组件添加到容器中。
   * 确保卡组件映射到SPA中相应的资源类型。

   ```javascript
   <ResponsiveGrid
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid' />
   ```

1. 添加创建的 `wknd-spa/components/imagecard` 组件到容器组件允许的组件 [在页面模板中。](/help/sites-authoring/templates.md)

现在， `imagecard` 组件可以在AEM编辑器中直接添加到容器中。

![编辑器中的复合信息卡](assets/composite-card.gif)

### AEM项目中同时存在该组件及其必需内容。 {#both-exist}

如果内容存在于AEM中，则通过提供内容的路径可以直接将其包含在SPA中。

```javascript
<AEMCard
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid/imagecard' />
```

![节点结构中的复合路径](assets/composite-path.png)

此 `AEMCard` 组件与定义的组件相同 [在上一个用例中。](#content-does-not-exist) 此处，在AEM项目的上述位置中定义的内容包含在SPA中。
