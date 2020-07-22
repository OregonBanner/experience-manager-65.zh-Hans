---
title: 页面导出器
description: 了解如何使用AEM Page Exporter。
translation-type: tm+mt
source-git-commit: c152cf4bf8cf19e0fa7b328241ced753fa42f7a4
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---


# 页面导出器{#the-page-exporter}

AEM允许您将页面导出为包含图像和文件的完整网 `.js` 页 `.css` 。

配置后，您可以通过替换为URL，从浏览器 `html` 请求 `export.zip` 页面导出。 这将生成一个归档(zip)文件，其中包含以html格式呈现的页面以及引用的资产。 页面中的所有路径（例如，到图像的路径）都将重写，以指向归档中包含的文件或指向服务器上的资源。 然后，可从您的浏览器下载存档(zip)文件。

>[!NOTE]
>
>根据您的浏览器和设置，下载将是：
>* 存档文件(`<page-name>.export.zip`)
>* 文件夹(`<page-name>`); 有效地扩展了存档文件


## 导出页面 {#exporting-a-page}

以下步骤介绍了如何导出页面，并假定站点存在导出模板。 导出模板可定义页面的导出方式，并特定于您的站点。 要创建导出模板，请参阅为 [您的站点创建页面导出器配置](#creating-a-page-exporter-configuration-for-your-site) 。

要导出页面，请执行以下操作：

1. 导航到站点控制台中的所 **需页面** 。

1. 选择页面，然后打开“属 **性** ”对话框。

1. Select the **Advanced** tab.

1. 展开“ **导出** ”字段以选择导出模板。
为站点选择所需的模板，然后单击“确定” **进行确认**。

1. 选择 **保存并关闭** ，以关闭页面属性对话框。

1. 请求要导出的页面，将后缀 `html` 替换 `export.zip` 为URL中的。

   例如：
   * 本地主机：4502/content/we-retail/language-masters/en.html

   可通过以下方式访问：
   * localhost:4502/content/we-retail/language-masters/en.export


1. 将存档文件下载到文件系统。

1. 在文件系统中，根据需要解压缩文件。 展开后，将会有一个与选定页面同名的文件夹。 此文件夹包含：

   * 子文件夹， `content`它是反映存储库中页面路径的一系列子文件夹的根

      * 在此结构中，有选定页面的html文件(`<page-name>.html`)
   * 其他资源`.js` (文件 `.css` 、文件、图像等) 根据导出模板中的设置进行定位


1. 在浏览器中打开页`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`面html文件()检查呈现。

## 为站点创建页面导出器配置 {#creating-a-page-exporter-configuration-for-your-site}

页面导出器基于内容 [同步框架](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)。 “页面属性”对话 **框中提供** 的配置是导出模板，它们定义了页面所需的依赖关系。

触发页面导出时，将引用导出模板并动态应用页面路径和设计路径。 然后，使用标准内容同步功能创建zip文件。

现成的AEM安装包含下的默认模板 `/etc/contentsync/templates/default`。

* 在存储库中未找到导出模板时，此模板是回退模板。

* 该模 `default` 板会向您显示如何配置页面导出，以作为新导出模板的基础。

* 要将浏览器中模板的节点结构视图为JSON格式，请请求以下URL:
   `http://localhost:4502/etc/contentsync/templates/default.json`

创建新页面导出器模板的最简单方法是：

* 复制模 `default` 板，

* 指定适合您的站点的新名称，

* 然后进行所需的更新。

要创建全新模板，请执行以下操作：

1. 在 **CRXDE Lite中**，创建以下节点 `/etc/contentsync/templates`:

   * `Name`: 与您的站点相称的名称； 例如 `<mysite>`, 选择页面导出器模板时，该名称将显示在页面属性对话框中。

   * `Type`: `nt:unstructured`

2. 在此处调用的模板节点下， `mysite`使用下面描述的配置节点创建一个节点结构。

## 为页面激活页面导出器模板 {#activating-a-page-exporter-configuration-for-your-pages}

配置模板后，您需要使其可用：

1. 在CRXDE中，导航到分支中的所需 `/content` 页面。

1. 在页 `jcr:content` 面的节点上创建属性：
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: 模板的路径； 例如： `/etc/contentsync/templates/mysite`

### 页面导出器配置节点 {#page-exporter-configuration-nodes}

该模板由节点结构组成，因为它使用内 [容同步框架](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)。  每个节点都有 `type` 一个属性，该属性定义了在zip文件创建过程中执行的特定操作。

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

以下节点可用于构建导出模板：

* `page`
页面节点用于将页面html复制到zip文件。 具有以下特点：

   * 是必需节点。
   * 位于下 `/etc/contentsync/templates/<mysite>`方。
   * 使用设置为的属 `Name`性定义 `page`。
   * 节点类型为 `nt:unstructured`

   节 `page` 点具有以下属性：

   * 用 `type` 值设置的属性 `pages`。

   * 它没有属性， `path` 因为当前页面路径是动态复制到配置的。

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
重写节点定义链接在导出的页面中如何重写。 重写的链接可以指向包含在zip文件中的文件，也可以指向服务器上的资源。
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
设计节点用于复制用于导出页面的设计。 具有以下特点：

   * 是可选的。
   * 位于下 `/etc/contentsync/templates/<mysite>`方。
   * 使用设置为的 `Name` 属性定 `design`义。
   * 节点类型为 `nt:unstructured`。

   节 `design` 点具有以下属性：

   * 设置 `type` 为该值的属性 `copy`。

   * 它没有属性， `path` 因为当前页面路径是动态复制到配置的。


* `generic`
通用节点用于复制诸如clientlibs之类的资源 
`.js` 或 `.css` 将文件转换为zip文件。 具有以下特点：

   * 是可选的。
   * 位于下 `/etc/contentsync/templates/<mysite>`方。
   * 没有特定名称。
   * 节点类型为 `nt:unstructured`。
   * 具有属 `type` 性和相 `type` 关属性。 <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   例如，以下配置节点将文 `mysite.clientlibs.js` 件复制到zip文件：

   ```xml
   "mysite.clientlibs.js": {
       "extension": "js",
       "type": "clientlib",
       "path": "/etc/designs/mysite/clientlibs",
       "jcr:primaryType": "nt:unstructured"
   }
   ```

**实现自定义配置**

也可以进行自定义配置。

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

为了满足某些特定要求，您可能需要实现一个自定 [义更新处理程序](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html)。

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## 以编程方式导出页面 {#programmatically-exporting-a-page}

要以编程方式导出页面，您可以 [使用PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI服务。 此服务允许您：

* 导出页面并写入HTTP servlet响应。
* 导出页面并在特定位置保存zip文件。

绑定到选择器且扩 `export` 展名的Servlet `zip` 使用PageExporter服务。

## 疑难解答 {#troubleshooting}

如果您在下载zip文件时遇到问题，可以删除存储库中 `/var/contentsync` 的节点并再次发送导出请求。
