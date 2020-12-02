---
title: 将AEM表单工作区与Microsoft Office SharePoint Server集成
seo-title: 将AEM表单工作区与Microsoft Office SharePoint Server集成
description: '您可以将AEM表单工作区与Microsoft Office SharePoint Server集成。 '
seo-description: '您可以将AEM表单工作区与Microsoft Office SharePoint Server集成。 '
uuid: 69d51bdf-729f-4eea-8fae-1e2b8aacaae6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8990b422-f4f6-4080-871a-33cdf7ca6455
docset: aem65
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---


# 将AEM表单工作区与Microsoft Office SharePoint Server{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}集成

**-要求**

**必备**
知识在将AEM Forms工作区添加到SharePoint Server之前，您必须具有相应权限访问SharePoint Server，并且必须知道访问Workspace的URL。以下步骤假定您已熟悉SharePoint Server。 有关SharePoint Server中Web部件的详细信息，请参阅Windows SharePoint Services中的Web部件。

**用户级**
别开始

您可以在Microsoft Office SharePoint Server（例如，Microsoft Office SharePoint Server 2007）中将AEM Forms工作区用作Web部件。 用户可使用Web浏览器连接到SharePoint Server，以提供统一的体验，从而访问AEM Forms工作区。 在本文中，您将学习在Microsoft Office SharePoint Server中将AEM Forms工作区显示为Web部件的基本步骤。 您可以执行本文中所述的步骤，以提供统一的体验，以便连接到SharePoint服务器的用户可以从同一端口访问AEM Forms工作区。

>[!NOTE]
>
>本文中列出的步骤是特定的Microsoft SharePoint Server 2007。 您还可以使用其他支持的Microsoft SharePoint版本配置HTML Workspace。

## 将AEM Forms工作区与Microsoft Office SharePoint Server 2007{#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}集成

执行以下步骤将AEM Forms工作区集成到Web部件中：

1. 在Web浏览器中，导航到SharePoint站点，如`https://[myMOSSserver]:44299/default.aspx`，其中`[myMOSSserver]`是Sharepoint服务器的名称或IP地址。

   >[!NOTE]
   >
   >44299是SharePoint服务器的默认端口号。 端口号取决于SharePoint Server的安装。

1. 在网页的右上方，单击&#x200B;**站点操作**&#x200B;并选择&#x200B;**编辑页面**。
1. 单击&#x200B;**添加Web部件**&#x200B;按钮。
1. 在“添加Web部件——网页对话框”的“其他”下，选择&#x200B;**“页面查看器Web部件**”，然后单击&#x200B;**添加**。
1. 在“页面查看器Web部件”框中，单击&#x200B;**edit**&#x200B;并选择&#x200B;**修改共享Web部件**。

   >[!NOTE]
   >
   >“Page Viewer Web Part”（页面查看器Web部件）框出现在&#x200B;**添加Web部件**&#x200B;按钮下，您在步骤3中单击了该按钮，如下图所示（图1）:

   ![Microsoft Office SharePoint服务器中的“页面查看器Web部件”框。](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   图1. - Microsoft Office SharePoint服务器中的“页面查看器Web部件”框。

1. 在“页面查看器”页面上，执行以下任务:

   1. 在“链接”框中，键入AEM FormsWorkspace的URL，如`https://[AEM_forms_Server]:8080/lc/ws`，其中`[AEM_forms_Server]`表示AEM表单服务器的IP或名称。
   1. 单击&#x200B;**外观**&#x200B;并修改高度、宽度和标题，以便您能够看到整个Workspace用户界面。 例如，可将高度和宽度分别设置为6英寸和11英寸。
   1. 单击&#x200B;**测试链接**。 将出现一个新的Web浏览器窗口，其中显示工作区。
   1. （可选）单击&#x200B;**布局**&#x200B;并修改Web部件中工作区的布局。
   1. （可选）单击&#x200B;**高级**&#x200B;并修改其他设置，如说明以及Web部件中的工作区可以最小化还是关闭。

      单击&#x200B;**应用**。

1. 单击&#x200B;**退出编辑模式**&#x200B;并验证是否可以访问工作区。

完成上述步骤后，您的SharePoint站点的外观与下图类似（图2）:

![AEM Forms工作区与Microsoft Office SharePoint Server集成](assets/aem-forms-workspace.jpg)

图2 —— 与Microsoft Office SharePoint Server集成的AEM FormsWorkspace

