---
title: 管理 [!DNL Adobe Stock] 资产
description: 搜索、获取、许可和管理 [!DNL Adobe Stock] 资产范围 [!DNL Adobe Experience Manager]. 将许可资产用作任何其他数字资产。
contentOwner: Vishabh Gupta
feature: Search, Adobe Stock
role: User, Admin
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '2481'
ht-degree: 7%

---

# 使用 [!DNL Adobe Stock] 中的资产 [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-assets-adobe-stock.html?lang=en) |
| AEM 6.5 | 本文 |

<!-- old content

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager]. 

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] service provides designers and businesses with access to millions of high-quality, curated, royalty-free photos, vectors, illustrations, videos, templates, and 3D assets for all their creative projects. [!DNL Experience Manager] users are able to quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in [!DNL Experience Manager], without leaving the [!DNL Experience Manager] interface.
-->

<!-- New overview content
-->

[!DNL Adobe Stock] 该服务使设计人员和企业能够为其所有创意项目访问数百万张高质量、精选且免版税的照片、矢量、插图、视频、模板和3D资产。

[!DNL Adobe Stock] 默认情况下，企业产品包括组织内的共享权限。 资产获得贵组织的用户许可后，贵组织的其他用户便可以识别、下载和使用此资产，而无需再次许可。 资产获得贵组织的许可后，便享有永久使用权。

组织可以集成其企业 [!DNL Adobe Stock] 计划方式 [!DNL Experience Manager Assets] 通过强大的资产管理功能，确保许可资产可广泛用于其创意和营销项目。 [!DNL Experience Manager]. [!DNL Experience Manager] 用户可以快速查找、预览和许可保存在中的Adobe Stock资源 [!DNL Experience Manager]，而不离开 [!DNL Experience Manager] 界面。

<!-- Old content
## Prerequisites {#prerequisites}

The integration requires an [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).
-->

## 集成 [!DNL Experience Manager] 和 [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] 允许用户搜索、预览、保存和许可 [!DNL Adobe Stock] 资产直接来自 [!DNL Experience Manager].

**前提条件**

集成需要：

* An [企业 [!DNL Adobe Stock] 计划](https://stockenterprise.adobe.com/)
* 具有默认Stock产品配置文件Admin Console权限的用户
* 具有在Adobe Developer Console中创建集成的开发人员访问配置文件权限的用户

企业 [!DNL Adobe Stock] 计划，

* 提供产品权利 [!DNL Adobe Stock] (与Experience Manager相关的股票)
* 购买到的积分 [!DNL Adobe Admin Console] 您股票权益的
* 在中启用服务帐户(JWT)身份验证 [!DNL Adobe Developer Console] 您股票权益的
* 支持从内部全局管理信用和许可 [!DNL Adobe Admin Console]

在权利中，默认产品配置文件 [!DNL Adobe Stock] 存在于 [!DNL Admin Console]. 可以创建多个配置文件，这些配置文件确定谁可以许可Stock资产。 可直接访问产品配置文件的用户可以访问 [https://stock.adobe.com/](https://stock.adobe.com/) 并许可Stock资产。 而还有另一种使用开发人员访问权限创建集成(API)的方法，来验证之间的通信 [!DNL Experience Manager] 和 [!DNL Adobe Stock].

>[!NOTE]
>
>Stock服务帐户(JWT)身份验证随企业股票权利提供。
>
>该集成不支持企业股票权利的Oauth身份验证。

<!-- old content
To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.
-->

## 集成步骤 [!DNL Experience Manager] 和 [!DNL Adobe Stock] {#integration-steps}

要集成 [!DNL Experience Manager] 和 [!DNL Adobe Stock]，请按列出的顺序执行以下步骤：

1. [获取公共证书](#public-certificate)

   In [!DNL Experience Manager]，创建IMS帐户并生成公共证书（公共密钥）。

1. [创建服务帐户(JWT)连接](#createnewintegration)

   In [!DNL Adobe Developer Console]，为您的创建一个项目 [!DNL Adobe Stock] 组织。 在项目下，使用公钥配置API以创建服务帐户(JWT)连接。 获取服务帐户凭据和JWT有效负载信息。

1. [配置IMS帐户](#create-ims-account-configuration)

   In [!DNL Experience Manager]，使用服务帐户凭据和JWT有效负载配置IMS帐户。

1. [配置云服务](#configure-the-cloud-service)

   In [!DNL Experience Manager]，配置 [!DNL Adobe Stock] 使用IMS帐户的云服务。


### 创建IMS配置 {#create-an-ims-configuration}

IMS配置验证您的 [!DNL Experience Manager Assets] 使用的创作实例 [!DNL Adobe Stock] 权利。

IMS 配置包括两个步骤：

* [获取公共证书](#public-certificate)
* [配置IMS帐户](#create-ims-account-configuration)

### 获取公共证书 {#public-certificate}

公钥（证书）在Adobe Developer控制台中验证您的产品配置文件。

1. 登录 [!DNL Experience Manager Assets] 创作实例。 默认URL为 `http://localhost:4502/aem/start.html`.

1. 从 **[!UICONTROL 工具]** 面板，导航到 **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS配置]**.

1. 在“Adobe IMS配置”页面中，单击 **[!UICONTROL 创建]**. 此 **[!UICONTROL Adobe IMS技术帐户配置]** 页面打开。

1. 在 **[!UICONTROL 证书]** 选项卡，选择 **[!UICONTROL Adobe Stock]** 从 **[!UICONTROL 云解决方案]** 下拉列表。

1. 您可以为配置创建证书或重用现有证书。

   要创建证书，请选择 **[!UICONTROL 创建新证书]** 复选框，并指定 **别名** 用于公钥。 别名用作公钥的名称。

1. 单击&#x200B;**[!UICONTROL 创建证书]**。然后，单击 **[!UICONTROL 确定]** 以生成公钥。

1. 单击 **[!UICONTROL 下载公钥]** 图标并将公钥(.crt)文件保存到计算机上。 公钥稍后用于为Brand Portal租户配置API并在Adobe Developer控制台中生成服务帐户凭据。

   单击&#x200B;**[!UICONTROL 下一步]**。

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. 在 **帐户** 选项卡，创建Adobe IMS帐户时需要服务帐户凭据。

   打开新选项卡并 [在Adobe Developer控制台中创建服务帐户(JWT)连接](#createnewintegration).

### 创建服务帐户(JWT)连接 {#createnewintegration}

在Adobe Developer控制台中，项目和API在组织级别进行配置。 配置API会创建服务帐户(JWT)连接。 配置API的方法有两种：生成密钥对（私钥和公钥）或上传公钥。 在此示例中，服务帐户凭据是通过上传公钥生成的。

要生成服务帐户凭据和JWT有效负载，请执行以下操作：

1. 使用系统管理员权限登录到Adobe Developer控制台。 默认URL为 [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   确保您从下拉列表（组织）中选择了正确的IMS组织（库存权利）。

1. 单击 **[!UICONTROL 创建新项目]**. 系统会为您的组织创建一个名称由系统生成的空白项目。

   单击 **[!UICONTROL 编辑项目]**. 更新 **[!UICONTROL 项目标题]** 和 **[!UICONTROL 描述]**，然后单击 **[!UICONTROL 保存]**.

1. 在 **[!UICONTROL 项目概述]** 选项卡，单击 **[!UICONTROL 添加API]**.

1. 在 **[!UICONTROL 添加API窗口]**，选择 **[!UICONTROL Adobe Stock]**. 单击&#x200B;**[!UICONTROL 下一步]**。

1. 在 **[!UICONTROL 配置API]** 窗口，选择 **[!UICONTROL 服务帐户(JWT)]** 身份验证。 单击&#x200B;**[!UICONTROL 下一步]**。

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. 单击 **[!UICONTROL 上传公钥]**. 单击 **[!UICONTROL 选择文件]** 并上传您在中下载的公共密钥（.crt文件） [获取公共证书](#public-certificate) 部分。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 验证公钥并单击 **[!UICONTROL 下一个]**.

1. 选择默认值 **[!UICONTROL Adobe Stock]** 产品配置文件并单击 **[!UICONTROL 保存配置的API]**.

1. 配置API后，您将被重定向到API概述页面。 从左侧导航栏中的 **[!UICONTROL 凭据]**，单击 **[!UICONTROL 服务帐户(JWT)]** 选项。 在这里，您可以查看凭据并执行操作，如生成JWT令牌、复制凭据详细信息和检索客户端密码。

1. 从 **[!UICONTROL 客户端凭据]** 选项卡，复制 **[!UICONTROL 客户端ID]**.

   单击 **[!UICONTROL 检索客户端密码]** 并复制 **[!UICONTROL 客户端密码]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. 导航到 **[!UICONTROL 生成JWT]** 制表并复制 **[!UICONTROL JWT有效负荷]** 信息。

您现在可以将客户端ID（API密钥）、客户端密钥和JWT有效负载用于 [配置IMS帐户](#create-ims-account-configuration) 在 [!DNL Experience Manager Assets].

### 配置IMS帐户 {#create-ims-account-configuration}

您必须拥有 [证书](#public-certificate) 和 [服务帐户(JWT)凭据](#createnewintegration) 配置IMS帐户。

配置IMS帐户：

1. 打开IMS配置并导航到 **[!UICONTROL 帐户]** 选项卡。 您保持页面打开的时间 [获取公共证书](#public-certificate).

1. 为 IMS 帐户指定&#x200B;**[!UICONTROL 标题]**。

   在 **[!UICONTROL 授权服务器]** 字段中，输入URL： [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   在中输入客户端ID **[!UICONTROL API密钥]** 字段， **[!UICONTROL 客户端密码]**、和 **[!UICONTROL 有效负荷]** （JWT有效负荷）之前复制的时间 [创建服务帐户(JWT)连接](#createnewintegration).

1. 单击&#x200B;**[!UICONTROL 创建]**。已创建IMS帐户配置。

   ![configure-ims-account](assets/aem-stock-ims-config.png)

1. 选择IMS帐户配置并单击 **[!UICONTROL 检查运行状况]**.

   单击 **[!UICONTROL Check]** 对话框中。 成功配置后，将显示一条消息，指出 *已成功检索令牌*.

   ![运行状况检查](assets/aem-stock-healthcheck.png)


### 配置云服务 {#configure-the-cloud-service}

要配置 [!DNL Adobe Stock] 云服务：

1. 在 [!DNL Experience Manager] 用户界面，导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. 在 [!DNL Adobe Stock Configurations] 页面，单击 **[!UICONTROL 创建]**.

1. 指定 **[!UICONTROL 标题]** 用于云配置。

   选择您已在以下时间创建的IMS配置： [配置IMS帐户](#create-ims-account-configuration).

   从下拉列表中选择您的区域设置。

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. 单击“**[!UICONTROL 保存并关闭]**”。

   您的 [!DNL Experience Manager Assets] 创作实例现已与集成 [!DNL Adobe Stock]. 您可以创建多个 [!DNL Adobe Stock] 配置（例如，基于区域设置的配置）。 您现在可以访问、搜索和许可 [!DNL Adobe Stock] 内的资产 [!DNL Experience Manager] 用户界面。

   ![search-stock-assets](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >在集成的此阶段，只有管理员才能访问 [!DNL Adobe Stock] 资产，搜索Stock资产（使用Omnisearch），并许可 [!DNL Adobe Stock] 资产。
   >
   >管理员可以将用户或组进一步添加到 [!DNL Adobe Stock] cloud service并将权限授予中的这些非管理员用户 [!DNL Experience Manager] 以访问Stock配置。

1. 要添加用户或组，请选择 [!DNL Adobe Stock] 云配置并单击 **[!UICONTROL 属性]**.

1. 搜索以添加您为其分配了访问Adobe Stock配置的权限的用户或组。 参见 [向用户组分配权限](#assign-permissions-to-group).


## 为用户组分配权限 {#assign-permissions-to-group}

管理员可以创建用户组，并将权限授予特定用户或组，以访问 [!DNL Adobe Stock] 云服务。

以下是用户搜索和许可Adobe Stock资源所需的权限：

* 配置路径： `/conf/global/settings/stock`
* 特权: `jcr:read`
* 权限类型: `Allow`

您可以创建用户群组或向现有用户群组分配权限。 可以从分配权限 [!DNL Experience Manager Assets] 界面或从 [!DNL User Admin] 控制台。

**要提供对用户组的访问权限，请执行以下操作： [!DNL Experience Manager]：**

1. 在 [!DNL Experience Manager] 用户界面，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 组]**. 创建用户组 [!DNL Adobe Stock].

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 权限]**.

1. 在左侧面板中搜索用户组并添加新用户组 **[!UICONTROL 访问控制条目(ACE)]** 适用于Adobe Stock的。

   * 配置路径： `/conf/global/settings/stock`
   * 特权: `jcr:read`
   * 权限类型: `Allow`

   单击 **[!UICONTROL 添加]**.

   ![user-permissions](assets/aem-stock-user-permissions.png)

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**. 选择 [!DNL Adobe Stock] 云配置并单击 **[!UICONTROL 属性]**.

1. 将新创建的用户组添加到 [!DNL Adobe Stock] 配置。 单击“**[!UICONTROL 保存并关闭]**”。

   ![分配 — 用户](assets/aem-stock-adduser.png)

**要从以下位置提供对用户的访问权限： [!DNL User Admin Console]：**

1. 打开 [!DNL Experience Manager] 用户Admin Console。 默认URL为 `http://localhost:4502/userdamin`.

1. 在左侧面板中，通过输入 `user_id` 或 `name`. 双击以打开用户属性。

1. 导航到 **[!UICONTROL 权限]** 制表符并允许 `read` 的权限 [!DNL Adobe Stock] 云配置： `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >如果不允许云配置，则用户只能访问 **[!UICONTROL 资产]** 在 [!DNL Experience Manager] 界面。
   >
   >允许访问 [!UICONTROL 资产] 和 [!DNL Adobe Stock] 资源，确保用户允许云配置。

1. 单击 **[!UICONTROL 保存]** 以更新权限。

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. 将用户或组添加到 [!DNL Adobe Stock] 云配置。


## 访问Adobe Stock资源 {#access-stock-assets}

具有权限的非管理员用户 [!DNL Adobe Stock] 云配置可以搜索并许可 [!DNL Adobe Stock] 中的资产 [!DNL Experience Manager] 界面。

用户必须执行额外的步骤来激活 [!DNL Adobe Stock] 访问之前的云配置 [!DNL Adobe Stock] 资产。 这是一次性活动。 如果用户被分配了多个权限 [!DNL Adobe Stock] 云配置，用户可以从中选择所需的配置 **[!UICONTROL 用户首选项]**.

激活 [!DNL Adobe Stock] 云配置：

1. 登录 [!DNL Experience Manager].

1. 单击右上角的用户图标，然后单击 **[!UICONTROL 我的首选项]**. 此 **[!UICONTROL 用户首选项]** 窗口打开。

1. 选择所需的 **[!UICONTROL Stock配置]** ，然后单击 **[!UICONTROL 接受]** 以激活配置。

   ![用户首选项](assets/aem-stock-preferences.png)

1. 导航到 **[!UICONTROL 资产]** > **[!UICONTROL Adobe Stock]**. 您现在可以查看、搜索和许可 [!DNL Adobe Stock] 资产。

下表说明了访问时用户权限的工作方式 [!DNL Adobe Stock] 资产：

| 用户 | 组 | 权限 | 在“用户首选项”中接受毛坯配置 | 访问资源 | 访问Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| 管理员 | 不适用 | 所有 | 不适用 | 是 | 是 |
| test-doc1 | DAM 用户 | /conf/global /settings/stock/cloud-config | 是 | 是 | 是 |
| test-doc1 | DAM 用户 | /conf/global /settings/stock/cloud-config | 否 | 错误：无法加载数据 | 否 |
| test-doc1 | DAM 用户 | **允许**： /conf/global /settings/stock     **拒绝**： /cloud-config | Stock配置不可见 | 是 | 否 |


## 使用和管理 [!DNL Adobe Stock] 中的资产 [!DNL Experience Manager] {#usemanage}

利用此功能，组织可允许其用户使用 [!DNL Adobe Stock] 中的资产 [!DNL Experience Manager Assets]. 从 [!DNL Experience Manager] 用户界面，用户可以进行搜索 [!DNL Adobe Stock] 并许可所需的资产。

一次 [!DNL Adobe Stock] 资产许可位置 [!DNL Experience Manager]，其使用和管理方式与典型资产类似。 In [!DNL Experience Manager]，用户可以搜索并预览资产，复制并发布资产，共享资产 [!DNL Brand Portal]；通过以下方式访问和使用资源 [!DNL Experience Manager] 桌面应用程序；等等。

![搜索 [!DNL Adobe Stock] 资源并从筛选结果 [!DNL Adobe Experience Manager] 工作区](assets/adobe-stock-search-results-workspace.png)

**A.**[!DNL Adobe Stock] 搜索与提供 ID 的资产类似的资产。**B.** 搜索与您选择的形状或方向匹配的资产。**C.** 搜索一种或多种受支持的资产类型 **D.** 打开或折叠过滤器窗格 **E.** 在 中授权并保存选定的资产 [!DNL Experience Manager]**F.**[!DNL Experience Manager] 在 中保存带水印的资产 **G.**[!DNL Adobe Stock] 在 网站上浏览与选定资产类似的资产 **H.**[!DNL Adobe Stock] 在 网站上查看选定资产 **I.** 搜索结果中的选定资产数 **J.** 在卡片视图和列表视图之间切换

### 查找资源 {#find-assets}

您的 [!DNL Experience Manager] 用户，可以在以下位置搜索资产： [!DNL Experience Manager] 和 [!DNL Adobe Stock]. 当搜索位置不限于 [!DNL Adobe Stock]，则搜索结果来自 [!DNL Experience Manager] 和 [!DNL Adobe Stock] 将显示。

* 要搜索 [!DNL Adobe Stock] 资产，请单击 **[!UICONTROL 导航]** > **[!UICONTROL 资产]** > **[!UICONTROL 搜索Adobe Stock]**.

* 要搜索中的资产，请执行以下操作 [!DNL Adobe Stock] 和 [!DNL Experience Manager Assets]，单击搜索 ![搜索](assets/do-not-localize/search_icon.png).

或者，开始键入 `Location: Adobe Stock` 在搜索栏中选择 [!DNL Adobe Stock] 资产。 [!DNL Experience Manager] 对搜索的资产提供高级筛选功能，允许用户使用筛选器快速聚焦于所需的资产，例如支持的资产类型、图像方向和许可状态。

>[!NOTE]
>
>搜索自的资源 [!DNL Adobe Stock] 显示于 [!DNL Experience Manager]. [!DNL Adobe Stock] 资产获取并存储在 [!DNL Experience Manager] 仅在用户执行以下任一操作后存储库： [保存资产](/help/assets/aem-assets-adobe-stock.md#saveassets) 或 [许可并保存资产](/help/assets/aem-assets-adobe-stock.md#licenseassets). 已存储在中的资产 [!DNL Experience Manager] 为了便于引用和访问，将显示和突出显示。 此外， [!DNL Stock] 资产会与一些其他元数据一起保存，以指示源为 [!DNL Stock].

![在中搜索筛选器 [!DNL Experience Manager] 和突出显示 [!DNL Adobe Stock] 搜索结果中的资产](assets/aem-search-filters2.jpg)

### 保存并查看所需的资产 {#saveassets}

选择要保存到的资源 [!DNL Experience Manager]. 单击 [!UICONTROL 保存] ，并提供资源的名称和位置。 未授权的资产使用水印保存在本地。

下次搜索资源时，保存的资源会以徽章突出显示，以指示此类资源在以下位置可用： [!DNL Experience Manager Assets].

>[!NOTE]
>
>最近添加的资产显示的是新徽章，而不是已许可徽章。

### 许可资产 {#licenseassets}

用户可以许可 [!DNL Adobe Stock] 资源(通过使用其资源的 [!DNL Adobe Stock] 企业计划。 当您许可资产时，该资产会保存而不加水印，并且可用于搜索和使用中 [!DNL Experience Manager Assets].

![用于许可和保存的对话框 [!DNL Adobe Stock] 中的资产 [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### 访问元数据和资源属性 {#access-metadata-and-asset-properties}

用户可以访问和预览元数据，包括 [!DNL Adobe Stock] 资源保存在中的元数据属性 [!DNL Experience Manager]，并添加 **[!UICONTROL 许可证引用]** （对于资产）。 但是，对许可证引用的更新不会在 [!DNL Experience Manager] 和 [!DNL Adobe Stock] 网站。

用户可以查看已许可和未许可资产的属性。

![查看和访问已保存资产的元数据和许可证引用](assets/metadata_properties.jpg)


## 已知限制 {#known-limitations}

* **与集成的问题 [!DNL Experience Manager] Service Pack 6.5.7.0及更高版本**：在与集成期间发现意外问题 [!DNL Experience Manager] 6.5.7.0及更高版本。 该问题正在测试中，预计将在以下位置提供： [!DNL Experience Manager] 6.5.11.0.联系 [!DNL Customer Support] 以获取即时修补程序。

* **限制用户许可的功能无法正常工作**：所有用户都具有 `read` 允许stock配置的权限来搜索和许可 [!DNL Adobe Stock] 资产。

* **非管理员用户必须手动激活 [!DNL Adobe Stock] 云配置**：在 **[!UICONTROL 用户首选项]** 窗口， **[!UICONTROL Stock配置]** 显示 [!DNL Adobe Stock] 云配置处于启用状态，但它不适用于非管理员用户。 用户必须单击 **[!UICONTROL 接受]** 按钮以激活Stock配置。 如果没有此步骤，系统将显示访问时的错误消息 **[!UICONTROL 资产]**.

* **不显示编辑图像警告**：在许可图像时，用户无法检查图像是否仅用于编辑。 为防止可能的误用，管理员可以从Admin Console中关闭对编辑资源的访问权限。

* **显示的许可证类型错误**：中可能会显示错误的许可证类型 [!DNL Experience Manager] （对于资产）。 用户可以登录到 [!DNL Adobe Stock] 网站以查看许可证类型。

* **引用字段和元数据未同步**：当用户更新许可证引用字段时，许可证引用信息更新于 [!DNL Experience Manager] 但不在 [!DNL Adobe Stock] 网站。 同样，如果用户更新 [!DNL Adobe Stock] 网站中，更新未同步 [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [有关使用的视频教程 [!DNL Adobe Stock] 带有以下项的资产： [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] 企业计划帮助](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] 常见问题](https://helpx.adobe.com/stock/faq.html)



<!--old content

### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in [!UICONTROL User Preferences] panel. To access the panel from [!DNL Experience Manager] home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.
-->

