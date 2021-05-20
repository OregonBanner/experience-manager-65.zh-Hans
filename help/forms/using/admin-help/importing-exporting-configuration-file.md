---
title: 导入和导出配置文件
seo-title: 导入和导出配置文件
description: 了解如何导入和导出配置文件，以编辑服务器首选项或配置其他AEM表单产品实例。
seo-description: 了解如何导入和导出配置文件，以编辑服务器首选项或配置其他AEM表单产品实例。
uuid: 32e8a709-2d7c-4740-9533-d53aa751bc58
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c1636537-f7dc-48d8-a3f0-9052bcd28b62
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# 导入和导出配置文件{#importing-and-exporting-the-configuration-file}

使用“手动配置”页可下载XML格式的配置设置副本。 此文件中的设置控制所有服务器首选项。 然后，您可以编辑文件并将其上传回服务器。 您还可以使用文件配置其他AEM表单产品实例。

为了避免安全风险，目录服务器的绑定密码值未包含在导出的配置文件中。 在将文件导入新系统之前，请更新XML文件中的密码。

>[!NOTE]
>
>导入配置文件会根据文件中的信息重新配置AEM表单。 只有系统管理员或熟悉AEM表单产品和XML的专业服务顾问才应考虑修改配置文件。 例如，他们可能需要编辑配置文件才能重新配置损坏的设置。

**导出配置信息**

1. 在管理控制台中，单击设置>用户管理>配置>导入和导出配置文件。
1. 单击导出。 如果您使用的是Microsoft Internet Explorer，系统会提示您指定保存文件的位置。 如果您使用的是Firefox，则文件会保存在您的桌面上。

**导入配置信息**

1. 在管理控制台中，单击设置>用户管理>配置>导入和导出配置文件。
1. 单击“浏览”(Browse)查找配置文件，单击“导入”(Import)，然后单击“确定”(OK)。
