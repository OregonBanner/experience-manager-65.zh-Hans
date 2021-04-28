---
title: 样式AEM CIF核心组件
description: 了解如何设计AEM CIF核心组件的样式。 本教程介绍如何使用客户端库或客户端库部署和管理Adobe Experience Manager(AEM)商务实施的CSS和Javascript。 本教程还将介绍如何将ui.frontend模块和Webpack项目集成到端到端构建流程中。
sub-product: 商务
topics: Development
version: cloud-service
doc-type: tutorial
feature: Commerce Integration Framework
kt: 3456
thumbnail: 3456-style-cif.jpg
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '2566'
ht-degree: 2%

---

# 样式AEM CIF核心组件{#style-aem-cif-core-components}

[CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia)是使用[CIF核心组件](https://github.com/adobe/aem-core-cif-components)的参考代码库。 在本教程中，您将检查Venia参考项目并了解AEM CIF核心组件使用的CSS和JavaScript的组织方式。 您还将使用CSS创建新样式以更新&#x200B;**产品Teaser**&#x200B;组件的默认样式。

>[!TIP]
>
> 启动您自己的商务实施时，请使用[AEM Project原型](https://github.com/adobe/aem-project-archetype)。

## 您将构建的

在本教程中，将为类似于卡的产品Teaser组件实施新样式。 本教程中吸取的经验教训可应用于其他CIF核心组件。

![您将构建的](../assets/style-cif-component/what-you-will-build.png)

## 前提条件 {#prerequisites}

完成本教程需要一个本地开发环境。 这包括已配置并连接到Magento实例的AEM运行实例。 查看使用AEM](../develop.md)设置本地开发的要求和步骤。[

## 克隆Venia项目{#clone-venia-project}

我们将克隆[Venia Project](https://github.com/adobe/aem-cif-guides-venia)，然后覆盖默认样式。

>[!NOTE]
>
> **您可以随意使用现有项目** (基于包含CIF的AEM项目原型)并跳过此部分。

1. 运行以下git命令以克隆项目：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 构建项目并将其部署到AEM的本地实例：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 添加必要的OSGi配置以将您的AEM实例连接到Magento实例，或将配置添加到新创建的项目。

1. 此时，您应该拥有连接到Magento实例的店面的工作版本。 导航到`US` > `Home`页，网址为：[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

   您应该看到店面当前使用Venia主题。 展开店面的主菜单时，您应会看到各种类别，表示连接Magento正在工作。

   ![配置了Venia主题的店面](../assets/style-cif-component/venia-store-configured.png)

## 客户端库和ui.frontend模块{#introduction-to-client-libraries}

负责呈现店面主题/样式的CSS和JavaScript在AEM中由[客户端库](/help/sites-developing/clientlibs.md)或clientlibs管理。 客户端库提供一种机制，用于在项目代码中组织CSS和Javascript，然后交付到页面上。

可以通过添加和覆盖由这些客户端库管理的CSS，将品牌特定样式应用于AEM CIF核心组件。 了解客户端库的结构和页面包含方式至关重要。

[ui.frontend](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/uifrontend.html)是专用的[webpack](https://webpack.js.org/)项目，用于管理项目的所有前端资源。 这允许前端开发人员使用任何语言和技术，如[TypeScript](https://www.typescriptlang.org/)、[Sass](https://sass-lang.com/)等。

`ui.frontend`模块也是Maven模块，通过使用[aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator)的NPM模块与较大项目集成。 在生成过程中，`aem-clientlib-generator`将编译的CSS和JavaScript文件复制到`ui.apps`模块中的客户端库中。

![ui.frontend to ui.apps architecture](../assets/style-cif-component/ui-frontend-architecture.png)

*在Maven构建期间，编译的CSS `ui.frontend` 和Javascript将 `ui.apps` 作为客户端库从模块复制到模块中*

## 更新Teaser样式{#ui-frontend-module}

接下来，对Teaser样式进行一小段更改，以查看`ui.frontend`模块和客户端库的工作方式。 使用您选择的[IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide)导入Venia项目。 使用的截屏来自[ Visual Studio代码IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)。

1. 导航并展开&#x200B;**ui.frontend**&#x200B;模块，然后展开文件夹层次结构以：`ui.frontend/src/main/styles/commerce`:

   ![ui.frontend商务文件夹](../assets/style-cif-component/ui-frontend-commerce-folder.png)

   请注意，文件夹下有多个Sass(`.scss`)文件。 这些是每个商务组件的商务特定样式。

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

   上述规则应在“产品Teaser组件”中添加非常粗体的粉红色边框。

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

   Inspect终端输出。 您将看到Maven命令执行了包括`npm run build`在内的几个NPM脚本。 `npm run build`命令在`package.json`文件中定义，具有编译webpack项目和触发客户端库生成的效果。

1. Inspect文件`ui.frontend/dist/clientlib-site/site.css`:

   ![已编译站点CSS](../assets/style-cif-component/comiled-site-css.png)

   该文件是项目中所有Sass文件的编译和缩小版本。

   >[!NOTE]
   >
   > 此类文件会从源代码管理中忽略，因为它们应在生成时生成。

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

   这是[aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator)的配置文件，它确定编译的CSS和JavaScript将转换为AEM客户端库的位置和方式。

1. 在`ui.apps`模块中，检查文件：`ui.apps/src/main/content/jcr_root/apps/venia/clientlibs/clientlib-site/css/site.css`:

   ![在ui.apps中编译的站点CSS](../assets/style-cif-component/comiled-css-ui-apps.png)

   这会将`site.css`文件复制到`ui.apps`项目中。 它现在是名为`clientlib-site`的客户端库的一部分，其类别为`venia.site`。 文件是`ui.apps`模块的一部分后，即可将其部署到AEM。

   >[!NOTE]
   >
   > 此类文件也会从源代码管理中忽略，因为它们应在生成时生成。

1. 接下来检查由项目生成的其他客户端库：

   ![其他客户端库](../assets/style-cif-component/other-clientlibs.png)

   这些客户端库不由`ui.frontend`模块管理。 而是这些客户端库包含由Adobe提供的CSS和JavaScript依赖项。 这些客户端库的定义位于每个文件夹下的`.content.xml`文件中。

   **clientlib-base**  — 这是一个空客户端库，它只嵌入AEM核心组件中必 [需的依赖项](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。类别为`venia.base`。

   **clientlib-cif**  — 这也是一个空客户端库，它只嵌入AEM CIF核心组件中 [的必要依赖项](https://github.com/adobe/aem-core-cif-components)。类别为`venia.cif`。

   **clientlib-grid**  — 这包括启用AEM响应式网格功能所需的CSS。使用AEM网格可启用AEM编辑器中的[布局模式](/help/sites-authoring/responsive-layout.md)，使内容作者能够重新调整组件大小。 该类别为`venia.grid`并嵌入到`venia.base`库中。

1. Inspect `ui.apps/src/main/content/jcr_root/apps/venia/components/page`下方的文件`customheaderlibs.html`和`customfooterlibs.html`:

   ![自定义页眉和页脚脚本](../assets/style-cif-component/custom-header-footer-script.png)

   这些脚本包括作为所有页面一部分的&#x200B;**venia.base**&#x200B;和&#x200B;**venia.cif**&#x200B;库。

   >[!NOTE]
   >
   > 只有基库作为页面脚本的一部分被“硬编码”。 `venia.site` 不包含在这些文件中，而是作为页面模板的一部分提供，以获得更大的灵活性。稍后会检查。

1. 从终端，构建整个项目并将其部署到AEM的本地实例：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

## 创作产品Teaser {#author-product-teaser}

现在已部署代码更新，请使用AEM创作工具将产品Teaser组件的新实例添加到站点主页。 这将允许我们视图更新的样式。

1. 打开新的浏览器选项卡，并导航到站点的&#x200B;**主页**:[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

1. 在&#x200B;**编辑**&#x200B;模式下展开资产查找器（侧边栏）。 将“资产”过滤器切换到&#x200B;**Products**。

   ![展开资产查找器并按产品进行筛选](../assets/style-cif-component/drag-drop-product-page.png)

1. 将新产品拖放到主布局容器的主页上：

   ![带粉红色边框的产品Teaser](../assets/style-cif-component/pink-border-product-teaser.png)

   您应当看到产品Teaser现在有一个基于之前创建的CSS规则更改的亮粉色边框。

## 验证页面{#verify-client-libraries}上的客户端库

接下来验证是否在页面中包含客户端库。

1. 导航到站点的&#x200B;**主页**:[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

1. 选择&#x200B;**页面信息**&#x200B;菜单，然后单击&#x200B;**视图作为已发布**:

   ![查看已发布的项目](../assets/style-cif-component/view-as-published.png)

   此操作将在未加载任何AEM作者javascript的情况下打开页面，就像在发布的站点上一样。 请注意，url中附加了查询参数`?wcmmode=disabled`。 在开发CSS和Javascript时，最好使用此参数来简化页面，而无需AEM作者提供任何内容。

1. 视图页面源，您应该能够识别包含的多个客户端库：

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

   将客户端库发送到页面时，以`/etc.clientlibs`为前缀，并通过[proxy](/help/sites-developing/clientlibs.md)提供客户端库，以避免暴露`/apps`或`/libs`中任何敏感内容。

   注意`venia/clientlibs/clientlib-site.min.css`和`venia/clientlibs/clientlib-site.min.js`。 这些是从`ui.frontend`模块派生的已编译CSS和Javascript文件。

## 包含页面模板的客户端库{#client-library-inclusion-pagetemplates}

有关如何包含客户端库的方法有多种选项。 接下来，通过[页面模板](/help/sites-developing/templates.md)检查生成的项目如何包含`clientlib-site`库。

1. 在AEM编辑器中，导航到站点的&#x200B;**主页**:[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

1. 选择&#x200B;**页面信息**&#x200B;菜单，然后单击&#x200B;**编辑模板**:

   ![编辑模板](../assets/style-cif-component/edit-template.png)

   这将打开&#x200B;**主页**&#x200B;页面所基于的&#x200B;**登陆页**&#x200B;模板。

   >[!NOTE]
   >
   > 要视图AEM 开始屏幕中的所有可用模板，请导航到&#x200B;**工具** > **常规** > **模板**。

1. 在左上角，选择&#x200B;**页面信息**&#x200B;图标，然后单击&#x200B;**页面策略**。

   ![页面策略菜单项](../assets/style-cif-component/page-policy-menu.png)

1. 这将打开登陆页模板的页面策略：

   ![页面策略 — 登陆页](../assets/style-cif-component/page-policy-properties.png)

   在右侧，您可以看到一个客户端库列表&#x200B;**类别**，这些客户端库将包含在使用此模板的所有页面上。

   * `venia.dependencies`  — 提供任何依赖的 `venia.site` 供应商库。
   * `venia.site`  — 这是模块生 `clientlib-site` 成的 `ui.frontend` 类别。

   请注意，其他模板使用相同的策略，**内容页**、**登陆页**&#x200B;等。 通过重新使用相同的策略，我们可以确保所有页面都包含相同的客户端库。

   使用“模板”和“页面策略”管理包含客户端库的好处在于，您可以根据模板更改策略。 例如，您可能在同一AEM实例中管理两个不同的品牌。 每个品牌将有其自己的独特样式或&#x200B;*theme*，但基库和代码将相同。 另一个示例是，如果您有一个较大的客户端库，而您只想在某些页面上显示它，则可以为该模板制定唯一的页面策略。

## 本地Webpack开发{#local-webpack-development}

在上一个练习中，对`ui.frontend`模块中的Sass文件进行了更新，然后在执行Maven构建后，更改将部署到AEM。 接下来，我们将研究如何利用webpack-dev-server快速开发前端样式。

webpack-dev-server代理来自AEM本地实例的图像和某些CSS/JavaScript，但允许开发人员修改`ui.frontend`模块中的样式和JavaScript。

1. 在浏览器中，导航到&#x200B;**主页**&#x200B;页面和&#x200B;**视图作为已发布**:[http://localhost:4502/content/venia/us/en.html?wcmmode=disabled](http://localhost:4502/content/venia/us/en.html?wcmmode=disabled)。

1. 视图页面的源和页面的&#x200B;**copy**&#x200B;原始HTML。

1. 返回至`ui.frontend`模块下您选择的IDE，打开文件：`ui.frontend/src/main/static/index.html`

   ![静态HTML文件](../assets/style-cif-component/static-index-html.png)

1. 覆盖在上一步中复制的`index.html`和&#x200B;**paste**&#x200B;的内容。

1. 查找`clientlib-site.min.css`、`clientlib-site.min.js`和&#x200B;**remove**&#x200B;的包含。

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

   删除这些组件是因为它们代表由`ui.frontend`模块生成的CSS和JavaScript的编译版本。 保留其他客户端库，它们将从正在运行的AEM实例中代理。

1. 打开新的终端窗口，并导航到`ui.frontend`文件夹。 运行命令`npm start`:

   ```shell
   $ cd ui.frontend
   $ npm start
   ```

   这将开始[http://localhost:8080/](http://localhost:8080/)上的webpack-dev-server

   >[!CAUTION]
   >
   > 如果出现与Sass相关的错误，请停止服务器并运行命令`npm rebuild node-sass`，然后重复上述步骤。 如果您在项目`aem-cif-guides-venia/pom.xml`中指定了不同版本的`npm`和`node`，则可能会发生这种情况。

1. 在与AEM登录实例浏览器相同的新选项卡中导航到[http://localhost:8080/](http://localhost:8080/)。 您应通过webpack-dev-server看到Venia主页:

   ![端口80上的Webpack开发服务器](../assets/style-cif-component/webpack-dev-server-port80.png)

   使webpack-dev-server保持运行。 它将用于下一个练习。

## 为产品Teaser {#update-css-product-teaser}实现卡样式

接下来，修改`ui.frontend`模块中的Sass文件，为Product Teaser实现类似卡的样式。 webpack-dev-server将用于快速查看更改。

返回IDE和生成的项目。

1. 在&#x200B;**ui.frontend**&#x200B;模块中，重新打开位于`ui.frontend/src/main/styles/commerce/_productteaser.scss`的文件`_productteaser.scss`。

1. 对产品Teaser边框进行以下更改：

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

   保存更改，webpack-dev-server应使用新样式自动刷新。

1. 添加投影并将圆角包含到产品预告中。

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

1. 更新产品名称以显示在Teaser底部并修改文本颜色。

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

1. 更新产品的价格，使其也显示在Teaser的底部并修改文本颜色。

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

   现在，您应该会看到webpack-dev-server中反映的卡样式：

   ![Webpack开发服务器Teaser更改](../assets/style-cif-component/webpack-dev-server-teaser-changes.png)

   但是，尚未将更改部署到AEM。 您可以在此处下载[解决方案文件](../assets/style-cif-component/_productteaser.scss)。

1. 使用Maven技能从命令行终端部署更新至AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

   >[!NOTE]
   >还有其他[IDE设置和工具](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment)，它们可以将项目文件直接同步到本地AEM实例，而无需执行完全的Maven生成。

## 视图已更新产品Teaser {#view-updated-product-teaser}

将项目的代码部署到AEM后，我们现在应能看到对产品Teaser的更改。

1. 返回浏览器并重新刷新主页:[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。 您应看到已应用更新的产品Teaser样式。

   ![更新的产品Teaser样式](../assets/style-cif-component/product-teaser-new-style.png)

1. 通过添加其他产品Teaser进行试验。 使用布局模式更改组件的宽度和偏移，以在一行中显示多个Teaser。

   ![多个产品Teaser](../assets/style-cif-component/multiple-teasers-final.png)

## 疑难解答 {#troubleshooting}

您可以在[CRXDE-Lite](http://localhost:4502/crx/de/index.jsp)中验证已部署更新的CSS文件：[http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css](http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css)

部署新的CSS和/或JavaScript文件时，确保浏览器不提供旧文件也很重要。 您可以通过清除浏览器缓存或启动新的浏览器会话来消除这种情况。

AEM还尝试缓存客户端库以提高性能。 偶尔，在代码部署之后，会提供旧文件。 可以使用[重建客户端库工具](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html)手动使AEM客户端库缓存失效。 *如果您怀疑AEM已缓存客户端库的旧版本，则首选使用Invalidate Cache。重建库效率低下且耗时。*

## 祝贺您{#congratulations}

您刚设置了您的第一个AEM CIF核心组件的样式，并且您使用了Webpack开发服务器！

## 奖金挑战{#bonus-challenge}

使用[AEM Style system](/help/sites-authoring/style-system.md)创建可由内容作者打开/关闭的两种样式。 [使用样式系统进](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) 行开发包括如何实现此目的的详细步骤和信息。

![奖金挑战 — 样式系统](../assets/style-cif-component/bonus-challenge.png)

## 其他资源 {#additional-resources}

* [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
* [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)
* [设置本地AEM开发环境](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)
* [客户端库](/help/sites-developing/clientlibs.md)
* [AEM Sites入门](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
* [用样式体系进行开发](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
