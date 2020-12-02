---
title: 手动配置与Adobe Target的集成
seo-title: 手动配置与Adobe Target的集成
description: 了解如何手动配置与Adobe Target的集成。
seo-description: 了解如何手动配置与Adobe Target的集成。
uuid: 0bb76a65-f981-4cc5-bee8-5feb3297137c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 20c8eb1d-5847-4902-b7d3-4c3286423b46
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '2202'
ht-degree: 4%

---


# 手动配置与Adobe Target{#manually-configuring-the-integration-with-adobe-target}的集成

您可以修改在使用向导时所做的选择加入向导配置，也可以手动与Adobe Target集成，而无需使用向导。

## 修改加入向导配置{#modifying-the-opt-in-wizard-configurations}

[将AEM与Adobe Target](/help/sites-administering/target.md)集成的[选择加入向导](/help/sites-administering/opt-in.md)会自动创建名为“预配目标配置”的目标云配置。 该向导还为名为“已配置目标框架”的云配置创建目标框架。 您可以根据需要修改云配置和框架的属性。

您还可以配置A4TAdobe Target配置，将Adobe Target用作定位内容时的报告源。

要找到云配置和框架，请通过&#x200B;**工具** > **部署** > **云**&#x200B;导航到&#x200B;**Cloud Services**。 ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
在Adobe Target下，单击或点按**显示配置**。

### 已设置目标配置属性{#provisioned-target-configuration-properties}

在“选择加入”向导创建的“已设置目标配置”云配置中使用以下属性值：

* **客户端代** 码：如在选择加入向导中输入的。
* **电子邮件：** 如在选择加入向导中输入的。
* **密码：** 如在“选择加入”向导中输入的。
* **API类型：** REST
* **从Adobe Target同步区段：** 已选。

* **客户端库：** mbox.js。
* **使用DTM传送客户端库：未** 选择。如果[使用DTM](/help/sites-administering/dtm.md)或其他标签管理系统来托管mbox.js或AT.js文件，则选择此选项。 Adobe建议您使用DTM而不是AEM来传送库。

* **自定义mbox.js:** 未指定，因此使用默认mbox.js文件。根据需要指定要使用的自定义mbox.js文件。 仅当您选择了mbox.js时显示。
* **自定义AT.js:** 未指定，以使用默认AT.js文件。根据需要指定要使用的自定义AT.js文件。 仅当您选择了AT.js时显示。

>[!NOTE]
>
>在AEM 6.3中，您可以选择目标库文件[AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html)，这是Adobe Target的一个新实现库，专为典型的Web实现和单页应用程序设计。
>
>AT.js优惠了mbox.js库的几项改进：
>
>* 改进了Web实现的页面加载时间
>* 改进的安全性
>* 针对单页应用程序的更好实施选项
>* AT.js包含包含在目标.js中的组件，因此不再调用目标.js


### 已设置目标框架属性{#provisioned-target-framework-properties}

选择加入向导创建的预配目标框架配置为从用户档案数据存储发送上下文数据。 默认情况下，商店的年龄和性别数据项会发送到目标。 您的解决方案可能需要发送其他参数。

![chlimage_1-158](assets/chlimage_1-158.png)

您可以配置框架以向目标发送其他上下文信息，如[添加目标框架](/help/sites-administering/target-configuring.md#adding-a-target-framework)中所述。

### 配置A4TAnalytics Cloud配置{#configuring-a-t-analytics-cloud-configuration}

您可以将Adobe Target配置为在定位内容时使用Adobe Analytics作为报告源。

为此，您需要指定要将您的Adobe Target云配置与以下项连接的A4T云配置：

1. 通过&#x200B;**AEM徽标** > **工具** > **部署** > **Cloud Services**&#x200B;导航到&#x200B;**Cloud Services**。
1. 在&#x200B;**Adobe Target**&#x200B;部分，单击&#x200B;**立即配置**。
1. 重新连接到您的Adobe Target配置。
1. 在&#x200B;**A4TAnalytics Cloud配置**&#x200B;下拉菜单中，选择框架。

   >[!NOTE]
   >
   >只有为A4T启用的分析配置才可用。
   >
   >使用AEM配置A4T时，可能会看到缺少配置引用条目。 要能够选择分析框架，请执行以下操作：
   >
   >1. 导航到&#x200B;**工具** > **常规** > **CRXDE Lite**。
   1. 导航到&#x200B;**/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. 将属性&#x200B;**disable**&#x200B;设置为&#x200B;**false**。
   1. 点按或单击&#x200B;**保存全部**。


   ![chlimage_1-159](assets/chlimage_1-159.png)

   单击&#x200B;**确定**。与Adobe Target目标内容时，您可以[选择报告源](/help/sites-authoring/content-targeting-touch.md)。

## 手动与Adobe Target{#manually-integrating-with-adobe-target}集成

手动与Adobe Target集成，而不是使用选择加入向导。

>[!NOTE]
目标库文件[AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html)是Adobe Target的一个新实现库，专为典型Web实现和单页应用程序设计。 Adobe建议您使用AT.js而不是mbox.js作为客户端库。
AT.js优惠了mbox.js库的几项改进：
* 改进了Web实现的页面加载时间
* 改进的安全性
* 针对单页应用程序的更好实施选项
* AT.js包含包含在目标.js中的组件，因此不再调用目标.js

您可以在&#x200B;**客户端库**&#x200B;下拉菜单中选择AT.js或mbox.js。

### 创建目标云配置{#creating-a-target-cloud-configuration}

要使AEM能够与Adobe Target交互，请创建目标云配置。 要创建配置，请提供Adobe Target客户端代码和用户凭据。

您只需创建一次目标云配置，因为您可以将配置与多个AEM活动关联。 如果您有多个Adobe Target客户端代码，请为每个客户端代码创建一个配置。

您可以配置云配置以同步来自Adobe Target的区段。 如果启用同步，则在保存云配置后，会立即从后台目标导入区段。

请按照以下过程在AEM中创建目标云配置：

1. 通过&#x200B;**AEM徽标** > **工具** > **部署** > **Cloud Services**&#x200B;导航到&#x200B;**Cloud Services**。 ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   将打开&#x200B;**Adobe Marketing Cloud**&#x200B;概述页面。

1. 在&#x200B;**Adobe Target**&#x200B;部分，单击&#x200B;**立即配置**。
1. 在&#x200B;**创建配置**&#x200B;对话框中：

   1. 为配置指定&#x200B;**Title**。
   1. 选择&#x200B;**Adobe Target配置**&#x200B;模板。
   1. 单击&#x200B;**创建**。

   此时将打开编辑对话框。

   ![chlimage_1-160](assets/chlimage_1-160.png)

   >[!NOTE]
   使用AEM配置A4T时，可能会看到缺少配置引用条目。 要能够选择分析框架，请执行以下操作：
   1. 导航到&#x200B;**工具** > **常规** > **CRXDE Lite**。
   1. 导航到&#x200B;**/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. 将属性&#x200B;**disable**&#x200B;设置为&#x200B;**false**。
   1. 点按或单击&#x200B;**保存全部**。


1. 在对话框中，提供这些属性的值。

   * **客户端代码**:目标帐户客户端代码
   * **电子邮件**:目标帐户电子邮件。
   * **密码**:目标帐户密码。
   * **API类型**:REST或XML
   * **A4TAnalytics Cloud配置**:选择用于目标活动目标和指标的Analytics云配置。如果您在定位内容时使用Adobe Analytics作为报告源，则需要此项。 如果看不到云配置，请参阅[配置A4TAnalytics Cloud配置](#configuring-a-t-analytics-cloud-configuration)中的注释。

   * **使用准确定位：** 默认情况下，此复选框处于选中状态。如果选中，云服务配置将在加载内容之前等待上下文加载。 请参阅以下注释。
   * **从Adobe Target同步区段：选** 择此选项可下载在目标中定义的区段，以在AEM中使用它们。当“API类型”属性为REST时，必须选择此选项，因为不支持内联段，并且您始终需要使用目标中的段。 (请注意，AEM术语“segment”等效于目标“受众”。)
   * **客户端** 库：选择mbox.js还是AT.js客户端库。
   * **使用DTM传送客户端库** -选择此选项可使用来自DTM的AT.js或mbox.js或其他标签管理系统。必须[配置DTM集成](/help/sites-administering/dtm.md)才能使用此选项。 Adobe建议您使用DTM而不是AEM来传送库。
   * **自定义mbox.js**:如果选中DTM框或使用默认mbox.js，则保留为空。或者上传自定义mbox.js。 仅当您选择了mbox.js时显示。
   * **自定义AT.js**:如果选中DTM框或使用默认的AT.js，则保留为空。或者上传自定义AT.js。 仅当您选择了AT.js时显示。

   >[!NOTE]
   默认情况下，当您选择加入Adobe Target配置向导时，将启用准确定位。
   准确定位意味着云服务配置在加载内容之前会等待上下文加载。 因此，在性能方面，准确定位可能会在加载内容之前造成毫秒的延迟。
   创作实例始终启用准确定位。 但是，在发布实例中，您可以通过清除云服务配置中“准确定位”旁的复选标记(**http://localhost:4502/etc/cloudservices.html**)，选择全局关闭准确定位。 无论您在云服务配置中进行何种设置，您仍然可以为各个组件打开和关闭精确定位。
   如果&#x200B;***已经创建了目标组件，并且您更改了此设置，则所做的更改不会影响这些组件。***&#x200B;您必须直接对这些组件进行任何更改。

1. 单击&#x200B;**连接到目标**&#x200B;以使用目标初始化连接。 如果连接成功，则显示消息&#x200B;**连接成功**。 单击消息上的&#x200B;**OK**，然后单击对话框上的&#x200B;**OK**。

   如果无法连接到目标，请参阅[疑难解答](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems)部分。

### 添加目标框架{#adding-a-target-framework}

配置目标云配置后，添加目标框架。 该框架标识从可用的[Client Context](/help/sites-administering/client-context.md)或[ContextHub](/help/sites-developing/ch-configuring.md)组件发送到Adobe Target的默认参数。 目标使用参数确定应用于当前上下文的区段。

您可以为单个目标配置创建多个框架。 当您需要将一组不同的参数发送到网站不同部分的目标时，多个框架非常有用。 为需要发送的每组参数创建一个框架。 将网站的每个部分与相应的框架相关联。 请注意，网页一次只能使用一个框架。

1. 在目标配置页面上，单击“可用框架”旁边的&#x200B;**+**（加号）。
1. 在“创建框架”对话框中，指定&#x200B;**标题**，选择&#x200B;**Adobe Target框架**，然后单击&#x200B;**创建**。

   ![chlimage_1-161](assets/chlimage_1-161.png)

   将打开框架页面。 Sidekick提供的组件表示您可以映射的[Client Context](/help/sites-administering/client-context.md)或[ContextHub](/help/sites-developing/ch-configuring.md)中的信息。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 拖动表示要用于映射到放置目标的数据的Client Context组件。 或者，将&#x200B;**ContextHub Store**&#x200B;组件拖到框架中。

   >[!NOTE]
   映射时，参数会通过简单字符串传递到mbox。 无法从ContextHub映射数组。

   例如，要使用关于站点访问者的&#x200B;**用户档案数据**&#x200B;来控制目标活动，请将&#x200B;**用户档案数据**&#x200B;组件拖到页面。 将显示可用于映射到用户档案参数的目标数据变量。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 通过选中相应列中的&#x200B;**Share**&#x200B;复选框，选择要在Adobe Target系统中显示的变量。

   ![chlimage_1-164](assets/chlimage_1-164.png)

   >[!NOTE]
   同步参数只是一种方式——从AEM到Adobe Target。

将创建您的框架。 要将框架复制到发布实例，请使用Sidekick中的&#x200B;**激活框架**&#x200B;选项。

### 将活动与目标云配置{#associating-activities-with-the-target-cloud-configuration}关联

将您的[AEM活动](/help/sites-authoring/activitylib.md)与您的目标云配置关联，以便您能够镜像[Adobe Target](https://docs.adobe.com/content/help/en/target/using/experiences/offers/manage-content.html)中的活动。

>[!NOTE]
可用的活动类型由以下因素决定：
* 如果对 AEM 端上用来连接到 Adobe Target 的 Adobe Target 租户 (clientcode) 启用了 **xt_only** 选项，则您&#x200B;**只**&#x200B;能在 AEM 中创建 XT 活动。

* 如果&#x200B;**未**&#x200B;对 Adobe Target 租户 (clientcode) 启用 **xt_only** 选项，则可以在 AEM 中创建 XT 活动&#x200B;**和** A/B 活动。

**另请注意：****xt_only** 选项是对特定 Target 租户 (clientcode) 应用的设置，只能直接在 Adobe Target 中进行修改。您无法在 AEM 中启用或禁用此选项。

### 将目标框架与站点{#associating-the-target-framework-with-your-site}关联

在AEM中创建目标框架后，将网页与框架关联。 页面上的目标组件会将框架定义的数据发送至Adobe Target进行跟踪。 （请参阅[内容定位](/help/sites-authoring/content-targeting-touch.md)。）

将页面与框架关联后，子页面将继承关联。

1. 在&#x200B;**站点**&#x200B;控制台中，导航到要配置的站点。
1. 使用[快速操作](/help/sites-authoring/basic-handling.md#quick-actions)或[选择模式](/help/sites-authoring/basic-handling.md)，选择&#x200B;**视图属性。**
1. 选择&#x200B;**Cloud Services**&#x200B;选项卡。
1. 点按／单击&#x200B;**编辑**。
1. 点按／单击&#x200B;**Cloud Service配置**&#x200B;下的&#x200B;**添加配置**，然后选择&#x200B;**Adobe Target**。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 在&#x200B;**配置引用**&#x200B;下选择您想要的框架。

   >[!NOTE]
   确保选择您创建的特定&#x200B;**框架**，而不是创建它时所依据的目标云配置。

1. 点按／单击&#x200B;**完成**。
1. 激活网站的根页面，将其复制到发布服务器。 （请参阅[如何发布页面](/help/sites-authoring/publishing-pages.md)。）

   >[!NOTE]
   如果您附加到页面的框架尚未激活，则会打开一个向导，通过该向导也可以发布页面。

## 目标连接问题疑难解答{#troubleshooting-target-connection-problems}

执行以下任务以排除连接到目标时出现的问题：

* 确保您提供的用户凭据正确无误。
* 确保AEM实例可以连接到目标服务器。 例如，确保防火墙规则不会阻止出站AEM连接，或将AEM配置为使用必要的代理。
* 在AEM错误日志中查找有用的消息。 error.log文件位于安装AEM的&#x200B;**crx-quickstart/logs**&#x200B;目录中。
* 在Adobe Target编辑活动时，URL指向localhost。 通过将AEM externalizer设置为正确的URL，解决此问题。

