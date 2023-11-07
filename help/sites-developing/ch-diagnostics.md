---
title: ContextHub 诊断
description: ContextHub提供了一个诊断页面，您可以在该页面中查看ContextHub框架的概述
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: b833c28b-76c6-42a2-b690-3e81ddf91bc2
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---

# ContextHub 诊断 {#contexthub-diagnostics}

ContextHub提供了一个诊断页面，您可以在该页面中查看ContextHub框架的概述。 要打开页面，请转到 `contexthub.diagnostics.html` AEM第页，例如：

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

ContextHub诊断页面提供有关已创建的存储和UI模块、已加载的客户端库文件夹以及指向有用页面的链接的信息。

>[!NOTE]
>
>为了返回诊断信息，必须启用调试模式，否则诊断页面将为空白。 请参阅 [本文档](ch-configuring.md#debugging-contexthub) 以了解有关如何启用调试模式的详细信息。

>[!NOTE]
>
>对于ContextHub配置，仍位于其旧路径下，诊断页面的位置为 `http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`.

## 商店 {#stores}

存储区部分列出了已配置的所有ContextHub存储。 列表中的每个项目均包含以下信息：

* **标题：** 此 [存储类型](/help/sites-developing/ch-samplestores.md) 商店所基于的数据。
* **路径：** 保存该配置的存储库节点的路径。
* **资源类型：** 定义存储类型的存储库节点的路径。
* **clientlibs：** 加载的客户端库的类别，这些库实现存储类型。

## 模块 {#modules}

模块部分列出了已配置的所有ContextHub UI模块。 列表中的每个项目均包含以下信息：

* **标题：** 此 [UI模块类型](/help/sites-developing/ch-samplemodules.md) UI模块所基于的内容。
* **路径：** 保存该配置的存储库节点的路径。
* **资源类型：** 定义UI模块类型的存储库节点的路径。
* **clientlibs：** 加载的实现UI模块类型的客户端库的类别。

## Clientlibs {#clientlibs}

Clientlibs部分列出了ContextHub已加载的所有客户端库文件夹。 客户端库分为以下几类：

* **kernel.js：** 实施ContextHub框架、区段引擎和存储类型的客户端库。
* **ui.js：** 实施ContextHub UI和UI模块类型的客户端库。
* **style.css：** 从客户端库加载的CSS文件。

## URL {#urls}

URL部分包含指向ContextHub功能的链接：

* **配置编辑器：** 打开 [ContextHub配置页面](ch-configuring.md) 可在其中配置存储、UI模式和UI模块。

* **contexthub模块的配置：** 打开/etc/cloudsettings/default/contexthub.config.kernel.js文件，该文件包含ContextHub存储配置的JavaScript对象表示形式。
* **contexthub UI的配置：** 打开/etc/cloudsettings/default/contexthub.config.ui.js文件，该文件包含ContextHub UI模式配置的JavaScript对象表示形式。
* **kernel.js：** 打开/etc/cloudsettings/default/contexthub.kernel.js文件，该文件包含实施ContextHub框架、区段引擎和存储类型的客户端库的源代码。
* **ui.js：** 打开/etc/cloudsettings/default/contexthub.ui.js文件，该文件包含实施ContextHub UI和UI模块类型的客户端库的源代码。
* **style.css：** 打开/etc/cloudsettings/default/contexthub.styles.css文件，该文件包含ContextHub UI和UI模块的CSS样式。
