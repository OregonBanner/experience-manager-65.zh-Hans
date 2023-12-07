---
title: 针对目标内容进行开发
description: 有关开发用于内容定位的组件的主题
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 92b62532-4f79-410d-903e-d2bca6d0fd1c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 3%

---

# 针对目标内容进行开发{#developing-for-targeted-content}

本节介绍有关开发用于内容定位的组件的主题。

* 有关连接到Adobe Target的信息，请参阅 [与Adobe Target集成](/help/sites-administering/target.md).
* 有关创作目标内容的信息，请参阅 [使用定位模式创作目标内容](/help/sites-authoring/content-targeting-touch.md).

>[!NOTE]
>
>在 AEM 创作实例中定位组件时，该组件会对 Adobe Target 进行一系列的服务器端调用，以便注册活动、设置选件和检索 Adobe Target 区段（如果已配置）。没有从 AEM Publish 到 Adobe Target 的服务器端调用。

## 在您的页面上使用Adobe Target启用定位功能 {#enabling-targeting-with-adobe-target-on-your-pages}

要在与Adobe Target交互的页面中使用目标组件，请在页面的 &lt;head> 元素。

### 头部部分 {#the-head-section}

将以下两个代码块添加到 &lt;head> 部分：

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

此代码添加所需的Analytics JavaScript对象，并加载与网站关联的云服务库。 对于Target服务，库通过以下方式加载： `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

加载的库集取决于Target配置中使用的Target客户端库类型（mbox.js或at.js）：

**对于默认mbox.js**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/mbox.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**对于自定义mbox.js**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/mbox.js"></script>
        <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**对于at.js**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs.js"></script>
```

>[!NOTE]
>
>仅版本 `at.js` 随产品一起提供的受支持。 的版本 `at.js` 随产品一起发运时，可通过查看 `at.js` 文件位置：
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**.

**对于自定义at.js**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

客户端上的Target功能由管理 `CQ_Analytics.TestTarget` 对象。 因此，该页面将包含一些init代码，如以下示例中的：

```
<script type="text/javascript">
            if ( !window.CQ_Analytics ) {
                window.CQ_Analytics = {};
            }
            if ( !CQ_Analytics.TestTarget ) {
                CQ_Analytics.TestTarget = {};
            }
            CQ_Analytics.TestTarget.clientCode = 'my_client_code';
        </script>
      ...

    <div class="cloudservice testandtarget">
  <script type="text/javascript">
  CQ_Analytics.TestTarget.maxProfileParams = 11;

  if (CQ_Analytics.CCM) {
   if (CQ_Analytics.CCM.areStoresInitialized) {
    CQ_Analytics.TestTarget.registerMboxUpdateCalls();
   } else {
    CQ_Analytics.CCM.addListener("storesinitialize", function (e) {
     CQ_Analytics.TestTarget.registerMboxUpdateCalls();
    });
   }
  } else {
   // client context not there, still register calls
   CQ_Analytics.TestTarget.registerMboxUpdateCalls();
  }
  </script>
 </div>
```

JSP将添加所需的Analytics JavaScript对象和对客户端JavaScript库的引用。 testandtarget.js文件包含mbox.js函数。 脚本生成的HTML类似于以下示例：

```xml
<script type="text/javascript">
        if ( !window.CQ_Analytics ) {
            window.CQ_Analytics = {};
        }
        if ( !CQ_Analytics.TestTarget ) {
            CQ_Analytics.TestTarget = {};
        }
        CQ_Analytics.TestTarget.clientCode = 'MyClientCode';
</script>
<link rel="stylesheet" href="/etc/clientlibs/foundation/testandtarget/testandtarget.css" type="text/css">
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/testandtarget.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/init.js"></script>
```

#### 正文部分（开始） {#the-body-section-start}

紧接着添加以下代码 &lt;body> 标记以将客户端上下文功能添加到页面：

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### 主体部分（结束） {#the-body-section-end}

将以下代码直接添加到 &lt;/body> 结束标记：

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

此组件的JSP脚本会生成对Target javascript API的调用，并实施其他所需的配置。 脚本生成的HTML类似于以下示例：

```xml
<div class="servicecomponents cloudservices">
  <div class="cloudservice testandtarget">
    <script type="text/javascript">
      CQ_Analytics.TestTarget.maxProfileParams = 11;
      CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
        CQ_Analytics.TestTarget.registerMboxUpdateCalls();
      });
    </script>
    <div id="cq-analytics-texthint" style="background:white; padding:0 10px; display:none;">
      <h3 class="cq-texthint-placeholder">Component clientcontext is missing or misplaced.</h3>
    </div>
    <script type="text/javascript">
      $CQ(function(){
      if( CQ_Analytics &&
          CQ_Analytics.ClientContextMgr &&
          !CQ_Analytics.ClientContextMgr.isConfigLoaded )
        {
          $CQ("#cq-analytics-texthint").show();
        }
      });
    </script>
  </div>
</div>
```

### 使用自定义Target库文件 {#using-a-custom-target-library-file}

>[!NOTE]
>
>如果您没有使用DTM或其他目标营销系统，则可以使用自定义目标库文件。

>[!NOTE]
>
>默认情况下，mbox处于隐藏状态 — mboxDefault类决定此行为。 隐藏mbox可确保访客在切换默认内容之前不会看到该内容；但是，隐藏mbox会影响感知到的性能。

用于创建mbox的默认mbox.js文件位于/etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js。 要使用客户mbox.js文件，请将该文件添加到Target云配置。 要添加文件，mbox.js文件必须在文件系统中可用。

例如，如果要使用 [Marketing CloudID服务](https://experienceleague.adobe.com/docs/id-service/using/home.html) 您需要下载mbox.js，以便它包含的正确值 `imsOrgID` 变量，该变量基于您的租户。 要与Marketing CloudID服务集成，需要此变量。 有关信息，请参阅 [将Adobe Analytics作为Adobe Target报表源](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) 和 [实施之前](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html).

>[!NOTE]
>
>如果在Target配置中定义了自定义mbox，则每个人都必须拥有对的读取访问权限 **/etc/cloudservices** 发布服务器上。 如果没有此访问权限，在发布网站上加载mbox.js文件会导致404错误。

1. 转到CQ **工具** 页面并选择 **Cloud Service**. ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. 在树中选择Adobe Target，然后在配置列表中双击Target配置。
1. 在配置页面上，单击编辑。
1. 对于“自定义mbox.js”属性，单击“浏览”并选择该文件。
1. 要应用更改，请输入Adobe Target帐户的密码，单击“重新连接到Target”，然后在连接成功后单击“确定”。 然后，在“编辑组件”对话框中单击“确定”。

您的Target配置包含一个自定义mbox.js文件， [head部分中的必需代码](/help/sites-developing/target.md#p-the-head-section-p) 的中，会将文件添加到客户端库框架，而不是testandtarget.js库的引用。

## 禁用组件的Target命令 {#disabling-the-target-command-for-components}

大多数组件都可以使用上下文菜单上的“目标”命令转换为目标组件。

![chlimage_1-21](assets/chlimage_1-21.png)

要从上下文菜单中移除Target命令，请将以下属性添加到组件的cq：editConfig节点：

* 名称：cq：disableTargeting
* 类型：布尔值
* 值： True

例如，要禁用“Geometrixx演示站点”页面标题组件的定位，请将属性添加到/apps/geometrixx/components/title/cq：editConfig节点。

![chlimage_1-22](assets/chlimage_1-22.png)

## 将订单确认信息发送到Adobe Target {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>如果您未使用DTM，则需要将订单确认发送到Adobe Target。

为了跟踪网站的性能，请将订单确认页面中的购买信息发送到Adobe Target。 (请参阅 [创建orderConfirmPage Mbox](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager/?lang=en) 和 [订单确认Mbox — 添加自定义参数。](https://experienceleaguecommunities.adobe.com/t5/adobe-target-questions/order-confirmation-mbox-add-custom-parameters/m-p/275779)) Adobe Target将mbox数据识别为订单确认数据，如果MBox名称为 `orderConfirmPage` 和使用以下特定参数名称：

* productPurchasedId：用于标识所购买产品的ID列表。
* orderId：订单的ID。
* orderTotal：采购的总金额。

渲染HTML页面上创建mbox的代码类似于以下示例：

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

每个订单的每个参数的值均不同。 因此，您需要一个根据购买的属性生成代码的组件。 CQ [电子商务集成框架](/help/commerce/cif-classic/administering/ecommerce.md) 使您能够与产品目录集成并实施购物车和结账页面。

当Geometrixx Outdoors购买产品时，访客示例会显示以下确认页面：

![chlimage_1-23](assets/chlimage_1-23.png)

以下组件的JSP脚本代码访问购物车的属性，然后打印用于创建mbox的代码。

```java
<%--

  confirmationmbox component.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
          import="com.adobe.cq.commerce.api.CommerceService,
                  com.adobe.cq.commerce.api.CommerceSession,
                  com.adobe.cq.commerce.common.PriceFilter,
                  com.adobe.cq.commerce.api.Product,
                  java.util.List, java.util.Iterator"%><%

/* obtain the CommerceSession object */
CommerceService commerceservice = resource.adaptTo(CommerceService.class);
CommerceSession session = commerceservice.login(slingRequest, slingResponse);

/* obtain the cart items */
List<CommerceSession.CartEntry> entries = session.getCartEntries();
Iterator<CommerceSession.CartEntry> cartiterator = entries.iterator();

/* iterate the items and get the product IDs */
String productIDs = new String();
while(cartiterator.hasNext()){
 CommerceSession.CartEntry entry = cartiterator.next();
 productIDs = productIDs + entry.getProduct().getSKU();
    if (cartiterator.hasNext()) productIDs = productIDs + ", ";
}

/* get the cart price and orderID */
String total = session.getCartPrice(new PriceFilter("CART", "PRE_TAX"));
String orderID = session.getOrderId();

%><div class="mboxDefault"></div>
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=<%= productIDs %>',
     'orderId=<%= orderID %>',
     'orderTotal=<%= total %>');
</script>
```

当上一示例中的结账页面中包含该组件时，页面源中包含以下用于创建mbox的脚本：

```
<div class="mboxDefault"></div>
<script type="text/javascript">

     mboxCreate('orderConfirmPage',
     'productPurchasedId=47638-S, 46587',
     'orderId=d03cb015-c30f-4bae-ab12-1d62b4d105ca',
     'orderTotal=US$677.00');

</script>
```

## 了解Target组件 {#understanding-the-target-component}

利用Target组件，作者可以从CQ内容组件创建动态mbox。 (请参阅 [内容定位](/help/sites-authoring/content-targeting-touch.md).) Target组件位于/libs/cq/personalization/components/target。

target.jsp脚本可访问页面属性，以确定用于组件的定位引擎，然后执行相应的脚本：

* Adobe Target： /libs/cq/personalization/components/target/engine_tnt.jsp
* [Adobe Target与AT.JS](/help/sites-administering/target.md)： /libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md)： /libs/cq/personalization/components/target/engine_cq_campaign.jsp
* 客户端规则/ContextHub： /libs/cq/personalization/components/target/engine_cq.jsp

### Mbox的创建 {#the-creation-of-mboxes}

>[!NOTE]
>
>默认情况下，mbox处于隐藏状态 — mboxDefault类决定此行为。 隐藏mbox可确保访客在切换默认内容之前不会看到该内容；但是，隐藏mbox会影响感知到的性能。

当Adobe Target驱动内容定位时，engine_tnt.jsp脚本会创建包含目标体验内容的mbox：

* 添加 `div` 具有以下类的元素 `mboxDefault`，如Adobe Target API所要求。

* 在中添加mbox内容（目标体验的内容） `div` 元素。

遵循 `mboxDefault` div元素中插入了创建mbox的javascript：

* mbox名称、ID和位置基于组件的存储库路径。
* 该脚本将获取Client Context参数名称和值。
* 将会调用mbox.js和其他客户端库定义的函数以创建mbox。

#### 用于内容定位的客户端库 {#client-libraries-for-content-targeting}

以下是可用的clientlib类别：

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
