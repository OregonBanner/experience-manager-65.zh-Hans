---
title: 与 Livefyre 集成
seo-title: Integrating with Livefyre
description: 了解如何将Livefyre业界领先的管理功能与您的AEM 6.5实例集成，使您能够在几分钟内将用户生成的有价值的内容(UGC)从社交网络发布到您的网站。
seo-description: Learn how to integrate and use Livefyre with AEM 6.5.
uuid: c355705d-6e0f-4a33-aa1f-d2d1c818aac0
contentOwner: ind14750
content-type: reference
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: bb3fcb53-b8c3-4b1d-9125-4715f34ceb0b
exl-id: 6327b571-4c7f-4a5e-ba93-45d0a064aa1f
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 2%

---

# 与 Livefyre 集成{#integrating-with-livefyre}

了解如何将Livefyre业界领先的管理功能与您的AEM 6.5实例集成，使您能够在几分钟内将用户生成的有价值的内容(UGC)从社交网络发布到您的网站。

## 快速入门 {#getting-started}

### 安装适用于AEM的Livefyre包 {#install-livefyre-package-for-aem}

AEM 6.5预装了Livefyre功能包1.2.6。 此软件包仅包含与AEM Sites的有限Livefyre集成，必须先卸载此软件包，然后才能安装更新的软件包。 通过最新包，您可以体验Livefyre与AEM（包括Sites、Assets和Commerce）的完全集成。

>[!NOTE]
>
>AEM-LF包的某些功能依赖于社交组件框架(SCF)。 如果您将Livefyre功能包用作非社区站点的一部分，则必须声明 *cq.social.scf* 作为网站创作clientlibs中的依赖项。 如果您将LF功能包用作Communities网站的一部分，则应已声明此依赖项。

1. 在AEM主页上，单击 **工具** 图标。
1. 导航到 **部署>包**.
1. 在包管理器中，滚动直到看到预安装的Livefyre功能包，然后单击包标题 **cq-social-livefyre-pkg-1.2.6.zip** 以展开选项。
1. 单击 **“更多”>“卸载”**.

   ![livefyre-aem-uninstall-64](assets/livefyre-aem-uninstall-64.png)

1. 从下载Livefyre包 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

1. 从包管理器中，安装下载的包。 参见 [如何使用包](/help/sites-administering/package-manager.md) 有关在AEM中使用软件分发和软件包的更多信息

   ![livefyre-aem4-6-4](assets/livefyre-aem4-6-4.png)

   现已安装Livefyre-AEM包。 在开始使用集成功能之前，必须将AEM配置为使用Livefyre。

   有关功能包的更多信息和发行说明，请参阅 [功能包](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/home.html).

### 配置AEM以使用Livefyre：创建配置文件夹 {#configure-aem-to-use-livefyre-create-a-configuration-folder}

1. 在AEM主页上，单击 **工具** 图标，然后导航到 **常规>配置浏览器**.
   * 请参阅 [配置浏览器](/help/sites-administering/configurations.md) 文档，以了解更多信息。
1. 单击 **创建** 打开“创建配置”对话框。
1. 命名您的配置并检查 **云配置** 复选框。

   这将在下创建一个文件夹 **工具>部署> Livefyre配置** 提供了名称。

   ![livefyre-aem-create-config-folder](assets/livefyre-aem-create-config-folder.png)

### 配置AEM以使用Livefyre：创建Livefyre配置 {#configure-aem-to-use-livefyre-create-a-livefyre-configuration}

将AEM配置为使用贵组织的Livefyre许可证凭据，以允许Livefyre和AEM之间的通信。

1. 在AEM主页上，单击 **工具** 图标，然后导航到 **部署> Livefyre配置**.
1. 选择要创建新Livefyre配置的配置文件夹，然后单击 **创建**.

   ![create-livefyre-configuration1](assets/create-livefyre-configuration1.png)

   >[!NOTE]
   >
   >必须先在文件夹属性中启用云配置，然后才能向文件夹中添加Livefyre配置。 配置文件夹是在中创建和管理的 [配置浏览器。](/help/sites-administering/configurations.md)
   >
   >不能为配置创建名称 — 该配置由所在文件夹的路径引用。 每个文件夹只能有一个配置。

1. 选择新创建的Livefyre配置卡，然后单击 **属性**.

   ![create-livefyre-configuration2](assets/create-livefyre-configuration2.png)

1. 输入贵组织的Livefyre凭据，然后单击 **确定**.

   ![configure-aem2](assets/configure-aem2.png)

   要访问此信息，请打开Livefyre studio并导航到 **设置>集成设置>凭据**.

   您的AEM实例现在配置为使用Livefyre，并且您可以使用集成功能。

### 自定义单点登录集成 {#customize-single-sign-on-integration}

Livefyre for AEM包中包含在AEM Communities配置文件和Livefyre的SSO服务之间现成的集成。

当用户登录AEM网站时，也会登录到Livefyre社交组件。 当注销的用户尝试使用需要身份验证的Livefyre组件功能（如上传照片）时，Livefyre组件会启动用户身份验证。

默认身份验证集成可能并非适用于每个站点。 为了与网站模板中的身份验证流程最匹配，您可以覆盖默认的Livefyre身份验证委派，以满足您的需求。 请按照以下步骤操作：

1. 使用CRXDE Lite，复制 */libs/social/integrations/livefyre/components/authorizablecomponent/authclientlib* 到 */apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib*.
1. 编辑并保存 */apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib/auth.js* 实施满足您需求的Livefyre身份验证委派。

   有关自定义身份验证委托的更多信息，请参阅 [身份集成](https://answers.livefyre.com/developers/identity-integration/).

   有关AEM Clientlibs的更多信息，请参阅 [使用客户端库](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html).

## 将Livefyre与AEM Sites结合使用 {#use-livefyre-with-aem-sites}

### 将Livefyre组件添加到页面 {#add-livefyre-components-to-a-page}

在将Livefyre组件添加到Sites中的页面之前，您必须通过从父页面继承Livefyre云配置或通过将配置直接添加到页面来为页面启用Livefyre。 请参阅您的实施，了解如何在您的网站上包含云服务。

为页面启用Livefyre后，必须将容器配置为允许Livefyre组件。 参见 [在设计模式下配置组件](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/default-components-designmode.html) 有关如何启用不同组件的说明。

>[!NOTE]
>
>在自定义单点登录集成中配置了身份验证之前，需要身份验证才能发布的应用无法正常运行。

1. 从 **组件** 在设计模式中，选择侧面板 **Livefyre** 以将列表限制为可用的Livefyre组件。

   ![livefyre-add](assets/livefyre-add.png)

1. 选择一个Livefyre组件，并将其拖动到页面上的适当位置。
1. 选择是创建新的Livefyre应用程序，还是嵌入现有应用程序。

   如果嵌入现有应用程序，AEM会要求您选择应用程序。 如果创建新应用程序，则需要在显示任何内容之前填充应用程序。 为页面启用Livefyre云配置后，应用程序将在所选的Livefyre网站和网络中创建。

   有关插入组件的详细信息，请参见 [编辑页面内容](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/authoring/editing-content.html).

### 编辑AEM页面的Livefyre组件。 {#edit-a-livefyre-component-for-an-aem-page}

您只能在Livefyre Studio中配置和编辑Livefyre组件。 从AEM：

1. 单击要配置的Livefyre组件。
1. 单击 **配置** 图标（扳手）以打开配置对话框。
1. 单击 **要编辑此组件，请转到Livefyre Studio**.
1. 在Livefyre Studio中编辑应用程序。

## 将Livefyre与AEM Assets结合使用 {#use-livefyre-with-aem-assets}

### 请求权限并将UGC导入AEM Assets {#request-rights-and-import-ugc-into-aem-assets}

您可以使用UGC导入器将Twitter和Instagram用户生成的内容(UGC)从Livefyre Studio导入AEM Assets。 选择要导入的内容后，您必须先请求对内容的权限，然后才能完成导入。

>[!NOTE]
>
>在使用资产导入UGC之前，您必须在Livefyre Studio中设置社交帐户和权限请求帐户。 参见 [设置：权限请求](https://experienceleague.adobe.com/docs/livefyre/using/rights-requests/c-how-requesting-rights-works.html) 了解更多信息。

要将UGC导入AEM Assets，请执行以下操作：

1. 在AEM主页中，导航到 **资产>文件**.
1. 单击 **创建**，然后单击 **导入UGC。**

   ![livefyre-aem-import-ugc](assets/livefyre-aem-import-ugc.png)

1. 查找内容：

   * 在Livefyre中，单击UGC库选项卡。 使用筛选器和搜索功能从UGC库中查找内容。
   * 在Twitter和Instagram中，单击Twitter或Instagram选项卡。 使用搜索或筛选器查找内容。

1. 选择要导入的资源。 您选择的资源将自动计数并保存在 **已选择** 选项卡。
1. **可选**：单击 **已选择** 选项卡，并查看选定的UGC内容以导入。
1. 单击&#x200B;**下一步**。

   ![livefyre-aem-import-ugc2](assets/livefyre-aem-import-ugc2.png)

1. 对于权限请求，请为每个资产选择以下选项之一：

   对于Instagram：

   * **手动请求权限** ，以获取可复制并粘贴的消息，并通过Instagram手动发送给内容所有者。
   * **手动属性内容权限** 覆盖单个资产的权限。

   >[!NOTE]
   >
   >由于更新影响了非企业用户帐户中的内容聚合，我们不再能够代表您发布评论或自动检查作者的回复。 [单击此处了解更多信息](https://developers.facebook.com/blog/post/2018/04/04/facebook-api-platform-product-changes/).

   ![livefyre-aem-import-ugc3-6-4](assets/livefyre-aem-import-ugc3-6-4.png)

   对于Twitter：

   * **消息作者** 向内容所有者发送消息，请求对资源的权限。
   * **手动属性内容权限** 覆盖单个资产的权限。


1. 单击&#x200B;**导入**。

   如果您发送了Twitter权限请求，则内容所有者将在其帐户中看到权限请求消息：

   ![livefyre-aem-rights-request-twitter](assets/livefyre-aem-rights-request-twitter.png)

   >[!NOTE]
   >
   >twitter对来自同一帐户的相同请求有限制。 导入多个资产时，请单独修改消息以避免被标记。

1. 单击 **完成** ，以完成权限请求工作流。

   您可以在Livefyre Studio中查看资产的待处理权限请求的状态。 如果内容未决权限请求，则在授予权限之前，资产将不会显示在AEM Assets中。 授予权限请求后，资产会自动显示在AEM Assets中。

   对于Instagram，您必须跟踪内容所有者的响应，并在为内容授予权限时手动授予权限。

## 在AEM Commerce中使用Livefyre {#use-livefyre-with-aem-commerce}

### 使用AEM Commerce将产品目录导入Livefyre {#import-product-catalogs-into-livefyre-with-aem-commerce}

AEM Commerce用户可以将其现有的产品目录无缝集成到Livefyre中，从而推动用户参与Livefyre的可视化应用程序。

导入产品目录后，产品会实时显示在您的Livefyre实例中。 如果您编辑或删除AEM Commerce产品目录中的项目，更改将自动在Livefrye中更新。

1. 确保您的AEM实例上安装最新的Livefyre for AEM软件包。
1. 在AEM主页中，导航到 **AEM商务**.
1. 创建新收藏集或使用现有收藏集。
1. 将鼠标悬停在收藏集上并单击 **收藏集属性** （铅笔图标）。
1. Check **同步到Livefyre**.
1. 填写 **Livefyre页面前缀** 以将此收藏集链接到AEM中的特定页面。

   页面前缀定义在您的环境中开始搜索产品页面的根路径。 Livefyre会选择具有与其关联的相应产品的第一个页面。 要获取不同产品的不同页面，需要多个收藏集。

## 适用于Livefyre应用程序的AEM支持列表 {#aem-support-matrix-for-livefyre-apps}

| Livefyre应用程序 | AEM 6.1 | AEM 6.2 | AEM 6.3 | AEM 6.4 |
|---|---|---|---|---|
| 轮盘 | X | X | X | X |
| 聊天 | X | X | X | X |
| 评论 | X | X | X | X |
| 电影胶片 |  | X | X | X |
| LiveBlog | X | X | X | X |
| 地图 | X | X | X | X |
| Media Wall | X | X | X | X |
| 马赛克 | X | X | X | X |
| 轮询 |  | X | X | X |
| 审核 |  | X | X | X |
| 单一信息卡 | X | X | X | X |
| Storify 2 |  | X | X | X |
| 热门 |  | X | X | X |
| 上传按钮 |  | X | X | X |
