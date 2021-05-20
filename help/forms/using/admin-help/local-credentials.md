---
title: 管理本地凭据
seo-title: 管理本地凭据
description: 了解如何管理本地凭据。
seo-description: 了解如何管理本地凭据。
uuid: 3c4358e0-aaff-4e94-a6b2-04b463fca260
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 598a9a03-3773-4620-8867-1f754d8ca031
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---

# 管理本地凭据{#managing-local-credentials}

本地凭据是托管在信任存储管理中的私钥凭据。 *本地凭据*&#x200B;标识用户的DES凭据的存储位置。 使用信任存储管理，您可以通过使用（例如）现有PFX文件来导入和管理本地凭据，以便导入、编辑和删除本地凭据。

AEM Forms支持标准PKCS12格式（.pfx和.p12文件）中的RSA和DSA凭据，长达4096位。

您可以导入和导出任意数量的凭据。 如果要使用相同的别名替换已过期的凭据，请删除凭据，然后使用相同的别名导入新凭据。

有关Acrobat Reader DC扩展的信息和说明，请参阅[配置凭据以与Acrobat Reader DC扩展一起使用](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)。

## 导入凭据{#import-a-credential}

1. 在管理控制台中，单击设置>信任存储管理>本地凭据。
1. 单击导入。在信任存储类型下，选择以下选项之一：

   * **文档签名凭据：** 用于在文档上发出数字签名的凭据。
   * **Acrobat Reader DC扩展凭据：** 特定于Acrobat Reader DC扩展的数字证书，用于在生成的PDF文档中激活Adobe Reader使用权限。
   * **默认：** 表示这是用于Acrobat Reader DC扩展的默认凭据。

   有关获取凭据的信息，请参阅[准备安装AEM表单](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)。

1. 在“别名”框中，键入凭据的标识符。 此标识符用作Acrobat Reader DC扩展和签名服务中凭据的显示名称。 此别名还用于使用AEM Forms SDK以编程方式访问凭据。

   >[!NOTE]
   >
   >出于显示目的，别名会自动转换为大写。 在流程中引用别名时，别名不区分大小写。

1. 单击浏览以找到凭据，键入凭据的密码，然后单击确定。

   如果出现错误消息“由于文件格式不正确或密码不正确而导入凭据失败”，请验证密码是否有效。

## 导出凭据{#export-a-credential}

凭据以PKCS#12格式导出为P12文件。

1. 在管理控制台中，单击设置>信任存储管理>本地凭据。
1. 单击要导出的凭据的别名，然后单击“导出”。
1. 在“密码”框中，键入密码。 此密码是新密码，用于加密导出的凭据。
1. 单击导出，按照说明导出凭据，然后单击确定。

## 编辑凭据的别名或信任存储类型{#edit-a-credential-s-alias-or-trust-store-type}

导入凭据后，您可以编辑其别名和信任存储类型。

1. 在管理控制台中，单击设置>信任存储管理>本地凭据。
1. 单击要编辑的凭据的别名。
1. 单击“更新凭据”。
1. 根据需要编辑别名和信任存储类型，然后单击“确定”。

## 删除凭据{#delete-a-credential}

1. 在管理控制台中，单击设置>信任存储管理>本地凭据。
1. 选中要删除的凭据的复选框。
1. 单击删除，然后单击确定。
