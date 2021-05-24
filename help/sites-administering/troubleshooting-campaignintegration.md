---
title: Adobe Campaign集成故障诊断
seo-title: Adobe Campaign集成故障诊断
description: 了解如何对Adobe Campaign集成问题进行故障诊断。
seo-description: 了解如何对Adobe Campaign集成问题进行故障诊断。
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# Adobe Campaign集成疑难解答{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>此页面适用于Campaign Classic。

以下故障诊断提示可帮助解决在将AEM与Adobe Campaign集成时可能遇到的最常见问题：

## 一般故障诊断提示{#general-troubleshooting-tips}

对于这两个集成，您可以检查是否发送了HTTP调用(AEM > Adobe Campaign、Adobe Campaign > AEM):

* 集成失败时，请确保这些调用到达另一端（以避免防火墙/SSL问题）。
* 对于AEM功能，您将看到从AEM创作界面请求json调用；这不应导致HTTP-500错误。 如果看到HTTP-500错误，请检查`error.log`以获取有关此内容的详细信息。
* 提高AEM中促销活动类的调试级别也有助于对问题进行故障诊断。

## 如果连接失败{#if-the-connection-fails}

检查您是否已在Adobe Campaign中配置了&#x200B;**aemserver**&#x200B;运算符。

## 如果图像未显示在Adobe Campaign控制台{#if-images-do-not-appear-in-the-adobe-campaign-console}中

检查HTML源并验证是否可以从客户端计算机打开该URL。 如果URL中包含localhost:4503，请更改创作实例上Day CQ Link Externalizer的配置，以指向可从Adobe Campaign控制台计算机访问的发布实例。

请参阅[配置外部器。](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## 如果无法从AEM连接到Adobe Campaign {#if-you-cannot-connect-from-aem-to-adobe-campaign}

在Adobe Campaign中查找以下错误消息：

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

要修复此问题，请在&#x200B;**$CAMPAIGN_HOME/conf/config-&lt;instance-name>.xml**&#x200B;中更改以下内容：

`<dataStore hosts="*" lang="en_GB">`

## 如果Adobe Campaign对话框{#if-no-data-displays-in-the-adobe-campaign-dialog}中未显示任何数据

在Adobe Campaign中，确保端口号后面没有尾随斜杠(/)。

![chlimage_1-149](assets/chlimage_1-149.png)

## 如果收到有关设置区域设置{#if-you-get-a-warning-about-your-setlocale}的警告

如果启动Apache HTTPD服务并看到错误`"Warning: setlocale: LC_CTYPE cannot change locale"`，请确保系统上已安装&#x200B;**en_CA.ISO-8859-15区域设置**。

您可以使用`local -a`检查是否安装了它。 如果未安装，则可以修补&#x200B;**/usr/local/neolane/nl6/env.sh**&#x200B;脚本，并将区域设置更改为已安装的脚本。

## 如果编译脚本“get_nms_amcGetSeedMetaData_jssp”时出错{#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

如果您在AEM日志文件中看到以下错误消息：

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

请使用以下解决方法：

1. 打开文件&#x200B;**$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. 修改“amcGetSeedMetaData”方法的467行
1. 将`label : [inclView.@label](mailto:inclView.@label)`更改为`label : String([inclView.@label](mailto:inclView.@label))`

1. 保存.
1. 重新启动服务器。

## 如果Adobe Campaign在单击同步按钮{#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}时显示错误

如果在Adobe Campaign Classic中单击&#x200B;**Synchronize**&#x200B;按钮，则会看到以下错误：

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

要解决此问题，请确保可从计算机访问在外部帐户中配置的AEM connection-url。

从&#x200B;**localhost**&#x200B;切换到IP地址的交换机解决了此问题。

## 如果收到“无法解析XTK Date+Time &#39;undefined&#39;”错误{#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

单击同步后，您会收到一个错误，指出页面上已发生脚本：无法解析XTK Date+Time &#39;undefined&#39;:不是有效的XTK值。

如果AEM实例上仍存在过时的Adobe Campaign信息，则会发生这种情况。 通过删除AEM上的所有促销活动集成配置并重建它们，可解决此问题。 然后，创建新模板。

## 如果在设置云服务{#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}时与SSL的连接显示错误

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

请向Adobe Campaign支持团队提票。

## 如果在同步对话框{#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}中看到http而不是预期的https链接

使用以下设置：

* 托管的Adobe Campaign，使用https与AEM作者通信
* 反向代理终止SSL
* 内部部署AEM创作实例

尝试同步Adobe Campaign交付中的内容时，AEM会返回新闻稿列表。 但是，列表中新闻稿的url是http地址。 选择列表中的某个项目时，会出错。

要解决此问题，请执行以下操作：

* 调度程序或反向代理需要配置为将原始协议作为标头进行传递。
* OSGi配置([https://&lt;host>:&lt;port>/system/console/configMgr](http://localhost:4502/system/console/configMgr))中的&#x200B;*Apache Felix Http服务SSL筛选器*&#x200B;需要将配置为相应的标头设置。 请参阅[https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## 如果在页面属性{#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}中无法选择我创建的自定义模板

为Adobe Campaign创建邮件模板时，必须在模板的&#x200B;**jcr:content**&#x200B;节点中包含值为&#x200B;**mapRecipient**&#x200B;的属性&#x200B;**，否则将无法在AEM的**&#x200B;页面属性&#x200B;**中选择Adobe Campaign模板（字段处于禁用状态）。**

## 如果在日志{#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}中收到错误“com.day.cq.mcm.campaign.servlets.util.ParameterMapper”

使用自定义模板时，日志中会显示错误“com.day.cq.mcm.campaign.servlets.util.ParameterMapper”。 在此事件中，请务必从[Package Share](/help/sites-administering/package-manager.md#package-share)安装Featurepack 6576。 这是一个问题，如果将acMapping属性设置为recipient.firstName以外的值，则会在Adobe Campaign管理器端创建空值。
