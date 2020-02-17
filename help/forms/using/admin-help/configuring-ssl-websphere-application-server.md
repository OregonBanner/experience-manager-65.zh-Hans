---
title: 为WebSphere应用程序服务器配置SSL
seo-title: 为WebSphere应用程序服务器配置SSL
description: 了解如何为WebSphere Application server配置SSL。
seo-description: 了解如何为WebSphere Application server配置SSL。
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# 为WebSphere应用程序服务器配置SSL {#configuring-ssl-for-websphere-application-server}

本节包括以下步骤，用于配置IBM webSphere Application server的SSL。

## 在WebSphere上创建本地用户帐户 {#creating-a-local-user-account-on-websphere}

要启用SSL,WebSphere需要访问本地操作系统用户注册表中具有管理系统权限的用户帐户：

* (Windows)创建属于管理员组的新Windows用户，该用户有权充当操作系统的一部分。 (请参 [阅为WebSphere创建Windows用户](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere)。)
* (Linux, UNIX)用户可以是根用户，也可以是具有根权限的其他用户。 在WebSphere上启用SSL时，请使用此用户的服务器标识和口令。

### 为WebSphere创建Linux或UNIX用户 {#create-a-linux-or-unix-user-for-websphere}

1. 以根用户身份登录。
1. 通过在命令提示符下输入以下命令创建用户：

   * （Linux和Sun Solaris） `useradd`
   * (IBM AIX) `mkuser`

1. 在命令提示符中输入新用户 `passwd` 的口令。
1. （Linux和Solaris）通过在命令提示符下输入(无参 `pwconv` 数)来创建卷影密码文件。

   >[!NOTE]
   >
   >（Linux和Solaris）要使WebSphere Application server本地OS安全注册表正常工作，必须存在卷影密码文件。 阴影密码文件通常命 **名为/etc/shadow** ，并基于/etc/passwd文件。 如果阴影密码文件不存在，则在启用全局安全性并将用户注册表配置为本地操作系统后，会发生错误。

1. 在文本编辑器中从/etc目录打开组文件。
1. 将您在步骤2中创建的用户添加到用 `root` 户组。
1. 保存并关闭文件。
1. （启用SSL的UNIX）以根用户身份启动和停止WebSphere。

### 创建WebSphere的Windows用户 {#create-a-windows-user-for-websphere}

1. 使用管理员用户帐户登录Windows。
1. 选择“ **开始”>“控制面板”>“管理工具”>“计算机管理”>“本地用户和用户组”**。
1. 右键单击“用户”，然后选择“ **新建用户”**。
1. 在相应的框中键入用户名和密码，并在其余框中键入所需的任何其他信息。
1. 取消选 **择“用户在下次登录时必须更改密码**”，单 **击“创建**” **，然后单击“**&#x200B;关闭”。
1. 单 **击“用户**”，右键单击刚创建的用户，然后选择“属 **性”**。
1. 单击“ **成员** ”选项卡，然后单 **击添加**。
1. 在“输入要选择的对象名称”(Enter The Object Names To Select)框中，键 `Administrators`入“选中名称”(Check Names)，确保组名称正确。
1. 单击 **确定** ，然后再次 **单击确定** 。
1. 选择“ **开始”>“控制面板”>“管理工具”>“本地安全策略”>“本地策略”**。
1. 单击“用户权限分配”，然后右键单击“作为操作系统的一部分”并选择“属性”。
1. Click **Add User or Group**.
1. 在“输入要选择的对象名称”框中，键入在步骤4中创建的用户的名称，单击“ **Check Names** ”（检查名称）以确保该名称正确，然后单击“ **确定”(OK)**。
1. 单击 **确定** ，关闭“作为操作系统属性”对话框的一部分。

### 将WebSphere配置为以管理员身份使用新创建的用户 {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. 确保WebSphere正在运行。
1. 在WebSphere管理控制台中，选择“安 **全性”>“全局安全性”**。
1. 在“管理安全性”下，选择“管 **理用户角色”**。
1. 单击“添加”并执行以下操作：

   1. **键入**&amp;ast;，然后单击“搜索”。
   1. 单击“ **管理员** ”(Administrator)。
   1. 将新创建的用户添加到映射到角色并将其映射到管理员。

1. Click **OK** and save your changes.
1. 重新启动WebSphere配置文件。

## 启用管理安全性 {#enable-administrative-security}

1. 在WebSphere管理控制台中，选择“安 **全性”>“全局安全性”**。
1. 单击“ **安全配置向导”**。
1. 确保 **已启用“启用应用程序安全** ”复选框。 单击&#x200B;**下一步**。
1. 选择 **Federated Reposities** ，然后单 **击Next**。
1. 指定要设置的凭据，然后单击“下 **一步”**。
1. 单击“ **完成**”。
1. 重新启动WebSphere配置文件。

   WebSphere将开始使用默认密钥库和truststore。

## 启用SSL（自定义密钥和信任存储） {#enable-ssl-custom-key-and-truststore}

可以使用ikeyman实用程序或管理控制台创建信任存储和密钥存储。 要使WebSphere正常工作，请确保WebSphere安装路径不包含括号。

1. 在WebSphere管理控制台中，选择“ **安全”>“SSL证书和密钥管理”**。
1. 单击“ **相关项目”下的** “密钥库和证书”。
1. 在“密钥 **存储使用情况** ”下拉菜单中，确保选 **择“SSL密钥存储** ”。 单击&#x200B;**新建**.
1. 键入逻辑名称和说明。
1. 指定要创建密钥库的路径。 如果已经通过ikeyman创建了密钥库，请指定密钥库文件的路径。
1. 指定并确认密码。
1. 选择密钥库类型，然后单击“ **应用”**。
1. 保存主配置。
1. 单击“ **个人证书**”。
1. 如果您已使用ikeyman添加了已创建密钥库的内容，则将显示您的证书。 否则，您需要通过执行以下步骤来添加新的自签名证书：

   1. 选择 **“创建”>“自签名证书”**。
   1. 在证书表单上指定适当的值。 确保将别名和通用名称保留为计算机的完全限定域名。
   1. 单击“ **应用**”。

1. 重复步骤2到10以创建信任存储。

## 将自定义密钥库和信任存储应用到服务器 {#apply-custom-keystore-and-truststore-to-the-server}

1. 在WebSphere管理控制台中，选择“ **安全”>“SSL证书和密钥管理”**。
1. 单击“ **管理端点安全配置”**。 将打开本地拓扑图。
1. 在“入站”下，选择节点的直接子项。
1. 在“相关项目”下，选择 **SSL配置**。
1. 选择 **NodeDefaultSSLSetting**。
1. 从truststore名称和keystore名称下拉列表中，选择您创建的自定义truststore和keystore。
1. 单击“ **应用**”。
1. 保存主配置。
1. 重新启动WebSphere配置文件。

   您的配置文件现在可在自定义SSL设置和您的证书上运行。

## 为AEM表单本机支持 {#enabling-support-for-aem-forms-natives}

1. 在WebSphere管理控制台中，选择“安 **全性”>“全局安全性”**。
1. 在“身份验证”部分，展开 **RMI/IIOP安全性** ，然后单 **击“CSIv2入站通信”**。
1. 确保在“ **传输”下拉列表中** ，选择了支持SSL的选项。
1. 重新启动WebSphere配置文件。

## 配置WebSphere以转换以https开头的URL {#configuring-websphere-to-convert-urls-that-begins-with-https}

要转换以https开头的URL，请为该URL添加一个签名者证书至WebSphere服务器。

**为启用https的站点创建签名者证书**

1. 确保WebSphere正在运行。
1. 在WebSphere管理控制台中，导航到签名者证书，然后单击“安全”>“SSL证书和密钥管理”>“密钥存储和证书”>“节点默认信任存储”>“签名者证书”。
1. 单击“从端口检索”并执行以下任务：

   * 在“主机”框中，键入URL。 例如，键入 `www.paypal.com`。
   * 在“端口”框中，键入 `443`。 此端口是默认的SSL端口。
   * 在“别名”框中，键入别名。

1. 单击“检索签名者信息”，然后验证是否检索到该信息。
1. 单击“应用”，然后单击“保存”。

现在，从添加证书的站点进行HTML到PDF的转换将可从“生成PDF”服务进行。

>[!NOTE]
>
>要使应用程序从WebSphere内部连接到SSL站点，需要签署者证书。 Java安全套接字扩展(JSSE)使用它验证在SSL握手期间发送的连接远程端的证书。

## 配置动态端口 {#configuring-dynamic-ports}

IBM webSphere不允许在启用全局安全时对ORB.init()进行多次调用。 您可以在https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704上阅读有关永久限制的信息。

执行以下步骤将端口设置为动态并解决问题：

1. 在WebSphere管理控制台中，选择“服 **务器** ”>“服 **务器类型** ” **>“** WebSphere应用程序服务器”。
1. 在“首选项”部分，选择您的服务器。
1. 在“配 **置** ”选项卡的“ **通信** ”部分下，展开“ **端口**”，然后单 ****&#x200B;击“详细信息”。
1. 单击以下端口名称，将端 **口号更改** 为0，然后单击“ **确定”**。

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## 配置sling.properties文件 {#configure-the-sling-properties-file}

1. 打开 `[aem-forms_root]`\crx-repository\launchpad\sling.properties文件进行编辑。
1. 找到该 `sling.bootdelegation.ibm` 属性并添 `com.ibm.websphere.ssl.*`加到其值字段。 更新后的字段如下所示：

   ```as3
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. 保存文件并重新启动服务器。

