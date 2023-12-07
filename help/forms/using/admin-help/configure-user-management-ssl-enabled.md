---
title: 为启用了SSL的LDAP服务器配置用户管理
description: 了解如何为启用了SSL的LDAP服务器配置用户管理，以使同步能够通过LDAPS正常工作。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 为启用了SSL的LDAP服务器配置用户管理 {#configure-user-management-for-an-ssl-enabled-ldap-server}

要使同步通过LDAPS正常工作，应用程序服务器的Java运行时环境(JRE)中必须存在证书颁发机构(CA)颁发的LDAP证书。 将证书导入应用服务器的JRE cacerts文件，该文件通常位于 *[JAVA_HOME]*/jre/lib/security/cacerts目录。

1. 在目录服务器上启用SSL。 有关详细信息，请参阅目录供应商提供的文档。
1. 从目录服务器导出客户端证书。
1. 使用keytool程序将客户端证书文件导入AEM forms应用程序服务器的默认Java虚拟机(JVM™)证书存储中。 此任务的过程因您的JVM和客户端安装路径而异。 例如，如果将BEA WebLogic Server与JDK 1.5一起使用，请在命令提示符下键入以下文本：

   `keytool -import -alias`*别名* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. 出现提示时，键入密码。 (对于Java，默认密码为 `changeit`.) 将显示一条消息，说明已成功导入证书。
1. 出现提示时，键入 `Yes` 以信任证书。
1. 在“用户管理”中启用SSL，并在配置目录设置时，为SSL选项选择“是”，然后相应地更改端口设置。 默认端口号为636。

>[!NOTE]
>
>如果您在使用SSL时遇到任何问题，请使用LDAP浏览器检查在使用SSL时它是否可以访问LDAP系统。 如果LDAP浏览器无法获得访问权限，则表示您的证书或应用程序服务器配置不正确。 如果LDAP浏览器工作正常，并且您仍然遇到问题，则用户管理配置不正确。
