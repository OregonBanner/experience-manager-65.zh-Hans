---
title: 配置AEM Forms以将数据提交到AEM Forms on JEE流程
description: 将自适应表单与AEM Forms on JEE流程集成以处理表单数据。
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
role: Admin
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 在JEE流程中配置AEM Forms以将表单数据提交到AEM表单{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

自适应表单支持将数据提交到AEM Forms on JEE流程以进行进一步处理。 它允许您使用已提交表单中可用的数据触发AEM Forms on JEE流程。 执行以下步骤，以便您可以启用AEM Forms实例将自适应表单提交到AEM Forms on JEE流程：

## 配置AEM Forms服务器 {#configure-your-aem-forms-server}

执行以下步骤，以便您可以启用AEM Forms服务器将数据提交到JEE服务器上的AEM Forms：

1. 转到AEM Web配置控制台，网址为https://[*主机*]：[*端口*]/system/console/configMgr.

1. 找到并单击 **AdobeLiveCycle客户端SDK配置** 组件。
1. 单击以编辑JEE服务器上AEM Forms的配置服务器URL、用户名和密码。
1. 查看设置并单击 **保存**.

![AdobeLiveCycle客户端SDK配置](assets/clientsdkconfiguration.jpg)

## 使用流程字段映射数据 {#map-data-with-process-fields}

配置AEM Forms后，将提交表单中的数据XML和附件映射到AEM Forms on JEE流程中的字段。 执行以下操作：

1. 在AEM Web配置控制台中，单击以编辑 **指导LiveCycle流程定位器和调用程序** 配置。
1. 指定以下参数：

   * **数据xml参数的名称** （必需）：指定必须处理提交数据的AEM Forms on JEE进程的XML属性文件。 默认值为 **数据XML**.

   * **文件附件参数的名称** （可选）：指定AEM Forms on JEE进程必须处理的文档对象列表。 默认值为 **文件附件列表**.

1. 查看设置并单击 **保存**.

![指导LiveCycle流程定位器和调用程序](assets/test3.jpg)

配置完毕后，提交到Forms Workflow提交操作会列出包含指定数据xml参数的JEE服务器进程上的AEM Forms。
