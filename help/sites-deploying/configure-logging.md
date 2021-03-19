---
title: 记录
seo-title: 记录
description: 了解如何为中央日志记录服务配置全局参数、单个服务的特定设置或如何请求数据记录。
seo-description: 了解如何为中央日志记录服务配置全局参数、单个服务的特定设置或如何请求数据记录。
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
feature: 配置
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---


# 记录{#logging}

AEM优惠您可以配置：

* 中央日志记录服务的全局参数
* 请求数据记录；请求信息的专用日志记录配置
* 具体设置；例如，单个日志文件和日志消息的格式

这些都是[OSGi配置](/help/sites-deploying/configuring-osgi.md)。

>[!NOTE]
>
>登录AEM基于Sling原则。 有关更多信息，请参阅[Sling日志](https://sling.apache.org/site/logging.html)。

## 全局日志记录{#global-logging}

[Apache Sling Logging Configuration](/help/sites-deploying/osgi-configuration-settings.md) 用于配置根记录器。这定义了在AEM中登录的全局设置：

* 记录级别
* 中央日志文件的位置
* 要保留的版本数
* 版本旋转；最大大小或时间间隔
* 写入日志消息时使用的格式

>[!NOTE]
>
>此[知识库文章](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html)说明如何旋转request.log和access.log文件。

## 个人服务的记录器和作者{#loggers-and-writers-for-individual-services}

除了全局日志记录设置之外，AEM还允许您为单个服务配置特定设置：

* 特定日志记录级别
* 单个日志文件的位置
* 要保留的版本数
* 版本旋转；最大大小或时间间隔
* 写入日志消息时使用的格式
* 记录器（提供日志消息的OSGi服务）

这允许您将单个服务的日志消息渠道到单独的文件中。 这在开发或测试时特别有用；例如，当您需要为特定服务增加日志级别时。

AEM使用以下方法将日志消息写入文件：

1. **OSGi服务**（记录器）写入日志消息。
1. **日志记录记录器**&#x200B;将采用此消息并根据您的规范设置其格式。
1. **日志记录编写器**&#x200B;将所有这些消息写入您定义的物理文件。

这些元素通过相应元素的以下参数链接：

* **记录器（记录器）**

   定义生成消息的服务。

* **日志文件（日志记录记录器）**

   定义用于存储日志消息的物理文件。

   这用于将日志记录器与日志记录写入器链接。 该值必须与要建立连接的日志记录写入器配置中的相同参数相同。

* **日志文件（日志编写器）**

   定义将写入日志消息的物理文件。

   这必须与日志记录编写器配置中的相同参数相同，否则将不进行匹配。 如果没有匹配项，则将使用默认配置（每日日志旋转）创建隐式编写器。

### 标准记录器和作者{#standard-loggers-and-writers}

标准AEM安装中包含某些记录程序和作者。

第一种是特殊情况，因为它同时控制`request.log`和`access.log`文件：

* 记录器：

   * Apache Sling可自定义请求数据记录器

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 向`request.log`写入有关请求内容的消息。

* 链接：

   * Apache Sling Request Logger

      (org.apache.sling.engine.impl.log.RequestLogger)

   * 将消息写入`request.log`或`access.log`。

如果需要，可以自定义这些配置，但标准配置适用于大多数安装。

其他对遵循标准配置：

* 记录器：

   * Apache Sling日志记录记录器配置

      (org.apache.sling.commons.log.LogManager.factory.config)

   * 将`Information`消息写入`logs/error.log`。

* 指向作者的链接：

   * Apache Sling日志记录编写器配置

      (org.apache.sling.commons.log.LogManager.factory.writer)

* 记录器：

   * Apache Sling日志记录记录器配置
(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * 将`Warning`消息写入`../logs/error.log`，以便服务`org.apache.pdfbox`。

* 不链接到特定的Writer，因此将创建并使用具有默认配置（每日日志旋转）的隐式Writer。

### 创建您自己的记录器和作者{#creating-your-own-loggers-and-writers}

您可以定义自己的记录器/写入器对：

1. 创建工厂配置[Apache Sling日志记录记录器配置](/help/sites-deploying/osgi-configuration-settings.md)的新实例。

   1. 指定日志文件。
   1. 指定记录器。
   1. 根据需要配置其他参数。

1. 创建工厂配置[Apache Sling日志记录编写器配置](/help/sites-deploying/osgi-configuration-settings.md)的新实例。

   1. 指定日志文件 — 此文件必须与为记录器指定的文件匹配。
   1. 根据需要配置其他参数。

>[!NOTE]
>
>在某些情况下，您可能希望创建[自定义日志文件](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)。

