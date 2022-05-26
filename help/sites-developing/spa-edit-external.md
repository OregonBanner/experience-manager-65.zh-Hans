---
title: 在 AEM 中编辑外部 SPA
description: 本文档介绍了将独立SPA上传到AEM实例、添加内容的可编辑部分以及启用创作的建议步骤。
exl-id: 25236af4-405a-4152-8308-34d983977e9a
source-git-commit: 237de641ba02705f8171b1526946a4dc1b60b6a3
workflow-type: tm+mt
source-wordcount: '2392'
ht-degree: 1%

---

# 在 AEM 中编辑外部 SPA {#editing-external-spa-within-aem}

在决定要在外部SPA与AEM之间实现的集成级别时，您通常需要能够在AEM中编辑和查看SPA。

## 概述 {#overview}

本文档介绍了将独立SPA上传到AEM实例、添加内容的可编辑部分以及启用创作的建议步骤。

## 前提条件 {#prerequisites}

先决条件很简单。

* 确保AEM实例在本地运行。
* 使用创建基本AEM SPA项目 [AEM项目原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties)
   * 这将构成AEM项目的基础，该项目将进行更新以包含外部SPA。
   * 对于本文档中的示例，我们使用 [WKND SPA项目。](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor)
* 您希望手上集成的外部React SPA正常运行。

## 将SPA上传到AEM项目 {#upload-spa-to-aem-project}

首先，您需要将外部SPA上传到AEM项目。

1. 替换 `src` 在 `/ui.frontend` 项目文件夹和React应用程序的 `src` 文件夹。
1. 在应用程序的 `package.json` 在 `/ui.frontend/package.json` 文件。
   * 确保SPA SDK依赖项为 [推荐版本。](spa-getting-started-react.md#dependencies)
1. 在 `/public` 文件夹。
1. 包括在 `/public/index.html` 文件。

## 配置远程SPA {#configure-remote-spa}

由于外部SPA是AEM项目的一部分，因此需要在AEM中对其进行配置。

### 包含AdobeSPA SDK包 {#include-spa-sdk-packages}

要利用AEM SPA功能，需依赖以下三个包。

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

`@adobe/aem-spa-page-model-manager` 提供用于初始化模型管理器和从AEM实例检索模型的API。 然后，此模型可用于使用 `@adobe/aem-react-editable-components` 和 `@adobe/aem-spa-component-mapping`.

#### 安装 {#installation}

运行以下npm命令以安装所需的包。

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### ModelManager初始化 {#model-manager-initialization}

在应用程序呈现之前， [`ModelManager`](spa-blueprint.md#pagemodelmanager) 需要进行初始化以处理AEM的创建 `ModelStore`.

这需要在 `src/index.js` 文件，或应用程序根目录的任何位置。

为此，我们可以使用 `initializationAsync` 由提供的API `ModelManager`.

以下屏幕截图显示了如何启用初始化 `ModelManager` 在简单的React应用程序中。 唯一的限制是 `initializationAsync` 需要先调用 `ReactDOM.render()`.

![初始化ModelManager](assets/external-spa-initialize-modelmanager.png)

在本例中， `ModelManager` 已初始化，并且为空 `ModelStore` 创建时。

`initializationAsync` 可以选择接受 `options` 对象作为参数：

* `path`  — 初始化时，将获取定义路径上的模型，并将其存储在 `ModelStore`. 这可用于获取 `rootModel` 初始化时。
* `modelClient`  — 允许提供负责获取模型的自定义客户端。
* `model` - A `model` 作为参数传递的对象，通常在 [使用SSR。](spa-ssr.md)

### AEM可创作叶组件 {#authorable-leaf-components}

1. 创建/标识将为其创建可授权的React组件的AEM组件。 在此示例中，我们使用的是WKND项目的文本组件。

   ![WKND文本组件](assets/external-spa-text-component.png)

1. 在SPA中创建一个简单的React文本组件。 在本例中，新文件 `Text.js` 已使用以下内容创建。

   ![Text.js](assets/external-spa-textjs.png)

1. 创建配置对象以指定启用AEM编辑所需的属性。

   ![创建配置对象](assets/external-spa-config-object.png)

   * `resourceType` 必须将AEM组件映射到AEM组件，并在编辑器中打开时启用编辑功能。

1. 使用包装函数 `withMappable`.

   ![与Mappable一起使用](assets/external-spa-withmappable.png)

   此包装函数将React组件映射到AEM `resourceType` 在配置中指定，并在AEM编辑器中打开时启用编辑功能。 对于独立组件，它还将获取特定节点的模型内容。

   >[!NOTE]
   >
   >在此示例中，组件有不同版本：AEM封装和解封装的React组件。 显式使用组件时，需要使用封装版本。 当组件是页面的一部分时，您可以继续使用默认组件，就像当前在SPA编辑器中一样。

1. 在组件中渲染内容。

   文本组件的JCR属性在AEM中如下所示。

   ![文本组件属性](assets/external-spa-text-properties.png)

   这些值将作为属性传递到新创建的 `AEMText` React组件和可用于渲染内容。

   ```javascript
   import React from 'react';
   import { withMappable } from '@adobe/aem-react-editable-components';
   
   export const TextEditConfig = {
       // Empty component placeholder label
       emptyLabel:'Text', 
       isEmpty:function(props) {
          return !props || !props.text || props.text.trim().length < 1;
       },
       // resourcetype of the AEM counterpart component
       resourceType:'wknd-spa-react/components/text'
   };
   
   const Text = ({ text }) => (<div>{text}</div>);
   
   export default Text;
   
   export const AEMText = withMappable(Text, TextEditConfig);
   ```

   这是组件在配置完成时的显示方式。AEM配置完成后。

   ```javascript
   const Text = ({ cqPath, richText, text }) => {
      const richTextContent = () => (
         <div className="aem_text" id={cqPath.substr(cqPath.lastIndexOf('/') + 1)} data-rte-editelement dangerouslySetInnerHTML={{__html: text}}/>
      );
      return richText ? richTextContent() : (<div className="aem_text">{text}</div>);
   };
   ```

   >[!NOTE]
   >
   >在此示例中，我们对渲染的组件进行了进一步自定义，以匹配现有的文本组件。 但是，这与在AEM中创作无关。

#### 将可创作组件添加到页面 {#add-authorable-component-to-page}

创建可创作的React组件后，我们可以在整个应用程序中使用这些组件。

让我们举一个示例页面，其中需要从WKND SPA项目添加文本。 在本例中，我们要显示文本“Hello World！” on `/content/wknd-spa-react/us/en/home.html`.

1. 确定要显示的节点的路径。

   * `pagePath`:在我们的示例中，包含节点的页面 `/content/wknd-spa-react/us/en/home`
   * `itemPath`:页面中节点的路径，在我们的示例中 `root/responsivegrid/text`
      * 这包括页面上包含项目的名称。

   ![节点的路径](assets/external-spa-path.png)

1. 在页面的所需位置添加组件。

   ![将组件添加到页面](assets/external-spa-add-component.png)

   的 `AEMText` 组件可添加到页面内的所需位置，该位置包含 `pagePath` 和 `itemPath` 值设置为属性。 `pagePath` 是强制属性。

#### 验证在AEM上编辑文本内容 {#verify-text-edit}

我们现在可以在运行的AEM实例上测试该组件。

1. 从 `aem-guides-wknd-spa` 目录来构建项目并将其部署到AEM。

```shell
mvn clean install -PautoInstallSinglePackage
```

1. 在您的AEM实例上，导航到 `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`.

![在AEM中编辑SPA](assets/external-spa-edit-aem.png)

的 `AEMText` 组件现在可在AEM上创作。

### AEM可创作页面 {#aem-authorable-pages}

1. 确定要添加以在SPA中进行创作的页面。 此示例使用 `/content/wknd-spa-react/us/en/home.html`.
1. 创建新文件(例如， `Page.js`)。 在此，我们可以重复使用 `@adobe/cq-react-editable-components`.
1. 在部分中重复步骤4 [AEM可创作叶组件。](#authorable-leaf-components) 使用包装函数 `withMappable` 在组件上。
1. 与以前一样，应用 `MapTo` 到页面中所有子组件的AEM资源类型。

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >在本例中，我们使用的是未封装的React文本组件，而不是封装的 `AEMText` 之前创建的。 这是因为当组件是页面/容器的一部分，而不是独立时，容器将负责递归映射组件并启用创作功能，并且每个子级不需要额外的包装器。

1. 要在SPA中添加可创作页面，请执行部分中的相同步骤 [将可创作组件添加到页面。](#add-authorable-component-to-page) 在这里，我们可以跳过 `itemPath` 属性。

#### 验证AEM上的页面内容 {#verify-page-content}

要验证是否可以编辑页面，请执行部分中的相同步骤 [验证在AEM上编辑文本内容。](#verify-text-edit)

![在AEM中编辑页面](assets/external-spa-edit-page.png)

现在，可以在具有布局容器和子文本组件的AEM上编辑页面。

### 虚拟叶组件 {#virtual-leaf-components}

在前面的示例中，我们使用现有的AEM内容将组件添加到SPA中。 但是，在某些情况下，尚未在AEM中创建内容，但需要由内容作者稍后添加。 为了适应此情况，前端开发人员可以在SPA内的适当位置添加组件。 这些组件在AEM的编辑器中打开时将显示占位符。 内容作者在这些占位符中添加内容后，将在JCR结构中创建节点，并保留内容。 创建的组件将允许与独立的叶组件具有相同的操作集。

在本例中，我们将重用 `AEMText` 组件。 我们希望在WKND主页上现有文本组件的下方添加新文本。 添加的组分与添加的常规叶组分相同。 但是， `itemPath` 可以更新到需要添加新组件的路径。

由于新组件需要添加到现有文本下方的 `root/responsivegrid/text`，则新路径为 `root/responsivegrid/{itemName}`.

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

的 `TestPage` 组件在添加虚拟组件后如下所示。

![测试虚拟组件](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>确保 `AEMText` 组件 `resourceType` 在配置中设置以启用此功能。

您现在可以按照部分中的步骤，将更改部署到AEM [验证在AEM上编辑文本内容。](#verify-text-edit) 将为当前不存在的显示占位符 `text_20` 节点。

![aem中的text_20节点](assets/external-spa-text20-aem.png)

内容作者更新此组件时，新 `text_20` 节点创建于 `root/responsivegrid/text_20` in `/content/wknd-spa-react/us/en/home`.

![text20节点](assets/external-spa-text20-node.png)

#### 要求和限制 {#limitations}

添加虚拟叶组件有许多要求，并且存在一些限制。

* 的 `pagePath` 属性是创建虚拟组件的必选项。
* 中路径处提供的页面节点 `pagePath` 必须存在于AEM项目中。
* 要创建的节点的名称必须在 `itemPath`.
* 组件可在任何级别创建。
   * 如果我们提供 `itemPath='text_20'` 在上一个示例中，新节点将直接在页面下创建，即 `/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* 通过提供时，指向创建新节点的节点的路径必须有效 `itemPath`.
   * 在本例中， `root/responsivegrid` 必须存在，以便新节点 `text_20` 可在此处创建。
* 仅支持创建叶组件。 未来版本将支持虚拟容器和页面。

### 虚拟容器 {#virtual-containers}

支持添加容器的功能，即使在AEM中尚未创建相应的容器也是如此。 该概念和方法类似于 [虚拟叶组件。](#virtual-leaf-components)

前端开发人员可以在SPA中的适当位置添加容器组件，这些组件在AEM的编辑器中打开时将显示占位符。 然后，作者可以将组件及其内容添加到容器，该容器将在JCR结构中创建所需的节点。

例如，如果容器在 `/root/responsivegrid` 并且开发人员想要添加新的子容器：

![容器位置](assets/container-location.png)

`newContainer` AEM中尚不存在。

在AEM中编辑包含此组件的页面时，将显示一个容器的空占位符，作者可以在其中添加内容。

![容器占位符](assets/container-placeholder.png)

![JCR中的容器位置](assets/container-jcr-structure.png)

作者向容器添加子组件后，将使用JCR结构中的相应名称创建新的容器节点。

![包含内容的容器](assets/container-with-content.png)

![JCR中包含内容的容器](assets/container-with-content-jcr.png)

现在可以根据作者的要求将更多组件和内容添加到容器中，并且这些更改将会保留。

#### 要求和限制 {#container-limitations}

添加虚拟容器有许多要求，并且存在一些限制。

* 用于确定可添加组件的策略将从父容器继承。
* 要创建的容器的直接父项必须已存在于AEM中。
   * 如果容器 `root/responsivegrid` AEM容器中已存在，则可以通过提供路径来创建新容器 `root/responsivegrid/newContainer`.
   * 但是 `root/responsivegrid/newContainer/secondNewContainer` 不可能。
* 一次只能虚拟创建一个新级别的组件。

## 其他自定义设置 {#additional-customizations}

如果您按照前面的示例进行操作，则现在可以在AEM中编辑外部SPA。 但是，您可以进一步自定义外部SPA的其他方面。

### 根节点ID {#root-node-id}

默认情况下，我们假定React应用程序呈现在 `div` 元素ID的 `spa-root`. 如果需要，可以自定义此设置。

例如，假设我们有一个SPA，其中应用程序呈现在 `div` 元素ID的 `root`. 这需要反映在三个文件中。

1. 在 `index.js` React应用程序(或 `ReactDOM.render()` 调用)

   ![index.js文件中的ReactDOM.render()](assets/external-spa-root-index.png)

1. 在 `index.html` React应用程序的

   ![应用程序的index.html](assets/external-spa-index.png)

1. 在AEM应用程序的页面组件正文中，通过以下两个步骤：

   1. 新建 `body.html` （对于页面组件）。

   ![创建新body.html文件](assets/external-spa-update-body.gif)

   1. 在新的 `body.html` 文件。

   ![将根元素添加到body.html](assets/external-spa-add-root.png)

### 使用路由编辑React SPA {#editing-react-spa-with-routing}

如果外部React SPA应用程序具有多个页面， [它可以使用路由确定要渲染的页面/组件。](spa-routing.md) 基本用例是将当前活动的URL与为路由提供的路径进行匹配。 要在此类启用路由的应用程序上启用编辑功能，需要转换要与之匹配的路径，以适应特定于AEM的信息。

在以下示例中，我们有一个简单的React应用程序，该应用程序包含两个页面。 要呈现的页面取决于提供给路由器的路径与活动URL的匹配。 例如，如果我们在 `mydomain.com/test`, `TestPage` 将呈现。

![外部SPA中的路由](assets/external-spa-routing.png)

要在AEM中为此示例SPA启用编辑功能，需要执行以下步骤。

1. 确定将作为AEM根的级别。

   * 对于我们的样本，我们考虑 `wknd-spa-react/us/en` 作为SPA的根。 这意味着该路径之前的所有内容都仅AEM页面/内容。

1. 在所需级别创建新页面。

   * 在本例中，要编辑的页面是 `mydomain.com/test`. `test` 位于应用程序的根路径中。 在AEM中创建页面时，也需要保留该设置。 因此，我们可以在上一步中定义的根级别创建新页面。
   * 创建的新页面必须与要编辑的页面同名。 在本例中，例如 `mydomain.com/test`，则创建的新页面必须 `/path/to/aem/root/test`.

1. 在SPA路由中添加帮助程序。

   * 新创建的页面尚未在AEM中呈现预期内容。 这是因为路由器希望路径为 `/test` 而AEM活动路径为 `/wknd-spa-react/us/en/test`. 为了适应URL中特定于AEM的部分，我们需要在SPA端添加一些帮助程序。

   ![路由辅助程序](assets/external-spa-router-helper.png)

   * 的 `toAEMPath` 提供的助手 `@adobe/cq-spa-page-model-manager` 可用于此。 当应用程序在AEM实例上打开时，它会转换为用于路由的路径，以包含AEM特定部分。 它接受三个参数：
      * 路由所需的路径
      * 编辑SPA的AEM实例的源URL
      * AEM上的项目根目录，在第一步中确定
   * 这些值可设置为环境变量，以便获得更大的灵活性。



1. 在AEM中验证是否编辑页面。

   * 将项目部署到AEM并导航到新创建的 `test` 页面。 现在会呈现页面内容，并且AEM组件可编辑。

## 其他资源 {#additional-resources}

以下参考材料可能有助于在SPA的上下文中了解AEM。

* [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* [WKND SPA项目](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html)
* [AEM中的SPA使用React快速入门](spa-getting-started-react.md)
* [SPA参考资料（API参考）](spa-reference-materials.md)
* [SPA Blueprint和PageModelManager](spa-blueprint.md#pagemodelmanager)
* [SPA模型路由](spa-routing.md)
* [SPA和服务器端渲染](spa-ssr.md)
