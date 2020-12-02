---
title: Adobe Campaign集成疑难解答
seo-title: Adobe Campaign集成疑难解答
description: 了解如何解决Adobe Campaign集成问题。
seo-description: 了解如何解决Adobe Campaign集成问题。
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---


# Adobe Campaign集成疑难解答{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>本页适用于Campaign Classic。

以下故障排除提示有助于解决在将AEM与Adobe Campaign集成时可能遇到的最常见问题：

## 一般疑难解答提示{#general-troubleshooting-tips}

对于这两种集成，您可以检查是否发送HTTP调用(AEM >Adobe Campaign、Adobe Campaign>AEM):

* 当集成失败时，请确保这些调用到达另一端（以避免防火墙/SSL问题）。
* 对于AEM功能，您将看到从AEM作者界面请求json调用；这不应导致HTTP-500错误。 如果您看到HTTP-500错误，请检查`error.log`以了解有关该错误的详细信息。
* 提高AEM中活动类的调试级别还有助于解决问题。

## 如果连接失败{#if-the-connection-fails}

检查您是否已在Adobe Campaign中配置了&#x200B;**aemserver**&#x200B;运算符。

## 如果图像未出现在Adobe Campaign控制台{#if-images-do-not-appear-in-the-adobe-campaign-console}中

检查HTML源并验证是否可以从客户端计算机打开URL。 如果URL中包含localhost:4503，则更改创作实例上Day CQ Link Externalizer的配置，以指向可从Adobe Campaign控制台计算机访问的发布实例。

请参阅[配置Externalizer。](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## 如果无法从AEM连接到Adobe Campaign{#if-you-cannot-connect-from-aem-to-adobe-campaign}

在Adobe Campaign中查找以下错误消息：

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

要解决此问题，请在&#x200B;**$活动_HOME/conf/config-&lt;instance-name>.xml**&#x200B;中更改以下内容：

`<dataStore hosts="*" lang="en_GB">`

## 如果Adobe Campaign对话框{#if-no-data-displays-in-the-adobe-campaign-dialog}中未显示数据

在Adobe Campaign中，确保端口号后没有尾随斜杠(/)。

![chlimage_1-149](assets/chlimage_1-149.png)

## 如果您收到有关setlocale {#if-you-get-a-warning-about-your-setlocale}的警告

如果您正在启动Apache HTTPD服务并看到错误`"Warning: setlocale: LC_CTYPE cannot change locale"`，请确保您的系统已安装&#x200B;**en_CA.ISO-8859-15区域设置**。

可以使用`local -a`检查是否已安装。 如果未安装，您可以修补&#x200B;**/usr/local/neolane/nl6/env.sh**&#x200B;脚本并将区域设置更改为已安装的脚本。

## 如果编译脚本“get_nms_amcGetSeedMetaData_jssp”时收到错误{#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

如果您在AEM日志文件中看到以下错误消息：

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

使用以下解决方法：

1. 打开文件&#x200B;**$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. 修改“amcGetSeedMetaData”方法的第467行
1. 将`label : [inclView.@label](mailto:inclView.@label)`更改为`label : String([inclView.@label](mailto:inclView.@label))`

1. 保存.
1. 重新启动服务器。

## 如果Adobe Campaign在单击同步按钮{#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}时显示错误

如果单击Adobe Campaign Classic的&#x200B;**同步**&#x200B;按钮，您会看到以下错误：

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

要解决此问题，请确保可以从计算机访问在外部帐户中配置的AEM connection-url。

从&#x200B;**localhost**&#x200B;切换到IP地址解决了此问题。

## 如果出现“无法解析XTK Date+Time &#39;undefined&#39;”错误{#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

单击“同步”后，您会收到页面上出现脚本的错误：无法解析XTK Date+Time &#39;undefined&#39;:不是有效的XTK值。

如果AEM实例上仍有过时的Adobe Campaign信息，则会发生这种情况。 通过删除AEM上的所有活动集成配置并重新构建这些配置，可解决此问题。 然后，创建新模板。

## 如果到SSL的连接在设置云服务{#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}时显示错误

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

## 如果在同步对话框{#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}中看到http而不是预期的https链接

使用以下设置：

* 使用https与AEM作者通信的托管Adobe Campaign
* 反向代理终止SSL
* 内部部署AEM作者实例

尝试在Adobe Campaign投放中同步内容时，AEM返回一列表新闻稿。 但是，列表中新闻稿的url是http地址。 在列表中选择其中一个项目时，会出错。

要解决此问题：

* 调度程序或反向代理需要配置为将原始协议作为标头进行传递。
* OSGi配置([https://&lt;host>:&lt;port>/system/console/configMgr](http://localhost:4502/system/console/configMgr))中的&#x200B;*Apache Felix Http Service SSL过滤器*&#x200B;需要配置为相应的头设置。 请参阅[https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## 如果无法在页面属性{#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}中选择我创建的自定义模板

创建Adobe Campaign邮件模板时，必须在模板的&#x200B;**jcr:content**&#x200B;节点中包含具有值&#x200B;**mapRecipient**&#x200B;的属性&#x200B;**，或者您将无法在模板的**&#x200B;页面属性&#x200B;**中选择Adobe Campaign模板（已禁用字段）)。**

## 如果日志{#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}中出现错误“com.day.cq.mcm.活动.servlets.util.ParameterMapper”

使用自定义模板时，日志中会显示错误“com.day.cq.mcm.活动.servlets.util.ParameterMapper”。 在此事件，请务必从[包共享](/help/sites-administering/package-manager.md#package-share)安装功能6576。 如果acMapping属性设置为收件人.firstName以外的值，则会在Adobe Campaign管理器端创建空值。
