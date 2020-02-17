---
title: 在Windows Vista上配置SSL
seo-title: 在Windows Vista上配置SSL
description: 了解如何在Windows Vista上配置SSL。
seo-description: 了解如何在Windows Vista上配置SSL。
uuid: 20bfcefb-ec84-4c55-bceb-6af106d883d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 667645a0-53d0-4f9b-a0ba-cc7e366a23a1
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# 在Windows Vista上配置SSL {#configuring-ssl-on-windows-vista}

要在Windows Vista™上配置SSL，您需要一个带有RSA密钥的SSL证书以进行身份验证。 可以使用Java密钥工具创建证书。

>[!NOTE]
>
>Windows Vista无法与DSA密钥配合使用。

您可以使用一个命令运行keytool，该命令包含创建证书和密钥库所需的所有信息。

**创建SSL证书**

1. 在命令提示符下，导航到 *`[JAVA HOME]`*/bin并键入以下命令以创建证书和密钥库：

   `keytool -genkey -keyalg RSA -dname "CN=`*Host Group Name Group Name NameState *NameNameState`, OU=`*NameNameStateCountry Contury* &quot;LC Rename Chart Cort&quot;Rename Rename Justate JustationChert，重命名CtRedChert_StSedCt.Ct.SemplySedCt.Ct.Sed `, O=`*SedCt.Ct.Ct.Ct.St.SedCt.SempSt.SeCt.Ly.St.ReSt.ReSt.*Ct.Rempst.`,L=`**`, S=`**`, C=`**`" -alias`**`-keypass``key`****`-keystore`**Ly.CrenStScrCtRempCt Rename`.keystore`

   >[!NOTE]
   >
   >替 *`[JAVA_HOME]`换为安装JDK的目录，并将斜体文本替换为与您的环境相对应的值。*

1. 键 `changeit` 入密码。 此密码是Java安装的默认密码，系统管理员可能已更改了该密码。

