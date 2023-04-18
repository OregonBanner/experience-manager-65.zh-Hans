---
title: 针对目标内容进行开发
seo-title: Developing for Targeted Content
description: 有关开发组件以与内容定位一起使用的主题
seo-description: Topics about developing components for use with content targeting
uuid: 2449347e-7e1c-427b-a5b0-561055186934
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bff078cd-c390-4870-ad1d-192807c67ca4
docset: aem65
exl-id: 92b62532-4f79-410d-903e-d2bca6d0fd1c
source-git-commit: fb9363a39ffc9d3929a31a3a19a124b806607ef4
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 3%

---

# 针对目标内容进行开发{#developing-for-targeted-content}

本节介绍有关开发与内容定位一起使用的组件的主题。

* 有关连接Adobe Target的信息，请参阅 [与Adobe Target集成](/help/sites-administering/target.md).
* 有关创作目标内容的信息，请参阅 [使用定位模式创作目标内容](/help/sites-authoring/content-targeting-touch.md).

>[!NOTE]
>
>在 AEM 创作实例中定位组件时，该组件会对 Adobe Target 进行一系列的服务器端调用，以便注册活动、设置选件和检索 Adobe Target 区段（如果已配置）。没有从 AEM Publish 到 Adobe Target 的服务器端调用。

## 在您的页面上启用使用Adobe Target进行定位 {#enabling-targeting-with-adobe-target-on-your-pages}

要在页面中使用与Adobe Target交互的目标组件，请在 &lt;head> 元素。

### 头部分 {#the-head-section}

将以下两个代码块添加到 &lt;head> 部分：

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

此代码可添加所需的Analytics Javascript对象并加载与网站关联的云服务库。 对于Target服务，库将通过 `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

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
>仅版本 `at.js` 支持随产品一起提供。 的版本 `at.js` 可通过查看 `at.js` 文件位置：
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**.

**对于自定义at.js**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

客户端上的Target功能由 `CQ_Analytics.TestTarget` 对象。 因此，页面将包含一些init代码，如以下示例中所示：

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

#### 正文部分（开始） {#the-body-section-start}

在 &lt;body> 标记以将客户端上下文功能添加到页面：

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### 正文部分（结尾） {#the-body-section-end}

在紧靠 &lt;/body> 结束标记：

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

### 使用自定义Target库文件 {#using-a-custom-target-library-file}

>[!NOTE]
>
>如果您没有使用DTM或其他Target营销系统，则可以使用自定义Target库文件。

>[!NOTE]
>
>默认情况下，mbox是隐藏的 — mboxDefault类确定此行为。 隐藏mbox可确保访客在交换默认内容之前不会看到默认内容；但是，隐藏mbox会影响感知到的性能。

用于创建mbox的默认mbox.js文件位于/etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js。 要使用客户mbox.js文件，请将该文件添加到Target云配置中。 要添加文件，mbox.js文件必须在文件系统上可用。

例如，如果要使用 [Marketing CloudID服务](https://experienceleague.adobe.com/docs/id-service/using/home.html) 您需要下载mbox.js，以便它包含 `imsOrgID` 变量，基于租户。 与Marketing CloudID服务集成时需要此变量。 有关信息，请参阅 [Adobe Analytics作为Adobe Target报表源](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) 和 [实施之前](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html).

>[!NOTE]
>
>如果在Target配置中定义了自定义mbox，则每个人都必须具有 **/etc/cloudservices** 在发布服务器上。 如果没有此访问权限，则在发布网站上加载mbox.js文件会导致404错误。

1. 转到CQ **工具** 页面并选择 **Cloud Services**. ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. 在树中，选择Adobe Target，然后在配置列表中，双击您的Target配置。
1. 在配置页面上，单击编辑。
1. 对于自定义mbox.js属性，单击浏览并选择文件。
1. 要应用更改，请输入Adobe Target帐户的密码，单击重新连接到Target ，然后在连接成功时单击确定。 然后，在“编辑组件”对话框中单击“确定”。

您的Target配置包含一个自定义mbox.js文件， [head部分中的必需代码](/help/sites-developing/target.md#p-the-head-section-p) 的页面会将文件添加到客户端库框架，而不是对testandtarget.js库的引用。

## 禁用组件的Target命令 {#disabling-the-target-command-for-components}

大多数组件都可以使用上下文菜单中的Target命令转换为目标组件。

![chlimage_1-21](assets/chlimage_1-21.png)

要从上下文菜单中删除Target命令，请将以下属性添加到组件的cq:editConfig节点：

* 名称：cq:disableTargeting
* 类型：布尔值
* 值：True

例如，要禁用Geometrixx演示网站页面标题组件的定位，请将该属性添加到/apps/geometrixx/components/title/cq:editConfig节点。

![chlimage_1-22](assets/chlimage_1-22.png)

## 向Adobe Target发送订单确认信息 {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>如果您没有使用DTM，则会向Adobe Target发送订单确认。

要跟踪网站的性能，请将购买信息从订单确认页面发送到Adobe Target。 (请参阅 [创建orderConfirmPage Mbox](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager/?lang=en) 和 [订单确认Mbox — 添加自定义参数。](https://experienceleaguecommunities.adobe.com/t5/adobe-target-questions/order-confirmation-mbox-add-custom-parameters/m-p/275779))当mbox名称为 `orderConfirmPage` 和会使用以下特定参数名称：

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

每个顺序的每个参数的值都不同。 因此，您需要一个组件，该组件会根据购买的属性生成代码。 CQ [电子商务集成框架](/help/commerce/cif-classic/administering/ecommerce.md) 允许您与产品目录集成并实施购物车和结账页面。

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

## 了解目标组件 {#understanding-the-target-component}

Target组件允许作者从CQ内容组件创建动态mbox。 (请参阅 [内容定位](/help/sites-authoring/content-targeting-touch.md).) Target组件位于/libs/cq/personalization/components/target。

target.jsp脚本访问页面属性以确定要用于组件的定位引擎，然后执行相应的脚本：

* Adobe Target:/libs/cq/personalization/components/target/engine_tnt.jsp
* [Adobe Target与AT.JS](/help/sites-administering/target.md):/libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md):/libs/cq/personalization/components/target/engine_cq_campaign.jsp
* 客户端规则/ContextHub:/libs/cq/personalization/components/target/engine_cq.jsp

### Mbox的创建 {#the-creation-of-mboxes}

>[!NOTE]
>
>默认情况下，mbox是隐藏的 — mboxDefault类确定此行为。 隐藏mbox可确保访客在交换默认内容之前不会看到默认内容；但是，隐藏mbox会影响感知到的性能。

当Adobe Target执行内容定位时，engine_tnt.jsp脚本会创建包含目标体验内容的mbox:

* 添加 `div` 具有类的元素 `mboxDefault`,Adobe Target API要求。

* 在 `div` 元素。

关注 `mboxDefault` div元素中，将插入用于创建mbox的javascript:

* mbox名称、ID和位置均基于组件的存储库路径。
* 脚本获取Client Context参数名称和值。
* 将对mbox.js和其他客户端库定义的用于创建mbox的函数进行调用。

#### 用于内容定位的客户端库 {#client-libraries-for-content-targeting}

以下是可用的clientlib类别：

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
