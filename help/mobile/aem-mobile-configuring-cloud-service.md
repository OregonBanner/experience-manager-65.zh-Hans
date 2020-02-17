---
title: 配置Adobe Target云服务
seo-title: 配置Adobe Target云服务
description: 可查看本页以了解如何获得针对用户和组的正确权限集、创建云服务、配置活动的应用程序以及最终生成内容。
seo-description: 可查看本页以了解如何获得针对用户和组的正确权限集、创建云服务、配置活动的应用程序以及最终生成内容。
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置Adobe Target云服务 {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>本文档是《AEM Mobile [](/help/mobile/getting-started-aem-mobile.md) Guide入门指南》（AEM Mobile参考的推荐起点）的一部分。

在内容作者开始为移动应用程序生成目标内容之前，需要先完成许多步骤：您可以为用户和用户组获取正确的权限集，创建云服务，为活动配置应用程序，最后生成内容。

以后的假设是 [AEM Mobile Hybrid Reference Application已成功部署](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) ，并可通过AEM Mobile控制面板访问。

## 权限 {#permissions}

需要访问个性化控制台的用户必须是组的一 `target-activity-authors` 部分。 建议在用户和用户组设置中，将target-activity-group添加到apps-admins组。 通过添加target-activity-authors组，用户将能够看到个性化导航菜单条目。

忘记将要有权访问个性化管理控制台的用户或用户组添加到target-activity-authors组将阻止用户看到个性化控制台。

## 云服务 {#cloud-services}

要使目标内容适用于移动应用程序，需要配置两个服务：Adobe Target服务和Adobe Mobile services服务。 Adobe Target service为处理客户请求和返回个性化内容提供了引擎。 Adobe Mobile services服务通过ADBMobileConfig.json文件（由AMS Cordova插件使用）提供Adobe服务与移动应用程序之间的连接。 从AEM Mobile控制面板中，您可以通过添加这两个服务来配置应用程序。

## Adobe Target Cloud Service {#adobe-target-cloud-service}

在AEM Mobile控制面板中，找到管理云服务，然后单击+按钮。

![chlimage_1-8](assets/chlimage_1-8.png)

从“添加云服务”向导中，选择“Adobe Target”云服务卡，然后单击“下一步”。

![chlimage_1-9](assets/chlimage_1-9.png)

从选择配置下拉列表中，您可以创建新配置或从现有配置中进行选择。 要创建新配置，请从下拉菜单中选择“创建配置”。 输入Target配置的标题。 输入与Target帐户关联的客户代码、电子邮件和密码。 如果您不知道这些字段的值，请与Adobe target支持联系。 单击“验证”按钮以验证凭据。 验证后，单击“提交”按钮以创建云服务。

创建的云服务会通过向导自动与移动应用程序关联。 cq:cloudserviceconfigs属性值在应用程序组节点的jcr:content节点上设置。 对于混合应用程序范例，将在/content/mobileapps/hybrid-reference-app/jcr:content上设置，其值指向位于/etc/cloudservices/testandtarget/adobe-target—aem-apps/framework的自动生成的框架节点。 框架节点默认设置有两个属性，即性别和年龄。 框架仅供AEM预览使用，对设备没有任何影响。

完成向导后，“管理云服务”拼贴将包含Target云服务，但是，它包含有关缺少Adobe Mobile service帐户的警告。

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe Mobile Service {#adobe-mobile-service}

还需要将Adobe Mobile Services(AMS)帐户关联到应用程序，AMS服务提供所需的ADBMobileConfig.json文件，其中包含Target客户端代码信息。 在创建与AMS帐户的关联之前，AMS帐户需要由具有AMS权限的用户修改。

### 客户代码 {#client-code}

要登录AMS服务，请访问https://mobilemarketing.adobe.com [](https://mobilemarketing.adobe.com/)，选择手机应用程序并单击设置。 找到“SDK目标选项”字段，将客户端代码放入该字段中，然后单击“保存”。

![chlimage_1-11](assets/chlimage_1-11.png)

既然客户端代码已与移动应用程序关联，通过Adobe Mobile Dashboard配置AMS云服务后，服务设置的设置将通过ADBMobileConfig.json文件传送。

### Adobe Mobile service可以服务 {#adobe-mobile-service-could-service}

AMS已配置完毕，现在是时候在Adobe Mobile Dashboard中关联移动应用程序了。 在AEM Mobile控制面板中，找到管理云服务，然后单击+按钮。

![chlimage_1-12](assets/chlimage_1-12.png)

选择Adobe Mobile services卡并单击“下一步”。

![chlimage_1-13](assets/chlimage_1-13.png)

从创建或选择向导步骤中，选择Mobile service下拉列表，然后选择创建配置条目。 提供标题、公司、用户名、密码，然后选择相应的数据中心。 如果您不知道这些值，请与Adobe Mobile service管理员联系以获取它们。 填写完所有字段后，单击“验证”按钮。 验证过程将转到AMS并验证帐户的凭据，成功验证后，将填充移动应用程序列表，您可以从下拉列表中选择关联的移动应用程序。 单击“提交”按钮以完成向导。 该过程可能需要一点时间才能获得配置数据以及与应用程序相关的任何分析。 完成该过程后，单击模态中的“完成”按钮，返回Adobe Mobile Dashboard。

返回至Mobile Dashboard,“管理云服务”拼贴将包含AMS云服务。 您还会注意到，“分析指标”拼贴中将填充生命周期报告。

![chlimage_1-14](assets/chlimage_1-14.png)

## 目标内容同步处理程序 {#target-content-sync-handlers}

要向用户的设备内容传送内容，请通过呈现由AEM内容作者创建的选件来生成内容。 要处理目标选件的呈现，有一个新的内容同步处理程序将处理选件。 使用Hybrid Reference Application作为示例，en（英语）内容包中包含带mobileapporfers处理函数的ContentSyncConfig [](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 。 下一步是向设备呈现选件的关键步骤。 mobileapporfers处理程序有一个路径属性，用于标识要用于应用程序的个性化活动的路径。

例如，如果存在位于 */content/campaigns/hybridref的活动，请复制此路径，并将其作为值粘贴到mobileapporfers处理程序的*** path属性中。

对于Hybrid Reference Application，有两个mobileapporfer处理程序，一个用于开发，一个用于制作。

在mobileapporfers处理程序的路径属性中设置活动路径后，保存该处理程序。 该处理程序现在可以开始为我们的移动设备渲染选件。

### 渲染模式 {#render-mode}

mobileapporfers处理程序的配置方式与发布和开发设置不同。 对于发布设置，存在一个名为 *renderMode的属性* ，该属性在cq:ContentSyncConfig节点上 *设置了publish* 的值。 mobileapporfers处理函数引用renderMode，如果设置为发布，将修改创建的mbox id。 默认情况下，由AEM创建的mbox在mbox id上附加一个—author值。 这会标识活动尚未发布，并应使用未发布的营销活动解决选件问题。

通过Adobe Mobile Dashboard暂存内容时，暂存内容将被视为生产就绪内容，并通过非开发内容同步配置进行呈现。 以这种方式呈现将导致从所有mbox ID中删除—author，并期望在Target服务器上提供已发布的活动。 在测试分阶段内容之前，请确保已发布活动。

## 创建内容 {#creating-content}

现在，已创建云服务并配置mobileapporfers处理程序，内容作者可以开始生成目标体验。
