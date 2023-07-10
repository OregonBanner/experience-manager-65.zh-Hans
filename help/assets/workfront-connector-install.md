---
title: 安装 [!DNL Workfront for Experience Manager enhanced connector]
description: 安装 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
hide: true
source-git-commit: 6f01f5725ed2b0533756830c1a5e55b7464708f6
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 4%

---

# 安装 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en) |
| AEM 6.5 | 本文 |

在中具有管理员访问权限的用户 [!DNL Adobe Experience Manager] 安装增强型连接器。 安装之前，请查看平台支持及其他 [连接器的先决条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe需要部署和配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 仅通过认证合作伙伴或 [!DNL Adobe Professional Services]. 如果部署与配置时没有认证合作伙伴或 [!DNL Adobe Professional Services]，它不受Adobe支持。
>
>* Adobe可能会将更新发布到 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使此连接器成为冗余连接器；如果发生这种情况，客户可能需要从使用此连接器过渡。
>
>* Adobe支持增强型连接器版本1.7.4及更高版本。 不支持以前的预发行版和自定义版本。 要检查增强型连接器版本，请导航至 `digital.hoodoo` 组在左窗格中可用 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en).
>
>* 参见 [Workfront for Experience Manager Assets增强型连接器的合作伙伴认证考试](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 有关考试的信息，请参见 [考试指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

要安装连接器，请执行以下步骤：

1. 从以下位置下载连接器 [[!DNL Software Distribution] 链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [配置防火墙](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).
1. 在Dispatcher上，允许命名的HTTP标头 `authorization`， `username`、和 `apikey`. 允许 `GET`， `POST`、和 `PUT` 请求 `/bin/workfront-tools`.
1. 确保中不存在以下路径 [!DNL Experience Manager] 存储库：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. 使用以下方式安装包 [!UICONTROL 包管理器]. 要了解如何安装软件包，请参阅 [包管理器文档](/help/sites-administering/package-manager.md).
1. 创建 `wf-workfront-users` 在 [!DNL Experience Manager] 用户组和分配权限 `jcr:all` 到 `/content/dam`.

系统用户 `workfront-tools` 将自动创建，并自动管理所需的权限。 所有用户来自 [!DNL Workfront] 使用该连接器的用户会自动添加为该组的一部分。

## 配置之间的连接 [!DNL Experience Manager] 和 [!DNL Workfront] {#configure-connection}

要创建与Workfront的连接，请执行以下步骤：

1. In [!DNL Experience Manager]，选择 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具配置]**.

1. 选择 `workfront-tools` 在左侧面板中选择 **[!UICONTROL 创建]** 选项。

1. 在 **[!UICONTROL Workfront连接]** 对话框，请提供以下内容所需的详细信息： [!DNL Workfront] 部署，并选择 **[!UICONTROL 连接到Workfront]** 选项。 成功连接后， [!DNL Workfront] 文档自定义集成是在以下位置自动创建的： [!DNL Workfront] 环境。

   ![Connect [!DNL Experience Manager] 和 [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 要验证连接，请在中访问该连接 [!DNL Workfront] 并验证API密钥是否相同，以及连接是否为 **[!UICONTROL 已启用]**. 要执行此操作，请选择 **[!UICONTROL 设置]** > **[!UICONTROL 文档]** > **[!UICONTROL 自定义集成]** 在 [!DNL Workfront].

## 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets允许您更新 [!DNL Workfront for Experience Manager enhanced connector] 从以前的版本到最新的版本。

要更新 [!DNL Workfront for Experience Manager enhanced connector] 到最新版本：

1. 从下载最新版本的增强型连接器 [[!DNL Software Distribution] 链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. 使用以下方式安装包 [!UICONTROL 包管理器]. 要了解如何安装软件包，请参阅 [包管理器文档](/help/sites-administering/package-manager.md).
