---
title: 管理HSM凭据
seo-title: Managing HSM credentials
description: 了解如何管理HSM凭证。
seo-description: Learn how to manage HSM credentials.
uuid: 30ddcd4a-f771-44d5-bdef-4826adcd0c44
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5f17ba8-8aab-4449-811a-20ad33de1c6f
exl-id: facbeab2-de95-4778-894c-faa771d3391e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 0%

---

# 管理HSM凭据 {#managing-hsm-credentials}

在“信任存储区管理”页面中，您可以管理Hardware Security Module (HSM)凭据。 HSM是第三方PKCS#11设备，可用于安全地生成和存储私钥。 HSM在物理上保护对私钥的访问和使用。

需要客户端软件与HSM通信。 HSM客户端软件必须安装在AEM Forms所在的计算机上。

AEM forms Digital Signatures可以使用HSM中存储的凭据来应用服务器端数字签名。 按照本节中的说明为Digital Signatures将使用的每个HSM凭据创建别名。 别名包含HSM所需的所有参数。

>[!NOTE]
>
>更改HSM配置后，重新启动AEM Forms服务器。

## 当HSM设备联机时，为HSM凭据创建别名 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“HSM凭据”，然后单击“添加”。
1. 在“配置文件名称”框中，键入用于标识别名的字符串。 此值用作某些数字签名操作（如“签名字段”操作）的属性。
1. 在“PKCS11库”框中，键入服务器上的HSM客户端库的完全限定路径。 例如， `c:\Program Files\LunaSA\cryptoki.dll`. 在群集环境中，此路径对于群集中的所有服务器必须相同。
1. 单击“测试HSM连通性”。 如果AEM Forms能够连接到HSM设备，则会显示一条消息，说明HSM可用。 单击下一步。
1. 使用“令牌名称”、“插槽ID”或“插槽列表索引”来标识凭据在HSM上的存储位置。

   * **令牌名称：** 对应于要使用的HSM分区的名称（例如HSMPART1）。
   * **插槽ID：** 插槽ID是数据类型为long的插槽标识符。
   * **插槽列表索引：** 如果选择“槽列表索引”，请将“槽信息”设置为与槽相对应的整数。 这是一个基于0的索引，这意味着如果客户端首先在HSMPART1分区中注册，则使用SlotListIndex值0引用HSMPART1。

1. 在“Token Pin（令牌固定）”框中，键入访问HSM密钥所需的密码，然后单击“Next（下一步）”。
1. 在“凭据”框中，选择一个凭据。 单击“保存”。

## 在HSM设备脱机时为HSM凭据创建别名 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“HSM凭据”，然后单击“添加”。
1. 在“配置文件名称”框中，键入用于标识别名的字符串。 此值用作某些数字签名操作（如“签名字段”操作）的属性。
1. 在“PKCS11库”框中，键入服务器上的HSM客户端库的完全限定路径。 例如， `c:\Program Files\LunaSA\cryptoki.dll`. 在群集环境中，此路径对于群集中的所有服务器必须相同。
1. 选中脱机配置文件创建复选框。 单击下一步。
1. 在HSM设备列表中，选择存储凭据的HSM设备的制造商。
1. 在“插槽类型”列表中，选择“插槽Id”、“插槽索引”或“令牌名称”，然后在“插槽信息”框中指定一个值。 AEM forms使用这些设置来确定凭据在HSM上的存储位置。

   * **令牌名称：** 对应于分区名称（例如HSMPART1）。
   * **插槽ID：** 插槽ID是与插槽对应的整数，而插槽ID又与分区相对应。 例如，客户端（表单服务器）首先在HSMPART1分区中注册。 对于此客户端，此函数将插槽1映射到HSMPART1分区。 由于HSMPART1是第一个注册的分区，因此插槽ID为1，而您应将“插槽信息”设置为1。

      插槽ID是逐个客户端设置的。 如果您将另一台计算机注册到不同的分区（例如，同一HSM设备上的HSMPART2），则插槽1将与该客户端的HSMPART2分区相关联。

   * **插槽索引：** 如果选择“槽索引”，请将“槽信息”设置为与槽相对应的整数。 这是一个基于0的索引，这意味着如果客户端首先在HSMPART1分区中注册，则插槽1将映射到该客户端的HSMPART1。 由于HSMPART1是第一个注册的分区，因此插槽索引为0。

1. 选择以下选项之一并提供路径：

   * **证书**：（如果使用SHA1，则不需要）单击浏览并找到要使用的凭据的公共密钥的路径。
   * **证书SHA1：** （使用物理证书时不需要）为正在使用的凭据键入公钥(.cer)文件的SHA1值（指纹）。 确保SHA1值中没有使用空格。

1. 在“密码”框中，键入访问给定插槽信息的HSM密钥所需的密码，然后单击保存。

## 查看HSM凭据别名属性 {#view-hsm-credential-alias-properties}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“HSM凭据”。
1. 单击凭据别名的别名以查看属性，然后单击确定。

## 检查HSM凭据的状态 {#check-the-status-of-an-hsm-credential}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“HSM凭据”。
1. 单击要检查的凭据旁边的复选框，然后单击检查状态。

状态列反映凭据的当前状态。 如果发生故障，“状态”列中会显示一个红色的X。 将鼠标悬停在X上可显示包含失败原因的工具提示。

## 更新HSM凭据别名属性 {#update-hsm-credential-alias-properties}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“HSM凭据”。
1. 单击凭据别名的别名。
1. 单击更新凭据，并根据需要更新设置。

## 重置所有HSM连接 {#reset-all-hsm-connections}

在表单服务器与HSM设备之间的网络会话出现任何中断后，重置与HSM设备的开放连接。 例如，由于网络中断或HSM设备因软件更新而脱机，可能会发生中断。 中断后，现有连接已过时，针对这些连接的任何签名请求都将失败。 使用“重置所有HSM连接”选项可清除旧连接。

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“HSM凭据”。
1. 单击“重置所有HSM连接”。

## 删除HSM凭据别名 {#delete-an-hsm-credential-alias}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“HSM凭据”。
1. 选中要删除的HSM凭据的复选框，单击“删除”，然后单击“确定”。

## 配置远程HSM {#configure-remote-hsm-support}

AEM forms使用基于Web服务的IPC/RPC机制。 此机制使AEM表单能够使用安装在远程计算机上的HSM。 要使用此功能，请在安装了HSM的远程计算机上安装Web服务。 参见 [在Windows 64位平台上使用Sun JDK配置AEM Forms ES的HSM支持](https://kb2.adobe.com/cps/808/cpsid_80835.html)了解更多信息。

此机制不支持在线创建HSM配置文件或状态检查。 但是，可通过两种方式创建HSM配置文件和执行状态检查：

* 通过传递签名者证书来创建AEM Forms客户端凭据。 请按照中的步骤操作 [在Windows 64位平台上使用Sun JDK配置AEM Forms ES的HSM支持](https://kb2.adobe.com/cps/808/cpsid_80835.html). Web服务位置作为Credential属性传入。 还支持使用证书或证书SHA-1十六进制创建离线HSM配置文件。 但是，如果您已从早期版本的AEM表单升级到AEM表单，则进行客户端更改，因为凭据包含证书和Web服务信息。
* Web服务位置在Signature服务的管理控制台中指定。 (请参阅 [签名服务设置](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings).) 在此，客户端仅将HSM配置文件的别名放在信任存储区中。 即使您从早期版本的AEM表单升级到AEM表单，也可以无缝地使用此选项，而无需进行任何客户端更改。 此选项不支持使用证书SHA-1的HSM配置文件。
