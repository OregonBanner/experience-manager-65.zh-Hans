---
title: 内容投放
seo-title: 内容投放
description: 'null'
seo-description: 'null'
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---


# 内容投放{#content-delivery}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

移动应用程序应能够根据需要使用AEM中的任何和所有内容来提供目标应用程序体验。

这包括使用资产、站点内容、CaaS内容（无线）以及可能具有其自身结构的自定义内容。

>[!NOTE]
>
>**Over-the-Air Content** 可通过ContentSync处理程序从以上任何一种方式获得。它可用于通过zip对包和投放进行批处理，以及维护更新或这些包。

内容服务提供的材料有三种主要类型：

1. **资产**
1. **打包的HTML内容(HTML/CSS/JS)**
1. **渠道无关内容**

![chlimage_1-154](assets/chlimage_1-154.png)

## 资产 {#assets}

资产收藏集是包含对其他收藏集的引用的AEM构造。

资产集合可以通过内容服务公开。 在请求中调用资产集合会返回资产的列表对象，包括其URL。 资产可通过URL访问。 URL在对象中提供。 例如：

* 页面实体返回包含图像引用的JSON（页面对象）。 图像引用是一个URL，用于获取图像的资产二进制文件。
* 请求列表文件夹中的资产将返回JSON，其中包含有关该文件夹中所有实体的详细信息。 那列表是个对象。 JSON具有URL引用，用于获取该文件夹中每个资产的二进制资产。

### 资产优化{#asset-optimization}

Content Services的一个关键价值是能够返回为设备优化的资产。 这降低了本地设备存储需求并提高了应用程序性能。

资产优化将基于API请求中提供的信息成为服务器端功能。 在可能的情况下，应缓存资产演绎版，这样类似的请求就不需要重新生成资产演绎版。

### 资产工作流{#assets-workflow}

资产工作流如下所示：

1. AEM开箱即用中的资产引用
1. 创建给定模型的资产引用实体
1. 编辑实体

   1. 选择资产或资产收集
   1. 自定义JSON渲染

下图显示了&#x200B;**资产引用工作流**:

![chlimage_1-155](assets/chlimage_1-155.png)

### 管理资产 {#managing-assets}

内容服务提供对AEM托管资产的访问，这些资产可能不通过其他AEM内容引用。

#### 现有托管资产{#existing-managed-assets}

现有的AEM Sites和资产用户正在使用AEM Assets管理其面向所有渠道的所有数字材料。 他们正在开发本机移动应用程序，需要使用由AEM Assets管理的多个资源。 例如徽标、背景图像、按钮图标等。

目前，这些资源分布在资产存储库周围。 应用程序需要引用的文件位于：

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### 访问CS资产实体{#accessing-cs-asset-entities}

现在，让我们暂且搁置通过API提供页面的步骤(它将在AEM UI描述中介绍)，并假定页面已完成。 资产实体已创建并添加到“appImages”空间。 为组织目的，在空间下创建了其他文件夹。 因此，资产实体存储在AEM JCR中为：

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### 获取可用资产实体的列表{#getting-a-list-of-available-asset-entities}

应用程序开发人员可以通过检索资产实体来列表可用的资产。 Content Services空间端点可以通过Web服务API SDK提供该信息。

结果将是JSON格式的对象，该对象将提供“icons”文件夹中资产的列表。

![chlimage_1-156](assets/chlimage_1-156.png)

#### 获取图像{#getting-an-image}

JSON为每个图像提供由内容服务生成的URL，用于图像。

要获取“购物车”映像的二进制文件，将再次使用客户端库。

## 打包的HTML内容{#packaged-html-content}

需要维护内容布局的客户需要HTML内容。 这对于使用Web容器（如Cordova Webview）显示内容的本机应用程序很有用。

AEM Content Services将能够通过API向移动应用程序提供HTML内容。 希望将AEM内容显示为HTML的客户将创建指向AEM内容源的HTML页面实体。

考虑以下选项：

* **Zip文件：** 要在设备上正确显示，请尽可能使用页面的所有引用材料- css、JavaScript、资源等。-将包含在具有响应的单个压缩文件中。 HTML页面中的引用将被调整为使用这些文件的相对路径。
* **流：** 从AEM获取所需文件的清单。然后使用该清单请求所有文件（HTML、CSS、JS等） 和后续请求。

![chlimage_1-157](assets/chlimage_1-157.png)

## 渠道独立内容{#channel-independent-content}

渠道独立内容是一种展示AEM内容结构（如页面）的方式，无需担心布局、组件或其他渠道特定信息。

这些内容实体是使用内容模型生成的，用于将AEM结构转换为JSON格式。 生成的JSON数据包含与内容数据相关的信息，该信息与AEM存储库相分离。 这包括返回元数据和AEM资产引用链接以及内容结构（包括实体层次结构）之间的关系。

### 管理渠道独立内容{#managing-channel-independent-content}

内容可以通过多种方式访问应用程序。

1. GET内容通过AEM Over-the-Air实现ZIPS

   * 内容同步处理程序可以直接更新zip包或通过调用现有内容呈示器来更新zip包

      * 平台处理程序
      * AEMM处理程序
      * 自定义处理函数

1. 通过内容呈示器直接GET内容

   * 现成默认Sling渲染器
   * AEM Mobile/内容服务内容渲染器
   * 自定义渲染

