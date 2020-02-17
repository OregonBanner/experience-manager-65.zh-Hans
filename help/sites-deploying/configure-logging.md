---
title: 记录
seo-title: 记录
description: 了解如何为中央日志记录服务配置全局参数、各个服务的特定设置或如何请求数据记录。
seo-description: 了解如何为中央日志记录服务配置全局参数、各个服务的特定设置或如何请求数据记录。
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 记录{#logging}

AEM允许您配置：

* 中央日志记录服务的全局参数
* 请求数据记录；请求信息的专用日志记录配置
* 具体服务设置；例如，单个日志文件和日志消息的格式

这些都是 [OSGi配置](/help/sites-deploying/configuring-osgi.md)。

>[!NOTE]
>
>登录AEM基于Sling原则。 有关更 [多信息，请参阅](https://sling.apache.org/site/logging.html) Sling日志记录。

## 全局日志记录 {#global-logging}

[Apache Sling日志记录配置](/help/sites-deploying/osgi-configuration-settings.md) (Apache Sling Logging Configuration)用于配置根记录器。 这定义了在AEM中登录的全局设置：

* 记录级别
* 中央日志文件的位置
* 要保存的版本数
* 版本旋转；最大大小或时间间隔
* 编写日志消息时使用的格式

>[!NOTE]
>
>本知 [识库文章](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html) ，介绍如何旋转request.log和access.log文件。

## 记事员与个人服务作者 {#loggers-and-writers-for-individual-services}

除了全局日志记录设置之外，AEM还允许您为单个服务配置特定设置：

* 特定日志记录级别
* 单个日志文件的位置
* 要保存的版本数
* 版本旋转；最大大小或时间间隔
* 编写日志消息时使用的格式
* 记录器（提供日志消息的OSGi服务）

这允许您将单个服务的日志消息引导到单独的文件中。 这在开发或测试过程中特别有用；例如，当您需要特定服务的更高日志级别时。

AEM使用以下代码将日志消息写入文件：

1. OSGi服 **务** （记录器）写入日志消息。
1. 记 **录器会采用此消息** ，并根据您的规范设置其格式。
1. 记 **录编写器** ，将所有这些消息写入您定义的物理文件。

这些元素通过相应元素的以下参数进行链接：

* **记录器（记录器）**

   定义生成消息的服务。

* **日志文件（记录器）**

   定义用于存储日志消息的物理文件。

   这用于将记录器与记录写入器链接。 该值必须与要建立连接的记录写入程序配置中的相同参数相同。

* **日志文件（记录编写器）**

   定义将写入日志消息的物理文件。

   这必须与“记录编写器”配置中的相同参数相同，否则将不匹配。 如果没有匹配项，则将使用默认配置（每日日志旋转）创建隐式编写器。

### 标准记事员和作者 {#standard-loggers-and-writers}

标准AEM安装中包含某些记录程序和作者。

第一种是特殊情况，因为它同时控制文件 `request.log` 和文 `access.log` 件：

* 记录器：

   * Apache Sling可自定义的请求数据记录器

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 将有关请求内容的消息写入 `request.log`。

* 链接到：

   * Apache Sling Request Logger

      (org.apache.sling.engine.impl.log.RequestLogger)

   * 将消息写入或 `request.log` 中 `access.log`。

如果需要，可以自定义这些配置，但标准配置适用于大多数安装。

其他对遵循标准配置：

* 记录器：

   * Apache Sling Logging Logger配置

      (org.apache.sling.commons.log.LogManager.factory.config)

   * 将消 `Information` 息写入 `logs/error.log`。

* 指向作者的链接：

   * Apache Sling日志记录编写器配置

      (org.apache.sling.commons.log.LogManager.factory.writer)

* 记录器：

   * Apache Sling Logging Logger Configuration(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * 为服 `Warning` 务将消 `../logs/error.log` 息写入 `org.apache.pdfbox`。

* 不链接到特定的Writer，因此将创建并使用具有默认配置（每日日志旋转）的隐式Writer。

### 创建您自己的伐木工和作者 {#creating-your-own-loggers-and-writers}

您可以定义自己的记录器／写入器对：

1. 创建工厂配置Apache Sling日志记录 [器配置的新实例](/help/sites-deploying/osgi-configuration-settings.md)。

   1. 指定日志文件。
   1. 指定记录器。
   1. 根据需要配置其他参数。

1. 创建工厂配置Apache Sling日志记录编写 [器配置的新实例](/help/sites-deploying/osgi-configuration-settings.md)。

   1. 指定日志文件——该文件必须与为记录器指定的文件匹配。
   1. 根据需要配置其他参数。

>[!NOTE]
>
>在某些情况下，您可能希望创建自定 [义日志文件](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)。

