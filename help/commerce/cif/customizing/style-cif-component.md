---
title: 样式AEM CIF核心组件
description: 了解如何设置AEM CIF核心组件的样式。 本教程介绍了如何使用客户端库或clientlibs为Adobe Experience Manager (AEM) Commerce实施部署和管理CSS和Javascript。 本教程还将介绍如何将ui.frontend模块和webpack项目集成到端到端构建过程中。
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
feature: Commerce Integration Framework
kt: 3456
thumbnail: 3456-style-cif.jpg
exl-id: 04d553be-c67d-4ecb-a23f-2694c2adfc2b
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '2551'
ht-degree: 3%

---

# 样式AEM CIF核心组件 {#style-aem-cif-core-components}

此 [CIF Venia项目](https://github.com/adobe/aem-cif-guides-venia) 是一个参考代码库，用于 [CIF核心组件](https://github.com/adobe/aem-core-cif-components). 在本教程中，您将检查Venia参考项目，并了解AEM CIF核心组件使用的CSS和JavaScript的组织方式。 您还将使用CSS创建新样式，以更新 **产品Teaser** 组件。

>[!TIP]
>
>使用 [AEM项目原型](https://github.com/adobe/aem-project-archetype) 在开始您自己的commerce实施时。

## 您将构建的内容

在本教程中，将为类似于信息卡的Product Teaser组件实施一个新样式。 从本教程中吸取的经验教训可以应用于其他CIF核心组件。

![您将构建的内容](../assets/style-cif-component/what-you-will-build.png)

## 前提条件 {#prerequisites}

需要本地开发环境来完成本教程。 这包括正在运行的AEM实例，该实例已配置并连接到Adobe Commerce实例。 查看的要求和步骤 [使用AEM设置本地开发](../develop.md).

## 克隆Venia项目 {#clone-venia-project}

我们将克隆 [Venia项目](https://github.com/adobe/aem-cif-guides-venia) 然后覆盖默认样式。

>[!NOTE]
>
>**可以随意使用现有项目** (基于包含CIF的AEM项目原型)并跳过此部分。

1. 运行以下git命令以克隆项目：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 生成项目并将其部署到AEM的本地实例：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 添加必要的OSGi配置以将您的AEM实例连接到Adobe Commerce实例，或将配置添加到新创建的项目。

1. 此时，您应该拥有连接到Adobe Commerce实例的工作中店面版本。 导航到 `US` > `Home` 页面位置： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   您应该会看到店面当前使用的是Venia主题。 展开店面的主菜单，您应该会看到各种类别，这表示与Adobe Commerce的连接正在正常工作。

   ![用Venia主题配置的店面](../assets/style-cif-component/venia-store-configured.png)

## 客户端库和ui.frontend模块 {#introduction-to-client-libraries}

在AEM中，负责呈现店面主题/样式的CSS和JavaScript由 [客户端库](/help/sites-developing/clientlibs.md) 或clientlibs简称。 客户端库提供了一种机制，用于在项目代码中组织CSS和Javascript，然后将其交付到页面上。

通过添加和覆盖由这些客户端库管理的CSS，可以将品牌特定的样式应用到AEM CIF核心组件。 了解如何在页面上构建和包含客户端库至关重要。

此 [ui.frontend](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) 是专用的 [webpack](https://webpack.js.org/) 用于管理项目的所有前端资产的项目。 这允许前端开发人员使用任意数量的语言和技术，例如 [TypeScript](https://www.typescriptlang.org/)， [萨斯](https://sass-lang.com/) 等等。

此 `ui.frontend` 模块也是Maven模块，并通过使用NPM模块与更大的项目集成 [aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator). 在构建期间， `aem-clientlib-generator` 将编译后的CSS和JavaScript文件复制到中的客户端库中 `ui.apps` 模块。

![ui.frontend到ui.apps架构](../assets/style-cif-component/ui-frontend-architecture.png)

*编译的CSS和Javascript复制自 `ui.frontend` 模块移入 `ui.apps` 在Maven构建期间用作客户端库的模块*

## 更新Teaser样式 {#ui-frontend-module}

接下来，对Teaser样式进行小幅更改，以了解 `ui.frontend` 模块和客户端库均可用。 使用 [您选择的IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) 以导入Venia项目。 使用的屏幕截图来自 [Visual Studio Code IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. 导航并展开 **ui.frontend** 模块并将文件夹层次结构展开到： `ui.frontend/src/main/styles/commerce`：

   ![ui.frontend商业文件夹](../assets/style-cif-component/ui-frontend-commerce-folder.png)

   请注意，存在多个Sass (`.scss`)文件。 这些是每个Commerce组件的Commerce特定样式。

1. 打开文件 `_productteaser.scss`.

1. 更新 `.item__image` 规则并修改边框规则：

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

   上述规则应为产品Teaser组件添加非常粗体的粉红色边框。

1. 打开新的终端窗口并导航到 `ui.frontend` 文件夹：

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

   Inspect终端输出。 您将看到Maven命令执行了多个NPM脚本，包括 `npm run build`. 此 `npm run build` 命令在 `package.json` 文件，具有编译webpack项目和触发客户端库生成的效果。

1. Inspect文件 `ui.frontend/dist/clientlib-site/site.css`：

   ![已编译的站点CSS](../assets/style-cif-component/comiled-site-css.png)

   该文件是项目中所有Sass文件的编译和缩小版本。

   >[!NOTE]
   >
   >此类文件会从源代码管理中忽略，因为它们应在构建期间生成。

1. Inspect文件 `ui.frontend/clientlib.config.js`.

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

   这是的配置文件 [aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator) 和确定编译后的CSS和JavaScript转换为AEM客户端库的位置和方式。

1. 在 `ui.apps` 模块检查文件： `ui.apps/src/main/content/jcr_root/apps/venia/clientlibs/clientlib-site/css/site.css`：

   ![ui.apps中已编译的站点CSS](../assets/style-cif-component/comiled-css-ui-apps.png)

   这将复制 `site.css` 文件放入中 `ui.apps` 项目。 它现在包含在名为的客户端库中 `clientlib-site` 具有类别 `venia.site`. 一旦文件成为 `ui.apps` 模块。可以将其部署到AEM。

   >[!NOTE]
   >
   >此类文件也会从源代码管理中忽略，因为它们应在构建期间生成。

1. 接下来，检查项目生成的其他客户端库：

   ![其他客户端库](../assets/style-cif-component/other-clientlibs.png)

   这些客户端库不受 `ui.frontend` 模块。 相反，这些客户端库包含由Adobe提供的CSS和JavaScript依赖项。 这些客户端库的定义位于 `.content.xml` 文件（在每个文件夹下）。

   **clientlib-base**  — 这是一个空的客户端库，它只是从嵌入必要的依赖项 [AEM核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans). 类别为 `venia.base`.

   **clientlib-cif**  — 这也是一个空的客户端库，它只是从中嵌入必要的依赖项 [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components). 类别为 `venia.cif`.

   **clientlib-grid**  — 这包括启用AEM响应式网格功能所需的CSS。 使用AEM网格可启用 [布局模式](/help/sites-authoring/responsive-layout.md) 通过AEM编辑器，内容作者可以调整组件的大小。 类别为 `venia.grid` 并嵌入在 `venia.base` 库。

1. Inspect文件 `customheaderlibs.html` 和 `customfooterlibs.html` 下 `ui.apps/src/main/content/jcr_root/apps/venia/components/page`：

   ![自定义页眉和页脚脚本](../assets/style-cif-component/custom-header-footer-script.png)

   这些脚本包括 **venia.base** 和 **venia.cif** 库作为所有页面的一部分。

   >[!NOTE]
   >
   >在页面脚本中，只有基础库是“硬编码”的。 `venia.site` 不会包含在这些文件中，而是作为页面模板的一部分包含，以便更加灵活。 稍后将对此进行检查。

1. 从终端，构建整个项目并将其部署到AEM的本地实例：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

## 创作产品Teaser {#author-product-teaser}

现在已部署代码更新，请使用AEM创作工具将新的Product Teaser组件实例添加到网站的主页。 这将允许我们查看更新的样式。

1. 打开新的浏览器选项卡，然后导航到 **主页** 网站的： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. 在中展开资产查找器（侧边栏） **编辑** 模式。 将资源筛选器切换到 **产品**.

   ![展开资产查找器并按产品进行筛选](../assets/style-cif-component/drag-drop-product-page.png)

1. 将新产品拖放到主布局容器的主页上：

   ![带粉红色边框的产品Teaser](../assets/style-cif-component/pink-border-product-teaser.png)

   您应该会看到，根据之前创建的CSS规则更改，产品Teaser现在具有亮粉红色边框。

## 验证页面上的客户端库 {#verify-client-libraries}

接下来，验证页面上是否包含客户端库。

1. 导航到 **主页** 网站的： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. 选择 **页面信息** 菜单并单击 **查看已发布的项目**：

   ![以发布的形式查看](../assets/style-cif-component/view-as-published.png)

   这将打开页面，而不加载任何AEM创作javascript，就像在已发布的站点上一样。 请注意，url具有查询参数 `?wcmmode=disabled` 已附加。 在开发CSS和Javascript时，最好使用此参数来简化页面，而无需使用AEM创作中的任何内容。

1. 查看页面源，您应该能够识别包括多个客户端库：

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

   客户端库在交付到页面时带有前缀 `/etc.clientlibs` 并通过提供 [代理](/help/sites-developing/clientlibs.md) 以避免泄露任何敏感内容 `/apps` 或 `/libs`.

   注意 `venia/clientlibs/clientlib-site.min.css` 和 `venia/clientlibs/clientlib-site.min.js`. 它们是编译的CSS和Javascript文件，派生自 `ui.frontend` 模块。

## 包含客户端库和页面模板 {#client-library-inclusion-pagetemplates}

有几个选项可用于包含客户端库。 接下来，检查生成的项目如何包含 `clientlib-site` 库，通过 [页面模板](/help/sites-developing/templates.md).

1. 导航到 **主页** AEM网站的URL路径： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. 选择 **页面信息** 菜单并单击 **编辑模板**：

   ![编辑模板](../assets/style-cif-component/edit-template.png)

   这将打开 **登陆页面** 模板 **主页** 页面基于。

   >[!NOTE]
   >
   >要从AEM开始屏幕查看所有可用的模板，请导航到 **工具** > **常规** > **模板**.

1. 在左上角，选择 **页面信息** 图标并单击 **页面策略**.

   ![页面策略菜单项](../assets/style-cif-component/page-policy-menu.png)

1. 这将打开登陆页面的页面策略模板：

   ![页面策略 — 登陆页面](../assets/style-cif-component/page-policy-properties.png)

   在右侧，您可以看到客户端库的列表 **类别** 该模板将被包含在使用此模板的所有页面中。

   * `venia.dependencies`  — 提供符合以下条件的任何供应商库： `venia.site` 取决于。
   * `venia.site`  — 这是的类别 `clientlib-site` 该 `ui.frontend` 模块生成。

   请注意，其他模板使用相同的策略， **内容页面**， **登陆页面**，等等。 通过重复使用相同的策略，我们可以确保在所有页面上包含相同的客户端库。

   使用模板和页面策略管理客户端库包含的好处是，您可以根据模板更改策略。 例如，您可能在同一个AEM实例中管理两个不同的品牌。 每个品牌都有自己独特的风格或 *主题* 但基础库和代码将相同。 另一个示例是，如果您有一个更大的客户端库，而您只想显示在某些页面上，则可以为该模板制定一个唯一的页面策略。

## 本地Webpack开发 {#local-webpack-development}

在上一个练习中，更新了 `ui.frontend` 模块，然后在执行Maven构建后，将更改部署到AEM。 接下来，我们将考虑利用webpack-dev-server快速开发前端样式。

webpack-dev-server代理来自AEM的本地实例的图像和一些CSS/JavaScript，但允许开发人员修改中的样式和JavaScript `ui.frontend` 模块。

1. 在浏览器中，导航到 **主页** 页面和 **查看已发布的项目**： [http://localhost:4502/content/venia/us/en.html?wcmmode=disabled](http://localhost:4502/content/venia/us/en.html?wcmmode=disabled).

1. 查看页面源和 **复制** 页面的原始HTML。

1. 返回您选择的IDE，位于 `ui.frontend` 模块打开文件： `ui.frontend/src/main/static/index.html`

   ![静态HTML文件](../assets/style-cif-component/static-index-html.png)

1. 覆盖的内容 `index.html` 和 **粘贴** 上一步中复制的HTML。

1. 查找的包含 `clientlib-site.min.css`， `clientlib-site.min.js` 和 **移除** 他们。

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

   由于它们表示由生成的CSS和JavaScript的编译版本，因此将被删除 `ui.frontend` 模块。 保留将从正在运行的AEM实例代理的其他客户端库。

1. 打开新的终端窗口并导航到 `ui.frontend` 文件夹。 运行命令 `npm start`：

   ```shell
   $ cd ui.frontend
   $ npm start
   ```

   这将启动webpack-dev-server [http://localhost:8080/](http://localhost:8080/)

   >[!CAUTION]
   >
   >如果收到Sass相关错误，请停止服务器并运行命令 `npm rebuild node-sass` 并重复上述步骤。 如果您有其他版本的 `npm` 和 `node` 然后在项目中指定 `aem-cif-guides-venia/pom.xml`.

1. 导航到 [http://localhost:8080/](http://localhost:8080/) 与登录的AEM实例使用同一浏览器的新选项卡中。 您应会通过webpack-dev-server看到Venia主页：

   ![端口80上的Webpack开发服务器](../assets/style-cif-component/webpack-dev-server-port80.png)

   使webpack-dev-server保持运行状态。 它将在下一个练习中使用。

## 实施产品Teaser的卡片样式 {#update-css-product-teaser}

接下来，修改 `ui.frontend` 模块，用于为Product Teaser实施类似卡片的样式。 webpack-dev-server将用于快速查看更改。

返回到IDE和生成的项目。

1. 在 **ui.frontend** 模块重新打开文件 `_productteaser.scss` 在 `ui.frontend/src/main/styles/commerce/_productteaser.scss`.

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

   保存更改，webpack-dev-server应自动使用新样式刷新。

1. 在产品Teaser中添加投影并包括圆角。

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

1. 更新产品的价格以使其也显示在Teaser的底部，并修改文本颜色。

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

1. 更新底部的媒体查询，在小于的屏幕中栈叠名称和价格 **992像素**.

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

   此时，您应会看到卡片样式反映在webpack-dev-server中：

   ![Webpack开发服务器Teaser更改](../assets/style-cif-component/webpack-dev-server-teaser-changes.png)

   但是，这些更改尚未部署到AEM。 您可以下载 [此处为解决方案文件](../assets/style-cif-component/_productteaser.scss).

1. 使用您的Maven技能从命令行终端将更新部署到AEM：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

   >[!NOTE]
   >还有其他的 [IDE设置和工具](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) 可以直接将项目文件同步到本地AEM实例，而无需执行完整的Maven构建。

## 查看更新的产品Teaser {#view-updated-product-teaser}

将项目代码部署到AEM后，我们现在应该能够查看产品Teaser的更改。

1. 返回浏览器并重新整理主页： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html). 您应该会看到已应用的更新后的产品Teaser样式。

   ![更新了产品Teaser样式](../assets/style-cif-component/product-teaser-new-style.png)

1. 通过添加其他产品Teaser进行试验。 使用“布局模式”可更改组件的宽度和偏移，以便一行显示多个Teaser。

   ![多个产品Teaser](../assets/style-cif-component/multiple-teasers-final.png)

## 疑难解答 {#troubleshooting}

您可以验证 [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) 已部署更新的CSS文件： [http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css](http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css)

在部署新的CSS和/或JavaScript文件时，确保浏览器不提供过时文件也很重要。 您可以通过清除浏览器缓存或启动新的浏览器会话来消除此情况。

AEM还会尝试缓存客户端库以提高性能。 有时，在代码部署后，会提供旧文件。 您可以使用手动使AEM客户端库缓存失效 [重建客户端库工具](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html). *如果您怀疑AEM缓存了客户端库的旧版本，首选方法是使缓存无效。 重建库效率低下且耗时。*

## 恭喜 {#congratulations}

您刚刚创建了第一个AEM CIF核心组件的样式，并且使用了webpack开发服务器！

## 奖励质询 {#bonus-challenge}

使用 [AEM样式系统](/help/sites-authoring/style-system.md) 创建可由内容作者打开/关闭的两种样式。 [用样式系统进行开发](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/style-system.html) 包括有关如何完成此操作的详细步骤和信息。

![附加练习 — 样式系统](../assets/style-cif-component/bonus-challenge.png)

## 其他资源 {#additional-resources}

* [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
* [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)
* [设置本地AEM开发环境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)
* [客户端库](/help/sites-developing/clientlibs.md)
* [AEM Sites快速入门](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans)
* [用样式系统进行开发](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/style-system.html)
