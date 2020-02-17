---
title: 内容交付
seo-title: 内容交付
description: 'null'
seo-description: 'null'
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 内容交付{#content-delivery}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

移动应用程序应能根据需要使用AEM中的任何和所有内容来提供目标应用程序体验。

这包括使用资产、站点内容、CaaS内容（无线）和可能具有其自身结构的自定义内容。

>[!NOTE]
>
>**Over-the-Air内容可以通过** ContentSync处理程序来自以上任何一种。 它可用于通过zip进行批量包和交付，以及维护更新或这些包。

内容服务提供的材料有三种主要类型：

1. **Assets**
1. **打包的HTML内容(HTML/CSS/JS)**
1. **与渠道无关的内容**

![chlimage_1-154](assets/chlimage_1-154.png)

## 资产 {#assets}

资产收藏集是AEM构造，包含对其他收藏集的引用。

资产集合可以通过内容服务公开。 在请求中调用资产集合会返回一个对象，该对象是资产列表，包括其URL。 资产可通过URL访问。 URL在对象中提供。 例如：

* 页面实体返回包含图像引用的JSON（页面对象）。 图像引用是用于获取图像的资产二进制文件的URL。
* 请求文件夹中的资产列表将返回JSON，其中包含该文件夹中所有实体的详细信息。 该列表是一个对象。 JSON包含URL引用，用于获取该文件夹中每个资产的资产二进制文件。

### 资产优化 {#asset-optimization}

Content services的一个关键价值是能够返回为设备优化的资产。 这降低了本地设备存储需求并提高了应用程序性能。

根据API请求中提供的信息，资产优化将是服务器端功能。 如果可能，应缓存资产演绎版，这样类似的请求就不需要重新生成资产演绎版。

### 资产工作流 {#assets-workflow}

资产工作流如下所示：

1. AEM现成版中提供的资产引用
1. 创建给定模型的资产引用实体
1. 编辑实体

   1. 挑选资产或资产收藏集
   1. 自定义JSON渲染

下图显示了资产引 **用工作流**:

![chlimage_1-155](assets/chlimage_1-155.png)

### 管理资产 {#managing-assets}

内容服务提供对AEM托管资产的访问，这些资产可能不通过其他AEM内容引用。

#### 现有托管资产 {#existing-managed-assets}

现有AEM Sites和Assets用户正在使用AEM Assets管理所有渠道的所有数字材料。 他们正在开发本机移动应用程序，并需要使用由AEM资产管理的多个资产。 例如徽标、背景图像、按钮图标等。

目前，这些资源分布在资产存储库周围。 应用程序需要引用的文件位于：

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### 访问CS资产实体 {#accessing-cs-asset-entities}

现在，我们暂且不要考虑如何通过API使页面可用的步骤（AEM UI描述将涵盖该页面），并假定页面已完成。 资产实体已创建并添加到“appImages”空间。 为了组织目的，在该空间下创建了其他文件夹。 因此，资产实体将作为以下对象存储在AEM JCR中：

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### 获取可用资产实体列表 {#getting-a-list-of-available-asset-entities}

应用程序开发人员可以通过检索资产实体来获取可用资产的列表。 Content services空间端点可以通过Web服务API SDK提供该信息。

结果将是一个JSON格式的对象，它将在“icons”文件夹中提供资产列表。

![chlimage_1-156](assets/chlimage_1-156.png)

#### 获取图像 {#getting-an-image}

JSON为每个图像提供一个URL，由内容服务生成该图像。

要获取“购物车”映像的二进制文件，将再次使用客户端库。

## 打包的HTML内容 {#packaged-html-content}

需要维护内容布局的客户需要HTML内容。 这对于使用Web容器（如Cordova Webview）显示内容的本机应用程序很有用。

AEM Content services将能够通过API向移动应用程序提供HTML内容。 希望将AEM内容显示为HTML的客户将创建指向AEM内容源的HTML页面实体。

考虑以下选项：

* **** Zip文件：为了尽可能在设备上正确显示，页面的所有引用材料-css、JavaScript、资源等。 -将包含在单个压缩文件中并做出响应。 将调整HTML页中的引用，以使用这些文件的相对路径。
* **** 流：从AEM获取所需文件的清单。 然后使用该清单请求所有文件（HTML、CSS、JS等）和后续请求。

![chlimage_1-157](assets/chlimage_1-157.png)

## 渠道无关内容 {#channel-independent-content}

渠道无关内容是一种公开AEM内容构造（如页面）的方式，无需担心布局、组件或其他渠道特定信息。

这些内容实体是使用内容模型生成的，以将AEM结构转换为JSON格式。 生成的JSON数据包含有关内容数据的信息，该信息与AEM存储库相分离。 这包括返回元数据和AEM引用资产链接以及内容结构（包括实体层次结构）之间的关系。

### 管理与渠道无关的内容 {#managing-channel-independent-content}

内容可以通过多种方式访问应用程序。

1. 通过AEM Over-the-Air获取内容ZIP

   * 内容同步处理程序可以直接更新zip包或通过调用现有内容渲染器来更新zip包

      * 平台处理程序
      * AEMM处理程序
      * 自定义处理函数

1. 直接通过内容呈示器获取内容

   * 现成默认Sling渲染器
   * AEM Mobile/Content services内容渲染器
   * 自定义渲染

