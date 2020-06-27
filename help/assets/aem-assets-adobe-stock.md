---
title: 在 [!DNL Adobe Stock] 中管理资产 [!DNL Adobe Experience Manager Assets]。
description: 从内部搜索、提取、许 [!DNL Adobe Stock] 可和管理资产 [!DNL Adobe Experience Manager]。 将授权资产用作任何其他数字资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a61e1e9ffb132b59c725b2078f09641a3c2a479a
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 15%

---


# 将资 [!DNL Adobe Stock] 产用于 [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

组织可以将其企 [!DNL Adobe Stock] 业计划与 [!DNL Experience Manager Assets] 其强大的资产管理功能集成在一起，以确保许可资产广泛用于其创意和营销项目 [!DNL Experience Manager]。

[!DNL Adobe Stock] 服务为设计师和企业提供了数百万种可用于所有创意项目的高品质、精选、免版税的照片、矢量、插图、视频、模板和 3D 资产。[!DNL Experience Manager] 用户无需离开界面，即可快速查找、 [!DNL Adobe Stock] 预览和许可保 [!DNL Experience Manager]存在的资 [!DNL Experience Manager] 源。

## 前提条件 {#prerequisites}

该集成需要 [企业Adobe Stock](https://stockenterprise.adobe.com/)[!DNL Experience Manager] 计划和6.5或更高版本。 有 [!DNL Experience Manager] 关6.5 Service Pack的详细信息，请参阅 [这些发行说明](/help/release-notes/sp-release-notes.md)。

## 集成 [!DNL Experience Manager] 和 [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

要允许与之间 [!DNL Experience Manager] 的通 [!DNL Adobe Stock]信，请在中创建IMS配置 [!DNL Adobe Stock] 和配置 [!DNL Experience Manager]。

>[!NOTE]
>
>只有 [!DNL Experience Manager] 组织的管 [!DNL Admin Console] 理员和管理员才能执行集成，因为它需要管理员权限。

### Create an IMS configuration {#create-an-ims-configuration}

1. Click on [!DNL Experience Manager] logo. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL Adobe IMS 配置]**。单击&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 云解决方案]** > **[!UICONTROL Adobe Stock]**。
1. 重用现有证书或选择“ **[!UICONTROL 创建新证书”]**。
1. 单击&#x200B;**[!UICONTROL 创建证书]**。创建后，下载公钥。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 在标题为&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 授权服务器]**、**[!UICONTROL API 密钥]**、**[!UICONTROL 客户端密钥]**&#x200B;和&#x200B;**[!UICONTROL 负载]**&#x200B;的字段中提供相应的值。See [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md), for detailed information to fetch these values from [!DNL Adobe I/O].
1. 将下载的公钥添加到您的服 [!DNL Adobe I/O] 务帐户。

<!-- TBD: Update the URL when the new URL is available. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### 创建 [!DNL Adobe Stock] 配置 [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. 单击 **[!UICONTROL 创建]** ，创建配置并将其与现有IMS配置关联。 选 `PROD` 作环境参数。
1. 在授 **[!UICONTROL 权资产路径]** 字段中，保留原样。 请勿更改要存储资产的位 [!DNL Adobe Stock] 置。
1. 通过添加所有所需属性完成创建。 Click **[!UICONTROL Save &amp; Close]**.
1. 添加 [!DNL Experience Manager] 可授权资产的用户或用户组。

>[!NOTE]
>
>如果有多个 [!DNL Adobe Stock] 配置，请单击用户界 [!UICONTROL 面右上角的] “用户 *”徽标，在“用户首选项* ”面板中选择所需 [!DNL Experience Manager] 的配置。

## 在以下位置使 [!DNL Adobe Stock] 用和管理资产 [!DNL Experience Manager] {#usemanage}

使用此功能，组织可以允许其用户使用中 [!DNL Adobe Stock] 的资产 [!DNL Experience Manager Assets]。 在用户界面 [!DNL Experience Manager] 中，用户可以搜索资 [!DNL Adobe Stock] 产并许可所需的资产。

在中授 [!DNL Adobe Stock] 权使用资产 [!DNL Experience Manager]后，即可像典型资产一样使用和管理资产。 在 [!DNL Experience Manager]中，用户可以搜索和预览资产； 复制和发布资产； 资产 [!DNL Brand Portal]; 通过桌面应用程序访问 [!DNL Experience Manager] 和使用资源； 等等。

![搜索Adobe Stock资源并从您的Adobe Experience Manager工作区过滤结果](assets/adobe-stock-search-results-workspace.png)

*图： 搜索资[!DNL Adobe Stock]产并从界面筛选[!DNL Experience Manager]结果。*

**A.**[!DNL Adobe Stock] 搜索与提供 ID 的资产类似的资产。**B.** 搜索与您选择的形状或方向匹配的资产。**C.** 搜索一种或多种受支持的资产类型 **D.** 打开或折叠过滤器窗格 **E.** 在 中授权并保存选定的资产 [!DNL Experience Manager]**F.**[!DNL Experience Manager] 在 中保存带水印的资产 **G.**[!DNL Adobe Stock] 在 网站上浏览与选定资产类似的资产 **H.**[!DNL Adobe Stock] 在 网站上查看选定资产 **I.** 搜索结果中的选定资产数 **J.** 在卡片视图和列表视图之间切换

### 查找资产 {#find-assets}

您 [!DNL Experience Manager] 的用户可以在和中搜索资 [!DNL Experience Manager] 产 [!DNL Adobe Stock]。 当搜索位置不限于时， [!DNL Adobe Stock]将显示来自和 [!DNL Experience Manager] 的搜 [!DNL Adobe Stock] 索结果。

* 要搜索资 [!DNL Adobe Stock] 产，请单 **[!UICONTROL 击导航]** > **[!UICONTROL 资]** 产 **[!UICONTROL >]**&#x200B;搜索Adobe Stock。

* 要在和之间搜 [!DNL Adobe Stock] 索资 [!DNL Experience Manager Assets]产，请单 ![击search_icon](assets/search_icon.png)。

或者，也可以开始 `Location: Adobe Stock` 在搜索栏中键入内容来选择 [!DNL Adobe Stock] 资产。 [!DNL Experience Manager] 优惠对已搜索的资产具有高级过滤功能，允许用户使用过滤器快速锁定所需的资产，如受支持的资产类型、图像方向和许可状态。

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] 只有在用户保存资产或 [!DNL Experience Manager] 许可证并保存资产 [后，才会](/help/assets/aem-assets-adobe-stock.md#saveassets) 将资 [产取回并存储在存储库中](/help/assets/aem-assets-adobe-stock.md#licenseassets)。 Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![在Experience Manager中搜索过滤器，并在搜索结果中高亮显示Adobe Stock资源](assets/aem-search-filters2.jpg)

*图： 在搜索结果中搜[!DNL Experience Manager]索过滤器[!DNL Adobe Stock]并突出显示资产。*

### 保存和视图所需的资产 {#saveassets}

选择要保存的资产 [!DNL Experience Manager]。 单 [!UICONTROL 击顶] 部工具栏中的保存，并提供资产的名称和位置。 未授权的资源将使用水印保存在本地。

下次搜索资产时，保存的资产会以徽章突出显示，以指示此类资产在中可用 [!DNL Experience Manager Assets]。

>[!NOTE]
>
>最近添加的资产会显示一个新徽章，而不是许可徽章。

### 许可资源 {#licenseassets}

用户可以 [!DNL Adobe Stock] 使用其企业计划的配额来许可 [!DNL Adobe Stock] 资产。 当您授权许可资产时，资产会保存，但不带水印，并且可在中搜索和使用 [!DNL Experience Manager Assets]。

![用于许可和保存Experience Manager资源中的Adobe Stock资源的对话框](assets/aem-stock_licenseandsave.jpg)

*图： 允许并保存资产的[!DNL Adobe Stock]对话框[!DNL Experience Manager Assets]。*

### 访问元数据和资产属性 {#access-metadata-and-asset-properties}

用户可以访问和预览元数据(包括保 [!DNL Adobe Stock] 存在中的资产的元数据属 [!DNL Experience Manager]性)，并 **[!UICONTROL 为资产添加]** 许可证引用。 但是，对许可证引用的更新不会在与网站之 [!DNL Experience Manager] 间 [!DNL Adobe Stock] 同步。

用户可以查看授权和未授权资产的属性。

![视图并访问已保存资产的元数据和许可证引用](assets/metadata_properties.jpg)

*图： 视图并访问已保存资产的元数据和许可证引用。*

## 已知限制 {#known-limitations}

* **不显示编辑图像警告**: 授权图像时，用户无法检查图像是否为“仅限编辑使用”。 为防止可能的误用，管理员可以关闭对Admin Console中编辑资源的访问。

* **显示错误的许可证类型**: 资产的许可证类型可能显示 [!DNL Experience Manager] 不正确。 用户可登录网 [!DNL Adobe Stock] 站查看许可证类型。

* **引用字段和元数据未同步**: 当用户更新许可证引用字段时，在网站中更新许可证引用 [!DNL Experience Manager] 信息，但不在网站 [!DNL Adobe Stock] 上更新。 同样，如果用户更新网站上的引用字 [!DNL Adobe Stock] 段，则更新不会在中同步 [!DNL Experience Manager]。

>[!MORELIKETHIS]
>
>* [有关将Adobe Stock资源与Experience Manager资源结合使用的视频教程](https://helpx.adobe.com/experience-manager/kt/assets/using/stock-assets-feature-video-use.html)
>* [Adobe Stock企业计划帮助](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Adobe Stock常见问题解答](https://helpx.adobe.com/stock/faq.html)

