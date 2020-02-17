---
title: 配置Acrobat Reader DC扩展以获取数据
seo-title: 配置Acrobat Reader DC扩展以获取数据
description: 了解如何配置Acrobat Reader DC扩展以进行数据捕获。
seo-description: 了解如何配置Acrobat Reader DC扩展以进行数据捕获。
uuid: af6b3c72-601e-4f54-8343-a323eeee5906
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8f8367fe-a8e9-46ee-a980-1633be02932d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置Acrobat Reader DC扩展以获取数据 {#configuring-acrobat-reader-dc-extensions-for-data-capture}

如果AEM表单安装的用户使用Content services的数据捕获功能（已弃用），则建议您为这些用户创建具有只读访问权限的角色。

***注意&#x200B;**:Adobe® LiveCycle® Content Services ES（已弃用）是随LiveCycle一起安装的内容管理系统。 它使用户能够设计、管理、监控和优化以人为中心的流程。 内容服务（已弃用）支持将于2014年12月31日结束。 请参阅[Adobe产品生命周期文档](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)。 要了解有关配置Content Services（已弃用）的信息，请参阅[管理Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf)。*

数据捕获要求您分配用户角色以访问SampleReaderExtensionsCredential。 您可以分配标准的“信任管理员”角色，但请考虑，此角色为一般的非管理用户授予了强大的管理员权限，这些权限用于控制PKI信任设置和管理PKI凭据，这可能会危及在生产环境中安装AEM表单的安全性。 建议AEM表单系统管理员创建一个仅授予对信任存储区的只读访问权限的角色，并将此新角色分配给使用数据捕获的非管理员用户。

## 为数据捕获用户创建角色 {#create-a-role-for-data-capture-users}

1. 在管理控制台中，单击设置>用户管理>角色管理，然后单击新建角色。
1. 在相应的字段中输入角色名称（例如，“数据捕获用户”）和说明，然后单击“下一步”。
1. 在“角色权限”屏幕上，单击“查找权限”，然后从可用权限列表中选择“凭据读取”。
1. 单击“确定”，然后单击“完成”。

## 分配数据捕获角色 {#assign-the-data-capture-role}

1. 在管理控制台中，单击设置>用户管理>角色管理，然后单击查找。
1. 单击您创建的数据捕获用户角色。
1. 在“角色用户／用户组”选项卡上，单击“查找用户／用户组”。
1. 在“查找用户和用户组”屏幕上，单击“查找”，选择需要数据捕获用户角色的用户，然后单击“确定”。
1. 在“编辑角色”屏幕上，单击“保存”。

