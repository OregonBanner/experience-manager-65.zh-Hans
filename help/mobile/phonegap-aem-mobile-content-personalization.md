---
title: AEM Mobile内容个性化
seo-title: AEM Mobile content personalization
description: 请阅读本页，了解AEM Mobile内容个性化功能，该功能允许AEM作者利用Adobe Target对移动应用程序内容进行个性化。
seo-description: Follow this page to learn about AEM Mobile content personalization feature that allows AEM authors to personalize mobile app content by leveraging Adobe Target.
uuid: 9078edd1-8399-485f-8a63-a07e766f7ef9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c9c818dc-c5c4-4a96-94fe-9dc9fe75705b
exl-id: 70d7ee0d-2f6d-4f97-a6e2-b02d84a0ca42
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '2673'
ht-degree: 0%

---

# AEM Mobile内容个性化{#aem-mobile-content-personalization}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

>[!NOTE]
>
>本文档是 [AEM Mobile快速入门](/help/mobile/getting-started-aem-mobile.md) 指南，建议的AEM Mobile参考起点。

AEM Mobile内容个性化功能允许 [AEM作者](#author) 利用个性化移动应用程序内容 [Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html). 这允许向移动应用程序用户投放定向优惠。 Adobe Experience Manager Mobile能够创建、定位和交付内容，这些内容将为用户提供特定于用户个人口味的内容。

与AEM中的常见情况一样，为了使作者开始创建此内容，管理员和开发人员需要先准备环境。

[AEM管理员](#administrator) 需要在AEM Mobile和Adobe TargetCloud Service之间建立连接。

与此同时，AEM Mobile [开发人员](#developer) 需要修改其现有脚本，以便进行目标内容创作。

## 适用于管理员 {#for-administrators}

在内容作者可以开始为移动应用程序生成目标内容之前，需要完成许多步骤：为用户和组获取正确的权限集、创建云服务、为活动配置应用程序，以及最终生成内容。

本文将引导您完成用于配置 [AEM Mobile混合引用应用程序](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 进行定位。

我们接下来将假定已成功部署并可通过AEM Mobile功能板访问AEM Mobile混合引用应用程序。

在作者可以在应用程序中生成目标内容之前，您的AEM实例需要是 [已使用Adobe TargetCloud Service进行配置。](/help/mobile/aem-mobile-configuring-cloud-service.md)

### 权限 {#permissions}

需要访问个性化控制台的用户需要成为 `target-activity-authors` 组。

建议在用户和组设置过程中，将target-activity-group添加到apps-admins组中。 通过添加target-activity-authors组，用户将能够查看个性化导航菜单条目。

>[!NOTE]
>
>如果忘记将您希望有权访问个性化管理控制台的用户或组添加到target-activity-authors组，则将阻止用户查看个性化控制台。

### Cloud Service {#cloud-services}

要获得适用于移动设备应用程序的目标内容，需要配置两项服务：Adobe Target服务和AdobeMobile Services服务。 Adobe Target服务提供用于处理客户端请求和返回个性化内容的引擎。 AdobeMobile Services服务通过AMS Cordova插件使用的ADBMobileConfig.json文件提供Adobe服务和移动应用程序之间的连接。 在AEM Mobile功能板中，您可以通过添加这两个服务来配置应用程序。

在AEM Mobile功能板中，找到管理Cloud Services，然后单击+按钮。

![chlimage_1-38](assets/chlimage_1-38.png)

从“添加Cloud Service”向导中，选择“Adobe Target”云服务卡，然后单击下一步。

![chlimage_1-39](assets/chlimage_1-39.png)

从选择配置下拉列表中，您可以创建新配置或从现有配置中进行选择。 要创建新配置，请从下拉菜单中选择“创建配置”。 输入Target配置的标题。 输入与Target帐户关联的客户端代码、电子邮件和密码。 如果您不知道这些字段的值，请联系Adobe Target支持。 单击“验证”按钮验证凭据。 验证后，单击提交按钮以创建云服务。

>[!NOTE]
>
>创建的云服务将通过向导自动与移动应用程序关联。 在apps组节点的jcr：content节点上设置cq：cloudserviceconfigs属性值。 对于混合应用程序示例，将在/content/mobileapps/hybrid-reference-app/jcr：content中设置此参数，其值指向自动生成的框架节点，该节点位于/etc/cloudservices/testandtarget/adobe-target—aem-apps/framework。 框架节点默认设置了两个属性：性别和年龄。 此框架仅供AEM预览使用，对设备没有任何影响。

完成该向导后，“管理Cloud Service”图块将包含Target云服务，但它包含有关缺少Adobe移动服务帐户的警告。

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

还必须将AdobeMobile Services (AMS)帐户链接到应用程序，AMS服务会提供所需的ADBMobileConfig.json文件，其中包含Target客户端代码信息。 在创建与AMS帐户的关联之前，需要由具有AMS权限的用户修改AMS帐户。

### 客户代码 {#client-code}

要登录AMS服务，请访问 [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)，选择移动设备应用程序，然后单击设置。 找到SDK目标选项字段，将客户端代码放入该字段，然后单击保存。

![chlimage_1-41](assets/chlimage_1-41.png)

现在，客户端代码已与移动应用程序关联，当通过Adobe移动仪表板配置AMS云服务时，服务设置的设置将通过ADBMobileConfig.json文件交付。

### Adobe移动服务Cloud Service {#adobe-mobile-service-cloud-service}

现在AMS已配置，是时候在Adobe移动设备仪表板中关联移动设备应用程序了。 在AEM Mobile功能板中，找到管理Cloud Services，然后单击+按钮。

![chlimage_1-42](assets/chlimage_1-42.png)

选择AdobeMobile Services信息卡，然后单击下一步。

![chlimage_1-43](assets/chlimage_1-43.png)

从创建或选择向导步骤中选择Mobile Service下拉列表，然后选择创建配置条目。 提供标题、公司、用户名、密码并选择适当的数据中心。 如果您不知道这些值，请与AdobeMobile Service管理员联系以获取它们。 填写完所有字段后，单击验证按钮。 验证过程将转至AMS并验证帐户的凭据，在验证成功后，将填充移动设备应用程序列表，您可以从下拉列表中选择关联的移动设备应用程序。 单击“提交”按钮以完成向导。 该过程可能需要一些时间来获取配置数据以及与应用程序关联的任何分析。 流程完成后，单击模式窗口中的Done按钮以返回到Adobe移动设备仪表板。

返回移动设备仪表板后，“管理Cloud Services”图块将包含AMS云服务。 您还将注意到，“分析量度”图块中将填充有生命周期报表。

![chlimage_1-44](assets/chlimage_1-44.png)

## 对于作者 {#for-authors}

**先决条件：** 如上所述，管理员需要先配置与Adobe Target服务的连接，然后作者才能生成新的目标内容。

在管理员配置两个云服务且开发人员配置mobileappoffers处理程序后，内容作者现在可以开始生成目标体验。

在AEM Mobile应用程序中创作目标内容时，会遵循与创作AEM Sites类似的过程：

有关以下内容的完整概述，请参阅此处 [在AEM中创作目标内容](/help/sites-authoring/personalization.md)

## 面向开发人员 {#for-developers}

构建移动应用程序的AEM开发人员在开发组件时应继续遵循整个AEM中常用的模式。 在本例中，我们将引导您完成必要步骤，以使内容作者能够创建目标内容：

### Adobe Target ContentSync处理程序 {#adobe-target-contentsync-handlers}

要向用户的设备内容交付内容，将通过呈现由AEM内容作者创建的选件来生成该内容。 要处理Target选件的渲染，可使用新的内容同步处理程序来处理选件。 使用混合引用应用程序作为示例，en（英语）内容包中包含的ContentSyncConfig具有 [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 处理程序。 下一步对于向设备呈现选件至关重要。 mobileappoffers处理程序的path属性标识要用于应用程序的个性化活动的路径。

例如，如果某个活动位于 */content/campaigns/hybridref* 复制此路径并将其作为值粘贴到 *路径* mobileappoffers处理程序的属性。

>[!NOTE]
>
>对于混合引用应用程序，有两个mobileappoffer处理程序，一个用于开发，一个用于生产。

在mobileappoffers处理程序的path属性中设置活动路径后，请保存该处理程序。 处理程序现在可以开始呈现我们移动设备的选件。

### 渲染模式 {#render-mode}

Mobileappoffers处理程序在发布和开发设置中的配置方式不同。 对于发布设置，有一个名为的属性 *渲染模式* 具有值 *发布* 在cq：ContentSyncConfig节点上设置。 mobileappoffers处理程序引用renderMode，如果设置为publish，则将修改所创建的mbox id。 默认情况下，由AEM创建的mbox会将 — author值附加到mbox id。 这会标识该活动尚未发布，应使用未发布的促销活动来获取优惠解决方案。

通过Adobe移动设备仪表板暂存内容时，暂存内容被视为生产就绪内容，并通过非开发内容同步配置进行渲染。 按此方式呈现将导致从所有mbox id中删除 — author，并预期Target服务器上会提供一个已发布的活动。 在测试暂存内容之前，请确保已发布活动。

### 个性化应用程序开发 {#personalization-app-development}

#### 组件 {#components}

任何内容的基础通常都是页面组件，该组件可以扩展基本AEM页面组件wcm/foundation/components/page或foundation/components/page之一，具体取决于您使用的是HTL还是JSP。 这些步骤的持续时间将侧重于使用wcm/foundation/components/page组件。 页面组件的基本结构被划分为多个脚本，每个脚本提供特定目的，以便开发人员在需要时组织和覆盖其代码。 对个性化感兴趣的两个脚本是head.html和body.html。 这两个脚本提供了一个区域，可在其中插入代码以支持Context Hub、Cloud Services和移动设备创作。

下面概述了用于启用内容定位的两个主要脚本。

#### head.html {#head-html}

为了让作者能够定位其内容，需要将“目标”菜单添加到页面，以便作者可以将上下文从编辑模式更改为定位模式。 要启用此功能，开发人员应修改head.html脚本，以在head.html顶部附近或在 &lt;title>&lt;/title> 元素。

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>请注意，只有在尚未禁用WCM模式，从而禁用了WCM模式时（有关详细信息，请参阅ContentSync处理程序一节），脚本才会包含在最终应用程序代码中。

为了让作者能够预览目标内容，编辑器需要能够找到Adobe Target云服务的配置。 下面的代码块添加了两个重要脚本。 首次添加功能，让页面能够找到关联的Target云服务并调用Adobe Target。 其次是添加了cq.apps.targeting类别。

此 **cq.apps.targeting** 类别会覆盖默认的cq/personalization/component/target组件，并使用可呈现专门用于移动应用程序使用的选件的mobileapps/components/target组件。 有关此要求的更多详细信息，请参阅目标组件一节。

代码应添加到head.html中，并放置在的末尾之前 &lt;/head> 元素。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>请注意，不会禁用WCM模式中包装的代码块，因此该代码块仅在内容作者正在创建内容时起作用。 云服务脚本将不会添加到生成的移动运行时代码。

#### body.html {#body-html}

要启用内容作者测试不同角色的功能，body.html脚本需要包含以下代码块作为body元素的第一个子级。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

所需代码的最后一位位于body.html的最底部。 此代码位将查找关联的云服务并注入相应的定位引擎代码。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### 引用应用程序 {#reference-application}

head.html和body.html的示例可在以下位置找到： [AEM Mobile混合引用应用程序](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 显示开发人员在两个脚本中放置脚本块的位置。

### 内容同步处理程序 {#content-sync-handlers}

当内容作者完成为移动应用程序创建内容时，下一步是下载源并构建应用程序，或暂存要发布的内容。 要实现此目的，开发人员需要执行许多步骤。 为帮助渲染内容，AEM Mobile使用内容同步处理程序来渲染和打包内容。 为个性化用例引入了一个新的内容同步处理程序，用于呈现目标内容。 “mobileappoffers”处理程序知道如何呈现由内容作者创建的关联目标选件。 mobileappoffers处理程序扩展了抽象页面更新处理程序，因此，许多属性是相似的。 mobileappoffers处理程序的详细信息具有以下属性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>重写</td>
   <td>+相对父路径<p> - "/"</p> </td>
   <td>rewrite属性标识应如何重写内容中的路径。</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>includePageTypes属性是可选的，默认为具有cq/personalization/components/teaserpage和cq/personalization/components/offerproxy资源类型的页面。 这两种资源类型是定位内容时使用的默认资源类型。 如果需要支持其他资源类型，则应将其添加到includePageTypes列表中。</td>
  </tr>
  <tr>
   <td>locationroot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>应用程序的位置。</td>
  </tr>
  <tr>
   <td>类型</td>
   <td>mobileappoffers</td>
   <td>作为mobileappoffers的处理程序的名称。</td>
  </tr>
  <tr>
   <td>选择器</td>
   <td>tandt</td>
   <td>tandt选择器用于呈现目标内容。 </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>用于保留渲染内容的根目录。</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>如果为true，则会渲染选件中包含的任何图像。 如果跳过假图像。</td>
  </tr>
  <tr>
   <td>includeVideo</td>
   <td>true | false</td>
   <td>如果为true，则会呈现选件中包含的任何视频。 如果视频错误，则跳过该视频。</td>
  </tr>
  <tr>
   <td>路径</td>
   <td>/content/campaigns/&lt;brand&gt;</td>
   <td>指向选件参与的活动品牌。 当前，所有选件都必须来自同一营销活动。</td>
  </tr>
  <tr>
   <td>深</td>
   <td>true | false</td>
   <td>如果为true，递归渲染所有子页面；如果为false，则不递归。 </td>
  </tr>
  <tr>
   <td>扩展</td>
   <td>html</td>
   <td>设置正在渲染的资源的扩展。 设置为html，以便页面具有.html扩展名。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此 [AEM Mobile混合引用应用程序](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 具有默认的mobileappoffer处理程序配置。 示例中的path属性为空，因为它取决于营销活动位置。 在Campaign作者创建了Campaign后，应用程序管理员应通过指定指向Campaign的path属性来将Campaign与处理程序关联。

### 目标组件 {#target-component}

为了帮助呈现专门用于移动设备应用程序的内容，AEM Mobile使用mobileapps/components/target组件。 移动定位组件扩展cq/personalization/components/target组件并覆盖engine_tnt.jsp脚本。 通过覆盖engine_tnt.jsp，AEM Mobile可以控制为移动设备应用程序用例生成的HTML。 对于内容作者定位的每个组件，都会由engine_tnt.jsp创建一个关联的mbox。

对于每个mbox，属性为 **cq-targeting** 添加了功能，允许应用程序开发人员编写自定义代码，以便随意使用和使用。 此 [AEM Mobile混合引用应用程序](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 有一个使用cq-targeting属性的Angular指令示例。 内容替换何时以及如何替换的概念在很大程度上取决于移动应用程序开发人员。 有一个通过AEM /etc/clientlibs/mobileapps/js/mobileapps.js交付的Mobile SDK，它提供了一个API来调用Adobe定位服务。 由应用程序开发人员根据他们的应用程序的设计来指定何时应该进行该调用。

## 后续内容? {#what-s-next}

1. [开始我的AEM Mobile应用程序体验](/help/mobile/starting-aem-phonegap-app.md)
1. [管理我的应用程序内容](/help/mobile/phonegap-manage-app-content.md)
1. [构建我的应用程序](/help/mobile/building-app-mobile-phonegap.md)
1. [使用Adobe移动分析跟踪我的应用程序的性能](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [使用Adobe Target提供个性化的应用程序体验](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [向我的用户发送重要消息](/help/mobile/phonegap-push-notifications.md)
