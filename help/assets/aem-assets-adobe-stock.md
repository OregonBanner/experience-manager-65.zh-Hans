---
title: 管理[!DNL Adobe Experience Manager资产]中的[!DNL Adobe Stock]资产。
description: 在Adobe Experience Manager中搜索、提取、许可和管理[!DNL Adobe Stock]资产。 将授权资产用作任何其他数字资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c9ac722cb8903d1d9946c7a6f797f102cb99bbf2

---


# Use Adobe Stock assets in AEM Assets {#use-adobe-stock-assets-in-aem-assets}

组织可以将其Adobe Stock企业计划与AEM资产相集成，以确保许可资产可广泛用于其创意和营销项目，并具备AEM强大的资产管理功能。

Adobe Stock 服务为设计师和企业提供了数百万种可用于所有创意项目的高品质、精选、免版税的照片、矢量、插图、视频、模板和 3D 资产。AEM用户无需离开AEM工作区，即可快速查找、预览和许可在AEM中保存的Adobe Stock资源。

## 前提条件 {#prerequisites}

该集成需要 [企业Adobe Stock计划](https://stockenterprise.adobe.com/) 和AEM 6.5或更高版本。 有关AEM 6.5 Service Pack的详细信息，请参阅这些 [发行说明](/help/release-notes/sp-release-notes.md)。

## 集成AEM和Adobe Stock {#integrate-aem-and-adobe-stock}

要允许AEM与Adobe Stock之间进行通信，请在AEM中创建IMS配置和Adobe Stock配置。

>[!NOTE]
>
>只有组织的AEM管理员和Admin Console管理员才能执行集成，因为它需要管理员权限。

### 创建IMS配置 {#create-an-ims-configuration}

1. 单击 AEM 徽标。导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL Adobe IMS 配置]**。单击&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 云解决方案]** > **[!UICONTROL Adobe Stock]**。
1. 重复使用现有证书或选择“ **[!UICONTROL 创建新证书”]**。
1. 单击“ **[!UICONTROL 创建证书]**”。 创建后，下载公钥。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 在标题为&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 授权服务器]**、**[!UICONTROL API 密钥]**、**[!UICONTROL 客户端密钥]**&#x200B;和&#x200B;**[!UICONTROL 负载]**&#x200B;的字段中提供相应的值。有关从 Adobe I/O 获取这些值的详细信息，请参阅 [JWT 身份验证快速入门](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)。
1. 将下载的公钥添加到您的Adobe I/O服务帐户。

### 在AEM中创建Adobe Stock配置 {#create-adobe-stock-configuration-in-aem}

1. 在 AEM 用户界面中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 云服务]** > **[!UICONTROL Adobe Stock]**。
1. 单击 **[!UICONTROL 创建]** ，创建配置并将其与现有IMS配置关联。 选择 `PROD` 作为环境参数。
1. 在“ **[!UICONTROL 许可资产路径]** ”字段中，保留原样。 请勿更改要存储Adobe Stock资源的位置。
1. 通过添加所有必需属性完成创建。 单击 **[!UICONTROL 保存并关闭]**。
1. 添加AEM用户或用户组，这些用户或用户组可以授权许可资产。

>[!NOTE]
>
>如果有多个Adobe Stock配置，请通过单击AEM用户界面中的 [!UICONTROL AEM徽标] ，在“用户首选项”面板中选择所需的配置。

## 在AEM中使用和管理Adobe Stock资源 {#usemanage}

使用此功能，组织可以允许其用户在AEM资产中使用Adobe Stock资产。 从AEM用户界面中，用户可以搜索Adobe Stock资产并许可所需的资产。

在AEM中许可Adobe Stock资产后，就可以像典型资产一样使用和管理它。 在AEM中，用户可以搜索和预览资产；复制和发布资产；在Brand Portal上共享资产；通过AEM桌面应用程序访问和使用资产；等等。

![搜索Adobe Stock资产并从AEM工作区过滤结果](assets/adobe-stock-search-results-workspace.png)

*图：搜索Adobe Stock资产并从AEM工作区过滤结果*

**A.** 搜索与提供 Adobe Stock ID 的资产类似的资产。**B.** 搜索与您选择的形状或方向匹配的资产。**C.** 搜索一种或多种受支持的资产类型 **D.** 打开或折叠过滤器窗格 **E.** 在 AEM 中授权并保存选定的资产 **F.** 在 AEM 中保存带水印的资产 **G.** 在 Adobe Stock 网站上浏览与选定资产类似的资产 **H.** 在 Adobe Stock 网站上查看选定资产 **I.** 搜索结果中的选定资产数 **J.** 在卡片视图和列表视图之间切换

### 查找资产 {#find-assets}

您的AEM用户可以在AEM和Adobe Stock中搜索资产。 当搜索位置不限于Adobe Stock时，将显示AEM和Adobe Stock的搜索结果。

* 要搜索Adobe Stock资源，请单击“导航 **[!UICONTROL ”>“资]** 产 **[!UICONTROL ”]** >“ **[!UICONTROL 搜索Adobe Stock]**”。

* 要在Adobe Stock和AEM资产中搜索资产，请单击搜索图 ![标search_icon](assets/search_icon.png)。

或者，开始在搜 `Location: Adobe Stock` 索栏中键入内容以选择Adobe Stock资源。  AEM优惠了针对搜索的资产的高级过滤功能，使用户能够使用过滤器（如支持的资产类型、图像方向和许可状态）快速锁定所需的资产。

>[!NOTE]
>
>从Adobe Stock搜索的资产刚刚在AEM中显示。 只有在用户保存资产或许可资产后，才会获取Adobe Stock资产并将其 [存储在AEM存](/help/assets/aem-assets-adobe-stock.md#saveassets) 储 [库中](/help/assets/aem-assets-adobe-stock.md#licenseassets)。 为便于引用和访问，将显示和高亮显示已存储在AEM中的资产。 此外，这些资产会与一些其他元数据一起保存，以将源指示为Adobe Stock。

![在AEM中搜索过滤器，并在搜索结果中高亮显示Adobe Stock资产](assets/aem-search-filters2.jpg)

*图：在AEM中搜索过滤器，并在搜索结果中高亮显示Adobe Stock资产*

### 保存和视图所需的资产 {#saveassets}

选择要在AEM中保存的资产。 单击顶部工具栏中的保存，并提供资产的名称和位置。 未授权的资源将用水印保存在本地。

下次搜索资产时，保存的资产会以徽章高亮显示，以指示此类资产在AEM资产中可用。

>[!NOTE]
>
>最近添加的资产会显示一个“新建”徽章，而不是“许可”徽章。

### 许可资源 {#licenseassets}

用户可以使用Adobe Stock企业计划的配额许可Adobe Stock资源。 在您为资产授权时，该资产会保存，但不会带有水印，并且可在AEM资产中搜索和使用。

![用于在AEM资产中许可和保存Adobe Stock资产的对话框](assets/aem-stock_licenseandsave.jpg)

*图：用于在AEM资产中许可和保存Adobe Stock资产的对话框*

### 访问元数据和资产属性 {#access-metadata-and-asset-properties}

用户可以访问和预览元数据（包括AEM中保存的资产的Adobe Stock元数据属性），并为资产添加 **[!UICONTROL 许可证引用]** 。 但是，对许可证参考的更新不会在AEM和Adobe Stock网站之间同步。

用户可以查看授权和未授权资产的属性。

![视图和访问已保存资产的元数据和许可证引用](assets/metadata_properties.jpg)

*图：视图和访问已保存资产的元数据和许可证引用*

## 已知限制 {#known-limitations}

### 未显示编辑图像警告

在许可图像时，用户无法检查图像是否为“仅限编辑使用”。 为防止可能的误用，管理员可以从Admin Console关闭对编辑资产的访问。

### 显示错误的许可证类型

资产的AEM中可能显示不正确的许可证类型。 用户可以登录Adobe Stock网站查看许可证类型。

### 引用字段和元数据不会同步

当用户更新许可证参考字段时，许可证参考信息将在AEM中更新，但不会在Adobe Stock网站上更新。 同样，如果用户更新Adobe Stock网站上的引用字段，则更新在AEM中不会同步。

>[!MORELIKETHIS]
>
>* [有关将Adobe Stock资产与AEM资产结合使用的视频教程](https://helpx.adobe.com/experience-manager/kt/assets/using/stock-assets-feature-video-use.html)
>* [Adobe Stock企业计划帮助](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Adobe Stock常见问题解答](https://helpx.adobe.com/stock/faq.html)

