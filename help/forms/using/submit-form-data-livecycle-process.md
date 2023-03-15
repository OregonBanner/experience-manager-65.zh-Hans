---
title: 配置AEM Forms以将表单数据提交到AEM Forms on JEE流程
seo-title: Configuring AEM Forms to submit form data to an AEM Forms on JEE process
description: AEM Forms允许您将自适应表单与AEM Forms on JEE流程集成以处理表单数据。
seo-description: AEM Forms allows you to integrate adaptive forms with AEM Forms on JEE processes for processing form data.
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
source-wordcount: '326'
ht-degree: 0%

---

# 配置AEM Forms以将表单数据提交到AEM Forms on JEE流程{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

自适应表单支持将数据提交到AEM Forms on JEE流程以进行进一步处理。 它允许您使用已提交表单中可用的数据触发AEM Forms on JEE流程。 执行以下步骤，使您的AEM Forms实例能够在JEE流程中向AEM Forms提交自适应表单：

## 配置AEM Forms服务器 {#configure-your-aem-forms-server}

执行以下步骤，使您的AEM表单服务器能够将数据提交到JEE服务器上的AEM Forms：

1. 转到AEM Web配置控制台，网址为https://[*主机*]：[*端口*]/system/console/configMgr.

1. 找到并单击 **AdobeLiveCycle客户端SDK配置** 组件。
1. 单击以编辑JEE服务器上AEM Forms的配置服务器URL、用户名和密码。
1. 查看设置并单击 **保存**.

![AdobeLiveCycle客户端SDK配置](assets/clientsdkconfiguration.jpg)

## 使用流程字段映射数据 {#map-data-with-process-fields}

配置AEM Forms后，将提交表单中的数据XML和附件映射到AEM Forms on JEE流程中的字段。 要执行此操作：

1. 在AEM Web配置控制台中，单击以编辑 **指导LiveCycle流程定位器和调用程序** 配置。
1. 指定以下参数：

   * **数据xml参数的名称** （必需）：指定需要处理提交的数据的AEM Forms on JEE进程的XML属性文件。 默认值为 **数据XML**.

   * **文件附件参数的名称** （可选）：指定AEM Forms on JEE进程需要处理的文档对象列表。 默认值为 **文件附件列表**.

1. 查看设置并单击 **保存**.

![指导LiveCycle流程定位器和调用程序](assets/test3.jpg)

配置完毕后，提交到Forms Workflow提交操作会列出包含指定数据xml参数的JEE服务器进程上的AEM Forms。
