---
title: 导入和导出配置文件
description: 了解如何导入和导出配置文件以编辑服务器首选项或配置其他AEM Forms产品实例。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 导入和导出配置文件 {#importing-and-exporting-the-configuration-file}

使用“手动配置”页可以以XML格式下载配置设置的副本。 此文件中的设置控制所有服务器首选项。 然后，您可以编辑该文件并将其上传回服务器。 您还可以使用文件配置另一个AEM Forms产品实例。

为避免安全风险，导出的配置文件中不包含目录服务器的绑定密码值。 在将文件导入到新系统之前，请更新XML文件中的密码。

>[!NOTE]
>
>导入配置文件会根据文件中的信息重新配置AEM表单。 只有熟悉AEM Forms产品和XML的系统管理员或专业服务顾问才应考虑修改配置文件。 用户可能需要编辑配置文件，例如，重新配置损坏的设置。

**导出配置信息**

1. 在Administration Console中，单击Settings > User Management > Configuration > Import and Export Configuration Files。
1. 单击“导出”。 如果您使用的是Microsoft Internet Explorer，系统会提示您指定保存文件的位置。 如果您使用的是Firefox，则文件会保存在您的桌面上。

**导入配置信息**

1. 在Administration Console中，单击Settings > User Management > Configuration > Import and Export Configuration Files。
1. 单击“浏览”查找配置文件，单击“导入”，然后单击“确定”。
