---
title: 与 Livefyre 集成
seo-title: 与 Livefyre 集成
description: 了解如何将Livefyre业界领先的管理功能与您的AEM 6.5实例相集成，从而在几分钟内将用户生成的有价值的内容(UGC)从社交网络发布到您的网站。
seo-description: 了解如何将Livefyre与AEM 6.5集成和使用。
uuid: c355705d-6e0f-4a33-aa1f-d2d1c818aac0
contentOwner: ind14750
content-type: reference
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: bb3fcb53-b8c3-4b1d-9125-4715f34ceb0b
exl-id: 6327b571-4c7f-4a5e-ba93-45d0a064aa1f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 2%

---

# 与 Livefyre 集成{#integrating-with-livefyre}

了解如何将Livefyre业界领先的管理功能与您的AEM 6.5实例相集成，从而在几分钟内将用户生成的有价值的内容(UGC)从社交网络发布到您的网站。

## 入门 {#getting-started}

### 安装适用于AEM {#install-livefyre-package-for-aem}的Livefyre包

AEM 6.5预安装了Livefyre功能包1.2.6。 此包仅包含与AEM Sites的有限Livefyre集成，在安装更新的包之前，必须先卸载该包。 通过最新的产品包，您可以体验到Livefyre与AEM的完整集成，包括Sites、Assets和Commerce。

>[!NOTE]
>
>AEM-LF包的某些功能取决于社交组件框架(SCF)。 如果您将Livefyre功能包用作非社区站点的一部分，则必须在网站的作者clientlibs中声明&#x200B;*cq.social.scf*&#x200B;为依赖项。 如果您将LF功能包用作社区网站的一部分，则应该已声明此依赖项。

1. 在AEM主页上，单击左边栏上的&#x200B;**工具**&#x200B;图标。
1. 导航到&#x200B;**Deployment > Packages**。
1. 在包管理器中，滚动直到您看到预安装的Livefyre功能包为止，然后单击包标题&#x200B;**cq-social-livefyre-pkg-1.2.6.zip**&#x200B;以展开选项。
1. 单击&#x200B;**更多>卸载**。

   ![livefyre-aem-uninstall-64](assets/livefyre-aem-uninstall-64.png)

1. 从[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下载Livefyre包。

1. 从包管理器中，安装下载的包。 请参阅[如何使用包](/help/sites-administering/package-manager.md) ，以了解有关在AEM中使用Software Distribution和包的详细信息

   ![livefyre-aem4-6-4](assets/livefyre-aem4-6-4.png)

   您的Livefyre-AEM包现已安装完成。 您必须先配置AEM以使用Livefyre，然后才能开始使用集成功能。

   有关功能包的更多信息和发行说明，请参阅[功能包](https://helpx.adobe.com/cn/experience-manager/6-3/release-notes/feature-packs-release-notes.html)。

### 配置AEM以使用Livefyre:创建配置文件夹{#configure-aem-to-use-livefyre-create-a-configuration-folder}

1. 在AEM主页上，单击左边栏中的&#x200B;**工具**&#x200B;图标，然后导航到&#x200B;**常规>配置浏览器**。
   * 有关更多信息，请参阅[配置浏览器](/help/sites-administering/configurations.md)文档。
1. 单击&#x200B;**创建**&#x200B;以打开创建配置对话框。
1. 命名您的配置并选中&#x200B;**云配置**&#x200B;复选框。

   这将在&#x200B;**工具>部署> Livefyre配置**&#x200B;下创建一个文件夹，其中提供了名称。

   ![livefyre-aem-create-config-folder](assets/livefyre-aem-create-config-folder.png)

### 配置AEM以使用Livefyre:创建Livefyre配置{#configure-aem-to-use-livefyre-create-a-livefyre-configuration}

配置AEM以使用贵组织的Livefyre许可证凭据，从而允许Livefyre与AEM之间进行通信。

1. 在AEM主页上，单击左边栏中的&#x200B;**工具**&#x200B;图标，然后导航到&#x200B;**Deployment > Livefyre Configuration**。
1. 选择要在其中创建新Livefyre配置的配置文件夹，然后单击&#x200B;**创建**。

   ![create-livefyre-configuration1](assets/create-livefyre-configuration1.png)

   >[!NOTE]
   >
   >文件夹的属性中必须启用云配置，然后才能向其添加Livefyre配置。 配置文件夹在[配置浏览器中创建和管理。](/help/sites-administering/configurations.md)
   >
   >不能为配置创建名称，该配置由其所在文件夹的路径引用。 每个文件夹只能有一个配置。

1. 选择新创建的Livefyre配置卡，然后单击&#x200B;**属性**。

   ![create-livefyre-configuration2](assets/create-livefyre-configuration2.png)

1. 输入贵组织的Livefyre凭据，然后单击&#x200B;**确定**。

   ![configure-aem2](assets/configure-aem2.png)

   要访问此信息，请打开Livefyre Studio并导航到&#x200B;**设置>集成设置>凭据**。

   您的AEM实例现已配置为使用Livefyre，并且您可以使用集成功能。

### 自定义单点登录集成{#customize-single-sign-on-integration}

Livefyre for AEM包中包含AEM Communities配置文件与Livefyre的SSO服务之间的现成集成。

当用户登录您的AEM网站时，他们也会登录到Livefyre社交组件。 当注销的用户尝试使用需要身份验证的Livefyre组件功能（如上传照片）时，Livefyre组件会启动用户身份验证。

默认身份验证集成可能并非适用于每个网站。 为了最好地匹配网站模板中的身份验证流程，您可以覆盖默认的Livefyre身份验证委托以满足您的需求。 使用以下步骤：

1. 使用CRXDE Lite，将&#x200B;*/libs/social/integrets/livefyre/components/authorizablecomponent/authclientlib*&#x200B;复制到&#x200B;*/apps/social/integritations/livefyre/components/authorizablecomponent/authclientlib*。
1. 编辑并保存&#x200B;*/apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib/auth.js*，以实施满足您需求的Livefyre Auth Delegate。

   有关自定义身份验证委托的更多信息，请参阅[身份集成](https://answers.livefyre.com/developers/identity-integration/)。

   有关AEM Clientlibs的更多信息，请参阅[使用客户端库](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/clientlibs.html)。

## 将Livefyre与AEM Sites {#use-livefyre-with-aem-sites}结合使用

### 将Livefyre组件添加到页面{#add-livefyre-components-to-a-page}

在将Livefyre组件添加到Sites中的页面之前，您必须通过从父页面继承Livefyre云配置或直接将配置添加到页面来为页面启用Livefyre。 有关如何在您的网站上包含云服务的信息，请参阅您的实施。

为页面启用Livefyre后，必须将容器配置为允许使用Livefyre组件。 有关如何启用不同组件的说明，请参阅[在设计模式下配置组件](https://helpx.adobe.com/experience-manager/6-3/sites/authoring/using/default-components-designmode.html)。

>[!NOTE]
>
>在自定义单点登录集成中配置了身份验证后，需要进行身份验证的应用程序才能正常运行。

1. 在设计模式下，从&#x200B;**Components**&#x200B;侧面板中，从菜单中选择&#x200B;**Livefyre** ，以将列表限制为可用的Livefyre组件。

   ![livefyre-add](assets/livefyre-add.png)

1. 选择一个Livefyre组件，并将其拖动到页面上的位置。
1. 选择是创建新的Livefyre应用程序还是嵌入现有应用程序。

   如果嵌入现有应用程序，则AEM会要求您选择该应用程序。 如果创建新应用程序，则需要先填充该应用程序，然后才能显示任何内容。 在为页面启用Livefyre云配置时，将在选定的Livefyre网站和网络中创建应用程序。

   有关插入组件的更多信息，请参阅[编辑页面内容](https://helpx.adobe.com/experience-manager/6-3/sites/authoring/using/editing-content.html)。

### 编辑AEM页面的Livefyre组件。{#edit-a-livefyre-component-for-an-aem-page}

您只能在Livefyre Studio中配置和编辑Livefyre组件。 从AEM:

1. 单击Livefyre组件以进行配置。
1. 单击&#x200B;**配置**&#x200B;图标（扳手）以打开配置对话框。
1. 单击&#x200B;**要编辑此组件，请转到Livefyre Studio**。
1. 在Livefyre Studio中编辑应用程序。

## 将Livefyre与AEM Assets {#use-livefyre-with-aem-assets}结合使用

### 请求权限并将UGC导入AEM Assets {#request-rights-and-import-ugc-into-aem-assets}

您可以使用UGC导入程序将Twitter和Instagram用户生成的内容(UGC)从Livefyre Studio导入AEM Assets。 选择要导入的内容后，您必须先请求内容的权限，然后才能完成导入。

>[!NOTE]
>
>在使用Assets导入UGC之前，您必须在Livefyre Studio中设置Social帐户和权限请求帐户。 请参阅[设置：权限请求](https://docs.adobe.com/content/help/en/livefyre/using/rights-requests/c-how-requesting-rights-works.html)以了解更多信息。

要将UGC导入AEM Assets，请执行以下操作：

1. 从AEM主页中，导航到&#x200B;**Assets > Files**。
1. 单击&#x200B;**创建**，然后单击&#x200B;**导入UGC。**

   ![livefyre-aem-import-ugc](assets/livefyre-aem-import-ugc.png)

1. 查找内容：

   * 单击UGC库选项卡，以从Livefyre中访问。 使用过滤器和搜索功能可从UGC库中查找内容。
   * 单击Twitter或Instagram选项卡，以从Twitter和Instagram中访问。 使用搜索或过滤器查找内容。

1. 选择要导入的资产。 您选择的资产会自动计数并保存在&#x200B;**Selected**&#x200B;选项卡下。
1. **可选**:单击选 **** 定的选项卡并查看要导入的选定UGC内容。
1. 单击&#x200B;**下一步**。

   ![livefyre-aem-import-ugc2](assets/livefyre-aem-import-ugc2.png)

1. 对于权限请求，请为每个资产选择以下选项之一：

   对于Instagram:

   * **手动请** 求权限，以获取可复制和粘贴的消息，并通过Instagram手动发送给内容所有者。
   * **手动属性内** 容权限，以覆盖单个资产的权限。

   >[!NOTE]
   >
   >由于更新影响来自非业务用户帐户的内容汇总，我们无法再代表您发布评论或自动检查作者的回复。 [单击此处了解更多信息](https://developers.facebook.com/blog/post/2018/04/04/facebook-api-platform-product-changes/)。

   ![livefyre-aem-import-ugc3-6-4](assets/livefyre-aem-import-ugc3-6-4.png)

   对于Twitter:

   * **消息** 作者向内容所有者发送消息，请求获取资产的权限。
   * **手动属性内** 容权限，以覆盖单个资产的权限。


1. 单击&#x200B;**导入**。

   如果您发送了Twitter权限请求，内容所有者将在其帐户中看到权限请求消息：

   ![livefyre-aem-rights-request-twitter](assets/livefyre-aem-rights-request-twitter.png)

   >[!NOTE]
   >
   >Twitter对来自同一帐户的相同请求有限制。 导入多个资产时，请单独修改消息以避免被标记。

1. 单击右上角的&#x200B;**Done**&#x200B;以完成权限请求工作流。

   您可以在Livefyre Studio中查看资产的待处理权限请求的状态。 如果内容等待权限请求，则在授予权限之前，资产将不会显示在AEM Assets中。 在授予权限请求后，资产会自动显示在AEM Assets中。

   对于Instagram，您必须跟踪内容所有者的响应，并在为内容授予权限时手动授予权限。

## 将Livefyre与AEM Commerce {#use-livefyre-with-aem-commerce}结合使用

### 将产品目录导入Livefyre with AEM Commerce {#import-product-catalogs-into-livefyre-with-aem-commerce}

AEM Commerce用户可以将其现有产品目录无缝集成到Livefyre中，以提高用户对Livefyre可视化应用程序的参与度。

导入产品目录后，这些产品将实时显示在您的Livefyre实例中。 如果您编辑或删除了AEM Commerce Product Catalog中的项目，则所做的更改会在Livefrye中自动更新。

1. 确保在AEM实例上安装了最新的AEM Livefyre包。
1. 从AEM主页中，导航到&#x200B;**AEM Commerce**。
1. 创建新收藏集或使用现有收藏集。
1. 将鼠标悬停在收藏集上，然后单击&#x200B;**收藏集属性**（铅笔图标）。
1. 选中&#x200B;**同步到Livefyre**。
1. 填写&#x200B;**Livefyre页面前缀**&#x200B;以将此集合链接到AEM中的特定页面。

   页面前缀用于定义环境中开始搜索产品页面的根路径。 Livefyre会选择与其关联相应产品的第一个页面。 要为不同的产品获取不同的页面，需要多个收藏集。

## AEM Livefyre应用程序支持列表{#aem-support-matrix-for-livefyre-apps}

| Livefyre应用程序 | AEM 6.1 | AEM 6.2 | AEM 6.3 | AEM 6.4 |
|---|---|---|---|---|
| 轮播 | X | X | X | X |
| 聊天 | X | X | X | X |
| 评论 | X | X | X | X |
| Filmstrip |  | X | X | X |
| LiveBlog | X | X | X | X |
| 地图 | X | X | X | X |
| 媒体墙 | X | X | X | X |
| 马赛克 | X | X | X | X |
| 轮询 |  | X | X | X |
| 审核 |  | X | X | X |
| 单卡 | X | X | X | X |
| Storify 2 |  | X | X | X |
| 热门 |  | X | X | X |
| 上传按钮 |  | X | X | X |
