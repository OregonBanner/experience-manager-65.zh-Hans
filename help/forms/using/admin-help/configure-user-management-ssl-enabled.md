---
title: 为启用SSL的LDAP服务器配置用户管理
seo-title: 为启用SSL的LDAP服务器配置用户管理
description: 了解如何为启用SSL的LDAP服务器配置用户管理，以使同步能够通过LDAPS正常工作。
seo-description: 了解如何为启用SSL的LDAP服务器配置用户管理，以使同步能够通过LDAPS正常工作。
uuid: 4b3f8ac7-fa38-4adf-a851-82d55fe431fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e6e7e2fa-579d-4b36-8598-6ced469a94b1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 为启用SSL的LDAP服务器配置用户管理 {#configure-user-management-for-an-ssl-enabled-ldap-server}

要使同步在LDAPS上正常工作，证书颁发机构(CA)颁发的LDAP证书必须存在于应用程序服务器的Java运行时环境(JRE)中。 将证书导入应用程序服务器的JRE cacerts文件，该文件通常位于 *[JAVA_HOME]*/jre/lib/security/cacerts目录中。

1. 在目录服务器上启用SSL。 有关详细信息，请参阅目录供应商提供的文档。
1. 从目录服务器导出客户端证书。
1. 使用keytool程序将客户端证书文件导入AEM表单应用程序服务器的默认Java虚拟机(JVM™)证书存储区。 根据JVM和客户端安装路径，此任务的过程会有所不同。 例如，如果将BEA webLogic server与JDK 1.5一起使用，请在命令提示符下键入以下文本：

   `keytool -import -alias`*alias *`-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. 出现提示时，键入密码。 (对于Java，默认密码为 `changeit`。)将显示一条消息，指明证书已成功导入。
1. 出现提示时，键 `Yes` 入以信任证书。
1. 在“用户管理”中启用SSL，在配置目录设置时，为SSL选项选择“是”并相应地更改端口设置。 默认端口号为636。

>[!NOTE]
>
>如果使用SSL时遇到任何问题，请使用LDAP浏览器检查它在使用SSL时是否可以访问LDAP系统。 如果LDAP浏览器无法访问，则您的证书或应用程序服务器配置不正确。 如果LDAP浏览器正常工作，并且您仍然遇到问题，则用户管理配置不正确。

