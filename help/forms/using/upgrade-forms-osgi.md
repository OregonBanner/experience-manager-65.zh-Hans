---
title: 升级到AEM 6.5 Forms
seo-title: 升级到AEM 6.5 Forms
description: 您可以从AEM 6.1 Forms、AEM 6.2 Forms和LiveCycle ES4 SP1直接升级到AEM 6.3 Forms。
seo-description: 您可以从AEM 6.1 Forms、AEM 6.2 Forms和LiveCycle ES4 SP1直接升级到AEM 6.3 Forms。
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# 在OSGi上升级到AEM 6.5 Forms {#upgrade-to-aem-forms-osgi}

您可以从AEM 6.3 Forms或AEM 6.4 Forms直接升级到AEM 6.5 Forms。

无法从AEM 6. **0 Forms、AEM 6.1 Forms****和AEM 6.2 Forms直接升级到AEM** 6.5 Forms。 执行到 [AEM 6.2 Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html)、 [升级到AEM 6.3 Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html)、 [升级到AEM 6.4 Forms](/help/forms/using/upgrade.md) ，然后从AEM 6.3 Forms或AEM 6.4 Forms升级到AEM 6.5 Forms。

请执行以下操作，从AEM 6.3 Forms或AEM 6.4 Forms升级到AEM 6.5 Forms:

1. 将现有AEM实例升级到AEM 6.5。以下步骤列出：

   1. 安装AEM 6.3 Forms或AEM 6.4 Forms的最新Service Pack和修补程序。 有关详细信息，请 [参阅AEM维护中心](https://helpx.adobe.com/cn/experience-manager/aem-releases-updates.html)。
   1. 准备源实例以进行升级。 有关详细步骤，请 [参阅升级到AEM 6.5](/help/sites-deploying/upgrade.md)。
   1. 下载 [AEM 6.5快速入门](/help/sites-deploying/deploy.md#getting%20the%20software)。
   1. **(仅限基于Unix/Linux的安装** )如果您使用UNIX或Linux作为基础操作系统，请打开终端窗口，导览至包含crx-quickstart的文件夹，然后运行以下命令：

      `chmod -R 755 ../crx-quickstart`

   1. 将AEM实例升级到AEM 6.3。有关分步说明，请参 [阅升级到AEM 6.5](/help/sites-deploying/upgrade.md)。

      在继续执行后续步骤之前，请等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止显示在&lt;crx-repository>/error.log文件中。

      >[!NOTE]
      >
      >服务器启动并运行后，一些AEM Forms包仍处于安装状态。 每个安装的捆绑包数量可能不同。 您可以安全地忽略这些包的状态。 这些包列在https://&#39;[server]:[port]&#39;/system/console/中。

1. 安装AEM Forms加载项包。 这些步骤如下所示：

   1. 开放 [软件分发](https://experience.adobe.com/downloads)。 您需要Adobe ID登录软件分发。
   1. 点按 **[!UICONTROL 标题]** 菜单中可用的Adobe Experience Manager。
   1. 在过滤器 **[!UICONTROL 部分]** :
      1. 从“ **[!UICONTROL 解决方]** 案 **[!UICONTROL ”下]** 拉列表中选择“表单”。
      1. 选择包的版本和类型。 您还可以使用“搜 **[!UICONTROL 索下载]** ”选项筛选结果。
   1. 点按适用于您的操作系统的包名称，选择“ **[!UICONTROL 接受EULA条款]**”，然后点 **[!UICONTROL 按下载]**。
   1. 打开 [包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) ，然后单 **[!UICONTROL 击“上传包]** ”以上传包。
   1. Select the package and click **[!UICONTROL Install]**.

      您还可以使用AEM Forms版本文章中列出的直接链接 [下载包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) 。

      >[!NOTE]
      >
      >安装包后，系统会提示您重新启动AEM实例。 **不要立即停止服务器。** 在停止AEM Forms服务器之前，请等到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止显示在&lt;crx-repository>/error.log文件中，并且日志是稳定的。 另请注意，一些包可以保持安装状态。 您可以安全地忽略这些包的状态。

1. 重新启动AEM实例。

1. 执行安装后活动。

   * **运行迁移实用程序**

      迁移实用程序使早期版本的自适应表单和对应管理资产与AEM 6.5表单兼容。 您可以从AEM软件分发下载该实用程序。 有关配置和使用迁移实用程序的分步信息，请参阅迁 [移实用程序](../../forms/using/migration-utility.md)。

      如果您使用示 [例将草稿和提交组件与查询库集成](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) ，并从先前版本升级，则在执行升级后运行以下SQL:

      ```
      UPDATE metadata m, additionalmetadatatable am
      SET m.dataType = am.value
      WHERE m.id = am.id
      AND am.key = 'dataType'
      ```

      ```
      DELETE from additionalmetadatatable
      WHERE `key` = 'dataType'
      ```

   * **（如果仅从AEM 6.2表单或先前版本升级）重新配置Adobe Sign**

      如果您在AEM Forms的先前版本中配置了Adobe Sign，请从AEM cloud services重新配置Adobe Sign。 有关详细信息，请参 [阅将Adobe Sign与AEM Forms集成](../../forms/using/adobe-sign-integration-adaptive-forms.md)。

   * **支持jQuery**

      在AEM 6.5表单中，jQuery的版本将更新为3.2.1，而jQuery UI版本将更新为1.12.1。AEM表单在无冲突模式下 **使用** JQuery。 因此，如果您使用任何其他jQuery版本，则在执行升级时不会显示任何问题。 但是，升级到AEM 6.5 Forms时：

      * 确保自定义组件（如果有）与支持的jQuery版本兼容。
      * 从自定义组件中删除不支持的API。 请参 [阅升级指南](https://jquery.com/upgrade-guide/3.0/) ，了解删除的API的列表。 例如，删除了对load()、 .unload()和。error()API的支持。 使用。on()方法代替前面提到的API。 例如，将$(&quot;img&quot;)。load(fn)更改为$(&quot;img&quot;)。on(&quot;load&quot;, fn)。
   * **（如果仅从AEM 6.2表单或先前版本升级）重新配置分析和报告**

      在AEM 6.4 Forms中，不提供源的流量变量和印象的成功事件。 因此，当您从AEM 6.2 Forms或先前版本升级时，AEM Forms将停止向AdobeAnalytics服务器发送数据，并且自适应表单的分析报告不可用。 此外，AEM 6.4 Forms还为表单分析版本引入了流量变量，并为在字段上花费的时间引入了成功事件。 因此，请为您的AEM Forms环境重新配置分析和报告。 有关详细步骤，请参 [阅配置分析和报告](../../forms/using/configure-analytics-forms-documents.md)。


1. 验证服务器是否升级成功，所有数据是否也成功迁移，并且它可以正常运行。

   * **验证捆绑包的状态：** 确保所有捆绑包都处于活动状态。
   * **验证复制和反向复制：** 发布、填写和提交几个迁移的表单。 同时验证提交的数据。
   * **验证对管理员和开发人员用户界面的访问权限：** 从管理员帐户登录到AEM实例，并验证您是否有权访问以下URL:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   在AEM 6.4 Forms中，crx-repository的结构已更改。 如果从6.3 Forms升级到AEM 6.5 Forms，请使用您重新创建的更改的路径进行自定义。 有关更改路径的完整列表，请参 [阅AEM中的Forms Repository Restruct](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)。

