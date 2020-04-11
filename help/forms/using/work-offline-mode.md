---
title: 在脱机模式下工作
seo-title: 在脱机模式下工作
description: 将您的移动设备脱机到AEM Forms网络范围之外或完全脱机模式，然后使用AEM Forms应用程序
seo-description: 将您的移动设备脱机到AEM Forms网络范围之外或完全脱机模式，然后使用AEM Forms应用程序
uuid: b900a0f8-90ce-486a-bde6-6cdf11bd2801
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9a3c6ab4-8bb9-40c7-8c56-59153b364887
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 在脱机模式下工作 {#working-in-the-offline-mode}

AEM Forms应用程序的脱机模式使您能够无缝地工作，即使应用程序脱机也是如此。 您可以打开、更新和提交表单，无需任何网络连接。

您可以通过将应用程序与AEM Forms服务器同步来开始在AEM Forms应用程序上工作。 分配给您的所有表单都将下载到您的应用程序中。 对于JEE上的AEM表单，将在“任务”选项卡中获取任务，并在“表单”选项卡中提取关联表单和其他表单的起点。 对于OSGi上的AEM Forms,“表单”选项卡中仅加载表单。

有关如何同步应用程序的详细信息，请参阅同 [步应用程序](/help/forms/using/sync-app.md)。

## 使表单脱机可用 {#making-forms-available-offline}

当您将应用程序与AEM Forms服务器同步时，表单将下载到您的移动设备。 但是，默认情况下，不会下载与表单关联的附件。 这意味着，如果您在线，则可以视图附件。 但是，要确保您可以在脱机模式下视图附件，请更改应用程序中的默认设置。

要确保关联的附件随每个表单一起下载，请将“提取附件”设置为“打开”。 有关详细信息，请参 [阅更新常规设置](/help/forms/using/update-general-settings.md)。

由于在移动设备上下载数据可能会影响设备的性能，因此默认情况下，“提取附件”设置设置为“关闭”。 在将设置更新为ON后，将附件从服务器下载到设备的任何任务。 在脱机模式下，用户随后可以处理将“提取附件”选项设置为“打开”后下载到设 **备的所有任务** 。

## 为AEM Forms应用程序配置脱机服务 {#configuring-offline-service-for-aem-forms-app-br}

AEM Forms应用程序脱机服务标识表单中使用的资源。 AEM Forms应用程序依赖此服务获取有关表单依赖关系的信息。 要启用脱机功能，需要有关表单依赖关系的信息。 AEM Forms应用程序脱机服务会缓存表单中使用的资源的路径或URL。 根据表单中的更改和为脱机服务配置的有效期更新缓存。 缓存表单中使用的资源路径或URL可提高服务器端性能。

要配置AEM Forms应用程序的服务器端脱机组件，请执行以下操作：

1. 在创作实例中，导航到 **Adobe Experience Manager** >**Tools >** Forms **>****** Configure Forms App Offline Service。

   URL: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. 在“常规设置”下，您可以执行以下操作：

   * **清除缓存**:清除表单依赖关系的服务器端缓存。
   * **重置配置**:重置AEM Forms应用程序脱机配置。
   * **缓存有效性**:指定服务器端脱机缓存的有效期。
   * **资源观察路径**:指定脱机服务监视资源更改的路径。 如果指定路径中发生任何更改，则所有从属表单的脱机缓存都会更新。 For example, `/etc/clientlibs/fd,/content/dam/images`.

1. 在“手动 **资源缓存”选项卡中** ，指定表单依赖关系脱机服务无法识别。 可以指定资源，如从JavaScript中加载的图像。 AEM Forms应用程序将下载这些资源以用于脱机模式。
