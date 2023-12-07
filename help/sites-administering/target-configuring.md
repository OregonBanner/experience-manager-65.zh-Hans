---
title: 手动配置与Adobe Target的集成
description: 了解如何手动配置与Adobe Target的集成。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 0f710685-dc4f-4333-9847-d002b2637d08
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 28%

---

# 手动配置与Adobe Target的集成 {#manually-configuring-the-integration-with-adobe-target}

您可以修改使用向导时所做的选择加入向导配置，也可以不使用向导手动与Adobe Target集成。

## 修改选择加入向导配置 {#modifying-the-opt-in-wizard-configurations}

此 [选择加入向导](/help/sites-administering/opt-in.md) 该 [将AEM与Adobe Target集成](/help/sites-administering/target.md) 自动创建一个名为已设置Target配置的Target云配置。 该向导还会为名为“已设置的Target框架”的云配置创建一个Target框架。 您可以修改云配置和框架的属性（如有必要）。

您还可以通过配置A4T Analytics Cloud配置，将Adobe Target配置为在定位内容时使用Adobe Target作为报表源。

要找到云配置和框架，请导航到 **Cloud Service** via **工具** > **部署** > **云**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))在Adobe Target下，单击 **显示配置**.

### 已设置的目标配置属性 {#provisioned-target-configuration-properties}

以下属性值用于选择加入向导创建的已设置Target配置云配置中：

* **客户端代码：** 在选择加入向导中输入。
* **电子邮件：** 在选择加入向导中输入。
* **密码：** 在选择加入向导中输入。
* **API类型：** REST
* **从Adobe Target同步区段：** 已选定。

* **客户端库：** mbox.js.
* **使用DTM提供客户端库：** 未选择。 如果符合以下条件，请选择此选项 [使用DTM](/help/sites-administering/dtm.md) 或其他标记管理系统来托管mbox.js或AT.js文件。 Adobe建议您使用DTM而不是AEM来交付库。

* **自定义mbox.js：** 未指定以便使用默认的mbox.js文件。 根据需要指定要使用的自定义mbox.js文件。 仅当您选择了mbox.js时显示。
* **自定义AT.js：** 未指定以便使用默认的AT.js文件。 根据需要指定要使用的自定义AT.js文件。 仅当您选择了AT.js时才显示。

>[!NOTE]
>
>在AEM 6.3中，您可以选择Target库文件， [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/)，是适用于Adobe Target的新实施库，专为典型的Web实施和单页应用程序而设计。
>
>AT.js 对 mbox.js 库进行了多项改进：
>
>* 缩短了 Web 实现的页面加载时间
>* 提高了安全性
>* 改善了针对单页应用程序的实施选项
>* AT.js包含target.js中包含的组件，因此不再需要调用target。

<!-- OLD URL WHICH IS 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### 已设置的目标框架属性 {#provisioned-target-framework-properties}

选择加入向导创建的预配目标框架配置为从配置文件数据存储中发送上下文数据。 默认情况下，存储区的年龄和性别数据项会发送到Target。 您的解决方案可能需要发送其他参数。

![已设置的目标框架](assets/chlimage_1-158.png)

您可以配置框架以向Target发送其他上下文信息，如中所述 [添加Target框架](/help/sites-administering/target-configuring.md#adding-a-target-framework).

### 配置A4T Analytics Cloud配置 {#configuring-a-t-analytics-cloud-configuration}

您可以将Adobe Target配置为在定位内容时使用Adobe Analytics作为报表源。

>[!NOTE]
>
>用户凭据身份验证（旧版）不适用于A4T（适用于Target和Analytics）。 因此，客户应使用IMS身份验证而不是User-Credential身份验证。

为此，您可以指定将您的Adobe Target云配置连接到的A4T云配置：

1. 导航到 **Cloud Service** 通过 **AEM徽标** > **工具** > **部署** > **Cloud Service**.
1. 在 **Adobe Target** 部分中，单击&#x200B;**立即配置**。
1. 重新连接到您的Adobe Target配置。
1. 在 **A4T Analytics Cloud配置** 下拉菜单中，选择框架。

   >[!NOTE]
   >
   >只有为A4T启用的Analytics配置可用。
   >
   >使用AEM配置A4T时，您可能会看到缺少条目的配置引用。 要能够选择分析框架，请执行以下操作：
   >
   >1. 导航到 **工具** > **常规** > **CRXDE Lite**.
   1. 导航至 [A4T分析配置对话框](#a4t-analytics-config-dialog) （见下文）
   1. 设置属性 **disable** 到 **false**.
   1. 单击&#x200B;**全部保存**。

#### A4T分析配置对话框 {#a4t-analytics-config-dialog}

```xml
/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig
```

![AdobeTargetSettings](assets/adobe-target-settings.jpg)

单击 **确定**. 使用Adobe Target定位内容时，您能够 [选择您的报表源](/help/sites-authoring/content-targeting-touch.md).

## 手动与Adobe Target集成 {#manually-integrating-with-adobe-target}

手动与Adobe Target集成，而不是使用选择加入向导。

>[!NOTE]
>
Target库文件， [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/)，是适用于Adobe Target的新实施库，专为典型的Web实施和单页应用程序而设计。 Adobe 建议您使用 AT.js 而不是 mbox.js 作为客户端库。
>
AT.js 对 mbox.js 库进行了多项改进：
>
* 缩短了 Web 实现的页面加载时间
* 提高了安全性
* 改善了针对单页应用程序的实施选项
* AT.js 包含 target.js 具有的组件，因此不再调用 target.js
>
您可以在&#x200B;**客户端库**&#x200B;下拉菜单中选择 AT.js 或 mbox.js。

<!-- OLD URL from above was 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### 创建 Target 云配置 {#creating-a-target-cloud-configuration}

要启用 AEM 以便与 Adobe Target 交互，请创建 Target 云配置。要创建配置，您需要提供 Adobe Target 客户端代码和用户凭据。

您只需创建一次 Target 云配置，因为您可以将该配置与多个 AEM 活动关联。如果您有多个 Adobe Target 客户端代码，请为每个客户端代码创建一个配置。

您可以配置云配置以从 Adobe Target 同步片段。如果启用同步，则在保存云配置时，将在后台从Target导入区段。

使用以下过程可在 AEM 中创建 Target 云配置：

1. 导航到 **Cloud Service** 通过 **AEM徽标** > **工具** > **Cloud Service** > **旧版Cloud Service**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   此 **Cloud Service** “概述”页面将打开。

1. 在 **Adobe Target** 部分中，单击&#x200B;**立即配置**。
1. 在&#x200B;**创建配置**&#x200B;对话框中：

   1. 为配置提供&#x200B;**标题**。
   1. 选择 **Adobe Target 配置**&#x200B;模板。
   1. 单击&#x200B;**创建**。

   此时将打开编辑对话框。

   ![AdobeTargetSettings](assets/adobe-target-settings.jpg)

   >[!NOTE]
   >
   使用AEM配置A4T时，您可能会看到缺少条目的配置引用。 要能够选择分析框架，请执行以下操作：
   >
   1. 导航到 **工具** > **常规** > **CRXDE Lite**.
   1. 导航到 **/libs/cq/analytics/components/testandtargetpage/dialog/items/tables/items/tab1_general/items/a4tAnalyticsConfig**
   1. 设置属性 **disable** 到 **false**.
   1. 单击&#x200B;**全部保存**。

1. 在对话框中，提供这些属性的值。

   * **客户端代码**：Target 帐户的客户端代码
   * **电子邮件**：Target帐户电子邮件。
   * **密码**：Target帐户密码。
   * **API类型**：REST或XML
   * **A4T Analytics Cloud配置**：选择用于Target活动目标和量度的Analytics Cloud配置。 如果您在定位内容时使用Adobe Analytics作为报表源，则需要此配置。 如果您看不到云配置，请参阅中的注释 [配置A4T Analytics Cloud配置](#configuring-a-t-analytics-cloud-configuration).

   * **使用准确定位：**&#x200B;默认情况下，此复选框处于选中状态。如果选中，云服务配置会等待上下文加载完后再加载内容。 请参阅以下注释。
   * **从Adobe Target同步区段：** 选择此选项后，您可以下载Target中定义的区段以在AEM中使用它们。 当API类型属性为REST时，选择此选项，因为内联区段不受支持，您必须从Target使用区段。 (AEM术语“区段”等同于Target“受众”。)
   * **客户端库：** 选择需要mbox.js还是AT.js客户端库。
   * **使用DTM提供客户端库**  — 选择此选项可使用DTM或其他标记管理系统中的AT.js或mbox.js。 配置 [dtm集成](/help/sites-administering/dtm.md) 以使用此选项。 Adobe建议您使用DTM而不是AEM来交付库。
   * **自定义mbox.js**：如果选中DTM框或使用默认的mbox.js，则保留为空。 或者，上传您的自定义mbox.js。 仅当您选择了mbox.js时显示。
   * **自定义AT.js**：如果选中DTM框或使用默认的AT.js，则保留为空。 或者，上传您的自定义AT.js。 仅当您选择了AT.js时才显示。

   >[!NOTE]
   >
   默认情况下，当您选择加入 Adobe Target 配置向导时，将启用“准确定位”。
   >
   准确定位意味着，云服务配置将等到上下文加载完后，再加载内容。因此，就性能而言，准确定位可能会导致加载内容前有几毫秒的延迟。
   >
   对于创作实例，“准确定位”始终处于启用状态。但在发布实例上，您可以通过清除云服务配置中“准确定位”旁边的复选标记来选择全局关闭准确定位 (**http://localhost:4502/etc/cloudservices.html**)。无论您在云服务配置中的设置如何，您都可以为各个组件打开和关闭“准确定位”。
   >
   如果您&#x200B;***已经***&#x200B;创建目标组件并更改此设置，则您的更改不会影响这些组件。直接更改这些组件。

1. 单击 **连接到Target** 初始化与Target的连接。 如果连接成功，则将显示消息&#x200B;**连接成功**。单击消息上的&#x200B;**确定**，然后单击对话框上的&#x200B;**确定**。

   如果无法连接到 Target，请参阅[疑难解答](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems)部分。

### 添加 Target 框架 {#adding-a-target-framework}

配置 Target 云配置后，可以添加 Target 框架。此框架标识从可用发送到Adobe Target的默认参数 [客户端上下文](/help/sites-administering/client-context.md) 或 [ContextHub](/help/sites-developing/ch-configuring.md) 组件。 Target 使用参数来确定适用于当前上下文的分段。

您可以为单个 Target 配置创建多个框架。当您必须为网站的不同部分向Target发送一组不同的参数时，多个框架会很有用。 为您发送的每组参数创建一个框架。 将网站的每个部分与适当的框架关联。一个网页一次只能使用一个框架。

1. 在Target配置页面上，单击 **+** （加号）图标。
1. 在“创建框架”对话框中，指定&#x200B;**标题**，选择 **Adobe Target 框架**，然后单击&#x200B;**创建**。

   ![“创建框架”对话框](assets/chlimage_1-161.png)

   这将打开框架页面。Sidekick提供的组件表示来自以下各项的信息： [客户端上下文](/help/sites-administering/client-context.md) 或 [ContextHub](/help/sites-developing/ch-configuring.md) 可以映射的图象。

   ![框架组件](assets/chlimage_1-162.png)

1. 将表示要用于映射的数据的客户端上下文组件拖动到放置目标。或者，拖动&#x200B;**ContextHub存储** 组件添加到框架。

   >[!NOTE]
   >
   映射时，参数通过简单字符串传递给 mbox。无法从 ContextHub 映射数组。

   例如，要使用 **配置文件数据** 关于要控制Target促销活动的网站访客，请拖动 **配置文件数据** 组件添加到页面。 可用于映射到 Target 参数的配置文件数据变量随即显示。

   ![配置文件数据](assets/chlimage_1-163.png)

1. 通过选中相应列中的&#x200B;**共享**&#x200B;复选框，选择要对 Adobe Target 系统可见的变量。

   ![共享](assets/chlimage_1-164.png)

   >[!NOTE]
   >
   同步参数是唯一方式 – 从 AEM 到 Adobe Target。

此时将创建您的框架。要将框架复制到发布实例，请使用 sidekick 中的&#x200B;**激活框架**&#x200B;选项。

### 将活动与Target云配置关联  {#associating-activities-with-the-target-cloud-configuration}

关联您的 [AEM活动](/help/sites-authoring/activitylib.md) 使用Target云配置，以便镜像中的活动 [Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).

>[!NOTE]
>
可用的活动类型由以下因素决定：
>
>
* 如果 **xt_only** 在AEM端使用的Adobe Target租户(clientcode)上启用选项以连接到Adobe Target，然后您可以创建 **仅限** AEM XT活动。
>
* 如果 **xt_only** 选项为 **非** 已在Adobe Target租户(clientcode)上启用，然后您可以创建 **两者** AEM中的XT和A/B活动。
>
**其他说明：** **xt_only** 选项是对特定Target租户(clientcode)应用的设置，只能在Adobe Target中直接修改。 您无法在 AEM 中启用或禁用此选项。

### 将Target框架与您的站点关联 {#associating-the-target-framework-with-your-site}

在AEM中创建Target框架后，将网页与该框架关联。 页面上的目标组件会将框架定义的数据发送到Adobe Target进行跟踪。 (请参阅 [内容定位](/help/sites-authoring/content-targeting-touch.md).)

将页面与框架关联时，子页面将继承关联。

1. 在 **站点** 控制台中，导航到要配置的站点。
1. 使用 [快速操作](/help/sites-authoring/basic-handling.md#quick-actions) 或 [选择模式](/help/sites-authoring/basic-handling.md)，选择 **查看属性。**
1. 选择&#x200B;**云服务**&#x200B;选项卡。
1. 单击 **编辑**.
1. 单击 **添加配置** 下 **Cloud Service配置** 并选择 **Adobe Target**.

   ![添加配置](assets/chlimage_1-165.png)

1. 选择所需的框架 **配置引用**.

   >[!NOTE]
   >
   确保选择特定的 **框架** 中创建的，而不是在其中创建它的Target云配置。

1. 单击&#x200B;**完成**。
1. 激活网站的根页面，以便将其复制到发布服务器。 (请参阅 [如何发布页面](/help/sites-authoring/publishing-pages.md).)

   >[!NOTE]
   >
   如果尚未激活您附加到页面的框架，则会打开一个向导，通过该向导也可以发布该框架。

## Target连接问题疑难解答 {#troubleshooting-target-connection-problems}

要排除连接到Target时出现的问题，可以执行以下任务：

* 确保您提供的用户凭据正确。
* 确保AEM实例可以连接到Target服务器。 例如，请确保防火墙规则未阻止出站AEM连接，或者已将AEM配置为使用必要的代理。
* 在AEM错误日志中查找有用的消息。 error.log文件位于 **crx-quickstart/logs** 安装AEM的目录。
* 在Adobe Target中编辑活动时，URL指向本地主机。 通过将AEM外部化器设置为正确的URL来解决此理解。
