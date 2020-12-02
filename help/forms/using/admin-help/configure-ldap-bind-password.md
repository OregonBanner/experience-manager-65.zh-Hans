---
title: 配置LDAP绑定口令
seo-title: 配置LDAP绑定口令
description: 了解如何在将配置文件导入另一个系统之前配置绑定密码字段。
seo-description: 了解如何在将配置文件导入另一个系统之前配置绑定密码字段。
uuid: 1ab1907c-8b55-4b6f-bd5b-49f22d78b8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 165b3950-b03f-4848-8361-ffb0a26d2658
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# 配置LDAP绑定口令{#configure-the-ldap-bind-password}

为避免安全风险，未配置导出配置文件(config.xml)中的绑定密码字段。 在将配置文件导入其他系统之前，请确保配置此密码。 此口令将覆盖存储在数据库中的现有口令。 空密码不会覆盖现有的非空密码值。

1. 在管理控制台中，单击“设置”>“用户管理”>“配置”>“导入和导出配置文件”。
1. 要将当前配置设置导出到文件，请单击“导出”，然后将配置文件保存到其他位置。
1. 在文件中，找到`Domains` > *[您的域名]* > `DirectoryConfigs` > `LDAPGroupConfig`节点。 以下是一个示例：

   ```xml
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   键入`bindpassword`的值并保存更改。

1. 在文件中，找到`Domains` > *[您的域名]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig`节点。 以下是一个示例：

   ```xml
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   键入`bindpassword`的值并保存更改。

1. 要导入更新的文件，请在“用户管理”中，单击“配置”>“导入和导出配置文件”。
1. 单击“浏览”以查找文件，单击“导入”，然后单击“确定”。

