---
title: 内容交付
seo-title: Content Delivery
description: 内容交付
seo-description: null
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
exl-id: 85e73679-684e-402f-8186-8b56d8bd9372
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# 内容交付{#content-delivery}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

移动设备应用程序应能够根据需要使用AEM中的任意和所有内容来提供目标应用程序体验。

这包括使用资产、网站内容、CaaS内容（免费）内容以及可能具有自身结构的自定义内容。

>[!NOTE]
>
>**空中内容** 可以通过ContentSync处理程序从以上任何一项中获取。 它可用于通过ZIP对包进行批量打包和交付，以及维护更新或这些包。

Content Services提供了三种主要类型的资料：

1. **Assets**
1. **打包的HTML内容(HTML/CSS/JS)**
1. **独立于渠道的内容**

![chlimage_1-154](assets/chlimage_1-154.png)

## Assets {#assets}

资源收藏集是包含对其他收藏集引用的AEM构造。

资产收藏集可以通过Content Services公开。 在请求中调用资产收藏集将返回一个对象，该对象是资产的列表 — 包括其URL。 通过URL访问资源。 URL在对象中提供。 例如：

* 页面实体返回包含图像引用的JSON（页面对象）。 图像引用是用于获取图像的资产二进制文件的URL。
* 请求文件夹中的资产列表会返回JSON，其中包含有关该文件夹中所有实体的详细信息。 该列表是一个对象。 JSON具有URL引用，用于获取该文件夹中每个资源的二进制资源。

### 资产优化 {#asset-optimization}

Content Services的一个关键价值是能够返回针对设备优化的资产。 这减少了本地设备存储需求并提高了应用程序性能。

资源优化将是一个服务器端函数，它基于API请求中提供的信息。 应尽可能缓存资产演绎版，以便类似的请求不需要重新生成资产演绎版。

### 资产工作流程 {#assets-workflow}

资源工作流如下：

1. AEM中现成可用的资源引用
1. 根据资源引用实体的模型创建资源引用实体
1. 编辑实体

   1. 选择资源或资源收藏集
   1. 自定义JSON渲染

下图显示了 **资产引用工作流**：

![chlimage_1-155](assets/chlimage_1-155.png)

### 管理资产 {#managing-assets}

Content Services允许访问可能不会通过其他AEM内容引用的AEM托管资源。

#### 现有受管资产 {#existing-managed-assets}

现有AEM Sites和Assets用户正在使用AEM Assets管理其所有渠道的所有数字资料。 他们正在开发本机移动设备应用程序，并且需要使用AEM Assets管理的多个资源。 例如，徽标、背景图像、按钮图标等。

目前，这些功能分布在Assets存储库中。 应用程序需要引用的文件位于：

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/grey_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### 访问CS资产实体 {#accessing-cs-asset-entities}

现在，让我们暂且将通过API提供页面的步骤放在一边(AEM UI描述将涵盖该页面)，并假设该步骤已完成。 已创建资产实体并将其添加到“appImages”空间。 出于组织目的，在空间下创建了其他文件夹。 因此，资产实体在AEM JCR中存储为：

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### 获取可用资源实体的列表 {#getting-a-list-of-available-asset-entities}

应用程序开发人员可以通过检索资产实体来获取可用的资产列表。 内容服务空间端点可以通过Web服务API SDK提供该信息。

结果将是一个JSON格式的对象，它将提供“图标”文件夹中的资产列表。

![chlimage_1-156](assets/chlimage_1-156.png)

#### 获取图像 {#getting-an-image}

JSON为每个图像提供一个URL，由Content Services生成以供图像使用。

要获取“cart”图像的二进制文件，请再次使用客户端库。

## 打包HTML内容 {#packaged-html-content}

需要维护内容布局的客户需要HTML内容。 这对于使用Web容器（如Cordova Webview）显示内容的本机应用程序非常有用。

AEM Content Services将能够通过API向移动设备应用程序提供HTML内容。 希望将AEM内容公开为HTML的客户将创建指向AEM内容源的HTML页面实体。

将考虑以下选项：

* **Zip文件：** 为了尽可能在设备上正确显示，需要页面引用的所有材料 — css、JavaScript、资产等。  — 将包含在响应所在的单个压缩文件中。 将调整“HTML”页面中的引用，以使用这些文件的相对路径。
* **流：** 从AEM获取所需文件的清单。 然后使用该清单来请求所有文件(HTML、CSS、JS等) 后续请求。

![chlimage_1-157](assets/chlimage_1-157.png)

## 独立于渠道的内容 {#channel-independent-content}

与渠道无关的内容是一种无需担心布局、组件或其他特定于渠道的信息，即可公开AEM内容结构（如页面）的方法。

这些内容实体是使用内容模型生成的，用于将AEM结构转换为JSON格式。 生成的JSON数据包含有关内容数据的信息，这些数据与AEM存储库是相互分离的。 这包括返回指向资源的元数据和AEM引用链接，以及内容结构（包括实体层次结构）之间的关系。

### 管理独立于渠道的内容 {#managing-channel-independent-content}

内容可以通过多种方式到达应用程序。

1. 通过AEM Over-The-AirGET内容ZIP

   * 内容同步处理程序可以直接更新zip包，也可以通过调用现有的内容渲染器来更新

      * 平台处理程序
      * AEMM处理程序
      * 自定义处理程序

1. 直接通过内容渲染器GET内容

   * 开箱即用的默认Sling渲染器
   * AEM Mobile/Content Services内容渲染器
   * 自定义渲染
