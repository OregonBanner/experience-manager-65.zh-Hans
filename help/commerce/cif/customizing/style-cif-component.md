---
title: 样式AEM CIF核心组件
description: 了解如何设置AEM CIF核心组件的样式。 本教程介绍如何使用客户端库或客户端库来部署和管理Adobe Experience Manager(AEM)商务实施的CSS和Javascript。 本教程还将介绍如何将ui.frontend模块和Webpack项目集成到端到端构建过程中。
sub-product: 商务
topics: Development
version: cloud-service
doc-type: tutorial
feature: 商务集成框架
kt: 3456
thumbnail: 3456-style-cif.jpg
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '2566'
ht-degree: 2%

---

# 样式AEM CIF核心组件{#style-aem-cif-core-components}

[CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia)是使用[CIF核心组件](https://github.com/adobe/aem-core-cif-components)的参考代码库。 在本教程中，您将检查Venia参考项目，并了解AEM CIF核心组件使用的CSS和JavaScript的组织方式。 您还将使用CSS创建新样式以更新&#x200B;**Product Teaser**&#x200B;组件的默认样式。

>[!TIP]
>
> 启动您自己的商务实施时，请使用[AEM项目原型](https://github.com/adobe/aem-project-archetype)。

## 您将要构建的内容

在本教程中，将为类似于卡的Product Teaser组件实施新样式。 本教程中的课程可以应用到其他CIF核心组件。

![将构建的内容](../assets/style-cif-component/what-you-will-build.png)

## 前提条件 {#prerequisites}

需要本地开发环境才能完成本教程。 这包括已配置并连接到AEM实例的Magento实例。 查看[使用AEM](../develop.md)设置本地开发的要求和步骤。

## 克隆Venia项目{#clone-venia-project}

我们将克隆[Venia Project](https://github.com/adobe/aem-cif-guides-venia)，然后覆盖默认样式。

>[!NOTE]
>
> **请随时使用现有项目** (基于包含CIF的AEM项目原型)并跳过此部分。

1. 运行以下git命令以克隆项目：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 构建项目并将其部署到AEM的本地实例：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 添加必要的OSGi配置，以将您的AEM实例连接到Magento实例，或将配置添加到新创建的项目。

1. 此时，您应该拥有连接到Magento实例的店面的工作版本。 导航到`US` > `Home`页面：[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

   您应会看到，当前的店面使用的是Venia主题。 展开店面的主菜单时，您应会看到各种类别，表示连接Magento正在工作。

   ![使用Venia主题配置的店面](../assets/style-cif-component/venia-store-configured.png)

## 客户端库和ui.frontend模块{#introduction-to-client-libraries}

负责呈现店面主题/样式的CSS和JavaScript在AEM中由[客户端库](/help/sites-developing/clientlibs.md)或clientlibs来管理。 客户端库提供了一种机制，用于在项目代码中组织CSS和Javascript，然后将其交付到页面。

可通过添加和覆盖由这些客户端库管理的CSS，将特定于品牌的样式应用于AEM CIF核心组件。 了解客户端库的结构以及如何在页面上包含至关重要。

[ui.frontend](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/uifrontend.html)是一个专用的[Webpack](https://webpack.js.org/)项目，用于管理项目的所有前端资产。 这允许前端开发人员使用任意数量的语言和技术，如[TypeScript](https://www.typescriptlang.org/)、[Sass](https://sass-lang.com/)等。

`ui.frontend`模块也是Maven模块，通过使用[aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator)的NPM模块与较大的项目集成。 在生成过程中， `aem-clientlib-generator`会将编译的CSS和JavaScript文件复制到`ui.apps`模块的客户端库中。

![ui.frontend到ui.apps架构](../assets/style-cif-component/ui-frontend-architecture.png)

*在Maven内部版本中，编译的CSS `ui.frontend` 和Javascript将作 `ui.apps` 为客户端库从模块复制到模块中*

## 更新Teaser样式{#ui-frontend-module}

接下来，对Teaser样式进行细微更改，以了解`ui.frontend`模块和客户端库的工作方式。 使用[您选择的IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide)导入Venia项目。 使用的屏幕截图来自[Visual Studio代码IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)。

1. 导航并展开&#x200B;**ui.frontend**&#x200B;模块，然后展开文件夹层次结构以：`ui.frontend/src/main/styles/commerce`:

   ![ui.frontend商务文件夹](../assets/style-cif-component/ui-frontend-commerce-folder.png)

   请注意，文件夹下有多个Sass(`.scss`)文件。 这些是每个商务组件的特定于商务的样式。

1. 打开文件`_productteaser.scss`。

1. 更新`.item__image`规则并修改边框规则：

   ```scss
   .item__image {
       border: #ea00ff 8px solid; /* <-- modify this rule */
       display: block;
       grid-area: main;
       height: auto;
       opacity: 1;
       transition-duration: 512ms;
       transition-property: opacity, visibility;
       transition-timing-function: ease-out;
       visibility: visible;
       width: 100%;
   }
   ```

   上述规则应在产品Teaser组件中添加一个非常粗体的粉红色边框。

1. 打开新的终端窗口并导航到`ui.frontend`文件夹：

   ```shell
   $ cd <project-location>/aem-cif-guides-venia/ui.frontend
   ```

1. 运行以下Maven命令：

   ```shell
   $ mvn clean install
   ...
   [INFO] ------------------------------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ------------------------------------------------------------------------
   [INFO] Total time:  29.497 s
   [INFO] Finished at: 2020-08-25T14:30:44-07:00
   [INFO] ------------------------------------------------------------------------
   ```

   Inspect终端输出。 您将看到Maven命令执行了多个NPM脚本，包括`npm run build`。 `npm run build`命令在`package.json`文件中定义，具有编译Webpack项目并触发客户端库生成的效果。

1. Inspect文件`ui.frontend/dist/clientlib-site/site.css`:

   ![编译的网站CSS](../assets/style-cif-component/comiled-site-css.png)

   该文件是项目中所有Sass文件的编译和缩小版本。

   >[!NOTE]
   >
   > 此类文件会从源代码管理中忽略，因为它们应在生成期间生成。

1. Inspect文件`ui.frontend/clientlib.config.js`。

   ```js
   /* clientlib.config.js*/
   ...
   // Config for `aem-clientlib-generator`
   module.exports = {
       context: BUILD_DIR,
       clientLibRoot: CLIENTLIB_DIR,
       libs: [
           {
               ...libsBaseConfig,
               name: 'clientlib-site',
               categories: ['venia.site'],
               dependencies: ['venia.dependencies', 'aem-core-cif-react-components'],
               assets: {
   ...
   ```

   这是[aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator)的配置文件，它确定编译的CSS和JavaScript将转换到AEM客户端库的位置和方式。

1. 在`ui.apps`模块中，检查文件：`ui.apps/src/main/content/jcr_root/apps/venia/clientlibs/clientlib-site/css/site.css`:

   ![ui.apps中编译的站点CSS](../assets/style-cif-component/comiled-css-ui-apps.png)

   这会将`site.css`文件复制到`ui.apps`项目中。 它现在是名为`clientlib-site`且类别为`venia.site`的客户端库的一部分。 文件成为`ui.apps`模块的一部分后，即可将其部署到AEM。

   >[!NOTE]
   >
   > 此类文件也会从源代码管理中忽略，因为它们应该在生成期间生成。

1. 接下来，检查由项目生成的其他客户端库：

   ![其他客户端库](../assets/style-cif-component/other-clientlibs.png)

   这些客户端库不由`ui.frontend`模块管理。 相反，这些客户端库包含由Adobe提供的CSS和JavaScript依赖项。 这些客户端库的定义位于每个文件夹下的`.content.xml`文件中。

   **clientlib-base**  — 这是一个空的客户端库，它只嵌入AEM核心组件中的必 [要依赖项](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。类别为`venia.base`。

   **clientlib-cif**  — 这也是一个空的客户端库，只需嵌入AEM CIF核心组件中 [的必需依赖项即可](https://github.com/adobe/aem-core-cif-components)。类别为`venia.cif`。

   **clientlib-grid**  — 这包括启用AEM响应式网格功能所需的CSS。使用AEM网格可在AEM编辑器中启用[布局模式](/help/sites-authoring/responsive-layout.md)，并使内容作者能够重新调整组件的大小。 类别为`venia.grid`，并嵌入在`venia.base`库中。

1. Inspect `customheaderlibs.html`和`customfooterlibs.html`下`ui.apps/src/main/content/jcr_root/apps/venia/components/page`的文件：

   ![自定义页眉和页脚脚本](../assets/style-cif-component/custom-header-footer-script.png)

   这些脚本包括作为所有页面一部分的&#x200B;**venia.base**&#x200B;和&#x200B;**venia.cif**&#x200B;库。

   >[!NOTE]
   >
   > 只有基础库会作为页面脚本的一部分进行“硬编码”。 `venia.site` 不包含在这些文件中，而是作为页面模板的一部分包含在内，以便获得更大的灵活性。以后会检查。

1. 从终端，构建整个项目并将其部署到AEM的本地实例：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

## 创作产品Teaser {#author-product-teaser}

现在，代码更新已部署，请使用AEM创作工具将产品Teaser组件的新实例添加到站点的主页。 这将允许我们查看更新的样式。

1. 打开新的浏览器选项卡，然后导航到网站的&#x200B;**主页**:[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

1. 在&#x200B;**编辑**&#x200B;模式下展开资产查找器（侧边栏）。 将资产筛选器切换到&#x200B;**Products**。

   ![展开资产查找器并按产品进行筛选](../assets/style-cif-component/drag-drop-product-page.png)

1. 将新产品拖放到主布局容器的主页上：

   ![带粉色边框的产品Teaser](../assets/style-cif-component/pink-border-product-teaser.png)

   您应会看到Product Teaser现在有一个基于之前创建的CSS规则更改的亮粉色边框。

## 验证页面{#verify-client-libraries}上的客户端库

接下来，验证是否在页面上包含客户端库。

1. 导航到网站的&#x200B;**主页**:[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

1. 选择&#x200B;**页面信息**&#x200B;菜单，然后单击&#x200B;**查看已发布的项目**:

   ![查看已发布的项目](../assets/style-cif-component/view-as-published.png)

   这将打开页面，且未加载任何AEM作者javascript，就像它显示在已发布的网站上一样。 请注意，URL中附加了查询参数`?wcmmode=disabled`。 在开发CSS和Javascript时，最好使用此参数来简化页面，而无需AEM作者提供任何内容。

1. 查看页面源，您应该能够识别其中包含的多个客户端库：

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-site.min.css" type="text/css">
   </head>
   ...
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/core/wcm/components/commons/site/clientlibs/container.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-base.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/common.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-cif.min.js"></script>
   </body>
   </html>
   ```

   客户端库在交付到页面时以`/etc.clientlibs`为前缀，并通过[proxy](/help/sites-developing/clientlibs.md)提供，以避免公开`/apps`或`/libs`中任何敏感内容。

   请注意`venia/clientlibs/clientlib-site.min.css`和`venia/clientlibs/clientlib-site.min.js`。 这些是从`ui.frontend`模块派生的编译的CSS和Javascript文件。

## 包含页面模板的客户端库{#client-library-inclusion-pagetemplates}

有关如何包含客户端库的选项有多种。 接下来，通过[页面模板](/help/sites-developing/templates.md)检查生成的项目如何包含`clientlib-site`库。

1. 在AEM编辑器中，导航到网站的&#x200B;**主页**:[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

1. 选择&#x200B;**页面信息**&#x200B;菜单，然后单击&#x200B;**编辑模板**:

   ![编辑模板](../assets/style-cif-component/edit-template.png)

   这将打开&#x200B;**登陆页面**&#x200B;模板，该模板是&#x200B;**Home**&#x200B;页面所基于的。

   >[!NOTE]
   >
   > 要从“AEM开始”屏幕中查看所有可用的模板，请导航到&#x200B;**工具** > **常规** > **模板**。

1. 在左上角，选择&#x200B;**页面信息**&#x200B;图标，然后单击&#x200B;**页面策略**。

   ![页面策略菜单项](../assets/style-cif-component/page-policy-menu.png)

1. 这将打开登陆页面模板的页面策略：

   ![页面策略 — 登陆页面](../assets/style-cif-component/page-policy-properties.png)

   在右侧，您可以看到将包含在使用此模板的所有页面上的客户端库&#x200B;**类别**&#x200B;的列表。

   * `venia.dependencies`  — 提供任何依赖的供 `venia.site` 应商库。
   * `venia.site`  — 这是模块生 `clientlib-site` 成的 `ui.frontend` 类别。

   请注意，其他模板使用相同的策略：**内容页面**、**登陆页面**，等等。 通过重新使用相同的策略，我们可以确保所有页面上都包含相同的客户端库。

   使用模板和页面策略管理客户端库的包含的好处是您可以根据模板更改策略。 例如，您可能在同一AEM实例中管理了两个不同的品牌。 每个品牌将有其自己的唯一样式或&#x200B;*theme*，但基本库和代码将相同。 另一个示例是，如果您有一个更大的客户端库，而您只希望在某些页面上显示该库，则可以仅为该模板制定唯一的页面策略。

## 本地Webpack开发{#local-webpack-development}

在上一个练习中，对`ui.frontend`模块中的Sass文件进行了更新，然后执行Maven内部版本后，更改将部署到AEM。 接下来，我们将研究如何利用Webpack-dev-server来快速开发前端样式。

Webpack-dev-server代理AEM本地实例中的图像和某些CSS/JavaScript，但允许开发人员在`ui.frontend`模块中修改样式和JavaScript。

1. 在浏览器中，导航到&#x200B;**Home**&#x200B;页面和&#x200B;**查看已发布的**:[http://localhost:4502/content/venia/us/en.html?wcmmode=disabled](http://localhost:4502/content/venia/us/en.html?wcmmode=disabled)。

1. 查看页面的源，以及&#x200B;**copy**&#x200B;页面的原始HTML。

1. 返回到在`ui.frontend`模块下选择的IDE，打开文件：`ui.frontend/src/main/static/index.html`

   ![静态HTML文件](../assets/style-cif-component/static-index-html.png)

1. 覆盖在上一步中复制的HTML的`index.html`和&#x200B;**粘贴**&#x200B;内容。

1. 找到`clientlib-site.min.css`、`clientlib-site.min.js`和&#x200B;**remove**&#x200B;的包含项。

   ```html
   <head>
       <!-- remove this link -->
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       ...
   </head>
   <body>
       ...
        <!-- remove this link -->
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
   </body>
   ```

   由于它们表示由`ui.frontend`模块生成的CSS和JavaScript的编译版本，因此它们会被删除。 保留其他客户端库，因为它们将从运行的AEM实例中代理。

1. 打开新的终端窗口，然后导航到`ui.frontend`文件夹。 运行命令`npm start`:

   ```shell
   $ cd ui.frontend
   $ npm start
   ```

   这将在[http://localhost:8080/](http://localhost:8080/)上启动Webpack-dev-server

   >[!CAUTION]
   >
   > 如果出现与Sass相关的错误，请停止服务器并运行命令`npm rebuild node-sass`并重复上述步骤。 如果您的`npm`和`node`版本不同，则可能会发生这种情况，这些版本随后会在项目`aem-cif-guides-venia/pom.xml`中指定。

1. 在与已登录的AEM实例具有相同浏览器的新选项卡中，导航到[http://localhost:8080/](http://localhost:8080/)。 您应该通过webpack-dev-server看到Venia主页：

   ![端口80上的Webpack开发服务器](../assets/style-cif-component/webpack-dev-server-port80.png)

   保持Webpack-dev-server运行。 它将用于下一个练习。

## 为Product Teaser {#update-css-product-teaser}实施卡样式

接下来，修改`ui.frontend`模块中的Sass文件，以实现Product Teaser的类卡样式。 webpack-dev-server将用于快速查看更改。

返回到IDE和生成的项目。

1. 在&#x200B;**ui.frontend**&#x200B;模块中，重新打开位于`ui.frontend/src/main/styles/commerce/_productteaser.scss`的文件`_productteaser.scss`。

1. 对Product Teaser边框进行以下更改：

   ```diff
       .item__image {
   -       border: #ea00ff 8px solid;
   +       border-bottom: 1px solid #c0c0c0;
           display: block;
           grid-area: main;
           height: auto;
           opacity: 1;
           transition-duration: 512ms;
           transition-property: opacity, visibility;
           transition-timing-function: ease-out;
           visibility: visible;
           width: 100%;
       }
   ```

   保存更改，Webpack-dev-server应自动刷新新样式。

1. 向Product Teaser添加投影并包含圆角。

   ```scss
    .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

1. 更新产品名称以显示在Teaser底部，并修改文本颜色。

   ```css
   .item__name {
       color: #000;
       display: block;
       float: left;
       font-size: 22px;
       font-weight: 900;
       line-height: 1em;
       padding: 0.75em;
       text-transform: uppercase;
       width: 75%;
   }
   ```

1. 更新产品价格以同时显示在Teaser底部并修改文本颜色。

   ```css
   .price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   
       ...
   ```

1. 更新底部的媒体查询，以在小于&#x200B;**992px**&#x200B;的屏幕中堆叠名称和价格。

   ```css
   @media (max-width: 992px) {
       .productteaser .item__name {
           font-size: 18px;
           width: 100%;
       }
       .productteaser .item__price {
           font-size: 14px;
           width: 100%;
       }
   }
   ```

   现在，您应会看到Webpack-dev-server中反映的卡片样式：

   ![Webpack开发服务器Teaser更改](../assets/style-cif-component/webpack-dev-server-teaser-changes.png)

   但是，这些更改尚未部署到AEM。 您可以在此处下载[解决方案文件](../assets/style-cif-component/_productteaser.scss)。

1. 使用您的Maven技能，从命令行终端部署对AEM的更新：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

   >[!NOTE]
   >还有其他的[IDE设置和工具](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment)，它们可以将项目文件直接同步到本地AEM实例，而无需执行完整的Maven生成。

## 查看更新的Product Teaser {#view-updated-product-teaser}

将项目的代码部署到AEM后，我们现在应该能够看到对Product Teaser的更改。

1. 返回浏览器并重新刷新主页：[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。 您应会看到已应用更新的产品Teaser样式。

   ![更新了产品Teaser样式](../assets/style-cif-component/product-teaser-new-style.png)

1. 通过添加其他产品Teaser来体验。 使用布局模式可更改组件的宽度和偏移，以便在一行中显示多个Teaser。

   ![多个产品Teaser](../assets/style-cif-component/multiple-teasers-final.png)

## 疑难解答 {#troubleshooting}

您可以在[CRXDE-Lite](http://localhost:4502/crx/de/index.jsp)中验证已部署更新的CSS文件：[http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css](http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css)

部署新的CSS和/或JavaScript文件时，还务必确保浏览器不提供过时文件。 您可以通过清除浏览器缓存或启动新的浏览器会话来消除这种情况。

AEM还尝试缓存客户端库以提高性能。 有时，在代码部署后，会提供旧版文件。 您可以使用[重建客户端库工具](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html)手动使AEM客户端库缓存失效。 *如果您怀疑AEM已缓存了旧版本的客户端库，则使用无效缓存是首选方法。重建库效率低下且耗时。*

## 恭喜 {#congratulations}

您刚刚设置了第一个AEM CIF核心组件的样式，并且使用了Web包开发服务器！

## 附加练习{#bonus-challenge}

使用[AEM Style system](/help/sites-authoring/style-system.md)创建可由内容作者打开/关闭的两个样式。 [使用样式系统进](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) 行开发，包括有关如何实现此目的的详细步骤和信息。

![奖金挑战 — 风格系统](../assets/style-cif-component/bonus-challenge.png)

## 其他资源 {#additional-resources}

* [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
* [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)
* [设置本地AEM开发环境](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)
* [客户端库](/help/sites-developing/clientlibs.md)
* [开始使用AEM Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
* [用风格体系发展](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
