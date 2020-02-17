---
title: 针对目标内容进行开发
seo-title: 针对目标内容进行开发
description: 有关开发组件以用于内容定位的主题
seo-description: 有关开发组件以用于内容定位的主题
uuid: 2449347e-7e1c-427b-a5b0-561055186934
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bff078cd-c390-4870-ad1d-192807c67ca4
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 针对目标内容进行开发{#developing-for-targeted-content}

本节介绍有关开发组件以用于内容定位的主题。

* 有关连接Adobe Target的信息，请参 [阅与Adobe Target集成](/help/sites-administering/target.md)。
* 有关创作目标内容的信息，请参阅使 [用定位模式创作目标内容](/help/sites-authoring/content-targeting-touch.md)。

>[!NOTE]
>
>在AEM作者中定位组件时，该组件会向Adobe Target发出一系列服务器端调用，以注册营销活动、设置选件和检索Adobe Target区段（如果已配置）。 不会从AEM发布到Adobe Target进行服务器端调用。

## 在页面上通过Adobe Target启用定位 {#enabling-targeting-with-adobe-target-on-your-pages}

要在页面中使用与Adobe Target交互的目标组件，请在&lt;head>元素中包含特定的客户端代码。

### 头部部分 {#the-head-section}

将以下两个代码块添加到页面的&lt;head>部分：

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

此代码添加所需的分析javascript对象并加载与网站关联的云服务库。 对于Target服务，将通过 `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

加载的库集取决于Target配置上使用的目标客户端库（mbox.js或at.js）的类型：

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
>仅支持随产 `at.js` 品提供的版本。 通过查 `at.js` 看位于以下位置的文件，可以获取随产品一 `at.js` 起提供的版本：
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**。

**对于自定义at.js**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

客户端上的Target功能由对象管 `CQ_Analytics.TestTarget` 理。 因此，该页面将包含一些init代码，如以下示例中所示：

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

JSP会添加所需的分析javascript对象和对客户端javascript库的引用。 testandtarget.js文件包含mbox.js函数。 脚本生成的HTML与以下示例类似：

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

在&lt;body>标记后面添加以下代码，将Client Context功能添加到页面：

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### 主体部分（结尾） {#the-body-section-end}

在&lt;/body>结束标记前面添加以下代码：

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

此组件的JSP脚本生成对Target javascript API的调用并实现其他必需配置。 脚本生成的HTML与以下示例类似：

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

### 使用自定义目标库文件 {#using-a-custom-target-library-file}

>[!NOTE]
>
>如果您没有使用DTM或其他目标营销系统，则可以使用自定义目标库文件。

>[!NOTE]
>
>默认情况下，mbox是隐藏的- mboxDefault类决定此行为。 隐藏mbox可确保访客在交换默认内容之前不会看到该内容；但是，隐藏mbox会影响感知到的性能。

用于创建mbox的默认mbox.js文件位于/etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js。 要使用客户mbox.js文件，请将该文件添加到Target云配置。 要添加文件，mbox.js文件必须在文件系统上可用。

例如，如果要使用 [Marketing Cloud ID服务](https://marketing.adobe.com/resources/help/en_US/mcvid/) ，您需要下载mbox.js，以便它包含基于租户的变量的正确值 `imsOrgID` 。 此变量是与Marketing Cloud ID服务集成所必需的。 有关信息，请参 [阅将Adobe Analytics作为Adobe Target的报告源](https://marketing.adobe.com/resources/help/en_US/target/a4t/a4t.html) ，并在 [实施之前查看](https://marketing.adobe.com/resources/help/en_US/target/a4t/c_before_implement.html)。

>[!NOTE]
>
>如果在Target配置中定义了自定义mbox，则每个人都必须对发布服务器上的 **/etc/cloudservices具有读访问权限** 。 如果没有此访问权限，在发布网站上加载mbox.js文件将导致404错误。

1. 转到“CQ工 **具** ”页面并选 **择云服务**。 ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. 在树中，选择Adobe Target，然后在配置列表中双击您的Target配置。
1. 在配置页面上，单击编辑。
1. 对于“自定义mbox.js”属性，单击“浏览”并选择文件。
1. 要应用更改，请输入Adobe target帐户的口令，单击“重新连接到目标”，然后在连接成功时单击“确定”。 然后，在“编辑组件”对话框上单击“确定”。

您的Target配置包括自定义mbox.js文件，页面 [](/help/sites-developing/target.md#p-the-head-section-p) head部分中所需的代码会将该文件添加到客户端库框架，而不是对testandtarget.js库的引用。

## 禁用组件的目标命令 {#disabling-the-target-command-for-components}

大多数组件都可以使用上下文菜单上的“目标”命令转换为目标组件。

![chlimage_1-21](assets/chlimage_1-21.png)

要从上下文菜单中删除Target命令，请将以下属性添加到组件的cq:editConfig节点：

* 名称：cq:disableTargeting
* 类型：布尔型
* 值：True

例如，要禁用Geometrixx演示站点页面的标题组件的定位，请将属性添加到/apps/geometrixx/components/title/cq:editConfig节点。

![chlimage_1-22](assets/chlimage_1-22.png)

## 将订单确认信息发送到Adobe Target {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>如果您未使用DTM，请向Adobe Target发送订单确认。

要跟踪网站的性能，请将订单确认页面中的购买信息发送到Adobe Target。 (请参 [阅Adobe Target文档中的创建orderConfirmPage](https://marketing.adobe.com/resources/help/en_US/dtm/target/order-confirmation-mbox.html) Mbox。)当您的MBox名称为并使用以下特定参数名称时，Adobe target会将mbox数据识别 `orderConfirmPage` 为订单确认数据：

* productPurchasedId:标识所购买产品的ID列表。
* orderId:订单的ID。
* orderTotal:购买的总额。

呈现的HTML页面上用于创建mbox的代码与以下示例类似：

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

每个顺序的每个参数的值都不同。 因此，您需要一个组件，该组件根据购买的属性生成代码。 CQ [eCommerce Integration Framework](/help/sites-administering/ecommerce.md) （CQ电子商务集成框架）允许您与产品目录集成并实施购物车和结帐页面。

当访客购买产品时，Geometrixx Outdoors示例显示以下确认页面：

![chlimage_1-23](assets/chlimage_1-23.png)

组件的JSP脚本的以下代码访问购物车的属性，然后打印创建mbox的代码。

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

当组件包含在上一个示例的结帐页面中时，页面源包括创建mbox的以下脚本：

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

Target组件使作者能够从CQ内容组件创建动态mbox。 (请参阅 [内容定位](/help/sites-authoring/content-targeting-touch.md)。)Target组件位于/libs/cq/personalization/components/target。

target.jsp脚本访问页面属性以确定要用于组件的定位引擎，然后执行相应的脚本：

* Adobe Target:/libs/cq/personalization/components/target/engine_tnt.jsp
* [Adobe Target with AT.JS](/help/sites-administering/target.md):/libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md):/libs/cq/personalization/components/target/engine_cq_campaign.jsp
* 客户端规则/ContextHub:/libs/cq/personalization/components/target/engine_cq.jsp

### Mbox的创建 {#the-creation-of-mboxes}

>[!NOTE]
>
>默认情况下，mbox是隐藏的- mboxDefault类决定此行为。 隐藏mbox可确保访客在交换默认内容之前不会看到该内容；但是，隐藏mbox会影响感知到的性能。

当Adobe target驱动内容定位时，engine_tnt.jsp脚本将创建包含目标体验内容的mbox:

* 根据 `div` Adobe Target API的要求，添加 `mboxDefault`一个包含类的元素。

* 在元素中添加mbox内容（目标体验的内容）。 `div`

在 `mboxDefault` div元素之后，将插入创建mbox的javascript:

* mbox名称、ID和位置基于组件的存储库路径。
* 该脚本获取Client Context参数名称和值。
* 调用mbox.js和其他客户端库定义的用于创建mbox的函数。

#### 用于内容定位的客户端库 {#client-libraries-for-content-targeting}

以下是可用的clientlib类别：

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
