---
title: 为WebSphere应用程序服务器配置SSL
seo-title: 为WebSphere应用程序服务器配置SSL
description: 了解如何为WebSphere Application Server配置SSL。
seo-description: 了解如何为WebSphere Application Server配置SSL。
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---


# 为WebSphere应用程序服务器{#configuring-ssl-for-websphere-application-server}配置SSL

本节包括通过IBM WebSphere Application Server配置SSL的以下步骤。

## 在WebSphere上创建本地用户帐户{#creating-a-local-user-account-on-websphere}

要启用SSL,WebSphere需要访问本地操作系统用户注册表中具有管理系统权限的用户帐户：

* (Windows)创建属于管理员组的新Windows用户，该用户具有充当操作系统一部分的权限。 （请参阅[为WebSphere创建Windows用户](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere)。）
* (Linux、UNIX)该用户可以是根用户，也可以是具有根权限的其他用户。 在WebSphere上启用SSL时，请使用此用户的服务器标识和密码。

### 为WebSphere创建Linux或UNIX用户{#create-a-linux-or-unix-user-for-websphere}

1. 以根用户身份登录。
1. 通过在命令提示符下输入以下命令创建用户：

   * （Linux和Sun Solaris）`useradd`
   * (IBM AIX)`mkuser`

1. 通过在命令提示符下输入`passwd`设置新用户的口令。
1. （Linux和Solaris）通过在命令提示符下输入`pwconv`（无参数），创建卷影密码文件。

   >[!NOTE]
   >
   >（Linux和Solaris）要使WebSphere Application Server本地OS安全注册表正常工作，必须存在卷影密码文件。 卷影密码文件通常名为&#x200B;**/etc/shadow**，基于/etc/passwd文件。 如果卷影密码文件不存在，则在启用全局安全性并将用户注册表配置为本地操作系统后，将发生错误。

1. 在文本编辑器中从/etc目录打开组文件。
1. 将您在步骤2中创建的用户添加到`root`组。
1. 保存并关闭文件。
1. （启用SSL的UNIX）开始并停止WebSphere作为根用户。

### 为WebSphere创建Windows用户{#create-a-windows-user-for-websphere}

1. 使用管理员用户帐户登录到Windows。
1. 选择&#x200B;**开始>控制面板>管理工具>计算机管理>本地用户和组**。
1. 右键单击“用户”，然后选择“新建用户”**。**
1. 在相应的框中键入用户名和密码，并在其余框中键入您需要的任何其他信息。
1. 取消选择&#x200B;**“用户在下次登录时必须更改密码**”，单击&#x200B;**创建**，然后单击&#x200B;**关闭**。
1. 单击&#x200B;**Users**，右键单击刚刚创建的用户，然后选择&#x200B;**Properties**。
1. 单击&#x200B;**“**&#x200B;的成员”选项卡，然后单击&#x200B;**添加**。
1. 在“输入要选择的对象名称”框中，键入`Administrators`，单击“检查名称”以确保组名称正确。
1. 单击&#x200B;**OK**，然后再次单击&#x200B;**OK**。
1. 选择&#x200B;**开始>控制面板>管理工具>本地安全策略>本地策略**。
1. 单击“用户权限分配”，然后右键单击“作为操作系统的一部分”，然后选择“属性”。
1. 单击&#x200B;**添加用户或组**。
1. 在“输入要选择的对象名称”框中，键入您在步骤4中创建的用户的名称，单击&#x200B;**检查名称**&#x200B;以确保名称正确，然后单击&#x200B;**确定**。
1. 单击&#x200B;**确定**&#x200B;以关闭“作为操作系统属性”对话框的一部分。

### 将WebSphere配置为以管理员{#configure-websphere-to-use-the-newly-created-user-as-administrator}身份使用新创建的用户

1. 确保WebSphere正在运行。
1. 在WebSphere管理控制台中，选择&#x200B;**安全>全局安全**。
1. 在“管理安全”下，选择&#x200B;**“管理用户角色”**。
1. 单击“添加”并执行以下操作：

   1. 在搜索框中键入&#x200B;**&amp;ast;**&#x200B;并单击“search”。
   1. 单击“角色”下的&#x200B;**Administrator**。
   1. 将新创建的用户添加到映射到角色，并将其映射到管理员。

1. 单击&#x200B;**确定**&#x200B;并保存更改。
1. 重新启动WebSphere用户档案。

## 启用管理安全性{#enable-administrative-security}

1. 在WebSphere管理控制台中，选择&#x200B;**安全>全局安全**。
1. 单击&#x200B;**安全配置向导**。
1. 确保&#x200B;**启用应用程序安全**&#x200B;复选框已启用。 单击&#x200B;**下一步**。
1. 选择&#x200B;**联合资料库**&#x200B;并单击&#x200B;**下一步**。
1. 指定要设置的凭据，然后单击&#x200B;**下一步**。
1. 单击&#x200B;**完成**。
1. 重新启动WebSphere用户档案。

   WebSphere将使用默认密钥库和信任存储进行开始。

## 启用SSL（自定义密钥和信任存储）{#enable-ssl-custom-key-and-truststore}

可以使用ikeyman实用程序或管理控制台创建信任存储和密钥存储。 要使ikeyman正常工作，请确保WebSphere安装路径不包含括号。

1. 在WebSphere管理控制台中，选择&#x200B;**安全> SSL证书和密钥管理**。
1. 单击“相关项目”下的&#x200B;**密钥库和证书**。
1. 在&#x200B;**密钥存储用法**&#x200B;下拉框中，确保选择&#x200B;**SSL密钥存储**。 单击&#x200B;**新建**.
1. 键入逻辑名称和说明。
1. 指定要创建密钥库的路径。 如果已通过ikeyman创建密钥库，请指定密钥库文件的路径。
1. 指定并确认密码。
1. 选择密钥库类型，然后单击&#x200B;**应用**。
1. 保存主控配置。
1. 单击&#x200B;**个人证书**。
1. 如果已使用ikeyman添加已创建密钥库，则将显示您的证书。 否则，您需要通过执行以下步骤来添加新的自签名证书：

   1. 选择&#x200B;**创建>自签名证书**。
   1. 在证书表单上指定适当的值。 确保将别名和通用名称保留为计算机的完全限定域名。
   1. 单击&#x200B;**应用**。

1. 重复步骤2到10以创建信任存储。

## 将自定义密钥库和信任存储应用到服务器{#apply-custom-keystore-and-truststore-to-the-server}

1. 在WebSphere管理控制台中，选择&#x200B;**安全> SSL证书和密钥管理**。
1. 单击&#x200B;**管理端点安全配置**。 本地拓扑图打开。
1. 在“入站”下，选择节点的直接子项。
1. 在“相关项目”下，选择&#x200B;**SSL配置**。
1. 选择&#x200B;**NodeDefaultSSLSetting**。
1. 从truststore名称和keystore名称下拉列表中，选择您创建的自定义truststore和keystore。
1. 单击&#x200B;**应用**。
1. 保存主控配置。
1. 重新启动WebSphere用户档案。

   您的用户档案现在可在自定义SSL设置和证书上运行。

## 启用对AEM表单原生代码{#enabling-support-for-aem-forms-natives}的支持

1. 在WebSphere管理控制台中，选择&#x200B;**安全>全局安全**。
1. 在“身份验证”部分，展开&#x200B;**RMI/IIOP security**&#x200B;并单击&#x200B;**CSIv2入站通信**。
1. 确保在“传输”下拉列表中选择了&#x200B;**支持SSL的**。
1. 重新启动WebSphere用户档案。

## 配置WebSphere以转换以https {#configuring-websphere-to-convert-urls-that-begins-with-https}开头的URL

要转换以https开头的URL，请为该URL添加一个签名者证书至WebSphere服务器。

**为启用https的站点创建签名者证书**

1. 确保WebSphere正在运行。
1. 在WebSphere管理控制台中，导航到签署者证书，然后单击“安全”>“SSL证书和密钥管理”>“密钥存储和证书”>“NodeDefaultTrustStore”>“签署者证书”。
1. 单击“从端口检索”并执行以下任务:

   * 在“主机”框中，键入URL。 例如，键入`www.paypal.com`。
   * 在“端口”框中，键入`443`。 此端口是默认的SSL端口。
   * 在“别名”框中，键入别名。

1. 单击“检索签署方信息”，然后验证是否检索到该信息。
1. 单击“应用”，然后单击“保存”。

现在，从添加证书的站点进行HTML到PDF的转换将通过“生成PDF”服务工作。

>[!NOTE]
>
>要使应用程序从WebSphere内连接到SSL站点，需要签署者证书。 Java安全套接字扩展(JSSE)使用它验证在SSL握手期间发送的连接远程端的证书。

## 配置动态端口{#configuring-dynamic-ports}

启用全局安全时，IBM WebSphere不允许对ORB.init()进行多次调用。 您可以在https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704上阅读有关永久限制的信息。

请执行以下步骤将端口设置为动态并解决问题：

1. 在WebSphere管理控制台中，选择&#x200B;**服务器** > **服务器类型** > **WebSphere应用程序服务器**。
1. 在“首选项”部分，选择您的服务器。
1. 在&#x200B;**配置**&#x200B;选项卡的&#x200B;**通信**&#x200B;部分下，展开&#x200B;**端口**，然后单击&#x200B;**详细信息**。
1. 单击以下端口名称，将&#x200B;**端口号**&#x200B;更改为0，然后单击&#x200B;**确定**。

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## 配置sling.properties文件{#configure-the-sling-properties-file}

1. 打开`[aem-forms_root]`\crx-repository\launchpad\sling.properties文件进行编辑。
1. 找到`sling.bootdelegation.ibm`属性，并将`com.ibm.websphere.ssl.*`添加到其值字段。 更新后的字段如下所示：

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. 保存文件并重新启动服务器。

