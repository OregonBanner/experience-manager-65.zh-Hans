---
title: 将资产导入和导出到AEM Forms
seo-title: 将资产导入和导出到AEM Forms
description: 您可以在和中导入和导出自适应表单和模板，以将其导入AEM实例。 这有助于迁移表单或跨系统移动表单。
seo-description: 您可以在和中导入和导出自适应表单和模板，以将其导入AEM实例。 这有助于迁移表单或跨系统移动表单。
uuid: 937daedd-56f3-4e02-b695-b194b494d9bf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 69210727-dde3-495a-87b7-2e8173e6b664
docset: aem65
role: Admin
exl-id: b5f6a54e-92d1-4631-a1d1-184f37d174b6
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 0%

---

# 将资产导入和导出到AEM Forms{#importing-and-exporting-assets-to-aem-forms}

您可以在不同的AEM Forms实例之间移动表单和相关资产、主题、数据字典、文档片段和字母。 在将系统迁移或表单从暂存服务器移动到生产服务器时需要这种移动。 对于支持通过AEM Forms UI上传和导入的资产，建议导出或导入方式为使用Forms UI。 不建议使用AEM包管理器导出或导入此类资产。

>[!NOTE]
>
>* 在AEM 6.4 Forms中，crx-repository的结构和路径已发生更改。 如果将资产从以前的版本导入AEM 6.4 Forms，并且该表单对旧结构有一些依赖关系，则必须手动导出依赖关系。 有关存储库结构和路径更改的详细信息，请参阅AEM](/help/sites-deploying/repository-restructuring.md)中的[存储库重组。

>



## 下载或上传Forms和文档资产 {#download-or-upload-forms-amp-documents-assets}

AEM Forms用户界面允许您通过将AEM实例中的资产下载为AEM CRX包或二进制文件来导出资产。 然后，您可以将下载的AEM CRX包或二进制文件导入另一个AEM实例。

除自适应表单模板和自适应表单内容策略外，所有资产均支持通过AEM Forms用户界面导出和导入。 因此，在从AEM Forms UI导出自适应表单时，相关的自适应表单模板和内容策略不会像其他相关资产一样自动导出。

对于这些资产类型，您必须使用AEM Package Manager在源AEM服务器上创建CRX包，并将该包安装到目标服务器上。 有关创建和安装包的信息，请参阅[使用包](/help/sites-administering/package-manager.md)。

### 下载Forms和文档资产 {#download-forms-amp-documents-assets}

要下载Forms和文档资产，请执行以下操作：

1. 登录到AEM Forms实例。
1. 点按Experience Manager![ adobeexperiencemanager](assets/adobeexperiencemanager.png)图标>导航![compass](assets/compass.png)图标> Forms > Forms和文档。
1. 选择表单资产，然后点按&#x200B;**下载**&#x200B;图标。
1. 在下载资产中，选择以下选项之一，然后点按&#x200B;**下载**。

   * **下载为CRX包：** 使用选项可从AEM Forms实例下载所有选定资产及相关依赖项并将其移动到另一个实例。它会将所有资产和文件夹下载为crx包。 任何表单资产(包括在AEM中创作的表单（自适应表单、交互式通信和自适应表单片段）、表单集、表单模板、PDF文档和资源（XSD、XFS、图像）均可从AEM Forms UI以包形式下载。
将资产下载为包的好处是，它还会下载选定要下载的资产所使用的资产。 例如，如果您的自适应表单使用表单模板、XSD和图像。 选择此自适应表单并将其下载为包时，下载的包中还包含表单模板、XSD和图像。 与资产关联的所有元数据属性（包括自定义属性）也会下载。

   * **将资产下载为二进制文件：** 使用选项仅下载表单模板(XDP)、PDF forms(PDF)、文档(PDF)和资源（图像、架构、样式表）。您可以使用外部应用程序编辑这些资产。 它将下载包含二进制文件的表单资产（如XSD、XDP、图像、PDF和XDP），作为.zip文件。
您无法下载具有**将资产下载为二进制文件**&#x200B;选项的自适应表单、交互式通信、自适应表单片段、主题和表单集。 要下载这些资产，您应使用&#x200B;**下载为CRX包**&#x200B;选项。

   选定资产将作为存档文件（.zip文件）下载。

   >[!NOTE]
   >
   >AEM包和二进制文件均下载为存档文件（.zip文件）。 不会随资产一起下载资产的模板。 您需要单独导出资产模板。

### 上传Forms和文档资产 {#upload-forms-amp-documents-assets}

要上传Forms和文档资产，请执行以下操作：

>[!VIDEO](https://vimeo.com/)

1. 登录到AEM Forms实例。
1. 点按Experience Manager![ adobeexperiencemanager](assets/adobeexperiencemanager.png)图标>导航![compass](assets/compass.png)图标> Forms> Forms和文档。
1. 点按&#x200B;**创建** >**文件上传**。 将显示上载表单或包对话框。
1. 在对话框中，浏览并选择要导入的包或存档。 您还可以选择PDF文档、XSD、图像、样式表和XDP表单。 点按&#x200B;**打开**。 您选择的文件夹或文件名不得包含任何特殊字符。

   在对话框中，验证所上传资产的详细信息，然后点按&#x200B;**上传**。

   如果您上传现有的表单资产，则资产会进行更新。

   >[!NOTE]
   >
   >上传资源包不会替换现有文件夹层次结构。 例如，如果您有一个名为“培训”的自适应表单，该表单位于某个服务器上的/content/dam/formsanddocuments位置。 您下载自适应表单，并将表单上载到其他服务器。 第二台服务器在同一位置/content/dam/formsanddocuments还有一个名为“Training”的文件夹。 上传失败。

## 下载或上传主题 {#downloading-or-uploading-a-theme}

通过AEM Forms，您可以创建、下载或上传主题。 与其他资产（如表单、文档和信件）一样，创建主题。 您可以创建主题、下载它，然后将其上传到单独的实例以重复使用。 有关主题的更多信息，请参阅AEM Forms](../../forms/using/themes.md)中的[主题。

### 下载主题 {#downloading-a-theme}

您可以在AEM Forms中导出可在其他项目或实例中使用的主题。 AEM允许您以zip文件的形式下载主题，您可以在实例上传该主题。

要下载主题，请执行以下操作：

1. 登录到AEM Forms实例。
1. 点按Experience Manager![adobeexperiencemanager](assets/adobeexperiencemanager.png)图标>导航![compass](assets/compass.png)图标> Forms>主题。
1. 选择主题，然后点按&#x200B;**Download**。 主题将下载为存档文件（.zip文件）。

### 上传主题 {#uploading-a-theme}

您可以在项目中将创建的主题与样式预设结合使用。 您可以通过在您的项目上上传他人创建的主题包来导入这些主题包。

要上传主题，请执行以下操作：

1. 在Experience Manager中，导航到&#x200B;**Forms >主题**。
1. 在“主题”页面中，单击&#x200B;**创建>文件上传**。
1. 在“文件上载”提示中，浏览并选择计算机上的主题包，然后单击&#x200B;**上载**。
已上传的主题可在主题页面中使用。

1. 登录到AEM Forms实例。
1. 点按Experience Manager![adobeexperiencemanager](assets/adobeexperiencemanager.png)图标>导航![compass](assets/compass.png)图标> Forms>主题。
1. 单击&#x200B;**创建** > **文件上传**。 在“文件上载”提示中，浏览并选择计算机上的主题包，然后单击&#x200B;**上载**。 主题已上传。

## 在通信管理中导入和导出资产 {#import-and-export-assets-in-correspondence-management}

要在通信管理的两个不同实施之间共享资产（如数据字典、字母和文档片段），您可以创建和共享.cmp文件。 .cmp文件可以包含一个或多个数据字典、字母、文档片段和表单。

### 导出文档片段、字母和/或数据字典 {#export-document-fragments-letters-and-or-data-dictionaries}

1. 在信件、文档片段或数据字典页面中，点按并选择要导出到单个包的资产，然后点按待下载队列。 这些资产已排列好可供导出。
1. 根据需要，重复上述步骤以添加字母、文档片段和数据字典。
1. 点按&#x200B;**下载**。
1. 通信管理显示“下载资产”对话框，其中包含导出列表中的资产列表。

   ![导出](assets/export.png)

1. 要查看导出的依赖项，请点按“解析”。 或者跳到下一步。 即使不点按“解析”，依赖项仍会导出。
1. 要下载.cmp文件，请点按&#x200B;**确定**。
1. 通信管理会将.cmp文件下载到您的计算机。

   .cmp文件包含导出的资产。 您可以与其他人共享.cmp文件。 其他用户可以将.cmp文件导入其他服务器，以获取新服务器中的所有资产。

### 将所有通信管理资产导出为一个包 {#export-all-the-correspondence-management-assets-as-a-package}

使用此选项可从AEM Forms实例将所有通信管理资产和相关依赖项下载为包。

例如，如果通信管理中的信件使用图像和文本，则下载的包中还包含与信件相关的图像和文本。 与资产关联的所有元数据属性（包括自定义属性）也会下载。 下载包(.cmp)后，您可以[将包导入其他AEM Forms实例](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p)。

要将所有通信管理资产和相关依赖项下载为包，请完成以下步骤：

1. 以表单用户身份登录AEM Forms服务器。
1. 点按全局导航栏中的&#x200B;**Adobe Experience Manager**。
1. 点按工具（![工具](assets/tools.png)），然后点按&#x200B;**Forms**。
1. 点按&#x200B;**导出通信管理资产**。

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   (出现“导出所有通信管理资产”页面，其中显示了有关上次尝试导出过程的信息以及用于下载上次成功导出的资源包的链接。

   ![export-last-run-details](assets/export-last-run-details.png)

1. 点按&#x200B;**导出**，然后在确认消息中，点按&#x200B;**确定**。

   完成批处理后，将更新最后运行的详细信息以及用于下载包的链接。 这包括管理员登录以及批处理是否成功运行或失败等信息。 资产将导出到资源包，此时会显示下载导出的资源包链接。

   >[!NOTE]
   >
   >启动“导出所有资产”流程后，将无法取消该流程。 此外，在导出所有资产操作正在进行中时，请勿创建、删除、修改或发布任何资产，或启动“发布所有资产”流程。a

1. 点按&#x200B;**下载导出的包**&#x200B;链接以下载包文件。

   要将包中的资产添加到通信管理的另一个实例，请[将包导入AEM Forms实例](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p)。

### 将文档片段、信件和/或数据字典导入通信管理 {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

您可以将导出的资产导入.cmp文件。 .cmp文件可以具有一个或多个字母、数据字典、文档片段和从属资产。

>[!NOTE]
>
>在导入旧的通信管理资产以进行迁移时，请使用管理员帐户登录。 有关迁移旧通信管理资产的更多信息，请参阅[将通信管理资产迁移到AEM 6.1 forms](/help/forms/using/migration-utility.md)。

1. 在数据字典、字母或文档片段页面上，点按&#x200B;**创建>文件上传**，然后选择.cmp文件。
1. 通信管理会显示导入资产对话框，其中包含已导入的资产列表。 点按&#x200B;**导入**。

   导入资产后，将更新资产的以下属性，而其他属性则保持不变：

   * 作者：显示将资产导入服务器的用户ID
   * 已修改：将资产导入服务器的时间

   >[!NOTE]
   >
   >为了能够上传XDP（作为cmp文件或其他内容的一部分），您需要成为表单级用户组的一部分。 要获取访问权限，请与管理员联系。

## 导出工作流应用程序 {#export-a-workflow-application}

您可以使用AEM包管理器导出工作流应用程序。 程序如下：

1. 打开AEM Forms包管理器。 包管理器的URL是https://&lt;server>:&lt;port>/crx/packmgr。
1. 单击&#x200B;**[!UICONTROL 创建包]**。 出现&#x200B;**[!UICONTROL 新建包]**&#x200B;对话框。
1. 指定包的名称、版本和组。 单击&#x200B;**[!UICONTROL 确定]**。
1. 单击&#x200B;**[!UICONTROL 编辑]**&#x200B;并打开&#x200B;**[!UICONTROL 过滤器]**&#x200B;选项卡。 单击&#x200B;**[!UICONTROL 添加过滤器]**。 指定工作流应用程序的路径。 例如， /etc/fd/dashboard/startpoints/homemortgage。 单击&#x200B;**[!UICONTROL Add rule]**。

1. 打开&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。在“ACL处理”字段中选择&#x200B;**[!UICONTROL Merge]**&#x200B;或&#x200B;**[!UICONTROL Overwrite]**。 单击&#x200B;**[!UICONTROL 保存]**。
1. 单击&#x200B;**[!UICONTROL Build]**&#x200B;以创建资源包。

   生成包后，您可以下载该包并将其导入到其他服务器。 工作流应用程序将显示在上传包的服务器上。

   >[!NOTE]
   >
   >为了使工作流应用程序正常工作，还导出相应的自适应表单和工作流模型与工作应用程序。

## 文件夹和组织资产 {#folders-and-organizing-assets}

AEM Forms用户界面使用文件夹来排列资产。 这些文件夹用于排列在AEM Forms用户界面中创建的资产。 您可以重命名子文件夹，并存储这些文件夹中的资产和文档。 通过在文件夹中组织文档和资产，可以将文件分组在一起，以便轻松管理。 您可以选择文件夹并选择下载或删除它。

要创建文件夹，请完成以下步骤：

### 创建文件夹 {#create-a-folder}

1. 登录到位于`https://<server>:<port>/aem/forms.html`的AEM Forms用户界面。
1. 导航到要创建文件夹的位置。
1. 点按创建>文件夹。
1. 输入以下详细信息：

   * **标题：** 文件夹的显示名称
   * **名称：** *（必需）* 要在存储库中存储文件夹的节点名称

   >[!NOTE]
   >
   >默认情况下，会从标题中自动填充name字段的值。 名称只能包含字母数字字符，或连字符(-)和下划线(_)特殊字符。 在标题中输入的任何其他特殊字符会自动替换为连字符，系统会提示您确认新名称。 您可以选择继续使用建议的名称，也可以进一步对其进行编辑。

1. 资产列表中的当前位置将显示一个新文件夹，其中包含您定义的标题。

   如果存在具有指定名称的文件夹，则提交会失败，并出现错误。 您可以通过将鼠标悬停在名称字段旁边显示的错误![aem6forms_error_alert](assets/aem6forms_error_alert.png)图标上来查看错误消息。

   您可以点按新创建的文件夹，以转到文件夹内，并在文件夹中创建资产或文件夹。 此外，您还可以选择文件夹并选择将其排入队列进行下载、删除或编辑其名称。

   ![editdeletedownloadolder](assets/editdeletedownloadafolder.png)

### 创建一个或多个资产或信件的副本 {#create-copies-of-one-or-more-assets-or-letters}

您可以使用现有资产和信件快速创建具有相似属性、内容和继承资产的资产和信件。 您可以复制并粘贴数据字典、文档片段和字母。

完成以下步骤以创建资产和信件的副本：

1. 在相关的资产或信件页面中，选择一个或多个资产/信件。 UI会显示复制图标。
1. 点按复制。UI会显示粘贴图标。 您还可以在粘贴之前选择在文件夹中转移/导航。 不同的文件夹可以包含具有相同名称的资产。 有关文件夹的更多信息，请参阅[文件夹和组织资产](#folders-and-organizing-assets)。
1. 点按粘贴。 此时会出现“粘贴”对话框。 系统会自动为资产/信件的新副本生成名称和标题，但您可以编辑资产/信件的标题和名称。

   如果您在同一位置复制和粘贴资产/信件，后缀“ — CopyXX”会添加到资产/信件的现有名称中。 如果复制的资产/信件不存在标题，则自动生成的标题字段将保留为空。

1. 如有需要，请编辑要用其保存资产/信件副本的标题和名称。
1. 点按粘贴。 将创建复制资产的新副本。

## 搜索 {#search-forms}

AEM Forms UI允许您搜索内容。 使用顶部栏，您可以点按搜索&#x200B;**[A]**&#x200B;以搜索内容以查找资产和文档等资源。

在搜索资产时，AEM Forms会显示侧面板。 您还可以点按![assets-browser-content-only](assets/assets-browser-content-only.png) >过滤器&#x200B;**[B]**&#x200B;以调用侧面板。 使用侧面板中的各种过滤器，可以缩小搜索范围。 侧面板还允许您保存搜索。

![search_topbar](assets/search_topbar.png)

**A.搜** 索 **B.过** 滤器

![侧面板 — 过滤器](assets/search_sidepanel.png)

侧面板 — 过滤器

在侧面板中，您可以使用以下内容来缩小搜索结果的范围：

* 搜索目录
* 标记
* 搜索条件；例如修改日期、发布状态、LiveCopy 状态。

侧面板还允许您使用所选名称保存搜索设置。

有关使用搜索、过滤器、保存的搜索和侧面板的更多信息和说明，请参阅[搜索](/help/sites-authoring/search.md)。
