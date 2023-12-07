---
title: 在Windows Vista上配置SSL
description: 了解如何在Windows Vista上配置SSL。 使用并运行Java Keytool生成包含RSA密钥的SSL证书以进行身份验证。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 在Windows Vista上配置SSL {#configuring-ssl-on-windows-vista}

要在Windows Vista™上配置SSL，您需要具有RSA密钥的SSL证书以进行身份验证。 可以使用Java keytool创建证书。

>[!NOTE]
>
>Windows Vista不能使用DSA密钥。

您可以使用包含创建证书和密钥库所需的所有信息的单个命令来运行keytool。

**创建SSL证书**

1. 在命令提示符下，导航至 *`[JAVA HOME]`*/bin ，然后键入以下命令以创建证书和密钥库：

   `keytool -genkey -keyalg RSA -dname "CN=`*主机名* `, OU=`*组名称* `, O=`*公司名称* `,L=`*城市名称* `, S=`*状态* `, C=`*国家/地区代码* `" -alias`*“LC证书”* `-keypass` `key`*_* *密码* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >替换 *`[JAVA_HOME]`替换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。*

1. 类型 `changeit` 作为密码。 此密码是Java安装的默认密码，系统管理员可能已更改此密码。
