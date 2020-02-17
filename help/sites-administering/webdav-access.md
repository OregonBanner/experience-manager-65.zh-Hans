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
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# WebDAV Access{#webdav-access}

要通过KDE通过WebDAV连接到AEM，请执行以下操作：

AEM提供WebDAV支持，允许您显示和编辑存储库内容。 通过WebDAV连接，您可以通过桌面直接访问内容存储库。 通过WebDAV连接添加到存储库的文本和PDF文件将自动建立全文索引，并且可以使用标准搜索界面和标准Java API进行搜索。

## 常规 {#general}

[本文档包含每个操作系统的详细说明](/help/sites-administering/webdav-access.md#connecting-via-webdav) ，但使用WebDAV协议连接到存储库的基本说明是，您将WebDAV客户端指向以下位置：

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

此URL从操作系统级别连接后，允许WebDAV访问默认工作区( `crx.default`)。 虽然对用户来说更简单，但它并没有赋予他们指定工作区名称的额外灵活性，这可以使用其他 [WebDAV URL来完成](/help/sites-administering/webdav-access.md#webdav-urls)。

AEM将按如下方式显示存储库内容：

* 类型的节点显 `nt:folder` 示为文件夹。 节点下的 `nt:folder` 节点将显示为文件夹内容。

* 类型的节点显 `nt:file` 示为文件。 不显示节 `nt:file` 点下的节点，但是这些节点构成了文件的内容。

当您使用WebDAV创建和编辑文件夹和文件时，AEM会创建和编辑必要的 `nt:folder` 和节 `nt:file` 点。 如果您计划使用WebDAV导入和导出内容，请尽可能 `nt:file` 使 `nt:folder` 用和节点类型。

>[!NOTE]
>
>在设置WebDAV之前，请查阅技 [术要求](/help/sites-deploying/technical-requirements.md#webdav-clients)。

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
   <td>WebDAV servlet映射到的路径</td>
   <td>工作区的名称</td>
  </tr>
 </tbody>
</table>

通过更改路径中的工作区元素，可以映射除默认()之外的工作区。 `crx.default`例如，要映射名为的工作区， `staging`请使用以下URL:

```xml
http://localhost:4502/crx/repository/staging
```

## 通过WebDAV连接 {#connecting-via-webdav}

[如上所述](/help/sites-administering/webdav-access.md#general)，要使用WebDAV协议连接到存储库，您需要将WebDAV客户端指向存储库位置。 但是，根据您的操作系统，连接客户端所涉及的步骤会有所不同，并且可能需要对操作系统进行配置。

提供了有关如何连接以下操作系统的说明：

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

要成功将Microsoft Windows 7（及更高版本）系统连接到未使用SSL保护的AEM实例，必须在Windows中显式启用通过不安全网络建立基本身份验证的选项。 这需要在WebClient的Windows注册表中进行更改。

更新注册表后，AEM实例便可映射为驱动器。

#### Windows 7及更高版本的配置 {#windows-and-greater-configuration}

要更新注册表以允许通过不安全的网络进行基本身份验证，请执行以下操作：

1. 找到以下注册表子项：

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. 将注册表 `BasicAuthLevel` 项子项设置为一个或更 `2` 大的值。

   如果不存在，则添加子键。

1. 必须重新启动系统，注册表更改才能生效。

有关此 [注册表更改的详细信息，请参阅Microsoft Support KB 841215](https://support.microsoft.com/default.aspx/kb/841215) 。

有关 [提高Windows下WebDav客户端响应性的信息，请参阅Microsoft Support KB 2445570](https://support.microsoft.com/kb/2445570) 。

>[!NOTE]
>
>Adobe建议您创建一个与存储库用户具有相同凭据的Windows用户，否则您可能会遇到权限冲突。

#### Windows 8配置 {#windows-configuration}

对于Windows 8，您还需要更改Windows 7及更 [高版本中描述的注册表条目](/help/sites-administering/webdav-access.md#windows-and-greater-configuration)。 但是，在执行此操作之前，必须启用桌面体验才能查看注册表条目。

要启用桌面体验，请依次打开 **Server Manager**、 **Features**、Add Features **、****** Desktop Experience Manager。

重新启动注册表条目后，Windows 7及更高版本中描述的注册表条目可用。 根据Windows 7及更高版本的说明修改它。

#### 在Windows中连接 {#connecting-in-windows}

要在Windows环境中通过WebDAV连接到AEM，请执行以下操作：

1. 打开 **Windows资源管理器****或文件资源管理器** ，然后单击“计算机” **或** “此PC ****&#x200B;调用”。

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. 单击 **映射网络驱动器** ，启动向导。
1. 输入映射详细信息：

   * **驱动器**:选择任何可用的字母
   * **文件夹**: `http://localhost:4502`
   * 使用 **不同凭据检查Connect**
   单击“完成”

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >如果AEM位于另一个端口上，请使用该端口号，而不是4502。 此外，如果您没有在本地计算机上运行内容存储库，请用相 `localhost` 应的服务器名或IP地址替换。

1. 输入用 `admin` 户名和密码 `admin`。 Adobe建议您使用预配置的管理员帐户进行测试。

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. 向导将关闭，并在Windows资源管理器或“文件资源管理器”窗口中打开新映射的驱动器。

   ![chlimage_1-115](assets/chlimage_1-115a.png)

Windows现在已通过WebDAV将AEM映射为驱动器，您可以将其用作任何其他驱动器。

### macOS {#macos}

在macOS上，无需执行任何配置步骤即可通过WebDAV进行连接。 您只需连接到WebDAV服务器。

1. 导航到任 **何Finder** ，单击“转到 ******,**&#x200B;连接到服务器 **”，或按** Command+k组合键。
1. 在“连 **接到服务器** ”窗口中，输入AEM位置：

   * `http://localhost:4502`
   >[!NOTE]
   >
   >如果AEM位于另一个端口上，请使用该端口号，而不是4502。 此外，如果您没有在本地计算机上运行内容存储库，请用相 `localhost` 应的服务器名或IP地址替换。

1. 当系统提示您进行身份验证时，请输入用 `admin` 户名和密码 `admin`。 Adobe建议您使用预配置的管理员帐户进行测试。

macOS现已通过WebDAV连接到AEM，您可以将其用作Mac上的任何其他文件夹。

### Linux {#linux}

在Linux上通过WebDAV进行连接不需要任何配置，但需要执行几个步骤来建立连接，具体取决于桌面环境。

#### GNOME {#gnome}

要通过WebDAV与GNOME连接到AEM，请执行以下操作：

1. 在Nautilus（文件浏览器）中，选择 **Places** ，然后选择 **Connect to Server**。
1. 在“连 **接到服务器** ”窗口中，选择“服务类型”中的“WebDAV(HTTP)”。

1. 在服 **务器中**，输入 `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >如果AEM位于另一个端口上，请使用该端口号，而不是4502。 此外，如果您没有在本地计算机上运行内容存储库，请用相 `localhost` 应的服务器名或IP地址替换。

1. 在文 **件夹中**，输入 `/dav`
1. 输入用户名 `admin`。 Adobe建议您使用预配置的管理员帐户进行测试。
1. 将端口留空，然后为连接输入任何名称。
1. 单击“ **连接**”。 AEM会提示您输入密码。
1. 输入密码， `admin` 然后单 **击Connect**。

GNOME现已将AEM作为卷安装，您可以像使用任何其他卷一样使用它。

#### KDE {#kde}

1. 打开“网络文件夹”向导。
1. 选择 **WebFolder**(webdav)，然后单击“下一步”。
1. 在“ **名称**”中，键入连接名称。
1. 在“ **用户**”中，输入 `admin.` Adobe建议您使用预配置的管理员帐户。
1. 在服 **务器中**，输入 `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >如果AEM位于另一个端口上，请使用该端口号，而不是4502。 此外，如果您没有在本地计算机上运行内容存储库，请用相应的服 `localhost` 务器名或IP地址替换

1. 在文 **件夹中**，输入 `dav`

1. 单击“ **保存并连接”**。
1. 当提示输入密码时，输入密码，然 `admin` 后单击“ **Connect**”。

KDE现已将AEM作为卷安装，您可以像使用任何其他卷一样使用它。
