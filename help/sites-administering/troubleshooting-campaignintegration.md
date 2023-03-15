---
title: Adobe Campaign集成故障诊断
seo-title: Troubleshooting your Adobe Campaign Integration
description: 了解如何对Adobe Campaign集成问题进行故障诊断。
seo-description: Learn how to troubleshoot issues with the Adobe Campaign Integration.
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# Adobe Campaign集成故障诊断{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>本页适用于Campaign Classic。

以下故障诊断提示有助于解决在将AEM与Adobe Campaign集成时可能遇到的最常见问题：

## 一般疑难解答提示 {#general-troubleshooting-tips}

对于这两种集成，您可以检查是否发送了HTTP调用(AEM > Adobe Campaign、Adobe Campaign > AEM)：

* 当集成失败时，请确保这些调用到达另一端（以避免防火墙/SSL问题）。
* 对于AEM功能，您将看到从AEM创作界面请求了json调用；这些调用不应导致HTTP-500错误。 如果您看到HTTP-500错误，请检查 `error.log` 了解更多相关信息。
* 提高AEM中促销活动类的调试级别还有助于排除问题。

## 如果连接失败 {#if-the-connection-fails}

检查您是否已配置 **aemserver** Adobe Campaign运算符。

## 如果图像未显示在Adobe Campaign控制台中 {#if-images-do-not-appear-in-the-adobe-campaign-console}

检查HTML源并验证是否可以从客户端计算机中打开URL。 如果URL中包含localhost：4503，则更改创作实例上Day CQ Link Externalizer的配置以指向可从Adobe Campaign控制台计算机访问的发布实例。

参见 [配置外部化器。](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## 如果无法从AEM连接到Adobe Campaign {#if-you-cannot-connect-from-aem-to-adobe-campaign}

在Adobe Campaign中查找以下错误消息：

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

要解决此问题，请将以下内容更改为 **$CAMPAIGN_HOME/conf/config-&lt;instance-name>.xml**：

`<dataStore hosts="*" lang="en_GB">`

## 如果Adobe Campaign对话框中未显示任何数据 {#if-no-data-displays-in-the-adobe-campaign-dialog}

在Adobe Campaign中，请确保端口号后面没有尾随斜杠(/)。

![chlimage_1-149](assets/chlimage_1-149.png)

## 如果您收到有关设置区域设置的警告 {#if-you-get-a-warning-about-your-setlocale}

如果您正在启动Apache HTTPD服务并看到错误 `"Warning: setlocale: LC_CTYPE cannot change locale"` 确保您拥有 **en_CA.ISO-8859-15区域设置** 安装在系统上。

您可以使用检查是否已安装它 `local -a`. 如果未安装，您可以进行修补 **/usr/local/neolane/nl6/env.sh** 脚本并将区域设置更改为已安装的区域设置。

## 编译脚本&#39;get_nms_amcGetSeedMetaData_jssp&#39;时出错 {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

如果您在AEM日志文件中看到以下错误消息：

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

使用以下解决方法：

1. 打开文件 **$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. 修改方法“amcGetSeedMetaData”的第467行
1. 更改 `label : [inclView.@label](mailto:inclView.@label)` 到 `label : String([inclView.@label](mailto:inclView.@label))`

1. 保存.
1. 重新启动服务器。

## 如果Adobe Campaign在单击“同步”按钮时显示错误 {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

如果在单击 **同步** Adobe Campaign Classic按钮时，您会看到以下错误：

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

要解决此问题，请确保可从计算机访问在外部帐户中配置的AEM连接URL。

切换来源 **localhost** IP地址解决了此问题。

## 如果您收到“无法解析XTK日期+时间”错误 {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

单击“同步”后，您会收到一个错误，指出页面上出现脚本：无法解析XTK日期+时间“未定义”：不是有效的XTK值。

如果AEM实例上仍有过时的Adobe Campaign信息，则会发生这种情况。 通过删除AEM上的所有Campaign集成配置并重建它们来解决此问题。 然后，创建一个新模板。

## 如果与SSL的连接在设置云服务时显示错误 {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

在AEM的error.log中，如果您看到以下内容：

```xml
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

请向Adobe Campaign支持团队提交票证。

## 如果在同步对话框中看到http而不是预期的https链接 {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

进行以下设置：

* 使用https托管Adobe Campaign以与AEM作者进行通信
* 反向代理终止SSL
* 内部部署AEM创作实例

尝试同步Adobe Campaign投放中的内容时，AEM会返回新闻稿列表。 但是，列表中新闻稿的url是http地址。 选择列表中的项目之一时出现错误。

要解决此问题：

* 需要将Dispatcher或反向代理配置为将原始协议作为标头传递。
* 此 *Apache Felix Http服务SSL过滤器* 在OSGi配置中([https://&lt;host>：&lt;port>/system/console/configMgr](http://localhost:4502/system/console/configMgr))需要配置为各自的标头设置。 参见 [https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## 如果无法在页面属性中选择我创建的自定义模板 {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

为Adobe Campaign创建邮件模板时，必须包含资产 **acMapping** 具有值 **mapRecipient** 在 **jcr：content** 节点，否则您将无法在中选择Adobe Campaign模板 **页面属性** AEM （字段已禁用）。

## 如果您在日志中收到错误“com.day.cq.mcm.campaign.servlets.util.ParameterMapper” {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

使用自定义模板时，日志中会显示“com.day.cq.mcm.campaign.servlets.util.ParameterMapper”错误。 在此情况下，请务必从以下位置安装Featurepack 6576： [包共享](/help/sites-administering/package-manager.md#package-share). 如果将acMapping属性设置为recipient.firstName以外的值，则会在Adobe Campaign Manager端创建一个空白值，出现此问题。
