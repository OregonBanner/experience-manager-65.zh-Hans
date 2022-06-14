---
title: 配置 [!DNL Workfront for Experience Manager enhanced connector]
description: 配置 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
source-git-commit: 00713ea7fe06d4e180232e48a9e3f11b53f4326f
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 0%

---

# 配置 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

具有 [!DNL Adobe Experience Manager] 在安装增强连接器后对其进行配置。 有关安装说明，请参阅 [安装连接器](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
>* Adobe需要部署和配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 仅通过认证合作伙伴或 [!DNL Adobe Professional Services]. 如果部署和配置时没有经过认证的合作伙伴或 [!DNL Adobe Professional Services]，则Adobe不支持此功能。
>
>* Adobe可发布 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使此连接器冗余；如果发生这种情况，客户可能需要从使用此连接器过渡。
>
>* Adobe支持增强的连接器版本1.7.4及更高版本。 不支持以前的预发行版和自定义版本。 要检查增强的连接器版本，请导航到 `digital.hoodoo` 组在 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hans).
>
>* 请参阅 [Workfront的Experience Manager Assets增强连接器合作伙伴认证考试](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 有关考试的信息，请参阅 [考试指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## 配置事件订阅 {#event-subscriptions}

事件订阅用于通知AEM发生在 [!DNL Adobe Workfront]. 有三个 [!DNL Workfront for Experience Manager enhanced connector] 需要事件订阅才能正常工作的功能包括：

* 自动创建项目链接的文件夹。
* 将Workfront文档中的自定义表单值更改同步到AEM资产元数据。
* 在项目完成后自动向Brand Portal发布资产。

要使用这些功能，请启用事件订阅。

* 编辑 [!UICONTROL Workfront工具] Cloud Services配置，然后选择 [!UICONTROL 事件订阅] 选项卡。
* 选择 [!UICONTROL Workfront自定义集成] 您在第6节中创建。
* 单击 [!UICONTROL 启用Workfront事件订阅].

   ![事件订阅](/help/assets/assets/event-subs.png)

## 配置链接的文件夹 {#linked-folders}

要订阅事件，请执行以下步骤：

1. 导航到 **[!UICONTROL 事件订阅]** 选项卡。
1. 选择在中创建的自定义集成 [!DNL Workfront].
1. 单击 **[!UICONTROL 启用Workfront事件订阅]**.

### 链接文件夹结构配置 {#linked-folder-structure}

1. 转到云服务中的项目链接文件夹选项卡。
1. 链接文件夹父路径：在DAM中选择要创建链接文件夹的文件夹。 如果留空，则默认为/content/dam。 确保将Workfront工具元数据架构和Workfront链接文件夹元数据架构应用到选定的文件夹。
1. 链接的文件夹结构：输入逗号分隔值。 每个值应为 `DE:<some-project-custom-form-field>`、Portfolio、程序、年、名称或某些“文字字符串值”（最后一个带引号的值）。 它当前设置为Portfolio、项目、年、DE：项目类型、名称。
1. 如果Workfront中文件夹的标题应包含结构中的所有文件夹，则应选中使用文件夹结构名称在Workfront中构建链接文件夹标题复选框。 否则，将为最后一个文件夹的标题。
1. 子文件夹多字段允许您指定应创建为链接文件夹子文件夹的文件夹列表。
1. 项目状态：选择要创建链接的文件夹，必须将项目设置为的状态。
1. 在具有项目组合的项目中创建链接的文件夹：项目必须属于才能创建链接文件夹的Portfolio列表。 将此列表留空，以便为所有项目组合创建链接的文件夹。
1. 在具有自定义表单字段的项目中创建链接的文件夹：自定义表单字段及其项目创建链接文件夹时必须具有的相应值。 如果此配置留空，则将忽略此配置。 选择 `CUSTOM FORMS: Create DAM Linked Folder` 字段和输入 `Yes` 值。
1. 单击启用自动创建链接文件夹。 如果返回到事件订阅选项卡，您将看到现在有一个创建事件。

![链接文件夹配置](/help/assets/assets/wf-linked-folder-config.png)

## 元数据架构映射 {#metadata-schema-mapping}

### 配置文件夹元数据映射 {#folder-metadata-mapping}

Workfront项目和AEM文件夹之间的元数据映射是在AEM文件夹元数据架构中定义的。 文件夹元数据架构应像往常一样在AEM中创建和配置。 Workfront工具将自动完成下拉列表添加到每个文件夹元数据架构表单字段的设置配置选项卡。 利用此自动完成下拉菜单，可指定每个AEM文件夹属性应映射到的Workfront字段。

要配置映射，请执行以下步骤：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 文件夹元数据架构]**.
1. 选择要编辑的文件夹元数据架构表单，然后单击编辑。
1. 选择要编辑的文件夹元数据架构表单字段，然后选择右侧面板上的设置选项卡。
1. 在 [!UICONTROL 从Workfront字段映射] 字段中，选择要映射到所选AEM文件夹属性的Workfront字段的名称。 可用选项包括：

   * 项目自定义表单字段
   * 项目概述字段(ID、名称、描述、参考编号、计划完成日期、项目所有者、项目赞助者、Portfolio或项目群)

![元数据映射配置](/help/assets/assets/wf-metadata-mapping-config2.png)

### 配置资产元数据映射 {#asset-metadata-mapping}

Adobe Workfront文档和资产之间的元数据映射是在AEM元数据架构中定义的。 应像往常一样在AEM中创建和配置元数据架构。 Workfront工具会将配置选项添加到每个元数据架构表单字段的设置配置选项卡。 利用这些选项，可指定每个AEM属性应映射到的Workfront字段。

要配置映射，请执行以下步骤：

1. 导航到 **工具** > **资产** > **元数据架构**.
1. 选择要编辑的元数据架构表单，然后单击 **编辑** 或从头开始创建新的元数据架构。
1. 选择要编辑的元数据架构表单字段，然后选择 **设置** 选项卡。
1. 在 [!DNL Workfront] 自定义表单字段选择 [!DNL Workfront] 要映射到选定AEM属性的字段。 可用选项包括：

   * 文档自定义表单字段
   * 项目自定义表单字段
   * 发出自定义表单字段
   * 任务自定义表单字段
   * 项目概述字段（ID、名称、描述或参考编号）

1. 如果 [!DNL Workfront] 所选字段 [!UICONTROL Workfront自定义表单字段] 是“Workfront用户提前键入”字段，则需要指定要映射的“Workfront用户”字段。 为此，请选中从Workfront引用的对象字段获取值，然后指定 [!UICONTROL Workfront用户自定义表单字段] 从中检索要映射的值。

   ![元数据映射配置](/help/assets/assets/wf-metadata-mapping-config1.png)

## 映射属性 {#map-property}

此工作流步骤允许用户将资产映射到 [!DNL Workfront] 项目、任务、问题或文档的自定义表单。 的 [!DNL Workfront] 使用有效负载中的相对路径查找此步骤影响的伪像。 要映射的属性在步骤对话框配置中进行控制。

**类型**:利用此字段，可选择属性应映射到的Workfront对象类型。

**ID属性**:利用此字段，可指定属性应映射到的Workfront对象ID的路径。 此字段中指定的路径应该相对于工作流有效负载。

**属性分配**:此多字段允许您指定AEM属性和Workfront字段之间的映射。 多字段中的每个项目都将指定一个映射。 每个映射应具有格式 `<workfront-field>=<aem-mapped-property>`.

* 的 `workfront-field` 可以

   * 由前缀标识的自定义表单字段 `DE:`.
   * 由其名称标识的可编辑字段。 字段名称可在 [[!DNL Workfront] API资源管理器](https://experience.workfront.com/s/api-explorer).

* 的 `aem-mapped-property` 可以是：

   * 文字值。 这些引号应当括起来。
   * AEM资产。 此引用应该相对于工作流有效负载。
   * 命名值。 这些应被括号括起来。
   * 以上3个项目的拼接。 使用指定 `{+}`.
   * 以上3项的变更，以 `{replace(<value>,”old-char”,”new-char”)}`.

* 例如：

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL=”https://my-aem-author/assets.html”{+}{path}`

![要映射属性的配置](/help/assets/assets/wf-map-property-config.png)

## 设置状态 {#set-status}

在工作流编辑器中，编辑 **[!UICONTROL Workfront — 设置状态]** 在 **[!UICONTROL 参数]** 选项卡。

![编辑工作流以设置状态](/help/assets/assets/wf-set-status.png)

## 注释同步 {#comments-sync}

1. 在 [!DNL Experience Manager]，访问 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具配置]**，选择配置，然后选择 **[!UICONTROL 属性]**.

   ![注释同步](/help/assets/assets/comments-sync1.png)

1. 选择 **[!UICONTROL 事件订阅]** ，单击 **[!UICONTROL 启用注释同步]** on **[!UICONTROL 将在Workfront中发表的评论发送到AEM]** 选项。

   ![已启用同步](/help/assets/assets/wf-comment-sync-enabled.png)

要测试从Workfront到AEM的注释同步，请执行以下步骤：

1. 导航到Workfront中的链接文档，然后在“更新”选项卡中添加评论。

   ![在Workfront发表评论](/help/assets/assets/comments-sync2.png)

1. 在AEM中导航到同一链接文档，选择该文档并打开 [!UICONTROL 时间轴] 选项，然后选择 [!UICONTROL 评论]. 左侧边栏显示从以下位置同步的评论 [!DNL Workfront].

## 资产版本 {#asset-versions}

要在AEM中维护资产的版本历史记录，请在AEM中配置资产版本控制。

1. 在Experience Manager中，访问 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具配置]**，然后打开 **[!UICONTROL 高级]** 选项卡。

1. 选择选项 **[!UICONTROL 存储与现有资产版本同名的资产]**. 选中此选项后，可将上传的资产存储到与现有资产版本相同的位置，且名称相同。 如果未选中此选项，则会使用其他名称创建新资产(例如， `asset-name.pdf` 和 `asset-name-1.pdf`)。

1. 选择选项 **[!UICONTROL 创建新版本时更新资产元数据]**. 选中此选项后，每当创建资产的新版本时，都会更新资产元数据。 如果未选中，则资产将保留在创建新版本之前拥有的元数据。

![配置资产版本控制](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>链接的文件夹不支持版本控制。 创建 [!DNL Workfront] 使用链接文件夹中的文档进行校样，则会删除对资产早期版本的注释和批注。

## 附加自定义表单 {#attach-custom-forms}

此工作流步骤允许用户将自定义表单附加到 [!DNL Workfront] 藏物。 此工作流步骤可添加到任何工作流模型。 的 [!DNL Workfront] 将使用有效负载中的相对路径查找此步骤影响的项目。

在Experience Manager的工作流编辑器中，编辑 [!UICONTROL Workfront — 附加自定义表单] 工作流步骤。

![自定义表单](/help/assets/assets/wf-custom-forms.png).

## 自动发布资产 {#auto-publish-assets}

1. 在Experience Manager中，访问 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具配置]**，然后打开 **[!UICONTROL 高级]** 选项卡。

1. 选择 **[!UICONTROL 从Workfront发送资产时自动发布资产]**. 当资产从Workfront发送到AEM时，此选项会启用自动发布功能。 可通过指定Workfront自定义表单字段以及应将其设置为的值，有条件地启用此功能。 每当将文档发送到AEM时，如果文档满足条件，则资产将自动发布。

1. 选择 **[!UICONTROL 在项目完成后将所有项目资产发布到Brand Portal]**. 此选项允许自动将资产发布到 [!DNL Brand Portal] 当它们所属的Workfront项目的状态更改为 `Complete`.

![配置自动发布](/help/assets/assets/wf-auto-publish-config.png)

## Workfront文档自定义表单更新 {#subscribe-workfront-doc-custom-form-updates}

订阅 [!DNL Workfront] 文档自定义表单中，选择 **[!UICONTROL 高级]** 选项卡。 当您订阅这些更新时，它会更新您映射的 [!DNL Experience Manager] 元数据字段(当 [!DNL Workfront] 文档自定义表单已更改。

![Workfront文档自定义表单更新配置 [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
