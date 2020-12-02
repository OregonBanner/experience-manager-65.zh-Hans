---
title: 页面导出器
description: 了解如何使用AEM Page Exporter。
translation-type: tm+mt
source-git-commit: 6aee1506b54a932bae8f2521fce4488de7d2a52a
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---


# 页面导出器{#the-page-exporter}

AEM允许您将页面导出为包含图像、`.js`和`.css`文件的完整网页。

配置后，您可以通过将URL中的`html`替换为`export.zip`从浏览器请求页面导出。 这将生成一个归档(zip)文件，其中包含以html格式呈现的页面以及引用的资产。 页面中的所有路径（例如，到图像的路径）都将重写，以指向归档中包含的文件或指向服务器上的资源。 然后，可从您的浏览器下载存档(zip)文件。

>[!NOTE]
>
>根据您的浏览器和设置，下载将是：
>* 存档文件(`<page-name>.export.zip`)
>* 文件夹(`<page-name>`);有效地扩展了存档文件


## 导出页面{#exporting-a-page}

以下步骤介绍了如何导出页面，并假定站点存在导出模板。 导出模板可定义页面的导出方式，并特定于您的站点。 要创建导出模板，请参阅[为站点创建页面导出器配置](#creating-a-page-exporter-configuration-for-your-site)部分。

要导出页面，请执行以下操作：

1. 导航到&#x200B;**站点**&#x200B;控制台中的所需页面。

1. 选择该页面，然后打开&#x200B;**属性**&#x200B;对话框。

1. 选择&#x200B;**高级**&#x200B;选项卡。

1. 展开&#x200B;**导出**字段以选择导出模板。
为站点选择所需的模板，然后使用**确定**&#x200B;进行确认。

1. 选择&#x200B;**保存并关闭**&#x200B;以关闭页面属性对话框。

1. 请求导出页面，将URL中后缀`html`替换为`export.zip`。

   例如：
   * 本地主机：4502/content/we-retail/language-masters/en.html

   可通过以下方式访问：
   * localhost:4502/content/we-retail/language-masters/en.export


1. 将存档文件下载到文件系统。

1. 在文件系统中，根据需要解压缩文件。 展开后，将会有一个与选定页面同名的文件夹。 此文件夹包含：

   * 子文件夹`content`，它是反映存储库中页面路径的一系列子文件夹的根

      * 在此结构中，有选定页面的html文件(`<page-name>.html`)
   * 其他资源（`.js`文件、`.css`文件、图像等） 根据导出模板中的设置进行定位


1. 在浏览器中打开页面html文件(`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`)以检查呈现。

## 为站点{#creating-a-page-exporter-configuration-for-your-site}创建页面导出器配置

页面导出器基于[内容同步框架](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)。 **页面属性**&#x200B;对话框中的可用配置是导出模板，用于定义页面所需的依赖关系。

触发页面导出时，将引用导出模板并动态应用页面路径和设计路径。 然后，使用标准内容同步功能创建zip文件。

现成的AEM安装在`/etc/contentsync/templates/default`下包含默认模板。

* 在存储库中未找到导出模板时，此模板是回退模板。

* `default`模板会向您显示如何配置页面导出，以便作为新导出模板的基础。

* 要将浏览器中模板的节点结构视图为JSON格式，请请求以下URL:
   `http://localhost:4502/etc/contentsync/templates/default.json`

创建新页面导出器模板的最简单方法是：

* 复制`default`模板，

* 指定适合您的站点的新名称，

* 然后进行所需的更新。

要创建全新模板，请执行以下操作：

1. 在&#x200B;**CRXDE Lite**&#x200B;中，在`/etc/contentsync/templates`下创建一个节点：

   * `Name`:与您的站点相称的名称；例如 `<mysite>`,选择页面导出器模板时，该名称将显示在页面属性对话框中。

   * `Type`: `nt:unstructured`

2. 在此处调用的模板节点`mysite`下，使用下面描述的配置节点创建一个节点结构。

## 为页面{#activating-a-page-exporter-configuration-for-your-pages}激活页面导出器模板

配置模板后，您需要使其可用：

1. 在CRXDE中，导航到`/content`分支中所需的页面。 这可以是单个页面，也可以是子树的根页面。

1. 在页面的`jcr:content`节点上创建以下属性：
   * `Name`:  `cq:exportTemplate`
   * `Type`:  `String`
   * `Value`:模板的路径；例如：  `/etc/contentsync/templates/mysite`

### 页面导出器配置节点{#page-exporter-configuration-nodes}

模板由节点结构组成，因为它使用[内容同步框架](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)。  每个节点都有一个`type`属性，该属性定义了zip文件创建过程中的特定操作。

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

以下节点可用于构建导出模板：

* `page`
页面节点用于将页面html复制到zip文件。具有以下特点：

   * 是必需节点。
   * 位于`/etc/contentsync/templates/<mysite>`下。
   * 定义为属性`Name`设置为`page`。
   * 节点类型为`nt:unstructured`

   `page`节点具有以下属性：

   * 设置了值`pages`的`type`属性。

   * 它没有`path`属性，因为当前页面路径是动态复制到配置的。

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
重写节点定义链接在导出的页面中如何重写。重写的链接可以指向包含在zip文件中的文件，也可以指向服务器上的资源。
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
设计节点用于复制用于导出页面的设计。具有以下特点：

   * 是可选的。
   * 位于`/etc/contentsync/templates/<mysite>`下。
   * 定义为属性`Name`设置为`design`。
   * 节点类型为`nt:unstructured`。

   `design`节点具有以下属性：

   * 设置为值`copy`的`type`属性。

   * 它没有`path`属性，因为当前页面路径是动态复制到配置的。


* `generic`
通用节点用于复制诸如clientlibs之类的资源 
`.js` 或文 `.css` 件到zip文件。具有以下特点：

   * 是可选的。
   * 位于`/etc/contentsync/templates/<mysite>`下。
   * 没有特定名称。
   * 节点类型为`nt:unstructured`。
   * 具有`type`属性和`type`相关属性。<!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   例如，以下配置节点将`mysite.clientlibs.js`文件复制到zip文件：

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

为了满足某些特定要求，您可能需要实现[自定义更新处理程序](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html)。

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## 以编程方式导出页面{#programmatically-exporting-a-page}

要以编程方式导出页面，可以使用[PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI服务。 此服务允许您：

* 导出页面并写入HTTP servlet响应。
* 导出页面并在特定位置保存zip文件。

绑定到`export`选择器和`zip`扩展的servlet使用PageExporter服务。

## 疑难解答 {#troubleshooting}

如果下载zip文件时遇到问题，可删除存储库中的`/var/contentsync`节点，然后再次发送导出请求。
