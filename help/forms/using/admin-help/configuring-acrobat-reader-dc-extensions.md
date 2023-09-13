---
title: 为数据捕获配置Acrobat Reader DC扩展
description: 了解如何配置Acrobat Reader DC扩展以进行数据捕获。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 1%

---

# 为数据捕获配置Acrobat Reader DC扩展 {#configuring-acrobat-reader-dc-extensions-for-data-capture}

如果AEM Forms安装的用户使用Content Services的数据捕获功能（已弃用），则建议为这些用户创建具有只读访问权限的角色。

***注意&#x200B;**：Adobe®LiveCycle®内容服务ES（已弃用）是随LiveCycle一起安装的内容管理系统。 它使用户能够设计、管理、监控和优化以人为中心的流程。 Content Services（已弃用）支持于2014年12月31日终止。 请参阅 [Adobe产品生命周期文档](https://helpx.adobe.com/cn/support/programs/eol-matrix.html).*

数据捕获要求您分配用户角色以访问SampleReaderExtensionsCredential。 您可以分配标准的信任管理员角色。 但是，请考虑一下，此角色赋予了常规的非管理用户管理员权限，这些权限可控制PKI信任设置并管理PKI凭据，这可能会危及在生产环境中安装AEM表单的安全性。 建议AEM Forms系统管理员创建一个仅授予信任存储区只读访问权限的角色，并将此新角色分配给使用数据捕获的非管理员用户。

## 为数据捕获用户创建角色 {#create-a-role-for-data-capture-users}

1. 在管理控制台中，单击设置>用户管理>角色管理，然后单击新建角色。
1. 在相应的字段中输入角色名称（例如，数据捕获用户）和说明，然后单击下一步。
1. 在“角色权限”屏幕上，单击“查找权限”，然后从可用权限列表中选择“凭据读取”。
1. 单击“确定”，然后单击“完成”。

## 分配数据捕获角色 {#assign-the-data-capture-role}

1. 在管理控制台中，单击设置>用户管理>角色管理，然后单击查找。
1. 单击您创建的数据捕获用户角色。
1. 在“角色用户/组”选项卡上，单击“查找用户/组”。
1. 在查找用户和组屏幕上，单击查找，选择需要数据捕获用户角色的用户，然后单击确定。
1. 在“编辑角色”屏幕上，单击“保存”。
