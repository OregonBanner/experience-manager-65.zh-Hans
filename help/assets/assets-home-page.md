---
title: AEM Assets主页体验
description: 个性化AEM资产主页，获得丰富的欢迎屏幕体验，包括有关资产近期活动的快照。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# AEM Assets主页体验 {#aem-assets-home-page-experience}

个性化Adobe Experience Manager(AEM)资产主页，获得丰富的欢迎屏幕体验，包括有关资产近期活动情况的快照。

AEM资产主页提供丰富且个性化的欢迎屏幕体验，其中包括最近活动的快照，如最近查看或上传的资产。

默认情况下，资产主页处于禁用状态。 要启用它，请执行以下步骤：

1. 打开AEM配置管理 `https://[aem_server]:[port]/system/console/configMgr`器。
1. 打开 **[!UICONTROL Day CQ DAM事件记录器服务]** 。
1. 选择“ **[!UICONTROL 启用此服务]** ”以启用活动录制。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 从事件类型 **[!UICONTROL 列表中]** ，选择要录制的事件并保存更改。

   >[!CAUTION]
   >
   >启用“已查看资产”、“已查看项目”和“已查看集合”选项，可显着增加已记录的事件数。

1. 从配置管 **[!UICONTROL 理器中打开]** DAM资产主页功能标记服务 `https://[aem_server]:[port]/system/console/configMgr`。
1. 选择选 `isEnabled.name` 项以启用“资产”主页功能。 保存更改。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. 打开“用 **[!UICONTROL 户首选项]** ”对话框，然后选择“ **[!UICONTROL 启用资产主页”]**。 保存更改。

   ![在“用户首选项”对话框中启用资产主页](assets/Annotation-color.png)

启用资产主页后，从导航页面导航到资产用户界面，或直接从URL访问该用户界面 `https://[aem_server]:[port]/aem/assetshome.html/content/dam`。

![在资产用户界面上配置体验链接](assets/config-experience-link.png)

单击 **[!UICONTROL 此处配置体验链接]** ，以添加用户名、背景图像和用户档案图像。

“资产”主页包括以下部分：

* 欢迎部分
* 构件部分

**欢迎部分**

如果您的用户档案存在，欢迎部分将显示一封发送给您的欢迎邮件。 此外，它还显示您的用户档案图片和欢迎图像（如果已配置）。

如果您的用户档案不完整，“欢迎”部分将显示一条通用的欢迎消息和一个用户档案图片的占位符。

**构件部分**

此部分显示在“欢迎”部分的下方，并在以下部分下显示现成构件：

* 活动
* 最近
* 发现

**活动**:在此部分中，“我的活动 **** ”构件显示由登录用户对资产（包括无演绎版的资产）执行的最近活动，例如资产上传、下载、资产创建、编辑、注释、注释和共享。

**最近**:此部 **[!UICONTROL 分下的“最近查看]** ”构件显示登录用户最近访问的实体，包括文件夹、集合和项目。

**发现**:此部 **[!UICONTROL 分下的]** “新建”构件显示最近上传到AEM资产实例的资产和演绎版。

要启用用户活动数据的清除，请从配置管理 **[!UICONTROL 器中启用DAM事件清除服务]** 。 启用此服务后，系统将删除超过指定数量的已登录用户的活动。

“欢迎”屏幕提供了简单的导航帮助，例如，工具栏上的图标可访问文件夹、集合和目录。

>[!NOTE]
>
>启用 [!UICONTROL Day CQ DAM事件记录器和] DAM事件清除服务可增加对JCR的写入操作和搜索索引，这会显着增加AEM服务器上的负载。 AEM服务器上的额外负载可能会影响其性能。

>[!CAUTION]
>
>捕获、过滤和清除资产活动所需的用户主页会对性能产生一定的开销。 因此，管理员应该为主页用户有效配置目标。
>
>Adobe建议执行批量操作的管理员和用户避免使用资产主页功能来防止用户活动增加。 此外，管理员还可以从配置管理器中配置 [!UICONTROL Day CQ DAM事件记录器，从而排除特定用户] 的录制活动 。
>
>如果您使用该功能，Adobe建议您根据服务器负载计划清除频率。
