---
title: 迁移AEM Forms资产和文档
seo-title: 迁移AEM Forms资产和文档
description: 迁移实用程序允许您将AEM Forms资产和文档从AEM 6.3Forms或先前版本迁移到AEM 6.4Forms。
seo-description: 迁移实用程序允许您将AEM Forms资产和文档从AEM 6.3Forms或先前版本迁移到AEM 6.4Forms。
uuid: a3fdf940-7fc2-441c-91c8-ad66ba47e5f2
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
discoiquuid: 39dfef85-d047-4b6d-a0f5-92bd77df103b
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1809'
ht-degree: 2%

---


# 迁移AEM Forms资产和文档{#migrate-aem-forms-assets-and-documents}

迁移实用程序将 [Adaptive](../../forms/using/introduction-forms-authoring.md)Forms资 [产、云配置](/help/sites-developing/extending-cloud-config.md)、Corresponce Management资产从早 [](/help/forms/using/cm-overview.md) 期版本中使用的格式转换为AEM 6.5 Forms中使用的格式。 运行迁移实用程序时，将迁移以下内容：

* 自适应表单的自定义组件
* 自适应表单和通信管理模板
* 云配置
* 通信管理和自适应表单资产

>[!NOTE]
>
>如果升级不当，对于Corresponce Management资产，您可以在每次导入资产时运行迁移。 对于通信管理迁移，您需要安装Forms兼容性包。

## 迁移方法 {#approach-to-migration}

您可 [以从](../../forms/using/upgrade.md) “AEM Forms” 6.4、6.3或6.2升级到最新版本的AEM Forms6.5，或执行全新安装。 根据您是升级了之前的安装还是执行了新安装，您需要执行下列操作之一：

**如果是就地升级**

如果您执行了就地升级，则升级实例已包含资产和文档。 但是，在使用资源和文档之前，您需要安装AEMFD [兼容性包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) （包括Corresponce Management兼容性包）

然后，您需要通过运行迁移实用程序来 [更新资产和文档](#runningmigrationutility)。

**如果安装不当**

如果安装不当（新安装），则在您使用资源和文档之前，您需要安装 [AEMFD兼容性包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) （包括Corresponsement Management Compatibility包）。

然后，您需要在新设置上导入您的资产包（zip或cmp），然后运行迁移实用程 [序更新资产和文档](#runningmigrationutility)。 Adobe建议仅在运行迁移实用程序后在新设置上创建新资产。

由于向 [后兼容性相关更改](/help/sites-deploying/backward-compatibility.md) ,crx-repository中几个文件夹的位置会发生更改。 手动将依赖项（自定义库和资源）从以前的设置导出并导入到新环境。

## 在继续迁移前阅读 {#prerequisites}

对于通信管理资产：

* 对于从前一个平台导入的资产，将添加一个属性： **fd:version=1.0**。
* 自AEM 6.1Forms以来，注释不会开箱即用。 以前添加的注释可在资产中使用，但不会自动在界面上显示。 您需要在AEM Forms用户界面中自定义extendedProperties属性，以使注释可见。
* 在LiveCycleES4等早期版本中，文本使用FlexRichTextEditor进行编辑，但自AEM 6.1Forms以来，使用HTML编辑器。 由于字体的呈现和外观、字体大小和字体边距可能与作者用户界面中的先前版本不同。 但是，这些字母在呈现时看起来是一样的。
* 文本模块中的列表得到了改进，现在呈现方式有所不同。 可能存在视觉差异。 我们建议您渲染并查看在文本模块中使用列表的字母。
* 由于图像内容模块已转换为DAM资产，并且布局和片段在迁移过程中会添加到表单，因此这些模块的“更新者”属性会更改为管理员。
* 资产的版本历史记录不会进行迁移，且在迁移后不可用。 后续版本历史记录迁移后将被保留。
* 自AEM 6.1Forms以来，“准备发布”状态已弃用，因此“准备发布”状态中的所有资源都将更改为“已修改”状态。
* 由于用户界面在AEM Forms6.3中进行了更新，因此执行自定义的步骤也有所不同。 如果您是从6.3之前的版本迁移，则需要重做自定义。
* 布局片段从/content/apps/cm/layouts/fragmentlayouts/1001移至/content/apps/cm/modules/fragmentlayouts。 资产中的数据字典引用显示数据字典的路径而不是其名称。
* 需要重新调整文本模块中用于对齐的任何制表符空格。 有关详细信息，请参 [阅对应管理——使用制表符间距排列文本](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html)。
* 资产书写器配置会更改为对应管理配置。
* 资产会移动到文件夹下，其名称包括“现有文本”和“现有列表”。

## 使用迁移实用程序 {#using-the-migration-utility}

### 运行迁移实用程序 {#runningmigrationutility}

在对资产进行任何更改或创建资产之前，请运行迁移实用程序。 我们建议您在进行任何更改或创建资源后不要运行该实用程序。 确保在迁移过程运行时，“对应管理”或“自适应Forms资产”用户界面未打开。

首次运行迁移实用程序时，将使用以下路径和名称创建日志：\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log。 此日志不断更新，包括通信管理和自适应Forms迁移信息，如资产移动。

>[!NOTE]
>
>运行迁移实用程序之前，请确保已备份crx存储库。

1. 在浏览器会话中，以管理员身份登录到AEM作者实例。

1. 在浏览器中打开以下URL:

   https://[*hostname*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   浏览器显示四个选项：

   * AEM Forms 资产迁移
   * 自适应Forms自定义组件迁移
   * 自适应Forms模板迁移
   * AEM Forms 云配置迁移

1. 执行以下操作以执行迁移：

   * 要迁移 **资产**，请点按AEM Forms资产迁移，然后在下一个屏幕中，点按 **开始迁移**。 迁移以下内容：

      * 自适应表单
      * 文档片段
      * 主题
      * 书信
      * 数据字典

   >[!NOTE]
   >
   >在资产迁移过程中，您会找到警告消息，如“找到冲突……”。 这些消息表示无法迁移自适应表单中某些组件的规则。 例如，如果组件具有同时具有规则和脚本的事件，则在任何脚本之后都会发生规则，则不迁移组件的任何规则。 但是，可以通过在自适应表单创作中打开规则编辑器来迁移此类规则。
   >
   >
   >通过在自适应Forms编辑器的规则编辑器中打开这些组件，可以迁移这些组件。
   >
   >
   >
   >    * 要在自定义组件中迁移规则和脚本（从6.3升级时不需要），请点按自适应Forms自定义组件迁移，在下一个屏幕中，点按开始迁移。 迁移以下内容：   >
      >
      >
      >        

      * 使用规则编辑器（6.1 FP1及更高版本）创建的规则和脚本
      >        * 使用6.1及更早版本UI中的“脚本”选项卡创建的脚本
   >
   >
   >    * 要迁移模板（从6.3和6.4升级时不需要），请点按自适应Forms模板迁移，在下一个屏幕中，点按开始迁移。 迁移以下内容：

      >
      >
      >
      >        


      * 旧模板——使用AEM 6.1Forms或更早版本在/apps下创建的自适应表单模板。 这包括在模板组件中定义的脚本。
      >        * 新模板——使用/conf下的模板编辑器创建的自适应表单模板。 这包括迁移使用规则编辑器创建的规则和脚本。


   * 要迁移自适应表单自定义组件，请点 **按自适应Forms自定义组件迁移** ，在自定义组件迁移页面中，点 **按开始迁移**。 迁移以下内容：

      * 为自适应Forms编写的自定义组件
      * 组件叠加（如果有）。
   * 要迁移自适应表单模板，请点 **按自适应Forms模板迁移** ，在“自定义组件迁移”页面，点按 **开始迁移**。 迁移以下内容：

      * 使用AEM模板编辑器在/apps或/conf下创建的自适应表单模板。
   * 迁移AEM Forms云配置服务以利用新的上下文感知云服务模式，该模式包括触屏优化UI（在/conf下）。 当您迁移AEM Forms云配置服务时，/etc中的云服务将移至/conf。 如果您没有任何依赖旧路径(/etc)的云服务自定义，建议您在升级到6.5后立即运行迁移实用程序，并使用云配置触屏UI进行进一步的工作。 如果您有任何现有的云服务自定义，请在已升级的设置上继续使用经典UI，直到自定义更新为与迁移路径(/conf)一致，然后运行迁移实用程序。

   要迁移 **AEM Forms云服务**（包括以下内容），请点按AEM Forms云配置迁移（云配置迁移独立于AEMFD兼容性包），点按AEM Forms云配置迁移，然后在配置迁移页，点按 **开始迁移**:

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

   * 资产更新时：资产已成功更新。
   * 迁移完成后：已完成资产迁移。

   执行迁移实用程序后，将执行以下操作：

   * **向资产中添加标记**:添加标签“Corresponce Management:迁移资产”/“自适应Forms:迁移资产”。 到迁移的资产，以便用户能够识别迁移的资产。 运行迁移实用程序时，系统中的所有现有资产都标记为已迁移。
   * **生成标记**:以前系统中存在的类别和子类别将创建为标记，然后这些标记与AEM中的相关对应管理资产相关联。 例如，字母模板的类别（声明）和子类别（声明）会生成为标记。

















1. 迁移实用程序完成运行后，继续执行家 [务任务](#housekeepingtasks)。

### 运行迁移实用程序后的管理任务 {#housekeepingtasks}

运行迁移实用程序后，请注意以下家政任务: [](../../forms/using/import-export-forms-templates.md)

1. 确保XFA版本的布局和片段布局为3.3或更高版本。 如果您使用旧版本的布局和片段布局，则呈现该字母时可能会出现问题。 要将旧XFA的版本更新到最新版本，请完成以下步骤：

   1. [从Forms用户界面下载](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) XFA作为zip文件。
   1. 解压文件。
   1. 在最新的设计器中打开XFA文件并保存它。 XFA的版本将更新为最新版本。
   1. 在Forms用户界面中上传XFA。

1. 在迁移之前发布之前在先前系统中发布的所有资产。 迁移实用程序仅更新作者实例上的资产，并更新发布实例上需要发布资产的资产。
1. 在AEM Forms6.4和6.5中，表单用户组的某些权利已更改。 如果希望任何用户能够上传包含脚本的XDP和自适应Forms，或使用代码编辑器，您需要将它们添加到表单功能用户组。 同样，模板作者无法再在规则编辑器中使用代码编辑器。 为使用户能够使用代码编辑器，请将他们添加到 af-template-script-writers 组。有关将用户添加到组的说明，请参 [阅管理用户和用户组](/help/communities/users.md)。

