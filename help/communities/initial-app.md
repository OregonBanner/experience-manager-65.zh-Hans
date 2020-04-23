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
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# 初始沙箱应用程序 {#initial-sandbox-application}

在本节中，您将创建以下内容：

* 用 **[](#createthepagetemplate)**于在示例网站中创建内容页面的模板。
* 用 **[于呈现网站页面的组件](#create-the-template-s-rendering-component)**和脚本。

## 创建内容模板 {#create-the-content-template}

模板可定义新页面的默认内容。 复杂网站可能使用多个模板在站点中创建不同类型的页面。 此外，模板集可以成为用于将更改转出到服务器群集的蓝图。

在此练习中，所有页面都基于一个简单的模板。

1. 在CRXDE Lite的资源管理器窗格中：

   * 选择 `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL “创建]** ”>“ **[!UICONTROL 创建模板”]**

1. 在“创建模板”对话框中，键入以下值，然后单击“下 **[!UICONTROL 一步”]**:

   * 标签: `playpage`
   * 标题: `An SCF Sandbox Play Template`
   * 描述: `An SCF Sandbox template for play pages`
   * 资源类型: `an-scf-sandbox/components/playpage`
   * 排名：&lt;leave as default>
   标签用于节点名称。

   资源类型将作为属 `playpage`性显示在jcr:content节点上 `sling:resourceType`。 它标识在浏览器请求时呈现内容的组件（资源）。

   在这种情况下，使用模板创建的所 `playpage` 有页面都由组件呈 `an-scf-sandbox/components/playpage` 现。 根据惯例，组件的路径是相对的，允许Sling首先在文件夹中搜索资源，如果找不到， `/apps` 则在文件夹中搜索该资 `/libs` 源。

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. 如果使用复制／粘贴，请确保“资源类型”值没有前导或尾部空格。

   单击&#x200B;**[!UICONTROL 下一步]**。

1. “允许的路径”指使用此模板的页面的路径，以便该模板列在“新建页面”对 **[!UICONTROL 话框中]** 。

   要添加路径，请单击加号按 `+` 钮并 `/content(/.&ast;)?` 在显示的文本框中键入。 如果使用复制／粘贴，请确保没有前导或尾部空格。

   注意：允许的路径属性的值是常规 *表达式。* 具有与表达式匹配的路径的内容页面可以使用模板。 在这种情况下，常规表达式与 **/content文件夹的路径及其所有子页面相匹配** 。

   当作者在下面创建页面 `/content`时，标 `playpage` 题为“SCF沙箱页面模板”的模板将显示在可用模板的列表中以供使用。

   从模板创建根页面后，可以通过修改属性将根路径包含在常规表达式(即，

   `/content/an-scf-sandbox(/.&ast;)?`

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   在“允 **[!UICONTROL 许的父项]** ”面板中 **[!UICONTROL 单击“下一步]** ”。

   在“允 **[!UICONTROL 许的子项]** ”面板中 **[!UICONTROL 单击“下一步]** ”。

   单击&#x200B;**[!UICONTROL 确定]**。

1. 单击“确定”并完成模板的创建后，您会注意到新模板的“属性”选项卡值的角中显示了红色的三 `playpage` 角形。 这些红色三角形指示尚未保存的编辑。

   单击 **[!UICONTROL 全部保存]** ，将新模板保存到存储库。

   ![chlimage_1-77](assets/chlimage_1-77.png)

### 创建模板的渲染组件 {#create-the-template-s-rendering-component}

创建定 *义内容的组件* ，并呈现基于播放页面模板创建的 [任何页面](#createthepagetemplate)。

1. 在CRXDE Lite中，右键单击并单 **`/apps/an-scf-sandbox/components`** 击创建 **[!UICONTROL >组件]**。
1. 通过将节点的名称（标签）设置为 *播放页*，组件的路径为

   `/apps/an-scf-sandbox/components/playpage`

   它与播放页模板的资源类型(可选地减去路径的 **`/apps/`** 初始部分)相对应。

   在创建 **[!UICONTROL 组件对话框中]** ，键入以下属性值：

   * 标签：播 **放页**
   * 标题：SCF **沙箱播放组件**
   * 说明：这 **是为SCF沙箱页面呈现内容的组件。**
   * 超级类型： *&lt;留空>*
   * 组:
   ![chlimage_1-78](assets/chlimage_1-78.png)

1. 单击 **[!UICONTROL “下一步]** ”，直 **[!UICONTROL 到显示对话框的“允许的子项]** ”面板：

   * Click **[!UICONTROL OK]**
   * 单击“ **[!UICONTROL 全部保存”]**

1. 验证组件的路径与模板的resourceType是否匹配。

   >[!CAUTION]
   >
   >播放页面组件的路径与播放页面模板的sling:resourceType属性之间的对应关系对于网站的正确运行至关重要。

   ![chlimage_1-79](assets/chlimage_1-79.png)