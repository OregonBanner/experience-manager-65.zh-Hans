---
title: 选择加入Adobe Analytics和Adobe Target
seo-title: Opting Into Adobe Analytics and Adobe Target
description: 了解如何选择加入Adobe Analytics和Adobe Target。
seo-description: Learn how to opt into Adobe Analytics and Adobe Target.
uuid: 9090a0f3-d373-4826-aa68-6aa82c0fbfbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: de466511-d82f-4ddb-8f6a-7ca9240fdeab
exl-id: 3603e929-2aa1-4c25-ad9a-b10ff52a59f4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 10%

---

# 选择加入Adobe Analytics和Adobe Target{#opting-into-adobe-analytics-and-adobe-target}

AEM有一个选择加入过程，可帮助您与Adobe Analytics和Adobe Target集成。 这是现成的，即分配给管理员用户组的预加载任务。

当您以管理员身份登录时，此任务(**配置Analytics和定位**) [收件箱](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks). 根据您提供的凭据，它可帮助您配置和集成这些服务。

您可以使用以下选项来配置集成：

* 通过任务配置集成。

   此操作可以立即执行，也可以稍后执行，该任务将保留在收件箱中，直到执行某些操作为止。 无论哪种情况，配置都可以直接在UI中完成，也可以使用预定义的 `.properties` 文件。

* 选择退出集成。

   如果您希望 [手动配置集成](/help/sites-administering/marketing-cloud.md). 另请参阅 [使用DTM将AEM与Adobe Target和Adobe Analytics集成](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

* 使用脚本配置设置和配置。

## 配置集成 {#configuring-the-integration}

选择加入与的集成：

* Analytics，以便能够使用其页面跟踪和分析功能。
* Target以启用其个性化功能。

对于任一选项，您都需要提供用户帐户信息并指定要跟踪的页面。

>[!NOTE]
>
>您可以选择使用在服务器启动时读取的属性文件来提供Analytics和Target帐户信息。 请参阅 [使用属性文件提供帐户信息](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file).

选择加入集成后，AEM会执行以下任务：

* 创建可启用与Analytics和Target连接的云配置。
* 创建用于确定所跟踪数据的框架。
* 配置网页以使用这些服务。

>[!NOTE]
>
>AT.js是默认的客户端库。 这是在 [target云服务配置](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration).
>
>Adobe建议您使用AT.js作为客户端库。

要选择加入预加载的即装即用任务，请执行以下操作：

1. 从 [收件箱、选择和 **打开** 配置Analytics和定位](/help/sites-authoring/inbox.md#taking-action-on-an-item) 任务。

   ![optin-01](assets/optin-01.png)

1. 对于Analytics:

   1. 输入Analytics的用户帐户信息，然后单击相应的 **添加** 按钮。
   1. 相应的凭据已进行身份验证。
   1. 在Analytics帐户进行身份验证后，选择要使用的Analytics报表包。 AEM会检索这些Analytics报表包。 状态已更新为 **添加了**.

1. 对于Target:

   1. 输入Target的用户帐户信息，然后单击相应的 **添加** 按钮。
   1. 相应的凭据已进行身份验证。 状态已更新为 **添加了**.

1. 选择&#x200B;**下一步**。
1. 选择应使用Analytics和/或Target的网站。

1. 选择 **完成** 完成。

   >[!CAUTION]
   >
   >选择加入配置后，您需要发布受影响的站点/页面，以将这些更改复制到发布实例。

## 选择退出集成 {#opting-out-of-the-integration}

在以下情况下选择退出与Analytics和Target的集成：

* 不希望与这些产品集成。
* 首选手动配置集成。

   有关手动配置集成的信息，请参阅 [与Adobe Analytics集成](/help/sites-administering/adobeanalytics.md) 和 [与Adobe Target集成](/help/sites-administering/target.md).

要选择禁用，您需要完成预加载的任务：

* 从 [收件箱、选择和 **完成** 配置Analytics和定位](/help/sites-authoring/inbox.md#taking-action-on-an-item) 任务。

## 使用属性文件提供帐户信息 {#providing-account-information-using-a-properties-file}

安装AEM在服务器启动时读取的属性文件，以配置与Analytics和Target集成的帐户属性。 使用属性文件时，选择加入向导会自动使用文件中的属性，并且会相应地创建云配置。

属性文件是名为marketingcloud.properties的文本文件，您将其保存在AEM进程所使用的工作目录中（通常与JAR文件相同的目录）。 文件包含以下属性：

* analytics.server:您使用的Analytics数据中心的URL。
* analytics.company:与您的Analytics用户帐户关联的公司。
* analytics.username:您的Analytics用户名。
* analytics.secret:与您的Analytics用户名关联的密钥。
* analytics.reportsuite:要使用的Analytics报表包的名称。
* target.clientcode:与您的Target帐户关联的客户端代码。
* target.email:用于验证Target帐户的电子邮件地址。
* target.password:与您的电子邮件地址关联的密码。

属性和值以等号(=)进行分隔。 Analytics属性的前缀为 `analytics`，并且Target属性的前缀为 `target`. 要配置服务，请为该服务的所有属性提供值。 如果不想配置服务，则不提供该服务的值。

以下示例 `.properties` 文件包含用于为Analytics创建云配置的属性值：

```xml
analytics.server=https://test.omniture.com/login/
analytics.company=MyCompany
analytics.username=sbroders
analytics.secret=12345678
analytics.reportsuite=myreportsuite
target.clientcode=
target.email=
target.password=
```

以下过程介绍如何使用属性文件选择加入集成。

1. 创建 `marketingcloud.properties` 文件（创作实例）。

   >[!NOTE]
   >
   >工作目录通常是存放jar或 `license.properties` 文件。
   >
   >但是，它也可以由系统属性定义为绝对路径：
   >
   >`mac.provisioning.file.container`

1. 根据您的Analytics和/或Target帐户添加属性值。
1. 启动或重新启动服务器，然后使用管理员帐户登录。
1. 按照 [配置集成](/help/sites-administering/opt-in.md#configuring-the-integration). 向导不会请求您的帐户信息，而是使用 `.properties` 文件。

   选择 **添加** 对于相应的服务，继续执行向导。

   ![optin-02](assets/optin-02.png)

## 关于云配置 {#about-the-cloud-configurations}

当您配置与Analytics和Target的集成时，AEM会自动创建所需的云配置和框架。 例如，Analytics云配置称为已配置的Analytics帐户。

您无需更改云配置。 但是，您可以根据需要配置框架。 (请参阅 [使用Adobe Analytics属性映射组件数据](/help/sites-administering/adobeanalytics-mapping.md) 和 [添加Target框架](/help/sites-administering/target.md).)

>[!NOTE]
>
>默认情况下，当您选择加入 Adobe Target 配置向导时，将启用“准确定位”。
>
>准确定位意味着，云服务配置将等到上下文加载完后，再加载内容。因此，就性能而言，准确定位可能会导致加载内容前有几毫秒的延迟。
>
>对于创作实例，“准确定位”始终处于启用状态。但在发布实例上，您可以通过清除云服务配置中“准确定位”旁边的复选标记来选择全局关闭准确定位 (**http://localhost:4502/etc/cloudservices.html**)。无论您在云服务配置中的设置如何，您都可以为各个组件打开和关闭“准确定位”。
>
>如果您&#x200B;***已经***&#x200B;创建目标组件并更改此设置，则您的更改不会影响这些组件。您必须直接对这些组件进行任何更改。

>[!CAUTION]
>
>当您选择加入Analytics配置和 `reportsuite` ，则框架将被限制为发布运行模式。 这意味着跟踪仅在发布实例上有效。
>
>如果需要对创作实例进行跟踪，则应将值更改为 `all`.

## 通过脚本配置设置和配置 {#configuring-the-setup-and-provisioning-via-script}

作为管理员，您可能希望使用脚本触发设置和配置，而不是手动逐步完成向导。 您可以通过以下方式执行此操作：

* 将POST请求发送到 **/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json** 参数。

您发送的参数取决于以下各项：

* 如果您想使用 **marketingcloud.properties** 已填写所有必需凭据的文件，则必须发送以下参数：

   * `automaticProvisioning`= `true`
   * `servicename`= `analytics|target`
   * `path`=用于附加已创建的云服务配置的AEM页面的路径

   例如，创建Analytics和Target配置并将其附加到we.retail页面的curl请求将为：

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

* 如果您不想使用 **marketingcloud.properties** 文件之后，您必须发送凭据和参数；例如：

   * automaticProvisioning= `true`
   * servicename= `analytics|target`
   * path=path到AEM页面以附加创建的云服务配置；可以定义多个路径
   * analytics.server= `https://servername`
   * analytics.company= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * target.clientcode= `mycompany`
   * target.email= `me@adobe.com`
   * target.password= `password`

   在这种情况下，用于创建Analytics和Target配置并将其附加到we-retail页面的curl请求将为：

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```
