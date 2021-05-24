---
title: WebDAV访问
seo-title: WebDAV访问
description: 了解AEM中的WebDAV访问。
seo-description: 了解AEM中的WebDAV访问。
uuid: b0ecaa5d-5454-42df-8453-404ece734c32
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 1eaf7afe-a181-45df-8766-bd564b1ad22a
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---

# WebDAV访问{#webdav-access}

要通过使用KDE通过WebDAV连接到AEM，请执行以下操作：

AEM提供了WebDAV支持，可让您显示和编辑存储库内容。 通过WebDAV连接可让您通过桌面直接访问内容存储库。 通过WebDAV连接添加到存储库的文本和PDF文件会自动建立全文索引，并且可以使用标准搜索界面和标准Java API进行搜索。

## 常规 {#general}

[本文档中包](/help/sites-administering/webdav-access.md#connecting-via-webdav) 含的每个操作系统的详细说明，但本质上是使用WebDAV协议连接到存储库的说明，您将WebDAV客户端指向以下位置：

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

当从操作系统级别连接此URL时，WebDAV将访问默认工作区(`crx.default`)。 虽然对于用户而言，这样更简单，但并不能赋予他们指定工作区名称的额外灵活性，可以使用附加的[WebDAV URL](/help/sites-administering/webdav-access.md#webdav-urls)来完成此操作。

AEM按如下方式显示存储库内容：

* 类型`nt:folder`的节点显示为文件夹。 `nt:folder`节点下的节点将显示为文件夹内容。

* 类型`nt:file`的节点显示为文件。 未显示`nt:file`节点下的节点，但会形成文件的内容。

使用WebDAV创建和编辑文件夹和文件时，AEM会创建和编辑必要的`nt:folder`和`nt:file`节点。 如果您计划使用WebDAV导入和导出内容，请尽量使用`nt:file`和`nt:folder`节点类型。

>[!NOTE]
>
>在设置WebDAV之前，请检查[技术要求](/help/sites-deploying/technical-requirements.md#webdav-clients)。

## WebDAV URL {#webdav-urls}

WebDAV服务器的URL具有以下结构：

<table>
 <colgroup>
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
 </colgroup>
 <tbody>
  <tr>
   <td>
    <code>
     <strong>URL Component</strong>
    </code></td>
   <td><code>https://&lt;host&gt;:&lt;port&gt;</code></td>
   <td><code>/&lt;crx-webapp-path&gt;</code></td>
   <td><code>/repository</code></td>
   <td><code>/&lt;workspace&gt;</code></td>
  </tr>
  <tr>
   <td>
    <code>
     <strong>Example</strong>
    </code></td>
   <td><code>http://localhost:4502</code></td>
   <td><code>/crx</code></td>
   <td><code>/repository</code></td>
   <td><code>/crx.default</code></td>
  </tr>
  <tr>
   <td><strong>描述</strong></td>
   <td>运行AEM的主机和端口</td>
   <td>AEM存储库Web应用程序的路径</td>
   <td>WebDAV Servlet映射到的路径</td>
   <td>工作区的名称</td>
  </tr>
 </tbody>
</table>

通过更改路径中的工作区元素，可以映射默认(`crx.default`)以外的工作区。 例如，要映射名为`staging`的工作区，请使用以下URL:

```xml
http://localhost:4502/crx/repository/staging
```

## 通过WebDAV {#connecting-via-webdav}连接

[如上所述](/help/sites-administering/webdav-access.md#general)，要使用WebDAV协议连接到存储库，您需要将WebDAV客户端指向您的存储库位置。但是，根据您的操作系统，连接客户端时涉及的步骤会有所不同，并且可能需要配置操作系统。

提供了关于如何连接以下操作系统的说明：

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

要成功将Microsoft Windows 7（及更高版本）系统连接到未使用SSL保护的AEM实例，必须在Windows中明确启用通过不安全网络建立基本身份验证的选项。 这要求在WebClient的Windows注册表中进行更改。

更新注册表后，AEM实例即可映射为驱动器。

#### Windows 7及更高配置{#windows-and-greater-configuration}

要更新注册表，以允许在不安全的网络上进行基本身份验证，请执行以下操作：

1. 找到以下注册表子项：

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. 将`BasicAuthLevel`注册表项子项设置为值`2`或更高。

   如果不存在，请添加子键。

1. 必须重新启动系统，注册表更改才能生效。

有关此注册表更改的详细信息，请参阅[Microsoft支持KB 841215](https://support.microsoft.com/default.aspx/kb/841215)。

请参阅[Microsoft支持KB 2445570](https://support.microsoft.com/kb/2445570) ，以了解有关在Windows下改进WebDav客户端响应性的信息。

>[!NOTE]
>
>Adobe建议您创建一个与存储库用户具有相同凭据的Windows用户，否则可能会遇到权限冲突。

#### Windows 8配置{#windows-configuration}

对于Windows 8，还需要按照Windows 7及更高版本](/help/sites-administering/webdav-access.md#windows-and-greater-configuration)的说明更改注册表项[。 但是，在执行此操作之前，必须启用桌面体验才能查看注册表项。

要启用桌面体验，请依次打开&#x200B;**服务器管理器**、**功能**、**添加功能**、**桌面体验**。

重新启动Windows 7及更高版本描述的注册表项后，可用。 按照Windows 7及更高版本中的说明对其进行修改。

#### 在Windows {#connecting-in-windows}中连接

要在Windows环境中通过WebDAV连接到AEM，请执行以下操作：

1. 打开&#x200B;**Windows Explorer**&#x200B;或&#x200B;**文件资源管理器**&#x200B;并单击&#x200B;**Computer**&#x200B;或&#x200B;**此PC**。

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. 单击&#x200B;**映射网络驱动器**&#x200B;以启动向导。
1. 输入映射详细信息：

   * **驱动器**:选择任何可用的信件
   * **文件夹**:  `http://localhost:4502`
   * 检查&#x200B;**使用不同凭据连接**

   单击“完成”

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >如果AEM位于其他端口上，请使用该端口号，而不是4502。 此外，如果您未在本地计算机上运行内容存储库，请将`localhost`替换为相应的服务器名称或IP地址。

1. 输入用户名`admin`和密码`admin`。 Adobe建议您使用预配置的管理员帐户进行测试。

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. 向导关闭，并在Windows资源管理器或文件资源管理器窗口中打开新映射的驱动器。

   ![chlimage_1-114](assets/chlimage_1-115a.png)

Windows现在已通过WebDAV将AEM映射为驱动器，您可以将其用作任何其他驱动器。

### macOS {#macos}

在macOS中，无需执行任何配置步骤即可通过WebDAV连接。 您只需连接到WebDAV服务器即可。

1. 导航到任意&#x200B;**Finder**&#x200B;窗口，然后单击&#x200B;**Go**&#x200B;和&#x200B;**连接到服务器**，或按&#x200B;**Command+k**。
1. 在&#x200B;**连接到Server**&#x200B;窗口中，输入AEM位置：

   * `http://localhost:4502`
   >[!NOTE]
   >
   >如果AEM位于其他端口上，请使用该端口号，而不是4502。 此外，如果您未在本地计算机上运行内容存储库，请将`localhost`替换为相应的服务器名称或IP地址。

1. 提示您进行身份验证时，请输入用户名`admin`和密码`admin`。 Adobe建议您使用预配置的管理员帐户进行测试。

macOS现在已通过WebDAV连接到AEM，您可以将其用作Mac上的任何其他文件夹。

### Linux {#linux}

在Linux上通过WebDAV连接不需要任何配置，但需要执行一些步骤来建立连接，具体取决于您的桌面环境。

#### 格诺梅 {#gnome}

要通过使用GNOME通过WebDAV连接到AEM，请执行以下操作：

1. 在Nautilus（文件资源管理器）中，选择&#x200B;**Places**&#x200B;并选择&#x200B;**Connect to Server**。
1. 在&#x200B;**连接到服务器**&#x200B;窗口中，在服务类型中选择WebDAV(HTTP)。

1. 在&#x200B;**Server**&#x200B;中，输入`http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >如果AEM位于其他端口上，请使用该端口号，而不是4502。 此外，如果您未在本地计算机上运行内容存储库，请将`localhost`替换为相应的服务器名称或IP地址。

1. 在&#x200B;**文件夹**&#x200B;中，输入`/dav`
1. 输入用户名`admin`。 Adobe建议您使用预配置的管理员帐户进行测试。
1. 将端口留空，并输入连接的任意名称。
1. 单击&#x200B;**连接**。 AEM会提示您输入密码。
1. 输入密码`admin`并单击&#x200B;**连接**。

GNOME现已将AEM作为卷进行装载，您可以像任何其他卷一样使用它。

#### KDE {#kde}

1. 打开“网络文件夹”向导。
1. 选择&#x200B;**WebFolder**(webdav)，然后单击“下一步”。
1. 在&#x200B;**名称**&#x200B;中，键入连接名称。
1. 在&#x200B;**User**&#x200B;中，输入`admin.`Adobe，建议您使用预配置的管理员帐户。
1. 在&#x200B;**Server**&#x200B;中，输入`http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >如果AEM位于其他端口上，请使用该端口号，而不是4502。 此外，如果您未在本地计算机上运行内容存储库，请将`localhost`替换为相应的服务器名称或IP地址

1. 在&#x200B;**文件夹**&#x200B;中，输入`dav`

1. 单击&#x200B;**保存并连接**。
1. 提示输入密码时，输入密码`admin`并单击&#x200B;**连接**。

KDE现在已将AEM作为卷装载，您可以像使用任何其他卷一样使用它。
