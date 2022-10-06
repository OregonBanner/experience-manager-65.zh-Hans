---
title: 自定义CIF核心组件
description: 了解如何自定义AEM CIF核心组件。 本教程介绍如何安全扩展CIF核心组件以满足业务特定要求。 了解如何扩展GraphQL查询以返回自定义属性并在CIF核心组件中显示新属性。
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
exl-id: 8933942e-be49-49d3-bf0a-7225257e2803
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '2604'
ht-degree: 2%

---

# 自定义AEM CIF核心组件 {#customize-cif-components}

的 [CIF韦尼亚项目](https://github.com/adobe/aem-cif-guides-venia) 是用于 [CIF核心组件](https://github.com/adobe/aem-core-cif-components). 在本教程中，您将进一步扩展 [Product Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) 组件来显示来自Adobe Commerce的自定义属性。 您还将进一步了解AEM与Adobe Commerce之间的GraphQL集成以及CIF核心组件提供的扩展挂钩。

>[!TIP]
>
> 使用 [AEM项目原型](https://github.com/adobe/aem-project-archetype) 启动您自己的商务实施时。

## 您将要构建的内容

Venia品牌最近开始使用可持续材料制造一些产品，该公司希望展示 **生态友好** 标记。 将在Adobe Commerce中创建新的自定义属性，以指示产品是否使用 **生态友好** 材料。 然后，此自定义属性将作为GraphQL查询的一部分添加，并显示在指定产品的Product Teaser中。

![生态友好徽章最终实施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 前提条件 {#prerequisites}

需要本地开发环境才能完成本教程。 这包括已配置并连接到Adobe Commerce实例的AEM运行实例。 查看 [使用AEM设置本地开发](../develop.md). 要完整地学习本教程，您需要权限才能添加 [产品属性](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) 在Adobe Commerce。

您还需要GraphQL IDE，例如 [GraphiQL](https://github.com/graphql/graphiql) 或用于运行代码示例和教程的浏览器扩展。 如果安装浏览器扩展，请确保它能够设置请求标头。 在Google Chrome上， [Altair GraphQL客户端](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) 是可以执行该作业的扩展之一。

## 克隆Venia项目 {#clone-venia-project}

我们将克隆 [韦尼亚项目](https://github.com/adobe/aem-cif-guides-venia) ，然后覆盖默认样式。

>[!NOTE]
>
> **随时可以使用现有项目** (基于包含CIF的AEM项目原型)并跳过此部分。

1. 运行以下git命令以克隆项目：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 构建项目并将其部署到AEM的本地实例：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 添加必要的OSGi配置，以将您的AEM实例连接到Adobe Commerce实例，或将配置添加到新创建的项目。

1. 此时，您应该拥有连接到Adobe Commerce实例的店面的工作版本。 导航到 `US` > `Home` 页面： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   您应会看到，当前的店面使用的是Venia主题。 展开店面的主菜单时，您应会看到各种类别，这表示与Adobe Commerce的连接正在工作。

   ![使用Venia主题配置的店面](../assets/customize-cif-components/venia-store-configured.png)

## 创作Product Teaser {#author-product-teaser}

将在本教程中扩展产品Teaser组件。 第一步，将产品Teaser的新实例添加到主页以了解基线功能。

1. 导航到 **主页** 网站： [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. 插入新 **Product Teaser** 组件放入页面上的主布局容器中。

   ![插入产品Teaser](../assets/customize-cif-components/product-teaser-add-component.png)

3. 展开侧面板（如果尚未切换），然后将资产查找器下拉列表切换为 **产品**. 这应会显示连接的Adobe Commerce实例中可用产品的列表。 选择产品和 **拖放** 就在 **Product Teaser** 组件。

   ![拖放产品Teaser](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > 请注意，您还可以通过使用对话框(单击 _扳手_ 图标)。

4. 此时您应会看到产品Teaser正在显示。 产品名称和产品价格是显示的默认属性。

   ![产品Teaser — 默认样式](../assets/customize-cif-components/product-teaser-default-style.png)

## 在Adobe Commerce中添加自定义属性 {#add-custom-attribute}

AEM中显示的产品和产品数据存储在Adobe Commerce中。 接下来，为 **生态友好** 作为使用Adobe Commerce UI设置的产品属性的一部分。

>[!TIP]
>
> 已具有自定义 **是/否** 属性作为产品属性集的一部分？ 请随时使用该插件并跳过此部分。

1. 登录Adobe Commerce实例。
1. 导航到 **目录** > **产品**.
1. 更新搜索过滤器以查找 **可配置产品** 在上一个练习中添加到Teaser组件时使用。 在编辑模式下打开产品。

   ![搜索有效产品](../assets/customize-cif-components/search-valeria-product.png)

1. 在产品视图中，单击 **添加属性** > **创建新属性**.
1. 填写 **新属性** 表单，其值如下（保留其他值的默认设置）

   | 字段集 | 字段标签 | 值 |
   | ----------------------------- | ------------------ | ---------------- |
   | 属性属性 | 属性标签 | **生态友好** |
   | 属性属性 | 目录输入类型 | **是/否** |
   | 高级属性 | 属性代码 | **eco_friendly** |

   ![新属性表单](../assets/customize-cif-components/attribute-new-form.png)

   单击 **保存属性** 完成。

1. 滚动到产品底部并展开 **属性** 标题。 您应会看到新 **生态友好** 字段。 将切换切换切换到 **是**.

   ![切换为是](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **保存** 对产品所做的更改。

   >[!TIP]
   >
   > 有关管理的更多详细信息 [产品属性可在Adobe Commerce用户指南中找到](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html).

1. 导航到 **系统** > **工具** > **缓存管理**. 由于对数据架构进行了更新，因此我们需要使Adobe Commerce中的某些缓存类型失效。
1. 选中旁边的复选框 **配置** 并提交的缓存类型 **刷新**

   ![刷新配置缓存类型](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > 有关 [缓存管理可在Adobe Commerce用户指南中找到](https://docs.magento.com/user-guide/system/cache-management.html).

## 使用GraphQL IDE验证属性 {#use-graphql-ide}

在跳转到AEM代码之前，探索 [Adobe Commerce GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) 使用GraphQL IDE。 与AEM的Adobe Commerce集成主要通过一系列GraphQL查询来完成。 了解和修改GraphQL查询是扩展CIF核心组件的关键方法之一。

接下来，使用GraphQL IDE验证 `eco_friendly` 属性已添加到产品属性集。 本教程中的屏幕截图使用 [Altair GraphQL客户端](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja).

1. 打开GraphQL IDE并输入URL `http://<server>/graphql` 在IDE或扩展的URL栏中。
2. 添加以下内容 [产品查询](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) where `YOUR_SKU` 是 **SKU** 上一练习中使用的产品的“受众”(A):

   ```json
     {
       products(
       filter: { sku: { eq: "YOUR_SKU" } }
       ) {
           items {
           name
           sku
           eco_friendly
           }
       }
   }
   ```

3. 执行查询，您应获得如下响应：

   ```json
   {
     "data": {
       "products": {
         "items": [
           {
             "name": "Valeria Two-Layer Tank",
             "sku": "VT11",
             "eco_friendly": 1
           }
         ]
       }
     }
   }
   ```

   ![示例GraphQL响应](../assets/customize-cif-components/sample-graphql-query.png)

   请注意， **是** 是 **1**. 当我们使用Java编写GraphQL查询时，这将非常有用。

   >[!TIP]
   >
   > 有关 [Adobe Commerce GraphQL可在此处找到](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## 更新Product Teaser的Sling模型 {#updating-sling-model-product-teaser}

接下来，我们将通过实施Sling模型来扩展产品Teaser的业务逻辑。 [Sling模型](https://sling.apache.org/documentation/bundles/models.html)，是注释驱动的“POJO”（普通旧Java对象），用于实施组件所需的任何业务逻辑。 Sling模型会与HTL脚本一起用作组件的一部分。 我们将跟踪 [Sling模型的委派模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) 这样我们就可以扩展现有产品Teaser模型的部分。

Sling模型将作为Java实施，并可在 **核心** 模块。

使用 [您选择的IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) 导入Venia项目。 使用的屏幕截图来自 [Visual Studio代码IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. 在IDE中，在 **核心** 模块： `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![核心位置IDE](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` 是一个扩展CIF的Java界面 [ProductTeaser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) 界面。

   已添加一个名为 `isShowBadge()` ，以在产品被视为“新”时显示徽章。

1. 添加新方法， `isEcoFriendly()` 到界面：

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   这是我们将引入的一种新方法，用于封装逻辑以指示产品是否具有 `eco_friendly` 属性设置为 **是** 或 **否**.

1. 接下来，检查 `MyProductTeaserImpl.java` at `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   的 [Sling模型的委派模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) 允许 `MyProductTeaserImpl` 引用 `ProductTeaser` 通过 `sling:resourceSuperType` 属性：

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   对于我们不希望覆盖或更改的所有方法，我们只需返回 `ProductTeaser` 返回。 例如：

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   这可以最大限度地减少实施需要写入的Java代码量。

1. AEM CIF核心组件提供的额外扩展点之一是 `AbstractProductRetriever` 提供对特定产品属性的访问权限。 Inspect `initModel()` 方法：

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to intialize the proudctRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   的 `@PostConstruct` 注释可确保在初始化Sling模型后立即调用此方法。

   请注意，产品GraphQL查询已使用 `extendProductQueryWith` 用于检索附加 `created_at` 属性。 此属性稍后会用作 `isShowBadge()` 方法。

1. 更新GraphQL查询以包含 `eco_friendly` 属性：

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p -> p
               .createdAt()
               .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
           );
       }
   }
   ```

   添加到 `extendProductQueryWith` 方法是确保模型其余部分可以使用其他产品属性的一种有效方法。 它还可以最大限度地减少所执行查询的数量。

   在上述代码中，`addCustomSimpleField` 用于检索 `eco_friendly` 属性。 这说明了如何查询属于Adobe Commerce架构一部分的任何自定义属性。

   >[!NOTE]
   >
   > 的 `createdAt()` 方法已作为 [产品界面](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java). 大多数常见的架构属性都已实施，因此仅使用 `addCustomSimpleField` ，以了解真正的自定义属性。

1. 添加日志记录器以帮助调试Java代码：

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. 接下来，实施 `isEcoFriendly()` 方法：

   ```java
   @Override
   public Boolean isEcoFriendly() {
   
       Integer ecoFriendlyValue;
       try {
           ecoFriendlyValue = productRetriever.fetchProduct().getAsInteger(ECO_FRIENDLY_ATTRIBUTE);
           if(ecoFriendlyValue != null && ecoFriendlyValue.equals(Integer.valueOf(1))) {
               LOGGER.info("*** Product is Eco Friendly**");
               return true;
           }
       } catch (SchemaViolationError e) {
           LOGGER.error("Error retrieving eco friendly attribute");
       }
       LOGGER.info("*** Product is not Eco Friendly**");
       return false;
   }
   ```

   在上述方法中， `productRetriever` 用于获取产品和 `getAsInteger()` 方法来获取 `eco_friendly` 属性。 根据我们之前运行的GraphQL查询，我们知道当 `eco_friendly` 属性设置为“**是**&quot;实际上是 **1**.

   现在，Sling模型已更新，需要更新组件标记以实际显示 **生态友好** 基于Sling模型。

## 自定义Product Teaser的标记 {#customize-markup-product-teaser}

AEM组件的常见扩展是修改由组件生成的标记。 这是通过覆盖 [HTL脚本](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) 组件用来呈现其标记的标记。 HTML模板语言(HTL)是一种轻量级的模板语言，AEM组件使用它根据创作内容动态渲染标记，从而允许重复使用组件。 例如，可以反复重复使用产品Teaser来显示不同的产品。

在本例中，我们要在Teaser顶部渲染一个横幅，以指示产品基于自定义属性为“生态友好”。 的设计模式 [自定义标记](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) 组件的实际上是所有AEM组件的标准，而不仅仅是AEM CIF核心组件的标准。

>[!NOTE]
>
> 如果您使用CIF产品和类别选取器（如此Product Teaser或CIF页面组件）自定义组件，请确保包含所需的 `cif.shell.picker` 组件对话框的clientlib 。 请参阅 [CIF产品和类别选取器的用法](use-cif-pickers.md) 以了解详细信息。

1. 在IDE中，导航并展开 `ui.apps` 模块，并将文件夹层次结构展开为： `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` 检查 `.content.xml` 文件。

   ![产品Teaser ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   上面是我们项目中Product Teaser组件的组件定义。 请注意资产 `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. 以下是创建 [代理组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components). 我们可以使用，而不是从AEM CIF核心组件中复制和粘贴所有Product Teaser HTL脚本 `sling:resourceSuperType` 继承所有功能。

1. 打开文件 `productteaser.html`. 这是 `productteaser.html` 文件 [CIF产品Teaser](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

   ```html
   <!--/* productteaser.html */-->
   <sly
     data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
     data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
     data-sly-use.actionsTpl="actions.html"
     data-sly-test.isConfigured="${properties.selection}"
     data-sly-test.hasProduct="${product.url}"
   ></sly>
   ```

   请注意， `MyProductTeaser` 的 `product` 变量。

1. 修改 `productteaser.html` 打电话 `isEcoFriendly` 方法：

   ```html
   ...
   <div
     data-sly-test="${isConfigured && hasProduct}"
     class="item__root"
     data-cmp-is="productteaser"
     data-virtual="${product.virtualProduct}"
   >
     <div data-sly-test="${product.showBadge}" class="item__badge">
       <span>${properties.text || 'New'}</span>
     </div>
     <!--/* Insert call to Eco Friendly here */-->
     <div data-sly-test="${product.ecoFriendly}" class="item__eco">
       <span>Eco Friendly</span>
     </div>
     ...
   </div>
   ```

   在HTL中调用Sling模型方法时， `get` 和 `is` 删除该方法的一部分，并将第一个字母转换为小写。 所以 `isShowBadge()` 变量 `.showBadge` 和 `isEcoFriendly` 变量 `.ecoFriendly`. 基于从 `.isEcoFriendly()` 确定是否 `<span>Eco Friendly</span>` 中。

   有关 `data-sly-test` 其他 [可以在此处找到HTL块语句](https://docs.adobe.com/content/help/en/experience-manager-htl/using/htl/block-statements.html#test).

1. 通过命令行终端保存更改并使用您的Maven技能部署对AEM的更新：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 打开新的浏览器窗口，然后导航到AEM和 **OSGi控制台** > **状态** > **Sling模型**: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. 搜索 `MyProductTeaserImpl` 此时您应会看到如下行：

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   这表示Sling模型已正确部署并映射到正确的组件。

1. 刷新到 **韦尼亚主页** at [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) 添加了产品Teaser的位置。

   ![显示生态友好消息](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   如果产品具有 `eco_friendly` 属性设置为 **是**，则应会在页面上看到“Eco Friendly”文本。 尝试切换到不同的产品以查看行为更改。

1. 下一步打开AEM `error.log` 以查看我们添加的log语句。 的 `error.log` 位于 `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   搜索AEM日志以查看在Sling模型中添加的log语句：

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > 如果在Teaser中使用的产品没有 `eco_friendly` 属性。

## 为Eco友好徽章添加样式 {#add-styles}

此时，显示时间的逻辑 **生态友好** 标记正常工作，但纯文本可能使用某些样式。 接下来，向 `ui.frontend` 模块来完成实施。

1. 下载 [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) 文件。 这将用作 **生态友好** 徽章。
1. 返回到IDE并导航到 `ui.frontend` 文件夹。
1. 添加 `eco_friendly.svg` 文件 `ui.frontend/src/main/resources/images` 文件夹：

   ![添加了生态友好SVG](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. 打开文件 `productteaser.scss` at `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. 在 `.productteaser` 类：

   ```scss
   .productteaser {
       ...
       .item__eco {
           width: 60px;
           height: 60px;
           left: 0px;
           overflow: hidden;
           position: absolute;
           padding: 5px;
   
       span {
           display: block;
           position: absolute;
           width: 45px;
           height: 45px;
           text-indent: -9999px;
           background: no-repeat center center url('../resources/images/eco_friendly.svg');
           }
       }
   ...
   }
   ```

   >[!NOTE]
   >
   > 查看 [样式CIF核心组件](./style-cif-component.md) 有关前端工作流的更多详细信息。

1. 通过命令行终端保存更改并使用您的Maven技能部署对AEM的更新：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 刷新到 **韦尼亚主页** at [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) 添加了产品Teaser的位置。

   ![生态友好徽章最终实施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 恭喜 {#congratulations}

您刚刚自定义了第一个AEM CIF组件！ 下载 [此处已完成的解决方案文件](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## 奖金挑战 {#bonus-challenge}

查看 **新建** 已在产品Teaser中实施的标记。 尝试为作者添加一个额外的复选框，以控制 **生态友好** 标记。 您需要在 `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![新徽章实施挑战](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## 其他资源 {#additional-resources}

- [AEM原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
- [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)
- [自定义AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
- [自定义核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
- [开始使用AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
- [CIF产品和类别选取器的用法](use-cif-pickers.md)
