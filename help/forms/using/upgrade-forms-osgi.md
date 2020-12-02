---
title: 升级到AEM 6.5Forms
seo-title: 升级到AEM 6.5Forms
description: 您可以从AEM 6.1Forms、AEM 6.2Forms和LiveCycleES4 SP1直接升级到6.3Forms。
seo-description: 您可以从AEM 6.1Forms、AEM 6.2Forms和LiveCycleES4 SP1直接升级到6.3Forms。
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# 升级到OSGi上的AEM 6.5Forms{#upgrade-to-aem-forms-osgi}

您可以从AEM 6.3Forms或AEM 6.4Forms直接升级到AEM 6.5Forms。

不提供从&#x200B;**AEM 6.0Forms、AEM 6.1Forms**&#x200B;和&#x200B;**AEM 6.2Forms**&#x200B;到AEM 6.5Forms的直接升级途径。 执行中间[升级到AEM 6.2Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html)、[升级到AEM 6.3Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html)或[升级到AEM 6.4Forms](/help/forms/using/upgrade.md)，然后从FormsAEM6.3或AEM6.4Forms升级到AEM6.5Forms。

请执行以下操作，从AEM 6.3Forms或AEM 6.4Forms升级到AEM 6.5Forms:

1. 将现有AEM实例升级到AEM 6.5。以下步骤列出：

   1. 为AEM 6.3Forms或AEM 6.4Forms安装最新的Service Pack和修补程序。 有关详细信息，请参阅[AEM Susement Hub](https://helpx.adobe.com/cn/experience-manager/aem-releases-updates.html)。
   1. 准备源实例以进行升级。 有关详细步骤，请参阅[升级到AEM 6.5](/help/sites-deploying/upgrade.md)。
   1. 下载[AEM 6.5 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software)。
   1. **(仅限基于Unix/Linux的** 安装)如果您使用UNIX或Linux作为基础操作系统，请打开终端窗口，导览至包含crx-quickstart的文件夹，然后运行以下命令：

      `chmod -R 755 ../crx-quickstart`

   1. 将AEM实例升级到AEM 6.3。有关分步说明，请参阅[升级到AEM 6.5](/help/sites-deploying/upgrade.md)。

      在继续执行后续步骤之前，请等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止显示在&lt;crx-repository>/error.log文件中。

      >[!NOTE]
      >
      >服务器启动并运行后，一些AEM Forms捆绑包仍处于安装状态。 每个安装的捆绑包数量可能不同。 您可以安全地忽略这些包的状态。 捆绑包列在https://&#39;[server]:[port]&#39;/system/console/。

1. 安装AEM Forms加载项包。 这些步骤如下所示：

   1. 打开[软件分发](https://experience.adobe.com/downloads)。 您需要Adobe ID才能登录软件分发。
   1. 点按标题菜单中的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
   1. 在&#x200B;**[!UICONTROL 过滤器]**&#x200B;部分中：
      1. 从&#x200B;**[!UICONTROL 解决方案]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Forms]**。
      1. 选择包的版本和类型。 您还可以使用&#x200B;**[!UICONTROL 搜索下载]**&#x200B;选项筛选结果。
   1. 点按适用于您的操作系统的程序包名称，选择&#x200B;**[!UICONTROL 接受EULA条款]**，然后点按&#x200B;**[!UICONTROL 下载]**。
   1. 打开[包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html)并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
   1. 选择软件包，然后单击&#x200B;**[!UICONTROL 安装]**。

      您还可以使用[AEM Forms版本](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)文章中列出的直接链接下载包。

      >[!NOTE]
      >
      >安装包后，系统会提示您重新启动AEM实例。 **不要立即停止服务器。** 在停止AEM Forms服务器之前，请等到/error.log文件中停止显示ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消 &lt;crx-repository>息，并且日志是稳定的。另请注意，一些包可以保持安装状态。 您可以安全地忽略这些包的状态。

1. 重新启动AEM实例。

1. 执行安装后活动。

   * **运行迁移实用程序**

      迁移实用程序使早期版本的自适应表单和对应管理资源与AEM 6.5表单兼容。 您可以从AEM软件分发下载该实用程序。 有关配置和使用迁移实用程序的分步信息，请参阅[迁移实用程序](../../forms/using/migration-utility.md)。

      如果您使用[示例将草稿和提交组件](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html)与数据库集成并从先前版本升级，则在执行升级后运行以下SQL查询:

      ```sql
      UPDATE metadata m, additionalmetadatatable am
      SET m.dataType = am.value
      WHERE m.id = am.id
      AND am.key = 'dataType'
      ```

      ```sql
      DELETE from additionalmetadatatable
      WHERE `key` = 'dataType'
      ```

   * **(如果仅从AEM 6.2Forms或先前版本升级)重新配置Adobe Sign**

      如果您在AEM Forms的先前版本中配置了Adobe Sign，请从AEM云服务中重新配置Adobe Sign。 有关详细信息，请参阅[将Adobe Sign与AEM Forms整合](../../forms/using/adobe-sign-integration-adaptive-forms.md)。

   * **支持jQuery**

      在AEM 6.5Forms,jQuery的版本更新为3.2.1,jQuery UI版本更新为1.12.1。AEM表单在&#x200B;**noConflict**&#x200B;模式下使用JQuery。 因此，如果您使用任何其他jQuery版本，则在执行升级时不会显示任何问题。 但是，升级到AEM 6.5Forms时：

      * 确保自定义组件（如果有）与支持的jQuery版本兼容。
      * 从自定义组件中删除不支持的API。 有关已删除API的列表，请参阅[升级指南](https://jquery.com/upgrade-guide/3.0/)。 例如，删除了对load()、 .unload()和。error()API的支持。 使用。on()方法代替前面提到的API。 例如，将$(&quot;img&quot;)。load(fn)更改为$(&quot;img&quot;)。on(&quot;load&quot;, fn)。
   * **(如果仅从AEM 6.2Forms或先前版本升级)重新配置分析和报告**

      在AEM 6.4Forms，不提供源流量变量和印象成功事件。 因此，从AEM 6.2Forms或先前版本升级后，AEM Forms将停止向Adobe Analytics服务器发送数据，并且不提供自适应表单的分析报告。 此外，AEM 6.4Forms还为表单分析版本引入了流量变量，并为字段所用的时间引入了成功事件。 因此，请重新配置AEM Forms环境的分析和报告。 有关详细步骤，请参阅[配置分析和报告](../../forms/using/configure-analytics-forms-documents.md)。


1. 验证服务器是否升级成功，所有数据是否也成功迁移，并且它可以正常运行。

   * **验证捆绑包的状态：确** 保所有捆绑包都处于活动状态。
   * **验证复制和反向复制：发** 布、填写和提交几个迁移的表单。同时验证提交的数据。
   * **验证对管理员和开发人员用户界面的** 访问权限：从管理员帐户登录到AEM实例，并验证您是否有权访问以下URL:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   在AEM 6.4Forms,crx-repository的结构已更改。 如果从6.3Forms升级到AEM 6.5Forms，请使用您重新创建的更改的自定义路径。 有关更改路径的完整列表，请参阅AEM中的[Forms存储库重组。](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)

