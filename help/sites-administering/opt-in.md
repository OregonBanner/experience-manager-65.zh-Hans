---
title: 选择Adobe Analytics和Adobe Target
seo-title: 选择Adobe Analytics和Adobe Target
description: 了解如何选择使用Adobe Analytics和Adobe Target。
seo-description: 了解如何选择使用Adobe Analytics和Adobe Target。
uuid: 9090a0f3-d373-4826-aa68-6aa82c0fbfbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: de466511-d82f-4ddb-8f6a-7ca9240fdeab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 选择Adobe Analytics和Adobe Target{#opting-into-adobe-analytics-and-adobe-target}

AEM有一个选择加入过程，可帮助您与Adobe Analytics和Adobe Target集成。 这是现成的，作为分配给管理员用户组的预加载任务。

当您以管理员身份登录时，此任务(**配置分析和定位**)可从收件箱 [中获取](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks)。 根据您提供的凭据，它可以帮助您配置和集成这些服务。

您可以使用以下选项来配置集成：

* 通过任务配置集成。

   此操作可以立即执行，也可以稍后执行，任务将一直保留在收件箱中，直到采取某些操作。 无论哪种情况，配置都可以直接在UI中完成，或使用预定义的文 `.properties` 件。

* 选择退出集成。

   如果您希望手动配置集 [成，请考虑此选项](/help/sites-administering/marketing-cloud.md)。 另请参 [阅使用DTM将AEM与Adobe target和Adobe Analytics集成](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)。

* 使用脚本配置设置和配置。

## 配置集成 {#configuring-the-integration}

选择与以下产品集成：

* 分析功能，以便使用其页面跟踪和分析功能。
* Target可支持使用其个性化功能。

对于任一选项，您都需要提供用户帐户信息并指定要跟踪的页面。

>[!NOTE]
>
>您可以选择使用在服务器启动时读取的属性文件提供Analytics和Target帐户信息。 请参 [阅使用属性文件提供帐户信息](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file)。

当您选择加入集成时，AEM将执行以下任务：

* 创建支持与Analytics和Target连接的云配置。
* 创建用于确定被跟踪数据的框架。
* 配置网页以使用这些服务。

>[!NOTE]
>
>AT.js是默认客户端库。 这是在您的目标云服 [务配置下配置的](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration)。
>
>Adobe建议您使用AT.js作为客户端库。

要从预先加载的现成任务中选择加入，请执行以下操作：

1. 从您的收 [件箱中，选择并打 **开**](/help/sites-authoring/inbox.md#taking-action-on-an-item) “配置分析和定位”任务。

   ![optin-01](assets/optin-01.png)

1. 对于Analytics:

   1. 输入Analytics的用户帐户信息，然后单击相应的“添 **加** ”按钮。
   1. 将验证相应的凭据。
   1. 验证Analytics帐户后，选择要使用的Analytics报表包。 AEM会检索这些Analytics报表包。 状态将更新为“已添 **加”**。

1. 对于目标：

   1. 输入Target的用户帐户信息，然后单击相应的“添 **加** ”按钮。
   1. 将验证相应的凭据。 状态将更新为“已添 **加”**。

1. 选择&#x200B;**下一步**。
1. 选择应使用Analytics和／或Target的站点。

1. 选择 **完成** ，以完成。

   >[!CAUTION]
   >
   >在选择加入配置后，您需要发布受影响的站点／页面，以将这些更改复制到发布实例。

## 选择退出集成 {#opting-out-of-the-integration}

选择退出与Analytics和Target的集成，当您执行以下操作之一时：

* 不希望与这些产品集成。
* 希望手动配置集成。

   有关手动配置集成的信息，请参 [阅与Adobe Analytics集成](/help/sites-administering/adobeanalytics.md)[和与Adobe Target集成](/help/sites-administering/target.md)。

要选择退出，您需要完成预加载的任务：

* 从您的收 [件箱中，选择并完 **成** “配置分析和定位”任务](/help/sites-authoring/inbox.md#taking-action-on-an-item) 。

## 使用属性文件提供帐户信息 {#providing-account-information-using-a-properties-file}

安装AEM在服务器启动时读取的属性文件，以配置帐户属性以与Analytics和Target集成。 当您使用属性文件时，选择加入向导会自动使用文件中的属性，并相应地创建云配置。

属性文件是名为marketingcloud.properties的文本文件，您保存在AEM进程正在使用的工作目录中（通常与JAR文件位于同一目录）。 该文件包括以下属性：

* analytics.server:您使用的Analytics数据中心的URL。
* analytics.company:与您的Analytics用户帐户关联的公司。
* analytics.username:您的Analytics用户名。
* analytics.secret:与您的Analytics用户名关联的机密。
* analytics.reportsuite:要使用的Analytics报表包的名称。
* target.clientcode:与您的Target帐户关联的客户端代码。
* target.email:用于验证Target帐户的电子邮件地址。
* target.password:与您的电子邮件地址关联的密码。

属性和值以等号(=)分隔。 分析属性的前缀 `analytics`有，而目标属性的前缀有 `target`。 要配置服务，请为该服务提供所有属性的值。 如果不想配置服务，请不提供该服务的值。

以下示例文 `.properties` 件包括用于为Analytics创建云配置的属性值：

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

以下过程介绍如何使用属性文件加入集成。

1. 在AEM `marketingcloud.properties` 进程正在使用的工作目录中创建文件（作者实例）。

   >[!NOTE]
   >
   >工作目录通常是保存jar或文件的目 `license.properties` 录。
   >
   >但是，它也可以由系统属性定义为绝对路径：
   >
   >`mac.provisioning.file.container`

1. 根据您的Analytics和／或Target帐户添加属性值。
1. 启动或重新启动服务器，然后使用管理员帐户登录。
1. 如配置集成中所述，打开配置分析 [和定位任务](/help/sites-administering/opt-in.md#configuring-the-integration)。 向导使用文件中的值，而不是请求您的帐户信 `.properties` 息。

   选 **择相应服务** ，然后继续向导。

   ![optin-02](assets/optin-02.png)

## 关于云配置 {#about-the-cloud-configurations}

当您配置与Analytics和Target的集成时，AEM会自动创建所需的云配置和框架。 例如，Analytics云配置称为“已配置分析帐户”。

您无需更改云配置。 但是，您可以根据需要配置框架。 (请参 [阅使用Adobe Analytics属性映射组件数据](/help/sites-administering/adobeanalytics-mapping.md) , [并添加目标框架](/help/sites-administering/target.md)。)

>[!NOTE]
>
>默认情况下，当您选择加入Adobe target配置向导时，“准确定位”处于启用状态。
>
>准确定位意味着云服务配置在加载内容之前会等待上下文加载。 因此，在性能方面，准确定位可能会在加载内容之前造成毫秒的延迟。
>
>创作实例上始终启用准确定位。 但是，在发布实例中，您可以通过清除云服务配置(http://localhost:4502/etc/cloudservices.html)中“准确定位”旁边的复选标记，选择全局关闭准确&#x200B;**定位**。 您还可以打开和关闭各个组件的精确定位，而不管您在云服务配置中进行了何种设置。
>
>如果您已经创 ***建了目标组件*** ，并且更改了此设置，则您所做的更改不会影响这些组件。 您必须直接对这些组件进行任何更改。

>[!CAUTION]
>
>当您选择Analytics配置并选择特定 `reportsuite` 配置时，框架将被限制为发布运行模式。 这意味着跟踪仅适用于发布实例。
>
>如果需要对创作实例进行跟踪，则值应更改为 `all`。

## 通过脚本配置设置和配置 {#configuring-the-setup-and-provisioning-via-script}

作为管理员，您可能希望使用脚本触发设置和设置，而不是手动遍历向导。 您可以通过以下方式执行此操作：

* 将POST请求发送到 **/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json** ，并包含所需参数。

您发送的参数取决于以下各项：

* 如果要使用已填 **充所有必需凭据的marketingcloud.properties** 文件，则必须发送以下参数：

   * `automaticProvisioning`= `true`
   * `servicename`= `analytics|target`
   * `path`=AEM页面的路径，以附加创建的云服务配置
   例如，创建Analytics和Target配置并将其附加到we.retail页面的curl请求为：

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

* 如果您不想使用marketingcloud. **properties文件** ，则必须发送凭据和参数；例如：

   * automaticProvisioning= `true`
   * servicename= `analytics|target`
   * path=path to an AEM page to attach created cloud services configurs;可以定义多个路径
   * analytics.server= `https://servername`
   * analytics.company= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * target.clientcode= `mycompany`
   * target.email= `me@adobe.com`
   * target.password= `password`
   在这种情况下，创建Analytics和Target配置并将其附加到we-retail页面的curl请求为：

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

