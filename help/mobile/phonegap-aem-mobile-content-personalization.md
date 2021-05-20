---
title: AEM Mobile内容个性化
seo-title: AEM Mobile内容个性化
description: 可查看本页以了解AEM Mobile内容个性化功能，该功能允许AEM作者利用Adobe Target对移动应用程序内容进行个性化。
seo-description: 可查看本页以了解AEM Mobile内容个性化功能，该功能允许AEM作者利用Adobe Target对移动应用程序内容进行个性化。
uuid: 9078edd1-8399-485f-8a63-a07e766f7ef9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c9c818dc-c5c4-4a96-94fe-9dc9fe75705b
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2701'
ht-degree: 0%

---


# AEM Mobile内容个性化{#aem-mobile-content-personalization}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

>[!NOTE]
>
>本文档是[AEM Mobile快速入门](/help/mobile/getting-started-aem-mobile.md)指南的一部分，该指南是AEM Mobile参考的推荐起点。

AEM Mobile内容个性化功能允许[AEM作者](#author)利用[Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html)个性化移动设备应用程序内容。 这允许向移动应用程序用户交付目标选件。 Adobe Experience Manager Mobile提供创建、定位和交付内容的功能，以便为用户提供特定于其个人品味的内容。

与AEM中的常见情况一样，为了让作者开始创建此内容，管理员和开发人员需要先准备环境。

[AEM ](#administrator) dministrator需要在AEM Mobile和Adobe TargetCloud Service之间建立连接。

同时，AEM Mobile [开发人员](#developer)需要修改其现有脚本，以便于进行目标内容创作。

## 对于管理员{#for-administrators}

在内容作者开始为移动设备应用程序生成目标内容之前，需要先完成许多步骤：我们将为用户和组获取正确的权限集，创建云服务，配置活动的应用程序，最后生成内容。

本文将指导您完成配置[AEM Mobile混合引用应用程序](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)以进行定位的过程。

今后的假设是AEM Mobile混合参考应用程序已成功部署并可通过AEM Mobile功能板访问。

在作者可以在应用程序中生成目标内容之前，您的AEM实例需要[配置Adobe TargetCloud Service。](/help/mobile/aem-mobile-configuring-cloud-service.md)

### 权限 {#permissions}

需要访问个性化控制台的用户必须属于`target-activity-authors`组。

建议在用户和组设置中，将target-activity-group添加到apps-admins组。 通过添加target-activity-authors组，用户将能够查看个性化导航菜单条目。

>[!NOTE]
>
>忘记将您希望有权访问个性化管理控制台的用户或组添加到target-activity-authors组将阻止用户看到个性化控制台。

### 云服务 {#cloud-services}

要使目标内容适用于移动设备应用程序，需要配置两项服务：Adobe Target服务和AdobeMobile Services服务。 Adobe Target服务提供用于处理客户请求和返回个性化内容的引擎。 AdobeMobile Services服务通过ADBMobileConfig.json文件（AMS Cordova插件使用该文件）提供Adobe服务与移动应用程序之间的连接。 在AEM Mobile功能板中，您可以通过添加这两项服务来配置应用程序。

在AEM Mobile功能板中找到管理Cloud Services，然后单击+按钮。

![chlimage_1-38](assets/chlimage_1-38.png)

从添加Cloud Service向导中，选择“Adobe Target”云服务卡，然后单击下一步。

![chlimage_1-39](assets/chlimage_1-39.png)

从选择配置下拉列表中，您可以创建新配置或从现有配置中进行选择。 要创建新配置，请从下拉菜单中选择“创建配置”。 输入Target配置的标题。 输入与您的Target帐户关联的客户端代码、电子邮件和密码。 如果您不知道这些字段的值，请联系Adobe Target支持。 单击“验证”按钮以验证凭据。 验证后，单击提交按钮以创建云服务。

>[!NOTE]
>
>创建的云服务将通过向导自动与移动应用程序关联。 在应用程序组节点的jcr:content节点上设置cq:cloudserviceconfigs属性值。 对于混合应用程序示例，将在/content/mobileapps/hybrid-reference-app/jcr:content中设置，其值指向位于/etc/cloudservices/testandtarget/adobe-target—aem-apps/framework的自动生成框架节点。 框架节点默认设置两个属性，即性别和年龄。 框架仅供AEM预览使用，对设备没有任何影响。

完成向导后，管理Cloud Service拼贴将包含Target云服务，但是它包含有关缺少AdobeMobile Service帐户的警告。

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

还必须将AdobeMobile Services(AMS)帐户关联到应用程序，AMS服务会提供所需的ADBMobileConfig.json文件，其中包含Target客户端代码信息。 在创建与AMS帐户的关联之前，AMS帐户需要由具有AMS权限的用户修改。

### 客户代码 {#client-code}

要登录AMS服务，请访问[https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)，选择移动应用程序并单击设置。 找到“SDK目标选项”字段，并将客户端代码放入该字段中，然后单击保存。

![chlimage_1-41](assets/chlimage_1-41.png)

现在，客户端代码已与移动设备应用程序关联，在通过Adobe移动设备功能板配置AMS云服务后，服务设置的设置将通过ADBMobileConfig.json文件交付。

### AdobeMobile ServiceCloud Service{#adobe-mobile-service-cloud-service}

配置AMS后，应将移动应用程序与Adobe移动功能板中的移动应用程序关联。 在AEM Mobile功能板中找到管理Cloud Services，然后单击+按钮。

![chlimage_1-42](assets/chlimage_1-42.png)

选择AdobeMobile Services卡片，然后单击下一步。

![chlimage_1-43](assets/chlimage_1-43.png)

从创建或选择向导步骤中，选择Mobile Service下拉列表，然后选择创建配置条目。 提供标题、公司、用户名、密码，并选择相应的数据中心。 如果您不知道这些值，请联系AdobeMobile Service管理员以获取它们。 填写完所有字段后，单击“Verify（验证）”按钮。 验证过程将转到AMS并验证帐户的凭据，成功验证后，将填充移动应用程序列表，您从下拉菜单中选择关联的移动应用程序。 单击提交按钮以完成向导。 该过程可能需要一些时间才能获取配置数据以及与应用程序关联的任何分析。 流程完成后，单击模式中的完成按钮以返回至Adobe移动设备功能板。

返回到Mobile Dashboard时，“管理Cloud Services”拼贴将包含AMS云服务。 您还会注意到分析量度拼贴将填充生命周期报表。

![chlimage_1-44](assets/chlimage_1-44.png)

## 对于作者{#for-authors}

**先决条件：** 如上所述，管理员需要先配置与Adobe Target服务的连接，然后作者才能生成新的目标内容。

管理员配置了两项云服务，并且开发人员配置了mobileapporfers处理程序后，内容作者现在可以开始生成目标体验。

在AEM Mobile应用程序中创作目标内容的过程与创作AEM Sites类似：

请参阅此处，获取有关[在AEM](/help/sites-authoring/personalization.md)中创作目标内容的完整概述

## 对于开发人员{#for-developers}

构建移动应用程序的AEM开发人员应继续遵循开发组件时在AEM中常用的模式。 在此，我们将指导您完成使内容作者能够创建目标内容的必要步骤：

### Adobe Target ContentSync处理程序{#adobe-target-contentsync-handlers}

向用户的设备内容交付内容是通过渲染由AEM内容作者创建的选件来生成的。 要处理目标选件的渲染，有一个新的内容同步处理程序将处理选件。 以混合引用应用程序为例， en（英语）内容包包含带有[mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml)处理程序的ContentSyncConfig。 下一步对于向设备渲染选件至关重要。 mobileappoppers处理程序具有path属性，该属性用于标识要用于应用程序的个性化活动的路径。

例如，如果存在位于&#x200B;*/content/campaigns/hybridref*&#x200B;的活动，请复制此路径并将其作为值粘贴到mobileappoffers处理程序的&#x200B;*path*&#x200B;属性中。

>[!NOTE]
>
>对于混合引用应用程序，有两个mobileappopfers处理程序，一个用于开发，一个用于生产。

在mobileapporfers处理程序的路径属性中设置活动路径后，保存处理程序。 处理程序现在可以开始为我们的移动设备渲染选件。

### 呈现模式{#render-mode}

对于发布和开发设置，mobileappoppers处理程序的配置方式有所不同。 对于发布设置，在cq:ContentSyncConfig节点上设置了名为&#x200B;*renderMode*&#x200B;的属性，其值为&#x200B;*publish*。 mobileappopfers处理程序引用renderMode，如果设置为发布，则将修改创建的mbox ID。 默认情况下，由AEM创建的mbox具有一个 — author值，附加到mbox ID。 这表示该活动尚未发布，应使用未发布的营销活动解决选件问题。

通过Adobe移动设备功能板暂存内容时，暂存内容会被视为生产就绪内容，并通过非开发内容同步配置进行渲染。 以这种方式渲染将导致 — author从所有mbox ID中删除，并预期Target服务器上会有发布的活动可用。 在测试暂存内容之前，请确保活动已发布。

### 个性化应用程序开发{#personalization-app-development}

#### 组件 {#components}

任何内容的基础通常是一个页面组件，它根据您使用的是HTL或JSP，扩展了基本AEM页面组件wcm/foundation/components/page或foundation/components/page中的任一个。 这些步骤的持续时间将主要用于使用wcm/foundation/components/page组件。 页面组件的基本结构可划分为多个脚本，每个脚本都提供了特定目的，允许开发人员根据需要组织和覆盖其代码。 “个性化”需要使用的两个脚本是head.html和body.html。 这两个脚本提供了一个可插入代码以支持Context Hub、Cloud Services和移动设备创作的区域。

以下是用于启用内容定位的两个主要脚本的概述。

#### head.html {#head-html}

为了让作者能够定位其内容，需要将目标菜单添加到页面，以便作者可以将上下文从编辑模式更改为定位模式。 要启用此功能，开发人员应修改head.html脚本，以在head.html顶部附近或尽可能靠近&lt;title>&lt;/title>元素的位置包含以下代码片段。

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>请注意，仅当WCM模式未被禁用时，才应包括该脚本，以便在禁用WCM模式时（有关详细信息，请参阅ContentSync处理程序的部分），该脚本将不会包含在最终应用程序代码中。

为了让作者能够预览目标内容，编辑器需要能够找到Adobe Target云服务的配置。 下面的代码块会添加两个重要的脚本。 首先，为页面添加功能，以找到关联的Target云服务并发出对Adobe Target的调用。 第二个是添加了cq.apps.targeting类别。

**cq.apps.targeting**&#x200B;类别覆盖默认的cq/personalization/component/target组件，并使用mobileapps/components/target组件来呈现专门用于移动设备应用程序使用情况的选件。 有关此内容的更多详细信息，请参阅目标组件一节。

应将代码添加到head.html中，并放在&lt;/head>元素结尾之前。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>请注意，代码块将封装在WCM模式中，且未被禁用，因此，仅在内容作者处理创建内容时才会起作用。 云服务脚本将不会添加到生成的移动运行时代码中。

#### body.html {#body-html}

要使内容作者能够测试body.html脚本的不同角色，需要将以下代码块作为body元素的第一个子项包含在内。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

所需的最后一位代码位于body.html的最底部。 此位代码会查找关联的云服务，并插入相应的定位引擎代码。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### 引用应用程序{#reference-application}

[AEM Mobile混合引用应用程序](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)中显示了head.html和body.html的示例，其中显示了开发人员将脚本块放置在两个脚本中的位置。

### 内容同步处理程序{#content-sync-handlers}

内容作者为移动设备应用程序创建完内容后，下一步是下载源并构建应用程序，或暂存要发布的内容。 开发人员涉及许多步骤来实现此目的。 为帮助渲染内容，AEM Mobile会利用内容同步处理程序来渲染和打包内容。 为个性化用例引入了新的内容同步处理程序，以渲染目标内容。 “mobileappoffers”处理程序知道如何渲染由内容作者创建的关联目标选件。 因此，mobileappoffers处理程序扩展了抽象页面更新处理程序，因此许多属性都相似。 mobileappopers处理程序的详细信息具有以下属性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>重写</td>
   <td>+ relativeParentPath<p> - "/"</p> </td>
   <td>rewrite属性标识内容中的路径应如何重写。</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>includePageTypes属性是可选的，默认使用资源类型为cq/personalization/components/teaserpage和cq/personalization/components/offerproxy的页面。 这两种资源类型是定位内容时使用的默认资源类型。 如果需要支持其他资源类型，则应将其添加到includePageTypes的列表。</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>应用程序的位置。</td>
  </tr>
  <tr>
   <td>类型</td>
   <td>mobileappoffers</td>
   <td>作为mobileappopfers的处理程序的名称。</td>
  </tr>
  <tr>
   <td>选择器</td>
   <td>tandt</td>
   <td>标准选择器用于呈现目标内容。 </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>ww</td>
   <td>用于保留已渲染内容的根目录。</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>如果为true，则选件中包含的任何图像都将呈现。 如果跳过假图像。</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true | false</td>
   <td>如果为true，则选件中包含的任何视频都将呈现。 如果跳过假视频。</td>
  </tr>
  <tr>
   <td>路径</td>
   <td>/content/campaigns/&lt;brand&gt;</td>
   <td>指向选件参与的营销活动品牌。 当前，所有选件都必须来自同一营销活动。</td>
  </tr>
  <tr>
   <td>深</td>
   <td>true | false</td>
   <td>如果以递归方式呈现所有子页面，则不以递归方式呈现false。 </td>
  </tr>
  <tr>
   <td>扩展</td>
   <td>html</td>
   <td>设置所呈现资源的扩展。 设置为html，以使页面具有.html扩展名。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>[AEM Mobile混合引用应用程序](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)具有默认mobileappoffer处理程序的配置。 示例中的路径属性为空，因为它取决于营销活动位置。 营销活动作者创建营销活动后，应用程序管理员应通过指定指向营销活动的路径属性，将营销活动与处理程序关联。

### 目标组件{#target-component}

为了帮助专门为移动设备应用程序渲染内容，AEM Mobile使用了mobileapps/components/target组件。 移动设备目标组件扩展了cq/personalization/components/target组件，并覆盖engine_tnt.jsp脚本。 通过覆盖engine_tnt.jsp，AEM Mobile可以控制为移动设备应用程序用例生成的HTML。 对于内容作者所定向的每个组件，engine_tnt.jsp会创建一个关联的mbox。

对于每个mbox，添加了&#x200B;**cq-targeting**&#x200B;的属性，使应用程序开发人员能够编写自定义代码，以便随意使用和使用。 [AEM Mobile混合引用应用程序](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)有一个使用cq-targeting属性的Angular指令示例。 内容替换的概念何时以及如何完成，完全取决于移动应用程序开发人员。 有一个通过AEM /etc/clientlibs/mobileapps/js/mobileapps.js交付的Mobile SDK，该SDK提供了一个API来调用Adobe定位服务。 由应用程序开发人员根据应用程序的设计来指定何时应进行该调用。

## 接下来是什么？{#what-s-next}

1. [开始我的AEM Mobile应用程序体验](/help/mobile/starting-aem-phonegap-app.md)
1. [管理我的应用程序的内容](/help/mobile/phonegap-manage-app-content.md)
1. [构建我的应用程序](/help/mobile/building-app-mobile-phonegap.md)
1. [使用AdobeMobile Analytics跟踪我的应用程序性能](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [使用Adobe Target提供个性化的应用程序体验](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [向我的用户发送重要消息](/help/mobile/phonegap-push-notifications.md)
