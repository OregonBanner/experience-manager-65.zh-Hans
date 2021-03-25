---
title: RemotePage组件
description: RemotePage组件是一个自定义页面组件，用于在AEM中编辑远程React SPA。
translation-type: tm+mt
source-git-commit: 431bed450ed5b0239d9191dcf061f01e64b8981a
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# RemotePage组件{#remote-page-component}

在决定要在外部SPA和AEM之间实现何种级别的集成时，您通常需要能够在AEM内视图和编辑SPA。 RemotePage组件是一个自定义页面组件，仅用于此用途。

## 概述 {#overview}

RemotePage组件从应用程序生成的`asset-manifest.json`中获取所有必需的资产，并使用它在AEM中呈现SPA。

* RemotePage允许您将SPA的脚本和样式表注入AEM页面组件的正文中。
* 虚拟前端组件允许将部分标记为在AEM SPA编辑器中可编辑。
* 同时，可以在AEM中编辑托管在其他域上的SPA。

有关可编辑的AEM(中的外部SPA的详细信息，请参阅文章[在AEM中编辑外部SPA。](spa-edit-external.md)

## 要求{#requirements}

* 使CORS能够开发
* 在页面属性中配置远程URL
* 在AEM中渲染SPA

## 限制 {#limitations}

* RemotePage组件的当前实现仅支持远程React应用程序。
* 在AEM中进行远程渲染时，应用程序的根HTML文件中定义的内部CSS以及根DOM节点上的内联CSS将不可用。

## 技术详细信息{#technical-details}

与AEM SPA项目的其余部分一样，RemotePage组件是开放源。 有关RemotePage组件的完整技术详细信息，请参阅GitHub存储库。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)[
