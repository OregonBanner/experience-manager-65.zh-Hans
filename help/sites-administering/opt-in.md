---
title: 选择加入Adobe Analytics和Adobe Target
seo-title: 选择加入Adobe Analytics和Adobe Target
description: 了解如何加入Adobe Analytics和Adobe Target。
seo-description: 了解如何加入Adobe Analytics和Adobe Target。
uuid: 9090a0f3-d373-4826-aa68-6aa82c0fbfbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: de466511-d82f-4ddb-8f6a-7ca9240fdeab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 0%

---


# 选择加入Adobe Analytics和Adobe Target{#opting-into-adobe-analytics-and-adobe-target}

AEM有一个选择加入的过程，可帮助您与Adobe Analytics和Adobe Target集成。 这是现成的，作为分配给管理员用户组的预加载任务。

以管理员身份登录时，可从[收件箱](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks)中找到此任务（**配置分析和定位**）。 根据您提供的凭据，它可以帮助您配置和集成这些服务。

您有以下用于配置集成的选项：

* 通过任务配置集成。

   此操作可以立即执行，也可以稍后执行，任务将保留在收件箱中，直到执行某些操作。 无论哪种情况，配置都可以直接在UI中完成，或使用预定义的`.properties`文件完成。

* 集选择退出成。

   如果您希望[手动配置集成](/help/sites-administering/marketing-cloud.md)，请考虑此选项。 另请参阅[使用DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)将AEM与Adobe Target和Adobe Analytics集成。

* 使用脚本配置设置和设置。

## 配置集成{#configuring-the-integration}

选择与以下产品集成：

* Analytics可启用页面跟踪和分析功能。
* 目标，以支持使用其个性化功能。

对于任一选项，您都需要提供用户帐户信息并指定要跟踪的页面。

>[!NOTE]
>
>您可以选择使用在服务器启动时读取的属性文件提供分析和目标帐户信息。 请参阅[使用属性文件提供帐户信息](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file)。

当您选择进行集成时，AEM将执行以下任务:

* 创建云配置，以启用与Analytics和目标的连接。
* 创建确定要跟踪的数据的框架。
* 配置网页以使用这些服务。

>[!NOTE]
>
>AT.js是默认客户端库。 这是在您的[目标云服务配置](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration)下配置的。
>
>Adobe建议您使用AT.js作为客户端库。

要从预先加载的现成任务中选择加入，请执行以下操作：

1. 从[收件箱中，选择并&#x200B;**打开**&#x200B;配置分析和定位](/help/sites-authoring/inbox.md#taking-action-on-an-item)任务。

   ![optin-01](assets/optin-01.png)

1. 对于Analytics:

   1. 输入Analytics的用户帐户信息，然后单击相应的&#x200B;**添加**&#x200B;按钮。
   1. 验证相应的凭据。
   1. 验证Analytics帐户后，选择要使用的Analytics报表包。 AEM检索那些Analytics报表包。 状态将更新为&#x200B;**Added**。

1. 对于目标:

   1. 输入目标的用户帐户信息，然后单击相应的&#x200B;**添加**&#x200B;按钮。
   1. 验证相应的凭据。 状态将更新为&#x200B;**Added**。

1. 选择&#x200B;**下一步**。
1. 选择应使用Analytics和／或目标的网站。

1. 选择&#x200B;**完成**&#x200B;以完成。

   >[!CAUTION]
   >
   >选择加入配置后，您需要发布受影响的站点／页面，以将这些更改复制到发布实例。

## 选择退出集成{#opting-out-of-the-integration}

与选择退出Analytics和目标的集成：

* 不想与这些产品集成。
* 希望手动配置集成。

   有关手动配置集成的信息，请参阅[与Adobe Analytics集成](/help/sites-administering/adobeanalytics.md)和[与Adobe Target集成](/help/sites-administering/target.md)。

要完选择退出成预加载的任务:

* 从[收件箱中，选择并&#x200B;**完成**&#x200B;配置分析和定位](/help/sites-authoring/inbox.md#taking-action-on-an-item)任务。

## 使用属性文件{#providing-account-information-using-a-properties-file}提供帐户信息

安装AEM在服务器启动时读取的属性文件，以配置帐户属性以与Analytics和目标集成。 当您使用属性文件时，选择加入向导会自动使用文件中的属性，并相应地创建云配置。

属性文件是名为marketingcloud.properties的文本文件，您将其保存在AEM进程所使用的工作目录中（通常与JAR文件相同的目录）。 该文件包含以下属性：

* analytics.server:您使用的Analytics数据中心的URL。
* analytics.公司:与您的Analytics用户帐户关联的公司。
* analytics.username:您的Analytics用户名。
* analytics.secret:与您的Analytics用户名关联的机密。
* analytics.reportsuite:要使用的Analytics报表包的名称。
* 目标.clientcode:与您的目标帐户关联的客户端代码。
* 目标.email:用于验证目标帐户的电子邮件地址。
* 目标.密码：与您的电子邮件地址关联的密码。

属性和值以等号(=)分隔。 Analytics属性的前缀为`analytics`,目标属性前缀为`target`。 要配置服务，请为该服务提供所有属性的值。 如果不想配置服务，请不提供该服务的值。

以下示例`.properties`文件包含用于为Analytics创建云配置的属性值：

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

1. 在AEM进程正在使用的工作目录中创建`marketingcloud.properties`文件（作者实例）。

   >[!NOTE]
   >
   >工作目录通常是保存jar或`license.properties`文件的目录。
   >
   >但是，它也可以由系统属性定义为绝对路径：
   >
   >`mac.provisioning.file.container`

1. 根据您的Analytics和／或目标帐户添加属性值。
1. 开始或重新启动服务器，然后使用管理员帐户登录。
1. 打开“配置分析和定位”任务，如[配置集成](/help/sites-administering/opt-in.md#configuring-the-integration)中所述。 向导使用`.properties`文件中的值，而不是请求帐户信息。

   选择&#x200B;**添加**&#x200B;作为相应的服务，然后继续向导。

   ![optin-02](assets/optin-02.png)

## 关于云配置{#about-the-cloud-configurations}

当您配置与Analytics和目标的集成时，AEM会自动创建所需的云配置和框架。 例如，Analytics云配置称为“已配置分析帐户”。

您无需更改云配置。 但是，您可以根据需要配置框架。 (请参阅[使用Adobe Analytics属性](/help/sites-administering/adobeanalytics-mapping.md)和[添加目标框架](/help/sites-administering/target.md)映射组件数据。)

>[!NOTE]
>
>默认情况下，当您选择加入Adobe Target配置向导时，将启用准确定位。
>
>准确定位意味着云服务配置在加载内容之前会等待上下文加载。 因此，在性能方面，准确定位可能会在加载内容之前造成毫秒的延迟。
>
>创作实例始终启用准确定位。 但是，在发布实例中，您可以通过清除云服务配置中“准确定位”旁的复选标记(**http://localhost:4502/etc/cloudservices.html**)，选择全局关闭准确定位。 无论您在云服务配置中进行何种设置，您仍然可以为各个组件打开和关闭精确定位。
>
>如果&#x200B;***已经创建了目标组件，并且您更改了此设置，则所做的更改不会影响这些组件。***&#x200B;您必须直接对这些组件进行任何更改。

>[!CAUTION]
>
>当您选择加入Analytics配置并选择特定`reportsuite`时，框架将被限制为发布运行模式。 这意味着跟踪仅适用于发布实例。
>
>如果创作实例需要跟踪，则值应更改为`all`。

## 通过脚本{#configuring-the-setup-and-provisioning-via-script}配置设置和配置

作为管理员，您可能希望使用脚本触发设置和设置，而不是手动遍历向导。 您可以通过以下方式执行此操作：

* 使用所需参数向&#x200B;**/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json**&#x200B;发送POST请求。

您发送的参数取决于以下参数：

* 如果要使用已填写所有必需凭据的&#x200B;**marketingcloud.properties**&#x200B;文件，则必须发送以下参数：

   * `automaticProvisioning`= `true`
   * `servicename`=  `analytics|target`
   * `path`=AEM页面的路径以附加创建的云服务配置

   例如，创建Analytics和目标配置并将其附加到we.retail页面的curl请求为：

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

* 如果您不想使用&#x200B;**marketingcloud.properties**&#x200B;文件，则必须发送凭据和参数；例如：

   * automaticProvisioning= `true`
   * servicename= `analytics|target`
   * path=path到AEM页面以附加创建的云服务配置；可以定义多个路径
   * analytics.server= `https://servername`
   * analytics.公司= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * 目标.clientcode= `mycompany`
   * 目标.email= `me@adobe.com`
   * 目标.password= `password`

   在这种情况下，创建Analytics和目标配置并将其附加到we-retail页面的curl请求为：

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

