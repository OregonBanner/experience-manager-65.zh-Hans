---
title: 内容交付
seo-title: 内容交付
description: 内容交付
seo-description: 'null'
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
exl-id: 85e73679-684e-402f-8186-8b56d8bd9372
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# 内容交付{#content-delivery}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

移动设备应用程序应该能够根据需要在AEM中使用任何和所有内容来提供目标应用程序体验。

这包括使用资产、网站内容、CaaS内容（空中）和可能具有其自身结构的自定义内容。

>[!NOTE]
>
>**Over-the-Air Content可以通** 过ContentSync处理程序从以上任何位置获取。它可用于通过zip批量打包和交付，以及维护更新或这些包。

内容服务提供的材料有三种主要类型：

1. **资产**
1. **打包的HTML内容(HTML/CSS/JS)**
1. **与渠道无关的内容**

![chlimage_1-154](assets/chlimage_1-154.png)

## 资产 {#assets}

资产收藏集是AEM结构，其中包含对其他收藏集的引用。

资产集合可以通过内容服务公开。 在请求中调用资产集合会返回一个资产列表（包括其URL）的对象。 通过URL访问资产。 URL在对象中提供。 例如：

* 页面实体返回包含图像引用的JSON（页面对象）。 图像引用是用于获取图像资产二进制文件的URL。
* 请求文件夹中的资产列表会返回JSON，其中包含该文件夹中所有实体的详细信息。 该列表是一个对象。 JSON具有URL引用，用于获取该文件夹中每个资产的资产二进制文件。

### 资产优化{#asset-optimization}

内容服务的一个关键价值是能够返回针对设备优化的资产。 这减少了本地设备存储需求并改进了应用程序性能。

根据API请求中提供的信息，资产优化将是一个服务器端函数。 尽可能地，应缓存资产演绎版，以便类似请求无需重新生成资产演绎版。

### 资产工作流{#assets-workflow}

资产工作流如下所示：

1. AEM即装即用中的资产引用
1. 创建资产引用实体（给定其模型）
1. 编辑实体

   1. 选取资产或资产收集
   1. 自定义JSON渲染

下图显示了&#x200B;**资产引用工作流**:

![chlimage_1-155](assets/chlimage_1-155.png)

### 管理资产 {#managing-assets}

内容服务提供对AEM托管资产的访问，这些资产可能不会通过其他AEM内容引用。

#### 现有托管资产{#existing-managed-assets}

现有的AEM Sites和Assets用户正在使用AEM Assets管理其所有渠道的所有数字材料。 他们正在开发本机移动设备应用程序，需要使用多个由AEM Assets管理的资产。 例如徽标、背景图像、按钮图标等。

目前，这些量度分布在资产存储库中。 应用程序需要引用的文件位于：

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### 访问CS资产实体{#accessing-cs-asset-entities}

现在，让我们暂且搁置有关如何通过API提供页面的步骤(AEM UI描述将介绍该页面)，并假定该页面已完成。 资产实体已创建并添加到“appImages”空间。 出于组织目的，在空间下创建了其他文件夹。 因此，资产实体将作为以下内容存储在AEM JCR中：

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### 获取可用资产实体列表{#getting-a-list-of-available-asset-entities}

应用程序开发人员可以通过检索资产实体来获取可用资产的列表。 内容服务空间端点可以通过Web服务API SDK提供该信息。

结果将是JSON格式的对象，该对象将在“图标”文件夹中提供资产列表。

![chlimage_1-156](assets/chlimage_1-156.png)

#### 获取图像{#getting-an-image}

JSON为由Content Services生成的每个图像提供一个URL给该图像。

要获取“购物车”映像的二进制文件，请再次使用客户端库。

## 打包的HTML内容{#packaged-html-content}

需要维护内容布局的客户需要HTML内容。 这对于使用Web容器（如Cordova Web视图）显示内容的本机应用程序非常有用。

AEM Content Services将能够通过API向移动设备应用程序提供HTML内容。 希望以HTML形式显示AEM内容的客户将创建一个指向AEM内容源的HTML页面实体。

考虑以下选项：

* **Zip文件：** 为了在设备上正确显示，请尽可能保留页面的所有引用材料 — css、JavaScript、资产等。 — 将包含在包含响应的单个压缩文件中。 HTML页面中的引用将被调整为使用这些文件的相对路径。
* **流：** 从AEM获取所需文件的清单。然后，使用该清单请求所有文件（HTML、CSS、JS等） 的次数。

![chlimage_1-157](assets/chlimage_1-157.png)

## 与渠道无关的内容{#channel-independent-content}

独立于渠道的内容是公开AEM内容结构（如页面）的一种方式，它无需担心布局、组件或其他渠道特定信息。

这些内容实体是使用内容模型生成的，用于将AEM结构转换为JSON格式。 生成的JSON数据包含有关内容数据的信息，这些信息与AEM存储库相分离。 这包括返回元数据和AEM引用链接到资产，以及内容结构（包括实体层次结构）之间的关系。

### 管理与渠道无关的内容{#managing-channel-independent-content}

内容可以通过多种方式访问应用程序。

1. GET内容通过AEM的无线传送

   * 内容同步处理程序可以直接更新zip包，也可以通过调用现有内容渲染器来更新zip包

      * 平台处理程序
      * AEMM处理程序
      * 自定义处理程序

1. GET内容直接通过内容渲染器进行

   * 现成的默认Sling渲染器
   * AEM Mobile/Content Services内容渲染器
   * 自定义呈现
