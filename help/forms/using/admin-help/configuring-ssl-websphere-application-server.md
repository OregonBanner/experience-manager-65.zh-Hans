---
title: 为WebSphere应用程序服务器配置SSL
description: 了解如何为WebSphere应用程序服务器配置SSL。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b0786b52-879e-4a24-9cc9-bd9dcb2473cc
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 1%

---

# 为WebSphere应用程序服务器配置SSL {#configuring-ssl-for-websphere-application-server}

此部分包含使用IBM WebSphere应用程序服务器配置SSL的以下步骤。

## 在WebSphere中创建本地用户帐户 {#creating-a-local-user-account-on-websphere}

要启用SSL，WebSphere需要访问本地操作系统用户注册表中具有管理系统管理权限的用户帐户：

* (Windows)创建一个Windows用户，该用户是管理员组的成员，并且有权作为操作系统的一部分进行操作。 (请参阅 [为WebSphere创建Windows用户](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).)
* (Linux、UNIX)用户可以是超级用户或具有超级用户权限的其他用户。 在WebSphere上启用SSL时，请使用此用户的服务器标识和密码。

### 为WebSphere创建Linux或UNIX用户 {#create-a-linux-or-unix-user-for-websphere}

1. 以根用户登录。
1. 在命令提示符下输入以下命令，以创建用户：

   * （Linux 和 Sun Solaris） `useradd`
   * （IBM AIX） `mkuser`

1. 通过在命令提示符中输入 `passwd` ，设置新用户的密码。
1. （Linux 和 Solaris）通过在命令提示符中输入 `pwconv` （无参数）来创建阴影密码文件。

   >[!NOTE]
   >
   >（Linux和Solaris）要使WebSphere Application Server本地OS安全注册表正常工作，必须存在卷影密码文件。 影子密码文件通常命名 **为/etc/shadow** ，基于/etc/passwd 文件。 如果影子密码文件不存在，则启用全局安全性并将用户注册表配置为本地操作系统后会出现错误。

1. 在文本编辑者中，从/etc 目录打开群组文件。
1. 将您在步骤2中创建的用户添加到 `root` 群组中。
1. 保存并关闭该文件。
1. （启用SSL的UNIX）以root用户身份启动和停止WebSphere。

### 为WebSphere创建Windows用户 {#create-a-windows-user-for-websphere}

1. 使用管理员用户帐户登录到Windows。
1. 选择 **“开始” > “控制面板” > “管理工具” > “计算机管理” > “本地用户和组”**.
1. 右键单击“用户”并选择 **新用户**.
1. 在相应的框中键入用户名和密码，并在其余框中键入所需的任何其他信息。
1. 取消选择 **用户下次登录时必须更改密码**，单击 **创建**，然后单击 **关闭**.
1. 单击 **用户**，右键单击您创建的用户并选择 **属性**.
1. 单击 **成员** 选项卡，然后单击 **添加**.
1. 在“输入要选择的对象名称”框中，键入 `Administrators`，单击检查名称以确保组名称正确。
1. 单击 **确定** 然后单击 **确定** 再来一次。
1. 选择 **“开始” > “控制面板” > “管理工具” > “本地安全策略” > “本地策略”**.
1. 单击用户权限分配，然后右键单击作为操作系统的一部分操作，并选择属性。
1. 单击 **添加用户或组**.
1. 在输入要选择的对象名称框中，键入您在步骤4中创建的用户的名称，然后单击 **检查名称** 以确保名称正确，然后单击 **确定**.
1. 单击 **确定** 关闭Act As A Operating System Properties对话框。

### 配置WebSphere以使用新创建的用户作为管理员 {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. 确保WebSphere正在运行。
1. 在WebSphere管理控制台中，选择 **安全>全局安全**.
1. 在管理安全下，选择 **管理用户角色**.
1. 单击添加，然后执行以下操作：

   1. 类型 **&amp;ast；** ，然后单击搜索。
   1. 单击 **管理员** 在“角色”下。
   1. 将新创建的用户添加到映射到角色并将其映射到管理员。

1. 单击 **确定** 并保存更改。
1. 重新启动WebSphere配置文件。

## 启用管理安全性 {#enable-administrative-security}

1. 在WebSphere管理控制台中，选择 **安全>全局安全**.
1. 单击 **安全配置向导**.
1. 确保 **启用应用程序安全** 复选框已启用。 单击&#x200B;**下一步**。
1. 选择 **联合存储库** 并单击 **下一个**.
1. 指定要设置的凭据，然后单击 **下一个**.
1. 单击 **完成**.
1. 重新启动WebSphere配置文件。

   WebSphere开始使用默认密钥库和truststore。

## 启用SSL（自定义密钥和信任库） {#enable-ssl-custom-key-and-truststore}

可以使用ikeyman实用程序或Admin Console创建信任库和密钥库。 要使ikeyman正常工作，请确保WebSphere安装路径不包含圆括号。

1. 在WebSphere管理控制台中，选择 **安全> SSL证书和密钥管理**.
1. 单击 **密钥库和证书** 在“相关项目”下。
1. 在 **密钥存储使用情况** 下拉列表，确保 **SSL密钥库** 已选中。 单击 **新建**.
1. 键入逻辑名称和说明。
1. 指定要创建密钥库的路径。 如果已通过ikeyman创建了keystore，请指定指向keystore文件的路径。
1. 指定并确认密码。
1. 选择密钥库类型并单击 **应用**.
1. 保存主配置。
1. 单击 **个人证书**.
1. 如果您添加了已使用ikeyman创建的密钥库，则会显示您的证书。 否则，您需要通过执行以下步骤来添加新的自签名证书：

   1. 选择 **创建 > 自签名证书** 。
   1. 在证书表单中指定相应的值。 确保将别名和公用名保留为计算机的完全限定域名。
   1. 单击&#x200B;**应用**。

1. 重复步骤2至10以创建 truststore。

## 应用自定义的密钥库和 truststore 至服务器 {#apply-custom-keystore-and-truststore-to-the-server}

1. 在 WebSphere 管理控制台中，选择 **安全 > SSL 证书和密钥管理** 。
1. 单击 **管理端点安全配置** 。 将打开 &quot;本地拓扑图&quot;。
1. 在入站下，选择节点的直接子项。
1. 在相关项目下，选择 **SSL 配置** 。
1. 选择 **NodeDeafultSSLSetting** 。
1. 从信任库名称和密钥库名称下拉列表中，选择您创建的自定义信任库和密钥库。
1. 单击&#x200B;**应用**。
1. 保存主配置。
1. 重新启动WebSphere配置文件。

   现在，您的配置文件会在自定义SSL设置和证书上运行。

## 启用对AEM表单本地程序的支持 {#enabling-support-for-aem-forms-natives}

1. 在WebSphere管理控制台中，选择 **安全>全局安全**.
1. 在身份验证部分，展开 **RMI/IIOP安全** 并单击 **CSIv2入站通信**.
1. 确保 **支持SSL** 在“传输”下拉列表中选择。
1. 重新启动WebSphere配置文件。

## 配置WebSphere以转换以https开头的URL {#configuring-websphere-to-convert-urls-that-begins-with-https}

要转换以https开头的URL，请将该URL的签名者证书添加到WebSphere服务器。

**为启用https的站点创建签名者证书**

1. 确保WebSphere正在运行。
1. 在WebSphere管理控制台中，导航到签名者证书，然后单击“安全”>“SSL证书和密钥管理”>“密钥存储和证书”>“NodeDefaultTrustStore”>“签名者证书”。
1. 单击从端口检索并执行以下任务：

   * 在主机框中，键入URL。 例如，键入 `www.paypal.com`.
   * 在“端口”框中，键入 `443`. 此端口是默认的SSL端口。
   * 在“别名”框中，键入别名。

1. 单击检索签名者信息，然后验证是否检索了信息。
1. 单击应用，然后单击保存。

现在，从已添加证书的站点的HTML到PDF转换将在生成PDF服务中起作用。

>[!NOTE]
>
>对于从WebSphere内部连接到SSL站点的应用程序，需要签名者证书。 它由Java安全套接字扩展(JSSE)用来验证在SSL握手期间连接的远程端发送的证书。

## 配置动态端口 {#configuring-dynamic-ports}

启用全局安全后，IBM WebSphere不允许对ORB.init()进行多次调用。 您可以在https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704上阅读有关永久限制的信息。

执行以下步骤，将端口设置为动态并解决问题：

1. 在WebSphere管理控制台中，选择 **服务器** > **服务器类型** > **WebSphere应用程序服务器**.
1. 在“首选项”部分，选择您的服务器。
1. 在 **配置** 选项卡，下 **通信** 部分，展开 **端口**，然后单击 **详细信息**.
1. 单击以下端口名称，更改 **端口号** 到0，然后单击 **确定**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## 配置sling.properties文件 {#configure-the-sling-properties-file}

1. 打开 `[aem-forms_root]`\crx-repository\launchpad\sling.properties文件进行编辑。
1. 找到 `sling.bootdelegation.ibm` 属性和添加 `com.ibm.websphere.ssl.*`到其值字段。 更新的字段如下所示：

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. 保存文件并重新启动服务器。
