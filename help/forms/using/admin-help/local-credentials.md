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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# 管理本地凭据{#managing-local-credentials}

本地凭据是托管在信任存储管理中的私钥凭据。 *本地凭据*&#x200B;标识用户的DES凭据的存储位置。 使用信任存储管理，您可以导入和管理本地凭据，例如，使用现有PFX文件，以便导入、编辑和删除本地凭据。

AEM表单支持标准PKCS12格式（.pfx和。p12文件）中高达4096位的RSA和DSA凭据。

您可以导入和导出任意数量的凭据。 如果要使用相同的别名替换过期的凭据，请删除该凭据，然后使用相同的别名导入新凭据。

有关Acrobat Reader DC扩展的信息和说明，请参阅[配置用于Acrobat Reader DC扩展的凭据](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)。

## 导入凭据{#import-a-credential}

1. 在管理控制台中，单击“设置”>“信任存储管理”>“本地凭据”。
1. 单击导入。在“信任存储类型”下，选择以下选项之一：

   * **文档签名凭** 据：用于在文档上发出数字签名的凭据。
   * **Acrobat Reader DC扩展凭** 据：特定于Acrobat Reader DC扩展的数字证书，它允许在生成的PDF文档中激活Adobe Reader的使用权。
   * **默认：** 指示这是用于Acrobat Reader DC扩展的默认凭据。

   有关获取凭据的信息，请参阅[准备安装AEM表单](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)。

1. 在“别名”框中，键入凭据的标识符。 此标识符用作Acrobat Reader DC扩展和签名服务中凭据的显示名称。 此别名还用于使用AEM forms SDK以编程方式访问凭据。

   >[!NOTE]
   >
   >别名将自动转换为大写以用于显示目的。 在进程中引用别名时，别名不区分大小写。

1. 单击“浏览”以查找凭据，键入凭据的口令，然后单击“确定”。

   如果出现错误消息“由于文件格式不正确或密码不正确而导入凭据失败”，请验证密码是否有效。

## 导出凭据{#export-a-credential}

凭据以PKCS#12格式导出为P12文件。

1. 在管理控制台中，单击“设置”>“信任存储管理”>“本地凭据”。
1. 单击要导出的凭据的别名，然后单击导出。
1. 在“口令”框中，键入口令。 此密码是新密码，用于加密导出的凭据。
1. 单击“Export（导出）” ，按照指示导出凭据，然后单击“OK（确定）”。

## 编辑凭据的别名或信任存储类型{#edit-a-credential-s-alias-or-trust-store-type}

导入凭据后，您可以编辑其别名和信任存储类型。

1. 在管理控制台中，单击“设置”>“信任存储管理”>“本地凭据”。
1. 单击要编辑的凭据的别名。
1. 单击“更新凭据”。
1. 根据需要编辑别名和信任存储类型，然后单击确定。

## 删除凭据{#delete-a-credential}

1. 在管理控制台中，单击“设置”>“信任存储管理”>“本地凭据”。
1. 选中要删除的凭据的复选框。
1. 单击“删除”，然后单击“确定”。

