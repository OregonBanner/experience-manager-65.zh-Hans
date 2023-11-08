---
title: 迁移 AEM Forms 资产和文档
description: 通过迁移实用程序，您可以将Adobe Experience Manager (AEM) Forms资源和文档从AEM 6.3 Forms或更早版本迁移到AEM 6.4 Forms。
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
docset: aem65
role: Admin
exl-id: 0f9aab7d-8e41-449a-804b-7e1bfa90befd
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 2%

---

# 迁移 AEM Forms 资产和文档{#migrate-aem-forms-assets-and-documents}

迁移实用程序将转换 [自适应Forms资源](../../forms/using/introduction-forms-authoring.md)， [云配置](/help/sites-developing/extending-cloud-config.md)、和 [相应的管理资源](/help/forms/using/cm-overview.md) 从早期版本中使用的格式转换到Adobe Experience Manager (AEM) 6.5 Forms中使用的格式。 运行迁移实用程序时，将迁移以下内容：

* 自适应表单的自定义组件
* 自适应表单和通信管理模板
* 云配置
* 通信管理和自适应表单资产

>[!NOTE]
>
>如果异地升级，则对于通信管理资产，您可以在每次导入资产时运行迁移。 要迁移Correspondence Management，您必须安装Forms兼容包。

## 迁移方法 {#approach-to-migration}

您可以 [升级](../../forms/using/upgrade.md) 从AEM Forms 6.4、6.3或6.2到最新版本的AEM Forms 6.5，或者安装了一个新版本。 根据您是升级以前的安装还是执行了全新安装，您必须执行以下操作之一：

**如果有就地升级**

如果您执行就地升级，则升级的实例已经具有资源和文档。 但是，您必须先安装 [AEMFD兼容包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans) （包括Correspondence Management兼容包）

然后，您必须通过以下方式更新资源和文档 [运行迁移实用程序](#runningmigrationutility).

**如果有异地安装**

如果这是异地（全新）安装，则在您能够使用资源和文档之前，您必须安装 [AEMFD兼容包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans) （包括Correspondence Management兼容包）。

然后，您必须在新设置中导入资产包（zip或cmp），然后通过以下方式更新资产和文档 [运行迁移实用程序](#runningmigrationutility). Adobe建议仅在运行迁移实用程序后，才在新设置上创建资源。

到期日期 [向后兼容性相关](/help/sites-deploying/backward-compatibility.md) 会更改crx-repository中几个文件夹的位置。 手动将依赖项（自定义库和资产）从以前的设置导出和导入到新的环境。

## 在继续迁移之前 {#prerequisites}

对于相应的管理资产：

* 对于从上一个平台导入的资产，将添加一个属性： **fd：version=1.0**.
* 自AEM 6.1 Forms起，无法立即使用注释。 之前添加的注释可在资源中使用，但不会自动在界面中显示。 自定义AEM Forms用户界面中的extendedProperties属性以显示注释。
* 在某些早期版本(如LiveCycleES4)中，文本是使用Flex RichTextEditor进行编辑的，但由于AEM 6.1 Forms，因此使用HTML编辑器。 由于此渲染和字体外观，字体大小和字体边距可能与创作用户界面中以前的版本不同。 但是，字母在呈现时看起来相同。
* 文本模块中的列表已得到改进，现在呈现方式有所不同。 视觉上可能有所差异。 Adobe建议您渲染并查看您在文本模块中使用列表的字母。
* 由于图像内容模块已转换为DAM资源并在迁移期间将布局和片段添加到表单，因此这些模块的“更新者”属性将更改为“管理员”。
* 资产的版本历史记录未迁移，且在迁移后不可用。 迁移后的后续版本历史记录将得到维护。
* 由于AEM 6.1 Forms已弃用发布准备就绪状态，因此所有处于发布准备就绪状态的资源都将更改为已修改状态。
* 由于用户界面在AEM Forms 6.3中进行了更新，因此执行自定义设置的步骤也有所不同。 如果您是从6.3之前的版本迁移，请重做自定义设置。
* 布局片段移自 `/content/apps/cm/layouts/fragmentlayouts/1001` 到 `/content/apps/cm/modules/fragmentlayouts`. 资产中的数据字典引用显示数据字典的路径而不是其名称。
* 必须重新调整用于文本模块中对齐的任何制表符空格。 有关更多信息，请参阅 [通信管理 — 使用制表符间距排列文本](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* 资产编辑器配置会更改为通信管理配置。
* 资产将移动到名为“现有文本”和“现有列表”等名称的文件夹下。

## 使用迁移实用程序 {#using-the-migration-utility}

### 运行迁移实用程序 {#runningmigrationutility}

在更改资产或创建资产之前，请运行迁移实用程序。 Adobe建议您在进行任何更改或创建资源后不要运行该实用程序。 确保在迁移过程中未打开通信管理或自适应Forms Assets用户界面。

首次运行Migration Utility时，将使用以下路径和名称创建日志： `\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log`. 此日志会不断更新通信管理和自适应Forms迁移信息，例如移动资源。

>[!NOTE]
>
>在运行迁移实用程序之前，请确保已备份crx存储库。

1. 在浏览器会话中，以管理员身份登录到您的AEM创作实例。

1. 在浏览器中打开以下URL：

   https://[*主机名*]：[*端口*]/[*上下文路径*]/libs/fd/foundation/gui/content/migration.html

   浏览器显示四个选项：

   * AEM Forms 资产迁移
   * 自适应Forms自定义组件迁移
   * 自适应Forms模板迁移
   * AEM Forms 云配置迁移

1. 执行以下操作以执行迁移：

   * 要迁移 **资产**，点按AEM Forms资产迁移，然后在下一个屏幕中，点按 **开始迁移**. 将迁移以下项：

      * 自适应表单
      * 文档片段
      * 主题
      * 书信
      * 数据字典

   >[!NOTE]
   >
   >在资源迁移过程中，您可能会找到警告消息，例如“发现冲突……”。 此类消息指示无法迁移自适应表单中某些组件的规则。 例如，如果组件有一个同时包含规则和脚本的事件，如果规则发生在任何脚本之后，则不会迁移组件的任何规则。 您可以 [通过打开规则编辑器迁移此类规则](#migrate-rules) 在自适应表单创作中。

   * 要迁移自适应表单自定义组件，请点击 **自适应Forms自定义组件迁移** 在自定义组件迁移页面中，点按 **开始迁移**. 将迁移以下项：

      * 为自适应Forms编写的自定义组件
      * 组件叠加（如果有）。

   * 要迁移自适应表单模板，请点击 **自适应Forms模板迁移** 在自定义组件迁移页面中，点按 **开始迁移**. 将迁移以下项：

      * 自适应表单模板创建于 `/apps` 或 `/conf` 使用AEM模板编辑器。

   * 迁移AEM Forms Cloud Configuration Services以使用新的上下文感知云服务范例，其中包括支持触摸的UI(在 `/conf`)。 迁移AEM Forms云配置服务时，云服务位于 `/etc` 已移动到 `/conf`. 如果您没有任何依赖于旧版路径的云服务自定义(`/etc`)，Adobe建议您在升级到6.5后运行迁移实用程序；使用云配置触屏UI执行任何进一步的工作。 如果您有任何现有的云服务自定义设置，请继续在升级后的设置中使用经典UI，直到自定义设置更新以与迁移的路径保持一致(`/conf`)，然后运行迁移实用程序。

   要迁移 **AEM Forms云服务**，其中包括以下内容，请点按AEM Forms云配置迁移（云配置迁移独立于AEMFD兼容包）。 点按AEM Forms云配置迁移，然后在配置迁移页面上点按 **开始迁移**：

   * 表单数据模型云服务

      * 源路径： `/etc/cloudservices/fdm`
      * 目标路径： `/conf/global/settings/cloudconfigs/fdm`

   * Recaptcha

      * 源路径： `/etc/cloudservices/recaptcha`
      * 目标路径： `/conf/global/settings/cloudconfigs/recaptcha`

   * Adobe Sign

      * 源路径： `/etc/cloudservices/echosign`
      * 目标路径： `/conf/global/settings/cloudconfigs/echosign`

   * Typekit云服务

      * 源路径： `/etc/cloudservices/typekit`
      * 目标路径： `/conf/global/settings/cloudconfigs/typekit`

   在迁移过程中，浏览器窗口会显示以下内容：

   * 资产更新时：资产已成功更新。
   * 迁移完成后：完成资产的迁移。

   运行迁移实用程序时，会执行以下操作：

   * **将标记添加到资源**：添加标记“通信管理：已迁移资源”/“自适应Forms：已迁移资源”。 ，以便用户能够识别已迁移的资产。 运行迁移实用程序时，系统中所有现有资源均标记为已迁移。
   * **生成标记**：以前系统中存在的类别和子类别将作为标记创建，然后这些标记与AEM中的相关通信管理资源相关联。 例如，信件模板的类别（索赔）和子类别（索赔）作为标记生成。

1. 在迁移实用程序运行完成后，继续执行 [内部管理任务](#housekeepingtasks).

#### 使用规则编辑器迁移规则 {#migrate-rules}

通过在自适应Forms编辑器的规则编辑器中打开这些组件，可以迁移这些组件。

* 要在自定义组件中迁移规则和脚本（如果从6.3升级，则不需要这样做），请点按自适应Forms自定义组件迁移，然后在下一个屏幕中，点按开始迁移。 将迁移以下项：

   * 使用规则编辑器（6.1 FP1及更高版本）创建的规则和脚本

   * 在6.1及更低版本的UI中使用“脚本”选项卡创建的脚本

* 要迁移模板（如果从6.3和6.4升级，则不需要迁移模板），请点按自适应Forms模板迁移，然后在下一个屏幕中，点按开始迁移。 将迁移以下项：

   * 旧模板 — 在/apps下使用AEM 6.1 Forms或更低版本创建的自适应表单模板。 这包括模板组件中定义的脚本。

   * 新模板 — 使用下的模板编辑器创建的自适应表单模板 `/conf`. 这包括迁移使用规则编辑器创建的规则和脚本。

### 运行迁移实用程序后的内部管理任务 {#housekeepingtasks}

运行迁移实用程序后，请完成以下内部管理任务：

1. 确保布局和片段布局的XFA版本为3.3或更高版本。 如果您使用的是较旧版本的布局和片段布局，则呈现信件时可能会出现问题。 要将旧版XFA更新到最新版本，请完成以下步骤：

   1. [以zip文件格式下载XFA](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) 从Forms用户界面访问。
   1. 提取文件。
   1. 在最新的设计器中打开XFA文件并保存。 XFA的版本将更新到最新版本。
   1. 在Forms用户界面中上传XFA。

1. 发布迁移前在上一个系统中发布的所有资源。 迁移实用程序仅在创作实例上更新资产，要更新发布实例上的资产，您必须发布资产。

1. 在AEM Forms 6.4和6.5中，更改了Forms用户组的某些权限。 如果您希望您的任何用户能够上传包含脚本的XDP和自适应Forms或使用代码编辑器，则必须将它们添加到forms-power-users组。 同样，模板作者无法在规则编辑器中再使用代码编辑器。 要使用户能够使用代码编辑器，请将其添加到af-template-script-writers组。 有关将用户添加到组的说明，请参阅 [管理用户和用户组](/help/communities/users.md).
