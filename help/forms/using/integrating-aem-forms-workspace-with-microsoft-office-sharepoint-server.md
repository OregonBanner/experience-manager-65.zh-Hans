---
title: 将AEM表单工作区与Microsoft Office SharePoint Server集成
description: 您可以将AEM表单工作区与Microsoft Office SharePoint Server集成。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
exl-id: d080932f-d5fb-482d-9329-62da5df10362
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 将AEM表单工作区与Microsoft Office SharePoint Server集成{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**— 要求**

**必备知识**
在将AEM Forms工作区添加到SharePoint服务器之前，您必须拥有对具有适当权限的SharePoint服务器的访问权限，并且必须知道用于访问工作区的URL。 以下步骤假定您熟悉SharePoint Server。 有关SharePoint服务器中Web部件的详细信息，请参阅Windows SharePoint服务中的Web部件。

**用户级别**
开始

您可以在AEM Forms Office SharePoint Server(例如，Microsoft Office SharePoint Server 2007)中将Microsoft Workspace用作Web部件。 用户可以通过使用Web浏览器连接到您的AEM Forms服务器来访问SharePoint工作区，以提供统一的体验。 在本文中，您将了解在Microsoft Office SharePoint Server中将AEM Forms Workspace显示为Web部件的基本步骤。 您可以执行本文中所述的步骤来提供统一的体验，以便连接到SharePoint服务器的用户可以从同一端口访问AEM Forms工作区。

>[!NOTE]
>
>本文中列出的步骤特定于Microsoft SharePoint Server 2007。 您还可以将HTML工作区与其他受支持的Microsoft SharePoint版本一起配置。

## 将AEM Forms工作区与Microsoft Office SharePoint Server 2007集成 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

执行以下步骤以将AEM Forms工作区集成到Web部件中：

1. 在Web浏览器中，导航到SharePoint站点，例如， `https://[myMOSSserver]:44299/default.aspx` 位置 `[myMOSSserver]` 是Sharepoint服务器的名称或IP地址。

   >[!NOTE]
   >
   >44299是SharePoint服务器的默认端口号。 端口号取决于您安装的SharePoint Server。

1. 在网页的右上角，单击 **站点操作** 并选择 **编辑页面**.
1. 单击 **添加Web部件** 按钮。
1. 在“添加Web部件 — Web页”对话框的“其他”下，选择 **页面查看器Web部件** 然后单击 **添加**.
1. 在Page Viewer Web部件框中，单击 **编辑** 并选择 **修改共享的Web部件**.

   >[!NOTE]
   >
   >“页面查看器Web部件”框出现在 **添加Web部件** 在步骤3中单击的按钮，如下图所示（图1）：

   ![Microsoft Office SharePoint服务器中的页面查看器Web部件框。](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   图1. - Microsoft Office SharePoint Server中的“页面查看器Web部件”框。

1. 在“页面查看器”页上，执行以下任务：

   1. 在链接框中，键入AEM Forms工作区的URL，例如 `https://[AEM_forms_Server]:8080/lc/ws` 位置 `[AEM_forms_Server]` 表示AEM Forms Server的IP或名称。
   1. 单击 **外观** 并修改高度、宽度和标题，以便您能够查看整个Workspace用户界面。 例如，可以将高度和宽度分别设置为6英寸和11英寸。
   1. 单击 **测试链接**. 将出现一个新的Web浏览器窗口，其中显示工作区。
   1. （可选）单击 **布局** 并修改Web部件中的工作区布局。
   1. （可选）单击 **高级** 并修改其他设置，如说明以及工作区在Web部件中是否可以最小化或关闭。

      单击&#x200B;**应用**。

1. 单击 **退出编辑模式** 并确认您可以访问工作区。

完成上述步骤后，您的SharePoint网站外观类似于下图（图2）：

![AEM Forms工作区与Microsoft Office SharePoint Server集成](assets/aem-forms-workspace.jpg)

图2 - AEM Forms工作区与Microsoft Office SharePoint Server集成
