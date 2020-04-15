---
title: 资产中的数字版权管理
description: 了解如何在AEM中管理授权资产的资产到期状态和信息。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Digital Rights Management for digital assets {#digital-rights-management-in-assets}

数字资产通常与许可证相关联，许可证会指定其使用条款和持续时间。 由于Adobe Experience Manager(AEM)资产已与AEM平台完全集成，因此您可以有效管理资产到期信息和资产状态。 您还可以将许可信息与资产关联。

## 资产过期 {#asset-expiration}

资产到期是强制执行资产许可要求的有效方式。 它可确保发布的资产在过期时取消发布，这样不会发生任何许可违规。 没有管理员权限的用户无法编辑、复制、移动、发布和下载过期的资产。

您可以在“卡片”和“视图”视图的“资产”控制台中，对资产进行过期状态列表。

![expired_flag_card](assets/expired_flag_card.png)

*图：在卡视图中，卡上的标记指示已过期的资产*

**列表视图**

![expired_flag_列表](assets/expired_flag_list.png)

*图：在列表视图中，“状[!UICONTROL 态]”列显示“[!UICONTROL 已过期]”横幅。*

您可以视图时间轴中资产的到期状态。 选择资产，然后从GlobalNav菜单中选择时间轴。

![chlimage_1-144](assets/chlimage_1-144.png)

您还可以视图引用边栏中资产的到期 **[!UICONTROL 状态]** 。 它管理资产到期状态以及复合资产与引用的子资产、集合和项目之间的关系。

1. 导航到要视图其引用网页和复合资产的资产。
1. 选择资产，然后选择Experience Manager徽标。

1. 从菜 **[!UICONTROL 单中选择]** “引用”(References)。

   ![chlimage_1-146](assets/chlimage_1-146.png)

   对于过期的资产，引用边栏顶部会显示资产 **[!UICONTROL 的到期状态]** “已过期”。

   ![chlimage_1-147](assets/chlimage_1-147.png)

   如果资产已过期子资产，则引用边栏会显示资产已 **[!UICONTROL 过期子资产的状态]**。

   ![chlimage_1-148](assets/chlimage_1-148.png)

### 搜索过期的资产 {#search-expired-assets}

您可以在“搜索”面板中搜索过期的资产，包括过期的子资产。

1. 在“资产”控制台中，单击工 **[!UICONTROL 具栏中]** 的搜索以显示“全局搜索”框。

1. 在“搜索”框中放置光标时，点击“返回”键以显示“搜索结果”页。

   ![chlimage_1-150](assets/chlimage_1-150.png)

1. 单击Experience Manager徽标以显示搜索面板。

   ![chlimage_1-151](assets/chlimage_1-151.png)

1. Click the **[!UICONTROL Expiry Status]** option to expand it.

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. 选择 **[!UICONTROL 过期]**。 过期的资产会显示在搜索结果中。

   ![chlimage_1-153](assets/chlimage_1-153.png)

当您选择“已过 **期** ”选项时，“资产”控制台仅显示复合资产引用的已过期资产和子资产。 引用已过期子资产的复合资产在子资产过期后不会立即显示。 而是在AEM资产检测到下次运行调度程序时引用过期的子资产后显示子资产。

如果您将已发布资产的到期日修改为早于当前调度程序周期的日期，计划会在下次运行时将此资产检测为已过期资产，并相应地反映其状态。

此外，如果故障或错误导致调度程序无法检测当前周期中的过期资产，调度程序会在下一个周期中重新检查这些资产并检测其过期状态。

要启用 Assets 控制台以显示引用的复合资产以及过期的子资产，请在 AEM Configuration Manager 中配置 **Adobe CQ DAM 到期通知**&#x200B;工作流。

1. 打开AEM配置管理器。
1. 选择 **[!UICONTROL Adobe CQ DAM到期通知]**。 默认情况下， **[!UICONTROL 将选择基于时间的调度程序]** ，这将计划作业以在特定时间检查资产是否已过期子资产。 作业完成后，已过期的子资产和引用的资产会在搜索结果中显示为已过期。

   ![chlimage_1-154](assets/chlimage_1-154.png)

1. 要定期运行该作业，请清除&#x200B;**[!UICONTROL 基于时间的计划程序规则]**&#x200B;字段，并在&#x200B;**[!UICONTROL 周期性计划程序]**&#x200B;字段中修改时间（以秒为单位）。例如，示例表达式“0 0 0 &amp;ast; &amp;ast; ?”会在 00 小时开始作业。
1. 选择 **[!UICONTROL 发送电子邮件]** ，以在资产过期时接收电子邮件。

   >[!NOTE]
   >
   >只有资产创建者（将特定资产上传到AEM资产的人员）在资产过期时才会收到电子邮件。 有关在 [](/help/sites-administering/notification.md) 整个AEM级别配置电子邮件通知的其他详细信息，请参阅配置电子邮件通知。

1. 在“先 **[!UICONTROL 前通知(以秒为单位]** )”字段中，指定您要接收到有关到期的通知时，资产到期前的时间（以秒为单位）。 如果您是管理员或资产创建者，您会在资产到期前收到一条消息，通知您该资产将在指定时间后过期。

   资产到期后，您会收到另一则通知，确认到期。 此外，过期的资产也会被取消激活。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 资产状态 {#asset-states}

Adobe Experience Manager(AEM)资产的“资产”控制台可显示资产的各种状态。 根据特定资产的当前状态，其卡视图会显示描述其状态的标签，例如“已过期”、“已发布”、“已批准”、“被拒绝”等。

1. 在“资产”用户界面中，选择一个资产。

   ![chlimage_1-155](assets/chlimage_1-155.png)

1. 单击 **[!UICONTROL 工具栏]** 中的发布。 如果工具栏上未显示 **发布** ，请单击工具栏上的 **[!UICONTROL 更多]** ，然后找到发布 **[!UICONTROL 选项]** 。

   ![chlimage_1-156](assets/chlimage_1-156.png)

1. 从菜 **[!UICONTROL 单中选择]** “发布”，然后关闭确认对话框。
1. 退出选择模式。 资产的发布状态显示在卡片视图中资产缩略图的底部。 在列表视图中，已发布列显示资产发布的时间。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 在“资产”界面中，选择一个资产，然后单击“ **[!UICONTROL 属性]** ”以显示其资产详细信息页面。

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. 在高级选项卡中，从过期字段中设置资产的过 **[!UICONTROL 期日]** 。

   ![在“过期”字段中设置资产到期日期和时间](assets/asset-properties-advanced-tab.png)


   *图：资产属性中的“高级”选项卡，用于设置资产过期时间*

1. 单击 **[!UICONTROL 保存]** ，然后单 **[!UICONTROL 击关闭]** ，以显示资产控制台。
1. 资产的发布状态会在卡片视图中资产缩略图的底部指示过期状态。 在列表视图中，资产的状态显示为“已过期” ****。

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. 在“资产”控制台中，选择一个文件夹，然后在该文件夹上创建审核任务。
1. 在审核任务中审核和批准／拒绝资产，然后单击完 **[!UICONTROL 成]**。
1. 导览至创建了审核任务的文件夹。 您批准／拒绝的资产的状态显示在卡视图的底部。 在列表视图中，批准和到期状态显示在相应的列中。

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. 要根据资产的状态搜索资产，请单击“搜 **[!UICONTROL 索]** ”以显示“搜索”栏。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 按回车键，然后单 **[!UICONTROL 击GlobalNav]** 以显示“搜索”面板。
1. In the Search panel, click **[!UICONTROL Publish Status]** and select **[!UICONTROL Published]** to search for published assets in AEM Assets.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Click **[!UICONTROL Approval Status]** and click the appropriate option to search for approved or rejected assets.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 要根据资产的到期状态搜索资产，请在“搜索”面板中选择&#x200B;**[!UICONTROL 到期状态]**，然后选择相应的选项。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 您还可以根据各种搜索彩块化下的状态组合来搜索资产。 例如，您可以在搜索彩块化中选择相应的选项，以搜索已在审核任务中批准但尚未过期的已发布资产。

   ![chlimage_1-166](assets/chlimage_1-166.png)

## Digital Rights Management in Assets {#digital-rights-management-in-assets-1}

此功能强制您接受许可协议，然后您才能从Adobe Experience Manager资产下载许可资产。

如果您选择受保护的资产并单击“ **[!UICONTROL 下载]**”，则会将您重定向到接受许可协议的许可页面。 如果您不接受许可协议，则禁用“ **[!UICONTROL 下载]** ”按钮。

如果选择包含多个受保护的资产，则一次选择一个资产，接受许可协议，然后继续下载该资产。

如果满足以下任一条件，则资产将被视为受保护：

* 资产元数据属 `xmpRights:WebStatement` 性指向包含资产的许可协议的页面路径。
* 资产元数据属性的值是 `adobe_dam:restrictions` 一个原始HTML，用于指定许可协议。

>[!NOTE]
>
>已弃用 `/etc/dam/drm/licenses` 用于在AEM早期版本中存储许可证的位置。
>
>如果您创建或修改许可证页面，或从以前的AEM版本中移植这些页面，Adobe建议您将它们存储在或 `/apps/settings/dam/drm/licenses` 下方 `/conf/&ast;/settings/dam/drm/licenses`。

### 下载受DRM保护的资源 {#downloading-drm-assets}

1. 在卡片视图中，选择要下载的资产，然后单击下 **[!UICONTROL 载]**。
1. 在&#x200B;**[!UICONTROL 版权管理]**&#x200B;页面，从列表中选择要下载的资产。
1. 在“许可”窗格中，选择“ **[!UICONTROL 同意”]**。 您接受其许可协议的资产旁边会显示一个勾号。 单击“下 **[!UICONTROL 载]** ”按钮。

   >[!NOTE]
   >
   >仅当 **[!UICONTROL 您选择同意受保护资产的许可协议时]** ，才会启用“下载”按钮。 但是，如果您的选择包含受保护和不受保护的资产，则只有受保护的资产会列在左侧窗格中，并且会启用“ **[!UICONTROL Download]** ”按钮来下载不受保护的资产。 要同时接受多个受保护资产的许可协议，请从列表中选择资产，然后选择“同 **[!UICONTROL 意”]**。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 在对话框中，单击 **[!UICONTROL 下载]** ，以下载资产或其演绎版。
