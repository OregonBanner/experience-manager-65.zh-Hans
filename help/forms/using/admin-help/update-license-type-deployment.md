---
title: 更新部署的许可证类型
description: 使用管理控制台中的“更改许可证”页面更新部署的许可证类型。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 更新部署的许可证类型 {#update-the-license-type-for-the-deployment}

在AEM表单安装过程中，您使用Configuration Manager配置和部署所需的AEM表单模块。 默认情况下，这些模块配置有60天的评估版许可证。 使用管理控制台中的“更改许可证”页面可更改部署的许可证类型。 当前部署的模块将显示在“更改许可证”页面上。

“更改许可证”页面显示有关您的许可证的信息：

* 当前许可证类型
* 上次更新许可证的日期和时间
* 上次更新的执行者
* 许可证的当前状态
* AEM表单的安装日期
* 当前许可证到期的日期

>[!NOTE]
>
>许可证更改适用于所有已部署的模块。 在更改许可证类型之前，请取消部署任何未授予许可证的模块。 如果部署的模块列表包含的模块不是您从Adobe购买的模块，请勿选择生产许可证类型。

## 更新许可证类型 {#update-the-license-type}

1. 在管理控制台中，单击“许可”。
1. 阅读AEM Forms最终用户许可协议，选择“I Accept（我接受）”（如果您同意协议条款），然后单击“Next（下一步）”。
1. 在“更改许可证”页面上，选择许可证类型：

   * **估计：** 60天试用许可证
   * **开发：** 永久开发许可证
   * **NFR：** 2年评估许可证
   * **IDEV：** 订购1年Adobe Developer计划
   * **生产：** 永久许可证

1. 选择是，许可证更改对所有已部署的模块有效。
1. 单击Confirm License Change。 出现一条消息，说明许可证已成功更新。
