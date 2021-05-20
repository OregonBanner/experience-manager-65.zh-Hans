---
title: 为WebSphere应用程序服务器配置SSL
seo-title: 为WebSphere应用程序服务器配置SSL
description: 了解如何为WebSphere应用程序服务器配置SSL。
seo-description: 了解如何为WebSphere应用程序服务器配置SSL。
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
exl-id: b0786b52-879e-4a24-9cc9-bd9dcb2473cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---

# 为WebSphere应用程序服务器{#configuring-ssl-for-websphere-application-server}配置SSL

本节包括以下步骤，用于使用IBM WebSphere Application Server配置SSL。

## 在WebSphere {#creating-a-local-user-account-on-websphere}上创建本地用户帐户

要启用SSL，WebSphere需要访问本地操作系统用户注册表中有权管理系统的用户帐户：

* (Windows)创建新的Windows用户，该用户属于管理员组，并有权作为操作系统的一部分。 （请参阅[为WebSphere](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere)创建Windows用户。）
* (Linux、UNIX)用户可以是根用户，也可以是具有根权限的其他用户。 在WebSphere上启用SSL时，请使用此用户的服务器标识和密码。

### 为WebSphere {#create-a-linux-or-unix-user-for-websphere}创建Linux或UNIX用户

1. 以根用户身份登录。
1. 在命令提示符下输入以下命令以创建用户：

   * （Linux和Sun Solaris）`useradd`
   * (IBM AIX)`mkuser`

1. 通过在命令提示符下输入`passwd`来设置新用户的密码。
1. （Linux和Solaris）通过在命令提示符下输入`pwconv`（没有参数）来创建卷影密码文件。

   >[!NOTE]
   >
   >（Linux和Solaris）要使WebSphere应用程序服务器本地操作系统安全注册表正常工作，必须存在卷影密码文件。 卷影密码文件通常名为&#x200B;**/etc/shadow**，并基于/etc/passwd文件。 如果卷影密码文件不存在，则在启用全局安全性并将用户注册表配置为本地操作系统后，会发生错误。

1. 在文本编辑器中从/etc目录打开组文件。
1. 将您在步骤2中创建的用户添加到`root`组。
1. 保存并关闭文件。
1. （启用SSL的UNIX）以根用户身份启动和停止WebSphere。

### 为WebSphere {#create-a-windows-user-for-websphere}创建Windows用户

1. 使用管理员用户帐户登录到Windows。
1. 选择&#x200B;**开始>控制面板>管理工具>计算机管理>本地用户和组**。
1. 右键单击“用户”并选择&#x200B;**新建用户**。
1. 在相应的框中键入用户名和密码，然后在其余的框中键入您需要的任何其他信息。
1. 取消选择&#x200B;**用户在下次登录时必须更改密码**，单击&#x200B;**创建**，然后单击&#x200B;**关闭**。
1. 单击&#x200B;**Users**，右键单击刚刚创建的用户，然后选择&#x200B;**Properties**。
1. 单击&#x200B;**成员**&#x200B;选项卡，然后单击&#x200B;**添加**。
1. 在输入要选择的对象名称框中，键入`Administrators`，单击检查名称以确保组名称正确。
1. 单击&#x200B;**OK**，然后再次单击&#x200B;**OK**。
1. 选择&#x200B;**开始>控制面板>管理工具>本地安全策略>本地策略**。
1. 单击“用户权限分配”，然后右键单击“作为操作系统的一部分”，然后选择“属性”。
1. 单击&#x200B;**添加用户或组**。
1. 在输入要选择的对象名称框中，键入您在步骤4中创建的用户的名称，单击&#x200B;**检查名称**&#x200B;以确保名称正确，然后单击&#x200B;**确定**。
1. 单击&#x200B;**确定**&#x200B;以关闭作为操作系统属性对话框一部分的操作。

### 配置WebSphere以使用新创建的用户作为管理员{#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. 确保WebSphere正在运行。
1. 在WebSphere管理控制台中，选择&#x200B;**安全>全局安全**。
1. 在管理安全下，选择&#x200B;**管理用户角色**。
1. 单击添加，然后执行以下操作：

   1. 在搜索框中键入&#x200B;**&amp;ast;**&#x200B;并单击搜索。
   1. 单击角色下的&#x200B;**管理员**。
   1. 将新创建的用户添加到映射到角色，然后将其映射到管理员。

1. 单击&#x200B;**确定**&#x200B;并保存更改。
1. 重新启动WebSphere配置文件。

## 启用管理安全性{#enable-administrative-security}

1. 在WebSphere管理控制台中，选择&#x200B;**安全>全局安全**。
1. 单击&#x200B;**安全配置向导**。
1. 确保&#x200B;**启用应用程序安全**&#x200B;复选框已启用。 单击&#x200B;**下一步**。
1. 选择&#x200B;**联合资料库**&#x200B;并单击&#x200B;**下一步**。
1. 指定要设置的凭据，然后单击&#x200B;**Next**。
1. 单击&#x200B;**完成**。
1. 重新启动WebSphere配置文件。

   WebSphere将开始使用默认密钥库和truststore。

## 启用SSL（自定义密钥和信任存储）{#enable-ssl-custom-key-and-truststore}

可以使用ikeyman实用程序或管理控制台创建信任库和密钥库。 要使键盘正常工作，请确保WebSphere安装路径不包含圆括号。

1. 在WebSphere管理控制台中，选择&#x200B;**安全> SSL证书和密钥管理**。
1. 单击“相关项目”下的&#x200B;**密钥库和证书**。
1. 在&#x200B;**密钥存储用法**&#x200B;下拉列表中，确保已选择&#x200B;**SSL密钥存储**。 单击&#x200B;**新建**。
1. 键入逻辑名称和描述。
1. 指定希望创建密钥库的路径。 如果已通过ikeyman创建密钥库，请指定密钥库文件的路径。
1. 指定并确认密码。
1. 选择密钥库类型，然后单击&#x200B;**Apply**。
1. 保存主控配置。
1. 单击&#x200B;**个人证书**。
1. 如果您已使用ikeyman添加了已创建密钥库的内容，则将显示您的证书。 否则，您需要执行以下步骤来添加新的自签名证书：

   1. 选择&#x200B;**创建>自签名证书**。
   1. 在证书表单上指定适当的值。 确保将别名和通用名称保留为计算机的完全限定的域名。
   1. 单击&#x200B;**Apply**。

1. 重复步骤2至10以创建信任存储。

## 将自定义密钥库和信任存储应用到服务器{#apply-custom-keystore-and-truststore-to-the-server}

1. 在WebSphere管理控制台中，选择&#x200B;**安全> SSL证书和密钥管理**。
1. 单击&#x200B;**管理端点安全配置**。 将打开本地拓扑图。
1. 在“入站”下，选择节点的直接子项。
1. 在“相关项目”下，选择&#x200B;**SSL配置**。
1. 选择&#x200B;**NodeDefaultSSLSetting**。
1. 从truststore名称和KeyStore名称下拉列表中，选择您创建的自定义truststore和KeyStore。
1. 单击&#x200B;**Apply**。
1. 保存主控配置。
1. 重新启动WebSphere配置文件。

   您的配置文件现在在自定义SSL设置和证书上运行。

## 启用对AEM表单本机{#enabling-support-for-aem-forms-natives}的支持

1. 在WebSphere管理控制台中，选择&#x200B;**安全>全局安全**。
1. 在“Authentication（身份验证）”部分中，展开&#x200B;**RMI/IIOP security**&#x200B;并单击&#x200B;**CSIv2入站通信**。
1. 确保在“传输”下拉列表中选择了&#x200B;**SSL支持的**。
1. 重新启动WebSphere配置文件。

## 配置WebSphere以转换以https {#configuring-websphere-to-convert-urls-that-begins-with-https}开头的URL

要转换以https开头的URL，请为该URL添加签名者证书至WebSphere服务器。

**为启用https的站点创建签名者证书**

1. 确保WebSphere正在运行。
1. 在WebSphere管理控制台中，导航到签名者证书，然后单击安全> SSL证书和密钥管理>密钥存储和证书> NodeDefaultTrustStore >签名者证书。
1. 单击从端口检索并执行以下任务：

   * 在“主机”框中，键入URL。 例如，键入`www.paypal.com`。
   * 在“Port（端口）”框中，键入`443`。 此端口是默认的SSL端口。
   * 在“别名”框中，键入别名。

1. 单击检索签名者信息，然后验证该信息是否已检索到。
1. 单击“应用”，然后单击“保存”。

现在，从添加了证书的网站进行HTML到PDF的转换，将可从“生成PDF”服务中正常工作。

>[!NOTE]
>
>要使应用程序从WebSphere内部连接到SSL站点，需要签名者证书。 Java安全套接字扩展(JSSE)使用它来验证在SSL握手期间发送的连接远程端的证书。

## 配置动态端口{#configuring-dynamic-ports}

启用“全局安全”后，IBM WebSphere不允许对ORB.init()进行多次调用。 有关永久限制的信息，请访问https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704。

执行以下步骤以将端口设置为动态并解决此问题：

1. 在WebSphere管理控制台中，选择&#x200B;**服务器** > **服务器类型** > **WebSphere应用程序服务器**。
1. 在“首选项”部分，选择您的服务器。
1. 在&#x200B;**Configuration**&#x200B;选项卡的&#x200B;**Communications**&#x200B;部分下，展开&#x200B;**Ports** ，然后单击&#x200B;**Details**。
1. 单击以下端口名称，将&#x200B;**端口号**&#x200B;更改为0，然后单击&#x200B;**确定**。

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## 配置sling.properties文件{#configure-the-sling-properties-file}

1. 打开`[aem-forms_root]`\crx-repository\launchpad\sling.properties文件进行编辑。
1. 找到`sling.bootdelegation.ibm`属性，并将`com.ibm.websphere.ssl.*`添加到其值字段。 更新的字段如下所示：

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. 保存文件并重新启动服务器。
