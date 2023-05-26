---
title: RemotePage 组件
description: RemotePage组件是一个自定义页面组件，用于在AEM中编辑远程React SPA。
exl-id: 3f015997-0d42-4241-a890-0f16a19c5e34
source-git-commit: 41aac3b4ea3b100e9d927bef161929477d667a95
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---

# RemotePage 组件 {#remote-page-component}

在决定外部SPA与AEM之间的集成级别时，通常需要能够在AEM中查看和编辑SPA，这一点很明显。 RemotePage组件只是用于此目的的自定义页面组件。

## 概述 {#overview}

RemotePage组件从应用程序生成的中提取所有必需的资源 `asset-manifest.json` 和使用此项在AEM中渲染SPA。

* RemotePage允许您将SPA的脚本和样式表插入AEM Page组件的正文中。
* 虚拟前端组件允许在AEM SPA编辑器中将部分标记为可编辑。
* 托管在不同域上的SPA可以一起在AEM中编辑。

请参阅文章 [在AEM中编辑外部SPA](spa-edit-external.md) 有关AEM中可编辑的外部SPA的更多详细信息。

## 要求 {#requirements}

* 在开发中启用CORS
* 在页面属性中配置远程URL
* 在AEM中渲染SPA
* Web应用程序必须使用类似于以下内容的捆绑器资产清单，并在域根目录下公开一个asset-manifest.json文件，该文件在入口点属性中列出了要加载的所有CSS和JS文件：
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

   ![入口点](assets/asset-manifest-entrypoints.png)

* 应用程序必须能够在中初始化 `<div id="root"></div>` 主体元素下。 如果应用程序需要不同的标记才能实例化，则必须在具有的代理组件的HTL脚本中相应地调整此设置 `sling:resourceSuperType="spa-project-core/components/remotepage`.

## 限制 {#limitations}

* RemotePage组件要求实施提供与资产清单类似的资产清单 [此处找到。](https://github.com/shellscape/webpack-manifest-plugin) 但是，RemotePage组件仅经过测试，可以与React框架（和通过remote-page-next组件的Next.js）配合使用，因此不支持从其他框架(如Angular)远程加载应用程序。
* 在AEM中执行远程渲染时，在应用程序的根HTML文件中定义的内部CSS以及根DOM节点上的内联CSS将不可用。

## 技术详细信息 {#technical-details}

与AEM SPA项目的其余部分一样，RemotePage组件是开源的。 有关RemotePage组件的完整技术详细信息， [请参阅GitHub存储库。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
