---
title: 管理HSM凭据
seo-title: 管理HSM凭据
description: 了解如何管理HSM凭据。
seo-description: 了解如何管理HSM凭据。
uuid: 30ddcd4a-f771-44d5-bdef-4826adcd0c44
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5f17ba8-8aab-4449-811a-20ad33de1c6f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 管理HSM凭据 {#managing-hsm-credentials}

从“信任存储管理”页面，可以管理硬件安全模块(HSM)凭据。 HSM是第三方PKCS#11设备，可用于安全地生成和存储私钥。 HSM以物理方式保护对私钥的访问和使用。

需要客户端软件才能与HSM通信。 HSM客户端软件必须与AEM表单安装并配置在同一台计算机上。

AEM表单数字签名可以使用存储在HSM上的凭据应用服务器端数字签名。 按照本节中的说明为数字签名将使用的每个HSM凭证创建别名。 别名包含HSM所需的所有参数。

>[!NOTE]
>
>更改HSM配置后，重新启动AEM表单服务器。

## 在HSM设备联机时为HSM凭证创建别名 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. 在管理控制台中，单击“设置”>“信任存储管理”>“HSM凭据”，然后单击“添加”。
1. 在“配置文件名称”框中，键入用于标识别名的字符串。 此值用作某些“数字签名”操作（如“签名字段”操作）的属性。
1. 在“PKCS11库”框中，在服务器上键入HSM客户端库的完全限定路径。 For example, `c:\Program Files\LunaSA\cryptoki.dll`. 在群集环境中，此路径必须对群集中的所有服务器都相同。
1. 单击“测试HSM连接”。 如果AEM表单能够连接到HSM设备，将显示一条消息，指明HSM可用。 单击下一步。
1. 使用令牌名称、插槽ID或插槽列表索引来标识凭据在HSM上的存储位置。

   * **** 令牌名称：与要使用的HSM分区的名称（例如，HSMPART1）相对应。
   * **** 插槽ID:插槽ID是数据类型长的插槽标识符。
   * **** 插槽列表索引：如果选择“插槽列表索引”，请将“插槽信息”设置为与插槽对应的整数。 这是一个从0开始的索引，这意味着如果客户端首先注册到HSMPART1分区，则使用SlotListIndex值0将引用HSMPART1。

1. 在“令牌管脚”框中，键入访问HSM密钥所需的口令，然后单击“下一步”。
1. 在“凭据”框中，选择凭据。 单击保存。

## 在HSM设备脱机时为HSM凭证创建别名 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. 在管理控制台中，单击“设置”>“信任存储管理”>“HSM凭据”，然后单击“添加”。
1. 在“配置文件名称”框中，键入用于标识别名的字符串。 此值用作某些“数字签名”操作（如“签名字段”操作）的属性。
1. 在“PKCS11库”框中，在服务器上键入HSM客户端库的完全限定路径。 For example, `c:\Program Files\LunaSA\cryptoki.dll`. 在群集环境中，此路径必须对群集中的所有服务器都相同。
1. 选中“脱机创建配置文件”复选框。 单击下一步。
1. 在“HSM设备”列表中，选择存储凭据的HSM设备的制造商。
1. 在“插槽类型”列表中，选择“插槽ID”、“插槽索引”或“令牌名称”，然后在“插槽信息”框中指定一个值。 AEM表单使用这些设置确定凭据在HSM上的存储位置。

   * **** 令牌名称：与分区名称（例如，HSMPART1）对应。
   * **** 插槽ID:插槽ID是与插槽对应的整数，插槽ID又与分区对应。 例如，首先注册HSMPART1分区的客户端（表单服务器）。 这会将此客户端的插槽1映射到HSMPART1分区。 由于HSMPART1是注册的第一个分区，因此插槽ID为1，您应将插槽信息设置为1。

      插槽ID是逐个客户端设置的。 如果您向另一个分区注册了另一台计算机（例如，同一HSM设备上的HSMPART2），那么插槽1将与该客户端的HSMPART2分区相关联。

   * **** 插槽索引：如果选择“插槽索引”，请将“插槽信息”设置为与插槽对应的整数。 这是一个基于0的索引，这意味着如果客户端首先注册到HSMPART1分区，则插槽1将映射到此客户端的HSMPART1。 由于HSMPART1是已注册的第一个分区，因此插槽索引为0。

1. 选择以下选项之一并提供路径：

   * **证书**:（使用SHA1时不需要）单击“浏览”并找到您所使用的凭证的公钥路径。
   * **** 证书SHA1:（如果使用物理证书，则不需要）为您所使用的凭证键入公钥(.cer)文件的SHA1值（指纹）。 确保SHA1值中不使用空格。

1. 在“密码”框中，键入访问给定插槽信息的HSM密钥所需的密码，然后单击“保存”。

## 查看HSM凭据别名属性 {#view-hsm-credential-alias-properties}

1. 在管理控制台中，单击“设置”>“信任存储管理”>“HSM凭据”。
1. 单击凭据别名的别名以查看属性，然后单击确定。

## 检查HSM凭证的状态 {#check-the-status-of-an-hsm-credential}

1. 在管理控制台中，单击“设置”>“信任存储管理”>“HSM凭据”。
1. 单击要检查的凭证旁边的复选框，然后单击检查状态。

“状态”列反映凭据的当前状态。 如果失败，“状态”列中将显示红色的X。 将鼠标悬停在X上可显示包含失败原因的工具提示。

## 更新HSM凭据别名属性 {#update-hsm-credential-alias-properties}

1. 在管理控制台中，单击“设置”>“信任存储管理”>“HSM凭据”。
1. 单击凭据别名的别名。
1. 单击“更新凭据”，然后根据需要更新设置。

## 重置所有HSM连接 {#reset-all-hsm-connections}

在表单服务器和HSM设备之间的网络会话中断后，重置到HSM设备的打开连接。 例如，由于网络中断或HSM设备离线进行软件更新，可能会发生中断。 中断后，现有连接会失效，并且针对这些连接的任何签名请求都会失败。 使用“重置所有HSM连接”选项可清除旧连接。

1. 在管理控制台中，单击“设置”>“信任存储管理”>“HSM凭据”。
1. 单击“重置所有HSM连接”。

## 删除HSM凭据别名 {#delete-an-hsm-credential-alias}

1. 在管理控制台中，单击“设置”>“信任存储管理”>“HSM凭据”。
1. 选中要删除的HSM凭据对应的复选框，单击删除，然后单击确定。

## 配置远程HSM支持 {#configure-remote-hsm-support}

AEM表单使用基于Web服务的IPC/RPC机制。 此机制使AEM表单能使用安装在远程计算机上的HSM。 要使用此功能，请在安装HSM的远程计算机上安装Web服务。 有关 [详细信息，请参阅在Windows 64位平台上使用Sun JDK配置AEM表单ES的HSM](https://kb2.adobe.com/cps/808/cpsid_80835.html)支持。

此机制不支持在线创建HSM配置文件或状态检查。 但是，有两种方法可创建HSM配置文件并执行状态检查：

* 通过传递签名者的证书，创建AEM表单客户端凭据。 按照在Windows 64位平 [台上使用Sun JDK配置AEM表单ES的HSM支持中的步骤操作](https://kb2.adobe.com/cps/808/cpsid_80835.html)。 Web服务位置作为“凭证”属性传入。 还支持使用证书编号或证书SHA-1十六进制创建脱机HSM配置文件。 但是，如果您已从AEM表单的早期版本升级到AEM表单，请更改客户端，因为凭据包含证书和Web服务信息。
* Web服务位置在签名服务的管理控制台中指定。 (请参阅 [签名服务设置](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings)。)此处，客户端仅在信任存储中携带HSM配置文件的别名。 即使您已从AEM表单的早期版本升级到AEM表单，也可以无缝地使用此选项，而不会对客户端进行任何更改。 此选项不支持使用证书SHA-1的HSM配置文件。

