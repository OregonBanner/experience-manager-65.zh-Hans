---
title: ContextHub诊断
seo-title: ContextHub诊断
description: ContextHub提供了诊断页面，您可以在其中查看ContextHub框架的概述
seo-description: ContextHub提供了诊断页面，您可以在其中查看ContextHub框架的概述
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: e37ff1c9e657c580c607f2656adca01a2b39f81f

---


# ContextHub诊断 {#contexthub-diagnostics}

ContextHub提供了诊断页面，您可以在其中查看ContextHub框架的概述。 要打开页面，请转到AEM作 `contexthub.diagnostics.html` 者实例的页面，例如：

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

“ContextHub诊断”页提供有关已创建的商店和UI模块、已加载的客户端库文件夹以及指向有用页面的链接的信息。

>[!NOTE]
>
>要返回诊断信息，必须启用调试模式，否则诊断页面将为空。 有关如何启 [用调试模式](/help/sites-administering/contexthub-config.md#debugging-contexthub) ，请参阅本文档。

>[!NOTE]
>
>对于仍位于其旧版路径下的ContextHub配置，诊断页面的位置为 `http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`。

## 商店 {#stores}

“商店”部分列出所有已配置的ContextHub存储。 列表中的每个项目都包含以下信息：

* **** 标题：存 [储所基于的存储类型](/help/sites-developing/ch-samplestores.md) 。
* **** 路径：保存配置的存储库节点的路径。
* **** resourceType:定义存储类型的存储库节点的路径。
* **** clientlibs:加载的实现存储类型的客户端库的类别。

## 模块 {#modules}

“模块”部分列出已配置的所有ContextHub UI模块。 列表中的每个项目都包含以下信息：

* **** 标题：UI [模块所基于的](/help/sites-developing/ch-samplemodules.md) “UI模块”类型。
* **** 路径：保存配置的存储库节点的路径。
* **** resourceType:定义UI模块类型的存储库节点的路径。
* **** clientlibs:加载的客户端库的类别，这些库实现UI模块类型。

## Clientlibs {#clientlibs}

“Clientlibs”部分列出ContextHub已加载的所有客户端库文件夹。 客户端库分为以下几类：

* **** kernel.js:实现ContextHub框架、区段引擎和存储类型的客户端库。
* **** ui.js:实现ContextHub UI和UI模块类型的客户端库。
* **** style.css:从客户端库加载的CSS文件。

## URL {#urls}

URL部分包含指向ContextHub功能的链接：

* **** 配置编辑器：打开“ [ContextHub配置”页](/help/sites-administering/contexthub-config.md) ，您可以在该页中配置存储、UI模式和UI模块。

* **** ContextHub模块的配置：打开/etc/cloudsettings/default/contexthub.config.kernel.js文件，其中包含ContextHub存储配置的Javascript对象表示形式。
* **** ContextHub UI的配置：打开/etc/cloudsettings/default/contexthub.config.ui.js文件，其中包含ContextHub UI模式配置的Javascript对象表示形式。
* **** kernel.js:打开/etc/cloudsettings/default/contexthub.kernel.js文件，该文件包含实现ContextHub框架、区段引擎和存储类型的客户端库的源代码。
* **** ui.js:打开/etc/cloudsettings/default/contexthub.ui.js文件，该文件包含实现ContextHub UI和UI模块类型的客户端库的源代码。
* **** style.css:打开/etc/cloudsettings/default/contexthub.styles.css文件，其中包含ContextHub UI和UI模块的CSS样式。