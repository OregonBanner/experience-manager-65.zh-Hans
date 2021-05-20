---
title: 在脱机模式下工作
seo-title: 在脱机模式下工作
description: 将移动设备脱机到AEM Forms网络范围外或完全脱机模式，然后在AEM Forms应用程序上工作
seo-description: 将移动设备脱机到AEM Forms网络范围外或完全脱机模式，然后在AEM Forms应用程序上工作
uuid: b900a0f8-90ce-486a-bde6-6cdf11bd2801
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9a3c6ab4-8bb9-40c7-8c56-59153b364887
exl-id: ba4ceef1-510d-41ef-94b8-4834fb7de804
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# 在脱机模式下工作{#working-in-the-offline-mode}

通过AEM Forms应用程序的离线模式，即使应用程序离线，您也可以无缝地工作。 您可以打开、更新和提交表单，而无需任何网络连接。

您可以通过将应用程序与AEM Forms服务器同步来开始使用AEM Forms应用程序。 分配给您的所有表单都将在您的应用程序中下载。 对于JEE上的AEM Forms，任务选项卡中会获取任务，并且Forms选项卡中会提供与表单和其他表单关联的起点。 对于OSGi上的AEM Forms，“Forms”选项卡中只加载Forms。

有关如何同步应用程序的详细信息，请参阅[同步应用程序](/help/forms/using/sync-app.md)。

## 使Forms脱机可用{#making-forms-available-offline}

将应用程序与AEM Forms服务器同步后，这些表单会下载到您的移动设备。 但是，默认情况下，不会下载与表单关联的附件。 这意味着，如果您处于联机状态，则可以查看附件。 但是，为确保您能够在脱机模式下查看附件，请更改应用程序中的默认设置。

要确保随每个表单一起下载关联的附件，请将“获取附件”设置为“开”。 有关详细信息，请参阅[更新常规设置](/help/forms/using/update-general-settings.md)。

由于从移动设备上下载数据可能会影响设备的性能，因此默认情况下，“获取附件”设置将设置为“关闭”。 将设置更新为ON后，将从服务器下载的任何任务的附件都会被提取到设备。 在脱机模式下，用户可以在将&#x200B;**获取附件**&#x200B;选项设置为ON后，处理下载到设备的所有任务。

## 为AEM Forms应用程序{#configuring-offline-service-for-aem-forms-app-br}配置离线服务

AEM Forms应用程序离线服务可标识表单中使用的资源。 AEM Forms应用程序依赖此服务来获取有关表单依赖关系的信息。 要启用离线功能，需要提供有关表单依赖项的信息。 AEM Forms应用程序离线服务会缓存表单中所用资源的路径或URL。 缓存会根据表单中的更改以及为离线服务配置的有效期来更新。 缓存表单中使用的路径或资源的URL可提高服务器端性能。

要配置AEM Forms应用程序的服务器端离线组件，请执行以下操作：

1. 在创作实例中，导航到&#x200B;**Adobe Experience Manager** >**工具** > **Forms** > **配置Forms应用程序离线服务**。

   URL: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. 在“常规设置”下，您可以执行以下操作：

   * **清除缓存**:清除表单依赖项的服务器端缓存。
   * **重置配置**:重置AEM Forms应用程序离线配置。
   * **缓存有效性**:指定服务器端离线缓存的有效期。
   * **资源观察路径**:指定离线服务监视资源更改的路径。如果指定路径中发生任何更改，则所有从属表单的脱机缓存会更新。 例如，`/etc/clientlibs/fd,/content/dam/images`。

1. 在&#x200B;**手动资源缓存**&#x200B;选项卡中，指定脱机服务无法识别的表单依赖项。 您可以指定资源，如从JavaScript中加载的图像。 AEM Forms应用程序将下载这些资源以及脱机模式下的资源。
