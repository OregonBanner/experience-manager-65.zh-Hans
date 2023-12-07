---
title: WebDAV访问
description: 了解如何使用WebDAV访问AdobeExperience Manager。
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---

# WebDAV访问{#webdav-access}

要使用KDE通过WebDAV连接到AEM，请执行以下操作：

AEM提供WebDAV支持，可让您显示和编辑存储库内容。 通过WebDAV连接，您可以通过桌面直接访问内容存储库。 通过WebDAV连接添加到存储库中的文本和PDF文件会自动编制全文索引，并且可以使用标准搜索界面并通过标准Java™ API进行搜索。

## 常规 {#general}

[每个操作系统的详细说明](/help/sites-administering/webdav-access.md#connecting-via-webdav) 本文档中包含，但为了使用WebDAV协议连接到存储库，您可以将WebDAV客户端指向以下位置：

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

此URL在从操作系统级别连接时，提供对默认工作区的WebDAV访问( `crx.default`)。 虽然它对于用户来说比较简单，但是它没有为他们提供指定工作区名称的额外灵活性，而指定工作区名称可使用额外的 [WebDAV URL](/help/sites-administering/webdav-access.md#webdav-urls).

AEM按如下方式显示存储库内容：

* 类型的节点 `nt:folder` 显示为文件夹。 以下的节点 `nt:folder` 节点显示为文件夹内容。

* 类型的节点 `nt:file` 显示为文件。 以下的节点 `nt:file` 节点不会显示，但会构成文件的内容。

当您使用WebDAV创建和编辑文件夹和文件时，AEM会创建和编辑必要的 `nt:folder` 和 `nt:file` 节点。 如果您计划使用WebDAV导入和导出内容，请尝试使用 `nt:file` 和 `nt:folder` 尽可能多的节点类型。

>[!NOTE]
>
>在设置WebDAV之前，请检查 [技术要求](/help/sites-deploying/technical-requirements.md#webdav-clients).

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

通过更改路径中的工作区元素，可以映射默认工作区以外的工作区( `crx.default`)。 例如，要映射名为的工作区 `staging`，使用以下URL：

```xml
http://localhost:4502/crx/repository/staging
```

## 通过WebDAV连接 {#connecting-via-webdav}

[如上所述](/help/sites-administering/webdav-access.md#general)，要使用WebDAV协议连接到存储库，请将WebDAV客户端指向存储库位置。 但是，根据您的操作系统，连接客户端所涉及的步骤有所不同，可能需要配置操作系统。

提供了有关如何连接以下操作系统的说明：

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

要成功地将Microsoft® Windows 7（及更高版本）系统连接到不使用SSL保护的AEM实例，必须在Windows中明确启用通过不安全的网络建立基本身份验证的选项。 此功能要求在WebClient的Windows注册表中进行更改。

一旦更新了注册表，AEM实例就可以映射为驱动器。

#### Windows 7及更高配置 {#windows-and-greater-configuration}

要更新注册表以允许通过不安全的网络进行基本身份验证，请执行以下操作：

1. 找到以下注册表子项：

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. 设置 `BasicAuthLevel` 注册表项子项至值 `2` 或更高。

   如果不存在，请添加子键。

1. 重新启动系统以使注册表更改生效。

>[!NOTE]
>
>Adobe建议您使用与存储库用户相同的凭据创建Windows用户，否则可能会遇到权限冲突。

#### Windows 8配置 {#windows-configuration}

对于Windows 8，更改注册表项 [如Windows 7及更高版本中所述](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). 但是，在执行此任务之前，必须启用Desktop Experience才能看到注册表项。

要启用桌面体验，请打开 **服务器管理器**，则 **功能**，则 **添加功能**，则 **桌面体验**.

重新启动后，为Windows 7及更高版本描述的注册表项可用。 按照适用于Windows 7及更高版本的说明对其进行修改。

#### 在Windows中连接 {#connecting-in-windows}

要在Windows环境中通过WebDAV连接到AEM，请执行以下操作：

1. 打开 **Windows资源管理器** 或 **文件资源管理器** 并单击 **计算机** 或 **这台电脑**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. 要启动向导，请单击 **映射网络驱动器**.
1. 输入映射详细信息：

   * **驱动**：选择任意可用书信
   * **文件夹**： `http://localhost:4502`
   * Check **使用其他凭据连接**

   单击“完成”

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >如果AEM在另一个端口上，请使用该端口号，而不是4502。 此外，如果您没有在本地计算机上运行内容存储库，请将 `localhost` 相应的服务器名称或IP地址。

1. 输入用户名 `admin` 和密码 `admin`. Adobe建议您使用预配置的admin帐户进行测试。

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. 向导将关闭，新映射的驱动器将在Windows资源管理器或“文件资源管理器”窗口中打开。

   ![chlimage_1-115](assets/chlimage_1-115a.png)

Windows现在已通过WebDAV将AEM映射为驱动器，您可以将其用作任何其他驱动器。

### macOS {#macos}

在macOS上通过WebDAV连接不需要任何配置步骤。 您可以连接到WebDAV服务器。

1. 导航到任意 **Finder** 窗口，然后单击 **开始** 和 **连接到服务器**，或按 **Command+k**.
1. 在 **连接到服务器** 窗口中，输入AEM位置：

   * `http://localhost:4502`

   >[!NOTE]
   >
   >如果AEM在另一个端口上，请使用该端口号，而不是4502。 此外，如果您没有在本地计算机上运行内容存储库，请将 `localhost` 相应的服务器名称或IP地址。

1. 当系统提示您进行身份验证时，请输入用户名 `admin` 和密码 `admin`. Adobe建议您使用预配置的admin帐户进行测试。

macOS现在已通过WebDAV连接到AEM，您可以将其用作Mac上的任何其他文件夹。

### Linux® {#linux}

在Linux®上通过WebDAV进行连接不需要任何配置，但需要执行一些步骤才能建立连接，具体步骤因您的桌面环境而异。

#### 地名 {#gnome}

要使用GNOME通过WebDAV连接到AEM，请执行以下操作：

1. 在Nautilus （文件资源管理器）中，选择 **地标** 并选择 **连接到服务器**.
1. 在 **连接到服务器** 窗口，在服务类型中选择WebDAV (HTTP)。

1. 在 **服务器**，输入 `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >如果AEM在另一个端口上，请使用该端口号，而不是4502。 此外，如果您没有在本地计算机上运行内容存储库，请将 `localhost` 相应的服务器名称或IP地址。

1. 在 **文件夹**，输入 `/dav`
1. 输入用户名 `admin`. Adobe建议您使用预配置的admin帐户进行测试。
1. 将端口保留为空，并为连接输入任意名称。
1. 单击&#x200B;**连接**。AEM会提示您输入密码。
1. 输入密码 `admin` 并单击 **连接**.

GNOME现在已将AEM装载为卷，您可以像使用任何其他卷一样使用它。

#### KDE {#kde}

1. 打开网络文件夹向导。
1. 选择 **WebFolder**(webdav)，然后单击“下一步”。
1. 在 **名称**，键入连接名称。
1. 在 **用户**，输入 `admin.` Adobe建议您使用预配置的管理员帐户。
1. 在 **服务器**，输入 `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >如果AEM在另一个端口上，请使用该端口号，而不是4502。 此外，如果您没有在本地计算机上运行内容存储库，请将 `localhost` 相应的服务器名称或IP地址

1. 在 **文件夹**，输入 `dav`

1. 单击 **保存并连接**.
1. 提示输入密码时，请输入密码 `admin` 并单击 **连接**.

KDE现在已将AEM装载为卷，您可以像使用任何其他卷一样使用它。
