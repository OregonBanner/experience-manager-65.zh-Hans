---
title: 配置Adobe TargetCloud Service
seo-title: 配置Adobe TargetCloud Service
description: 可查看本页以了解如何获得针对用户和组的正确权限集、创建云服务、为活动配置应用程序以及最终生成内容。
seo-description: 可查看本页以了解如何获得针对用户和组的正确权限集、创建云服务、为活动配置应用程序以及最终生成内容。
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 0%

---


# 配置Adobe TargetCloud Service{#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>此文档是[《AEM Mobile入门指南》的一部分，该指南是推荐的AEM Mobile参考起点。](/help/mobile/getting-started-aem-mobile.md)

在内容作者可以开始为移动应用程序生成目标内容之前，需要先完成许多步骤：您可以为用户和用户组获取正确的权限集，创建云服务，为活动配置应用程序，最后生成内容。

未来的假设是[AEM Mobile混合参考应用程序](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)已成功部署并可通过AEM Mobile仪表板访问。

## 权限 {#permissions}

需要访问个性化控制台的用户必须属于`target-activity-authors`组。 建议在用户和组设置中，将目标活动组添加到应用程序管理员组。 通过添加目标-活动-作者组，用户将能够看到个性化导航菜单条目。

忘记将要有权访问个性化管理控制台的用户或用户组添加到目标活动作者组将阻止用户看到个性化控制台。

## 云服务 {#cloud-services}

要使目标内容适用于移动应用程序，需要配置两个服务：Adobe Target服务和Adobe移动服务。 Adobe Target服务提供处理客户请求和返回个性化内容的引擎。 AdobeMobile Services服务通过ADBMobileConfig.json文件提供Adobe服务与移动应用程序之间的连接，该文件由AMS Cordova插件使用。 从AEM Mobile仪表板，您可以通过添加两个服务来配置应用程序。

## Adobe TargetCloud Service{#adobe-target-cloud-service}

在AEM Mobile仪表板中找到“管理”Cloud Services并单击+按钮。

![chlimage_1-8](assets/chlimage_1-8.png)

从添加Cloud Service向导中，选择“Adobe Target”云服务卡，然后单击下一步。

![chlimage_1-9](assets/chlimage_1-9.png)

从选择配置下拉菜单中，您可以创建新配置或从现有配置中进行选择。 要创建新配置，请从下拉列表中选择“创建配置”。 输入目标配置的标题。 输入与您的目标帐户关联的客户代码、电子邮件和密码。 如果您不知道这些字段的值，请与Adobe Target支持部门联系。 单击“验证”按钮验证凭据。 验证后，单击“提交”按钮以创建云服务。

创建的云服务会通过向导自动与移动应用程序关联。 cq:cloudserviceconfigs属性值在应用程序组节点的jcr:content节点上设置。 对于混合应用程序范例，它将设置在/content/mobileapps/hybrid-reference-app/jcr:content上，该值指向位于/etc/cloudservices/testandtarget/adobe-目标的自动生成的框架节点。 框架节点默认设置两个属性，即性别和年龄。 框架仅供AEM预览使用，对设备没有任何影响。

完成向导后，管理Cloud Service拼贴将包含目标云服务，但是它包含有关缺少AdobeMobile服务帐户的警告。

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe移动服务{#adobe-mobile-service}

AMS服务还需要将AdobeMobile Services(AMS)帐户链接到应用程序，AMS服务提供所需的ADBMobileConfig.json文件，其中包含目标客户端代码信息。 在创建与AMS帐户的关联之前，AMS帐户需要由具有AMS权限的用户修改。

### 客户代码 {#client-code}

要登录AMS服务，请访问[https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)，选择移动应用程序并单击设置。 找到“SDK目标选项”字段，将客户端代码放入该字段，然后单击“保存”。

![chlimage_1-11](assets/chlimage_1-11.png)

既然客户端代码已与移动应用程序关联，通过Adobe移动仪表板配置AMS云服务时，服务设置的设置将通过ADBMobileConfig.json文件传送。

### Adobe移动服务可以服务{#adobe-mobile-service-could-service}

AMS已配置完毕，现在是时候在Adobe移动仪表板中关联移动应用程序了。 在AEM Mobile仪表板中找到“管理”Cloud Services并单击+按钮。

![chlimage_1-12](assets/chlimage_1-12.png)

选择AdobeMobile Services卡并单击“下一步”。

![chlimage_1-13](assets/chlimage_1-13.png)

从创建或选择向导步骤中，选择Mobile Service下拉列表，然后选择创建配置条目。 提供标题、公司、用户名、密码，并选择相应的数据中心。 如果您不知道这些值，请与AdobeMobile服务管理员联系以获取它们。 填写完所有字段后，单击“验证”按钮。 验证过程将转至AMS并验证帐户的凭据，成功验证后，将填充手机应用程序列表，从下拉列表中选择关联的手机应用程序。 单击“提交”按钮以完成向导。 该过程可能需要一些时间才能获得配置数据和与应用程序相关的任何分析。 完成该过程后，单击模态中的完成按钮，返回Adobe移动仪表板。

返回至移动仪表板，管理Cloud Services拼贴将包含AMS云服务。 您还会注意到，“分析指标”拼贴中将填充生命周期报告。

![chlimage_1-14](assets/chlimage_1-14.png)

## 目标内容同步处理程序{#target-content-sync-handlers}

要向用户的设备内容传送内容，请通过呈现AEM内容作者创建的优惠来生成内容。 要处理目标优惠的呈现，有一个新的内容同步处理程序将处理优惠。 将Hybrid Reference Application作为示例，en（英语）内容包包含带有[mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml)处理函数的ContentSyncConfig。 下一步对于向设备呈现优惠至关重要。 mobileapporfers处理程序具有一个路径属性，它标识要用于应用程序的个性化活动的路径。

例如，如果存在位于&#x200B;*/content/活动/hybridref*&#x200B;的活动，则复制此路径并将其作为值粘贴到mobileapporfers处理函数的&#x200B;*path*&#x200B;属性。

对于Hybrid Reference Application，有两个mobileappoffers处理程序，一个用于开发，一个用于制作。

在mobileapporfers处理函数的路径属性中设置活动路径后，保存该处理函数。 该处理程序现在可以为我们的移动设备开始渲染优惠。

### 渲染模式{#render-mode}

mobileapporfers处理程序的配置方式与发布和开发设置不同。 对于发布设置，在cq:ContentSyncConfig节点上设置了名为&#x200B;*renderMode*&#x200B;的属性值为&#x200B;*publish*&#x200B;的属性。 mobileapporfers处理函数引用renderMode，如果设置为发布，将修改创建的mbox id。 默认情况下，AEM创建的mbox在mbox id后附加一个—author值。 这表示活动尚未发布，应使用未发布的活动进行优惠解决。

通过Adobe移动仪表板暂存内容时，暂存内容将被视为生产就绪内容，并通过非开发内容同步配置进行呈现。 以这种方式呈现将导致从所有mbox id中删除—author，并期望在目标服务器上提供已发布的活动。 在测试分阶段内容之前，请确保活动已发布。

## 创建内容{#creating-content}

现在，已创建云服务并配置mobileapporfers处理程序，内容作者现在可以开始生成目标体验。
