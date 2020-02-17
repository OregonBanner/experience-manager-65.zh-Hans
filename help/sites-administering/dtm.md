---
title: 与Adobe动态标签管理集成
seo-title: 与Adobe动态标签管理集成
description: 了解与Adobe动态标签管理的集成。
seo-description: 了解与Adobe动态标签管理的集成。
uuid: cbb9f942-44e3-4cd5-b07d-4298a7a08376
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b8c7a20a-7694-4a49-b66a-060720f17dad
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 与Adobe动态标签管理集成 {#integrating-with-adobe-dynamic-tag-management}

将 [Adobe动态标签管理与AEM集成](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) ，以便您可以使用动态标签管理Web属性跟踪AEM站点。 动态标签管理使营销人员能够管理用于收集数据的标签，并跨数字营销系统分发数据。 例如，使用动态标签管理收集AEM网站的使用数据，并分发数据以在Adobe Analytics或Adobe Target中进行分析。

在集成之前，您需要创建跟踪AEM站 [点域的动态标签](https://microsite.omniture.com/t2/help/en_US/dtm/#Web_Properties) Web属性。 必须 [配置Web属性的托管选项](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) ，以便您能够配置AEM以访问动态标签管理库。

配置集成后，对动态标签管理部署工具和规则所做的更改不需要您在AEM中更改动态标签管理配置。 这些更改将自动对AEM可用。

>[!NOTE]
>
>如果您使用具有自定义代理配置的DTM，则需要配置两个HTTP客户端代理配置，因为AEM的某些功能使用3.x API，而其他功能使用4.x API:
>
>* 3.x已配置http://localhost:4502/system/console/configMgr/com.day.commons.httpclient [](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x已配置http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator [](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



## 部署选项 {#deployment-options}

以下部署选项影响与动态标签管理集成的配置。

### 动态标签管理托管 {#dynamic-tag-management-hosting}

AEM支持在云中托管或在AEM上托管的动态标签管理。

* 云托管：动态标签管理javascript库存储在云中，您的AEM页面会直接引用它们。
* AEM托管：动态标签管理生成javascript库。 AEM使用工作流模型获取并安装这些库。

实施所使用的托管类型决定了您执行的某些配置和实施任务。 有关托管选项的信息，请参阅动态标 [签管理帮助中的托管](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) -嵌入选项卡。

### 暂存和生产库 {#staging-and-production-library}

确定AEM作者实例是使用动态标签管理暂存还是生产代码。

通常，您的创作实例使用动态标签管理暂存库，而生产实例使用生产库。 此方案允许您使用作者实例测试未批准的动态标签管理配置。

如果需要，您的创作实例可以使用生产库。 Web浏览器插件可用，使您能够在云托管库时，在使用暂存库进行测试之间切换。

### 使用动态标签管理部署挂钩 {#using-the-dynamic-tag-management-deployment-hook}

当AEM托管动态标签管理库时，您可以使用动态标签管理部署挂钩服务自动将库更新推送到AEM。 在对库进行更改（如编辑动态标签管理Web属性时）时，会推送库更新。

要使用部署挂接，动态标签管理必须能够连接到承载库的AEM实例。 您必须 [启用对动态标签管理](/help/sites-administering/dtm.md#enabling-access-for-the-deployment-hook-service) 服务器的AEM访问权限。

在某些情况下，AEM可能无法访问，例如当AEM位于防火墙后时。 在这些情况下，您可以使用AEM轮询导入程序选项定期检索库。 cron作业表达式指示库下载的时间表。

## 启用对部署挂接服务的访问 {#enabling-access-for-the-deployment-hook-service}

启用动态标签管理部署挂钩服务以访问AEM，以便该服务可以更新AEM托管的库。 根据需要指定更新暂存和生产库的动态标签管理服务器的IP地址：

* 暂存: `107.21.99.31`
* 生产： `23.23.225.112` 和 `204.236.240.48`

Perform the configuration using either the [Web Console](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) or a [`sling:OsgiConfig`](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) node:

* 在Web控制台中，使用“配置”页上的“Adobe DTM部署挂接配置”项。
* 对于OSGi配置，服务PID为 `com.adobe.cq.dtm.impl.servlets.DTMDeployHookServlet`。

下表介绍了要配置的属性。

| Web控制台属性 | OSGi属性 | 描述 |
|---|---|---|
| 暂存DTM IP白名单 | `dtm.staging.ip.whitelist` | 用于更新暂存库的动态标签管理服务器的IP地址。 |
| 生产DTM IP白名单 | `dtm.production.ip.whitelist` | 用于更新生产库的动态标签管理服务器的IP地址。 |

## 创建动态标签管理配置 {#creating-the-dynamic-tag-management-configuration}

创建云配置，以便AEM实例可以使用动态标签管理进行身份验证并与您的Web属性交互。

>[!NOTE]
>
>当您的DTM web属性包括Adobe Analytics工具并且您也在使用内容分析时，请避免在您的页面上包含两个Adobe Analytics跟 [踪代码](/help/sites-authoring/content-insights.md)。 在 [Adobe Analytics云配置中](/help/sites-administering/adobeanalytics-connect.md#configuring-the-connection-to-adobe-analytics)，选择“不包括跟踪代码”选项。

### 常规设置 {#general-settings}

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>API令牌</td>
   <td>动态标签管理用户帐户的API令牌属性值。 AEM使用此属性使用动态标签管理进行身份验证。</td>
  </tr>
  <tr>
   <td>公司</td>
   <td>与您的登录ID关联的公司。</td>
  </tr>
  <tr>
   <td>属性</td>
   <td>您为管理AEM站点的标记而创建的Web属性的名称。</td>
  </tr>
  <tr>
   <td>包含有关作者的生产代码</td>
   <td><p>选择此选项可使AEM作者实例和发布实例使用动态标签管理库的生产版本。 </p> <p>如果未选择此选项，则暂存设置将应用于作者实例，生产设置将应用于发布实例。</p> </td>
  </tr>
 </tbody>
</table>

### 自托管属性——暂存和生产 {#self-hosting-properties-staging-and-production}

动态标签管理配置的以下属性使AEM能托管动态标签管理库。 这些属性使AEM能够下载并安装这些库。 或者，您也可以自动更新库，以确保它们反映在动态标签管理应用程序中所做的任何更改。

某些属性使用您从“动态标签管理”Web属性的“嵌入”选项卡的“库下载”部分获得的值。 有关信息，请参 [阅动态标签管理](https://microsite.omniture.com/t2/help/en_US/dtm/#Library_Download) “帮助”中的库下载。

>[!NOTE]
>
>在AEM上承载动态标签管理捆绑包时，必须先在动态标签管理中启用库下载，然后才能创建配置。 此外，必须启用Akamai，因为Akamai提供供下载的库。

在AEM上托管动态标签管理库时，AEM会根据您的配置自动配置Web属性的某些属性。 请参阅下表中的说明。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>使用自托管</td>
   <td>选择在AEM上承载动态标签管理库文件的时间。 选择此选项将显示此表中的其他属性。</td>
  </tr>
  <tr>
   <td>DTM 包 URL</td>
   <td>用于下载动态标签管理库的URL。 从动态标签管理的“库下载”页面的“下载URL”部分获取此值。 出于安全原因，必须手动配置此值。</td>
  </tr>
  <tr>
   <td>下载工作流</td>
   <td><p>用于下载和安装动态标签管理库的工作流模型。 默认型号为“默认DTM Bundle下载”。 除非已创建自定义模型，否则请使用此模型。</p> <p>请注意，默认的下载工作流会在下载库时自动激活它们。</p> </td>
  </tr>
  <tr>
   <td>域提示</td>
   <td><p>（可选）承载动态标签管理库的AEM服务器的域。 指定一个值以覆盖为 <a href="/help/sites-developing/externalizer.md">Day CQ Link Externalizer服务配置的默认域</a>。</p> <p>连接到动态标签管理时，AEM使用此值为动态标签管理Web属性配置“库下载”属性的暂存HTTP路径或生产HTTP路径。</p> </td>
  </tr>
  <tr>
   <td>安全域提示</td>
   <td><p>（可选）通过HTTPS承载动态标签管理库的AEM服务器的域。 指定一个值以覆盖为 <a href="/help/sites-developing/externalizer.md">Day CQ Link Externalizer服务配置的默认域</a>。</p> <p>连接到动态标签管理时，AEM使用此值为动态标签管理Web属性配置“库下载”属性的暂存HTTPS路径或生产HTTPS路径。</p> </td>
  </tr>
  <tr>
   <td>共享密钥</td>
   <td><p>（可选）用于解密下载的共享机密。 从动态标签管理的“库下载”页的“共享机密”字段中获取此值。</p> <p><strong></strong> 注意：必须在安装 <a href="https://www.openssl.org/docs/apps/openssl.html">AEM的计算机上安装OpenSSL</a> 库，这样AEM才能解密下载的库。</p> </td>
  </tr>
  <tr>
   <td>启用轮询导入程序</td>
   <td><p>（可选）选择定期下载并安装动态标签管理库，以确保您使用的是更新版本。 选择后，动态标签管理不会将HTTP POST请求发送到部署挂接URL。</p> <p>AEM会为动态标签管理Web属性自动配置“库下载”属性的“部署挂接URL”属性。 选中后，该属性将配置为无值。 如果未选择，则该属性将配置为动态标签管理配置的URL。</p> <p>当动态标签管理部署挂接无法连接到AEM时（例如，当AEM位于防火墙后时）启用轮询导入程序。</p> </td>
  </tr>
  <tr>
   <td>时间表表达式</td>
   <td>（在选择“启用轮询导入程序”时显示并且为必需。）控制下载动态标签管理库的时间的cron表达式。</td>
  </tr>
 </tbody>
</table>

![chlimage_1-352](assets/chlimage_1-352.png)

### 云托管属性——暂存和生产 {#cloud-hosting-properties-staging-and-production}

在云托管动态标签配置时，您可以为动态标签管理配置配置以下属性。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>使用自托管</td>
   <td>在云中托管动态标签管理库文件时，请清除此选项。</td>
  </tr>
  <tr>
   <td>页眉代码</td>
   <td><p>从主机的动态标签管理中获取的用于暂存的标题代码。 当您连接到动态标签管理时，会自动填充此值。</p> <p> 要在动态标签管理中查看代码，请单击“嵌入”选项卡，然后单击主机名。 展开“标题代码”部分，然后根据需要单击“暂存嵌入代码”或“生产嵌入代码”区域的“复制嵌入代码”。</p> </td>
  </tr>
  <tr>
   <td>页脚代码</td>
   <td><p>用于暂存的页脚代码，该代码是从主机的动态标签管理中获取的。 当您连接到动态标签管理时，会自动填充此值。</p> <p>要在动态标签管理中查看代码，请单击“嵌入”选项卡，然后单击主机名。 展开“页脚代码”部分，然后根据需要单击“暂存嵌入代码”或“生产嵌入代码”区域的“复制嵌入代码”。</p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-353](assets/chlimage_1-353.png)

以下过程使用触屏优化UI配置与动态标签管理的集成。

1. 在边栏上，单击工具>操作>云>云服务。
1. 在“动态标签管理”区域中，将显示以下用于添加配置的链接之一：

   * 如果这是您添加的第一个配置，请单击“立即配置”。
   * 如果已创建一个或多个配置，请单击“显示配置”，然后单击“可用配置”旁边的“+”链接。
   ![chlimage_1-354](assets/chlimage_1-354.png)

1. 键入配置的标题，然后单击创建。
1. 在“API令牌”字段中，输入动态标签管理用户帐户的API令牌属性值。

   要获取API令牌的值，请与DTM客户关怀联系。

   >[!NOTE]
   >
   >在动态标签管理用户明确请求它之前，API令牌不会过期。

   ![chlimage_1-355](assets/chlimage_1-355.png)

1. 单击“连接到DTM”。 AEM使用动态标签管理进行身份验证并检索您的帐户关联的公司列表。
1. 选择公司，然后选择您用来跟踪AEM站点的属性。
1. 如果您正在创作实例上使用分阶段代码，请取消选择“在创作时包括生产代码”。
1. 根据需要，在“暂存设置”选项卡和“生产设置”选项卡上提供属性值，然后单击“确定”。

## 手动下载动态标签管理库 {#manually-downloading-the-dynamic-tag-management-library}

手动下载动态标签管理库以立即在AEM上更新它们。 例如，当您希望在轮询导入程序计划为自动下载库之前测试更新的库时，请手动下载。

1. 在边栏上，单击工具>操作>云>云服务。
1. 在“动态标签管理”区域，单击“显示配置”，然后单击您的配置。
1. 在“暂存设置”区域或“生产设置”区域，单击“触发器下载工作流”按钮以下载和部署库包。

   ![chlimage_1-356](assets/chlimage_1-356.png)

>[!NOTE]
>
>下载的文件存储在下 `/etc/clientlibs/dtm/my config/companyID/propertyID/servertype`。
>
>以下内容直接从您的 [DTM配置中获取](#creating-the-dynamic-tag-management-configuration)。
>
>* `myconfig`
>* `companyID`
>* `propertyID`
>* `servertype`
>



## 将动态标签管理配置与站点关联 {#associating-a-dynamic-tag-management-configuration-with-your-site}

将您的动态标签管理配置与网站的页面相关联，以便AEM将所需的脚本添加到页面。 将站点的根页面与配置关联。 该页面的所有子代都继承关联。 如果需要，您可以覆盖子代页面上的关联。

请按照以下过程将页面和子体与动态标签管理配置相关联。

1. 在经典UI中打开站点的根页面。
1. 使用Sidekick打开页面属性。
1. 在云服务选项卡上，单击添加服务，选择动态标签管理，然后单击确定。

   ![chlimage_1-357](assets/chlimage_1-357.png)

1. 使用动态标签管理下拉菜单选择您的配置，然后单击确定。

请按照以下过程覆盖页面的继承配置关联。 覆盖会影响页面和所有页面的后代。

1. 在经典UI中打开页面。
1. 使用Sidekick打开页面属性。
1. 在“云服务”选项卡上，单击“继承自”属性旁边的挂锁图标，然后在确认对话框中单击“是”。

   ![chlimage_1-358](assets/chlimage_1-358.png)

1. 删除或选择其他动态标签管理配置，然后单击确定。

