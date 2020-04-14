---
title: 资产工作流卸载程序
seo-title: 资产工作流卸载程序
description: 了解资产工作流卸载程序。
seo-description: 了解资产工作流卸载程序。
uuid: d1c93ef9-a0e1-43c7-b591-f59d1ee4f88b
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 91f0fd7d-4b49-4599-8f0e-fc367d51aeba
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# 资产工作流卸载程序{#assets-workflow-offloader}

资产工作流卸载程序允许您启用Adobe Experience Manager(AEM)资产的多个实例，以减少主（领导）实例的处理负载。 处理负载分布在引线实例和您添加到引线实例的各种卸载程序(worker)实例之间。 分配资产的处理负载可提高AEM资产处理资产的效率和速度。 此外，它还有助于分配专用资源以处理特定MIME类型的资产。 例如，您可以在拓扑中分配特定节点，以仅处理InDesign资源。

## 配置卸载器拓扑 {#configure-offloader-topology}

使用配置管理器为引线实例添加URL，为引线实例上的连接请求添加卸载程序实例的主机名。

1. 点按／单击AEM徽标，然后选择“工 **具** ”>“操作 **”** >“Web控 **制台** ”以打开配置管理器。
1. 从Web控制台中，选择“ **Sling** ”>“拓 **扑管理”**。

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. 在拓扑管理页面中，点按／单击 **配置Discovery.Oak服务链接** 。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 在“发现服务配置”页中，在“拓扑连接器URL”字段中为前导实例指 **定连接器URL** 。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 在“拓 **扑连接器白名单** ”字段中，指定允许与引线实例连接的脱机实例的IP地址或主机名。 Tap/click **Save**.

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. 要查看连接到引线实例的卸载器实例，请转到“工 **具** ”>“部署 **”** >“拓扑” **** ，然后点按／单击“群集视图”。

## 禁用卸载 {#disable-offloading}

1. 点按／单击AEM徽标，然后选择“工 **具** ”>“ **部署** ” **>“**&#x200B;卸载”。 “卸 **载浏览器** ”页显示主题和可使用主题的服务器实例。

   ![chlimage_1-48](assets/chlimage_1-48a.png)

1. 禁用 *用户与之交互以上传或更改AEM资产的引导实例的com/adobe/granite/workflow/offloading* 主题。

   ![chlimage_1-49](assets/chlimage_1-49a.png)

## 在引导器实例上配置工作流启动器 {#configure-workflow-launchers-on-the-leader-instance}

将工作流启动程序配置为在 [!UICONTROL 引导实例上使用] DAM更新资产分载工作流，而不是 **Dam更新资产工作流** 。

1. 点按／单击AEM徽标，然后选择“工 **具** ”>“工作流 **”** >“启动 **器****** ”以打开Workflow LaunchersAchole。

   ![chlimage_1-50](assets/chlimage_1-50a.png)

1. 找到两个启动器配置，分别创建 **了事件类型节点** 和修改 **了节点** ，这两个配置运行 **** DAM更新资产工作流。
1. 对于每个配置，选中前面的复选框，然后点按／单击工具栏中的 **视图属性** 图标以显示启动 **器属性对话框** 。

   ![chlimage_1-51](assets/chlimage_1-51a.png)

1. 从“工 **作流** ”列表中 [!UICONTROL ，选择“] DAM更新资产卸载” **，然后点按／单击**&#x200B;保存。

   ![chlimage_1-52](assets/chlimage_1-52a.png)

1. 点按／单击AEM徽标，然后选择“工 **具** ”>“工作流 **”** >“模型 **”以打开“工作流模****** 型”页面。
1. 选择 [!UICONTROL DAM更新资产分载工作流] ，然后点按／单击工具栏中的 **编辑** ，以显示其详细信息。

   ![chlimage_1-53](assets/chlimage_1-53a.png)

1. 显示“ **DAM工作流卸载”步骤的上下文菜单** ，然后选择“编 **辑”**。 验证配置对话框的“ **常规参数** ”选项卡的“ **作业主题** ”字段中的条目。

   ![chlimage_1-54](assets/chlimage_1-54a.png)

## 禁用卸载器实例上的工作流启动器 {#disable-the-workflow-launchers-on-the-offloader-instances}

禁用在引导实例上运行 **DAM更新资产工作流的工作流启动程序** 。

1. 点按／单击AEM徽标，然后选择“工 **具** ”>“工作流 **”** >“启动 **器****** ”以打开Workflow LaunchersAchole。

   ![chlimage_1-55](assets/chlimage_1-55a.png)

1. 找到两个启动器配置，分别创建 **了事件类型节点** 和修改 **了节点** ，这两个配置运行 **** DAM更新资产工作流。
1. 对于每个配置，选中前面的复选框，然后点按／单击工具栏中的 **视图属性** 图标以显示启动 **器属性对话框** 。

   ![chlimage_1-56](assets/chlimage_1-56a.png)

1. 在“激 **活** ”部分，拖动滑块以禁用工作流启动器，然后点按／单击 **保存** 以禁用它。

   ![chlimage_1-57](assets/chlimage_1-57a.png)

1. 在前导实例上传任何图像类型的资产。 验证卸载的实例为资产生成并移回的缩略图。

