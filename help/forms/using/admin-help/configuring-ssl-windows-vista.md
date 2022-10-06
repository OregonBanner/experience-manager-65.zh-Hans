---
title: 在Windows Vista上配置SSL
seo-title: Configuring SSL on Windows Vista
description: 了解如何在Windows Vista上配置SSL。
seo-description: Learn how to configure SSL on Windows Vista.
uuid: 20bfcefb-ec84-4c55-bceb-6af106d883d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 667645a0-53d0-4f9b-a0ba-cc7e366a23a1
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 在Windows Vista上配置SSL {#configuring-ssl-on-windows-vista}

要在Windows Vista™上配置SSL，您需要一个包含RSA密钥的SSL证书进行身份验证。 您可以使用Java密钥工具创建证书。

>[!NOTE]
>
>Windows Vista无法与DSA密钥配合使用。

您可以使用包含创建证书和密钥库所需的所有信息的单个命令来运行密钥工具。

**创建SSL证书**

1. 在命令提示符下，导航到 *`[JAVA HOME]`*/bin并键入以下命令以创建证书和密钥库：

   `keytool -genkey -keyalg RSA -dname "CN=`*主机名* `, OU=`*群组名称* `, O=`*公司名称* `,L=`*城市名称* `, S=`*州* `, C=`*国家/地区代码* `" -alias`*&quot;LC证书&quot;* `-keypass` `key`*_* *密码* `-keystore`*密钥重命名* `.keystore`

   >[!NOTE]
   >
   >替换 *`[JAVA_HOME]`使用安装JDK的目录，并将斜体文本替换为与您的环境对应的值。*

1. 类型 `changeit` 作为密码。 此密码是Java安装的默认密码，系统管理员可能已更改此密码。
