---
title: 为IBM Content Manager配置Connector
seo-title: 为IBM Content Manager配置Connector
description: 配置Connector for IBM Content Manager以启用AEM Forms与IBM Content Manager之间的通信。
seo-description: 配置Connector for IBM Content Manager以启用AEM Forms与IBM Content Manager之间的通信。
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 为IBM Content Manager配置Connector{#configuring-connector-for-ibm-content-manager}

IBM Content Manager的Connector支持AEM Forms与IBM Content manager之间的通信。 有关其他背景信息，请参阅服务参考中的“ECM [连接器”](https://www.adobe.com/go/learn_aemforms_services_63)。

## 配置IBM Content Manager连接 {#configure-the-ibm-content-manager-connection}

1. 在管理控制台中，单击“服务”>“Connector for IBM Content Manager”。
1. 在“Datastore Name”（数据存储名称）框中，输入要连接到的IBM Content manager数据存储的名称。 如果数据库是本地的，请输入数据库的名称。 如果数据库是远程数据库，请输入其别名。
1. 在“用户名”框中，输入将连接到IBM Content Manager数据存储库的用户ID。
1. 在“口令”框中，输入用户的口令。
1. （可选）在“别名连接字符串”框中，输入其他连接参数。 在大多数情况下，此框应为空。 有关其他信息，请参阅您的IBM文档。
1. 单击保存。

## 服务设置的验证 {#validation-of-service-settings}

如果输入的dataStore别名、用户名或密码不正确，则根据IBM Content Manager服务的Content Repository Connector当前是否正在运行，您将获得以下结果：

* 如果服务停止，则在保存服务配置信息时，不会显示错误。 但是，下次启动服务时，将引发异常，且服务将不启动。
* 如果服务已启动，则在保存服务配置信息时，服务将尝试立即验证凭据信息。 在这种情况下，会发生错误，并且不会保存配置信息。

