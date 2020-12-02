---
title: 管理 [!DNL Adobe Stock] 资产
description: 从 [!DNL Adobe Experience Manager]中搜索、提取、许可和管理 [!DNL Adobe Stock] 资产。 将授权资产用作任何其他数字资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 13%

---


# 在[!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}中使用[!DNL Adobe Stock]资产

组织可以将其[!DNL Adobe Stock]企业计划与[!DNL Experience Manager Assets]集成，以确保许可资产广泛用于其创意和营销项目，并具有[!DNL Experience Manager]的强大资产管理功能。

[!DNL Adobe Stock] 服务为设计师和企业提供了数百万种可用于所有创意项目的高品质、精选、免版税的照片、矢量、插图、视频、模板和 3D 资产。[!DNL Experience Manager] 用户无需离开界面，即可快速查找、 [!DNL Adobe Stock] 预览和许可保 [!DNL Experience Manager]存在的资 [!DNL Experience Manager] 源。

## 前提条件 {#prerequisites}

集成需要[enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/)。

## 集成[!DNL Experience Manager]和[!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

要允许在[!DNL Experience Manager]和[!DNL Adobe Stock]之间进行通信，请在[!DNL Experience Manager]中创建IMS配置和[!DNL Adobe Stock]配置。

>[!NOTE]
>
>只有组织的[!DNL Experience Manager]管理员和[!DNL Admin Console]管理员才能执行集成，因为它需要管理员权限。

### 创建IMS配置{#create-an-ims-configuration}

1. 在[!DNL Experience Manager]用户界面中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL AdobeIMS配置]**。 单击&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 云解决方案]** > **[!UICONTROL Adobe Stock]**。
1. 重用现有证书或选择&#x200B;**[!UICONTROL 创建新证书]**。
1. 单击&#x200B;**[!UICONTROL 创建证书]**。创建后，下载公钥。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 将下载的公钥添加到您的[!DNL Adobe Developer Console]服务帐户。 单击&#x200B;**[!UICONTROL 下一步]**。使[!UICONTROL AdobeIMS技术帐户配置]屏幕保持打开状态，以便很快提供值。
1. 访问[Adobe开发者控制台](https://console.adobe.io)。 确保您的帐户对需要集成的组织具有管理员权限。
1. 单击&#x200B;**[!UICONTROL 新建项目]**&#x200B;并单击&#x200B;**[!UICONTROL 添加API]**。 从您可用的API列表中选择&#x200B;**[!UICONTROL Adobe Stock]**。 选择[!UICONTROL OAUTH 2.0 Web]。 配置并复制显示的各种值。
1. 在[!DNL Experience Manager]中，提供标题为&#x200B;**[!UICONTROL Title]**、**[!UICONTROL 授权服务器]**、**[!UICONTROL API密钥]**、**[!UICONTROL 客户机密码]**&#x200B;和&#x200B;**[!UICONTROL 负载]**&#x200B;的字段中的值。 有关这些值的详细信息，请参见[JWT身份验证快速开始](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)。

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### 在[!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}中创建[!DNL Adobe Stock]配置

1. 在[!DNL Experience Manager]中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**。
1. 单击&#x200B;**[!UICONTROL 创建]**&#x200B;以创建配置并将其与现有IMS配置关联。 选择`PROD`作为环境参数。
1. 在&#x200B;**[!UICONTROL 授权资产路径]**&#x200B;字段中，保留原样。 请勿更改要存储[!DNL Adobe Stock]资产的位置。
1. 通过添加所有所需属性完成创建。 单击&#x200B;**[!UICONTROL 保存并关闭]**。
1. 添加[!DNL Experience Manager]用户或用户组，这些用户或用户组可以授权资产。

>[!NOTE]
>
>如果有多个[!DNL Adobe Stock]配置，请在[!UICONTROL 用户首选项]面板中选择所需的配置。 要从[!DNL Experience Manager]主页访问该面板，请单击用户图标，然后单击&#x200B;**[!UICONTROL 用户首选项]** > **[!UICONTROL 库存配置]**。

## 使用和管理[!DNL Experience Manager] {#usemanage}中的[!DNL Adobe Stock]资产

使用此功能，组织可以允许其用户使用[!DNL Experience Manager Assets]中的[!DNL Adobe Stock]资产。 在[!DNL Experience Manager]用户界面中，用户可以搜索[!DNL Adobe Stock]资产并许可所需的资产。

在[!DNL Experience Manager]中许可[!DNL Adobe Stock]资产后，它便可以像典型资产一样使用和管理。 在[!DNL Experience Manager]中，用户可以搜索和预览资产；复制和发布资产；在[!DNL Brand Portal]上共享资产；通过[!DNL Experience Manager]桌面应用程序访问和使用资产；等等。

![搜索资 [!DNL Adobe Stock] 产并从工作区筛选结 [!DNL Adobe Experience Manager] 果](assets/adobe-stock-search-results-workspace.png)

*图：搜索资 [!DNL Adobe Stock] 产并从界面筛选 [!DNL Experience Manager] 结果。*

**A.**[!DNL Adobe Stock] 搜索与提供 ID 的资产类似的资产。**B.** 搜索与您选择的形状或方向匹配的资产。**C.** 搜索一种或多种受支持的资产类型 **D.** 打开或折叠过滤器窗格 **E.** 在 中授权并保存选定的资产 [!DNL Experience Manager]**F.**[!DNL Experience Manager] 在 中保存带水印的资产 **G.**[!DNL Adobe Stock] 在 网站上浏览与选定资产类似的资产 **H.**[!DNL Adobe Stock] 在 网站上查看选定资产 **I.** 搜索结果中的选定资产数 **J.** 在卡片视图和列表视图之间切换

### 查找资产{#find-assets}

您的[!DNL Experience Manager]用户可以在[!DNL Experience Manager]和[!DNL Adobe Stock]中搜索资产。 当搜索位置不限于[!DNL Adobe Stock]时，将显示[!DNL Experience Manager]和[!DNL Adobe Stock]的搜索结果。

* 要搜索[!DNL Adobe Stock]资产，请单击&#x200B;**[!UICONTROL 导航]** > **[!UICONTROL 资产]** > **[!UICONTROL 搜索Adobe Stock]**。

* 要在[!DNL Adobe Stock]和[!DNL Experience Manager Assets]中搜索资产，请单击搜索![搜索](assets/do-not-localize/search_icon.png)。

或者，也可以开始在搜索栏中键入`Location: Adobe Stock`以选择[!DNL Adobe Stock]资产。 [!DNL Experience Manager] 优惠对已搜索的资产具有高级过滤功能，允许用户使用过滤器快速锁定所需的资产，如受支持的资产类型、图像方向和许可状态。

>[!NOTE]
>
>从[!DNL Adobe Stock]搜索的资源只显示在[!DNL Experience Manager]中。 [!DNL Adobe Stock] 仅当用户保存资产或 [!DNL Experience Manager] 许可证并保存资产 [后，才](/help/assets/aem-assets-adobe-stock.md#saveassets) 会获取资 [产并](/help/assets/aem-assets-adobe-stock.md#licenseassets)将其存储在存储库中。为便于引用和访问，将显示和突出显示已存储在[!DNL Experience Manager]中的资产。 此外，[!DNL Stock]资产会与一些其他元数据一起保存，以将源指示为[!DNL Stock]。

![在搜索结果中搜 [!DNL Experience Manager] 索资产 [!DNL Adobe Stock] 并突出显示其过滤器](assets/aem-search-filters2.jpg)

*图：在搜索结果中 [!DNL Experience Manager] 搜索资 [!DNL Adobe Stock] 产并突出显示过滤器。*

### 保存并视图所需的资产{#saveassets}

选择要保存在[!DNL Experience Manager]中的资产。 单击顶部工具栏中的[!UICONTROL 保存]，并提供资产的名称和位置。 未授权的资源将使用水印保存在本地。

下次搜索资产时，保存的资产会以徽章高亮显示，以指示此类资产在[!DNL Experience Manager Assets]中可用。

>[!NOTE]
>
>最近添加的资产会显示一个新徽章，而不是许可徽章。

### 许可证资源{#licenseassets}

用户可以使用[!DNL Adobe Stock]企业计划的配额许可[!DNL Adobe Stock]资产。 当您许可某个资产时，该资产会保存，并且没有水印，可在[!DNL Experience Manager Assets]中进行搜索和使用。

![用于许可和保存资产的 [!DNL Adobe Stock] 对话框  [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)

*图：允许并保存资产的 [!DNL Adobe Stock] 对话框 [!DNL Experience Manager Assets]。*

### 访问元数据和资产属性{#access-metadata-and-asset-properties}

用户可以访问和预览元数据，包括保存在[!DNL Experience Manager]中的资产的[!DNL Adobe Stock]元数据属性，并为资产添加&#x200B;**[!UICONTROL 许可证引用]**。 但是，对许可证引用的更新不会在[!DNL Experience Manager]和[!DNL Adobe Stock]网站之间同步。

用户可以查看授权和未授权资产的属性。

![视图并访问已保存资产的元数据和许可证引用](assets/metadata_properties.jpg)

*图：视图并访问已保存资产的元数据和许可证引用。*

## 已知限制{#known-limitations}

* **不显示编辑图像警告**:授权图像时，用户无法检查图像是否为“仅限编辑使用”。为防止可能的误用，管理员可以关闭对Admin Console中编辑资源的访问。

* **显示错误的许可证类型**:资产的许可证类型可能显 [!DNL Experience Manager] 示不正确。用户可登录[!DNL Adobe Stock]网站查看许可证类型。

* **引用字段和元数据未同步**:当用户更新许可证引用字段时，在网站中更新许可证引用 [!DNL Experience Manager] 信息，但不在网站 [!DNL Adobe Stock] 上更新。同样，如果用户更新了[!DNL Adobe Stock]网站上的引用字段，则更新在[!DNL Experience Manager]中不会同步。

>[!MORELIKETHIS]
>
>* [有关将资源 [!DNL Adobe Stock] 与 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] 企业计划帮助](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] 常见问题解答](https://helpx.adobe.com/stock/faq.html)

