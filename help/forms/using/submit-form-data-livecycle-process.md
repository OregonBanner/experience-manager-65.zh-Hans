---
title: 配置AEM Forms以在JEE流程中将表单数据提交到AEM Forms
seo-title: 配置AEM Forms以在JEE流程中将表单数据提交到AEM Forms
description: AEM Forms允许您在JEE流程中将自适应表单与AEM Forms集成，以处理表单数据。
seo-description: AEM Forms允许您在JEE流程中将自适应表单与AEM Forms集成，以处理表单数据。
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
role: Admin
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 配置AEM Forms以在JEE流程中将表单数据提交到AEM Forms{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

自适应表单支持将数据提交到JEE上的AEM Forms进程，以便进一步处理。 它允许您使用提交的表单中提供的数据，在JEE上触发AEM Forms进程。 请执行以下步骤，使您的AEM Forms实例能够在JEE流程中向AEM Forms提交自适应表单：

## 配置AEM Forms服务器 {#configure-your-aem-forms-server}

请执行以下步骤，使您的AEM表单服务器能够向JEE服务器上的AEM Forms提交数据：

1. 转到位于https://[*host*]&#x200B;的AEM Web配置控制台：[*port*]/system/console/configMgr。

1. 找到并单击&#x200B;**AdobeLiveCycle客户端SDK配置**&#x200B;组件。
1. 单击以编辑JEE服务器上AEM Forms的配置服务器URL、用户名和密码。
1. 查看设置并单击&#x200B;**Save**。

![AdobeLiveCycle客户端SDK配置](assets/clientsdkconfiguration.jpg)

## 使用流程字段映射数据 {#map-data-with-process-fields}

配置AEM Forms后，将数据XML和附件从提交的表单映射到JEE流程中AEM Forms的字段。 要执行此操作：

1. 在AEM Web配置控制台中，单击以编辑&#x200B;**指南LiveCycle流程定位器和调用程序**&#x200B;配置。
1. 指定以下参数：

   * **数据xml参数的名称** （必需）：指定JEE进程中需要处理提交数据的AEM Forms的XML属性文件。默认值为&#x200B;**dataxml**。

   * **文件附件参数的名称** （可选）：指定JEE上的AEM Forms进程需要处理的文档对象列表。默认值为&#x200B;**fileAttachmentsList**。

1. 查看设置并单击&#x200B;**Save**。

![指南LiveCycle流程定位器和发票人](assets/test3.jpg)

配置完毕后，“提交到Forms Workflow”提交操作会列出JEE服务器上包含指定数据xml参数的AEM Forms进程。
