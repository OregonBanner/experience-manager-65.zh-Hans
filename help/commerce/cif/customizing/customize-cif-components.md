---
title: 自定义CIF核心组件
description: 了解如何自定义AEM CIF核心组件。 本教程介绍如何安全扩展CIF核心组件以满足业务特定要求。 了解如何扩展GraphQL查询以返回自定义属性并在CIF核心组件中显示新属性。
sub-product: 商务
topics: Development
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '2541'
ht-degree: 1%

---

# 自定义AEM CIF核心组件{#customize-cif-components}

[CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia)是使用[CIF核心组件](https://github.com/adobe/aem-core-cif-components)的参考代码库。 在本教程中，您将进一步扩展[产品Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser)组件，以显示来自Magento的自定义属性。 您还将进一步了解AEM与Magento之间的GraphQL集成以及CIF核心组件提供的扩展挂钩。

>[!TIP]
>
> 启动您自己的商务实施时，请使用[AEM Project原型](https://github.com/adobe/aem-project-archetype)。

## 您将构建的

韦尼亚品牌最近开始使用可持续材料生产某些产品，该企业希望将&#x200B;**Eco Friendly**&#x200B;徽章作为产品Teaser的一部分显示。 将在Magento中创建新的自定义属性，以指示产品是否使用&#x200B;**Eco friendly**&#x200B;材料。 此自定义属性随后将添加为GraphQL查询的一部分，并显示在指定产品的产品Teaser中。

![《生态友好徽章最终实施》](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 前提条件 {#prerequisites}

完成本教程需要一个本地开发环境。 这包括已配置并连接到Magento实例的AEM运行实例。 查看使用AEM](../develop.md)设置本地开发的要求和步骤。 [要完全学习本教程，您需要权限才能在Magento中向Product](https://docs.magento.com/user-guide/catalog/product-attributes-add.html)添加[属性。

您还需要GraphQL IDE（如[GraphiQL](https://github.com/graphql/graphiql)）或浏览器扩展)来运行代码示例和教程。 如果您安装了浏览器扩展，请确保它能够设置请求标头。 在Google Chrome上，[Altair GraphQL Client](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja)是可以执行该作业的扩展。

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

1. 此时，您应拥有连接到Magento实例的店面的工作版本。 导航到`US` > `Home`页，网址为：[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

   您应该看到店面当前使用Venia主题。 展开店面的主菜单时，您应会看到各种类别，表示连接Magento正在工作。

   ![配置了Venia主题的店面](../assets/customize-cif-components/venia-store-configured.png)

## 创作产品Teaser {#author-product-teaser}

产品Teaser组件将在本教程中进行扩展。 作为第一步，将产品Teaser的新实例添加到主页以了解基准功能。

1. 导航到站点的&#x200B;**主页**:[http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. 将新的&#x200B;**产品Teaser**&#x200B;组件插入页面的主布局容器。

   ![插入产品Teaser](../assets/customize-cif-components/product-teaser-add-component.png)

3. 展开侧面板（如果尚未切换），将资产查找器下拉列表切换到&#x200B;**产品**。 这应显示来自连接Magento实例的可用产品列表。 选择一个产品，并将其&#x200B;**drag+drop**&#x200B;拖放到页面上的&#x200B;**产品Teaser**&#x200B;组件上。

   ![拖放产品Teaser](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > 注意，您还可以通过使用对话框配置组件来配置显示的产品（单击&#x200B;_扳手_&#x200B;图标）。

4. 您现在应当看到一个产品正在由产品Teaser显示。 产品名称和产品价格是显示的默认属性。

   ![产品Teaser — 默认样式](../assets/customize-cif-components/product-teaser-default-style.png)

## 在Magento{#add-custom-attribute}中添加自定义属性

AEM中显示的产品和产品数据存储在Magento中。 接下来，使用MagentoUI将&#x200B;**Eco Friendly**&#x200B;的新属性添加为产品属性集的一部分。

>[!TIP]
>
> 您的产品属性集中是否已经有自定义&#x200B;**Yes/No**&#x200B;属性？ 请随时使用它并跳过此部分。

1. 登录到您的Magento实例。
1. 导航到&#x200B;**Catalog** > **Products**。
1. 更新搜索筛选器以查找在添加到上一个练习中的Teaser组件时使用的&#x200B;**可配置产品**。 在编辑模式下打开产品。

   ![搜索Valeria产品](../assets/customize-cif-components/search-valeria-product.png)

1. 在产品视图中，单击&#x200B;**添加属性** > **创建新属性**。
1. 使用以下值填写&#x200B;**新建属性**&#x200B;表单（保留其他值的默认设置）

   | 字段集 | 字段标签 | 值 |
   | ----------------------------- | ------------------ | ---------------- |
   | 属性属性 | 属性标签 | **生态友好** |
   | 属性属性 | 目录输入类型 | **是/否** |
   | 高级属性 | 属性代码 | **eco_friendly** |

   ![新建属性表单](../assets/customize-cif-components/attribute-new-form.png)

   完成后，单击&#x200B;**保存属性**。

1. 滚动到产品底部并展开&#x200B;**Attributes**&#x200B;标题。 您应当看到新的&#x200B;**Eco Friendly**&#x200B;字段。 切换到&#x200B;**是**。

   ![切换为“是”](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **** 保存对产品的更改。

   >[!TIP]
   >
   > 有关管理[产品属性的更多详细信息，请参阅Magento用户指南](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html)。

1. 导航到&#x200B;**System** > **Tools** > **Cache Management**。 由于对模式进行了更新，因此我们需要使Magento中的某些缓存类型失效。
1. 选中&#x200B;**Configuration**&#x200B;旁边的框，并提交&#x200B;**Refresh**&#x200B;的缓存类型

   ![刷新配置缓存类型](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > 有关[缓存管理的更多详细信息，请参阅Magento用户指南](https://docs.magento.com/user-guide/system/cache-management.html)。

## 使用GraphQL IDE验证属性{#use-graphql-ide}

在跳入AEM代码之前，使用GraphQL IDE浏览[MagentoGraphQL](https://devdocs.magento.com/guides/v2.4/graphql/)非常有用。 与AEM的Magento集成主要通过一系列GraphQL查询完成。 了解和修改GraphQL查询是扩展CIF核心组件的关键方法之一。

接下来，使用GraphQL IDE验证`eco_friendly`属性是否已添加到产品属性集。 本教程中的屏幕截图使用[Altair GraphQL客户端](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja)。

1. 打开GraphQL IDE，并在IDE或扩展的URL栏中输入URL `http://<magento-server>/graphql`。
2. 添加以下[产品查询](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html)，其中`YOUR_SKU`是上一练习中使用的产品的&#x200B;**SKU**:

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

3. 执行查询，您应得到如下响应：

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

   请注意，**Yes**&#x200B;的值是&#x200B;**1**&#x200B;的整数。 当我们使用Java编写GraphQL查询时，这将很有用。

   >[!TIP]
   >
   > 有关[MagentoGraphQL的更详细文档，请参阅此处](https://devdocs.magento.com/guides/v2.4/graphql/index.html)。

## 更新产品Teaser {#updating-sling-model-product-teaser}的Sling模型

接下来，我们将通过实施Sling模型来扩展产品Teaser的业务逻辑。 [Sling Models](https://sling.apache.org/documentation/bundles/models.html)是注释驱动的“POJO”(Plain Old Java Objects)，可实现组件所需的任何业务逻辑。Sling Models与HTL脚本结合使用，作为组件的一部分。 我们将遵循Sling Models](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models)的[委托模式，以便我们只扩展现有产品Teaser模型的部分。

Sling Models是作为Java实现的，可在生成的项目的&#x200B;**core**&#x200B;模块中找到。

使用您选择的[IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide)导入Venia项目。 使用的截屏来自[ Visual Studio代码IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)。

1. 在IDE中，在&#x200B;**core**&#x200B;模块下导航：`core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`。

   ![核心位置IDE](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` 是扩展CIF ProductTeaser接口的 [](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) Java接口。

   已经添加了名为`isShowBadge()`的新方法，以在产品被视为“New”时显示徽章。

1. 向接口添加新方法`isEcoFriendly()`:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   这是我们将引入的一种新方法，用于封装逻辑，以指示产品的`eco_friendly`属性是否设置为&#x200B;**Yes**&#x200B;或&#x200B;**No**。

1. 然后，在`core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`检查`MyProductTeaserImpl.java`。

   Sling Models](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models)的[委派模式允许`MyProductTeaserImpl`通过`sling:resourceSuperType`属性引用`ProductTeaser`模型：

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   对于所有不想覆盖或更改的方法，我们只需返回`ProductTeaser`返回的值即可。 例如：

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   这将最小化实现需要写入的Java代码量。

1. AEM CIF核心组件提供的额外扩展点之一是`AbstractProductRetriever`，它提供对特定产品属性的访问。 Inspect `initModel()`方法：

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

   `@PostConstruct`注释确保在初始化Sling Model后立即调用此方法。

   请注意，产品GraphQL查询已使用`extendProductQueryWith`方法进行扩展，以检索附加的`created_at`属性。 此属性稍后将用作`isShowBadge()`方法的一部分。

1. 更新GraphQL查询以在部分查询中包含`eco_friendly`属性：

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p ->
                productRetriever.extendProductQueryWith(p -> p
                   .createdAt()
                   .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
               );
           );
       }
   }
   ```

   添加到`extendProductQueryWith`方法是确保其他产品属性可用于模型其余部分的一种有效方法。 它还会最小化执行的查询数。

   在上述代码中，`addCustomSimpleField`用于检索`eco_friendly`属性。 这说明了如何查询属于Magento模式的任何自定义属性。

   >[!NOTE]
   >
   > `createdAt()`方法实际上已作为[产品接口](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java)的一部分实现。 大多数常见的模式属性都已实现，因此仅对真正的自定义属性使用`addCustomSimpleField`。

1. 添加记录器以帮助调试Java代码：

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. 接下来，实现`isEcoFriendly()`方法：

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

   在上述方法中，使用`productRetriever`获取产品，使用`getAsInteger()`方法获取`eco_friendly`属性的值。 根据我们之前运行的GraphQL查询，我们知道当`eco_friendly`属性设置为“**是**”时的预期值实际上是&#x200B;**1**&#x200B;的整数。

   既然Sling模型已更新，则需要更新组件标记，以便根据Sling模型实际显示&#x200B;**Eco Friendly**&#x200B;指示符。

## 自定义产品Teaser {#customize-markup-product-teaser}的标记

AEM组件的一个常见扩展是修改组件生成的标记。 通过覆盖组件用于呈现其标记的[HTL脚本](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html)来完成此操作。 HTML模板语言(HTL)是一种轻量级模板语言，AEM组件使用它根据创作的内容动态渲染标记，从而允许重复使用组件。 例如，可以反复重新使用产品Teaser来显示不同的产品。

在我们的案例中，我们希望在Teaser顶部渲染一个横幅，以指示产品基于自定义属性为“Eco Friendly”。 自定义组件标记[的设计模式实际上是所有AEM组件(而不仅仅是AEM CIF核心组件)的标准。](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup)

1. 在IDE中，导航并展开`ui.apps`模块，然后展开文件夹层次结构以：`ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser`并检查`.content.xml`文件。

   ![产品Teaser ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   以上是我们项目中产品Teaser组件的组件定义。 注意属性`sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`。 这是创建[Proxy组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components)的示例。 我们可以使用`sling:resourceSuperType`继承所有功能，而不是从AEM CIF核心组件复制和粘贴所有Product Teaser HTL脚本。

1. 打开文件`productteaser.html`。 这是[CIF产品Teaser](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)中`productteaser.html`文件的副本

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

   请注意，`MyProductTeaser`的Sling Model已使用并分配给`product`变量。

1. 修改`productteaser.html`以调用在上一个练习中实现的`isEcoFriendly`方法：

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

   当在HTL中调用Sling Model方法时，将删除该方法的`get`和`is`部分，并将第一个字母小写。 因此，`isShowBadge()`变为`.showBadge`,`isEcoFriendly`变为`.ecoFriendly`。 根据从`.isEcoFriendly()`返回的布尔值确定是否显示`<span>Eco Friendly</span>`。

   有关`data-sly-test`和其他[HTL块语句的详细信息，请访问](https://docs.adobe.com/content/help/en/experience-manager-htl/using/htl/block-statements.html#test)。

1. 通过命令行终端保存更改并使用您的Maven技能将更新部署到AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 打开新的浏览器窗口并导航到AEM和&#x200B;**OSGi console** > **状态** > **Sling Models**:[http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. 搜索`MyProductTeaserImpl`，您应看到如下代码行：

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   这表示Sling模型已正确部署并映射到正确的组件。

1. 刷新到&#x200B;**已添加产品预告的[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)的Venia主页**。

   ![显示“Eco Friendly（生态友好）”消息](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   如果产品的`eco_friendly`属性设置为&#x200B;**是**，则页面上应显示文本“Eco Friendly”。 尝试切换到不同的产品以查看行为更改。

1. 下一步打开AEM `error.log`以查看我们添加的日志语句。 `error.log`位于`<AEM SDK Install Location>/crx-quickstart/logs/error.log`。

   搜索AEM日志以查看在Sling Model中添加的日志语句：

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > 如果Teaser中使用的产品没有作为属性集的一部分的`eco_friendly`属性，您也会看到一些堆栈跟踪。

## 为Eco友好徽章{#add-styles}添加样式

此时，显示&#x200B;**Eco Friendly**&#x200B;徽章的逻辑正在工作，但纯文本可能使用某些样式。 然后，向`ui.frontend`模块添加图标和样式以完成实施。

1. 下载[eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg)文件。 此徽章将用作&#x200B;**Eco Friendly**&#x200B;徽章。
1. 返回到IDE并导航到`ui.frontend`文件夹。
1. 将`eco_friendly.svg`文件添加到`ui.frontend/src/main/resources/images`文件夹：

   ![添加了生态友好SVG](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. 在`ui.frontend/src/main/styles/commerce/_productteaser.scss`打开文件`productteaser.scss`。
1. 在`.productteaser`类内添加以下Sass规则：

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
   > 有关前端工作流的更多详细信息，请参阅[样式CIF核心组件](./style-cif-component.md)。

1. 通过命令行终端保存更改并使用您的Maven技能将更新部署到AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 刷新到&#x200B;**已添加产品预告的[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)的Venia主页**。

   ![《生态友好徽章最终实施》](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 祝贺您{#congratulations}

您刚刚自定义了您的第一个AEM CIF组件！ 在此处下载[已完成的解决方案文件](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip)。

## 奖金挑战{#bonus-challenge}

查看已在产品Teaser中实现的&#x200B;**New**&#x200B;徽章的功能。 尝试为作者添加一个额外的复选框以控制何时应显示&#x200B;**Eco Friendly**&#x200B;徽章。 您需要更新`ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`处的组件对话框。

![新徽章实施挑战](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## 其他资源 {#additional-resources}

- [AEM原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
- [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)
- [自定义AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
- [自定义核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
- [AEM Sites入门](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
