---
title: 配置SSL的概述
seo-title: 配置SSL的概述
description: 了解如何通过配置SSL来增强通信的安全性。
seo-description: 了解如何通过配置SSL来增强通信的安全性。
uuid: 3e99d2bf-137b-45ba-8384-309624094623
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e107abb-861f-4063-b600-c87e34639019
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置SSL的概述 {#overview-of-configuring-ssl}

您可以创建安全套接字层(SSL)凭据，并在应用程序服务器上配置SSL以增强与应用程序服务器通信的安全性。

作为安全产品，Rights Management需要配置SSL。 配置SSL证书时，请确保仅使用RSA密钥。 不支持带DSA密钥的SSL证书。

提供的信息适用于统包、自动和手动安装。 它提供了配置SSL的方法的示例。 您还可以使用其他更适合您的网络或组织的方法。

>[!NOTE]
>
>建议您完成AEM表单模块的安装、配置和部署，并确保在应用程序服务器上配置SSL之前产品正确运行。

>[!NOTE]
>
>创建SSL安全证书和凭据时，请使用与运行应用程序服务器时相同的用户帐户权限。 如果应用程序服务器是使用其他用户权限运行的，则当ContentRootURI指向https时，表单可能无法正确呈现PDFForm再现。

如果您有启用了SSL的LDAP服务器，请配置“用户管理”以使用它。 (请参 [阅为启用SSL的LDAP服务器配置用户管理](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)。)
