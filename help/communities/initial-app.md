---
title: 初始沙箱应用程序
seo-title: 初始沙箱应用程序
description: 创建模板、组件和脚本
seo-description: 创建模板、组件和脚本
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---


# 初始沙箱应用程序{#initial-sandbox-application}

在本节中，您将创建以下内容：

* 将用于在示例网站中创建内容页面的&#x200B;**[template](#createthepagetemplate)**。
* 用于呈现网站页面的&#x200B;**[组件和脚本](#create-the-template-s-rendering-component)**。

## 创建内容模板{#create-the-content-template}

模板可定义新页面的默认内容。 复杂网站可能使用多个模板在站点中创建不同类型的页面。 此外，模板集可以成为用于将更改转出到服务器群集的蓝图。

在此练习中，所有页面都基于一个简单的模板。

1. 在CRXDE Lite的资源管理器窗格中：

   * 选择 `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL 创建]** >创 **[!UICONTROL 建模板]**

1. 在“创建模板”对话框中，键入以下值，然后单击&#x200B;**[!UICONTROL Next]**:

   * 标签: `playpage`
   * 标题: `An SCF Sandbox Play Template`
   * 描述: `An SCF Sandbox template for play pages`
   * 资源类型: `an-scf-sandbox/components/playpage`
   * 排名：&lt;leave as default>

   标签用于节点名称。

   资源类型显示在`playpage`的jcr:content节点上，作为属性`sling:resourceType`。 它标识在浏览器请求时呈现内容的组件（资源）。

   在这种情况下，使用`playpage`模板创建的所有页面都由`an-scf-sandbox/components/playpage`组件呈现。 根据惯例，组件的路径是相对的，允许Sling首先在`/apps`文件夹中搜索资源，如果未找到，则在`/libs`文件夹中搜索。

   ![create-content-template](assets/create-content-template-1.png)

1. 如果使用复制／粘贴，请确保“资源类型”值没有前导或尾部空格。

   单击&#x200B;**[!UICONTROL 下一步]**。

1. “允许的路径”指使用此模板的页面的路径，因此该模板会列在&#x200B;**[!UICONTROL 新建页面]**&#x200B;对话框中。

   要添加路径，请单击加号按钮`+`，然后在显示的文本框中键入`/content(/.&ast;)?`。 如果使用复制／粘贴，请确保没有前导或尾部空格。

   注意：允许路径属性的值为&#x200B;*常规表达式*。 具有与表达式匹配的路径的内容页面可以使用模板。 在这种情况下，常规表达式符与&#x200B;**/content**&#x200B;文件夹及其所有子页面的路径匹配。

   当作者在`/content`下创建页面时，标题为“SCF沙箱页面模板”的`playpage`模板将显示在可用模板的列表中。

   从模板创建根页面后，可以通过修改属性将根路径包含在常规表达式(即，

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   单击&#x200B;**[!UICONTROL 允许的父项]**&#x200B;面板中的&#x200B;**[!UICONTROL 下一步]**。

   单击&#x200B;**[!UICONTROL 允许的子项]**&#x200B;面板中的&#x200B;**[!UICONTROL 下一步]**。

   单击&#x200B;**[!UICONTROL 确定]**。

1. 单击“确定”并完成模板的创建后，您会注意到新`playpage`模板的“属性”选项卡值的角中显示了红色三角形。 这些红色三角形指示尚未保存的编辑。

   单击&#x200B;**[!UICONTROL 全部保存]**&#x200B;将新模板保存到存储库。

   ![verify-content-template](assets/verify-content-template.png)

### 创建模板的渲染组件{#create-the-template-s-rendering-component}

创建定义内容并呈现基于[playpage template](#createthepagetemplate)创建的任何页面的&#x200B;*组件*。

1. 在CRXDE Lite中，右键单击&#x200B;**`/apps/an-scf-sandbox/components`**&#x200B;并单击&#x200B;**[!UICONTROL 创建>组件]**。
1. 通过将节点的名称(Label)设置为&#x200B;*playpage*，组件的路径为

   `/apps/an-scf-sandbox/components/playpage`

   它与播放页模板的资源类型（可选地减去路径的初始&#x200B;**`/apps/`**&#x200B;部分）相对应。

   在&#x200B;**[!UICONTROL 创建组件]**&#x200B;对话框中，键入以下属性值：

   * 标签：**playpage**
   * 标题：**SCF沙箱播放组件**
   * 描述：**这是为SCF沙箱页面呈现内容的组件。**
   * 超级类型：*&lt;lea blank>*
   * 组：*&lt;lea blank>*

   ![create-template-component](assets/create-template-component.png)

1. 单击&#x200B;**[!UICONTROL Next]**，直到显示对话框的&#x200B;**[!UICONTROL 允许的子项]**&#x200B;面板：

   * 单击&#x200B;**[!UICONTROL 确定]**。
   * 单击&#x200B;**[!UICONTROL 保存全部]**。

1. 验证组件的路径与模板的resourceType是否匹配。

   >[!CAUTION]
   >
   >播放页组件的路径与播放页模板的sling:resourceType属性之间的对应关系对于网站的正确功能至关重要。

   ![verify-template-component](assets/verify-template-component.png)