---
title: 配置SSL概述
seo-title: 配置SSL概述
description: 了解如何通过配置SSL来增强通信的安全性。
seo-description: 了解如何通过配置SSL来增强通信的安全性。
uuid: 3e99d2bf-137b-45ba-8384-309624094623
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e107abb-861f-4063-b600-c87e34639019
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 配置SSL {#overview-of-configuring-ssl}概述

您可以创建安全套接字层(SSL)凭据，并在应用程序服务器上配置SSL以增强与应用程序服务器通信的安全性。

作为安全产品，Rights Management需要配置SSL。 配置SSL证书时，请确保仅使用RSA密钥。 不支持包含DSA密钥的SSL证书。

提供的信息适用于统包、自动和手动安装。 它提供了配置SSL的方法的示例。 您还可以使用更适合您的网络或组织的其他方法。

>[!NOTE]
>
>建议您完成AEM表单模块的安装、配置和部署，并确保在应用程序服务器上配置SSL之前，产品正常运行。

>[!NOTE]
>
>创建SSL安全证书和凭据时，请使用与运行应用程序服务器时相同的用户帐户权限。 如果应用程序服务器是使用其他用户权限运行的，则当ContentRootURI指向https时，该表单可能无法正确呈现PDFForm呈现版本。

如果您有启用SSL的LDAP服务器，请配置“用户管理”以使用该服务器。 （请参阅[为启用SSL的LDAP服务器配置用户管理](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)。）
