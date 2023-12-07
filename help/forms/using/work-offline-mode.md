---
title: 在脱机模式下工作
description: 在AEM Forms网络范围之外或以完全脱机模式使移动设备脱机，然后使用AEM Forms应用程序
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: ba4ceef1-510d-41ef-94b8-4834fb7de804
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# 在脱机模式下工作 {#working-in-the-offline-mode}

利用AEM Forms应用程序的离线模式，您可以无缝地工作，即使应用程序离线也是如此。 您可以打开、更新和提交表单，而无需任何网络连接。

您可通过将应用程序与AEM Forms服务器同步来开始使用AEM Forms应用程序。 分配给您的所有表单都将在您的应用程序中下载。 对于JEE上的AEM Forms，任务在“任务”选项卡中获取，起点相关表单和其他表单在“Forms”选项卡中获取。 对于OSGi上的AEM Forms，Forms选项卡中只加载Forms。

有关如何同步应用程序的详细信息，请参阅 [同步应用程序](/help/forms/using/sync-app.md).

## 使Forms可离线使用 {#making-forms-available-offline}

将应用程序与AEM Forms服务器同步时，表单将下载到您的移动设备。 但是，默认情况下，不会下载与表单关联的附件。 这意味着如果您处于联机状态，则可以查看附件。 但是，要确保您可以在脱机模式下查看附件，请更改应用程序中的默认设置。

要确保关联的附件随每个表单一起下载，请将“提取附件”设置为“启用”。 有关详细信息，请参阅 [更新常规设置](/help/forms/using/update-general-settings.md).

由于在移动设备上下载数据可能会影响设备的性能，因此默认情况下，“获取附件”设置设置为“关”。 当设置更新为“开”后，从服务器下载的任何任务都将附件提取到设备。 在脱机模式下，用户可以在设置之后处理下载到设备的所有任务 **获取附件** 选项更改为ON。

## 为AEM Forms应用程序配置离线服务 {#configuring-offline-service-for-aem-forms-app-br}

AEM Forms app离线服务标识表单中使用的资源。 AEM Forms应用程序依赖此服务获取有关表单依赖项的信息。 需要有关表单依赖项的信息才能启用离线功能。 AEM Forms App离线服务可缓存表单中使用的资源的路径或URL。 缓存会根据表单中的更改以及为离线服务配置的有效期进行更新。 缓存表单中使用的资源的路径或URL可提高服务器端性能。

要配置AEM Forms应用程序的服务器端离线组件，请执行以下操作：

1. 在创作实例中，导航到 **Adobe Experience Manager** >**工具** > **Forms** > **配置Forms App离线服务**.

   URL： `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. 在“常规设置”下，可以执行以下操作：

   * **清除缓存**：清除表单依赖项的服务器端缓存。
   * **重置配置**：重置AEM Forms应用程序离线配置。
   * **缓存有效性**：指定服务器端离线缓存的有效期。
   * **资源观察路径**：指定脱机服务用于监视资源更改的路径。 如果在指定的路径中发生任何更改，则会更新所有依赖表单的离线缓存。 例如：`/etc/clientlibs/fd,/content/dam/images`。

1. 在 **手动资源缓存** 选项卡，指定表单依赖关系脱机服务无法识别的情况。 您可以指定资源，例如从JavaScript中加载的图像。 AEM Forms应用程序也将以离线模式下载这些资源。
