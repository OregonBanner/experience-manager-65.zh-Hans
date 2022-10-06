---
title: 页面导出程序
description: 了解如何使用AEM Page Exporter。
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---

# 页面导出程序{#the-page-exporter}

AEM允许您将页面导出为包括图像在内的完整网页， `.js` 和 `.css` 文件。

配置完毕后，您可以通过将 `html` with `export.zip` 中。 这会生成一个存档(zip)文件，其中包含以html格式呈现的页面以及引用的资产。 页面中的所有路径（例如，到图像的路径）都将被重写，以指向存档中包含的文件，或指向服务器上的资源。 然后，可以从您的浏览器下载存档(zip)文件。

>[!NOTE]
>
>根据您的浏览器和设置，下载内容将为：
>* 存档文件(`<page-name>.export.zip`)
>* 文件夹(`<page-name>`);有效地扩展了存档文件


## 导出页面 {#exporting-a-page}

以下步骤描述如何导出页面，并假定您的网站存在导出模板。 导出模板可定义页面的导出方式，并特定于您的网站。 要创建导出模板，请参阅 [为站点创建页面导出程序配置](#creating-a-page-exporter-configuration-for-your-site) 中。

要导出页面，请执行以下操作：

1. 导航到 **站点** 控制台。

1. 选择页面，然后打开 **属性** 对话框。

1. 选择 **高级** 选项卡。

1. 展开 **导出** 字段来选择导出模板。
为您的网站选择所需的模板，然后使用进行确认 **确定**.

1. 选择 **保存并关闭** 以关闭页面属性对话框。

1. 请求导出页面，替换后缀 `html` with `export.zip` 中。

   例如：
   * localhost:4502/content/we-retail/language-masters/en.html

   通过以下方式访问：
   * localhost:4502/content/we-retail/language-masters/en.export


1. 将存档文件下载到您的文件系统。

1. 在文件系统中，根据需要解压缩文件。 展开后，将有一个与选定页面同名的文件夹。 此文件夹包含：

   * 子文件夹 `content`，是反映存储库中页面路径的一系列子文件夹的根

      * 在此结构中，有用于选定页面的html文件(`<page-name>.html`)
   * 其他资源(`.js` 文件， `.css` 文件、图像等) 根据导出模板中的设置进行定位


1. 打开页面html文件(`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`)以检查渲染。

## 为站点创建页面导出程序配置 {#creating-a-page-exporter-configuration-for-your-site}

页面导出器基于 [内容同步框架](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html). 中可用的配置 **页面属性** 对话框是用于定义页面所需依赖项的导出模板。

触发页面导出时，将引用导出模板，并动态应用页面路径和设计路径。 然后，可使用标准的内容同步功能创建zip文件。

开箱即用的AEM安装包含 `/etc/contentsync/templates/default`.

* 当在存储库中未找到导出模板时，此模板便是回退模板。

* 的 `default` 模板可显示如何配置页面导出，以便用作新导出模板的基础。

* 要以JSON格式查看浏览器中模板的节点结构，请请求以下URL:
   `http://localhost:4502/etc/contentsync/templates/default.json`

创建新页面导出器模板的最简单方法是：

* 复制 `default` 模板，

* 为您的网站指定一个新名称，

* 然后进行所需的更新。

要创建全新的模板，请执行以下操作：

1. 在 **CRXDE Lite**，请在下面创建节点 `/etc/contentsync/templates`:

   * `Name`:与您的网站相称的名称；例如， `<mysite>`. 选择页面导出器模板时，该名称会显示在页面属性对话框中。

   * `Type`: `nt:unstructured`

2. 在模板节点下方，调用此处 `mysite`，请使用下面描述的配置节点创建节点结构。

## 为页面激活页面导出器模板 {#activating-a-page-exporter-configuration-for-your-pages}

配置模板后，您需要使其可用：

1. 在CRXDE中，导航到 `/content` 分支。 这可以是单个页面，也可以是子树的根页面。

1. 在 `jcr:content` 页面的节点创建属性：
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`:模板路径；例如： `/etc/contentsync/templates/mysite`

### 页面导出程序配置节点 {#page-exporter-configuration-nodes}

模板由节点结构组成，因为它使用 [内容同步框架](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html).  每个节点都有 `type` 属性，该属性定义在zip文件创建过程中执行的特定操作。

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

以下节点可用于构建导出模板：

* `page`
页面节点用于将页面html复制到zip文件。 具有以下特点：

   * 是强制节点。
   * 位于下方 `/etc/contentsync/templates/<mysite>`.
   * 使用属性定义 `Name`设置为 `page`.
   * 节点类型为 `nt:unstructured`

   的 `page` 节点具有以下属性：

   * A `type` 为值设置的属性 `pages`.

   * 它没有 `path` 属性，因为当前页面路径会动态复制到配置中。

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
重写节点定义链接在导出的页面中的重写方式。 重写的链接可以指向zip文件中包含的文件，也可以指向服务器上的资源。
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
设计节点用于复制用于导出页面的设计。 具有以下特点：

   * 是可选的。
   * 位于下方 `/etc/contentsync/templates/<mysite>`.
   * 使用属性定义 `Name` 设置为 `design`.
   * 节点类型为 `nt:unstructured`.

   的 `design` 节点具有以下属性：

   * A `type` 属性设置为值 `copy`.

   * 它没有 `path` 属性，因为当前页面路径会动态复制到配置中。


* `generic`
通用节点用于复制诸如clientlibs之类的资源 
`.js` 或 `.css` 文件到zip文件。 具有以下特点：

   * 是可选的。
   * 位于下方 `/etc/contentsync/templates/<mysite>`.
   * 没有特定名称。
   * 节点类型为 `nt:unstructured`.
   * 具有 `type` 资产和 `type` 相关属性。 <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   例如，以下配置节点复制 `mysite.clientlibs.js` 文件到zip文件：

   ```xml
   "mysite.clientlibs.js": {
       "extension": "js",
       "type": "clientlib",
       "path": "/etc/designs/mysite/clientlibs",
       "jcr:primaryType": "nt:unstructured"
   }
   ```

**实施自定义配置**

也可以使用自定义配置。

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

要满足某些特定要求，您可能需要实施 [自定义更新处理程序](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## 以编程方式导出页面 {#programmatically-exporting-a-page}

要以编程方式导出页面，您可以使用 [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI服务。 此服务允许您：

* 导出页面并写入HTTP Servlet响应。
* 导出页面并在特定位置保存zip文件。

绑定到的Servlet `export` 选择器和 `zip` 扩展使用PageExporter服务。

## 疑难解答 {#troubleshooting}

如果您在下载zip文件时遇到问题，可以删除 `/var/contentsync` 节点，然后再次发送导出请求。
