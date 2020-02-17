---
title: 迁移AEM Forms资产和文档
seo-title: 迁移AEM Forms资产和文档
description: 使用迁移实用程序，您可以将AEM Forms资产和文档从AEM 6.3 Forms或先前版本迁移到AEM 6.4 Forms。
seo-description: 使用迁移实用程序，您可以将AEM Forms资产和文档从AEM 6.3 Forms或先前版本迁移到AEM 6.4 Forms。
uuid: a3fdf940-7fc2-441c-91c8-ad66ba47e5f2
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
discoiquuid: 39dfef85-d047-4b6d-a0f5-92bd77df103b
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# 迁移AEM Forms资产和文档{#migrate-aem-forms-assets-and-documents}

迁移实用程序将 [Adaptive Forms资产](../../forms/using/introduction-forms-authoring.md)、云配置和 [](/help/sites-developing/extending-cloud-config.md)[](/help/forms/using/cm-overview.md) Correporsent Management资产从早期版本中使用的格式转换为AEM 6.5 Forms中使用的格式。 运行迁移实用程序时，将迁移以下内容：

* 自适应表单的自定义组件
* 自适应表单和通信管理模板
* 云配置
* 通信管理和自适应表单资产

>[!NOTE]
>
>如果升级不到位，对于Corroperse Management资产，您可以在每次导入资产时运行迁移。 对于“通信管理”迁移，您需要安装“表单兼容性包”。

## 迁移方法 {#approach-to-migration}

您可 [以从](../../forms/using/upgrade.md) AEM Forms 6.4、6.3或6.2升级到最新版AEM Forms 6.5，或执行全新安装。 根据您是升级了之前的安装还是执行了新安装，您需要执行以下操作之一：

**如果是就地升级**

如果您执行了就地升级，则升级后的实例已包含资产和文档。 但是，在使用资源和文档之前，您需要安装 [AEMFD兼容性包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) （包括对应管理兼容性包）

然后，您需要通过运行迁移实用程序来 [更新资源和文档](#runningmigrationutility)。

**如果安装不当**

如果安装不当（新），则在您使用资源和文档之前，您需要安装 [AEMFD兼容性包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) （包括Correponsement Management Compatibility包）。

然后，您需要在新设置上导入您的资产包（zip或cmp），然后运行迁移实用程序来更新 [资产和文档](#runningmigrationutility)。 Adobe建议仅在运行迁移实用程序之后才在新设置上创建新资源。

由于向后 [兼容性相关的更改](/help/sites-deploying/backward-compatibility.md) ,crx-repository中几个文件夹的位置会发生更改。 从以前的设置手动将依赖项（自定义库和资源）导出和导入到新环境。

## 在继续迁移前阅读 {#prerequisites}

对于通信管理资产：

* 对于从先前平台导入的资产，将添加一个属性： **fd:version=1.0**。
* 自AEM 6.1 Forms起，注释不会开箱即用。 之前添加的注释在资产中可用，但不会自动显示在界面上。 您需要自定义AEM Forms用户界面中的extendedProperties属性，以使注释可见。
* 在LiveCycle ES4等旧版本中，文本是使用Flex richTextEditor编辑的，但自AEM 6.1 Forms开始，便使用HTML编辑器。 由于字体的呈现和外观、字体大小和字体边距可能与作者用户界面中的先前版本不同。 但是，在呈现时，字母看起来是一样的。
* 文本模块中的列表得到改进，现在呈现方式有所不同。 可能存在视觉差异。 我们建议您渲染并查看您在文本模块中使用列表的字母。
* 由于图像内容模块已转换为DAM资产，并且布局和片段在迁移期间已添加到表单，因此这些模块的“更新依据”属性将更改为管理员。
* 资产的版本历史记录不会迁移，且在迁移后不可用。 迁移后将保留后续版本历史记录。
* 自AEM 6.1表单起，“准备发布”状态已弃用，因此“准备发布”状态中的所有资产都将更改为“已修改”状态。
* 由于AEM Forms 6.3中的用户界面已更新，因此执行自定义的步骤也有所不同。 如果您是从6.3之前的版本迁移，则需要重做自定义。
* 布局片段从/content/apps/cm/layouts/fragmentlayouts/1001移至/content/apps/cm/modules/fragmentlayouts。 资产中的数据字典引用显示数据字典的路径而不是其名称。
* 需要重新调整文本模块中用于对齐的任何制表符空间。 有关详细信息，请参 [阅对应管理——使用制表符间距排列文本](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html)。
* 资产书写器配置会更改为“对应管理”配置。
* 资产会移到文件夹下，并且文件夹的名称包括“现有文本”和“现有列表”。

## 使用迁移实用程序 {#using-the-migration-utility}

### 运行迁移实用程序 {#runningmigrationutility}

在对资产进行任何更改或创建资产之前，请运行迁移实用程序。 我们建议您在进行任何更改或创建资产后不要运行实用程序。 确保在迁移进程运行时，“对应管理”或“自适应表单资产”用户界面未打开。

首次运行迁移实用程序时，将创建具有以下路径和名称的日志：\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log。 此日志会不断更新“对应管理”和“自适应表单”迁移信息，如资产移动。

>[!NOTE]
>
>运行迁移实用程序之前，请确保已备份crx存储库。

1. 在浏览器会话中，以管理员身份登录到AEM作者实例。

1. 在浏览器中打开以下URL:

   https://[*hostname*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   浏览器显示四个选项：

   * AEM Forms 资产迁移
   * 自适应表单自定义组件迁移
   * 自适应表单模板迁移
   * AEM Forms 云配置迁移

1. 执行以下操作以执行迁移：

   * 要迁移 **资产**，请点按AEM Forms资产迁移，然后在下一个屏幕中，点按开始 **迁移**。 以下内容已迁移：

      * 自适应表单
      * 文档片段
      * 主题
      * 书信
      * 数据字典
   >[!NOTE]
   >
   >在资产迁移过程中，您可能会找到警告消息，如“找到的冲突……”。 这些消息表示无法迁移自适应表单中某些组件的规则。 例如，如果组件有一个同时具有规则和脚本的事件，则在任何脚本之后都会发生规则，则不会迁移组件的任何规则。 但是，可以通过在自适应表单创作中打开规则编辑器来迁移这些规则。
   >
   >
   >可以通过在自适应表单编辑器的规则编辑器中打开这些组件来迁移它们。
   >
   >
   >
   >    * 要在自定义组件中迁移规则和脚本（从6.3升级时不需要），请点按自适应表单自定义组件迁移，然后在下一个屏幕中，点按开始迁移。 以下内容已迁移：   >
      >
      >
      >        

      * 使用规则编辑器（6.1 FP1和更高版本）创建的规则和脚本
      >        * 使用6.1及更早版本UI中的“脚本”选项卡创建的脚本
   >
   >
   >    * 要迁移模板（从6.3和6.4升级时不需要），请点按自适应表单模板迁移，然后在下一个屏幕中，点按开始迁移。 以下内容已迁移：
      >
      >
      >
      >        


      * 旧模板——在/apps下使用AEM 6.1 Forms或更早版本创建的自适应表单模板。 这包括在模板组件中定义的脚本。
      >        * 新模板——使用/conf下的模板编辑器创建的自适应表单模板。 这包括迁移使用规则编辑器创建的规则和脚本。


   * 要迁移自适应表单自定义组件，请点 **按自适应表单自定义组件迁移** ，在自定义组件迁移页面中，点按开始 **迁移**。 以下内容已迁移：

      * 为自适应表单编写的自定义组件
      * 组件叠加（如果有）。
   * 要迁移自适应表单模板，请点 **按自适应表单模板迁移** ，在自定义组件迁移页面中，点按开始 **迁移**。 以下内容已迁移：

      * 使用AEM模板编辑器在/apps或/conf下创建的自适应表单模板。
   * 迁移AEM Forms云配置服务以利用新的上下文感知云服务模式，该模式包括触屏优化UI（在/conf下）。 当您迁移AEM Forms云配置服务时， /etc中的云服务将移至/conf。 如果您没有任何依赖旧路径(/etc)的云服务自定义，建议您在升级到6.5之后立即运行迁移实用程序，并使用云配置触屏UI进行进一步的工作。 如果您有任何现有的云服务自定义，请在升级后的设置中继续使用经典UI，直到自定义更新为与迁移路径(/conf)对齐，然后运行迁移实用程序。
   要迁移 **AEM Forms云服务**（包括以下内容），请点按AEM Forms云配置迁移（云配置迁移独立于AEMFD兼容性包），点按AEM Forms云配置迁移，然后在配置迁移页面，点按 **开始迁移**:

   * 表单数据模型云服务

      * 源路径：/etc/cloudservices/fdm
      * 目标路径：/conf/global/settings/cloudconfigs/fdm
   * Recaptcha

      * 源路径：/etc/cloudservices/recaptcha
      * 目标路径：/conf/global/settings/cloudconfigs/recaptcha
   * Adobe Sign

      * 源路径：/etc/cloudservices/echosign
      * 目标路径：/conf/global/settings/cloudconfigs/echosign
   * Typekit云服务

      * 源路径：/etc/cloudservices/typekit
      * 目标路径：/conf/global/settings/cloudconfigs/typekit
   迁移过程进行时，浏览器窗口将显示以下内容：

   * 更新资产时：资产已成功更新。
   * 完成迁移后：已完成资源迁移。
   执行迁移实用程序后，将执行以下操作：

   * **向资产中添加标记**:添加标签“Correponce Management:迁移的资产”/“自适应表单：迁移的资产”。 到迁移的资产，以便用户能够识别迁移的资产。 运行迁移实用程序时，系统中的所有现有资产都标记为已迁移。
   * **生成标记**:以前系统中存在的类别和子类别将创建为标记，然后这些标记将与AEM中的相关Correponce Management资产相关联。 例如，字母模板的类别（索赔）和子类别（索赔）将生成为标记。

















1. 迁移实用程序完成运行后，继续执行家务 [任务](#housekeepingtasks)。

### 运行迁移实用程序后的家务任务 {#housekeepingtasks}

运行迁移实用程序后，请处理以下家务任务： [](../../forms/using/import-export-forms-templates.md)

1. 确保XFA版的布局和片段布局为3.3或更高版本。 如果您使用旧版本的布局和片段布局，则在呈现字母时可能会出现问题。 要将旧版XFA的版本更新至最新版本，请完成以下步骤：

   1. [从Forms用户界面下载XFA](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) （zip文件）。
   1. 解压缩文件。
   1. 在最新的Designer中打开XFA文件并保存它。 XFA的版本将更新为最新版本。
   1. 在表单用户界面中上传XFA。

1. 在迁移之前发布之前在以前的系统中发布的所有资产。 迁移实用程序仅更新作者实例上的资产，并更新发布实例上的资产，这些资产是您发布资产所需的。
1. 在AEM Forms 6.4和6.5中，更改了表单用户组的某些权限。 如果您希望任何用户能够上传包含脚本的XDP和自适应表单或使用代码编辑器，则需要将它们添加到表单功能强大的用户组。 同样，模板作者也无法再使用规则编辑器中的代码编辑器。 为使用户能够使用代码编辑器，请将它们添加到af-template-script-writers组。 有关将用户添加到用户组的说明，请参阅 [管理用户和用户组](/help/communities/users.md)。

