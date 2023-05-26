---
title: 初始沙盒应用程序
seo-title: Initial Sandbox Application
description: 创建模板、组件和脚本
seo-description: Create template, component, and script
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 2%

---

# 初始沙盒应用程序 {#initial-sandbox-application}

在本节中，您将创建以下内容：

* 此 **[模板](#createthepagetemplate)** 该页面将用于创建示例网站中的内容页面。
* 此 **[组件和脚本](#create-the-template-s-rendering-component)** 将用于呈现网站页面的区段。

## 创建内容模板 {#create-the-content-template}

模板定义新页面的默认内容。 复杂的网站可能使用多个模板在站点中创建不同类型的页面。 此外，该模板集可以成为用于将更改转出到服务器集群的蓝图。

在本练习中，所有页面都基于一个简单的模板。

1. 在CRXDE Lite的浏览器窗格中：

   * 选择 `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL 创建]** > **[!UICONTROL 创建模板]**

1. 在创建模板对话框中，键入以下值，然后单击 **[!UICONTROL 下一个]**：

   * 标签: `playpage`
   * 标题: `An SCF Sandbox Play Template`
   * 描述: `An SCF Sandbox template for play pages`
   * 资源类型: `an-scf-sandbox/components/playpage`
   * 排名： &lt;leave as=&quot;&quot; default=&quot;&quot;>

   Label用于节点名称。

   资源类型将显示在 `playpage`的jcr：content节点作为属性 `sling:resourceType`. 它标识在浏览器请求时呈现内容的组件（资源）。

   在本例中，所有使用创建的页面 `playpage` 模板由渲染 `an-scf-sandbox/components/playpage` 组件。 按照惯例，组件的路径是相对路径，允许Sling首先在中搜索资源 `/apps` 文件夹，如果找不到，则在 `/libs` 文件夹。

   ![create-content-template](assets/create-content-template-1.png)

1. 如果使用复制/粘贴，请确保“资源类型”值没有前导或尾随空格。

   单击&#x200B;**[!UICONTROL 下一步]**。

1. “允许的路径”是指使用此模板的页面的路径，这样，模板便会 **[!UICONTROL 新页面]** 对话框。

   要添加路径，请单击加号按钮 `+` 和类型 `/content(/.&ast;)?` 在显示的文本框中。 如果使用复制/粘贴，请确保没有前导或尾随空格。

   注意： allowed path属性的值为 *正则表达式*. 路径与表达式匹配的内容页面可以使用模板。 在这种情况下，正则表达式将匹配 **/content** 文件夹及其所有子页面。

   当作者创建以下页面时 `/content`，则 `playpage` 标题为“SCF沙盒页面模板”的模板显示在要使用的可用模板列表中。

   从模板创建根页面后，可以通过修改属性以在正则表达式中包含根路径(即

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   单击 **[!UICONTROL 下一个]** 在 **[!UICONTROL 允许的父项]** 面板。

   单击 **[!UICONTROL 下一个]** 在 **[!UICONTROL 允许的子项]** 面板。

   单击&#x200B;**[!UICONTROL 确定]**。

1. 单击“确定”并完成模板创建后，您会注意到新模板的“属性”选项卡值的角上显示了红色三角形 `playpage` 模板。 这些红色三角形表示尚未保存的编辑。

   单击 **[!UICONTROL 全部保存]** 以将新模板保存到存储库。

   ![verify-content-template](assets/verify-content-template.png)

### 创建模板的渲染组件 {#create-the-template-s-rendering-component}

创建 *组件* 定义内容并渲染根据 [播放页面模板](#createthepagetemplate).

1. 在CRXDE Lite中，右键单击 **`/apps/an-scf-sandbox/components`** 并单击 **[!UICONTROL 创建>组件]**.
1. 通过将节点名称（标签）设置为 *playpage*，组件的路径为

   `/apps/an-scf-sandbox/components/playpage`

   播放页模板的资源类型（可选）减去初始值 **`/apps/`** 路径的一部分)。

   在 **[!UICONTROL 创建组件]** 对话框中，键入以下属性值：

   * 标签： **playpage**
   * 标题： **SCF沙盒播放组件**
   * 描述： **这是为SCF沙盒页面呈现内容的组件。**
   * 超级类型： *&lt;leave blank=&quot;&quot;>*
   * 组： *&lt;leave blank=&quot;&quot;>*

   ![create-template-component](assets/create-template-component.png)

1. 单击 **[!UICONTROL 下一个]** 直到 **[!UICONTROL 允许的子项]** 此时将显示对话框的面板：

   * 单击&#x200B;**[!UICONTROL 确定]**。
   * 单击 **[!UICONTROL 全部保存]**.

1. 验证组件的路径与模板的resourceType相匹配。

   >[!CAUTION]
   >
   >播放页面组件的路径与播放页面模板的sling：resourceType属性之间的对应关系对于网站的正确运行至关重要。

   ![verify-template-component](assets/verify-template-component.png)
