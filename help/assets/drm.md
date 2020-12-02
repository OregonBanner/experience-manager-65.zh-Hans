---
title: 资产Digital Rights Management
description: 了解如何在 [!DNL Experience Manager]中管理授权资产的到期状态和信息。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 97d3edf155ddeabf3f39139c9079621c3627820b
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 5%

---


# 资产Digital Rights Management{#digital-rights-management-in-assets}

数字资产通常与指定使用条款和持续时间的许可证相关联。 由于[!DNL Adobe Experience Manager Assets]与[!DNL Experience Manager]平台完全集成，因此您可以有效管理资产到期信息和资产状态。 您还可以将许可信息与资产关联。

## 资产过期 {#asset-expiration}

资产到期是实施资产许可要求的有效方式。 它可确保发布的资产在过期后取消发布，这样不会发生任何违反许可的情况。 没有管理员权限的用户无法编辑、复制、移动、发布和下载过期的资产。

您可以在卡和列表视图卡的[!DNL Assets]控制台中视图资产的过期状态。

![expired_flag_列表](assets/expired_flag_list.png)

*图：在列表视图中，“状  态”列显示“  过期”横幅。*

您可以在左边栏的[!UICONTROL 时间轴]中视图资产的过期状态。

![chlimage_1-144](assets/chlimage_1-144.png)

>[!NOTE]
>
>资产的到期日期对不同时区的用户显示不同。

您还可以在&#x200B;**[!UICONTROL 引用]**&#x200B;边栏中视图资产的过期状态。 它管理资产到期状态以及复合资产与引用的子资产、集合和项目之间的关系。

1. 导航到要视图其引用网页和复合资产的资产。
1. 选择资产并打开左边栏中的&#x200B;**[!UICONTROL 引用]**。 对于过期的资产，[!UICONTROL 引用]边栏会在顶部显示到期状态&#x200B;**[!UICONTROL 资产已过期]**。

   ![chlimage_1-147](assets/chlimage_1-147.png)

   如果资产已过期子资产，[!UICONTROL 引用]边栏会显示状态&#x200B;**[!UICONTROL 资产已过期子资产]**。

   ![chlimage_1-148](assets/chlimage_1-148.png)

### 搜索过期的资产{#search-expired-assets}

您可以在“搜索”面板中搜索过期的资产，包括过期的子资产。

1. 在[!DNL Assets]控制台中，单击工具栏中的&#x200B;**[!UICONTROL 搜索]**&#x200B;以显示“搜索”框。

1. 将光标置于“全搜索”框中，按Enter键显示搜索结果页面。
1. 打开左边栏中的搜索面板。 单击&#x200B;**[!UICONTROL Expiry Status]**&#x200B;选项以展开它。

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. 选择&#x200B;**[!UICONTROL 过期]**。 筛选搜索结果后，只会显示过期的资产。

当您选择&#x200B;**[!UICONTROL 已过期]**&#x200B;选项时，[!DNL Assets]控制台将仅显示复合资产引用的已过期资产和子资产。 在子资产过期后，不会立即显示引用已过期子资产的复合资产。 相反，在[!DNL Experience Manager]检测到下次运行调度程序时引用过期的子资产后，会显示这些子资产。

如果您将已发布资产的过期日期修改为早于当前调度程序周期的日期，计划仍会在下次运行时将此资产检测为过期资产，并相应地反映其状态。

此外，如果故障或错误导致调度程序无法在当前周期中检测过期的资产，调度程序会在下一个周期重新检查这些资产并检测其过期状态。

要使[!DNL Assets]控制台能够显示引用复合资产以及已过期的子资产，请在[!DNL Experience Manager]配置管理器中配置&#x200B;**[!UICONTROL Adobe CQDAM到期通知]**&#x200B;工作流。

1. 打开[!DNL Experience Manager] Configuration Manager。
1. 选择&#x200B;**[!UICONTROL Adobe CQDAM到期通知]**。 默认情况下，会选择&#x200B;**[!UICONTROL 基于时间的调度程序]**，这将计划作业以在特定时间检查资产是否已过期子资产。 作业完成后，已过期的子资产和引用的资产会在搜索结果中显示为过期。

1. 要定期运行该作业，请清除&#x200B;**[!UICONTROL 基于时间的计划程序规则]**&#x200B;字段，并在&#x200B;**[!UICONTROL 周期性计划程序]**&#x200B;字段中修改时间（以秒为单位）。例如，示例表达式`0 0 0 &ast; &ast; ?`在00小时触发作业。
1. 选择&#x200B;**[!UICONTROL 发送电子邮件]**&#x200B;以在资产过期时接收电子邮件。

   >[!NOTE]
   >
   >只有资产创建者（将特定资产上传到[!DNL Assets]的人员）在资产过期时才会收到电子邮件。 有关在整个[!DNL Experience Manager]级别配置电子邮件通知的更多详细信息，请参阅[如何配置电子邮件通知](/help/sites-administering/notification.md)。

1. 在&#x200B;**[!UICONTROL 以秒为单位的先前通知]**&#x200B;字段中，指定资产在您希望收到有关过期的通知时在到期前的秒数。 资产创建者在资产到期前会收到一条消息，通知您资产将在指定时间后过期。 资产到期后，您会收到另一则通知，确认到期。 此外，过期的资产也会停用。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 资产状态{#asset-states}

[!DNL Assets]控制台可显示资产的各种状态。 根据特定资产的当前状态，其卡片视图会显示一个标签，用于描述其状态，例如“已过期”、“已发布”、“已批准”、“被拒绝”等。

1. 在[!DNL Assets]用户界面中，选择一个资产。
1. 单击工具栏中的&#x200B;**[!UICONTROL 发布]**。 如果工具栏上未显示&#x200B;**发布**，请单击工具栏上的&#x200B;**[!UICONTROL 更多]**，然后找到&#x200B;**[!UICONTROL 发布]** ![发布选项](assets/do-not-localize/publish-globe.png)选项。
1. 从菜单中选择&#x200B;**[!UICONTROL 发布]**，然后关闭确认对话框。
1. 退出选择模式。 资产的发布状态会显示在卡片视图中资产缩略图的底部。 在列表视图中，已发布列显示资产发布的时间。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 要显示其资产详细信息页面，请在[!DNL Assets]界面中选择资产，然后单击&#x200B;**[!UICONTROL 属性]** ![视图属性](assets/do-not-localize/info-circle-icon.png)。

1. 在[!UICONTROL 高级]选项卡中，从&#x200B;**[!UICONTROL 过期]**&#x200B;字段设置资产的过期日期。

   ![在“过期”字段中设置资产过期日期和时间](assets/asset-properties-advanced-tab.png)

   *图： [!UICONTROL “资] 产属性”页中的“  高级”选项卡，以设置资产过期时间。*

1. 单击&#x200B;**[!UICONTROL 保存]**，然后单击&#x200B;**[!UICONTROL 关闭]**&#x200B;以显示资产控制台。
1. 资产的发布状态会在卡片视图中资产缩略图的底部指示过期状态。 在列表视图中，资产的状态显示为&#x200B;**[!UICONTROL 已过期]**。

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. 在[!DNL Assets]控制台中，选择一个文件夹，然后在该文件夹上创建一个审核任务。
1. 在审核任务中审核和批准／拒绝资产，然后单击&#x200B;**[!UICONTROL 完成]**。
1. 导航到创建审核任务的文件夹。 您批准／拒绝的资产的状态显示在卡视图的底部。 在列表视图中，批准和到期状态显示在相应的列中。

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. 要根据资产的状态搜索资产，请单击&#x200B;**[!UICONTROL 搜索]** ![搜索选项](assets/do-not-localize/search_icon.png)以显示Omnisearch栏。
1. 按返回并单击[!DNL Experience Manager]以显示搜索面板。
1. 在搜索面板中，单击&#x200B;**[!UICONTROL 发布状态]**&#x200B;并选择&#x200B;**[!UICONTROL 已发布]**&#x200B;以在[!DNL Assets]中搜索已发布的资产。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 单击&#x200B;**[!UICONTROL 批准状态]**&#x200B;并单击相应选项以搜索已批准或已拒绝的资产。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 要根据资产的到期状态搜索资产，请在“搜索”面板中选择&#x200B;**[!UICONTROL 到期状态]**，然后选择相应的选项。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 您还可以根据各种搜索彩块化下的状态组合来搜索资产。 例如，您可以通过在搜索彩块化中选择相应的选项，来搜索在审核任务中已批准但尚未过期的已发布资产。

   ![chlimage_1-166](assets/chlimage_1-166.png)

## [!DNL Assets]{#digital-rights-management-in-assets-1}中的Digital Rights Management

此功能强制您接受许可协议，然后您才能从[!DNL Adobe Experience Manager Assets]下载许可资产。

如果您选择受保护的资产并单击&#x200B;**[!UICONTROL 下载]**，则会将您重定向到许可页面以接受该许可协议。 如果您不接受许可协议，则&#x200B;**[!UICONTROL 下载]**&#x200B;选项不可用。

如果选择的内容包含多个受保护的资产，则一次选择一个资产，接受许可协议，然后继续下载该资产。

如果满足以下任一条件，资产将被视为受保护：

* 资产元数据属性`xmpRights:WebStatement`指向包含资产许可协议的页面路径。
* 资产元数据属性`adobe_dam:restrictions`的值是一个原始HTML，用于指定许可协议。

>[!NOTE]
>
>[!DNL Experience Manager]早期版本中用于存储许可证的位置`/etc/dam/drm/licenses`已弃用。
>
>如果您创建或修改许可证页面，或移植前一个[!DNL Experience Manager]版本的许可证页面，Adobe建议将它们存储在`/apps/settings/dam/drm/licenses`或`/conf/&ast;/settings/dam/drm/licenses`下。

### 下载受DRM保护的资源{#downloading-drm-assets}

1. 在卡视图中，选择要下载的资产，然后单击&#x200B;**[!UICONTROL 下载]**。
1. 在&#x200B;**[!UICONTROL 版权管理]**&#x200B;页面，从列表中选择要下载的资产。
1. 在[!UICONTROL 许可证]窗格中，选择&#x200B;**[!UICONTROL 同意]**。 资产旁边会显示一个勾形。 单击&#x200B;**[!UICONTROL 下载]**&#x200B;选项。

   >[!NOTE]
   >
   >仅当您选择同意受保护资产的许可协议时，才启用&#x200B;**[!UICONTROL 下载]**&#x200B;选项。 但是，如果您的选择同时包含受保护和不受保护的资产，则窗格中仅列出受保护的资产，并启用&#x200B;**[!UICONTROL 下载]**&#x200B;选项来下载不受保护的资产。 要同时接受多个受保护资产的许可协议，请从列表中选择资产，然后选择“同 **[!UICONTROL 意”]**。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 在对话框中，单击&#x200B;**[!UICONTROL 下载]**&#x200B;以下载资产或其演绎版。
