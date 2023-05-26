---
title: 集成问题疑难解答
seo-title: Troubleshooting Integration Issues
description: 了解如何解决集成问题。
seo-description: Learn how to troubleshoot integration issues.
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
exl-id: 11b0023e-34bd-4dfe-8173-5466db9fbe34
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 1%

---

# 集成问题疑难解答{#troubleshooting-integration-issues}

## 一般疑难解答提示 {#general-troubleshooting-tips}

### 确保没有JavaScript错误 {#ensure-there-are-no-javascript-errors}

检查浏览器的JavaScript控制台是否显示任何错误。 未处理的错误可能会阻止正确执行后续代码。 如果出现错误，请检查导致错误的脚本以及在哪个区域。 脚本的路径可能会指示脚本所属的功能。

### 在组件级别登录 {#logging-on-component-level}

在某些情况下，在组件级别添加其他语句可能会有帮助。 由于组件已呈现，因此您可以添加临时标记以显示变量值，这可以帮助您识别潜在问题。 例如：

```
<%
log.info("myVariable={}", myVariable);
%>

<!--
<%= myJspVariable %>
-->

<!--
${ myHtlVariable }
-->
```

有关日志记录的其他详细信息，请参见 [日志记录](/help/sites-deploying/configure-logging.md) 和 [使用审计记录和日志文件](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 页数。

## Analytics集成问题 {#analytics-integration-issues}

### 报告导入程序会导致CPU/内存使用率过高 {#the-report-importer-causes-high-cpu-memory-usage}

报告导入器导致CPU/内存使用率高或导致 `OutOfMemoryError` 例外。

#### 解决方案 {#solution}

要解决此问题，您可以尝试以下操作：

* 确保没有注册大量PollingImporters（请参阅下面的“由于PollingImporter而关闭需要很长时间”部分）。
* 对使用CRON表达式在一天中的某个时间运行报表导入程序 `ManagedPollingImporter` 中的配置 [OSGi控制台](/help/sites-deploying/configuring-osgi.md).

有关在AEM中创建自定义数据导入器服务的其他详细信息，请参阅以下文章 [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### 由于PollingImporter，关闭需要很长时间 {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics在设计时考虑了继承机制。 通常，您通过在页面属性中添加对Analytics配置的引用来启用网站的Analytics [Cloud Services](/help/sites-developing/extending-cloud-config.md) 选项卡。 然后，配置会自动继承到所有子页面，而无需再次引用它，除非页面需要其他配置。 添加对站点的引用也会自动创建该类型的多个节点(12个用于AEM 6.3及更早版本，6个用于AEM 6.4及更高版本) `cq;PollConfig` 实例化用于将Analytics数据导入AEM的PollingImporters。 因此：

* 具有引用Analytics的大量页面会导致大量轮询导入程序。
* 此外，复制和粘贴引用Analytics配置的页面会导致其PollingImporters重复。

#### 解决方案 {#solution-1}

首先，分析 [error.log](/help/sites-deploying/configure-logging.md) 可让您深入了解活动或注册轮询导入程序的数量。 例如：

```
# Count PollingImporter entries
$ sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\),interval.*/\1/p" error.log | wc -l
86415
# Count PollingImporter entries for last30days
$ sed -n "s/.*(aem-analytics-integration-last30Days).*target=\(.*\),interval.*/\1/p" error.log | wc -l
14531
# Count unique paths of PollingImporter registrations
sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\)\/jcr:content.*/\1/p" error.log | sort | uniq -c
28115
```

其次，确保仅顶级页面（层次结构中的较高位置）引用了Analytics配置。

有关在AEM中创建自定义数据导入器服务的其他详细信息，请参阅以下文章 [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## DTM（旧版）问题 {#dtm-legacy-issues}

### DTM脚本标记未在页面源中渲染 {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

此 [DTM](/help/sites-administering/dtm.md) 脚本标记未正确包含在页面中，即使已在页面属性中引用了该配置 [Cloud Services](/help/sites-developing/extending-cloud-config.md) 选项卡。

#### 解决方案 {#solution-2}

要解决此问题，您可以尝试以下操作：

* 确保加密的属性可以解密(请注意，加密可能在每个AEM实例上使用不同的自动生成密钥)。 有关其他详细信息，另请参阅 [对配置属性的加密支持](/help/sites-administering/encryption-support-for-configuration-properties.md).
* 重新发布在中找到的配置 `/etc/cloudservices/dynamictagmanagement`
* 检查ACL `/etc/cloudservices`. ACL应为：

   * 允许； jcr：read； webservice-support-servicelibfinder
   * 允许； jcr：read；每个人； rep:glob:&amp;ast；/defaults/&amp;ast；
   * 允许； jcr：read；每个人； rep:glob:&amp;ast；/defaults
   * 允许； jcr：read；每个人； rep:glob:&amp;ast；/public/&amp;ast；
   * 允许； jcr：read；每个人； rep:glob:&amp;ast；/public

有关管理ACL的详细信息，请阅读 [用户管理和安全性](/help/sites-administering/security.md#permissions-in-aem) 页面。

## Target集成问题 {#target-integration-issues}

### 使用自定义页面组件时，目标内容在预览模式下不可见 {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

出现此问题的原因是，自定义页面组件不包含处理Target DTM集成的正确JSP或客户端库。

#### 解决方案 {#solution-3}

您可以尝试以下解决方案：

* 确保自定义 `headlibs.jsp` （如果有） `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`)包括以下各项：

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* 确保自定义 `head.html` （如果有） `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **不会** 选择性地包括特定的集成头库，如下例所示：

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

此 `servicelibs.jsp` 添加所需的Analytics JavaScript对象，并加载与网站关联的云服务库。 对于Target服务，库是通过 `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

加载的库集取决于目标客户端库的类型( `mbox.js` 或 `at.js`)在Target配置上使用。

使用DTM进行投放时 `mbox.js` 或 `at.js` 确保在呈现内容之前加载库。 使用异步加载这些库的Tag Management Systems可能会导致执行特定于Target的JavaScript代码时出现问题。

欲了解更多信息，请阅读 [针对目标内容进行开发](/help/sites-developing/target.md#understanding-the-target-component) 页面。

### 浏览器控制台中会显示错误“AppMeasurement初始化中缺少报表包ID” {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

当使用DTM在网站上实施Adobe Analytics并使用自定义代码时，可能会出现此问题。 原因是使用 `s = new AppMeasurement()` 实例化 `s` 对象。

#### 解决方案 {#solution-4}

使用 `s_gi` 而不是 `new AppMeasurement` 实例化方法。 例如：

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### 默认选件是随机显示的，而不是正确选件 {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

此问题可能由多种原因引起：

* 正在加载Target客户端库( `mbox.js` 或 `at.js`)异步使用第三方Tag Management Systems可能会随机中断定位。 Target库应在页面标头中同步加载。 当库从AEM交付时，此情况始终为true。

* 正在加载两个Target客户端库( `at.js`)同时(例如，一个使用DTM，另一个使用AEM中的Target配置)。 这可能会导致 `adobe.target` 定义，如果 `at.js` 版本不同。

#### 解决方案 {#solution-5}

您可以尝试以下解决方案：

* 确保在中同步执行加载类似DTM的库的客户代码（进而加载Target库） [页头](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* 如果将站点配置为使用DTM来交付Target库，请确保 **DTM提供的Clientlib** 选项已勾选 [Target配置](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) 用于该站点。

### 使用AT.js 1.3+时，始终显示默认选件，而不是正确选件 {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

开箱即用的AEM 6.2和6.3与AT.js版本1.3.0+不兼容。 利用AT.js版本1.3.0，引入了对其API进行参数验证的功能， `adobe.target.applyOffer()` 需要“mbox”参数，但该参数未由 `atjs-itegration.js` 代码。

#### 解决方案 {#solution-6}

要解决此问题，请编辑 `atjs-itegration.js` 并添加 `"mbox": mboxName` 参数对象中的字段 `adobe.target.applyOffer()` 如下所示：

```
adobe.target.getOffer({
    "mbox": mboxName,
    "params": params,
    "success": function (response) {
        adobe.target.applyOffer({
            "mbox": mboxName, //<--- ADDED PARAM
            "selector": "#" + mboxName,
            "offer": response
        })
    },
```

### “目标和设置”页面不显示“报表源”部分 {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

此问题很可能是 [A4T Analytics Cloud配置](/help/sites-administering/target-configuring.md) 配置问题。

#### 解决方案 {#solution-7}

您需要通过向AEM发出以下验证请求来验证是否已为Target帐户正确启用A4T：

```
http://localhost:4502/etc/cloudservices/testandtarget/<YOUR-CONFIG>/jcr:content.a4t.json

{
    "a4tEnabled": true,
    "sharedsecret": "SECRET",
    "proxyUrl": "/libs/cq/contentinsight/content/proxy.reportingservices.json",
    "active": "true",
    "pageName": "",
    "url": "https://api5.omniture.com/rs/0.5/",
    "username": "USER@DOMAIN"
}
```

如果响应包含行 `a4tEnabled:false`，contact [Adobe客户关怀](https://helpx.adobe.com/contact.html) 以正确配置您的帐户。

### 有用的Target API {#helpful-target-apis}

下面提供了两个Target API，它们在解决Target问题时可能会很有用：

* 检索给定clientcode的Target端点

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* 检索客户机的配置文件

```
https://admin<N>.testandtarget.omniture.com/admin/rest/v1/clients/<CLIENT>?email=<EMAIL>&password=<PASSWORD>

Response for N=4, CLIENT-dayintegrationintern
{
    "clientCode": "dayintegrationintern",
    "companyName": "Day Integration - Internal",
    "omnitureCompanyId": "Day Integration Internal",
    "softTraxId": -1,
    "address1": "XYZ",
    "city": "San Francisco",
    "state": "ca",
    "zip": "94107",
    "country": "UNITED STATES",
    "locale": "de_DE",
    "timeZone": "Europe/Berlin",
    "phone": "XX-XX-XXXX",
    "serviceLevel": "Up to 100,000",
    "privileges": [
        "a4t",
        "hosts",
        "TnT-SC-integration",
        "mvt",
        "steps",
        "testing-campaigns",
        "view-snapshot",
        "on-site-editor",
        "optimizing-campaign",
        "third-party-id-support",
        "landing-page-campaigns",
        "segment",
        "rest-create-user",
        "advanced-targeting",
        "mobile-device-targeting",
        "beta",
        "geolocation"
    ]
}
```
