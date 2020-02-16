---
title: 页面导出器
seo-title: 页面导出器
description: 了解如何使用AEM Page Exporter。
seo-description: 了解如何使用AEM Page Exporter。
uuid: 2ca2b8f1-c723-4e6b-8c3d-f5886cd0d3f1
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6ab07b5b-ee37-4029-95da-be2031779107
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 页面导出器{#the-page-exporter}

AEM允许您将页面导出为包含图像、.js和。css文件的完整网页。

配置导出后，您只需在浏览器中通过URL中的替换来请求页面， `html``export.zip` 然后您会获得一个zip文件下载，其中包含以html格式呈现的页面和引用的资产。 页面中的所有路径（例如图像路径）都会重写，以指向zip文件中包含的文件或指向服务器上的资源。

## 导出页面 {#exporting-a-page}

以下步骤介绍了如何导出页面，并假定站点存在导出配置模板。 配置模板定义了导出页面的方式，并特定于您的站点。 要创建配置模板，请参阅为 [您的站点创建页面导出器配置](#creating-a-page-exporter-configuration-for-your-site) 。

要导出页面，请执行以下操作：

1. 在您的浏览器中，打开页面。 例如：
1. `http://localhost:4502/content/geometrixx/en/products/triangle.html`
1. 打开页面属性对话框，选择高 **级** 选项卡并展 **** 开导出字段集。

1. 单击放大镜图标，然后选择配置模板。 选择 **geometrixx** 模板，因为它是Geometrixx站点的默认模板。 单击&#x200B;**确定**。

1. 单击 **确定** ，关闭页面属性对话框。
1. 请求页面时，请 `html` 在URL `export.zip` 中替换。

1. 将文件 `<page-name>.export.zip` 下载到文件系统。

1. 在文件系统中，解压缩文件：

   * 页面html文件( `<page-name>.html`)位于 `<unzip-dir>/<page-path>`
   * 其他资源（.js文件、.css文件、图像……）根据导出模板中的设置进行定位。 在此示例中，一些资源在下面， `<unzip-dir>/etc`一些在下面 `<unzip-dir>/<page-path>`。

1. 在浏览器中打开页面html `<unzip-dir>/<page-path>.html`文件()以检查呈现。

## 为站点创建页面导出器配置 {#creating-a-page-exporter-configuration-for-your-site}

页面导出器基于内容同步框架。 页面属性对话框中的可用配置是配置模板。 它们为页面定义了所有必需的依赖关系。 触发页面导出时，将使用配置模板，并且页面路径和设计路径都会动态地应用于配置。 然后，使用标准内容同步功能创建zip文件。

AEM嵌入了一些模板，包括：

* 默认值 `/etc/contentsync/templates/default`。 此模板：

   * 是在存储库中未找到配置模板时的回退模板。
   * 可以作为新配置模板的基础。

* 专用于 **Geometrixx站点的** ，位于 `/etc/contentsync/templates/geometrixx`。 此模板可用作创建新模板的示例。

要创建页面导出器配置模板，请执行以下操作：

1. 在 **CRXDE Lite中**，创建以下节点 `/etc/contentsync/templates`:

   * 名称：例如， `mysite`. 选择页面导出器模板时，该名称会显示在页面属性对话框中。
   * 类型: `nt:unstructured`

1. 在此处调用的模板节点下， `mysite`使用下面描述的配置节点创建一个节点结构。

### 页面导出器配置节点 {#page-exporter-configuration-nodes}

配置模板由节点结构组成。 每个节点都有一 `type` 个属性，该属性定义了zip文件创建过程中的特定操作。 有关type属性的更多详细信息，请参阅“内容同步框架”页中的“配置类型概述”部分。

以下节点可用于构建导出配置模板：

**page node** （页面节点）用于将页面html复制到zip文件。 它具有以下特点：

* 是必需节点。
* 位于下 `/etc/contentsync/templates/<sitename>`方。
* 名字是 `page`。
* 其节点类型为 `nt:unstructured`

节 `page` 点具有以下属性：

* 用 `type` 值设置的属性 `pages`。

* 它没有属性， `path` 因为当前页面路径是动态复制到配置的。

* 其他属性在内容同步框架的配置类型概述部分中进行了介绍。

**重写节点** 重写节点定义如何在导出的页面中重写链接。 重写的链接可以指向包含在zip文件中的文件或指向服务器上的资源。

有关节点的完整说明，请参阅内容同步页 `rewrite` 面。

**设计节点** “设计”节点用于复制用于导出页面的设计。 它具有以下特点：

* 是可选的。
* 位于下 `/etc/contentsync/templates/<sitename>`方。
* 名字是 `design`。
* 其节点类型 `nt:unstructured`为。

节 `design` 点具有以下属性：

* 设置 `type` 为该值的属性 `copy`。

* 它没有属性， `path` 因为当前页面路径是动态复制到配置的。

**通用节点** 通用节点用于将clientlibs .js或。css文件等资源复制到zip文件。 它具有以下特点：

* 是可选的。
* 位于下 `/etc/contentsync/templates/<sitename>`方。
* 没有特定名称。
* 其节点类型 `nt:unstructured`为。
* 具有在内 `type` 容同步框架 `type` 的配置类型概述部分中定义的属性和任何相关属性。

例如，以下配置节点将geometrixx clientlibs .js文件复制到zip文件：

```xml
"geometrixx.clientlibs.js": {
    "extension": "js",
    "type": "clientlib",
    "path": "/etc/designs/geometrixx/clientlibs",
    "jcr:primaryType": "nt:unstructured"
}
```

Geometrixx **** page export configuration template向您显示如何配置页面导出。 要以json格式查看浏览器中模板的节点结构，请请求以下URL:

`http://localhost:4502/etc/contentsync/templates/geometrixx.-1.json`

**实施自定义配置**

正如您在节点结构中注意到的， **Geometrixx** page export configuration template有一个 `logo` 将属性设置为 `type` 的节点 `image`。 这是一种特殊的配置类型，已创建该配置类型以将图像徽标复制到zip文件。 要满足某些特定要求，您可能需要实现自定义属 `type` 性：为此，请参阅“内容同步”页中的“实施自定义更新处理程序”一节。

## 以编程方式导出页面 {#programmatically-exporting-a-page}

要以编程方式导出页面，您可以使 [用PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI服务。 此服务允许您：

* 导出页面并写入HTTP servlet响应。
* 导出页面并将zip文件保存在特定位置。

绑定到选择器和扩展 `export` 的Servlet使 `zip` 用PageExporter服务。

## 疑难解答 {#troubleshooting}

如果您在下载zip文件时遇到问题，可以删除存储库中的 `/var/contentsync` 节点，然后再次发送导出请求。

