---
title: 为Forms配置缓存
seo-title: 为Forms配置缓存
description: 了解如何配置缓存设置以及如何对缓存进行群集注意事项。
seo-description: 了解如何配置缓存设置以及如何对缓存进行群集注意事项。
uuid: 70f36191-4163-410b-991a-e1481488aea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8a07dddf-1281-45ac-a55e-4333b860a261
exl-id: 6b57d00e-5ba0-41ee-8497-49ecfec5b9ed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 0%

---

# 为Forms配置缓存{#configuring-caching-for-forms}

Forms服务采用在Designer中创建的表单设计，并以各种格式呈现它们。

管理控制台中的Forms页面包含一些设置，这些设置可控制Forms服务缓存项目的方式。 您可以调整这些设置以优化Forms服务的性能。

Forms服务缓存以下项：

* **表单设计：** Forms服务会缓存从存储库或HTTP源中检索的表单设计。此缓存可提高性能，因为对于后续渲染请求，Forms服务会从缓存中检索表单设计，而不是从存储库中检索。
* **片段和图像：** Forms服务可以缓存表单设计中使用的片段和图像。当Forms服务缓存这些对象时，它会提高性能，因为片段和图像仅在第一次请求时从存储库中读取。
* **表单：** Forms服务会缓存它呈现的表单。此类型的缓存会提高性能，因为Forms服务不需要在后续请求中解析和渲染相同的表单。

Forms将缓存存储在以下两个位置：

* **内存中：** 项目存储在内存中以便快速访问。内存中的缓存大小有限，在重新启动服务器时将被删除。
* **在磁盘上：** 项目存储在服务器的文件系统中。磁盘缓存的容量大于内存中的缓存，并且在重新启动服务器时保留该缓存。 磁盘缓存的位置取决于您的应用程序服务器。 有关更改磁盘缓存位置的信息，请参阅[配置Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)的位置。

## 指定缓存模式{#specifying-the-cache-mode}

Forms支持两种缓存模式：

* 无条件
* 使用缓存检查点

如果在缓存模式之间切换，请重新启动Forms服务以使更改生效。 要重新启动此服务，请使用Workbench或参阅[启动或停止与AEM表单模块关联的服务](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules)以获取相关说明。

在模式之间切换时，缓存检查点时间会自动重置。

### 使用无条件缓存{#using-unconditional-caching}

在此模式下，当Forms服务收到请求时，将验证所需的资源（表单设计以及任何相关资产，如片段和图像）。 Forms服务将存储库中资源的时间戳与缓存中资源的时间戳进行比较。 如果缓存中的资源较旧，Forms服务会更新该资源。

此缓存模式可确保使用最新的资源。 但是，性能会受到影响，因为Forms服务会通过每个请求来验证针对存储库的缓存项目。 此缓存模式适用于资源经常更新且性能不是主要问题的开发和暂存环境。

**指定无条件缓存**

1. 在管理控制台中，单击服务> Forms。
1. 在“Forms缓存控制设置”下，选择“无条件”并单击“保存”。

### 使用缓存检查点{#use-the-cache-check-point}

在此模式下，当缓存资源的时间戳早于缓存检查点时间时，Forms服务仅会检查存储库是否有较新版本的资源。 最后一个缓存检查点时间显示在管理控制台的Forms页面上。

在高性能生产环境中使用此缓存模式，因为在高性能生产环境中，性能是一个问题，并且资源的更改很少。 当要部署对存储库资源所做的任何更改时，可以重置缓存检查点时间。

**指定缓存检查点的使用**

1. 在管理控制台中，单击服务> Forms。
1. 在“Forms缓存控制设置”下，仅当其上次验证在缓存检查点时间之前完成时，才选择，然后单击保存。

**重置缓存检查点**

1. 在管理控制台中，单击服务> Forms。
1. 在“Forms缓存控制设置”下，单击缓存检查点。

**重置缓存内容**

您可以随时清除缓存的内容。 重置缓存后，每个表单的第一个请求速度会减慢，因为Forms服务会执行完整渲染并创建新的缓存内容。

1. 在管理控制台中，单击服务> Forms。
1. 在“Forms缓存控制设置”下，单击重置缓存。

## 配置缓存设置{#configuring-cache-settings}

您可以指定Forms用于缓存的设置，以优化AEM表单环境的性能。

要访问这些设置，请在管理控制台中，单击服务> Forms。

>[!NOTE]
>
>缓存的磁盘要求应等于存储库。

### 指定全局缓存设置{#specifying-global-cache-settings}

**全局缓存设置**&#x200B;区域中的设置会影响所有类型的缓存。 如果您更改其中任一设置，请重新启动Forms服务，以使更改生效。 要重新启动此服务，请使用Workbench或参阅[启动或停止与AEM表单模块关联的服务](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules)以获取相关说明。

**最大缓存文档大小(KB):** 表单设计或其他资源可存储在任何内存中缓存中的最大大小（以千字节为单位）。这是适用于所有内存中缓存的全局设置。 如果资源大于此值，则不会将其缓存在内存中。 默认值为1024千字节。 此设置不影响磁盘缓存。

**表单渲染缓存已启用：** 默认情况下，选中此选项，这意味着已渲染的表单会缓存以供后续检索。此设置可提高性能，因为Forms服务只需渲染特定表单一次，然后便使用缓存版本。 此选项适用于表单设计的缓存属性。 有关在表单设计中配置此值的信息，请参阅设计器帮助。

### 缓存表单设计{#caching-form-designs}

当Forms服务收到渲染请求时，它会从存储库中检索表单设计并缓存它。 此缓存可提高性能，因为对于后续渲染请求，Forms服务会从缓存中检索表单设计，而不是从存储库中检索。

Forms服务始终在磁盘上缓存表单设计。 如果表单设计存储在服务器上，则这些文件将被视为磁盘缓存。 Forms服务还根据&#x200B;**In Memory Template Cache**&#x200B;区域中的设置，在内存中缓存表单设计。 如果您更改了其中的任何设置，请重新启动Forms服务，以使更改生效。 要重新启动此服务，请使用Workbench或参阅[启动或停止与AEM表单模块关联的服务](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules)以获取相关说明。

**模板配置缓存大小：** 要保留在内存中的模板配置对象的最大数量。默认值为 100。建议您将此值设置为大于或等于“模板缓存大小”值。 此设置不影响磁盘缓存。

**模板缓存大小：** 要保留在内存中的模板内容对象的最大数量。默认值为 100。此设置不影响磁盘缓存。

**启用：** 默认情况下，此复选框处于选中状态，这意味着表单模板已缓存在内存中。如果未选择此选项，则表单模板仅缓存在磁盘上。

### 缓存已呈现的表单{#caching-rendered-forms}

Forms服务会缓存已渲染的表单，以便它无需在后续请求中解析和渲染相同的表单。 呈现的表单会同时缓存在磁盘和内存中。

这些设置位于&#x200B;**In Memory Form Rendering Cache**&#x200B;区域。 如果您更改其中任一设置，请重新启动Forms服务，以使更改生效。 要重新启动此服务，请使用Workbench或参阅[启动或停止与AEM表单模块关联的服务](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules)以获取相关说明。

**缓存大小：** 指定内存中缓存的可呈现表单的最大数量。默认值为 100。此设置不影响磁盘缓存。

**启用：** 默认情况下，此选项处于选中状态，这意味着已渲染的表单会缓存在内存中。如果未选择此选项，则仅在磁盘上缓存呈现的表单。

### 缓存片段和图像{#caching-fragments-and-images}

Forms服务在磁盘上缓存表单设计中使用的片段和图像。 这会提高性能，因为片段和图像仅在第一次请求时从存储库中读取。 然后，在后续请求中，Forms服务会从磁盘缓存中读取片段和图像。 片段和图像仅缓存在磁盘上，而不在内存中。

您可以使用以下设置控制片段和图像的磁盘缓存。 这些设置位于&#x200B;**模板资源缓存设置**&#x200B;区域：

**资源** 缓存从列表中选择以下选项之一：

**为片段和图像启用：** Forms服务可缓存片段和图像。这是默认选项。

**为片段启用：** Forms服务会缓存片段，但不会缓存图像。

**禁用：** Forms服务不缓存片段或图像。

**清理间隔（秒）：** 指定Forms服务删除旧无效缓存文件的频率。Forms服务不会删除有效的缓存文件。 如果更改清理间隔，请重新启动Forms服务，以使更改生效。 要重新启动此服务，请使用Workbench或参阅启动或停止与AEM表单模块关联的服务，以获取相关说明。 默认值为600秒。

## 缓存{#clustering-considerations-for-caches}的群集注意事项

在群集环境中，每个节点都维护其自己的内存和磁盘缓存。 每个节点上的缓存内容取决于该节点上已呈现的表单。

缓存在群集每个节点上的位置必须相同（磁盘和路径相同）。 请勿将缓存置于共享存储上。

如果使用管理控制台中的Forms页面更改特定节点的缓存设置，则当请求转到该节点时，其他节点上的缓存设置将会更新。 此行为也适用于重置缓存按钮。 如果单击某个节点的“重置缓存”按钮，则会立即从该节点中删除缓存。 当请求转到该节点时，将清除其他节点上的缓存。
