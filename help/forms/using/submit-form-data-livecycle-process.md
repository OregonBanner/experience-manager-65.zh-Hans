---
title: 配置AEM Forms以在JEE流程中向AEM Forms提交表单数据
seo-title: 配置AEM Forms以在JEE流程中向AEM Forms提交表单数据
description: AEM Forms允许您将自适应表单与AEM Forms在JEE流程上集成，以处理表单数据。
seo-description: AEM Forms允许您将自适应表单与AEM Forms在JEE流程上集成，以处理表单数据。
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
role: 管理员
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---


# 配置AEM Forms以在JEE进程{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}上向AEM Forms提交表单数据

自适应表单支持向AEM Forms on JEE流程提交数据以进一步处理。 它允许您使用提交表单中提供的数据触发JEE流程上的AEM Forms。 请执行以下步骤，使您的AEM Forms实例能够在JEE流程中向AEM Forms提交自适应表单：

## 配置AEM Forms服务器{#configure-your-aem-forms-server}

请执行以下步骤，使您的AEM表单服务器能够向JEE服务器上的AEM Forms提交数据：

1. 转到AEM Web配置控制台，网址为：https://[*host*]:[*port*]/system/console/configMgr。

1. 找到并单击&#x200B;**Adobe LiveCycle客户端SDK配置**&#x200B;组件。
1. 单击可编辑JEE服务器上AEM Forms的配置服务器URL、用户名和密码。
1. 查看设置并单击&#x200B;**保存**。

![Adobe LiveCycle客户端SDK配置](assets/clientsdkconfiguration.jpg)

## 用进程字段{#map-data-with-process-fields}映射数据

配置AEM Forms后，将数据XML和附件从提交的表单映射到AEM Forms on JEE进程中的字段。 要执行此操作：

1. 在AEM Web配置控制台中，单击以编辑&#x200B;**指南LiveCycle流程定位器和调用器**&#x200B;配置。
1. 指定以下参数：

   * **数据xml参数的名称** （必填）：指定JEE进程上需要处理提交数据的AEM Forms的XML属性文件。默认值为&#x200B;**dataxml**。

   * **文件附件参数的名称** （可选）：指定JEE上的AEM Forms进程需要处理的文档对象的列表。默认值为&#x200B;**fileAttachmentsList**。

1. 查看设置并单击&#x200B;**保存**。

![指南LiveCycle流程定位器和发票人](assets/test3.jpg)

配置完毕后，“提交到Forms Workflow”提交操作将列表AEM Forms在JEE服务器进程上，该进程包含指定的data xml参数。
