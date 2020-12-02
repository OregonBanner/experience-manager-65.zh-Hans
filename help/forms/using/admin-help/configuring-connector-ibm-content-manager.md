---
title: 为IBM Content Manager配置连接器
seo-title: 为IBM Content Manager配置连接器
description: 配置Connector for IBM Content Manager，以实现AEM表单与IBM Content Manager之间的通信。
seo-description: 配置Connector for IBM Content Manager，以实现AEM表单与IBM Content Manager之间的通信。
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# 为IBM Content Manager配置连接器{#configuring-connector-for-ibm-content-manager}

IBM Content Manager的Connector支持AEM表单与IBM Content Manager之间的通信。 有关其他背景信息，请参阅[服务参考](https://www.adobe.com/go/learn_aemforms_services_63)中的“Connectors for ECM”。

## 配置IBM Content Manager连接{#configure-the-ibm-content-manager-connection}

1. 在管理控制台中，单击“服务”>“IBM Content Manager的连接器”。
1. 在“Datastore Name”（数据存储名称）框中，输入要连接的IBM Content Manager数据存储的名称。 如果数据库是本地的，请输入数据库的名称。 如果数据库是远程数据库，请输入其别名。
1. 在“用户名”框中，输入将连接到IBM Content Manager数据存储库的用户ID。
1. 在“口令”框中，输入用户的口令。
1. （可选）在“别名连接字符串”框中，输入其他连接参数。 在大多数情况下，此框应为空。 有关其他信息，请参阅您的IBM文档。
1. 单击保存。

## 服务设置{#validation-of-service-settings}的验证

如果输入了不正确的dataStore别名、用户名或密码，您将获得以下结果，具体取决于IBM Content Manager服务的Content Repository Connector当前是否正在运行：

* 如果服务停止，则在保存服务配置信息时，不会显示错误。 但是，下次开始服务时，将引发异常，服务将不开始。
* 如果服务已启动，则在保存服务配置信息时，服务将尝试立即验证凭据信息。 在这种情况下，将发生错误，并且不保存配置信息。

