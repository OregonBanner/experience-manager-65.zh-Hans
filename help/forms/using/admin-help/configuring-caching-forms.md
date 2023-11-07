---
title: 为Forms配置缓存
seo-title: Configuring caching for Forms
description: 了解如何配置缓存设置以及如何对缓存的注意事项进行群集。
seo-description: Learn how to configure cache settings and how to cluster considerations for caches.
uuid: 70f36191-4163-410b-991a-e1481488aea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8a07dddf-1281-45ac-a55e-4333b860a261
exl-id: 6b57d00e-5ba0-41ee-8497-49ecfec5b9ed
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 0%

---

# 为Forms配置缓存{#configuring-caching-for-forms}

Forms服务采用在Designer中创建的表单设计，并以各种格式呈现它们。

管理控制台中的“Forms”页面包含控制Forms服务缓存项目的方式的设置。 您可以调整这些设置以优化Forms服务的性能。

Forms服务缓存以下项目：

* **表单设计：** Forms服务缓存从存储库或HTTP源检索的表单设计。 此缓存可提高性能，因为对于后续渲染请求，Forms服务会从缓存而不是存储库检索表单设计。
* **片段和图像：** Forms服务可以缓存表单设计中使用的片段和图像。 当Forms服务缓存这些对象时，它会提高性能，因为片段和图像仅在第一次请求时才会从存储库中读取。
* **表单：** Forms服务缓存其渲染的表单。 此类缓存可提高性能，因为Forms服务不需要在后续请求中解析和呈现相同的表单。

Forms将缓存存储在两个位置：

* **在内存中：** 项目存储在内存中以便快速访问。 内存中缓存的大小有限，重新启动服务器时会将其删除。
* **在磁盘上：** 项目存储在服务器的文件系统中。 磁盘缓存的容量比内存中的缓存大，重新启动服务器时会保留磁盘缓存。 磁盘缓存的位置取决于您的应用程序服务器。 有关更改磁盘缓存位置的信息，请参见 [为Forms配置位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).

## 指定高速缓存模式 {#specifying-the-cache-mode}

Forms支持两种缓存模式：

* 无条件
* 使用缓存检查点

如果在缓存模式之间切换，请重新启动Forms服务以使更改生效。 要重新启动此服务，请使用Workbench或参阅 [启动或停止与AEM表单模块关联的服务](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 以获取说明。

在模式之间切换时，会自动重置缓存检查点时间。

### 使用无条件缓存 {#using-unconditional-caching}

在此模式中，当Forms服务收到请求时，将验证所需的资源（表单设计以及片段和图像等相关资源）。 Forms服务会将存储库中资源的时间戳与缓存中资源的时间戳进行比较。 如果缓存中的资源较旧，则Forms服务会更新该资源。

此缓存模式可确保使用最新的资源。 但是，性能会受到影响，因为Forms服务会在每次请求时根据存储库验证缓存的项目。 此缓存模式适用于开发和暂存环境，在这些环境中，资源更新频繁并且性能不是主要问题。

**指定无条件缓存**

1. 在管理控制台中，单击服务> Forms。
1. 在Forms缓存控制设置下，无条件选择并单击保存。

### 使用缓存检查点 {#use-the-cache-check-point}

在此模式下，仅当缓存资源的时间戳早于缓存检查点时间时，Forms服务才会检查存储库中是否有较新版本的资源。 上次缓存检查点时间显示在管理控制台的Forms页面上。

在高性能生产环境中使用此缓存模式，此时需要考虑性能问题并且资源更改不频繁。 当要部署对存储库资源所做的任何更改时，可以重置缓存检查点。

**指定高速缓存检查点的使用**

1. 在Administration Console中，单击服务> Forms。
1. 在“Forms缓存控制设置”下，仅当上一次验证是在缓存检查点时间之前完成时，才选择，然后单击“保存”。

**重置缓存检查点**

1. 在管理控制台中，单击服务> Forms。
1. 在“Forms缓存控制设置”下，单击缓存检查点。

**重置缓存内容**

您可以随时清除缓存的内容。 缓存重置后，每个表单的第一个请求速度会变慢，因为Forms服务会执行完整的渲染并创建新缓存内容。

1. 在管理控制台中，单击服务> Forms。
1. 在“Forms缓存控制设置”下，单击重置缓存。

## 配置缓存设置 {#configuring-cache-settings}

您可以指定Forms用于缓存的设置，这会优化AEM表单环境的性能。

要访问这些设置，请在管理控制台中单击服务> Forms。

>[!NOTE]
>
>缓存的磁盘要求应与存储库相等。

### 指定全局缓存设置 {#specifying-global-cache-settings}

中的设置 **全局缓存设置** 区域将影响所有类型的缓存。 如果更改其中任一设置，请重新启动Forms服务以使更改生效。 要重新启动此服务，请使用Workbench或参阅 [启动或停止与AEM表单模块关联的服务](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 以获取说明。

**最大缓存文档大小(KB)：** 可存储在任何内存缓存中的表单设计或其他资源的最大大小（以KB为单位）。 这是适用于所有内存缓存的全局设置。 如果资源大于此值，则不会将其缓存在内存中。 默认值为1024 KB。 此设置不会影响磁盘缓存。

**表单渲染缓存已启用：** 默认情况下，此选项处于选中状态，这意味着将缓存渲染的表单以供后续检索。 此设置可提高性能，因为Forms服务只需呈现特定表单一次，然后它使用缓存的版本。 此选项适用于表单设计的缓存属性。 有关在窗体设计中配置此值的信息，请参阅设计器帮助。

### 缓存表单设计 {#caching-form-designs}

当Forms服务收到渲染请求时，它会从存储库检索表单设计并将其缓存。 此缓存可提高性能，因为对于后续渲染请求，Forms服务会从缓存而不是存储库检索表单设计。

Forms服务始终在磁盘上缓存表单设计。 如果表单设计存储在服务器上，则这些文件被视为磁盘缓存。 Forms服务还会根据中的设置，在内存中缓存表单设计 **内存中模板缓存** 区域。 如果更改其中任何设置，请重新启动Forms服务以使更改生效。 要重新启动此服务，请使用Workbench或参阅 [启动或停止与AEM表单模块关联的服务](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 以获取说明。

**模板配置缓存大小：** 要保留在内存中的模板配置对象的最大数目。 默认值为 100。建议将此值设置为大于或等于模板缓存大小值。 此设置不会影响磁盘缓存。

**模板缓存大小：** 要保留在内存中的模板内容对象的最大数量。 默认值为 100。此设置不会影响磁盘缓存。

**已启用：** 默认情况下，此复选框处于选中状态，这意味着表单模板会缓存在内存中。 如果未选择此选项，则仅在磁盘上缓存表单模板。

### 缓存渲染的表单 {#caching-rendered-forms}

Forms服务缓存渲染的表单，以便它不需要在后续请求中解析和渲染相同的表单。 呈现的表单缓存在磁盘和内存中。

这些设置位于 **内存中表单渲染缓存** 区域。 如果更改其中任一设置，请重新启动Forms服务以使更改生效。 要重新启动此服务，请使用Workbench或参阅 [启动或停止与AEM表单模块关联的服务](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 以获取说明。

**高速缓存大小：** 指定可驻留在内存缓存中的渲染表单的最大数目。 默认值为 100。此设置不会影响磁盘缓存。

**已启用：** 默认情况下，此选项处于选中状态，这意味着呈现的表单会缓存在内存中。 如果未选择此选项，则呈现的表单将仅缓存在磁盘上。

### 缓存片段和图像 {#caching-fragments-and-images}

Forms服务在磁盘上缓存表单设计中使用的片段和图像。 这可以提高性能，因为仅在第一次请求时才会从存储库中读取片段和图像。 然后，在后续请求中，Forms服务会从磁盘缓存中读取片段和图像。 片段和图像仅缓存在磁盘上，不在内存中。

您可以使用以下设置来控制片段和映像的磁盘上缓存。 这些设置位于 **模板资源缓存设置** 区域：

**资源缓存** 从列表中选择以下选项之一：

**为片段和图像启用：** Forms服务缓存片段和图像。 这是默认选项。

**为片段启用：** Forms服务缓存片段，但不缓存图像。

**已禁用：** Forms服务不缓存片段或图像。

**清理间隔（秒）：** 指定Forms服务删除旧的无效缓存文件的频率。 Forms服务未删除有效的缓存文件。 如果更改清理间隔，请重新启动Forms服务以使更改生效。 要重新启动此服务，请使用Workbench或参阅启动或停止与AEM表单模块关联的服务以获取说明。 默认值为600秒。

## 缓存的群集注意事项 {#clustering-considerations-for-caches}

在群集环境中，每个节点都维护自己的内存和磁盘缓存。 每个节点上的缓存内容取决于该节点上已渲染的表单。

在群集的每个节点上，缓存的位置必须相同（相同的磁盘和路径）。 不要将缓存放在共享存储上。

如果您使用管理控制台中的“Forms”页面更改特定节点的缓存设置，则当有请求进入其他节点时，该节点上的缓存设置也会更新。 此行为也适用于“重置缓存”按钮。 如果单击某个节点的“重置高速缓存”按钮，将立即从该节点中删除高速缓存。 当请求到达其他节点时，将清除该节点上的缓存。
