---
title: AEM Mobile内容个性化
seo-title: AEM Mobile内容个性化
description: 可查看本页以了解AEM Mobile内容个性化功能，该功能允许AEM作者利用Adobe Target个性化移动App内容。
seo-description: 可查看本页以了解AEM Mobile内容个性化功能，该功能允许AEM作者利用Adobe Target个性化移动App内容。
uuid: 9078edd1-8399-485f-8a63-a07e766f7ef9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c9c818dc-c5c4-4a96-94fe-9dc9fe75705b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2701'
ht-degree: 0%

---


# AEM Mobile内容个性化{#aem-mobile-content-personalization}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>此文档是[《AEM Mobile入门指南》的一部分，该指南是推荐的AEM Mobile参考起点。](/help/mobile/getting-started-aem-mobile.md)

AEM Mobile内容个性化功能允许[AEM作者](#author)利用[Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html)个性化移动应用程序内容。 这允许将目标优惠投放给移动应用程序用户。 Adobe Experience Manager Mobile提供创建、目标和交付内容的能力，这些内容将为用户提供特定于其个人口味的内容。

正如AEM中经常出现的情况一样，为了作者能够开始创建此内容，管理员和开发人员需要先准备环境。

[AEM ](#administrator) dministrator需要在AEM Mobile和Adobe TargetCloud Service之间建立联系。

同时，AEM Mobile[开发人员](#developer)需要修改其现有脚本以便于进行有针对性的内容创作。

## 对于管理员{#for-administrators}

在内容作者可以开始为移动应用程序生成目标内容之前，需要先完成许多步骤：您可以为用户和用户组获取正确的权限集，创建云服务，为活动配置应用程序，最后生成内容。

本文将指导您完成配置[AEM Mobile混合引用应用程序](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)用于定位的过程。

今后的假设是，AEM Mobile混合参考应用程序已经成功部署，并可通过AEM Mobile仪表板访问。

在作者可以在应用程序中生成目标内容之前，AEM实例需要使用Adobe TargetCloud Service[进行配置。](/help/mobile/aem-mobile-configuring-cloud-service.md)

### 权限 {#permissions}

需要访问个性化控制台的用户必须属于`target-activity-authors`组。

建议在用户和组设置中，将目标活动组添加到应用程序管理员组。 通过添加目标-活动-作者组，用户将能够看到个性化导航菜单条目。

>[!NOTE]
>
>忘记将要有权访问个性化管理控制台的用户或用户组添加到目标活动作者组将阻止用户看到个性化控制台。

### 云服务 {#cloud-services}

要使目标内容适用于移动应用程序，需要配置两个服务：Adobe Target服务和Adobe移动服务。 Adobe Target服务提供处理客户请求和返回个性化内容的引擎。 AdobeMobile Services服务通过ADBMobileConfig.json文件提供Adobe服务与移动应用程序之间的连接，该文件由AMS Cordova插件使用。 从AEM Mobile仪表板，您可以通过添加两个服务来配置应用程序。

在AEM Mobile仪表板中找到“管理”Cloud Services并单击+按钮。

![chlimage_1-38](assets/chlimage_1-38.png)

从添加Cloud Service向导中，选择“Adobe Target”云服务卡，然后单击下一步。

![chlimage_1-39](assets/chlimage_1-39.png)

从选择配置下拉菜单中，您可以创建新配置或从现有配置中进行选择。 要创建新配置，请从下拉列表中选择“创建配置”。 输入目标配置的标题。 输入与您的目标帐户关联的客户代码、电子邮件和密码。 如果您不知道这些字段的值，请与Adobe Target支持部门联系。 单击“验证”按钮验证凭据。 验证后，单击“提交”按钮以创建云服务。

>[!NOTE]
>
>创建的云服务会通过向导自动与移动应用程序关联。 cq:cloudserviceconfigs属性值在应用程序组节点的jcr:content节点上设置。 对于混合应用程序范例，它将设置在/content/mobileapps/hybrid-reference-app/jcr:content上，该值指向位于/etc/cloudservices/testandtarget/adobe-目标的自动生成的框架节点。 框架节点默认设置两个属性，即性别和年龄。 框架仅供AEM预览使用，对设备没有任何影响。

完成向导后，管理Cloud Service拼贴将包含目标云服务，但是它包含有关缺少AdobeMobile服务帐户的警告。

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

AMS服务还需要将AdobeMobile Services(AMS)帐户链接到应用程序，AMS服务提供所需的ADBMobileConfig.json文件，其中包含目标客户端代码信息。 在创建与AMS帐户的关联之前，AMS帐户需要由具有AMS权限的用户修改。

### 客户代码 {#client-code}

要登录AMS服务，请访问[https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)，选择移动应用程序并单击设置。 找到“SDK目标选项”字段，将客户端代码放入该字段，然后单击“保存”。

![chlimage_1-41](assets/chlimage_1-41.png)

既然客户端代码已与移动应用程序关联，通过Adobe移动仪表板配置AMS云服务时，服务设置的设置将通过ADBMobileConfig.json文件传送。

### Adobe移动服务Cloud Service{#adobe-mobile-service-cloud-service}

AMS已配置完毕，现在是时候在Adobe移动仪表板中关联移动应用程序了。 在AEM Mobile仪表板中找到“管理”Cloud Services并单击+按钮。

![chlimage_1-42](assets/chlimage_1-42.png)

选择AdobeMobile Services卡并单击“下一步”。

![chlimage_1-43](assets/chlimage_1-43.png)

从创建或选择向导步骤中，选择Mobile Service下拉列表，然后选择创建配置条目。 提供标题、公司、用户名、密码，并选择相应的数据中心。 如果您不知道这些值，请与AdobeMobile服务管理员联系以获取它们。 填写完所有字段后，单击“验证”按钮。 验证过程将转至AMS并验证帐户的凭据，成功验证后，将填充手机应用程序列表，从下拉列表中选择关联的手机应用程序。 单击“提交”按钮以完成向导。 该过程可能需要一些时间才能获得配置数据和与应用程序相关的任何分析。 完成该过程后，单击模态中的完成按钮，返回Adobe移动仪表板。

返回至移动仪表板，管理Cloud Services拼贴将包含AMS云服务。 您还会注意到，“分析指标”拼贴中将填充生命周期报告。

![chlimage_1-44](assets/chlimage_1-44.png)

## 对于作者{#for-authors}

**入门项** 目：如上所述，管理员需要先配置到Adobe Target服务的连接，然后作者才能生成新的目标内容。

管理员配置了两个云服务并且开发人员配置了mobileapporfers处理程序后，内容作者现在可以开始生成目标体验。

在AEM Mobile应用程序内创作目标内容的过程与创作AEM Sites类似：

有关在AEM[中创作目标内容的完整概述，请参阅此处](/help/sites-authoring/personalization.md)

## 对于开发人员{#for-developers}

构建移动应用程序的AEM开发人员应继续遵循在开发组件时在整个AEM中常用的模式。 在此，我们将引导您完成使内容作者能够创建目标内容的必要步骤：

### Adobe TargetContentSync处理程序{#adobe-target-contentsync-handlers}

要向用户的设备内容传送内容，请通过呈现AEM内容作者创建的优惠来生成内容。 要处理目标优惠的呈现，有一个新的内容同步处理程序将处理优惠。 将Hybrid Reference Application作为示例，en（英语）内容包包含带有[mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml)处理函数的ContentSyncConfig。 下一步对于向设备呈现优惠至关重要。 mobileapporfers处理程序具有一个路径属性，它标识要用于应用程序的个性化活动的路径。

例如，如果存在位于&#x200B;*/content/活动/hybridref*&#x200B;的活动，则复制此路径并将其作为值粘贴到mobileapporfers处理函数的&#x200B;*path*&#x200B;属性。

>[!NOTE]
>
>对于Hybrid Reference Application，有两个mobileappoffers处理程序，一个用于开发，一个用于制作。

在mobileapporfers处理函数的路径属性中设置活动路径后，保存该处理函数。 该处理程序现在可以为我们的移动设备开始渲染优惠。

### 渲染模式{#render-mode}

mobileapporfers处理程序的配置方式与发布和开发设置不同。 对于发布设置，在cq:ContentSyncConfig节点上设置了名为&#x200B;*renderMode*&#x200B;的属性值为&#x200B;*publish*&#x200B;的属性。 mobileapporfers处理函数引用renderMode，如果设置为发布，将修改创建的mbox id。 默认情况下，AEM创建的mbox在mbox id后附加一个—author值。 这表示活动尚未发布，应使用未发布的活动进行优惠解决。

通过Adobe移动仪表板暂存内容时，暂存内容将被视为生产就绪内容，并通过非开发内容同步配置进行呈现。 以这种方式呈现将导致从所有mbox id中删除—author，并期望在目标服务器上提供已发布的活动。 在测试分阶段内容之前，请确保活动已发布。

### 个性化应用程序开发{#personalization-app-development}

#### 组件 {#components}

任何内容的基础通常是页面组件，它根据您使用的是HTL还是JSP扩展了基本AEM页面组件wcm/foundation/components/page或foundation/components/page。 这些步骤的持续时间将集中于使用wcm/foundation/components/page组件。 页面组件的基本结构被分解为多个脚本，每个脚本提供允许开发人员根据需要组织和覆盖其代码的特定用途。 个性化需要的两个脚本是head.html和body.html。 这两个脚本提供了一个可插入代码以支持Context Hub、Cloud Services和移动创作的区域。

以下是用于启用内容定位的两个主脚本的概述。

#### head.html {#head-html}

要使作者能够目标其内容，需要将目标菜单添加到页面，以便作者能够将上下文从编辑模式更改为定位模式。 要启用此功能，开发人员应修改head.html脚本，在head.html顶部附近或尽可能靠近&lt;title>&lt;/title>元素的地方加入以下代码片段。

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>请注意，仅当WCM模式未禁用时才应包括该脚本，这样在禁用WCM模式时（有关详细信息，请参阅ContentSync处理程序的部分），该脚本将不包括在最终的应用程序代码中。

要使作者能够预览目标内容，编辑者需要能够找到Adobe Target云服务的配置。 下面的代码块添加了两个重要的脚本。 首先，添加页面查找关联的目标云服务并拨叫Adobe Target的功能。 第二种是添加cq.apps.targeting类别。

**cq.apps.targeting**&#x200B;类别将覆盖默认的cq/personalization/component/目标组件，并使用mobileapps/components/目标组件来呈现专门用于移动应用程序使用的优惠。 有关此内容的更多详细信息，将在目标组件部分中讨论。

应将代码添加到head.html中，并放在&lt;/head>元素末尾之前。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>请注意，代码块打包在WCM模式中，未禁用，因此仅在内容作者正在创建内容时才开始播放。 云服务脚本将不会添加到生成的移动运行时代码中。

#### body.html {#body-html}

要使内容作者能够测试body.html脚本的不同角色，需要将以下代码块作为body元素的第一个子代包含进来。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

所需的最后一位代码位于body.html的最底部。 此部分代码会查找关联的云服务并注入相应的定位引擎代码。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### 引用应用程序{#reference-application}

可以在[AEM Mobile混合引用应用程序](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)中找到head.html和body.html的示例，该应用程序显示开发人员将脚本块放在两个脚本中的位置。

### 内容同步处理程序{#content-sync-handlers}

当内容作者为移动应用程序创建完内容后，下一步是下载源并构建应用程序，或暂存要发布的内容。 开发人员参与了许多步骤，以实现此目的。 为了帮助呈现内容，AEM Mobile利用内容同步处理程序来呈现和打包内容。 为个性化用例引入了一个新的内容同步处理程序，用于呈现目标内容。 “mobileapporfers”处理程序知道如何呈现由内容作者创建的关联目标优惠。 mobileapporfers处理函数因此扩展了抽象页面更新处理函数，因此许多属性是相似的。 mobileapporpers处理程序的详细信息具有以下属性。

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
   <td>rewrite属性标识如何重写内容中的路径。</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>“cq/personalization/components/offerproxy”</p> </td>
   <td>includePageTypes属性是可选的，默认使用资源类型为cq/personalization/components/teaserpage和cq/personalization/components/offerproxy的页面。 这两种资源类型是定位内容时使用的默认资源类型。 如果需要支持其他资源类型，应将其添加到includePageTypes的列表。</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>应用程序的位置。</td>
  </tr>
  <tr>
   <td>类型</td>
   <td>mobileapporffers</td>
   <td>作为mobileapporffers的处理程序的名称。</td>
  </tr>
  <tr>
   <td>选择器</td>
   <td>tandt</td>
   <td>标准选择器用于呈现目标内容。 </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>ww</td>
   <td>保留呈现内容的根目录。</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>真 |假</td>
   <td>如果为true，则渲染优惠中包含的任何图像。 如果跳过假图像。</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>真 |假</td>
   <td>如果为true，则将呈现优惠中包含的任何视频。 如果跳过假视频。</td>
  </tr>
  <tr>
   <td>路径</td>
   <td>/content/活动/&lt;brand&gt;</td>
   <td>指向活动所参与的优惠品牌。 目前，所有优惠必须来自同一活动。</td>
  </tr>
  <tr>
   <td>深</td>
   <td>真 |假</td>
   <td>如果递归呈现所有子页面，则不递归呈现false。 </td>
  </tr>
  <tr>
   <td>扩展</td>
   <td>html</td>
   <td>设置要呈现的资源的扩展。 设置为html，使页面具有。html扩展名。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>[AEM Mobile混合引用应用程序](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)具有默认mobileappoffer处理程序的配置。 示例中的路径属性为空，因为它取决于活动位置。 在活动作者创建活动后，应用程序管理员应通过指定指向活动的路径属性，将活动与处理函数相关联。

### 目标组件{#target-component}

为了帮助呈现专为移动应用程序而设计的内容，AEM Mobile使用mobileapps/components/目标组件。 移动目标组件扩展了cq/personalization/components/目标组件并覆盖engine_tnt.jsp脚本。 通过覆盖engine_tnt.jsp,AEM Mobile可以控制为移动应用程序用例生成的HTML。 对于内容作者所针对的每个组件，将由engine_tnt.jsp创建一个关联的mbox。

对于每个mbox，都添加了&#x200B;**cq-targeting**&#x200B;的属性，允许应用程序开发人员编写自定义代码以随心所欲地使用和使用。 [AEM Mobile混合引用应用程序](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)有一个使用cq-targeting属性的Angular指令示例。 内容替换的概念在何时以及如何完成，这完全取决于移动应用程序开发者。 有一个通过AEM /etc/clientlibs/mobileapps/js/mobileapps.js交付的Mobile SDK，它提供一个API来调用Adobe定位服务。 由应用程序开发人员根据应用程序的设计指定何时应进行该调用。

## 下一步是什么？{#what-s-next}

1. [开始我的AEM Mobile应用程序体验](/help/mobile/starting-aem-phonegap-app.md)
1. [管理我的应用程序的内容](/help/mobile/phonegap-manage-app-content.md)
1. [构建我的应用程序](/help/mobile/building-app-mobile-phonegap.md)
1. [使用Adobe移动分析跟踪我的应用程序的性能](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [通过Adobe Target提供个性化的App体验](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [向我的用户发送重要消息](/help/mobile/phonegap-push-notifications.md)
