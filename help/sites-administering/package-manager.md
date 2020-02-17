---
title: 如何使用包
seo-title: 如何使用包
description: 了解在AEM中处理包的基础知识。
seo-description: 了解在AEM中处理包的基础知识。
uuid: cba76a5f-5d75-4d63-a0f4-44c13fa1baf2
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6694a135-d1e1-4afb-9f5b-23991ee70eee
docset: aem65
translation-type: tm+mt
source-git-commit: 5e10ddb0e5cf24e1915d0840cd380520374e93ea

---


# How to Work With Packages{#how-to-work-with-packages}

包支持导入和导出存储库内容。 例如，您可以使用包安装新功能、在实例之间传输内容以及备份存储库内容。

可以从以下页面访问和／或维护包：

* [包管理器](#package-manager)，用于管理本地AEM实例中的包。

* [Package Share](#package-share)，一个集中服务器，它既包含公开可用的包，又包含您公司的私有包。 公共包可以包含修补程序、新功能、文档等。

可以在包管理器、包共享和文件系统之间传输包。

## 什么是包？ {#what-are-packages}

包是一个zip文件，它以文件系统序列化（称为“Vault”序列化）的形式保存存储库内容。 这为文件和文件夹提供了易于使用和编辑的表示形式。

包中包括使用过滤器选择的内容，包括页面内容和项目相关内容。

包中还包含电子仓库元信息，包括过滤器定义和导入配置信息。 包中可以包含其他内容属性（不用于包提取），如描述、可视图像或图标；这些属性仅用于内容包消费者和信息用途。

>[!NOTE]
>
>包表示构建包时内容的当前版本。 它们不包括AEM保存在存储库中的任何旧版本内容。

您可以对包或对包执行以下操作：

* 创建新包；根据需要定义包设置和过滤器
* 预览包内容（构建前）
* 构建包
* 查看包信息
* 查看包内容（构建后）
* 修改现有包的定义
* 重建现有包
* 重新打包包
* 将包从AEM下载到文件系统
* 将包从文件系统上传到本地AEM实例
* 安装前验证包内容
* 执行练习安装
* 安装包（AEM在上传后不会自动安装包）
* 删除包
* 从包共享库下载包，如修补程序
* 将包上传到包共享库的公司内部部分

## 包信息 {#package-information}

包定义由各种类型的信息组成：

* [包设置](#package-settings)
* [包过滤器](#package-filters)
* [打包屏幕截图](#package-screenshots)
* [包图标](#package-icons)

### 包设置 {#package-settings}

您可以编辑各种“包设置”来定义包描述、相关错误、依赖关系和提供者信息等方面。

在创 **建或编辑Package时** ，可通过“编辑 **”按钮使用“包设** 置”对话框，并提 [](#creating-a-new-package)[](#viewing-and-editing-package-information) 供三个用于配置的选项卡。 进行任何更改后，单击“ **确定** ”以保存这些更改。

![包编辑](assets/packagesedit.png)

| **字段** | **描述** |
|---|---|
| 名称 | 包的名称。 |
| 组 | 要将包添加到的组的名称，用于组织包。 键入新用户组的名称，或选择现有用户组。 |
| 版本 | 用于自定义版本的文本。 |
| 描述 | 包的简要说明。 HTML标记可用于格式化。 |
| 缩略图 | 随包列表一起显示的图标。 单击“浏览”以选择本地文件。 |

![chlimage_1-108](assets/chlimage_1-108.png)

<table>
 <tbody>
  <tr>
   <th><strong>字段</strong></th>
   <th><strong>描述</strong></th>
   <th><strong>格式／示例</strong></th>
  </tr>
  <tr>
   <td>名称</td>
   <td>提供者的名称。</td>
   <td><em>AEM Geometrixx<br /> </em></td>
  </tr>
  <tr>
   <td>URL</td>
   <td>提供者的URL。</td>
   <td><em>https://www.aem-geometrixx.com</em></td>
  </tr>
  <tr>
   <td>链接</td>
   <td>指向提供者页面的包特定链接。</td>
   <td><em>https://www.aem-geometrixx.com/mypackage.html</em></td>
  </tr>
  <tr>
   <td>需要<br /> </td>
   <td>
    <ul>
     <li>管理员：选择何时包只能由具有管理员权限的帐户安装。</li>
     <li>重新启动：选择安装包后需要重新启动服务器的时间。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AC 处理</td>
   <td><p>指定在导入包时如何处理包中定义的访问控制信息：</p>
    <ul>
     <li><strong>忽略</strong></li>
     <li><strong>覆盖</strong></li>
     <li><strong>合并</strong></li>
     <li><strong>清除</strong></li>
     <li><strong>MergePreserve</strong></li>
    </ul> <p>The default value is <strong>Ignore</strong>.</p> </td>
   <td>
    <ul>
     <li><strong>忽略</strong> -保留存储库中的ACL</li>
     <li><strong>覆盖</strong> -覆盖存储库中的ACL</li>
     <li><strong>合并</strong> -合并两组ACL</li>
     <li><strong>清除</strong> -清除ACL</li>
     <li><strong>合并保留</strong> -通过添加内容中不存在的承担者的访问控制条目，将内容中的访问控制与包中提供的访问控制合并</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

![包依赖关系](assets/packagesdependencies.png)

| **字段** | **描述** | **格式／示例** |
|---|---|---|
| 已通过 | 此包的目标产品名称和版本或与之兼容的版本。 | *AEM6* |
| 修复了错误／问题 | 一个文本字段，它允许您列出使用此包修复的错误的详细信息。 请在单独的行中列出每个错误。 | bug-nr摘要 |
| 依赖于 | 列出当需要其他包时需要遵守的依赖关系信息，以使当前包按预期运行。 使用修补程序时，此字段很重要。 | groupId:name:version |
| 替换 | 此包替换的已弃用包列表。 在安装之前，请检查此包是否包含旧版包中的所有必要内容，以便不覆盖任何内容。 | groupId:name:version |

### 包过滤器 {#package-filters}

过滤器标识要包含在包中的存储库节点。 “过 **滤器定义** ”指定以下信息：

* 要包 **含的内容的根路径** 。
* **包含** 或排除根路径下特定节点的规则。

过滤器可以包括零个或多个规则。 当未定义规则时，包中包含根路径下的所有内容。

您可以为包定义一个或多个过滤器定义。 使用多个过滤器来包含来自多个根路径的内容。

![chlimage_1-109](assets/chlimage_1-109.png)

下表介绍了这些规则并提供了示例：

<table>
 <tbody>
  <tr>
   <th> 规则类型</th>
   <th>描述 </th>
   <th>示例 </th>
  </tr>
  <tr>
   <td> 包括</td>
   <td>您可以定义路径，或使用正则表达式指定要包括的所有节点。<br /> 包 <br /> 含目录将：
    <ul>
     <li>包括该 <i>目录</i> ，以及该目录中的所有文件和文件夹（即整个子树）</li>
     <li><strong>不包含</strong> 指定根路径下的其他文件或文件夹</li>
    </ul> </td>
   <td>/libs/sling/install(/)*)? </td>
  </tr>
  <tr>
   <td> 排除</td>
   <td>您可以指定路径或使用正则表达式来指定要排除的所有节点。<br /> 排 <br /> 除目录将排除该目录 <i>以及该目录</i> （即整个子树）中的所有文件和文件夹。<br /> </td>
   <td>/libs/wcm/foundation/components(/)*)?</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>一个包可以包含多个过滤器定义，这样，来自不同位置的节点可以很容易地合并到一个包中。

在您首次创建包时，通常会定 [义包过滤器](#creating-a-new-package)，但以后也可以编辑这些过滤器（之后应重建包）。

### 打包屏幕截图 {#package-screenshots}

您可以将屏幕截图附加到包中，以直观地呈现内容的外观；例如，通过提供新功能的截屏。

### 包图标 {#package-icons}

您还可以向包附加一个图标，以提供包中包含内容的快速参考可视表示形式。 然后，该列表会显示在包列表中，并可帮助您轻松标识包或包类。

由于包中可以包含图标，因此以下约定用于正式包：

>[!NOTE]
>
>要避免混淆，请为包使用描述性图标，而不要使用其中一个官方图标。

正式修补程序包：

![](do-not-localize/chlimage_1-28.png)

正式AEM安装或扩展包：

正式功能包：

![](do-not-localize/chlimage_1-29.png)

## 包管理器 {#package-manager}

包管理器管理本地AEM安装上的包。 在分配了必 [要的权限后](#permissions-needed-for-using-the-package-manager) ，您可以使用包管理器执行各种操作，包括配置、构建、下载和安装包。 要配置的关键元素包括：

* [包设置](#package-settings)
* [包过滤器](#package-filters)

### 使用包管理器所需的权限 {#permissions-needed-for-using-the-package-manager}

要授予用户创建、修改、上传和安装包的权利，您必须在以下位置为他们授予相应的权限：

* **/etc/packages** （完全权限不包括删除）
* 包含包内容的节点

有关更 [改权限的说明](/help/sites-administering/security.md#setting-page-permissions) ，请参阅设置权限。

### 创建新包 {#creating-a-new-package}

要创建新包定义，请执行以下操作：

1. 在AEM欢迎屏幕上，单击“ **包** ”(或从“工具”控制台中双击“包” ********)。

1. 然后选择“ **包管理器**”。
1. 单击“ **创建包”**。

   >[!NOTE]
   >
   >如果实例有大量包，则可能存在一个文件夹结构，因此您可以在创建新包之前导航到所需的目标文件夹。

1. 在对话框中：

   ![packagesnew](assets/packagesnew.png)

   输入：

   * **组名称**

      目标用户组（或文件夹）名称。 组旨在帮助您组织包。

      如果组尚不存在，则将为其创建文件夹。 如果将用户组名称留空，它将在主包列表（“主页”>“包”）中创建包。

   * **包名称**

      新包的名称。 选择一个描述性名称，以帮助您（和其他人）轻松识别包的内容。

   * **版本**

      用于指示版本的文本字段。 这将附加到包名称中，以形成zip文件的名称。
   单击 **确定** ，以创建包。

1. AEM会在相应的用户组文件夹中列出新包。

   ![packagesitem](assets/packagesitem.png)

   单击要打开的图标或包名称。

   ![packageitemclicked](assets/packagesitemclicked.png)

   >[!NOTE]
   >
   >您可以在以后的阶段（如果需要）返回此页。

1. 单击 **编辑** ，以编辑 [包设置](#package-settings)。

   在这里，您可以添加信息和／或定义某些设置；例如，这包括描述、图 [标](#package-icons)、相关错误和添加提供程序详细信息。

   编辑 **完设置** 后，单击“确定”。

1. 根据 **[需要将截屏](#package-screenshots)**添加到包中。 创建包时有一个实例可用，如果需要，可使用Sidekick的包屏幕截图添&#x200B;**加更多**。

   在“截屏”区域中双击图像组件，添加图像，然 **后单击** “确定”，即可添加实际 **图像**。

1. 定义包 **[过滤器](#package-filters)**，方法是从Sidekick中拖动&#x200B;**过滤器定义的实例**，然后双击打开进行编辑：

   ![包过滤器](assets/packagesfilter.png)

   指定：

   * **根路径**&#x200B;要打包的内容；这可以是子树的根。
   * **规则**&#x200B;规则是可选的；对于简单的包定义，无需指定包含或排除规则。

      如果需要，您可以定义“包 [**含&#x200B;**”或“排**&#x200B;除&#x200B;**”规则](#package-filters)，以准确定义包内容。

      使用 **+符号添加规则** ，或使用 **-符号删除规则** 。 规则会根据其顺序应用，以便使用“向上”和“向下”按 **钮** ，根据需 **要定位** 。
   然后，单 **击确定** ，以保存过滤器。

   >[!NOTE]
   >
   >您可以根据需要使用任意数量的过滤器定义，但必须小心确保它们不会发生冲突。 使用 **预览** ，确认包内容的内容。

1. 要确认包将包含的内容，您可以使用“预 **览”**。 此操作将执行构建过程的练习，并列出实际构建包时将添加到包的所有内容。
1. 您现在可以 [构建](#building-a-package) 包。

   >[!NOTE]
   >
   >此时构建包并非强制性的，它可以在以后的时间点完成。

### 构建包 {#building-a-package}

通常，在创建包定义的同时 [构建包](#creating-a-new-package)，但您可以在以后的时间点返回构建或重建包。 如果存储库中的内容已更改，则此功能可能很有用。

>[!NOTE]
>
>在构建包之前，预览包的内容可能很有用。 要执行此操作，请单击“ **预览**”。

1. 从“包管理器”中打 **开包定义** （单击包图标或名称）。

1. 单击“ **构建**”。 对话框会要求您确认是否确实要构建包。

   >[!NOTE]
   >
   >当您重新构建包时，当包内容将被覆盖时，这尤其重要。

1. 单击&#x200B;**确定**。AEM将构建包，并列出添加到包的所有内容。 完成后，AEM会显示确认已构建包，并且（关闭对话框时）会更新包列表信息。

### 重新打包包 {#rewrapping-a-package}

构建包后，可以根据需要重新打包。

重新打包会更改包信息- *而不* 更改包内容。 包信息是缩览图、说明等，换言之，您可以使用“包设置”对话框编辑的所有内容 **(要打开此选项，请单击“编** 辑 ****”)。

重新包装的一个主要用例是为包共享准备包。 例如，您可能拥有一个现有包，并决定与他人共享它。 要添加缩略图并添加说明。 您不必使用其所有功能重新创建整个包（可能需要一些时间，并承担包不再与原始包相同的风险），而是可以重新包装它，只需添加缩略图和说明。

1. 从“包管理器”中打 **开包定义** （单击包图标或名称）。

1. 单击 **编辑** ，然后根据需 **[要更新包设置](#package-settings)**。 单击&#x200B;**确定**进行保存。

1. 单击 **重新绕排**，将显示一个对话框要求确认。

### 查看和编辑包信息 {#viewing-and-editing-package-information}

要查看或编辑有关包定义的信息，请执行以下操作：

1. 在包管理器中，导航到要查看的包。
1. 单击要查看的包的包图标。 此操作将打开包页面，其中列出有关包定义的信息：

   ![packagesiteclicked-1](assets/packagesitemclicked-1.png)

   >[!NOTE]
   >
   >您还可以通过此页编辑并对包执行某些操作。
   >
   >可用的按钮取决于包是否已构建。

1. 如果已构建包，请单击“ **内容**”，将打开一个窗口并列出包的整个内容：

### 查看包内容和测试安装 {#viewing-package-contents-and-testing-installation}

构建包后，您可以查看内容：

1. 在包管理器中，导航到要查看的包。
1. 单击要查看的包的包图标。 此操作将打开包页面，其中列出有关包定义的信息。

1. 要查看内容，请单 **击“内容**”，此时将打开一个窗口并列出包的整个内容：

   ![包内容](assets/packgescontents.png)

1. 要执行安装的练习，请单击“测试 **安装”**。 确认操作后，将打开一个窗口并列出结果，就像执行了安装一样：

   ![packestestinstall](assets/packagestestinstall.png)

### 将包下载到文件系统 {#downloading-packages-to-your-file-system}

本节介绍如何使用包管理器将包从AEM下载到文 **件系统**。

>[!NOTE]
>
>有关 [](#package-share) 从公共区域和您公司内部的包共享区域下载修补程序、功能包和包的信息，请参阅包共享。
>
>从包共享中，您可以：
>
>* 将包从包共 [享直接下载到您的本地AEM实例中](#downloading-and-installing-packages-from-package-share)。
   >  下载包后，该包会导入到您的存储库中，之后，您可以使用包管理器将其立即安装到您的本 **地实例上**。 这些包包括修补程序和其他共享包。
   >
   >
* 将包从包共 [享下载到文件系统](#downloading-packages-to-your-file-system-from-package-share)。
>



1. 在AEM欢迎屏幕上，单击“包” ****，然后选择“ **包管理器”**。
1. 导航到要下载的包。

   ![包下载](assets/packagesdownload.png)

1. 单击要下载的包的zip文件名称（带下划线）所形成的链接；例如 `export-for-offline.zip`,

   AEM将包下载到您的计算机（使用标准浏览器下载对话框）。

### 从文件系统上传包 {#uploading-packages-from-your-file-system}

包上传允许您将包从文件系统上传到AEM包管理器。

>[!NOTE]
>
>请参 [阅将包上传到公司内部包共享](#uploading-packages-to-the-company-internal-package-share) ，以将包上传到公司的包共享的专用区域。

要上传包，请执行以下操作：

1. 导航到包 **管理器**。 然后，转到要将包上传到的组文件夹。

   ![包上载按钮](assets/packagesuploadbutton.png)

1. 单击“ **上传包”**。

   ![packagesuploadalog](assets/packagesuploaddialog.png)

   * **文件**

      **您可以直接键入文件名或使用“浏**&#x200B;览……”对话框，从本地文件系统中选择所需的包(选择后，单击“ **确定**”)。

   * **强制上传**

      如果具有此名称的包已存在，则可以单击它以强制上传（并覆盖现有包）。
   单击 **确定** ，以便上传新包并列在“包管理器”列表中。

   >[!NOTE]
   >
   >要使内容可用于AEM，请务必安 [装该包](#installing-packages)。

### 验证包 {#validating-packages}

在安装包之前，您可能希望验证其内容。 由于包可以修改ACL下的叠加文 `/apps` 件和／或添加、修改和删除ACL，因此在安装前验证这些更改通常很有用。

#### 验证选项 {#validation-options}

验证机制可以检查包的以下特性：

* OSGi包导入
* 叠加
* ACL

这些选项详见下文。

* **验证 OSGi 包的导入情况**

   **检查内容**

   此验证检查所有JAR文件（OSGi捆绑包）的包，提取其 `manifest.xml` （其中包含所述OSGi捆绑包所依赖的版本依赖关系），并验证AEM实例将所述捆绑包导出为正确版本。

   **报告方式**

   AEM实例无法满足的任何版本化依赖关系列在包管理 **器的活动日志** 中。

   **错误状态**

   如果依赖关系不满足要求，则包中包含这些依赖关系的OSGi包将不启动。 这会导致应用程序部署中断，因为依赖未启动的OSGi捆绑的任何组件都将无法正常工作。

   **错误解决**

   要解决由于未满足要求的OSGi捆绑包导致的错误，需要调整捆绑包中具有未满足要求的导入的依赖关系版本。

* **验证覆盖**

   **检查内容**

   此验证确定所安装的包是否包含已覆盖在目标AEM实例中的文件。

   例如，给定位于的现有叠加 `/apps/sling/servlet/errorhandler/404.jsp`的包，它包含 `/libs/sling/servlet/errorhandler/404.jsp`，以便更改位于的现有文件 `/libs/sling/servlet/errorhandler/404.jsp`。

   **报告方式**

   包管理器的活动日志中对 **任何此类叠加** 进行了说明。

   **错误状态**

   错误状态表示包尝试部署已覆盖的文件，因此包中的更改将被叠加覆盖（因此“隐藏”），而不会生效。

   **错误解决**

   要解决此问题，中叠加文件的维护人员必须在中查看对叠加文件所做的更改，并根据需要将更改合并到叠加( `/apps``/libs``/apps`)中，然后重新部署叠加文件。

   >[!NOTE]
   >
   >请注意，如果叠加文件中正确并入了叠加内容，则验证机制无法协调。 因此，即使进行了必要的更改，此验证仍将继续报告冲突。

* **验证 ACL**

   **检查内容**

   此验证会检查添加的权限、将如何处理这些权限（合并／替换）以及当前权限是否受到影响。

   **报告方式**

   包管理器的活动日 **志中介绍了** 这些权限。

   **错误状态**

   不能提供显式错误。 验证仅指示安装包后是添加还是影响任何新的ACL权限。

   **错误解决**

   使用验证提供的信息，可以在CRXDE中查看受影响的节点，并可以根据需要在包中调整ACL。

   >[!CAUTION]
   >
   >作为最佳实践，建议软件包不要影响AEM提供的ACL，因为这可能导致意外的产品行为。

#### 执行验证 {#performing-validation}

可以通过两种不同的方式验证包：

* 通过包管理器UI
* 通过HTTP POST请求（如与cURL）

>[!NOTE]
>
>上传包后但安装包之前，应始终进行验证。

**通过包管理器进行包验证**

1. 打开包管理器，网址为 `https://<server>:<port>/crx/packmgr`
1. 在列表中选择包，然后从标题中选 **择** “更多”下拉列表，然后从下 **拉菜单中选择“验证** ”。

   >[!NOTE]
   >
   >这应在上传内容包之后，但在安装包之前完成。

1. 在随后出现的模态对话框中，使用复选框选择验证类型，然后单击验证以开始验 **证**。 或者，单击 **取消**。

1. 然后运行所选的验证。 结果显示在包管理器的活动日志中。

**通过HTTP POST请求进行包验证**

POST请求采用以下形式。

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

>[!NOTE]
>
>该参 `type` 数可以是以逗号分隔的无序列表，包括：
>
>* `osgiPackageImports`
>* `overlays`
>* `acls`
>
>
如果未传 `type` 递，则 `osgiPackageImports` 默认值为。

以下是使用cURL执行包验证的示例。

1. 如果使用cURL，则执行与以下内容类似的语句：

   ```shell
   curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
   ```

1. 将运行所请求的验证，并将响应作为JSON对象发送回。

>[!NOTE]
>
>对验证HTTP POST请求的响应将是一个JSON对象，其验证结果为。

### 安装包 {#installing-packages}

上传包后，您需要安装内容。 要安装包内容并使其正常工作，它必须同时满足以下两个条件：

* 加载到AEM(从您的 [文件系统上载](#uploading-packages-from-your-file-system) , [或从包共享下载](#downloading-and-installing-packages-from-package-share))

* 已安装

>[!CAUTION]
>
>安装包可覆盖或删除现有内容。 仅在您确定不删除或覆盖您需要的内容时上传包。
>
>要查看包的内容或影响，您可以：
>
>* 在不修改任何内容的情况下，对包执行测试安装：
   >  打开包（单击包图标或名称），然后单击“ **测试安装”**。
   >
   >
* 请参阅包内容列表：
   >  打开包，然后单击“ **内容”**。
>



>[!NOTE]
>
>在安装包之前，会立即创建一个快照包以包含将被覆盖的内容。
>
>卸载包时，将重新安装此快照。

>[!CAUTION]
>
>如果要安装数字资产，您必须：
>
>* 首先，取消激活WorkflowLauncher。
   >  使用OSGi控制台的“组件”菜单选项可取消激活 `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl`。
   >
   >
* 接下来，安装完成后，重新激活WorkflowLauncher。
>
>
取消激活WorkflowLauncher可确保资产导入程序框架在安装时不会（无意中）操纵资产。

1. 在“包管理器”中，导航到要安装的包。

   “ **安装** ”按钮显示在尚未安装的包的一侧。

   >[!NOTE]
   >
   >或者，您也可以通过单击包的图标打开包，以访问该包的“安 **装** ”按钮。

1. 单击 **“安装** ”以开始安装。 对话框将请求确认并列出所做的所有更改。 完成后，单击对 **话框上的** “关闭”。

   安装包 **后** ，包旁边将显示“已安装”字样。

### 基于文件系统的上传和安装 {#file-system-based-upload-and-installation}

有一种替代方法可将包上载和安装到实例。 在文件系统中，您的jar和 `crx-quicksart` 文件旁边有一个文 `license.properties` 件夹。 您需要创建一个名为“”的 `install` 文件夹 `crx-quickstart`。 然后您会有这样的功能： `<aem_home>/crx-quickstart/install`

在此安装文件夹中，您可以直接添加包。 它们将自动上传并安装在您的实例上。 完成后，您可以在包管理器中查看包。

如果实例正在运行，则向文件夹添加包 `install` 将直接启动上传和实例上的安装。 如果实例未运行，您放入文件夹的包将 `install` 在启动时按字母顺序安装。

>[!NOTE]
>
>您还可以在首次启动实例之前执行此操作。 为此，您需要手动创建文 `crx-quickstart` 件夹，在其下面创 `install` 建文件夹，然后将包放在那里。 然后，当您首次启动实例时，将按字母顺序安装这些包。

### 卸载包 {#uninstalling-packages}

AEM允许您卸载包。 此操作会还原受到在包安装之前立即创建的快照影响的存储库内容。

>[!NOTE]
>
>安装后，将创建一个包含将被覆盖的内容的快照包。
>
>卸载包时，将重新安装此包。

1. 在“包管理器”中，导航到要卸载的包。
1. 单击要卸载的包的包图标。
1. 单击 **卸载** ，以从存储库中删除此包的内容。 对话框将请求确认并列出所做的所有更改。 完成后，单击对 **话框上的** “关闭”。

### 删除包 {#deleting-packages}

要从“包管理器”列表中删除包，请执行以下操作：

>[!NOTE]
>
>不会删除包中已安装的文件/ **节点** 。

1. 在“工 **具** ”控制台中，展开“包” **文件夹** ，以在右侧窗格中显示包。

1. 单击要删除的包，以突出显示它，然后：

   * 单击工 **具栏菜单** 中的“删除”。
   * 右键单击并选择“删 **除”**。
   ![包删除](assets/packagesdelete.png)

1. AEM会要求您确认是否要删除包。 Click **OK** to confirm the deletion.

>[!CAUTION]
>
>如果此包已安装，则不会删 *除***已安装** 的内容。

### 复制包 {#replicating-packages}

复制包的内容以将其安装到发布实例：

1. 在包管 **理器中**，导航到要复制的包。

1. 单击要复制的包的图标或名称以展开它。
1. 在工具 **栏的** “更多”下拉菜单中，选择“复 **制”**。

## 包共享 {#package-share}

包共享是公开提供的用于共享内容包的中央服务器。

通过包共享，您可以下载这些包，其中可包括正式的修补程序、功能集、更新或其他用户生成的示例内容。

您还可以在公司内上传和共享包。

### 访问包共享 {#access-to-package-share}

对包共享没有匿名访问权；即，只允许注册用户查看、下载和上传包。

我们的合作伙伴和客户可以访问包共享。 必须提交注册详细信息才能分配访问权限。

要获取包共享，请执行以下操作：

* 使用“ [登录”页面](#signing-in-to-package-share)
* 首次使用登录页面时，您需要：

   * [注册Adobe ID](#registering-for-package-share) ，和／或验 [证您的现有Adobe ID](#validating-your-adobe-id)
   * 以便创建 [包共享帐户](#package-share-account) 。

>[!NOTE]
>
>任何尚未分配给客户的包共享用户都必须通过单击包共享登录旁的“加入”来加入社区以查看这些资源。 ****

#### 登录到包共享 {#signing-in-to-package-share}

1. 在AEM欢迎屏幕上，单击“工 **具”**。
1. 然后选择 **包共享**。 您必须执行以下任一操作：

   * 使用您的Adobe ID登录
   * [创建Adobe ID](#registering-for-package-share)
   >[!NOTE]
   >
   >首次使用Adobe ID登录时，必须完成对电子 [邮件地址的验证](#validating-your-adobe-id)。

   >[!NOTE]
   >
   >如果您忘记密码，请使用“帮 [助页面](https://enterprise-dev.adobe.com/content/edev/en/registration/account.html) ”链接（也位于登录对话框中）。

#### 验证您的Adobe ID {#validating-your-adobe-id}

首次使用Adobe ID登录包共享时，将验证您的电子邮件地址。

1. 您将收到一封包含链接的电子邮件。
1. 您需要单击此链接。
1. 将打开网页。

   打开此网页的操作将作为验证。

1. 登录将继续。

1. 您将收到一封包含链接的电子邮件。
1. 您需要单击此链接。
1. 将打开网页。 打开此网页的操作将作为验证。
1. 登录将继续。

#### 注册包共享 {#registering-for-package-share}

如果您需要访问包共享，则需要注册Adobe ID:

* “包 [共享”登录页面提供了用于注册Adobe ID的链接](#signing-in-to-package-share) 。
* 您可以从某些Adobe桌面软件注册Adobe ID。
* 或者，也可以在 [Adobe登录页面上联机注册](https://www.adobe.com/cfusion/membership/index.cfm?nf=1&nl=1)。

可通过提供以下内容创建Adobe ID:

* 您的电子邮件地址
* 您选择的密码
* 您的姓名和居住地等其他信息

#### 包共享帐户 {#package-share-account}

在以下步骤之前，将检查您的应用程序的有效性：

* 您的用户帐户是使用所需／允许的权限创建的。
* 您的帐户已添加到您公司的组中。

>[!NOTE]
>
>其中一个合作伙伴公司的用户也可以是其客户组的成员。

#### 网络注意事项 {#network-considerations}

**IPv6**

在尝试从纯IPv6环境访问包共享时，您可能会遇到问题。

这是因为包共享是服务器上托管的服务，这意味着您的连接是通过Internet上的各种网络建立的。 不能保证所有连接网络都支持IPv6;如果没有，连接可能失败。

要避免此问题，您可以从IPv4网络访问包共享，下载包，然后将其上传到IPv6环境。

**HTTP代理**

如果您的公司运行需要身份验证的http代理，则包共享当前不可用。

包共享仅在AEM服务器无需身份验证即可访问Internet时可用。 要为使用http客户端（包括包共享）的所有服务配置代理，请使用Day Commons HTTP Client 3.1包的 [OSGi配置](/help/sites-deploying/osgi-configuration-settings.md)。

### 内部包共享 {#inside-package-share}

在包共享中，包排列在树子树中：

* Adobe提供的Adobe包。
* 由其他公司提供并由Adobe公开的共享包。
* 您的公司包是私有的。

![chlimage_1-110](assets/chlimage_1-110.png)

### 搜索和筛选包 {#searching-and-filtering-packages}

“包共享”提供了一个搜索栏，可用于搜索特定的关键字或／和标记。 关键字和标记都支持多个值。

* 要搜索多个关键字，您必须按空格分隔每个关键字。
* 要搜索多个标记，您必须在包树中选择每个标记。

您还可以将过滤器摘要栏右侧的条件运算符从OR更改为AND。

### 从包共享下载和安装包 {#downloading-and-installing-packages-from-package-share}

要从包共享下载包并将其安装到本地实例上，从AEM实例访问包共享更简单。 这将下载包并立即在包管理器中注册它，从中可以安装它。

1. 在AEM欢迎屏幕中，单击工 **具**，然后选择 **包共享** ，以打开包共享页。
1. 使用帐户详细信息，登录“包共享”。 此时将显示登录页，其中列出了Adobe文件夹、共享文件夹以及特定于您公司的文件夹。

   >[!NOTE]
   >
   >在开始从“包共享”下载包之前，请确保您具有所需 [的访问权](#access-to-package-share)。

1. 导航到要下载的包，然后单击“下 **载”**。

1. 返回或导航到AEM实 **例上的包管理器** 。 然后导航到刚下载的包。

   >[!NOTE]
   >
   >要查找您下载的包，请按照与包共享中相同的路径操作。 例如，如果您从“包共享”中的以下路径下载了包：
   >
   >**“包** ”>“ **公共** ”>“修 **补程序”**
   然后，在本地实例的“包管理器”中，该包也将显示在：
   **“包** ”>“ **公共** ”>“修 **补程序”**

1. 单击 **安装** ，将包安装到本地AEM安装中。

   >[!NOTE]
   如果实例上已安装该包，则该包旁边将显示“已 **安装** ”指示符，而不是“安装” **按钮** 。

   >[!CAUTION]
   安装包可覆盖存储库中的现有内容。 因此，我们建议您先执行 **测试安装** 。 这允许您检查包中包含的内容是否与您的现有内容冲突。

### 从包共享将包下载到文件系统 {#downloading-packages-to-your-file-system-from-package-share}

[下载和安装](#downloading-and-installing-packages-from-package-share) ，非常方便，但如果需要，您还可以下载包并将其保存到本地文件系统：

1. 在“包共享”中，单击包图标或名称。
1. Click the **Assets** tab.
1. 单击 **下载到磁盘**。

### 上传包 {#uploading-a-package}

通过包共享，您可以将包上传到公司内部的包共享区域。 这样，它们便可在您的公司内共享。

这些包不 *适用于* 常规AEM社区，但适用于在您的公司注册的所有用户。

要上传包，请执行以下操作：

>[!CAUTION]
要将包上传到包共享，您首先必须在本地包管理器上创建一个以您的公司命名的组文件夹。 例如，geometrixx。 要上传以进行共享的所有包都必须放置在此用户组文件夹中。
无法共享“包管理器”主列表中或其他文件夹中的包。

1. 打开包 **管理器** ，然后导航到要上传的包。

1. 单击包图标以将其打开。
1. 单击 **共享** ，打开将包上传到包共享的对话框。
1. 如果尚未登录到包共享，则需要输入登录凭据。

   登录后，AEM将显示有关要上传的包的详细信息：

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. 单击 **共享** ，将包上传到您公司的内部包共享。

   AEM显示状态并指示包何时完成上传，然后您可以单击 **x** （右上角）退出“共享包” **窗口** 。

1. 上传完成后，您可以导航到公司的内部文件夹以查看刚才共享的包。

>[!NOTE]
要修改包共享上可用的包，您需要下载它，重新构建它，然后再次将其上传到包共享。

### 删除包 {#deleting-a-package}

您只能通过以下步骤删除上传的包：

1. 在公司树中，检查包含该包的包组。
1. 单击包。
1. 单击“删除”按钮。

   ![chlimage_1-18](do-not-localize/chlimage_1-30.png)

1. 单击 **删除** ，确认您要删除包。

### 使包成为半私有包 {#making-packages-semi-private}

您可以在组织之外共享包，但不能公开共享。 这些方案将被视为半私有的。 要共享这些半私有包，您需要Adobe支持部门的一些帮助。 为此，请向Adobe支持部门打开一张票，请求在您的组织之外提供一个包。 他们将要求您提供您要授予对包访问权限的Adobe ID列表。

## 软件分发（测试版） {#software-distribution-beta}

[Software Distribution](https://downloads.experiencecloud.adobe.com) 是新的用户界面，旨在简化AEM包的搜索和下载。 它当前处于测试状态，并且仅可以作为云服务客户和Adobe员工访问Adobe Managed Services和AEM。

>[!NOTE]
* [包共享](#package-share) (Package Share)将一直运行，直到所有客户都可以访问软件分发。
* 所有软件包都可从“包共享”和“软件分发”中获得。


>[!CAUTION]
目前，AEM包管理器不可用于软件分发，您将包下载到本地磁盘。

