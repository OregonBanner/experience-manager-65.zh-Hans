---
title: 导入和导出配置文件
seo-title: Importing and exporting the configuration file
description: 了解如何导入和导出配置文件，以编辑服务器首选项或配置其他AEM Forms产品实例。
seo-description: Learn how to import and export the configuration file in order to edit server preferences or configure another AEM forms product instance.
uuid: 32e8a709-2d7c-4740-9533-d53aa751bc58
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c1636537-f7dc-48d8-a3f0-9052bcd28b62
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 导入和导出配置文件 {#importing-and-exporting-the-configuration-file}

使用“手动配置”页可以以XML格式下载配置设置的副本。 此文件中的设置控制所有服务器首选项。 然后，您可以编辑该文件并将其上传回服务器。 您还可以使用该文件配置另一个AEM Forms产品实例。

为避免安全风险，导出的配置文件中不包含目录服务器的绑定密码值。 在将文件导入新系统之前，请更新XML文件中的密码。

>[!NOTE]
>
>导入配置文件会根据文件中的信息重新配置AEM表单。 只有熟悉AEM Forms产品和XML的系统管理员或专业服务顾问才应考虑修改配置文件。 他们可能需要编辑配置文件，例如，重新配置损坏的设置。

**导出配置信息**

1. 在Administration Console中，单击Settings > User Management > Configuration > Import and Export Configuration Files。
1. 单击“导出”。 如果您使用的是Microsoft Internet Explorer，系统会提示您指定保存文件的位置。 如果您使用的是Firefox，则文件会保存在您的桌面上。

**导入配置信息**

1. 在Administration Console中，单击Settings > User Management > Configuration > Import and Export Configuration Files。
1. 单击“浏览”查找配置文件，单击“导入”，然后单击“确定”。
