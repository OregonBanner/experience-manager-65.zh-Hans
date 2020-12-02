---
title: ContextHub诊断
seo-title: ContextHub诊断
description: ContextHub提供诊断页面，您可以在其中看到ContextHub框架的概述
seo-description: ContextHub提供诊断页面，您可以在其中看到ContextHub框架的概述
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---


# ContextHub诊断{#contexthub-diagnostics}

ContextHub提供诊断页面，您可以在其中查看ContextHub框架的概述。 要打开该页面，请转到AEM作者实例的`contexthub.diagnostics.html`页，例如：

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

ContextHub诊断页面提供有关已创建的商店和UI模块、已加载的客户端库文件夹以及指向有用页面的链接的信息。

>[!NOTE]
>
>要返回诊断信息，必须启用调试模式，否则诊断页面将为空。 有关如何启用调试模式的详细信息，请参阅[此文档](ch-configuring.md#debugging-contexthub)。

>[!NOTE]
>
>对于仍位于其旧路径下的ContextHub配置，诊断页面的位置为`http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`。

## 存储{#stores}

“存储”部分列表所有已配置的ContextHub存储。 该列表中的每个项目都包含以下信息：

* **标题：** 商 [店](/help/sites-developing/ch-samplestores.md) 所基于的商店类型。
* **path:** 保存配置的存储库节点的路径。
* **resourceType:** 定义存储类型的存储库节点的路径。
* **clientlibs:** 加载的实现存储类型的客户端库的类别。

## 模块{#modules}

“模块”部分列表已配置的所有ContextHub UI模块。 该列表中的每个项目都包含以下信息：

* **标题：** UI [模块](/help/sites-developing/ch-samplemodules.md) 所基于的UI模块类型。
* **path:** 保存配置的存储库节点的路径。
* **resourceType:** 定义UI模块类型的存储库节点的路径。
* **clientlibs:** 加载的实现UI模块类型的客户端库的类别。

## Clientlibs {#clientlibs}

Clientlibs部分列表ContextHub已加载的所有客户端库文件夹。 客户端库分类：

* **kernel.js：实** 现ContextHub框架、段引擎和存储类型的客户端库。
* **ui.js：实** 现ContextHub UI和UI模块类型的客户端库。
* **style.css：从** 客户端库加载的CSS文件。

## URL {#urls}

URL部分包含指向ContextHub功能的链接：

* **配置编辑** 器：打 [开ContextHub配](ch-configuring.md) 置页，在该页可以配置存储、UI模式和UI模块。

* **ContextHub模块的配** 置：打开/etc/cloudsettings/default/contexthub.config.kernel.js文件，该文件包含ContextHub存储配置的Javascript对象表示。
* **ContextHub UI的配置：** 打开/etc/cloudsettings/default/contexthub.config.ui.js文件，该文件包含ContextHub UI模式配置的Javascript对象表示形式。
* **kernel.js：打** 开/etc/cloudsettings/default/contexthub.kernel.js文件，该文件包含实现ContextHub框架、段引擎和存储类型的客户端库的源代码。
* **ui.js：打** 开/etc/cloudsettings/default/contexthub.ui.js文件，该文件包含实现ContextHub UI和UI模块类型的客户端库的源代码。
* **style.css：打** 开/etc/cloudsettings/default/contexthub.styles.css文件，该文件包含ContextHub UI和UI模块的CSS样式。