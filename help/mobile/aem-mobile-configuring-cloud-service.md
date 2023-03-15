---
title: 配置Adobe TargetCloud Service
seo-title: Configuring Adobe Target Cloud Service
description: 按照本页面了解如何为用户和组获取正确的权限集、创建云服务、为活动配置应用程序，以及最终生成内容。
seo-description: Follow this page to understand how to get right set of permissions for users and groups, creating cloud services, configuring the application for the activity, and finally generating the content.
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
exl-id: d370d772-ef4d-4f38-826c-e90d07735822
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1298'
ht-degree: 0%

---

# 配置Adobe TargetCloud Service {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

>[!NOTE]
>
>本文档是 [AEM Mobile快速入门](/help/mobile/getting-started-aem-mobile.md) 指南，建议的AEM Mobile参考起点。

在内容作者可以开始为移动应用程序生成目标内容之前，需要完成许多步骤：为用户和组获取正确的权限集、创建云服务、为活动配置应用程序，以及最终生成内容。

未来的假设是 [AEM Mobile混合引用应用程序](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 已成功部署并可通过AEM Mobile功能板访问。

## 权限 {#permissions}

需要访问个性化控制台的用户需要成为 `target-activity-authors` 组。 建议在用户和组设置过程中，将target-activity-group添加到apps-admins组中。 通过添加target-activity-authors组，用户将能够查看个性化导航菜单条目。

如果忘记将您希望有权访问个性化管理控制台的用户或组添加到target-activity-authors组，则将阻止用户查看个性化控制台。

## Cloud Service {#cloud-services}

要获得适用于移动设备应用程序的目标内容，需要配置两项服务：Adobe Target服务和AdobeMobile Services服务。 Adobe Target服务提供用于处理客户端请求和返回个性化内容的引擎。 AdobeMobile Services服务通过AMS Cordova插件使用的ADBMobileConfig.json文件提供Adobe服务和移动应用程序之间的连接。 在AEM Mobile功能板中，您可以通过添加这两个服务来配置应用程序。

## Adobe TargetCloud Service {#adobe-target-cloud-service}

在AEM Mobile功能板中，找到管理Cloud Services，然后单击+按钮。

![chlimage_1-8](assets/chlimage_1-8.png)

从“添加Cloud Service”向导中，选择“Adobe Target”云服务卡，然后单击下一步。

![chlimage_1-9](assets/chlimage_1-9.png)

从选择配置下拉列表中，您可以创建新配置或从现有配置中进行选择。 要创建新配置，请从下拉菜单中选择“创建配置”。 输入Target配置的标题。 输入与Target帐户关联的客户端代码、电子邮件和密码。 如果您不知道这些字段的值，请联系Adobe Target支持。 单击“验证”按钮验证凭据。 验证后，单击提交按钮以创建云服务。

创建的云服务将通过向导自动与移动应用程序关联。 在apps组节点的jcr：content节点上设置cq：cloudserviceconfigs属性值。 对于混合应用程序示例，将在/content/mobileapps/hybrid-reference-app/jcr：content中设置此参数，其值指向自动生成的框架节点，该节点位于/etc/cloudservices/testandtarget/adobe-target—aem-apps/framework。 框架节点默认设置了两个属性：性别和年龄。 此框架仅供AEM预览使用，对设备没有任何影响。

完成该向导后，“管理Cloud Service”图块将包含Target云服务，但它包含有关缺少Adobe移动服务帐户的警告。

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe移动服务 {#adobe-mobile-service}

还必须将AdobeMobile Services (AMS)帐户链接到应用程序，AMS服务会提供所需的ADBMobileConfig.json文件，其中包含Target客户端代码信息。 在创建与AMS帐户的关联之前，需要由具有AMS权限的用户修改AMS帐户。

### 客户代码 {#client-code}

要登录AMS服务，请访问 [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)，选择移动设备应用程序，然后单击设置。 找到SDK目标选项字段，将客户端代码放入该字段，然后单击保存。

![chlimage_1-11](assets/chlimage_1-11.png)

现在，客户端代码已与移动应用程序关联，当通过Adobe移动仪表板配置AMS云服务时，服务设置的设置将通过ADBMobileConfig.json文件交付。

### Adobe移动服务可以提供服务 {#adobe-mobile-service-could-service}

现在AMS已配置，是时候在Adobe移动设备仪表板中关联移动设备应用程序了。 在AEM Mobile功能板中，找到管理Cloud Services，然后单击+按钮。

![chlimage_1-12](assets/chlimage_1-12.png)

选择AdobeMobile Services信息卡，然后单击下一步。

![chlimage_1-13](assets/chlimage_1-13.png)

从创建或选择向导步骤中选择Mobile Service下拉列表，然后选择创建配置条目。 提供标题、公司、用户名、密码并选择适当的数据中心。 如果您不知道这些值，请与AdobeMobile Service管理员联系以获取它们。 填写完所有字段后，单击验证按钮。 验证过程将转至AMS并验证帐户的凭据，在验证成功后，将填充移动设备应用程序列表，您可以从下拉列表中选择关联的移动设备应用程序。 单击“提交”按钮以完成向导。 该过程可能需要一些时间来获取配置数据以及与应用程序关联的任何分析。 流程完成后，单击模式窗口中的Done按钮以返回到Adobe移动设备仪表板。

返回移动设备仪表板后，“管理Cloud Services”图块将包含AMS云服务。 您还将注意到，“分析量度”图块中将填充有生命周期报表。

![chlimage_1-14](assets/chlimage_1-14.png)

## Target内容同步处理程序 {#target-content-sync-handlers}

要向用户的设备内容交付内容，将通过呈现由AEM内容作者创建的选件来生成该内容。 要处理Target选件的渲染，可使用新的内容同步处理程序来处理选件。 使用混合引用应用程序作为示例，en（英语）内容包中包含的ContentSyncConfig具有 [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 处理程序。 下一步对于向设备呈现选件至关重要。 mobileappoffers处理程序的path属性标识要用于应用程序的个性化活动的路径。

例如，如果某个活动位于 */content/campaigns/hybridref* 复制此路径并将其作为值粘贴到 *路径* mobileappoffers处理程序的属性。

对于混合引用应用程序，有两个mobileappoffer处理程序，一个用于开发，一个用于生产。

在mobileappoffers处理程序的path属性中设置活动路径后，请保存该处理程序。 处理程序现在可以开始呈现我们移动设备的选件。

### 渲染模式 {#render-mode}

Mobileappoffers处理程序在发布和开发设置中的配置方式不同。 对于发布设置，有一个名为的属性 *渲染模式* 具有值 *发布* 在cq：ContentSyncConfig节点上设置。 mobileappoffers处理程序引用renderMode，如果设置为publish，则将修改所创建的mbox id。 默认情况下，由AEM创建的mbox会将 — author值附加到mbox id。 这会标识该活动尚未发布，应使用未发布的促销活动来获取优惠解决方案。

通过Adobe移动设备仪表板暂存内容时，暂存内容被视为生产就绪内容，并通过非开发内容同步配置进行渲染。 按此方式呈现将导致从所有mbox id中删除 — author，并预期Target服务器上会提供一个已发布的活动。 在测试暂存内容之前，请确保已发布活动。

## 创建内容 {#creating-content}

现在，创建了云服务并配置了mobileappoffers处理程序，内容作者现在可以开始生成目标体验。
