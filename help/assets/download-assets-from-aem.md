---
title: 从[!DNL Adobe Experience Manager]下载数字资产。
description: 了解如何从[!DNL Adobe Experience Manager]下载资产并启用或禁用下载功能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# Download assets from [!DNL Adobe Experience Manager] {#download-assets-from-aem}

您可以下载包括静态和动态演绎版在内的资产。 或者，您也可以发送电子邮件，其中直接包含指向资产的链 [!DNL Adobe Experience Manager Assets]接。 下载的资产会打包在 ZIP 文件中。对于导出作业，压缩的 ZIP 文件大小最大为 1 GB。每个导出作业最多允许处理的资产总数为 500 个。

>[!NOTE]
>
>收件人的电子邮件必须是用户组的成 `dam-users` 员才能访问电子邮件中的ZIP下载链接。 要能够下载资产，成员必须具有启动触发资产下载的工作流的权限。

要下载资产，请导航到资产，选择资产，然后点按工具 **[!UICONTROL 栏中]** 的下载。 在显示的对话框中，指定下载选项。

无法下载图像集、旋转集、混合媒体集和传送集等资产类型。

![从Experience Manager资产下载资产时可用的选项](assets/asset_download_dialog.png)

*图：从下载资产时可用的选[!DNL Experience Manager Assets]项。*

以下是“导出／下载”选项。 动态演绎版是Dynamic Media特有的，它允许您在动态生成演绎版的同时选择资产——只有在启用了Dynamic Media的情况下，此选项才可用。

| 导出或下载选项 | 描述 |
|---|---|
| [!UICONTROL 资产] | 选择此选项可以下载资产的原始形式，而无需任何演绎版。 |
| [!UICONTROL 演绎版] | 演绎版是资产的二进制表示形式。资产具有主要表示形式——已上传文件的表示形式。 他们可以有任意数量的表示形式。 <br> 通过此选项，您可以选择要下载的演绎版。 可用的演绎版取决于您选择的资产。 |
| [!UICONTROL 动态演绎版] | 动态演绎版可动态生成其他演绎版。When you select this option, you also select the renditions you want to create dynamically by selecting from the [Image Preset](image-presets.md) list. <br>此外，您还可以选择大小和度量单位、格式、色彩空间、分辨率以及任何图像修饰符（例如反转图像） |
| [!UICONTROL 电子邮件] | 将向用户发送电子邮件通知。 标准电子邮件模板位于以下位置：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> 在部署过程中自定义的模板应位于以下位置： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul>您可以在以下位置存储特定于租户的自定义模板：<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> |
| [!UICONTROL 为每个资产创建单独的文件夹] | 选择此选项可在下载资产时保留文件夹层次结构。 默认情况下，文件夹层次结构将被忽略，所有资产都下载在本地系统的一个文件夹中。 |

如果资产有任何演绎版，则选项演绎版选项可用。 如果资产包含子资产，则子资产选项可用。

当您选择要下载的文件夹时，将下载该文件夹下的完整资产层次结构。 要将您下载的每个资产（包括嵌套在父文件夹下的子文件夹中的资产）包含在单个文件夹中，请为每个资 **[!UICONTROL 产选择创建单独的文件夹]**。

## 启用资产下载servlet {#enable-asset-download-servlet}

中的默认servlet允 [!DNL Experience Manager] 许经过身份验证的用户发出任意大的并发下载请求，以创建对他们可见的资产的ZIP文件，这些文件可能会使服务器和网络过载。 为了减轻由此功能引起的潜在DoS风险， `AssetDownloadServlet` OSGi组件在默认情况下对发布实例处于禁用状态。

要允许从您的DAM下载资产，例如，在使用类似于Asset Share Commons或其他类似门户的实施时，请通过OSGi配置手动启用servlet。 Adobe建议尽可能低地设置允许的下载大小，而不影响日常下载要求。 高价值可能会影响性能。

1. 创建一个具有命名约定的文件夹，该命名约定目标发布运行模式，即 `config.publish`:

   `/apps/<your-app-name>/config.publish`

   要为运行模式定义配置属性，请参阅 [运行模式](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode) ，了解详细信息。

1. 在config文件夹中，创建一个名为的新文 `nt:file` 件类型 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`。
1. 填充 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` 以下内容。 将下载的最大大小（以字节为单位）设置为 `asset.download.prezip.maxcontentsize`。 以下示例将ZIP下载的最大大小配置为不超过100 kB。

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## 禁用资产下载servlet {#disable-asset-download-servlet}

通过 `Asset Download Servlet` 更新调度程序配置以阻止任何资 [!DNL Experience Manager] 产下载请求，可以在Publish实例上禁用该功能。 也可以直接通过OSGi控制台手动禁用Servlet。

1. 要通过调度程序配置阻止资产下载请求，请编辑 `dispatcher.any` 配置，并向过滤器部分添加新 [规则](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)。

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. 通过导航到位于的OSGi控制台，可以手动禁用Publish实例上的OSGi组件 `<aem-host>/system/console/components`。 找到并 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` 单击“ **[!UICONTROL 禁用]**”。

>[!MORELIKETHIS]
>
>* [下载受DRM保护的资源](drm.md)
>* [在Win或Mac桌面上使用Experience Manager桌面应用程序下载资源](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [从支持的Adobe Creative Cloud应用程序中使用Adobe Assets Link下载资源](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html)

