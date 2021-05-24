---
title: RemotePage组件
description: RemotePage组件是一个自定义页面组件，用于在AEM中编辑远程React SPA。
exl-id: 3f015997-0d42-4241-a890-0f16a19c5e34
source-git-commit: a92358d187aa78e05dd9b5a7bd4ae14bf0972f62
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# RemotePage组件{#remote-page-component}

在决定要在外部SPA与AEM之间实现的集成级别时，通常可以清楚地知道，您需要能够在AEM中查看和编辑SPA。 RemotePage组件是一个自定义页面组件，仅用于此目的。

## 概述 {#overview}

RemotePage组件从应用程序生成的`asset-manifest.json`中提取所有必需的资产，并将其用于在AEM中渲染SPA。

* RemotePage允许您将SPA的脚本和样式表注入AEM页面组件的正文中。
* 虚拟前端组件允许在AEM SPA编辑器中将部分标记为可编辑。
* 同时，可以使在其他域上托管的SPA在AEM中可编辑。

有关AEM中可编辑外部SPA的更多详细信息，请参阅文章[在AEM中编辑外部SPA](spa-edit-external.md)。

## 要求 {#requirements}

* 在开发中启用CORS
* 在页面属性中配置远程URL
* 在AEM中渲染SPA
* Web应用程序必须使用与以下任一内容类似的捆绑器资产清单，并在域根目录下公开asset-manifest.json文件，该文件在入口点属性中列出要加载的所有CSS和JS文件：
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

   ![入口点](assets/asset-manifest-entrypoints.png)

* 应用程序必须能够在主体元素下方的`<div id="root"></div>`中初始化。 如果应用程序要实例化需要其他标记，则必须在具有`sling:resourceSuperType="spa-project-core/components/remotepage`的代理组件的HTL脚本中相应地调整此标记。

## 限制 {#limitations}

* RemotePage组件的当前实施仅支持远程React应用程序。
* 在AEM中进行远程渲染时，在应用程序的根HTML文件中定义的内部CSS以及根DOM节点上的内联CSS将不可用。

## 技术详细信息{#technical-details}

与AEM SPA项目的其余部分一样， RemotePage组件是开源组件。 有关RemotePage组件的完整技术详细信息，请[参阅GitHub存储库。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
