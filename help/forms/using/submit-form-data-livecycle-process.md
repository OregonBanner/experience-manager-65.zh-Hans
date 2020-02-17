---
title: 将AEM Forms配置为在JEE流程中将表单数据提交到AEM Forms
seo-title: 将AEM Forms配置为在JEE流程中将表单数据提交到AEM Forms
description: AEM Forms允许您将自适应表单与JEE流程中的AEM Forms集成，以处理表单数据。
seo-description: AEM Forms允许您将自适应表单与JEE流程中的AEM Forms集成，以处理表单数据。
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# 将AEM Forms配置为在JEE流程中将表单数据提交到AEM Forms{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

自适应表单支持将数据提交到JEE上的AEM表单进行进一步处理。 它允许您使用提交的表单中提供的数据触发JEE上的AEM表单进程。 执行以下步骤，使您的AEM Forms实例能够将自适应表单提交到JEE流程中的AEM Forms:

## 配置AEM Forms服务器 {#configure-your-aem-forms-server}

执行以下步骤，使AEM表单服务器能够将数据提交到JEE服务器上的AEM表单：

1. 转到AEM web配置控制台&#x200B;[*https://*]:[*port*]/system/console/configMgr。

1. 找到并单击 **Adobe LiveCycle Client SDK配置组件** 。
1. 单击可编辑JEE服务器上AEM Forms的配置服务器URL、用户名和密码。
1. 查看设置，然后单击“ **保存”**。

![Adobe LiveCycle Client SDK配置](assets/clientsdkconfiguration.jpg)

## 用进程字段映射数据 {#map-data-with-process-fields}

配置AEM表单后，将提交表单中的数据XML和附件映射到JEE流程中AEM表单的字段。 要执行此操作：

1. 在AEM web配置控制台中，单击以编辑指南LiveCycle **Process Locator和Invoker配置** 。
1. 指定以下参数：

   * **data xml参数的名称** （必填）:指定JEE进程中需要处理提交数据的AEM Forms的XML属性文件。 The default value is **dataxml**.

   * **文件附件参数的名称** （可选）:指定JEE上的AEM Forms进程需要处理的文档对象列表。 The default value is **fileAttachmentsList**.

1. 查看设置，然后单击“ **保存”**。

![指南LiveCycle Process Locator和Invoker](assets/test3.jpg)

配置完毕后，“提交到表单工作流”提交操作会列出JEE服务器进程中包含指定数据xml参数的AEM Forms。
