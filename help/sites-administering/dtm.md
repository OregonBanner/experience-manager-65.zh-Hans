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
exl-id: 1e0821f5-627f-4262-ba76-62303890e112
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2222'
ht-degree: 1%

---

# 与Adobe动态标签管理集成{#integrating-with-adobe-dynamic-tag-management}

将[Adobe动态标签管理](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html)与AEM集成，以便您可以使用动态标签管理Web属性来跟踪AEM网站。 动态标签管理使营销人员能够管理用于收集数据的标签，并跨数字营销系统分发数据。 例如，使用动态标签管理收集AEM网站的使用情况数据，并在Adobe Analytics或Adobe Target中分发数据以进行分析。

在集成之前，您需要创建跟踪AEM网站域的Dynamic Tag Management [Web属性](https://microsite.omniture.com/t2/help/en_US/dtm/#Web_Properties)。 必须配置Web属性的[托管选项](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab)，以便您能够配置AEM以访问动态标签管理库。

配置集成后，对动态标签管理部署工具和规则所做的更改不会要求您更改AEM中的动态标签管理配置。 更改将自动可供AEM使用。

>[!NOTE]
>
>如果您使用的是具有自定义代理配置的DTM，则需要配置两个HTTP客户端代理配置，因为AEM的某些功能使用3.x API，而其他一些功能使用4.x API:
>
>* 3.x配置了[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x配置了[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



## 部署选项{#deployment-options}

以下部署选项会影响与动态标签管理集成的配置。

### Dynamic Tag Management托管{#dynamic-tag-management-hosting}

AEM支持在云中托管或在AEM上托管的动态标签管理。

* 云托管：动态标签管理Javascript库存储在云中，您的AEM页面会直接引用它们。
* AEM托管：动态标签管理会生成Javascript库。 AEM使用工作流模型获取并安装库。

您的实施所使用的托管类型决定了您执行的某些配置和实施任务。 有关托管选项的信息，请参阅“动态标签管理帮助”中的[托管 — 嵌入选项卡](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) 。

### 暂存和生产库{#staging-and-production-library}

确定您的AEM创作实例是使用Dynamic Tag Management暂存代码还是生产代码。

通常，您的创作实例使用动态标签管理暂存库，而生产实例使用生产库。 此方案允许您使用创作实例来测试未批准的动态标签管理配置。

如果需要，您的创作实例可以使用生产库。 提供了Web浏览器插件，在云托管库时，这些插件允许您在使用暂存库进行测试时进行切换。

### 使用Dynamic Tag Management部署挂接{#using-the-dynamic-tag-management-deployment-hook}

当AEM托管Dynamic Tag Management库时，您可以使用Dynamic Tag Management部署挂接服务自动将库更新推送到AEM。 当对库进行更改（例如，编辑Dynamic Tag Management Web属性属性时）时，会推送库更新。

要使用部署挂接，动态标签管理必须能够连接到托管库的AEM实例。 您必须[启用对动态标签管理服务器的AEM](/help/sites-administering/dtm.md#enabling-access-for-the-deployment-hook-service)的访问权限。

在某些情况下，AEM可能不可访问，例如当AEM位于防火墙后面时。 在这些情况下，您可以使用AEM轮询导入器选项定期检索库。 cron作业表达式指示库下载的计划。

## 启用部署挂接服务{#enabling-access-for-the-deployment-hook-service}的访问

启用Dynamic Tag Management部署挂接服务以访问AEM，以便该服务可以更新AEM托管的库。 根据需要指定更新暂存和生产库的动态标签管理服务器的IP地址：

* 暂存: `107.21.99.31`
* 生产：`23.23.225.112`和`204.236.240.48`

使用[Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或[`sling:OsgiConfig`](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)节点执行配置：

* 在Web控制台中，使用“配置”页面上的AdobeDTM部署挂接配置项。
* 对于OSGi配置，服务PID为`com.adobe.cq.dtm.impl.servlets.DTMDeployHookServlet`。

下表介绍了要配置的属性。

| Web控制台属性 | OSGi属性 | 描述 |
|---|---|---|
| 暂存DTM IP白名单 | `dtm.staging.ip.whitelist` | 用于更新暂存库的动态标签管理服务器的IP地址。 |
| 生产DTM IP白名单 | `dtm.production.ip.whitelist` | 更新生产库的动态标签管理服务器的IP地址。 |

## 创建动态标签管理配置{#creating-the-dynamic-tag-management-configuration}

创建云配置，以便AEM实例可以使用动态标签管理进行身份验证并与您的Web资产进行交互。

>[!NOTE]
>
>当您的DTM Web属性包含Adobe Analytics工具并且您还在使用[内容分析](/help/sites-authoring/content-insights.md)时，请避免在您的页面上包含两个Adobe Analytics跟踪代码。 在[Adobe Analytics云配置](/help/sites-administering/adobeanalytics-connect.md#configuring-the-connection-to-adobe-analytics)中，选择不包含跟踪代码选项。

### 常规设置 {#general-settings}

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>API令牌</td>
   <td>您的Dynamic Tag Management用户帐户的API令牌属性值。 AEM使用此属性通过动态标签管理进行身份验证。</td>
  </tr>
  <tr>
   <td>公司</td>
   <td>与您的登录ID关联的公司。</td>
  </tr>
  <tr>
   <td>属性</td>
   <td>您为管理AEM网站的标记而创建的Web属性的名称。</td>
  </tr>
  <tr>
   <td>包含有关作者的生产代码</td>
   <td><p>选择此选项可使AEM创作和发布实例使用动态标签管理库的生产版本。 </p> <p>未选择此选项时，暂存设置将应用于创作实例，生产设置将应用于发布实例。</p> </td>
  </tr>
 </tbody>
</table>

### 自托管属性 — 暂存和生产{#self-hosting-properties-staging-and-production}

动态标签管理配置的以下属性使AEM能够托管动态标签管理库。 通过这些属性，AEM可以下载和安装库。 或者，您也可以自动更新库，以确保库反映动态标签管理应用程序中所做的任何更改。

某些资产会使用您从“嵌入”选项卡的“库下载”部分中为Dynamic Tag Management Web资产获取的值。 有关信息，请参阅Dynamic Tag Management帮助中的[库下载](https://microsite.omniture.com/t2/help/en_US/dtm/#Library_Download) 。

>[!NOTE]
>
>在AEM上托管动态标签管理包时，必须先在动态标签管理中启用库下载，然后才能创建配置。 此外，必须启用Akamai，因为Akamai提供了供下载的库。

在AEM上托管动态标签管理库时，AEM会根据您的配置自动配置Web属性的某些属性。 请参阅下表中的描述。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>使用自托管</td>
   <td>选择在AEM上托管动态标签管理库文件的时间。 选择此选项将导致此表中显示其他属性。</td>
  </tr>
  <tr>
   <td>DTM 包 URL</td>
   <td>用于下载动态标签管理库的URL。 从Dynamic Tag Management的库下载页面的下载URL部分获取此值。 出于安全考虑，必须手动配置此值。</td>
  </tr>
  <tr>
   <td>下载工作流</td>
   <td><p>用于下载和安装动态标签管理库的工作流模型。 默认模型为“默认DTM包下载”。 除非已创建自定义模型，否则使用此模型。</p> <p>请注意，默认的下载工作流会在下载库时自动激活它们。</p> </td>
  </tr>
  <tr>
   <td>域提示</td>
   <td><p>（可选）托管动态标签管理库的AEM服务器的域。 指定一个值，以覆盖为<a href="/help/sites-developing/externalizer.md">Day CQ Link Externalizer服务</a>配置的默认域。</p> <p>连接到Dynamic Tag Management时，AEM会使用此值为Dynamic Tag Management Web属性配置库下载属性的暂存HTTP路径或生产HTTP路径。</p> </td>
  </tr>
  <tr>
   <td>安全域提示</td>
   <td><p>（可选）通过HTTPS托管动态标签管理库的AEM服务器的域。 指定一个值，以覆盖为<a href="/help/sites-developing/externalizer.md">Day CQ Link Externalizer服务</a>配置的默认域。</p> <p>连接到Dynamic Tag Management时，AEM会使用此值为Dynamic Tag Management Web属性配置库下载属性的暂存HTTPS路径或生产HTTPS路径。</p> </td>
  </tr>
  <tr>
   <td>共享密钥</td>
   <td><p>（可选）用于解密下载的共享密钥。 从Dynamic Tag Management的库下载页面的共享密钥字段中获取此值。</p> <p><strong>注意：</strong> 您必须在安装 <a href="https://www.openssl.org/docs/apps/openssl.html"></a> AEM的计算机上安装OpenSSL库，以便AEM能够解密下载的库。</p> </td>
  </tr>
  <tr>
   <td>启用轮询导入程序</td>
   <td><p>（可选）选择以定期下载和安装动态标签管理库，以确保您使用的是更新版本。 选择此选项后，动态标签管理不会向部署挂接URL发送HTTPPOST请求。</p> <p>AEM会为Dynamic Tag Management web属性自动配置“库下载”属性的“部署挂接URL”属性。 选择后，将配置属性，但没有值。 如果未选择，则会使用您的动态标签管理配置的URL来配置属性。</p> <p>当动态标签管理部署挂接无法连接到AEM时(例如，当AEM位于防火墙后时)启用轮询导入程序。</p> </td>
  </tr>
  <tr>
   <td>时间表表达式</td>
   <td>（选中“启用轮询导入器”时，显示并且是必需的。） 可控制下载动态标签管理库的时间的CRON表达式。</td>
  </tr>
 </tbody>
</table>

![chlimage_1-352](assets/chlimage_1-352.png)

### 云托管属性 — 暂存和生产{#cloud-hosting-properties-staging-and-production}

在云托管动态标签配置时，您可以为动态标签管理配置配置配置以下属性。

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
   <td><p>从主机的Dynamic Tag Management中获取的用于暂存的标头代码。 此值在您连接到动态标签管理时自动填充。</p> <p> 要在动态标签管理中查看代码，请单击“嵌入”选项卡，然后单击主机名。 展开页眉代码部分，然后根据需要单击暂存嵌入代码或生产嵌入代码区域的复制嵌入代码。</p> </td>
  </tr>
  <tr>
   <td>页脚代码</td>
   <td><p>用于暂存的页脚代码，该代码是从主机的Dynamic Tag Management中获取的。 此值在您连接到动态标签管理时自动填充。</p> <p>要在动态标签管理中查看代码，请单击“嵌入”选项卡，然后单击主机名。 展开页脚代码部分，然后根据需要单击暂存嵌入代码或生产嵌入代码区域的复制嵌入代码。</p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-353](assets/chlimage_1-353.png)

以下过程使用触屏优化UI配置与动态标签管理的集成。

1. 在边栏中，单击工具>操作>云>Cloud Services。
1. 在“动态标签管理”区域中，将显示用于添加配置的以下链接之一：

   * 如果这是您添加的第一个配置，请单击立即配置。
   * 如果已创建一个或多个配置，请单击显示配置，然后单击可用配置旁边的+链接。

   ![chlimage_1-354](assets/chlimage_1-354.png)

1. 键入配置的标题，然后单击创建。
1. 在API令牌字段中，输入Dynamic Tag Management用户帐户的API令牌属性值。

   要获取API令牌的值，请联系DTM客户关怀团队。

   >[!NOTE]
   >
   >在Dynamic Tag Management用户明确请求API令牌之前，该API令牌不会过期。

   ![chlimage_1-355](assets/chlimage_1-355.png)

1. 单击连接到DTM。 AEM通过动态标签管理进行身份验证，并检索您的帐户关联的公司列表。
1. 选择公司，然后选择用于跟踪AEM网站的资产。
1. 如果在创作实例中使用暂存代码，请取消选择“在创作时包含生产代码”。
1. 根据需要，在“暂存设置”选项卡和“生产设置”选项卡中提供属性值，然后单击“确定”。

## 手动下载动态标签管理库{#manually-downloading-the-dynamic-tag-management-library}

手动下载动态标签管理库，以便在AEM上立即更新它们。 例如，当要在轮询导入程序计划自动下载库之前测试更新的库时，请手动下载。

1. 在边栏中，单击工具>操作>云>Cloud Services。
1. 在“动态标签管理”区域，单击显示配置，然后单击您的配置。
1. 在“暂存设置”区域或“生产设置”区域中，单击“触发器下载工作流”按钮以下载和部署库包。

   ![chlimage_1-356](assets/chlimage_1-356.png)

>[!NOTE]
>
>下载的文件存储在`/etc/clientlibs/dtm/my config/companyID/propertyID/servertype`下。
>
>以下内容直接从您的[DTM配置](#creating-the-dynamic-tag-management-configuration)中获取。
>
>* `myconfig`
>* `companyID`
>* `propertyID`
>* `servertype`

>



## 将动态标签管理配置与您的网站{#associating-a-dynamic-tag-management-configuration-with-your-site}关联

将您的动态标签管理配置与网站的页面相关联，以便AEM将所需的脚本添加到页面。 将站点的根页面与配置关联。 该页面的所有子项都将继承关联。 如果需要，您可以覆盖子页面上的关联。

请按照以下过程将页面和子体与动态标签管理配置相关联。

1. 在经典UI中打开站点的根页面。
1. 使用Sidekick打开页面属性。
1. 在“Cloud Services”选项卡上，单击添加服务，选择“动态标签管理”，然后单击确定。

   ![chlimage_1-357](assets/chlimage_1-357.png)

1. 使用动态标签管理下拉菜单选择您的配置，然后单击确定。

请按照以下过程覆盖页面的继承配置关联。 覆盖会影响页面和所有页面后代。

1. 在经典UI中打开页面。
1. 使用Sidekick打开页面属性。
1. 在“Cloud Services”选项卡上，单击“继承自”属性旁边的挂锁图标，然后在确认对话框中单击“是”。

   ![chlimage_1-358](assets/chlimage_1-358.png)

1. 删除或选择其他动态标签管理配置，然后单击确定。
