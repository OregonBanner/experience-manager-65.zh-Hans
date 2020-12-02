---
title: 与Livefyre集成
seo-title: 与Livefyre集成
description: 了解如何将Livefyre行业领先的特选功能与AEM 6.5实例集成，使您能够在几分钟内将宝贵的用户生成内容(UGC)从社交网络发布到您的网站。
seo-description: 了解如何将Livefyre与AEM 6.5集成和使用。
uuid: c355705d-6e0f-4a33-aa1f-d2d1c818aac0
contentOwner: ind14750
content-type: reference
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: bb3fcb53-b8c3-4b1d-9125-4715f34ceb0b
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 1%

---


# 与Livefyre集成{#integrating-with-livefyre}

了解如何将Livefyre行业领先的特选功能与AEM 6.5实例集成，使您能够在几分钟内将宝贵的用户生成内容(UGC)从社交网络发布到您的网站。

## 入门 {#getting-started}

### 为AEM {#install-livefyre-package-for-aem}安装Livefyre包

AEM 6.5附带预安装的Livefyre功能包1.2.6。 此包仅包括与AEM Sites的有限Livefyre集成，在安装更新的包之前必须卸载它。 通过最新的包，您可以体验到Livefyre与AEM的完全集成，包括站点、资产和商务。

>[!NOTE]
>
>AEM-LF包的某些功能取决于社交组件框架(SCF)。 如果您将Livefyre功能包用作非社区站点的一部分，则必须在网站的作者客户端库中声明&#x200B;*cq.social.scf*&#x200B;为依赖关系。 如果您将LF功能包用作社区网站的一部分，应已声明此依赖关系。

1. 在AEM主页上，单击左边栏上的&#x200B;**工具**&#x200B;图标。
1. 导航到&#x200B;**部署>包**。
1. 在“包管理器”中，滚动直到您看到预安装的Livefyre功能包，然后单击包标题&#x200B;**cq-social-livefyre-pkg-1.2.6.zip**&#x200B;以展开选项。
1. 单击&#x200B;**更多>卸载**。

   ![livefyre-aem-uninstall-64](assets/livefyre-aem-uninstall-64.png)

1. 从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下载Livefyre包。

1. 从包管理器中，安装下载的包。 有关在AEM中使用软件分发和软件包的更多信息，请参见[如何使用软件包](/help/sites-administering/package-manager.md)

   ![livefyre-aem4-6-4](assets/livefyre-aem4-6-4.png)

   您的Livefyre-AEM包现已安装。 在开始使用集成功能之前，必须先配置AEM才能使用Livefyre。

   有关功能包的详细信息和发行说明，请参阅[功能包](https://helpx.adobe.com/experience-manager/6-3/release-notes/feature-packs-release-notes.html)。

### 将AEM配置为使用Livefyre:创建配置文件夹{#configure-aem-to-use-livefyre-create-a-configuration-folder}

1. 在AEM主页上，单击左边栏中的&#x200B;**工具**&#x200B;图标，然后导航到&#x200B;**常规>配置浏览器**。
   * 有关详细信息，请参阅[配置浏览器](/help/sites-administering/configurations.md)文档。
1. 单击&#x200B;**创建**&#x200B;以打开创建配置对话框。
1. 命名配置并选中&#x200B;**云配置**&#x200B;复选框。

   这将在&#x200B;**工具>部署> Livefyre配置**&#x200B;下创建一个文件夹，其名称为提供。

   ![livefyre-aem-create-config-folder](assets/livefyre-aem-create-config-folder.png)

### 将AEM配置为使用Livefyre:创建Livefyre配置{#configure-aem-to-use-livefyre-create-a-livefyre-configuration}

将AEM配置为使用您组织的Livefyre许可证凭据，允许Livefyre和AEM之间进行通信。

1. 在AEM主页上，单击左边栏中的&#x200B;**工具**&#x200B;图标，然后导航到&#x200B;**部署> Livefyre配置**。
1. 选择要在其中创建新Livefyre配置的配置文件夹，然后单击&#x200B;**创建**。

   ![create-livefyre-configuration1](assets/create-livefyre-configuration1.png)

   >[!NOTE]
   >
   >在向文件夹添加Livefyre配置之前，文件夹的属性中必须启用云配置。 在[配置浏览器中创建和管理配置文件夹。](/help/sites-administering/configurations.md)
   >
   >不能为配置创建名称——该配置由其所在文件夹的路径引用。 每个文件夹只能有一个配置。

1. 选择新创建的Livefyre配置卡，然后单击&#x200B;**属性**。

   ![create-livefyre-configuration2](assets/create-livefyre-configuration2.png)

1. 输入贵组织的Livefyre凭据，然后单击&#x200B;**确定**。

   ![configure-aem2](assets/configure-aem2.png)

   要访问此信息，请打开Livefyre Studio，然后导航到&#x200B;**设置>集成设置>凭据**。

   您的AEM实例现已配置为使用Livefyre，并且您可以使用集成功能。

### 自定义单点登录集成{#customize-single-sign-on-integration}

Livefyre for AEM软件包包括AEM Communities用户档案与Livefyre的SSO服务之间的现成集成。

当用户登录AEM站点时，他们也会登录到Livefyre社交组件。 当注销用户尝试使用需要身份验证的Livefyre组件功能（如上传照片）时，Livefyre组件会启动用户身份验证。

默认身份验证集成可能并不适合每个站点。 为了最好地匹配站点模板中的身份验证流程，您可以覆盖默认的Livefyre身份验证委托，以满足您的需求。 使用以下步骤：

1. 使用CRXDE Lite将&#x200B;*/libs/social/integrations/livefyre/components/authorizablecomponent/authclientlib*&#x200B;复制到&#x200B;*/apps/social/integrations/components/authorizablecomponent/authclientlib*。
1. 编辑并保存&#x200B;*/apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib/auth.js*&#x200B;以实施满足您需求的Livefyre身份验证委托。

   有关自定义身份验证委托的详细信息，请参阅[标识集成](https://answers.livefyre.com/developers/identity-integration/)。

   有关AEM Clientlibs的详细信息，请参阅[使用客户端库](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/clientlibs.html)。

## 将Livefyre与AEM Sites一起使用{#use-livefyre-with-aem-sites}

### 将Livefyre组件添加到页面{#add-livefyre-components-to-a-page}

在将Livefyre组件添加到站点中的页面之前，您必须通过从父页面继承Livefyre云配置或将配置直接添加到页面来为页面启用Livefyre。 有关如何在您的网站上包含云服务，请参阅您的实施。

为页面启用Livefyre后，必须将容器配置为允许Livefyre组件。 有关如何启用不同组件的说明，请参阅[在设计模式下配置组件](https://helpx.adobe.com/experience-manager/6-3/sites/authoring/using/default-components-designmode.html)。

>[!NOTE]
>
>在“自定义单点登录集成”中配置身份验证后，要求进行身份验证的应用程序才能运行。

1. 在设计模式下，从&#x200B;**组件**&#x200B;侧面板中，从菜单中选择&#x200B;**Livefyre**&#x200B;以将列表限制为可用的Livefyre组件。

   ![livefyre-add](assets/livefyre-add.png)

1. 选择一个Livefyre组件，然后将其拖动到页面上的位置。
1. 选择是创建新的Livefyre应用程序还是嵌入现有应用程序。

   如果嵌入现有应用程序，AEM将要求您选择该应用程序。 如果创建新应用程序，则需要先填充该应用程序，然后才能显示任何内容。 当为页面启用Livefyre云配置时，将在选择的Livefyre站点和网络中创建应用程序。

   有关插入组件的详细信息，请参阅[编辑页面内容](https://helpx.adobe.com/experience-manager/6-3/sites/authoring/using/editing-content.html)。

### 编辑AEM页面的Livefyre组件。{#edit-a-livefyre-component-for-an-aem-page}

您只能在Livefyre Studio中配置和编辑Livefyre组件。 来自AEM:

1. 单击要配置的Livefyre组件。
1. 单击&#x200B;**配置**&#x200B;图标（扳手）以打开配置对话框。
1. 单击&#x200B;**要编辑此组件，请转至Livefyre Studio**。
1. 在Livefyre Studio中编辑应用程序。

## 将Livefyre与AEM Assets一起使用{#use-livefyre-with-aem-assets}

### 请求权利并将UGC导入AEM Assets{#request-rights-and-import-ugc-into-aem-assets}

您可以使用UGC导入程序将Twitter和Instagram用户生成的内容(UGC)从Livefyre Studio导入AEM Assets。 选择要导入的内容后，您必须先请求对内容的权限，然后才能完成导入。

>[!NOTE]
>
>在使用资产导入UGC之前，您必须在Livefyre Studio中设置社交帐户和权限请求帐户。 请参阅[设置：权限请求](https://docs.adobe.com/content/help/en/livefyre/using/rights-requests/c-how-requesting-rights-works.html)以了解更多信息。

要将UGC导入AEM Assets:

1. 从AEM主页，导航到&#x200B;**资产>文件**。
1. 单击&#x200B;**创建**，然后单击&#x200B;**导入UGC。**

   ![livefyre-aem-import-ugc](assets/livefyre-aem-import-ugc.png)

1. 查找内容：

   * 单击“UGC库”选项卡，即可从Livefyre访问。 使用过滤器和搜索从UGC库中查找内容。
   * 点击Twitter或Instagram选项卡，从Twitter和Instagram上访问。 使用搜索或过滤器查找内容。

1. 选择要导入的资产。 您选择的资产会自动计数并保存在&#x200B;**Selected**&#x200B;选项卡下。
1. **可选**:单击“选 **** 择的”选项卡并查看要导入的选定UGC内容。
1. 单击&#x200B;**下一步**。

   ![livefyre-aem-import-ugc2](assets/livefyre-aem-import-ugc2.png)

1. 对于权限请求，请为每个资产选择以下选项之一：

   对于Instagram:

   * **手动请** 求权利，获取可复制粘贴的消息，并通过Instagram手动发送给内容所有者。
   * **手动属性内** 容权限可覆盖单个资产的权限。

   >[!NOTE]
   >
   >由于更新影响来自非业务用户帐户的内容的汇总，我们无法再代表您发布评论或自动检查作者的回复。 [单击此处了解更多信息](https://developers.facebook.com/blog/post/2018/04/04/facebook-api-platform-product-changes/)。

   ![livefyre-aem-import-ugc3-6-4](assets/livefyre-aem-import-ugc3-6-4.png)

   对于Twitter:

   * **消息** 作者：向内容所有者发送消息，请求对资产拥有权限。
   * **手动属性内** 容权限可覆盖单个资产的权限。


1. 单击&#x200B;**导入**。

   如果您发送了Twitter权限请求，内容所有者将在其帐户上看到权限请求消息：

   ![livefyre-aem-rights-request-twitter](assets/livefyre-aem-rights-request-twitter.png)

   >[!NOTE]
   >
   >Twitter对来自同一帐户的相同请求设置了限制。 导入多个资产时，请单独修改消息以避免被标记。

1. 单击右上角的&#x200B;**完成**&#x200B;以完成“权限请求”工作流。

   您可以在Livefyre Studio中查看某个资产的待处理权限请求的状态。 如果内容正在等待权限请求，则在授予权限之前，资产不会在AEM Assets显示。 当授予权利请求时，资产将自动显示在AEM Assets。

   对于Instagram，您必须跟踪内容所有者的响应并在授予内容权限时手动授予权限。

## 将Livefyre与AEM Commerce {#use-livefyre-with-aem-commerce}结合使用

### 使用AEM Commerce {#import-product-catalogs-into-livefyre-with-aem-commerce}将产品目录导入Livefyre

AEM Commerce用户可以将他们现有的产品目录无缝集成到Livefyre中，以推动用户参与Livefyre的可视化应用程序。

导入产品目录后，这些产品会实时显示在您的Livefyre实例中。 如果您编辑或删除AEM Commerce产品目录中的项目，这些更改将在Livefrye中自动更新。

1. 确保在AEM实例上安装了最新的Livefyre for AEM包。
1. 从AEM主页，导航到&#x200B;**AEM Commerce**。
1. 创建新集合或使用现有集合。
1. 将指针悬停在集合上并单击&#x200B;**集合属性**（铅笔图标）。
1. 选中&#x200B;**同步到Livefyre**。
1. 填写&#x200B;**Livefyre页面前缀**，将此集合链接到AEM中的特定页面。

   页面前缀定义环境中开始搜索产品页面的根路径。 Livefyre选择与其关联的相应产品的第一个页面。 要获取不同产品的不同页面，需要多个集合。

## AEM Livefyre应用程序支持列表{#aem-support-matrix-for-livefyre-apps}

| Livefyre应用程序 | AEM 6.1 | AEM 6.2 | AEM 6.3 | AEM 6.4 |
|---|---|---|---|---|
| 轮播 | X | X | X | X |
| 聊天 | X | X | X | X |
| 评论 | X | X | X | X |
| 幻灯片 |  | X | X | X |
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

