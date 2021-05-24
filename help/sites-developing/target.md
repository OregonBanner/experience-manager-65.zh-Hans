---
title: 针对目标内容进行开发
seo-title: 针对目标内容进行开发
description: 有关开发组件以与内容定位一起使用的主题
seo-description: 有关开发组件以与内容定位一起使用的主题
uuid: 2449347e-7e1c-427b-a5b0-561055186934
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bff078cd-c390-4870-ad1d-192807c67ca4
docset: aem65
exl-id: 92b62532-4f79-410d-903e-d2bca6d0fd1c
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '1287'
ht-degree: 0%

---

# 针对目标内容进行开发{#developing-for-targeted-content}

本节介绍有关开发与内容定位一起使用的组件的主题。

* 有关连接Adobe Target的信息，请参阅[与Adobe Target集成](/help/sites-administering/target.md)。
* 有关创作目标内容的信息，请参阅[使用定位模式创作目标内容](/help/sites-authoring/content-targeting-touch.md)。

>[!NOTE]
>
>在AEM作者中定位某个组件时，该组件会向Adobe Target发起一系列服务器端调用，以注册该促销活动、设置选件和检索Adobe Target区段（如果已配置）。 不会从AEM发布到Adobe Target中进行服务器端调用。

## 在您的页面{#enabling-targeting-with-adobe-target-on-your-pages}上启用Adobe Target定位

要在页面中使用与Adobe Target交互的目标组件，请在&lt;head>元素中包含特定的客户端代码。

### 标题部分{#the-head-section}

将以下两个代码块添加到页面的&lt;head>部分：

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

此代码可添加所需的Analytics Javascript对象并加载与网站关联的云服务库。 对于Target服务，将通过`/libs/cq/analytics/components/testandtarget/headlibs.jsp`加载库

加载的库集取决于Target配置中使用的Target客户端库（mbox.js或at.js）类型：

**对于默认的mbox.js**

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
>仅支持随产品一起提供的`at.js`版本。 通过查看位于以下位置的`at.js`文件，可以获取产品附带的`at.js`版本：
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**。

**对于自定义at.js**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

客户端上的Target功能由`CQ_Analytics.TestTarget`对象管理。 因此，页面将包含一些init代码，如以下示例中所示：

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

JSP会将所需的Analytics Javascript对象和引用添加到客户端Javascript库。 testandtarget.js文件包含mbox.js函数。 脚本生成的HTML与以下示例类似：

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

#### 正文部分（开始）{#the-body-section-start}

在&lt;body>标记之后立即添加以下代码，以将Client Context功能添加到页面：

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### 正文节（结尾）{#the-body-section-end}

在紧靠&lt;/body>结束标记之前添加以下代码：

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

此组件的JSP脚本生成对Target Javascript API的调用并实现其他必需的配置。 脚本生成的HTML与以下示例类似：

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

### 使用自定义Target库文件{#using-a-custom-target-library-file}

>[!NOTE]
>
>如果您没有使用DTM或其他Target营销系统，则可以使用自定义Target库文件。

>[!NOTE]
>
>默认情况下，mbox是隐藏的 — mboxDefault类确定此行为。 隐藏mbox可确保访客在交换默认内容之前不会看到默认内容；但是，隐藏mbox会影响感知到的性能。

用于创建mbox的默认mbox.js文件位于/etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js。 要使用客户mbox.js文件，请将该文件添加到Target云配置中。 要添加文件，mbox.js文件必须在文件系统上可用。

例如，如果您要使用[Marketing CloudID服务](https://docs.adobe.com/content/help/en/id-service/using/home.html)，则需要下载mbox.js，以便它包含`imsOrgID`变量的正确值，该值基于您的租户。 与Marketing CloudID服务集成时需要此变量。 有关信息，请参阅[Adobe Analytics作为Adobe Target](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html)和[实施](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/before-implement.html)之前的报表源。

>[!NOTE]
>
>如果在Target配置中定义了自定义mbox，则每个人都必须拥有对发布服务器上&#x200B;**/etc/cloudservices**&#x200B;的读取访问权限。 如果没有此访问权限，则在发布网站上加载mbox.js文件会导致404错误。

1. 转到CQ **工具**&#x200B;页面并选择&#x200B;**Cloud Services**。 ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. 在树中，选择Adobe Target，然后在配置列表中，双击您的Target配置。
1. 在配置页面上，单击编辑。
1. 对于自定义mbox.js属性，单击浏览并选择文件。
1. 要应用更改，请输入Adobe Target帐户的密码，单击重新连接到Target ，然后在连接成功时单击确定。 然后，在“编辑组件”对话框中单击“确定”。

您的Target配置包含一个自定义mbox.js文件， [页面标题部分](/help/sites-developing/target.md#p-the-head-section-p)中的所需代码会将该文件添加到客户端库框架中，而不是对testandtarget.js库的引用。

## 禁用组件{#disabling-the-target-command-for-components}的Target命令

大多数组件都可以使用上下文菜单中的Target命令转换为目标组件。

![chlimage_1-21](assets/chlimage_1-21.png)

要从上下文菜单中删除Target命令，请将以下属性添加到组件的cq:editConfig节点：

* 名称：cq:disableTargeting
* 类型：布尔型
* 值：True

例如，要禁用Geometrixx演示网站页面标题组件的定位，请将该属性添加到/apps/geometrixx/components/title/cq:editConfig节点。

![chlimage_1-22](assets/chlimage_1-22.png)

## 向Adobe Target发送订单确认信息{#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>如果您没有使用DTM，则会向Adobe Target发送订单确认。

要跟踪网站的性能，请将购买信息从订单确认页面发送到Adobe Target。 (请参阅Adobe Target文档中的[创建orderConfirmPage Mbox](https://docs.adobe.com/content/help/en/dtm/implementing/target/configure-target/mboxes/order-confirmation-mbox.html) 。) 当您的MBOX名称为`orderConfirmPage`时，Adobe Target会将mbox数据识别为订单确认数据，并使用以下特定参数名称：

* productPurchasedId:标识已购产品的ID列表。
* orderId:订单的ID。
* orderTotal:购买的总金额。

呈现的HTML页面上用于创建mbox的代码与以下示例类似：

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

每个顺序的每个参数的值都不同。 因此，您需要一个组件，该组件会根据购买的属性生成代码。 CQ [电子商务集成框架](/help/commerce/cif-classic/administering/ecommerce.md)允许您与产品目录集成并实施购物车和结帐页面。

Geometrixx Outdoors示例在访客购买产品时显示以下确认页面：

![chlimage_1-23](assets/chlimage_1-23.png)

组件的JSP脚本的以下代码访问购物车的属性，然后打印用于创建mbox的代码。

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

在上一个示例中，当组件包含在结帐页面中时，页面源将包含以下创建mbox的脚本：

```
<div class="mboxDefault"></div>
<script type="text/javascript">

     mboxCreate('orderConfirmPage',
     'productPurchasedId=47638-S, 46587',
     'orderId=d03cb015-c30f-4bae-ab12-1d62b4d105ca',
     'orderTotal=US$677.00');

</script>
```

## 了解目标组件{#understanding-the-target-component}

Target组件允许作者从CQ内容组件创建动态mbox。 （请参阅[内容定位](/help/sites-authoring/content-targeting-touch.md)。） Target组件位于/libs/cq/personalization/components/target。

target.jsp脚本访问页面属性以确定要用于组件的定位引擎，然后执行相应的脚本：

* Adobe Target:/libs/cq/personalization/components/target/engine_tnt.jsp
* [Adobe Target与AT.JS](/help/sites-administering/target.md):/libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md):/libs/cq/personalization/components/target/engine_cq_campaign.jsp
* 客户端规则/ContextHub:/libs/cq/personalization/components/target/engine_cq.jsp

### Mbox {#the-creation-of-mboxes}的创建

>[!NOTE]
>
>默认情况下，mbox是隐藏的 — mboxDefault类确定此行为。 隐藏mbox可确保访客在交换默认内容之前不会看到默认内容；但是，隐藏mbox会影响感知到的性能。

当Adobe Target执行内容定位时，engine_tnt.jsp脚本会创建包含目标体验内容的mbox:

* 根据Adobe Target API的要求，添加类为`mboxDefault`的`div`元素。

* 在`div`元素中添加mbox内容（目标体验的内容）。

在`mboxDefault` div元素之后，插入创建mbox的javascript:

* mbox名称、ID和位置均基于组件的存储库路径。
* 脚本获取Client Context参数名称和值。
* 将对mbox.js和其他客户端库定义的用于创建mbox的函数进行调用。

#### 用于内容定位的客户端库{#client-libraries-for-content-targeting}

以下是可用的clientlib类别：

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
